FROM hyperf/hyperf:7.2-alpine-cli
MAINTAINER JasonZhao <zhaoyingnan211@gmail.com>
RUN php -r "copy('https://install.phpcomposer.com/installer', 'composer-setup.php');" && \
    php composer-setup.php && php -r "unlink('composer-setup.php');" && \
    mv composer.phar /usr/local/bin/composer && chmod +x /usr/local/bin/composer && \
    composer config -g repo.packagist composer https://mirrors.aliyun.com/composer
