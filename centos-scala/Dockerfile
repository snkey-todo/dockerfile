# 继承
FROM zhushengdocker/centos-java:jdk8

# 维护者信息
MAINTAINER zhusheng 1537017271@qq.com

# 新建参数，Scala是一门语言，号称是下一代Java
ARG SCALA_VERSION=2.10.6

# 镜像描述
LABEL Description="Scala + CentOS (+OpenJDK)"

# 安装scala
RUN set -euxo pipefail && \
    rpm -ivh http://downloads.lightbend.com/scala/$SCALA_VERSION/scala-$SCALA_VERSION.rpm && \
    yum autoremove -y && \
    yum clean all && \
    rm -rf /var/cache/yum

# 容器启动执行
CMD /bin/bash