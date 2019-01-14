FROM node:8.15.0-alpine
MAINTAINER JasonZhao <zhaoyingnan211@gmail.com>
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories && \
    apk update && \
    apk add git && \
    mkdir -p /data/webroot
RUN apk add -U tzdata && \
    cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    date
RUN npm --registry=https://registry.npm.taobao.org install hexo-cli -g
ADD ./entrypoint.sh /bin/entrypoint.sh
WORKDIR /data/webroot
