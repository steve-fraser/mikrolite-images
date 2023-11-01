ARG RKE2_VERSION="v1.28.3+rke2r1"

FROM ubuntu:22.04
LABEL org.opencontainers.image.source=https://github.com/mikrolite/images

RUN apt-get update && apt-get install -y \
    kmod \
    dbus \
    iproute2 \
    iputils-ping \
    net-tools \
    openssh-server \
    dnsutils \
    sudo \
    curl \
    cloud-init \
    linux-image-virtual  \
    less \
    udev \
    wget \
    apt-transport-https \
    ca-certificates \
    gnupg2 \
    software-properties-common \
    libseccomp2 \
    systemd \
    jq && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    sed -i -e 's/^AcceptEnv LANG LC_\*$/#AcceptEnv LANG LC_*/' /etc/ssh/sshd_config

RUN mkdir -p /var/lib/rancher/rke2/agent/images/
RUN curl -Lo /var/lib/rancher/rke2/agent/images/rke2-images.linux-arm64.tar.gz https://github.com/rancher/rke2/releases/download/${RKE2_VERSION}/rke2-images.linux-arm64.tar.gz