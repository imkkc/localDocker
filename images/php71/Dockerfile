FROM php:7.1.13-fpm

RUN cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

ADD php.ini /usr/local/etc/php/php.ini
ADD php-fpm.conf /usr/local/etc/php-fpm.conf

# For wget zip bz2 gd ftp mcrypt Git cron
RUN apt-get update && apt-get install -y \
    wget \
    vim \
    zip \
    libbz2-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng12-dev \
    libssl-dev \
    libmcrypt-dev \
    libmemcached-dev \
    git \
    cron
# Cleanup
RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    mkdir -p /home/packages/download && \
    wget -P /home/packages/download/ https://pecl.php.net/get/redis-4.1.1.tgz && \
    tar zxvf /home/packages/download/redis-4.1.1.tgz  -C /home/packages/download/ && \
    mkdir -p /usr/src/php/ext && \
    mv /home/packages/download/redis-4.1.1 /usr/src/php/ext/redis && \
    wget -P /home/packages/download/ https://pecl.php.net/get/yaf-3.0.7.tgz && \
    tar zxvf /home/packages/download/yaf-3.0.7.tgz -C /home/packages/download/ && \
    mv /home/packages/download/yaf-3.0.7 /usr/src/php/ext/yaf && \
    docker-php-ext-install iconv mcrypt && \
    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-install gd && \
    docker-php-ext-install pdo_mysql && \
    docker-php-ext-install mbstring && \
    docker-php-ext-install exif && \
    docker-php-ext-install bz2 && \
    docker-php-ext-install bcmath && \
    docker-php-ext-install gettext  && \
    docker-php-ext-install redis && \
    docker-php-ext-install yaf && \
    docker-php-ext-enable redis yaf
    
RUN mkdir -p /localdocker/log

WORKDIR /www
RUN usermod -u 1000 www-data

EXPOSE 9002
VOLUME ["/www"]
