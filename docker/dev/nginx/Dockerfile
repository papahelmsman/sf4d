FROM nginx:latest

LABEL maintainer="Pavel A. Petrovv <papahelmsman@gmail.com>"

ARG MAX_EXECUTION_TIME

ADD nginx.conf /etc/nginx/
RUN sed "/fastcgi_read_timeout 60s;/c\  fastcgi_read_timeout ${MAX_EXECUTION_TIME}s;" -i /etc/nginx/nginx.conf

COPY conf.d/sf4d.conf /etc/nginx/conf.d/sf4d.conf

RUN rm /etc/nginx/conf.d/default.conf

WORKDIR /usr/srv/app
