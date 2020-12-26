FROM nginx:1.18.0-alpine

RUN apk add --no-cache shadow \
    && usermod -u 1001 nginx \
    && groupmod -g 1001 nginx

RUN  mkdir /app

COPY ./nginx.conf /etc/nginx/nginx.conf
COPY ./app.conf /etc/nginx/conf.d/app.conf
COPY ./index.html /app

EXPOSE 8000
USER 1001
