FROM ubuntu:22.04 AS builder

RUN apt-get update -y && \
    apt-get install -y --no-install-recommends \
    bc                  \
    bison               \
    build-essential     \
    gcc                 \
    flex                \
    git                 \
    libelf-dev          \
    libncurses-dev      \
    libssl-dev          \
    ca-certificates     \
    kmod                \
    curl                \
    wget

ENV SRC_DIR=/usr/src            \
    DIST_DIR=/dist              \
    LINUX_DIR=/usr/src/linux    \
    LINUX_REPO_URL=git://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git


ARG KERNEL_VERSION

RUN mkdir -p ${SRC_DIR} ${DIST_DIR} && \
    git clone --depth 1 --branch v${KERNEL_VERSION} ${LINUX_REPO_URL} ${LINUX_DIR} && \
    cd ${LINUX_DIR}

WORKDIR ${LINUX_DIR}

ARG KERNEL_CONFIG

RUN curl -L -o microvm-kernel.config ${KERNEL_CONFIG}
COPY k8s_additions.config .
RUN ./scripts/kconfig/merge_config.sh -m microvm-kernel.config k8s_additions.config

# Could also be done like this
# RUN curl -L -o .config ${KERNEL_CONFIG}
# RUN ./scripts/config --file .config \
#     --enable CONFIG_NETFILTER \
#     --enable CONFIG_NETFILTER_ADVANCED \
#     --enable CONFIG_NETFILTER_XT_TARGET_REDIRECT \
#     --enable CONFIG_NETFILTER_XT_MATCH_COMMENT \
#     --enable  CONFIG_NETFILTER_XT_TARGET_MARK \
#     --enable CONFIG_IP_SET \
#     --enable CONFIG_NF_CONNTRACK \
#     --enable CONFIG_NF_CONNTRACK_MARK \
#     --enable CONFIG_NF_CONNTRACK_SECMARK \
#     --enable CONFIG_NF_CONNTRACK_PROCFS \
#     --enable CONFIG_NF_NAT \
#     --enable CONFIG_NF_NAT_REDIRECT \
#     --enable CONFIG_NF_NAT_MASQUERADE \
#     --enable CONFIG_NETFILTER_XTABLES \
#     --enable CONFIG_KEYS \
#     --enable CONFIG_IP_NF_TARGET_MASQUERADE \
#     --enable CONFIG_NETFILTER_XT_MATCH_ADDRTYPE \
#     --enable CONFIG_NETFILTER_XT_MATCH_CONNTRACK \
#     --enable CONFIG_NETFILTER_XT_MATCH_IPVS \
#     --enable CONFIG_NETFILTER_XT_MATCH_MULTIPORT \
#     --enable CONFIG_IP_NF_NAT



RUN make LOCALVERSION= olddefconfig
RUN make LOCALVERSION= -j32

RUN cp vmlinux /boot/vmlinux && \
    cp .config /boot/config-${KERNEL_VERSION}

FROM scratch
LABEL org.opencontainers.image.source=https://github.com/liquidmetal-dev/mikrolite-images
COPY --from=builder /boot /boot