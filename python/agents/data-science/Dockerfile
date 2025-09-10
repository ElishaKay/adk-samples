FROM python:3.12-slim

# Install system dependencies required for Python shared libraries
RUN apt-get update && apt-get install -y \
    libexpat1 \
    && rm -rf /var/lib/apt/lists/*

# Prevents Python from buffering stdout and stderr
ENV PYTHONUNBUFFERED=1

WORKDIR /app

# Copy dependency files first for better caching
COPY uv.lock pyproject.toml ./

# Upgrade pip to the latest version and install uv
RUN pip install --no-cache-dir --upgrade pip && \
    pip install --no-cache-dir uv>=0.7.19

# Copy the application code (needed for package building)
COPY . .

# Install project dependencies, sync to uv's lockfile
# Use --no-dev to avoid installing development dependencies in production
# Set UV_SYSTEM_PYTHON to use the system Python instead of creating a venv
ENV UV_SYSTEM_PYTHON=1
RUN uv sync --frozen --no-dev

# Expose the port
EXPOSE 8080

CMD ["uv", "run", "uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8080"]
