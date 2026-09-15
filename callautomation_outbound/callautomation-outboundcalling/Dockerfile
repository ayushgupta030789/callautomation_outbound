FROM mcr.microsoft.com/devcontainers/python:3.11

RUN openssl version
# Prevent Python from creating .pyc files
ENV PYTHONDONTWRITEBYTECODE=1

# Send Python output directly to container logs
ENV PYTHONUNBUFFERED=1

# Application directory
WORKDIR /app

# Install Python dependencies
COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

# Copy application code
COPY app.py .

# Copy Flask templates
COPY template ./template

# Application listens on port 8080
EXPOSE 8080

# Start Flask application using Gunicorn
CMD ["gunicorn", "--bind", "0.0.0.0:8080", "--workers", "2", "--log-level", "info", "--access-logfile", "-", "--error-logfile", "-", "--capture-output", "app:app"]
