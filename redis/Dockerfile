#
# Dockerfile for building Redis images
#
# https://github.com/wangyongdong/docker-lnmp.git
#
FROM centos:7
MAINTAINER wangyongdong <wydchn@gmail.com>

ENV TZ "Asia/Shanghai"

# 设置 Redis 版本
ENV REDIS_VERSION 3.2.9

# 下载并编译
RUN set -x \
  && yum update -y \
  && yum install -y wget gcc gcc-c++ make perl tar \
  && mkdir ~/download \
  && cd ~/download \
  && wget http://download.redis.io/releases/redis-$REDIS_VERSION.tar.gz \
  && tar -zxf redis-$REDIS_VERSION.tar.gz -C /usr/local \
  && mv /usr/local/redis-$REDIS_VERSION /usr/local/redis \
  && cd /usr/local/redis \
  && make \
  && make -C /usr/local/redis/src install \
  && yum clean all \
  && rm -rf ~/download

ADD conf/redis.conf /usr/local/redis/conf/redis.conf
RUN chmod 777 -R /usr/local/redis/conf/redis.conf

# Define mountable directories.
VOLUME ["/data"]

## Define working directory.
WORKDIR /data

# Define default command.
CMD ["/usr/local/redis/src/redis-server","/usr/local/redis/conf/redis.conf"]

EXPOSE 6379