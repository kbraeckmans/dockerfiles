FROM alpine:latest
MAINTAINER Kenny Braeckmans <kbraeckmans@zerolabs.org>

RUN apk add --update curl python \
    && rm -rf /var/cache/apk/* \
    && curl https://yt-dl.org/latest/youtube-dl -o /usr/local/bin/youtube-dl \
    && chmod a+rx /usr/local/bin/youtube-dl

WORKDIR /root

ENTRYPOINT ["/usr/local/bin/youtube-dl"]
