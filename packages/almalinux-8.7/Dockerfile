FROM almalinux:8.7
MAINTAINER Michael J. Stealey <stealey@renci.org>

ENV SLURM_VERSION=20.11.9

RUN yum makecache --refresh
RUN yum -y install \
  drpm \
  epel-release \
  && yum -y install \
  which \
  wget \
  munge \
  munge-libs \
  python3

RUN dnf --enablerepo=powertools -y install munge-devel hwloc-devel openssl-devel libssh2-devel lua-devel  rrdtool-devel  gtk2-devel perl-Switch \
  && yum -y install \
  rpm-build \
  gcc \
  openssl \
  pam-devel \
  numactl \
  numactl-devel \
  hwloc \
  lua \
  readline-devel \
  ncurses-devel \
  man2html \
  libibmad \
  libibumad \
  perl-ExtUtils-MakeMaker \
  mariadb-server \
  mariadb-devel \
  && yum -y group install "Development Tools"

COPY docker-entrypoint.sh /docker-entrypoint.sh
RUN chmod +x /docker-entrypoint.sh
VOLUME ["/packages"]
ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["ls", "-alh", "/packages"]

