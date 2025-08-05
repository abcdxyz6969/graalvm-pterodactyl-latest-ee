FROM ubuntu:22.04

ARG TARGETPLATFORM
ARG GRAAL_VERSION=21
ARG JAVA_VERSION=21

MAINTAINER RikoDEV, <kontakt@riko.dev>

ENV DEBIAN_FRONTEND=noninteractive

# Default to UTF-8 file.encoding
ENV LANG='en_US.UTF-8' LANGUAGE='en_US:en' LC_ALL='en_US.UTF-8'

RUN apt-get update -y \
  && apt-get install -y curl ca-certificates openssl git tar sqlite3 fontconfig tzdata locales iproute2 \
  && echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen \
  && locale-gen en_US.UTF-8 \
  && case ${TARGETPLATFORM} in \
         "linux/amd64")  ARCH=linux-amd64  ;; \
         "linux/arm64")  ARCH=linux-aarch64  ;; \
    esac \
  && curl --retry 3 -Lfso /tmp/graalvm.tar.gz https://download850.mediafire.com/y5pesgbd5engvTVU9dA4XcqQAv6I4ooSeunyIeXD9sJ9kA00_17mGE5R28NEzXE5IjLpooUFHABfMbYE2KpbFJ6Sd5fjHRQy3VpgFN5exvN3xQMJ8R-U1As-nMMNhDEn_dkj9Ke44692rpt7YefGahFK_EBjJJ_mP8DHeasgWjG5/6atnvrn7du7me30/graalvm-jdk-21_linux-x64_bin.tar.gz \
  && mkdir -p /opt/java/graalvm \
  && cd /opt/java/graalvm \
  && tar -xf /tmp/graalvm.tar.gz --strip-components=1 \
  && export PATH="/opt/java/graalvm/bin:$PATH" \
  && rm -rf /var/lib/apt/lists/* \
  && rm -rf /tmp/graalvm.tar.gz

ENV JAVA_HOME=/opt/java/graalvm \
    PATH="/opt/java/graalvm/bin:$PATH"

# Step 2 - add pterodactyl stuff
RUN useradd -d /home/container -m container

USER        container
ENV         USER=container HOME=/home/container

WORKDIR     /home/container

COPY        ./entrypoint.sh /entrypoint.sh

CMD         ["/bin/bash", "/entrypoint.sh"]

