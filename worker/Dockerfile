FROM scidas/slurm.base:20.11.9
MAINTAINER Michael J. Stealey <stealey@renci.org>

# install openmpi 3.0.1
RUN yum makecache --refresh
RUN yum -y install \
  gcc-c++ \
  gcc-gfortran \
  && yum -y localinstall \
  /packages/openmpi-*.rpm



# install Lmod 7.7i
RUN dnf --enablerepo=powertools -y install lua-devel lua-posix lua-filesystem expect
RUN yum -y install \
  lua \
  wget \
  bzip2 \
  make 
#  && wget https://sourceforge.net/projects/lmod/files/Lmod-7.7.tar.bz2 \
#  && tar -xjvf Lmod-7.7.tar.bz2
#WORKDIR /Lmod-7.7
#RUN ./configure --prefix=/opt/apps \
 # && make install \
 # && ln -s /opt/apps/lmod/lmod/init/profile /etc/profile.d/z00_lmod.sh \
 # && ln -s /opt/apps/lmod/lmod/init/cshrc /etc/profile.d/z00_lmod.csh

WORKDIR /home/worker

# clean up
RUN rm -f /packages/slurm-*.rpm /packages/openmpi-*.rpm \
  && yum clean all \
  && rm -rf /var/cache/yum 
 # && rm -f /Lmod-7.7.tar.bz2

COPY docker-entrypoint.sh /docker-entrypoint.sh
RUN chmod +x /docker-entrypoint.sh
ENTRYPOINT ["/usr/local/bin/tini", "--", "/docker-entrypoint.sh"]

