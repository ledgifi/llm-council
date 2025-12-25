# Backend Dockerfile for LLM Council
FROM python:3.12-slim

# Set environment variables for Python
ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1 \
    PIP_NO_CACHE_DIR=1 \
    PIP_DISABLE_PIP_VERSION_CHECK=1

# Set work directory
WORKDIR /app

# Install uv for faster Python package management
RUN pip install uv

# Copy dependency files
COPY pyproject.toml uv.lock ./

# Install dependencies using uv
RUN uv pip install --system -r pyproject.toml

# Copy backend code
COPY backend/ ./backend/

# Create data directory for conversation storage
RUN mkdir -p data/conversations

# Create non-root user for security
RUN useradd -m -u 1000 council && \
    chown -R council:council /app
USER council

# Expose backend port
EXPOSE 8001

# Run the FastAPI application
CMD ["python", "-m", "backend.main"]
