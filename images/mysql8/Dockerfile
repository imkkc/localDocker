FROM mysql:8

#RUN cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

# Write Permission
RUN usermod -u 1000 mysql && chown mysql:mysql /var/run/mysqld/
# Custom config should go here
#  show variables like 'default_authentication_plugin';
#  select host,user,plugin from mysql.user;
# ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY '111111';  如果是docker环境访问的话要设置这个
# ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '111111'; 网络流传方法对docker架构无效
# FLUSH PRIVILEGES; 我没用这句刷新权限也正常访问了
COPY my.cnf /etc/mysql/my.cnf
#COPY mysql.cnf /etc/mysql/conf.d/mysql.cnf

EXPOSE 3306
VOLUME ["/opt"]
