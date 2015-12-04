# docker build --rm -t mwvaughn/centos67golang:1.4 .

FROM centos:6.7
MAINTAINER Matthew Vaughn <vaughn@tacc.utexas.edu>

RUN yum -y update && yum -y install \
		gcc-c++ \
		gcc \
		make \
		tar \
	&& yum clean all

ENV GOLANG_VERSION 1.4.3
ENV GOLANG_DOWNLOAD_URL https://golang.org/dl/go$GOLANG_VERSION.src.tar.gz
ENV GOLANG_DOWNLOAD_SHA1 486db10dc571a55c8d795365070f66d343458c48

RUN curl -fsSL "$GOLANG_DOWNLOAD_URL" -o golang.tar.gz \
	&& echo "$GOLANG_DOWNLOAD_SHA1  golang.tar.gz" | sha1sum -c - \
	&& tar -C /usr/src -xzf golang.tar.gz \
	&& rm -rf golang.tar.gz \
	&& cd /usr/src/go/src && ./make.bash --no-clean 2>&1

ENV GOPATH /go
ENV PATH $GOPATH/bin:/usr/src/go/bin:$PATH

RUN mkdir -p "$GOPATH/src" "$GOPATH/bin" && chmod -R 777 "$GOPATH"
WORKDIR $GOPATH

ADD https://raw.githubusercontent.com/docker-library/golang/master/1.4/go-wrapper /usr/local/bin/
RUN chmod a+rx /usr/local/bin/go-wrapper
