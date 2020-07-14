FROM centos:7

# Yum Initialize
RUN set -x && \
    : "タイムゾーンの変更" && \
    ln -sf  /usr/share/zoneinfo/Asia/Tokyo /etc/localtime && \
    yum -y update && yum clean all

# epel,remi
RUN yum install -y wget epel-release && \
	yum install -y http://rpms.famillecollet.com/enterprise/remi-release-7.rpm && \
    yum clean all && \
	sed -i -e "s/enabled *= *1/enabled=0/g" /etc/yum.repos.d/epel.repo && \
	sed -i -e "s/enabled *= *1/enabled=0/g" /etc/yum.repos.d/remi.repo && \
    sed -i '4a priority=1' /etc/yum.repos.d/remi-php74.repo

# Command
RUN yum install -y which sudo && \
    yum clean all

# Apache
RUN rpm --rebuilddb  && \
    yum -y install httpd httpd-tools mod_ssl mod_rewrite && \
    yum clean all && \
    systemctl enable httpd

# Apache Config
RUN cp -ap /etc/httpd/conf/httpd.conf /etc/httpd/conf/httpd.conf.org
ADD ./httpd/httpd.conf /etc/httpd/conf/

# php
RUN yum -y install --enablerepo=remi-php74 php && \
    yum clean all

# # PHP Config
# RUN cp -ap /etc/php.ini /etc/php.ini.org
# ADD ./setting/php/php.ini /etc/

# bash start
CMD "/bin/bash"
