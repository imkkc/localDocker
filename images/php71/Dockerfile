FROM php:7.1.13-fpm

RUN cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

ADD php.ini /usr/local/etc/php/php.ini
ADD php-fpm.conf /usr/local/etc/php-fpm.conf

# For wget zip bz2 gd ftp mcrypt Git cron
RUN apt-get update && apt-get install -y \
    # mv /etc/apt/sources.list /etc/apt/sources.list.bak && \
    # echo "deb http://mirrors.aliyun.com/debian/ jessie main non-free contrib" >/etc/apt/sources.list && \
    # echo "deb http://mirrors.aliyun.com/debian/ jessie-proposed-updates main non-free contrib" >>/etc/apt/sources.list && \
    # echo "deb http://mirrors.aliyun.com/debian-security/ jessie/updates main non-free contrib" >>/etc/apt/sources.list && \
    # echo "deb-src http://mirrors.aliyun.com/debian/ jessie main non-free contrib" >>/etc/apt/sources.list && \
    # echo "deb-src http://mirrors.aliyun.com/debian/ jessie-proposed-updates main non-free contrib" >>/etc/apt/sources.list && \
    # echo "deb-src http://mirrors.aliyun.com/debian-security/ jessie/updates main non-free contrib" >>/etc/apt/sources.list && \
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
    rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-install iconv mcrypt && \
    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-install gd && \
    docker-php-ext-install pdo_mysql && \
    docker-php-ext-install mbstring && \
    docker-php-ext-install exif && \
    docker-php-ext-install bz2 && \
    docker-php-ext-install bcmath && \
    docker-php-ext-install gettext && \
    docker-php-ext-install mysqli && \
    pecl install redis-4.1.1 && \
   # pecl install xdebug-2.6.0 && \
   # pecl install mongodb && \
    pecl install yaf-3.0.7 && \
    docker-php-ext-enable redis  yaf

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php -r "if (hash_file('SHA384', 'composer-setup.php') === '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" && \
    php composer-setup.php --install-dir=/usr/local/bin --filename=composer && \
    php -r "unlink('composer-setup.php');"

RUN mkdir -p /localdocker/log

WORKDIR /www
RUN usermod -u 1000 www-data

EXPOSE 9002
VOLUME ["/www"]
