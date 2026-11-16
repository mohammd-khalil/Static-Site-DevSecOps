FROM nginx:alpine

RUN apk update && apk upgrade --no-cache

COPY ./web-page /usr/share/nginx/html

COPY ./nginx/nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80