## MySql Dockerfile Build By CentOS7

### Get

`mkdir -p $HOME/docker/`
`cd $HOME/docker/`
`git clone xxx`

### Use

`cd $HOME/docker/mysql/`
`docker run --name mysql -p 33306:3306 -e MYSQL_ROOT_PASSWORD=123456 -d mysql`

挂载目录及配置文件运行

`docker run --name mysql -p 33306:3306 -e MYSQL_ROOT_PASSWORD=123456 \
 -v $HOME/docker-box/mount-data/docker-centos/mysql/data:/var/lib/mysql \
 -v $HOME/docker-box/mount-data/docker-centos/mysql/conf/my.cnf:/etc/my.cnf \
 -v $HOME/docker-box/mount-data/docker-centos/mysql/log:/var/log/mysql \
 -d mysql`

> 确保挂载位置有文件，否则挂载失败

### 命令说明

  - -d: 后台运行容器，并返回容器ID
  - --name: 为容器指定一个名称
  - -p: 端口映射，格式为：主机(宿主)端口:容器端口
  - -v: 挂载宿主机目录/文件到容器的目录/文件
  - -e: 设置环境变量，指定mysql密码
 