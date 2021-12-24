# Use phusion/passenger-full as base image. To make your builds reproducible, make
# sure you lock down to a specific version, not to `latest`!
# See https://github.com/phusion/passenger-docker/blob/master/CHANGELOG.md for
# a list of version numbers.
FROM phusion/passenger-ruby26:1.0.13
MAINTAINER Alodokter <info@alodokter.com>

# Set correct environment variables.
ENV HOME /root

# Update OS - security update
# RUN apt-get update && apt-get upgrade -y -o Dpkg::Options::="--force-confold"

# Use baseimage-docker's init process.
CMD ["/sbin/my_init"]

# Enable nginx
RUN rm -f /etc/service/nginx/down

RUN rm /etc/nginx/sites-enabled/default
ADD webapp.conf /etc/nginx/sites-enabled/webapp.conf
RUN --chown=app:app mkdir /home/app/webapp
COPY --chown=app:app index.html /home/app/webapp

# ...put your own build instructions here...

# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
