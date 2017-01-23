FROM centos:7
MAINTAINER Weihao Ming <mingweihao@gmail.com>

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

CMD /go/bin/shadowsocks-server -c /go/shadowsocks-config.json


