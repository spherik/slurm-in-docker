FROM scidas/slurm.base:17.11.5
MAINTAINER Michael J. Stealey <stealey@renci.org>

# install openmpi 3.0.1
RUN yum -y install \
  gcc-c++ \
  gcc-gfortran \
  python36-setuptools \
  && easy_install-3.6 pip \
  && yum -y localinstall \
  /packages/openmpi-*.rpm

RUN pip3 install mne nilearn matplotlib scipy

# install Lmod 7.7
RUN yum -y install \
  lua-posix \
  lua \
  lua-filesystem \
  lua-devel \
  wget \
  bzip2 \
  expectk \
  make \
  && wget https://sourceforge.net/projects/lmod/files/Lmod-7.7.tar.bz2 \
  && tar -xjvf Lmod-7.7.tar.bz2
WORKDIR /Lmod-7.7
RUN ./configure --prefix=/opt/apps \
  && make install \
  && ln -s /opt/apps/lmod/lmod/init/profile /etc/profile.d/z00_lmod.sh \
  && ln -s /opt/apps/lmod/lmod/init/cshrc /etc/profile.d/z00_lmod.csh

WORKDIR /home/worker

# clean up
RUN rm -f /packages/slurm-*.rpm /packages/openmpi-*.rpm \
  && yum clean all \
  && rm -rf /var/cache/yum \
  && rm -f /Lmod-7.7.tar.bz2

COPY docker-entrypoint.sh /docker-entrypoint.sh

ENTRYPOINT ["/usr/local/bin/tini", "--", "/docker-entrypoint.sh"]
