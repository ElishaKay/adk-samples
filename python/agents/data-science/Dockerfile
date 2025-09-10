FROM python:3.12-slim

# Install system dependencies required for Python shared libraries
RUN apt-get update && apt-get install -y \
    libexpat1 \
    && rm -rf /var/lib/apt/lists/*

# Prevents Python from buffering stdout and stderr
ENV PYTHONUNBUFFERED=1

# Copy from the cache instead of linking since it's a mounted volume
ENV UV_LINK_MODE=copy

WORKDIR /app

# Copy dependency files first for better caching
COPY uv.lock pyproject.toml ./

# Upgrade pip to the latest version and install uv
RUN pip install --no-cache-dir --upgrade pip && \
    pip install --no-cache-dir uv>=0.7.19

# Copy the application code (needed for package building)
COPY . .

# Install project dependencies, sync to uv's lockfile
RUN uv sync --frozen

# Expose the port
EXPOSE 8080

CMD ["uv", "run", "uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8080"]
