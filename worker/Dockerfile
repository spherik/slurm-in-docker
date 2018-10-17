FROM specsbcn/ubuntu_slurm.base:0.2
MAINTAINER Michael J. Stealey <stealey@renci.org>

# install openmpi 3.0.1
RUN apt -y install \
  build-essential \
  openmpi-bin libopenmpi-dev \
  python3-pip

RUN pip3 install --upgrade pip
RUN pip3 install -U mne nilearn matplotlib scipy

WORKDIR /home/worker

# clean up
RUN apt clean

COPY docker-entrypoint.sh /docker-entrypoint.sh

ENTRYPOINT ["/usr/local/bin/tini", "--", "/docker-entrypoint.sh"]
