# Start with slim Python 3.13 image
FROM python:3.13.10-slim

# Copy uv binary from official uv image (multi-stage build pattern)
COPY --from=ghcr.io/astral-sh/uv:latest /uv /bin/

# Set working directory
WORKDIR /app

# RUN pip install pandas pyarrow

# Copy dependency files first (better layer caching) - for uv
COPY "pyproject.toml" "uv.lock" ".python-version" ./

# Install dependencies from lock file via uv (ensures reproducible builds)
RUN uv sync --locked

# Copy application code
COPY ingest_data.py /app/my_pipeline.py
# COPY pipeline.py /app/my_pipeline.py

ENTRYPOINT ["uv", "run", "python", "my_pipeline.py"]