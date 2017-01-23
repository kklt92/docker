FROM centos:7
MAINTAINER Weihao Ming <mingweihao@gmail.com>

ENV container docker
RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == \
systemd-tmpfiles-setup.service ] || rm -f $i; done); \
rm -f /lib/systemd/system/multi-user.target.wants/*;\
rm -f /etc/systemd/system/*.wants/*;\
rm -f /lib/systemd/system/local-fs.target.wants/*; \
rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
rm -f /lib/systemd/system/basic.target.wants/*;\
rm -f /lib/systemd/system/anaconda.target.wants/*;

RUN yum install -y go \
      git
RUN mkdir /go
ENV GOPATH /go

ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH

RUN mkdir -p "$GOPATH/src" "$GOPATH/bin" && chmod -R 777 "$GOPATH"
WORKDIR $GOPATH

RUN go get github.com/shadowsocks/shadowsocks-go/cmd/shadowsocks-server && \
      go install github.com/shadowsocks/shadowsocks-go/cmd/shadowsocks-server

COPY shadowsocks-config.json /go/

EXPOSE 8388

CMD /go/bin/shadowsocks-server -c /go/shadowsocks-config.json


