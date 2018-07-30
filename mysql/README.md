## MySql Dockerfile Build By CentOS7

### Use

`cd $HOME`
`git clone git@github.com:wangyongdong/docker-centos.git` 克隆项目
`cd docker-centos/mysql/`
`docker build -t mysql .`   构建镜像

##### 运行

`cd $HOME/docker-centos`
`docker run --name mysql -p 33306:3306 -e MYSQL_ROOT_PASSWORD=123456 -d mysql`

##### 挂载目录及配置文件运行

`cd $HOME/docker-centos`
`docker run --name mysql -p 33306:3306 -e MYSQL_ROOT_PASSWORD=123456 \
 -v ./data/mysql/data:/var/lib/mysql \
 -v ./data/mysql/conf/my.cnf:/etc/my.cnf \
 -v ./data/mysql/log:/var/log/mysql \
 -d mysql`

> 确保挂载位置有文件，否则挂载失败

### 命令说明

  - -d: 后台运行容器，并返回容器ID
  - --name: 为容器指定一个名称
  - -p: 端口映射，格式为：主机(宿主)端口:容器端口
  - -v: 挂载宿主机目录/文件到容器的目录/文件
  - -e: 设置环境变量，指定mysql密码
 