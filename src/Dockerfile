FROM alpine:3.12 as rootfs-stage

ENV REL=bionic
ENV ARCH=amd64

RUN \
 apk add --no-cache \
        bash \
        curl \
        tzdata \
        xz

RUN \
 mkdir /root-out && \
 curl -o \
        /rootfs.tar.gz -L \
        https://partner-images.canonical.com/core/${REL}/current/ubuntu-${REL}-core-cloudimg-${ARCH}-root.tar.gz && \
 tar xf \
        /rootfs.tar.gz -C \
        /root-out

FROM scratch
COPY --from=rootfs-stage /root-out/ /
ARG BUILD_DATE
ARG VERSION
LABEL build_version="fossy.my.id base image version:- ${VERSION} Build-date:- ${BUILD_DATE}"
LABEL maintainer="Fossyy"

ARG DEBIAN_FRONTEND="noninteractive"
ENV HOME="/root" \
LANGUAGE="en_US.UTF-8" \
LANG="en_US.UTF-8" \
TERM="xterm"

COPY sources.list /etc/apt/

ENTRYPOINT ["bash"]
