FROM debian:jessie
MAINTAINER Kenny Braeckmans <kbraeckmans@zerolabs.org>

RUN echo "deb http://deb.torproject.org/torproject.org jessie main" >> /etc/apt/sources.list
RUN echo "deb-src http://deb.torproject.org/torproject.org jessie main" >> /etc/apt/sources.list
RUN gpg --keyserver keys.gnupg.net --recv 886DDD89
RUN gpg --export A3C4F0F979CAA22CDBA8F512EE8CBC9E886DDD89 | apt-key add -
RUN apt-get update && apt-get install -y \
	ca-certificates \
	curl \
	libasound2 \
	libdbus-glib-1-2 \
	libgtk2.0-0 \
	libxrender1 \
	libxt6 \
	xz-utils \
        tor \
        deb.torproject.org-keyring \
	--no-install-recommends \
	&& rm -rf /var/lib/apt/lists/*

ENV HOME /home/user
RUN useradd --create-home --home-dir $HOME user \
	&& chown -R user:user $HOME

ENV LANG C.UTF-8

ENV TOR_VERSION 5.0.4
ENV TOR_LANG en_US
ENV TOR_FINGERPRINT 0x4E2C6E8793298290

# download tor and check signature
RUN cd /tmp \
	&& curl -sSOL "https://www.torproject.org/dist/torbrowser/${TOR_VERSION}/tor-browser-linux64-${TOR_VERSION}_${TOR_LANG}.tar.xz" \
	&& curl -sSOL "https://www.torproject.org/dist/torbrowser/${TOR_VERSION}/tor-browser-linux64-${TOR_VERSION}_${TOR_LANG}.tar.xz.asc" \
	&& mkdir ~/.gnupg \
	&& gpg --keyserver x-hkp://pool.sks-keyservers.net --recv-keys ${TOR_FINGERPRINT} \
	&& gpg --fingerprint ${TOR_FINGERPRINT} | grep "Key fingerprint = EF6E 286D DA85 EA2A 4BA7  DE68 4E2C 6E87 9329 8290" \
	&& gpg --verify tor-browser-linux64-${TOR_VERSION}_${TOR_LANG}.tar.xz.asc \
	&& tar -vxJ --strip-components 1 -C /usr/local/bin -f tor-browser-linux64-${TOR_VERSION}_${TOR_LANG}.tar.xz \
	&& rm -rf tor-browser* \
	&& rm -rf ~/.gnupg


# good fonts
COPY local.conf /etc/fonts/local.conf

WORKDIR $HOME
USER user

#ENTRYPOINT ["/bin/bash"]
CMD [ "/usr/local/bin/Browser/start-tor-browser" ]
