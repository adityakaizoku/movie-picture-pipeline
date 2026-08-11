FROM python:3.10-bookworm

ENV FLASK_RUN_HOST=0.0.0.0

WORKDIR /app

RUN apt-get update && apt-get install -y \
    build-essential \
    gcc \
    libpcre3-dev \
    libssl-dev \
    && rm -rf /var/lib/apt/lists/*

RUN pip install --no-cache-dir pipenv

COPY Pipfile Pipfile.lock ./

RUN pipenv install --system --deploy

COPY . /app

EXPOSE 5000

CMD ["uwsgi", "--http", "0.0.0.0:5000", "--master", "--enable-threads", "--manage-script-name", "--mount", "/=app:app"]