FROM mysql:5.7

#RUN cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

# Write Permission
RUN usermod -u 1000 mysql && chown mysql:mysql /var/run/mysqld/

COPY my.cnf /etc/mysql/my.cnf

EXPOSE 3306
VOLUME ["/opt"]
