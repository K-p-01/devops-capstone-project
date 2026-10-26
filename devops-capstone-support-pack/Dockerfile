# Customer Accounts service container for the IBM DevOps capstone template.
FROM python:3.9-slim

ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1 \
    PORT=8080

WORKDIR /app

COPY requirements.txt ./requirements.txt
RUN python -m pip install --no-cache-dir --upgrade pip wheel \
    && python -m pip install --no-cache-dir -r requirements.txt

COPY service ./service
COPY Procfile ./Procfile

# OpenShift/Kubernetes can run this image as a non-root user.
USER 1001
EXPOSE 8080

CMD ["sh", "-c", "exec gunicorn --workers=1 --bind 0.0.0.0:${PORT:-8080} --log-level=info service:app"]
