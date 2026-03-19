FROM python:3.12-alpine AS builder
WORKDIR /app

RUN pip install --no-cache-dir uv
COPY docker_with_problems/src/requirements.txt .
RUN uv venv /opt/venv && uv pip install --python /opt/venv/bin/python --no-cache -r requirements.txt

FROM python:3.12-alpine
WORKDIR /app

ENV PATH="/opt/venv/bin:$PATH" PYTHONDONTWRITEBYTECODE=1 PYTHONUNBUFFERED=1

COPY --from=builder /opt/venv /opt/venv
COPY docker_with_problems/src/app.py ./app.py

EXPOSE 5001
CMD ["python", "app.py"]