# DEPRECATED!
# The last official release of obfs4proxy was 0.0.14 in 2022.
# There are several security issues in obfs4proxy right now, so I decided to deprecate this image.

FROM  --platform=$BUILDPLATFORM golang:1.21-bookworm AS obfs4build
RUN git clone -b obfs4proxy-0.0.14 --single-branch https://gitlab.com/yawning/obfs4.git
WORKDIR /go/obfs4/
ARG TARGETOS
ARG TARGETARCH
RUN GOOS=$TARGETOS GOARCH=$TARGETARCH go build -o obfs4proxy/obfs4proxy ./obfs4proxy

FROM wollomatic/torrelay:0.4.8.10
LABEL org.opencontainers.image.description="obfs4proxy in a ubuntu docker image"
COPY --from=obfs4build /go/obfs4/obfs4proxy/obfs4proxy /usr/bin/
