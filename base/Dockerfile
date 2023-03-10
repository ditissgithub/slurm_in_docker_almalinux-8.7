FROM almalinux:8.7
MAINTAINER Michael J. Stealey <stealey@renci.org>

ENV SLURM_VERSION=20.11.9 \
  MUNGE_UID=981 \
  SLURM_UID=982 \
  WORKER_UID=1000

RUN groupadd -g $MUNGE_UID munge \
  && useradd  -m -c "MUNGE Uid 'N' Gid Emporium" -d /var/lib/munge -u $MUNGE_UID -g munge  -s /sbin/nologin munge \
  && groupadd -g $SLURM_UID slurm \
  && useradd  -m -c "Slurm workload manager" -d /var/lib/slurm -u $SLURM_UID -g slurm  -s /bin/bash slurm \
  && groupadd -g $WORKER_UID worker \
  && useradd  -m -c "Workflow user" -d /home/worker -u $WORKER_UID -g worker  -s /bin/bash worker

# install packages for general functionality
RUN yum makecache --refresh
RUN dnf --enablerepo=powertools -y install  mariadb-devel munge-devel perl-Switch

RUN yum -y install \
  epel-release \
  && yum -y install \
  sudo \
  wget \
  passwd \
  procps-ng \
  dhcp-client \
  net-tools \
  which \
  tree \
  mariadb-server \
  munge \
  munge-libs \
  openssh-server \
  openssh-clients

# install slurm 20.11.9
COPY rpms /packages
# /usr/bin/mpiexec from slurm-torque conflicts with openmpi install
WORKDIR /packages
RUN yum -y localinstall $(ls | grep -v -e 'torque' -e 'openmpi')
WORKDIR /

VOLUME ["/home", "/.secret"]

#   22:         SSH
# 3306:         MariaDB
# 6817:         Slurm Ctl D
# 6818:         Slurm D
# 6819:         Slurm DBD
EXPOSE 22 3306 6817 6818 6819

