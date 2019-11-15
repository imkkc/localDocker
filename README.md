# pizza
pizza dinner room 

记录一些docker-compose的使用方法

在写Dockerfile失败，最后遇到 returned a non-zero code: 100，报这个错误是因为在install之前没有update
而遇到returned a non-zero code: 1，这个报错情况 多是docker-php-ext-install安装重复，
小插曲经历：
我在安装扩展amqp的时候，docker-php-ext-install依赖包rabbitmq-c，
但是我在前面有 apt-get update && apt-get install librabbitmq-dev 
导致returned a non-zero code: 1频繁出现，最后我把rabbitmq-c命令拿掉就安装成功了

秒懂Docker中安装扩展PHP，这篇文章写的不错，也可以看看作者的其他文章 
https://www.linuxprobe.com/docker-php.html

Docker php安装扩展步骤详解，这文章也不错，算是对上面的一些补充
https://www.cnblogs.com/yinguohai/p/11329273.html

当不知道php7.1、 php7.2、 php7.3、 php7.4 好像快有php8.0 这些php对应yaf、redis、amqp等扩展需要安装什么版本时

那就先根据phpinfo内容查看下：
Zend Extension Build 、PHP Extension Build

看这两项是API320160303,NTS 或者是 API320160303 TS,VC14

然后去扩展包官方下载列表查看：

各种扩展的版本适合php7.1还是7.2，以及与phpinfo里对应的NTS还是VC，选择适合的扩展版本号
ts是线程安全的  nts是非线程安全的，根据自已的php 是ts还是nts来进行选择

以redis为例：

https://windows.php.net/downloads/pecl/releases/redis/5.1.1/

11/13/2019 12:34 AM       583236 php_redis-5.1.1-7.1-nts-vc14-x86.zip

11/13/2019 12:28 AM       605068 php_redis-5.1.1-7.1-ts-vc14-x64.zip

11/12/2019 11:51 PM       604661 php_redis-5.1.1-7.2-nts-vc15-x64.zip

11/13/2019 12:09 AM       586675 php_redis-5.1.1-7.2-nts-vc15-x86.zip

其他的类似，可以去看看

https://pecl.php.net/package/swoole

https://pecl.php.net/package/yaf

http://pecl.php.net/package/amqp
