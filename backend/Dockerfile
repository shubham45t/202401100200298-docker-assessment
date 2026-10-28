FROM python:3.12.12-slim-bookworm

ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1

WORKDIR /app

# Update OS packages to obtain available security fixes
RUN apt-get update \
    && apt-get upgrade -y \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Install Python dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir --upgrade pip setuptools wheel \
    && pip install --no-cache-dir -r requirements.txt \
    && useradd --system --uid 10001 appuser

# Copy application files with appropriate ownership
COPY --chown=appuser:appuser app.py .

# Run as a non-root user
USER appuser

EXPOSE 5000

CMD ["python", "app.py"]
