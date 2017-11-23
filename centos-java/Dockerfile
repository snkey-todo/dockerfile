# 继承最新版的centos7
FROM centos:latest

# 维护者信息 
MAINTAINER zhusheng 1537017271@qq.com

# 描述信息
LABEL Description="Java + CentOS (OpenJDK)"

# 定义参数
ARG JAVA_VERSION=8
ARG JAVA_RELEASE=JDK

# 指定环境变量，为RUN指令所用
ENV JAVA_HOME=/usr

# 执行jdk安装指令
RUN set -euxo pipefail && \
    pkg="java-1.$JAVA_VERSION.0-openjdk" && \
    if [ "$JAVA_RELEASE" = "JDK" ]; then \
        pkg="$pkg-devel"; \
    else \
        pkg="$pkg-headless"; \
    fi; \
    yum install -y "$pkg" && \
    yum clean all && \
    rm -rf /var/cache/yum

# 拷贝
COPY profile.d/java.sh /etc/profile.d/

# 容器启动执行指令
CMD /bin/bash

