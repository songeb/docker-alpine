# docker build --rm -t local/alpine-rails:alpha-1 . 2>&1 | tee ../build.log
FROM alpine:3.13.4
MAINTAINER Alodokter <info@alodokter.com>

ENV RVM_USER    rvm
ENV RVM_GROUP   rvm

# Dependencies for getting/building
RUN apk update && \
    apk upgrade && \
    apk add gcc gnupg curl ruby bash procps musl-dev make linux-headers \
        zlib zlib-dev openssl openssl-dev libressl-dev && \
    gem install rake -N

# User
RUN addgroup $RVM_GROUP && \
    adduser -h /home/$RVM_USER -g 'RVM User' -s /bin/bash -G $RVM_GROUP -D $RVM_USER 

RUN gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 && \
    curl -L -o stable.tar.gz https://github.com/rvm/rvm/archive/stable.tar.gz && \
    gunzip -c stable.tar.gz | tar xf - && \
    cd rvm-stable && ./scripts/install

RUN /bin/bash -l -c 'source /etc/profile.d/rvm.sh'

# make bundler a default gem
RUN echo bundler >> /usr/local/rvm/gemsets/global.gems

# setup some default flags from rvm (auto install, auto gemset create, quiet curl)
RUN echo "rvm_install_on_use_flag=1\nrvm_gemset_create_on_use_flag=1\nrvm_quiet_curl_flag=1" > ~/.rvmrc

# preinstall some ruby versions
ENV PREINSTALLED_RUBIES "2.6.5 2.6.6"
RUN /bin/bash -l -c 'for version in $PREINSTALLED_RUBIES; do echo "Now installing Ruby $version"; rvm install $version; rvm cleanup all; done'

# source rvm in every shell
RUN echo '. /etc/profile.d/rvm.sh\n' >~/.profile

# disable strict host key checking (used for deploy)
RUN mkdir ~/.ssh
RUN echo "Host *\n\tStrictHostKeyChecking no\n\n" > ~/.ssh/config

# login shell by default so rvm is sourced automatically and 'rvm use' can be used
ENTRYPOINT /bin/sh -l
