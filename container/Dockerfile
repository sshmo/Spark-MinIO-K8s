FROM spark-base/spark-py:1.0.0

USER root

WORKDIR /app

COPY ./requirements.txt /app

RUN pip install --upgrade pip && \
    pip install --no-cache-dir -r requirements.txt && \
    rm -rf requirements.txt

COPY ./spark.py /app





