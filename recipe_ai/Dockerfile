# Dockerfile for AI Recipe Generator
FROM python:3.12-slim

# Set working directory
WORKDIR /app

# Install system dependencies
RUN apt-get update && apt-get install -y \
    gcc \
    g++ \
    curl \
    && rm -rf /var/lib/apt/lists/*

# Copy requirements first for better caching
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy the recipe_ai module
COPY . ./recipe_ai/

# Set environment variables
ENV PYTHONPATH=/app
ENV STREAMLIT_SERVER_PORT=8080
ENV STREAMLIT_SERVER_ADDRESS=0.0.0.0
ENV STREAMLIT_BROWSER_GATHER_USAGE_STATS=false
ENV STREAMLIT_SERVER_HEADLESS=true

# Expose port for Cloud Run
EXPOSE 8080

# Default command - run the Streamlit app
CMD ["streamlit", "run", "recipe_ai/ui/app.py", "--server.port=8080", "--server.address=0.0.0.0", "--server.headless=true"]
