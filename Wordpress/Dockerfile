FROM ubuntu:latest
MAINTAINER shibinc@qburst.com
RUN apt-get update

#webserver configuration
RUN apt-get -y install apache2 apache2-utils

#supervisor
RUN apt-get -y install supervisor

#php-extensions
RUN apt-get -y install php-curl php-gd php-mbstring php-xml php-xmlrpc php-soap php-intl php-zip
RUN apt-get clean

#mysql
RUN echo 'mysql-server mysql-server/root_password password root' | \
debconf-set-selections && \
echo 'mysql-server mysql-server/root_password_again password root' | \
debconf-set-selections
RUN apt-get install -y mysql-server


#wordpress
RUN apt-get -y install wget
RUN wget http://wordpress.org/latest.tar.gz 
RUN tar xzvf latest.tar.gz
RUN cp -R ./wordpress/* /var/www/html
RUN rm /var/www/html/index.html
RUN mkdir -p /var/run/mysqld
RUN chown mysql:mysql /var/run/mysqld
RUN (/usr/bin/mysqld_safe &); sleep 5; mysqladmin -uroot -proot create wordpress
CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]


EXPOSE 80
CMD ["apache2ctl", "-D", "FOREGROUND"]
CMD ["/usr/bin/supervisord"]


