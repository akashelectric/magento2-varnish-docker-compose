FROM ubuntu:20.04

LABEL maintainer="Akash Verma <akashkumarverma@cedcommerce.com>"

ARG mysql_password
ARG mysql_database
env MYSQL_ROOT_PASSWORD ${mysql_password}
env MYSQL_DATABASE ${mysql_database}

RUN apt-get update \
&& echo "mysql-server-8.0 mysql-server/root_password password ${mysql_password}" | debconf-set-selections \
&& echo "mysql-server-8.0 mysql-server/root_password_again password ${mysql_password}" | debconf-set-selections \
&& DEBIAN_FRONTEND=noninteractive apt-get -y install mysql-server-8.0 && \
    mkdir -p /var/lib/mysql && \
    mkdir -p /var/run/mysqld && \
    mkdir -p /var/log/mysql && \
    touch /var/run/mysqld/mysqld.sock && \
    touch /var/run/mysqld/mysqld.pid && \
    chown -R mysql:mysql /var/lib/mysql && \
    chown -R mysql:mysql /var/run/mysqld && \
    chown -R mysql:mysql /var/log/mysql &&\
    chmod -R 777 /var/run/mysqld/ \
    && sed -i -e"s/^bind-address\s*=\s*127.0.0.1/bind-address = 0.0.0.0/" /etc/mysql/mysql.conf.d/mysqld.cnf \
##install supervisor and setup supervisord.conf file
    && apt-get install -y supervisor nano \
    && mkdir -p /var/log/supervisor 
CMD ["/usr/bin/supervisord"]
