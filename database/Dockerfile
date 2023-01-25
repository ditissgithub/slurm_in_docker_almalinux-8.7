FROM scidas/slurm.base:20.11.9
MAINTAINER Michael J. Stealey <stealey@renci.org>

ENV DBD_ADDR=database \
  DBD_HOST=database \
  DBD_PORT=6819 \
  STORAGE_HOST=database.local.dev \
  STORAGE_PORT=3306 \
  STORAGE_PASS=password \
  STORAGE_USER=slurm

RUN wget https://github.com/krallin/tini/releases/download/v0.19.0/tini_0.19.0.rpm
RUN yum -y  install tini_0.19.0.rpm
RUN cp /usr/bin/tini* /usr/local/bin/

# clean up
RUN rm -f /packages/slurm-*.rpm /packages/openmpi-*.rpm \
  && yum clean all \
  && rm -rf /var/cache/yum

COPY docker-entrypoint.sh /docker-entrypoint.sh

RUN chmod +x /docker-entrypoint.sh

ENTRYPOINT ["/usr/local/bin/tini", "--", "/docker-entrypoint.sh"]
