FROM python:3.9 

WORKDIR /app 

COPY requirements.txt .
RUN pip install --no-cache-dir --upgrade pip && \
    pip install --no-cache-dir -r requirements.txt



CMD ["/app/.venv/bin/python", "kafka1:/home/appuser/Producer.py"]
