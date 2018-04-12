FROM ubuntu
RUN apt-get update
RUN apt-get install -y nodejs
RUN mkdir /var/www
WORKDIR /var/www

EXPOSE 8081

ADD app.js /var/www/app.js
CMD ["nodejs", "/var/www/app.js"]
