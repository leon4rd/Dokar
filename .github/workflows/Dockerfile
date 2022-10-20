FROM ubuntu:latest
MAINTAINER leon4rd <leon4rd@github.com>

ENV \
    CCACHE_SIZE=20G \
    CCACHE_DIR=/srv/ccache \
    USE_CCACHE=1 \
    CCACHE_COMPRESS=1 \
    PATH=$PATH:/usr/local/bin/

RUN apt update && apt upgrade -y && \
    apt install --no-install-recommends -y \
    debian-keyring \
    debian-archive-keyring \
    git

ARG hostuid=1000
ARG hostgid=1000

RUN git config --global user.name "leon4rd"
RUN git config --global user.email "apalotega02@gmail.com"
RUN git config --global credential.helper store

RUN \
    groupadd --gid $hostgid --force build && \
    useradd --gid $hostgid --uid $hostuid --non-unique build && \
    rsync -a /etc/skel/ /home/build/

RUN curl https://storage.googleapis.com/git-repo-downloads/repo > /usr/local/bin/repo \
    && chmod a+x /usr/local/bin/repo

RUN echo "build ALL=NOPASSWD: ALL" > /etc/sudoers.d/build

RUN chown -R build:build /home/build

VOLUME /home/build/android
VOLUME /srv/ccache

USER build
WORKDIR /home/build/android

RUN git clone https://github.com/akhilnarang/scripts && cd scripts && bash setup/android_build_env.sh

RUN rm -rf /var/lib/apt/lists /var/cache/apt/archives /tmp scripts
