# 继承
FROM zhushengdocker/centos-java:jdk8

# 维护者信息
MAINTAINER zhusheng 1537017271@qq.com

# 参数
ARG HADOOP_VERSION=2.8.2

ARG TAR=hadoop-$HADOOP_VERSION.tar.gz

# 环境变量
ENV PATH $PATH:/hadoop/bin

# 镜像描述信息
LABEL Description="Hadoop Dev", \
      "Hadoop Version"="$HADOOP_VERSION"

# 指定hadoop安装目录为根目录
WORKDIR /


# 安装ssh
RUN set -euxo pipefail && \
    yum install -y openssh-server openssh-clients tar which

# 安装hadoop
RUN set -euxo pipefail && \
    # 安装wget、hostname
    yum install -y wget hostname && \
    # 下载hadoop，给了2个下载链接，2选1，避免下载失败
    wget -t 10 --max-redirect 1 --retry-connrefused -O "$TAR" "http://www.apache.org/dyn/closer.lua?filename=hadoop/common/hadoop-${HADOOP_VERSION}/hadoop-$HADOOP_VERSION.tar.gz&action=download" || \
    wget -t 10 --max-redirect 1 --retry-connrefused -O "$TAR" "http://archive.apache.org/dist/hadoop/common/hadoop-${HADOOP_VERSION}/hadoop-$HADOOP_VERSION.tar.gz" && \
    # 安装和测试hadoop
    tar zxf "$TAR" && \
    test -d "hadoop-$HADOOP_VERSION" && \
    # 重命名
    ln -sv "hadoop-$HADOOP_VERSION" hadoop && \
    # 删除压缩包
    rm -fv "$TAR" && \
    # 删除文档文件
    { rm -rf hadoop/share/doc; : ; } && \
    # 格式化hdfs
    /hadoop/bin/hdfs namenode -format && \
    # 卸载wget
    yum remove -y wget && \
    yum autoremove -y && \
    # 重新执行一次，确保hostname安装了
    yum install -y hostname && \
    yum clean all && \
    # 清除安装缓存
    rm -rf /var/cache/yum

# 拷贝配置文件到项目下
COPY entrypoint.sh /
COPY conf/core-site.xml /hadoop/etc/hadoop/
COPY conf/hdfs-site.xml /hadoop/etc/hadoop/
COPY conf/yarn-site.xml /hadoop/etc/hadoop/
COPY conf/mapred-site.xml /hadoop/etc/hadoop/
COPY profile.d/hadoop.sh /etc/profile.d/

# 开放端口
# 50070:hdfs
# 8088：mapreduce
EXPOSE 8020 8042 8088 9000 10020 19888 50010 50020 50070 50075 50090

# 容器启动时执行
CMD "/entrypoint.sh"