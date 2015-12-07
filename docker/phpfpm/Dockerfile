# see: https://github.com/fideloper/docker-nginx-php/
FROM ubuntu:14.04
MAINTAINER Liu Dong <ddliuhb@gmail.com>

RUN sed -i "s/archive\.ubuntu\.com/mirrors.aliyun.com/g" /etc/apt/sources.list
RUN apt-get update && \
    apt-get install -y nginx \
    php5 php5-cli php5-fpm \
    php5-gd php5-mysql php5-memcached php5-redis php5-mcrypt \
    php5-curl && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
RUN sed -i -e "s/;daemonize\s*=\s*yes/daemonize = no/g" /etc/php5/fpm/php-fpm.conf
RUN sed -i '/^listen /c listen = 0.0.0.0:9000' /etc/php5/fpm/pool.d/www.conf
RUN sed -i 's/^listen.allowed_clients/;listen.allowed_clients/' /etc/php5/fpm/pool.d/www.conf

RUN sed -i "s/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/" /etc/php5/fpm/php.ini

RUN echo "Asia/Shanghai" > /etc/timezone
RUN dpkg-reconfigure -f noninteractive tzdata

EXPOSE 9000
CMD php5-fpm