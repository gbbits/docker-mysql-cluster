FROM mysql:5.7.30
MAINTAINER who "lianyan598@gmail.com"

ENV TZ "Asia/Shanghai"
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

COPY mysqld.cnf /etc/mysql/mysql.conf.d/mysqld.cnf

RUN mkdir -p /opt/log \
    && mkdir -p /opt/data \
    && bash -c 'chmod 777 -R /opt'