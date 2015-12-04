# docker build --rm -t mwvaughn/rktdev:v0.12.1 .

FROM mwvaughn/centos67golang:1.4
MAINTAINER Matthew Vaughn <vaughn@tacc.utexas.edu>

# apt-get update && apt-get install -y coreutils cpio squashfs-tools realpath autoconf file xz-utils patch bc

RUN yum -y update && \
    yum -y install curl \
    wget coreutils cpio \
    squashfs-tools autoconf \
    automake aclocal \
    file glibc-static \
    patch bc xz \
    curl-devel expat-devel \
    gettext-devel openssl-devel \
    zlib-devel perl-ExtUtils-MakeMaker && \
    yum clean all

RUN curl -sk -O -L "http://pkgs.repoforge.org/realpath/realpath-1.17-1.el6.rf.x86_64.rpm" && rpm -ivh realpath-1.17-1.el6.rf.x86_64.rpm && rm -rf realpath-1.17-1.el6.rf.x86_64.rpm

WORKDIR /home

RUN curl -sk -O -L "https://www.kernel.org/pub/software/scm/git/git-2.6.3.tar.gz" && \
    tar xvf git-2.6.3.tar.gz && \
    cd git-2.6.3 && \
    make prefix=/usr/local/git all && \
    make prefix=/usr/local/git install && \
    echo "export PATH=$PATH:/usr/local/git/bin" >> /etc/bashrc && \
    cd /home && rm -rf git-2.6.3 git-2.6.3.tar.gz

ENV PATH /usr/local/git/bin:$PATH
WORKDIR /home

RUN yum -y update && \
    yum -y install centos-release-SCL && \
    curl -skL -O "http://ftp.scientificlinux.org/linux/scientific/5x/x86_64/RPM-GPG-KEYs/RPM-GPG-KEY-cern" && \
    wget -O /etc/yum.repos.d/slc6-devtoolset.repo http://linuxsoft.cern.ch/cern/devtoolset/slc6-devtoolset.repo && \
    yum -y install devtoolset-2 && \
    yum clean all

