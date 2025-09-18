FROM python:3.12-slim

# Install uv using pip
RUN pip install uv

WORKDIR /app

# Copy dependency files and install dependencies
COPY pyproject.toml requirements.txt ./
RUN uv pip install --system -r requirements.txt

# Copy the rest of the backend application code
COPY ./app ./app

# Expose the port the app runs on
EXPOSE 8000

# Health check
HEALTHCHECK --interval=30s --timeout=10s --start-period=30s --retries=3 \
    CMD curl -f http://localhost:8000/health || exit 1

# Command to run the application
CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"] 
