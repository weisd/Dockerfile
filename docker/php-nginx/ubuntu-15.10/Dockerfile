#++++++++++++++++++++++++++++++++++++++
# Ubuntu 15.10 PHP-Nginx Docker container
#++++++++++++++++++++++++++++++++++++++

FROM webdevops/php:ubuntu-15.10
MAINTAINER info@webdevops.io
LABEL vendor=WebDevOps.io
LABEL io.webdevops.layout=6
LABEL io.webdevops.version=0.23.0

ENV WEB_DOCUMENT_ROOT  /app
ENV WEB_DOCUMENT_INDEX index.php
ENV WEB_ALIAS_DOMAIN   *.vm

# Install nginx
RUN /usr/local/bin/apt-install \
        nginx \
	&& ln -sf /opt/docker/etc/nginx/vhost.conf /etc/nginx/conf.d/10-docker.conf

# Deploy scripts/configurations
COPY conf/ /opt/docker/
RUN bash /opt/docker/bin/control.sh provision.role.bootstrap webdevops-nginx \
    && bash /opt/docker/bin/control.sh provision.role.bootstrap webdevops-php-nginx \
    && bash /opt/docker/bin/bootstrap.sh

EXPOSE 80 443

CMD ["supervisord"]
