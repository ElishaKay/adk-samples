FROM python:3.12-slim

# Install system dependencies required for Python shared libraries
RUN apt-get update && apt-get install -y \
    libexpat1 \
    && rm -rf /var/lib/apt/lists/*

# Prevents Python from buffering stdout and stderr
ENV PYTHONUNBUFFERED=1

WORKDIR /app

# Copy dependency files first for better caching
COPY pyproject.toml ./

# Upgrade pip to the latest version
RUN pip install --no-cache-dir --upgrade pip

# Copy the application code (needed for package building)
COPY . .

# Install project dependencies using pip directly
# Extract dependencies from pyproject.toml and install them
RUN pip install --no-cache-dir \
    python-dotenv>=1.0.1 \
    google-adk>=1.5.0 \
    immutabledict>=4.2.1 \
    sqlglot>=26.10.1 \
    db-dtypes>=1.4.2 \
    regex>=2024.11.6 \
    tabulate>=0.9.0 \
    "google-cloud-aiplatform[adk,agent-engines]>=1.93.0" \
    absl-py>=2.2.2 \
    pydantic>=2.11.3 \
    pandas>=2.3.0 \
    numpy>=2.3.1 \
    pg8000>=1.31.2 \
    uvicorn

# Expose the port
EXPOSE 8080

CMD ["python", "-m", "uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8080"]
