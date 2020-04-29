FROM registry.access.redhat.com/ubi8/ubi

WORKDIR /root 

ENV DRIVER_VERSION=4.7-1.0.0.1

ENV MLX=MLNX_OFED_LINUX-${DRIVER_VERSION}-rhel8.0-x86_64

RUN dnf -y install make gcc wget perl createrepo kernel-devel  pciutils python36-devel ethtool lsof elfutils-libelf-devel rpm-build kernel-rpm-macros python36 tk numactl-libs libmnl tcl binutils kmod procps git autoconf automake libtool 

RUN mkdir /lib/modules/$(uname -r)
RUN ln -s /usr/src/kernels/$(uname -r) /lib/modules/$(uname -r)/build
RUN touch /lib/modules/$(uname -r)/modules.order
RUN touch /lib/modules/$(uname -r)/modules.builtin

RUN wget http://content.mellanox.com/ofed/MLNX_OFED-${DRIVER_VERSION}/${MLX}.tgz

RUN tar xf ${MLX}.tgz

WORKDIR ${MLX}

RUN ./mlnxofedinstall --upstream-libs --dpdk --with-mft --add-kernel-support

