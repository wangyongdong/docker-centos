## NGINX Dockerfile Build By CentOS7

### Get

`mkdir -p $HOME/docker/`
`cd $HOME/docker/`
`git clone xxx`

### Use

`cd $HOME/docker/nxinx/`
`docker run --name nginx -p 80:80 -d nginx`

挂载目录及配置文件运行

`docker run --name nginx -p 80:80 \
 -v $HOME/docker-box/mount-data/docker-centos/www:/usr/local/nginx/html \
 -v $HOME/docker-box/mount-data/docker-centos/nginx/logs/error.log:/usr/local/nginx/logs/error.log \
 -v $HOME/docker-box/mount-data/docker-centos/nginx/logs/access.log:/usr/local/nginx/logs/access.log \
 -v $HOME/docker-box/mount-data/docker-centos/nginx/conf/nginx.conf:/usr/local/nginx/conf/nginx.conf \
 -v $HOME/docker-box/mount-data/docker-centos/nginx/conf/vhost:/usr/local/nginx/conf/vhost \
 --link php:php -d nginx`

> 确保挂载位置有文件，否则挂载失败

### 命令说明

  - -d: 后台运行容器，并返回容器ID
  - --name: 为容器指定一个名称
  - -p: 端口映射，格式为：主机(宿主)端口:容器端口
  - -v: 挂载宿主机目录/文件到容器的目录/文件
  - --link: 添加链接到另一个容器
 