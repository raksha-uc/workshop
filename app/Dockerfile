FROM python:3.9-alpine3.15

ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

COPY ./requirement.txt requirement.txt

RUN apk update \
    && apk add libpq libpq-dev gcc musl-dev make expat-dev\
    && mkdir -p /app \
    && pip3 install --no-cache-dir -r requirement.txt \
    && apk del gcc musl-dev make libpq-dev expat-dev\
    && rm -rf /var/cache/apk/*  /root/.cache/*


COPY ./ /app/
WORKDIR /app