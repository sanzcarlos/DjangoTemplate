FROM python:3.6.4-slim

ARG DJANGO_ENV

ENV PYTHONUNBUFFERED=1
ENV WEBAPP_DIR=/webapp
#ENV GUNICORN_LOG=/var/log/gunicorn

#RUN mkdir -p $GUNICORN_LOG
RUN mkdir -p $WEBAPP_DIR

WORKDIR $WEBAPP_DIR

ADD requirements/base.txt $WEBAPP_DIR
ADD requirements/$DJANGO_ENV.txt  $WEBAPP_DIR

RUN pip install -r $DJANGO_ENV.txt

ADD . $WEBAPP_DIR/ 
