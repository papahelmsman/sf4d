FROM nginx:latest

LABEL maintainer="Pavel A. Petrovv <papahelmsman@gmail.com>"

ARG WORKDIR
ARG APP_NAME

COPY docker/dev/nginx/nginx.conf /etc/nginx/nginx.conf

COPY docker/dev/nginx/conf.d/sf4d.conf /etc/nginx/conf.d/sf4d.conf
RUN sed "/    root public;/c\    root \/$WORKDIR\/$APP_NAME\/public;" -i /etc/nginx/conf.d/sf4d.conf

RUN rm /etc/nginx/conf.d/default.conf

WORKDIR /$WORKDIR/$APP_NAME/public
