FROM nginx:1.13.8-alpine

#ENV GUNICORN_LOG=/var/log/gunicorn

#RUN mkdir -p $GUNICORN_LOG

ADD nginx.conf /etc/nginx/nginx.conf

RUN mkdir -p /var/www/media
RUN mkdir -p /var/www/static

WORKDIR /var/www/media
WORKDIR /var/www/static

RUN chown -R nginx:nginx /var/www/media
RUN chown -R nginx:nginx /var/www/static
