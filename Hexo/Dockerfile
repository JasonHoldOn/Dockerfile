FROM node:8.15.0-alpine
MAINTAINER JasonZhao <zhaoyingnan211@gmail.com>
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories && \
    apk update
RUN apk add -U tzdata && \
    cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    date && \
    apk add git
RUN npm --registry=https://registry.npm.taobao.org install hexo-cli -g
RUN mkdir -p /data/webroot && \
    cd /data/webroot && \
    hexo init heox
WORKDIR /data/webroot/heox
ENTRYPOINT ["hexo", "s", "-p", "3000"]
