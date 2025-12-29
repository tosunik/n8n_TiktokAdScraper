# ---- Base
FROM python:3.11-slim

# Sistem bağımlılıkları (Chromium + chromedriver + fontlar)
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
    chromium \
    chromium-driver \
    fonts-liberation \
    libnss3 \
    libxss1 \
    libasound2 \
    libatk-bridge2.0-0 \
    libgtk-3-0 \
    && rm -rf /var/lib/apt/lists/*

ENV CHROME_BIN=/usr/bin/chromium
ENV CHROMEDRIVER=/usr/bin/chromedriver
ENV PYTHONUNBUFFERED=1

# ---- App
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY . .

# Uvicorn ile FastAPI servisini başlat
# Not: fastapi_server.py içinde FastAPI nesnesi 'app' olmalı
CMD ["uvicorn", "fastapi_server:app", "--host", "0.0.0.0", "--port", "$PORT"]
