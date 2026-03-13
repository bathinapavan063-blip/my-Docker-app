# ----------------------------------------
# Stage 1: Install dependencies
# ----------------------------------------
FROM python:3.11-slim AS builder

WORKDIR /app

COPY requirements.txt .
RUN pip install --upgrade pip && \
    pip install --prefix=/install -r requirements.txt


# ----------------------------------------
# Stage 2: Final runtime image
# ----------------------------------------
FROM python:3.11-slim

WORKDIR /app

# Copy installed site-packages
COPY --from=builder /install /usr/local

# Copy source code
COPY . .

# Create non-root user
RUN useradd -m appuser
USER appuser

EXPOSE 5000

CMD ["python", "app.py"]
