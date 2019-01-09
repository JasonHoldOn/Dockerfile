FROM php:7.2.6-fpm-alpine3.7
MAINTAINER JasonZhao <zhaoyingnan211@gmail.com>
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories && \
    apk update && \
    apk add libxml2-dev libpng libpng-dev supervisor git tzdata && \
    cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    date
RUN docker-php-ext-install pdo_mysql && \
    docker-php-ext-install soap && \
    docker-php-ext-install bcmath && \
    docker-php-ext-install gd && \
    docker-php-ext-install zip && \
    docker-php-ext-install sockets
RUN php -r "copy('https://install.phpcomposer.com/installer', 'composer-setup.php');" && \
    php composer-setup.php && php -r "unlink('composer-setup.php');" && \
    mv composer.phar /usr/local/bin/composer && chmod +x /usr/local/bin/composer && \
    composer config -g repo.packagist composer https://packagist.laravel-china.org
ENTRYPOINT ["/usr/bin/supervisord", "-n", "-c",  "/etc/supervisord.conf"]
