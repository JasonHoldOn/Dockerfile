# jason911/hexo:0.0.1
可以当做自己本地的开发环境

## .env
```sh
HEXO_VERSION=jason911/hexo:0.0.1
EXPOSE_PORT=3000
BLOG_DIR=blog
```

## docker-compose.yml
```sh
version: '3'
services:
    hexo:
        container_name: my_blog
        build:
            context: ./hexo
            dockerfile: Dockerfile
            args:
                - hexo_version=$HEXO_VERSION
                - blog_dir=$BLOG_DIR
        ports:
            - $EXPOSE_PORT:4000
        volumes:
            - ./data/:/data/webroot/
            - ./entrypoint.sh:/bin/entrypoint.sh
```

## entrypoint.sh
```sh
#!/bin/bash
#author JasonZhao <zhaoyingnan211@gmail.com>
nohup npm install && hexo s -p 4000
```

## hexo/Dockerfile
```sh
ARG hexo_version
FROM $hexo_version
MAINTAINER JasonZhao <zhaoyingnan211@gmail.com>
ARG blog_dir
WORKDIR /data/webroot/$blog_dir
#ENTRYPOINT ["/usr/local/bin/hexo", "s", "-p", "4000"]
ENTRYPOINT ["sh", "/bin/entrypoint.sh"]
```

## ./data
```sh
mkdir blog
cd blog
mkdir source
mkdir themes
touch _config.yml
```
