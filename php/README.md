## PHP7 Dockerfile Build By CentOS7

### Get

`mkdir -p $HOME/docker/`
`cd $HOME/docker/`
`git clone xxx`

### Use

`cd $HOME/docker/php/`
`docker run --name php -p 9000:9000 -d php`

挂载目录及配置文件运行

`docker run --name php -p 9000:9000 \
 -v $HOME/docker-box/mount-data/docker-centos/php/php.ini:/usr/local/php/etc/php.ini \
 -v $HOME/docker-box/mount-data/docker-centos/php/logs/php-fpm.log:/usr/local/php/var/log/php-fpm.log \
 -v $HOME/docker-box/mount-data/docker-centos/www:/usr/local/nginx/html \
 --link redis:redis --link mysql:mysql -d php`

> 确保挂载位置有文件，否则挂载失败

### 命令说明

  - -d: 后台运行容器，并返回容器ID
  - --name: 为容器指定一个名称
  - -p: 端口映射，格式为：主机(宿主)端口:容器端口
  - -v: 挂载宿主机目录/文件到容器的目录/文件
  - --link: 添加链接到另一个容器
 