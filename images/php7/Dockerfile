#FROM php:7.1.13-fpm
FROM php:7.4-fpm
#SHA2密码验证引起的PHP错误：SQLSTATE[HY000] [2054] The server requested authentication method unknown to the client
#忽然注意到的情况：
#2018/7/19至2018/9/13之间发布的7.1.20、7.1.21、7.1.22和7.2.8、7.2.9、7.2.10这六个版本提供的对caching_sha2_password插件的支持，
#后续的版本中又取消了相关支持，不知道是因为什么。按照PHP官方的文档，目前似乎只有xdevapi可以支持caching_sha2_password插件。
RUN cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
#这个路径在php-ini里先设置好，与docker-composer一致
#error_log = /localdocker/log/php7/php_errors.log
#ADD php.ini /usr/local/etc/php/php.ini
#ADD php-fpm.conf /usr/local/etc/php-fpm.conf
#ADD instantclient_21_1 /usr/local/instantclient_21_1
# 更新数据源镜像
#RUN  mv /etc/apt/sources.list /etc/apt/sources.list.bak && \
#     echo "deb http://mirrors.aliyun.com/debian wheezy main contrib non-free" >>/etc/apt/sources.list && \
#     echo "deb-src http://mirrors.aliyun.com/debian wheezy main contrib non-free" >>/etc/apt/sources.list && \
#     echo "deb http://mirrors.aliyun.com/debian wheezy-updates main contrib non-free" >>/etc/apt/sources.list && \
#     echo "deb-src http://mirrors.aliyun.com/debian wheezy-updates main contrib non-free" >>/etc/apt/sources.list && \
#     echo "deb http://mirrors.aliyun.com/debian-security wheezy/updates main contrib non-free" >>/etc/apt/sources.list && \
#     echo "deb-src http://mirrors.aliyun.com/debian-security wheezy/updates main contrib non-free" >>/etc/apt/sources.list && \
    # 相关依赖必须手动安装
RUN  apt-get update && apt-get install -y \
    libaio-dev \
    apt-utils \
    net-tools \
    iproute2 \
    telnet \
    procps \
    netcat \
    wget \
    vim \
    unzip \
    zip \
    #安装zip扩展必须先装libzip-dev composer与phpexcel等都会用到zip
    libzip-dev \
    libbz2-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    openssl \
    libssl-dev \
    libmcrypt-dev \
    libmemcached-dev \
    libonig-dev \
    librabbitmq-dev \
    git \
    cron \
    ## 清理安装包
#RUN sh -c "echo /usr/local/instantclient_21_1 > /etc/ld.so.conf.d/oracle-instantclient.conf"
#RUN ldconfig
#RUN export ORACLE_HOME=/usr/local/instantclient_21_1
&& apt-get clean && rm -rf /var/lib/apt/lists/*  && \
    docker-php-ext-install iconv && \
    # 如果安装的扩展需要自定义配置时
    #docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
    #PHP7.4的手册Other Changes才发现with参数改了
    docker-php-ext-configure gd  --with-jpeg=/usr/include --with-freetype=/usr/include/freetype2/ && \
    docker-php-ext-install gd && \
#    docker-php-ext-configure oci8 --with-oci8=instantclient,/usr/local/instantclient_21_1 && \
#    docker-php-ext-install oci8 && \
#    docker-php-ext-configure pdo_oci --with-pdo-oci=instantclient,/usr/local/instantclient_21_1,21.1 && \
#    docker-php-ext-install pdo_oci && \
        #注意：这里的 docker-php-ext-configure 和 docker-php-ext-install 已经包含了 docker-php-source 的操作，所有不需要再手动去执行。
        #官方提供 docker-php-source 快捷脚本，用于对源文件压缩包的解压（extract）及解压后的文件进行删除（delete）的操作。
        #注意：官方提供的 docker-php-ext-* 脚本接受任意的绝对路径（不支持相对路径，以便与系统内置的扩展程序进行区分），所以，上面的例子也可以这样写：
    docker-php-ext-install pdo_mysql && \
    docker-php-ext-install mbstring  && \
    docker-php-ext-install exif && \
    docker-php-ext-install bz2 && \
    docker-php-ext-install zip && \
    docker-php-ext-install bcmath && \
    docker-php-ext-install gettext && \
    docker-php-ext-install mysqli && \
    docker-php-ext-install opcache && \
    docker-php-ext-install sockets && \
    #PECL 扩展
    #因为一些扩展并不包含在 PHP 源码文件中，所有需要使用 PECL（PHP 的扩展库仓库，通过 PEAR 打包）。
    #用 pecl install 安装扩展，然后再用官方提供的 docker-php-ext-enable 快捷脚本来启用扩展，
    #php从7.2开始不再在源码里支持mcrypt扩展而转到pecl方式支持,
   # pecl install mcrypt-1.0.2 && \
    pecl install mcrypt && \
    pecl install memcached && \
#    xdebug会与swoole冲突
#    pecl install xdebug && \
    pecl install redis-5.1.1 && \
    pecl install amqp-1.10.2 && \
    pecl install yaf-3.3.1 && \
#    docker-php-ext-configure swoole --enable-openssl --enable-http2 && \
    pecl install swoole-4.6.4 && \
#    docker-php-ext-enable redis oci8 pdo_oci mcrypt opcache yaf memcached amqp swoole
    docker-php-ext-enable redis  mcrypt opcache yaf memcached amqp swoole
#RUN php -r "copy('https://install.phpcomposer.com/installer', 'composer-setup.php');"
#RUN php -r "if (hash_file('sha384', 'composer-setup.php') === 'a5c698ffe4b8e849a443b120cd5ba38043260d5c4023dbf93e1558871f1f07f58274fc6f4c93bcfd858c6bd0775cd8d1') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
#RUN php -r composer-setup.php --install-dir=/usr/local/bin --filename=composer
#RUN php -r "unlink('composer-setup.php');"
#RUN mv composer.phar /usr/local/bin/composer
#RUN mkdir -p /localdocker/log
#原本以为上面composer安装失败是因为没有启动php容器的原因，
#原本以为下面这个只是下载composer.phar还没有安装，结果进入容器里composer -v竟然有提示Composer version 1.9.1 安装成功
RUN curl -sS https://getcomposer.org/installer | php && \
 mv composer.phar /usr/local/bin/composer && \
 chmod -R 777 /usr/local/bin/composer
WORKDIR /www
#将www-data用户的uid改成1000
RUN usermod -u 1000 www-data
#Docker在进行bind mount或者COPY的时候，会保持文件的权限比特位（比如755）、owner ID（比如1000）、group ID（比如1000）与宿主机器上的来源文件相同。
#而【docker容器主进程的owner ID】（比如www-data(33)）往往与【宿主机器上的文件的owner ID】（比如xiaoming(1000)）不一样。
EXPOSE 9002
EXPOSE 9501
EXPOSE 9502
VOLUME ["/www"]
