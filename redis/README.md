## Redis Dockerfile Build By CentOS7

### Use

`cd $HOME`
`git clone git@github.com:wangyongdong/docker-centos.git` 克隆项目
`cd docker-centos/redis/`
`docker build -t redis .`   构建镜像

##### 运行

`cd $HOME/docker-centos`
`docker run -d --name redis --privileged=true -p 36379:6379 --restart=always -d redis redis-server --appendonly yes --requirepass "123456"`

##### 挂载目录及配置文件运行

`cd $HOME/docker-centos`
`docker run -d --name redis --privileged=true -p 36379:6379 \
-v $PWD/redis/data:/data \
-v $PWD/redis/conf/redis.conf:/usr/local/redis/conf/redis.conf \
--restart=always -d redis redis-server --appendonly yes --requirepass "123456"`


> 确保挂载位置有文件，否则挂载失败

### 命令说明

 - -d: 后台运行容器，并返回容器ID;
  - --name: 为容器指定一个名称;
  - -p: 将容器的端口映射到主机的端口;
  - -v: 将主机中的目录及文件挂载到容器的目录及文件;
 - redis-server --appendonly yes: 在容器执行 redis-server 启动命令，并打开 redis 持久化配置;
 - --requirepass "123456": 设置 redis 密码，或在配置文件 redis.conf 中添加 `requirepass 123456` 设置密码
 - –privileged=true: 默认情况下，Docker的容器是没有特权的，例如不能在容器中再启动一个容器，这是因为默认情况下容器是不能访问任何其它设备的。
但是通过"privileged"，容器就拥有了访问任何其它设备的权限。当操作者执行docker run --privileged时，Docker将拥有访问主机所有设备的权限，
同时Docker也会在apparmor或者selinux做一些设置，使容器可以容易的访问那些运行在容器外部的设备;
 