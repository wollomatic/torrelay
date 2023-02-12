FROM  --platform=$BUILDPLATFORM golang:1.19-bullseye AS obfs4build
RUN git clone -b obfs4proxy-0.0.14 --single-branch https://gitlab.com/yawning/obfs4.git
WORKDIR /go/obfs4/
ARG TARGETOS TARGETARCH
RUN GOOS=$TARGETOS GOARCH=$TARGETARCH go build -o obfs4proxy/obfs4proxy ./obfs4proxy

FROM wollomatic/torrelay:0.4.7.13
LABEL org.opencontainers.image.description="obfs4proxy in a ubuntu docker image"
COPY --from=obfs4build /go/obfs4/obfs4proxy/obfs4proxy /usr/bin/
