#
# Dockerfile for building Nginx images
#
# https://github.com/addcn/docker-lnmp.git
#
FROM centos:7
MAINTAINER dodo <lhuibo@gmail.com>

ENV TZ "Asia/Shanghai"

# 设置 nginx 版本
ENV NGINX_VERSION 1.13.0

# Yum
RUN yum -y update \
    && yum install -y gcc automake autoconf libtool make gcc-c++ vixie-cron  wget zlib  file openssl-devel sharutils zip  bash vim cyrus-sasl-devel libmemcached libmemcached-devel libyaml libyaml-devel unzip libvpx-devel openssl-devel ImageMagick-devel  autoconf  tar gcc libxml2-devel gd-devel libmcrypt-devel libmcrypt mcrypt mhash libmcrypt libmcrypt-devel libxml2 libxml2-devel bzip2 bzip2-devel curl curl-devel libjpeg libjpeg-devel libpng libpng-devel freetype-devel bison libtool-ltdl-devel net-tools \
    && yum clean all

# Nginx
RUN mkdir ~/download \
    && cd ~/download \
    && wget http://nginx.org/download/nginx-$NGINX_VERSION.tar.gz \
    && tar xzf nginx-$NGINX_VERSION.tar.gz \
    && cd nginx-$NGINX_VERSION \
    && ./configure \
        --prefix=/usr/local/nginx \
        --with-pcre \
        --with-http_v2_module \
        --with-http_ssl_module \
        --with-http_realip_module \
        --with-http_addition_module \
        --with-http_sub_module \
        --with-http_dav_module \
        --with-http_flv_module \
        --with-http_mp4_module \
        --with-http_gunzip_module \
        --with-http_gzip_static_module \
        --with-http_random_index_module \
        --with-http_secure_link_module \
        --with-http_stub_status_module \
        --with-http_auth_request_module \
        --with-mail \
        --with-mail_ssl_module \
        --with-file-aio \
        --with-http_v2_module \
        --with-threads \
        --with-stream \
        --with-stream_ssl_module \
        --with-debug \
    && make \
    && make install \
    && rm -rf ~/download \
    && yum clean all

ADD conf/nginx.conf /usr/local/nginx/conf/nginx.conf
ADD conf/vhost/* /usr/local/nginx/conf/vhost/
RUN chmod 755 /usr/local/nginx/conf/nginx.conf

# 若要使用https，请将以下三个注释去掉,并在ssl文件夹中添加你自己申请的两个证书文件
#RUN mkdir -p /etc/nginx/cert
#COPY ssl/nginx.pem /etc/nginx/cert/nginx.pem
#COPY ssl/nginx.key /etc/nginx/cert/nginx.key

EXPOSE 80 443

#启动nginx
ENTRYPOINT ["/usr/local/nginx/sbin/nginx", "-g", "daemon off;"]
