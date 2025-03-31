# Stage 1: Build
FROM python:3.9-slim AS builder

WORKDIR /app

# Copy dependencies file and install
COPY . /App 

# run the necessary package
RUN apt-get update && apt-get install -y python3 python3-pip

# Copy application source code
COPY . .

# Stage 2: Runtime
FROM python:3.9-slim

WORKDIR /app

# Add a non-root user for security
RUN addgroup --system appgroup && adduser --system --group appuser
USER appuser

# Copy files from the build stage
COPY --from=builder /app /app

# Expose the application port
EXPOSE 5000

# Run the Flask app
CMD ["python", "app.py"]