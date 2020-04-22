FROM alpine:latest

MAINTAINER n3wbiemember "<info@girirahayu.com>"

#ADD https://dl.bintray.com/php-alpine/key/php-alpine.rsa.pub /etc/apk/keys/php-alpine.rsa.pub
RUN set -x \
    && apk add --update --no-cache ca-certificates icu-libs tzdata && \
    #echo "@php https://dl.bintray.com/php-alpine/v3.10/php-7.4" >> /etc/apk/repositories && \
    #default install php library
    apk add --update --no-cache \
    php7-fpm \
    php7-cli \
    php7-xml \
    php7-curl \
    php7-mcrypt \
    php7-ctype \
    php7-json \
    php7-openssl \
    php7-pdo \
    php7-intl \
    php7-pdo_mysql \
    php7-mysqlnd \
    php7-mysqli \
    php7-mbstring \
    php7-opcache \
    php7-bcmath \
    php7-zip \
    php7-dom \
    php7-iconv \
    php7-exif \
    php7-gd \
    php7-phar \
    php7-tokenizer \
    php7-xmlreader \
    php7-xmlwriter \
    php7-xdebug \
    php7-redis \
    php7-fileinfo \
    php7-common \
    php7-bz2 \
    php7-session \
    curl

RUN curl -o /usr/bin/composer https://getcomposer.org/composer-stable.phar && chmod +x /usr/bin/composer

RUN s=";date.timezone =" && \
    r="date.timezone = 'Asia/Jakarta'" && \
    sed -i -e "s~$s~$r~g" /etc/php7/php.ini

RUN s=";session.save_path" && \
    r="session.save_path" && \
    sed -i -e "s~$s~$r~g" /etc/php7/php.ini

#custome php and other template config
RUN sed -i -e "s/;\?pid\s*=\s*.*/pid = \/run\/php-fpm7.pid/g" /etc/php7/php-fpm.conf && \
    sed -i -e "s/;\?upload_max_filesize\s*=\s*.*/upload_max_filesize = 30M/g" /etc/php7/php.ini && \
    sed -i -e "s/;\?post_max_size\s*=\s*.*/post_max_size = 250M/g" /etc/php7/php.ini && \
    sed -i -e "s/;\?memory_limit\s*=\s*.*/memory_limit = 300M/g" /etc/php7/php.ini && \
    sed -i -e "s/;\?max_execution_time\s*=\s*.*/max_execution_time = 60/g" /etc/php7/php.ini && \
    sed -i -e "s/;\?pm\s*=\s*.*/pm = static/g" /etc/php7/php-fpm.d/www.conf && \
    sed -i -e "s/;\?expose_php\s*=\s*.*/expose_php = Off/g" /etc/php7/php.ini && \
    sed -i -e "s/;\?pm.max_children\s*=\s*.*/pm.max_children = 16/g" /etc/php7/php-fpm.d/www.conf && \
    ln -nsf /usr/share/zoneinfo/Asia/Jakarta /etc/localtime

ENTRYPOINT /usr/sbin/php-fpm7 -c /etc/php7/php-fpm.conf --nodaemonize
EXPOSE 9000
