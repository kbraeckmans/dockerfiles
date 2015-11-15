FROM alpine:latest
MAINTAINER Kenny Braeckmans <kbraeckmans@zerolabs.org>

RUN apk add --update curl \
    && rm -rf /var/cache/apk/* \
    && curl -L https://github.com/andreimarcu/linx-server/releases/download/v1.1.6/linx-server-v1.1.6_linux-amd64 -o /usr/local/bin/linx-server \
    && chmod a+rx /usr/local/bin/linx-server

EXPOSE  8080
ENTRYPOINT ["/usr/local/bin/linx-server"]
