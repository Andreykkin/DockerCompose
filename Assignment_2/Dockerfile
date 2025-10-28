FROM python:3.9-alpine AS builder
WORKDIR /app
RUN python -m venv /app/venv
COPY requirements.txt .
RUN /app/venv/bin/pip install --no-cache-dir -r requirements.txt

FROM python:3.9-alpine AS runtime
RUN adduser -D webapp
WORKDIR /app
COPY --from=builder /app/venv /app/venv
COPY --chown=webapp:webapp app.py .
USER webapp
ENV PATH="/app/venv/bin:$PATH"
EXPOSE 5000
ENV FLASK_APP=app.py
ENV FLASK_RUN_HOST=0.0.0.0
CMD ["flask", "run"]