#++++++++++++++++++++++++++++++++++++++
# Ubuntu 15.10 Base Docker container
#++++++++++++++++++++++++++++++++++++++

FROM webdevops/bootstrap:ubuntu-15.10
MAINTAINER info@webdevops.io
LABEL vendor=WebDevOps.io
LABEL io.webdevops.layout=6
LABEL io.webdevops.version=0.23.0

ENV DOCKER_CONF_HOME  /opt/docker/

# Install services
RUN /usr/local/bin/apt-install \
    supervisor \
    syslog-ng \
    syslog-ng-core \
    logrotate \
    cron \
    wget \
    curl \
    net-tools

# Deploy scripts/configurations
COPY conf/ /opt/docker/
RUN bash /opt/docker/bin/control.sh provision.role.bootstrap webdevops-base \
    && bash /opt/docker/bin/control.sh provision.role.finish.build webdevops-cleanup \
    && bash /opt/docker/bin/bootstrap.sh

ENTRYPOINT ["/opt/docker/bin/entrypoint.sh"]
CMD ["noop"]
