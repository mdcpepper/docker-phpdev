FROM ubuntu:16.04

MAINTAINER Mike Pepper

RUN apt-get update \
    && apt-get install -y locales \
    && locale-gen en_GB.UTF-8

ENV LANG en_GB.UTF-8
ENV LANGUAGE en_GB:en
ENV LC_ALL en_GB.UTF-8

RUN apt-get update \
    && apt-get install -y nginx curl zip unzip git software-properties-common supervisor

RUN add-apt-repository -y ppa:ondrej/php \
    && apt-get update \
    && apt-get install -y \
        php7.2-fpm \
        php-pear \
        php-intl \
        libmagickwand-dev \
        imagemagick \
        php-dev \
        php7.2-curl \
        php7.2-dev \
        php7.2-mbstring \
        php7.2-zip \
        php7.2-mysql \
        php7.2-xml \
        php7.2-xdebug \
    && pecl install imagick \
    && php -r "readfile('https://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer \
    && mkdir /run/php \
    && apt-get remove -y --purge software-properties-common \
    && apt-get -y autoremove \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && echo "daemon off;" >> /etc/nginx/nginx.conf \
    && ln -sf /dev/stdout /var/log/nginx/access.log \
    && ln -sf /dev/stderr /var/log/nginx/error.log

COPY nginx-default /etc/nginx/sites-available/default

COPY php-fpm.conf /etc/php/7.2/fpm/php-fpm.conf
COPY php.ini /etc/php/7.2/fpm/conf.d/99-php.ini
COPY xdebug.ini /etc/php/7.2/mods-available/xdebug.ini

COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

COPY container-start /usr/local/bin/container-start
RUN chmod +x /usr/local/bin/container-start

EXPOSE 80

CMD ["/usr/local/bin/container-start"]