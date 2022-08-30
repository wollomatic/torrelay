FROM ubuntu:focal

LABEL maintainer="Wollomatic <gh2022@wollomatic.de>"

VOLUME ["/etc/tor", "/var/lib/tor"]

SHELL ["/bin/bash", "-o", "pipefail", "-c"]
RUN apt-get update \
 && apt-get install -y \
    apt-transport-https \
    wget \
    gpg \
    gpg-agent \
    ca-certificates \
    tini \
    --no-install-recommends \
 && wget -qO- https://deb.torproject.org/torproject.org/A3C4F0F979CAA22CDBA8F512EE8CBC9E886DDD89.asc | gpg --dearmor | tee /usr/share/keyrings/tor-archive-keyring.gpg \
 && printf "deb [arch=amd64 signed-by=/usr/share/keyrings/tor-archive-keyring.gpg] https://deb.torproject.org/torproject.org focal main\n" >> /etc/apt/sources.list.d/tor.list \
 && apt-get update \
 && apt-get install -y \
    tor \
    tor-geoipdb \
    --no-install-recommends \
 && apt-get purge -y \
    wget \
    gpg \
    gpg-agent \
 && apt-get autoremove -y \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* \
 && chown debian-tor:debian-tor /etc/tor

USER debian-tor

ENTRYPOINT [ "/usr/bin/tini", "--" ]

CMD [ "/usr/sbin/tor", "-f", "/etc/tor/torrc" ]
