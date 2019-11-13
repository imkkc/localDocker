# pizza
pizza dinner room 

记录一些docker-compose的使用方法

ERROR: Service 'php7' failed to build: The command ' xxx ' returned a non-zero code: 100

在写Dockerfile时遇到 returned a non-zero code: 100，报这个错误是因为在install之前没有update

RUN apt-get update && apt-get install -y xxx 就可以啦


秒懂Docker 中安装扩展 PHP
https://www.linuxprobe.com/docker-php.html

这篇文章写的不错，也可以看看作者的其他文章 
