FROM mysql:5.6

RUN cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

# Write Permission
RUN usermod -u 1000 mysql && chown mysql:mysql /var/run/mysqld/

EXPOSE 3306
VOLUME ["/opt"]
