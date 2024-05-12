FROM python:3.9 

WORKDIR /app 

COPY requirements.txt .
RUN pip install --no-cache-dir --upgrade pip && \
    pip install --no-cache-dir -r requirements.txt

COPY Producer.py .
COPY twitter_validation.csv .

CMD ["python", "Producer.py"]
