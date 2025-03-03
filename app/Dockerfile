# Stage 1
FROM python:3.9-slim as builder

WORKDIR /usr/src/app

RUN apt-get update && apt-get install -y --no-install-recommends gcc build-essential && \
    rm -rf /var/lib/apt/lists/*

COPY requirements.txt .

RUN python -m venv venv && \
    . venv/bin/activate && \
    pip install --no-cache-dir -r requirements.txt

# Stage 2
FROM python:3.9-slim

WORKDIR /usr/src/app

COPY --from=builder /usr/src/app/venv ./venv

COPY . .

ENV PATH="/usr/src/app/venv/bin:$PATH"

CMD [ "uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000" ]