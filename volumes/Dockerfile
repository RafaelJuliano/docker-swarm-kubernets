FROM php:8-apache

WORKDIR /var/www/html/

COPY . .

EXPOSE 80

RUN chown -R www-data:www-data /var/www

RUN chmod 755 /var/www/html/

USER www-data