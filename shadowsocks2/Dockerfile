FROM golang:1.16.5-alpine3.14 AS builder

RUN apk upgrade --update \
    && apk add git \
    && if [ "$(arch)" = "x86_64" ] ; then export GOARCH=amd64;fi \
    && if [ "$(arch)" = "aarch64" ] ; then export GOARCH=arm64;fi \
    && if [ "$(arch)" = "arm" ] ; then export GOARCH=arm GOARM=7;fi \
    && export GOOS=linux \
    && export CGO_ENABLED=0 \
    && export \
    && go get -ldflags '-w -s' \
         github.com/shadowsocks/go-shadowsocks2

FROM alpine:3.14

LABEL maintainer="mritd <mritd1234@gmail.com>"

ARG TZ="Asia/Shanghai"

ENV TZ ${TZ}

RUN apk upgrade --update \
    && apk add bash tzdata \
    && ln -sf /usr/share/zoneinfo/${TZ} /etc/localtime \
    && echo ${TZ} > /etc/timezone \
    && rm -rf /var/cache/apk/*

COPY --from=builder /go/bin/go-shadowsocks2 /usr/bin/shadowsocks

ADD entrypoint.sh /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
