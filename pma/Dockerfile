FROM ubuntu:latest
MAINTAINER shibinc@qburst.com
RUN apt-get update
RUN apt-get install -y phpmyadmin php-mbstring php-gettext
RUN sudo phpenmod mbstring
CMD ["apache2ctl", "-D", "FOREGROUND"]

