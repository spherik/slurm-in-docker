FROM specsbcn/ubuntu_slurm.base:0.2
MAINTAINER Michael J. Stealey <stealey@renci.org>

# install openmpi 3.0.1
RUN apt -y install \
  build-essential \
  openmpi-bin libopenmpi-dev

RUN apt -y install \
  nano \
  wget \
  bzip2

# install Lmod 7.7
#RUN yum -y install \
#  lua-posix \
#  lua \
#  lua-filesystem \
#  lua-devel \
#  wget \
#  bzip2 \
#  expectk \
#  nano \
#  make \
#  && wget https://sourceforge.net/projects/lmod/files/Lmod-7.7.tar.bz2 \
#  && tar -xjvf Lmod-7.7.tar.bz2
#WORKDIR /Lmod-7.7
#RUN ./configure --prefix=/opt/apps \
#  && make install \
#  && ln -s /opt/apps/lmod/lmod/init/profile /etc/profile.d/z00_lmod.sh \
#  && ln -s /opt/apps/lmod/lmod/init/cshrc /etc/profile.d/z00_lmod.csh

WORKDIR /

ENV USE_SLURMDBD=true \
  CLUSTER_NAME=snowflake \
  CONTROL_MACHINE=controller \
  SLURMCTLD_PORT=6817 \
  SLURMD_PORT=6818 \
  ACCOUNTING_STORAGE_HOST=database \
  ACCOUNTING_STORAGE_PORT=6819 \
  PARTITION_NAME=docker

# clean up
#RUN rm -f /packages/slurm-*.rpm /packages/openmpi-*.rpm \
#  && yum clean all \
#  && rm -rf /var/cache/yum \
#  && rm -f /Lmod-7.7.tar.bz2
RUN apt clean

COPY docker-entrypoint.sh /docker-entrypoint.sh

ENTRYPOINT ["/usr/local/bin/tini", "--", "/docker-entrypoint.sh"]
