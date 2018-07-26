FROM centos:7
MAINTAINER wangyongdong <wydchn@gmail.com>

#配置时区
ENV TZ "Asia/Shanghai"

RUN set -x \
  && yum update -y \
  && yum install -y wget gcc gcc-c++ make perl tar \
  && wget http://dev.mysql.com/get/mysql-community-release-el7-5.noarch.rpm -d \
  && yum localinstall mysql-community-release-el7-5.noarch.rpm -y \
  && yum install mysql-community-server -y \
  && rm mysql-community-release-el7-5.noarch.rpm \
  && yum clean all \
  && mkdir /scripts \
  && mkdir -p /var/log/mysql

# Copy configuration file and sh
COPY ./conf/my.cnf /etc/my.cnf
COPY ./scripts/docker-entrypoint.sh /scripts/docker-entrypoint.sh
RUN chmod +x /scripts/docker-entrypoint.sh

# Define mountable directories.
#VOLUME ["/var/lib/mysql", "/var/log/mysql"]

# Define port
EXPOSE 3306

# Define run
ENTRYPOINT ["/scripts/docker-entrypoint.sh"]
