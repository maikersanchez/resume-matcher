FROM python:3.12-slim

# Install system dependencies
RUN apt-get update && apt-get install -y \
    curl \
    && rm -rf /var/lib/apt/lists/*

# Install uv using pip
RUN pip install uv

# Set working directory
WORKDIR /app

# Copy dependency files and install dependencies
COPY pyproject.toml requirements.txt ./
RUN uv pip install --system -r requirements.txt

# Copy the rest of the backend application code
COPY ./app ./app

# Create data directory for SQLite
RUN mkdir -p /app/data

# Set default environment variables (pueden ser sobrescritas)
ENV PYTHONPATH=/app
ENV PYTHONUNBUFFERED=1
ENV PORT=8000
ENV HOST=0.0.0.0

# Variables por defecto para desarrollo (DEBEN ser sobrescritas en producción)
ENV SYNC_DATABASE_URL=sqlite:///./data/resume_matcher.db
ENV ASYNC_DATABASE_URL=sqlite+aiosqlite:///./data/resume_matcher.db
ENV SESSION_SECRET_KEY=development-key-change-in-production

# Expose the port the app runs on
EXPOSE 8000

# Health check
HEALTHCHECK --interval=30s --timeout=10s --start-period=30s --retries=3 \
    CMD curl -f http://localhost:8000/health || exit 1

# Command to run the application
CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]
