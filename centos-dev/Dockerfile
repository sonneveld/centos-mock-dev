FROM centos:7

# update first before we blat the repos
RUN yum update -y 
RUN yum --enablerepo=extras install -y epel-release
RUN yum --enablerepo=epel install -y mock

# grab some srpms for testing
RUN curl -O http://vault.centos.org/7.7.1908/os/Source/SPackages/curl-7.29.0-54.el7.src.rpm
RUN curl -O http://vault.centos.org/7.7.1908/os/Source/SPackages/less-458-9.el7.src.rpm

RUN yum install -y less vim

# disable original
COPY etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/
COPY etc/yum.repos.d/epel.repo /etc/yum.repos.d/

# add nexus
COPY etc/yum.repos.d/nexus.repo /etc/yum.repos.d/

COPY etc/rpm/macros.netshared /etc/rpm/

RUN mkdir -p /mock/{base,cache,config,out}
RUN chgrp mock /mock/{base,cache,config,out}
RUN chmod g+rws /mock/{base,cache,config,out}

COPY mock/config/site-defaults.cfg /mock/config/
COPY mock/config/logging.ini /mock/config/
COPY mock/config/default.cfg /mock/config/
RUN chgrp mock /mock/config/*

RUN useradd --no-log-init -r -g mock dev
USER dev
