FROM php:7.3-apache-stretch
ENV PHP_VERSION 7.3

# Ioncube
RUN apt update \
    && apt install -y wget \
    && apt clean

RUN cd /tmp \
    && wget https://downloads.ioncube.com/loader_downloads/ioncube_loaders_lin_x86-64.tar.gz \
    && tar -xvf ioncube_loaders_lin_x86* \
    && cd ioncube/ \
    && cp /tmp/ioncube/ioncube_loader_lin_${PHP_VERSION}.so $(php -i | grep extension_dir | awk -F " => " '{print $3}' | head -n 1)/ \
    && ls -lh $(php -i | grep extension_dir | awk -F " => " '{print $3}' | head -n 1)/ \
    && rm -rf /tmp/ioncube*
RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"
RUN echo "zend_extension = $(php -i | grep extension_dir | awk -F " => " '{print $3}' | head -n 1)/ioncube_loader_lin_${PHP_VERSION}.so" > $PHP_INI_DIR/conf.d/ioncube.ini
