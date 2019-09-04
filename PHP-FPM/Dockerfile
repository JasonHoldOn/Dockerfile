FROM php:7.2.6-fpm-alpine3.7
MAINTAINER JasonZhao <zhaoyingnan211@gmail.com>
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories && \
    apk update && \
    apk add libxml2-dev libpng libpng-dev supervisor git tzdata build-base openssl-dev autoconf && \
    cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    date
RUN docker-php-ext-install pdo_mysql && \
    docker-php-ext-install soap && \
    docker-php-ext-install bcmath && \
    docker-php-ext-install gd && \
    docker-php-ext-install zip && \
    docker-php-ext-install sockets && \
    docker-php-ext-install pcntl && \
    docker-php-ext-install posix && \
    cd /usr/src && \
    wget https://github.com/swoole/swoole-src/archive/v4.3.3.tar.gz && \
    tar -xzf v4.3.3.tar.gz && \
    mv swoole-src-4.3.3 swoole && \
    cd swoole && \
    phpize && \
    ./configure --with-php-config=/usr/local/bin/php-config --enable-sockets=yes --enable-openssl=yes --enable-mysqlnd=yes && \
    make && make install && \
    docker-php-ext-enable swoole && \
    php -m | grep swoole
RUN php -r "copy('https://install.phpcomposer.com/installer', 'composer-setup.php');" && \
    php composer-setup.php && php -r "unlink('composer-setup.php');" && \
    mv composer.phar /usr/local/bin/composer && chmod +x /usr/local/bin/composer && \
    composer config -g repo.packagist composer https://packagist.laravel-china.org
ENTRYPOINT ["/usr/bin/supervisord", "-n", "-c",  "/etc/supervisord.conf"]
