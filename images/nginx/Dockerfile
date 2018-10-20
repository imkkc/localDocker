FROM nginx

RUN cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

COPY nginx.conf /etc/nginx/nginx.conf
#COPY fastcgi_params /etc/nginx/fastcgi_params
COPY vhosts /etc/nginx/conf.d/vhosts

RUN mkdir -p /www/ && \
    mkdir -p /localdocker/log/nginx && \
    chown -R www-data.www-data /www

EXPOSE 80

VOLUME ["/www"]
