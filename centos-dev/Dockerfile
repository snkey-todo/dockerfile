# 继承
FROM zhushengdocker/centos-java:jdk8

# 维护者信息
MAINTAINER zhusheng 1537017271@qq.com

# 描述信息
LABEL Description="CentOS Dev Build"

# 添加环境变量
ENV GRADLE_HOME=/opt/gradle
ENV JYTHON_HOME=/opt/jython
ENV PATH $PATH:$GRADLE_HOME/bin:$JYTHON_HOME/bin

# 安装
RUN set -euxo pipefail && \
    yum update -y && \
    yum install -y \
    curl \
    cyrus-sasl-devel \
    dstat \
    expat-devel \
    expect \
    ethtool \
    gcc \
    gcc-c++ \
    git \
    groovy \
    hostname \
    libev \
    libev-devel \
    make \
    maven \
    mysql-devel \
    net-tools \
    openssl-devel \
    perl \
    perl-CPAN \
    perl-DBD-MySQL \
    perl-libwww-perl \
    python-devel \
    python-pip \
    python-setuptools \
    ruby \
    ruby-devel \
    snappy-devel \
    sysstat \
    tar \
    unzip \
    vim-enhanced \
    wget \
    which \
    yum-plugin-security \
    yum-security \
    zip \
    epel-release && \
    yum install -y jwhois && \
    curl -L https://bintray.com/sbt/rpm/rpm | tee /etc/yum.repos.d/bintray-sbt-rpm.repo && \
    yum install -y --nogpgcheck sbt && \
    yum autoremove -y && \
    yum clean all && \
    rm -rf /var/cache/yum && \
    # workaround for CentOS (found via strace) otherwise incorrectly states "Warning: You do not have write permission for Perl library directories." and local::lib hits use of uninitialized variables errors in base modules like even core File::Basename :-/
    mkdir -v /usr/local/share/perl5 /usr/local/lib64/perl5

# Gradle doesn't have an RPM :-(
RUN set -euxo pipefail && \
    wget https://raw.githubusercontent.com/HariSekhon/bash-tools/master/install_gradle.sh && \
    bash install_gradle.sh && \
    rm -f install_gradle.sh

# Jython
RUN set -euxo pipefail && \
    wget https://raw.githubusercontent.com/HariSekhon/pytools/master/jython_install.sh && \
    wget https://raw.githubusercontent.com/HariSekhon/pytools/master/jython_autoinstall.exp && \
    bash jython_install.sh && \
    rm -f jython_install.sh jython_autoinstall.exp

CMD /bin/bash