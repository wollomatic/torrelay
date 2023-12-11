FROM ubuntu:jammy

LABEL maintainer="Wollomatic <gh2022@wollomatic.de>"
LABEL org.opencontainers.image.source=https://github.com/wollomatic/torrelay
LABEL org.opencontainers.image.description="Tor relay in a ubuntu docker image"
LABEL org.opencontainers.image.licenses=MIT
LABEL securitytxt="https://wollomatic.de/.well-known/security.txt"
VOLUME ["/etc/tor", "/var/lib/tor"]

ENTRYPOINT [ "/usr/bin/tini", "--" ]
CMD [ "/usr/sbin/tor", "-f", "/etc/tor/torrc" ]

ARG TARGETARCH

RUN apt-get update \
 && apt-get upgrade -y \
 && apt-get install -y \
    apt-transport-https \
    wget \
    gpg \
    gpg-agent \
    ca-certificates \
    tini \
    --no-install-recommends \
 && wget -qO- https://deb.torproject.org/torproject.org/A3C4F0F979CAA22CDBA8F512EE8CBC9E886DDD89.asc | gpg --dearmor | tee /usr/share/keyrings/tor-archive-keyring.gpg \
 && printf "deb [arch=${TARGETARCH} signed-by=/usr/share/keyrings/tor-archive-keyring.gpg] https://deb.torproject.org/torproject.org jammy main\n" >> /etc/apt/sources.list.d/tor.list \
 && apt-get update \
 && apt-get install -y \
    tor=0.4.8.10-1~jammy+1 \
    tor-geoipdb=0.4.8.10-1~jammy+1 \
    --no-install-recommends \
 && apt-get purge -y \
    wget \
    curl \
    gpg \
    gpg-agent \
 && apt-get autoremove -y \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* \
 && chown debian-tor:debian-tor /etc/tor

USER debian-tor