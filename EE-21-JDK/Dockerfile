FROM ubuntu:22.04

ARG TARGETPLATFORM

MAINTAINER RikoDEV <kontakt@riko.dev>

ENV DEBIAN_FRONTEND=noninteractive
ENV LANG='en_US.UTF-8' LANGUAGE='en_US:en' LC_ALL='en_US.UTF-8'

RUN apt-get update -y \
  && apt-get install -y curl ca-certificates openssl git tar sqlite3 fontconfig tzdata locales iproute2 \
  && echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen \
  && locale-gen en_US.UTF-8 \
  && curl --retry 3 -Lfso /tmp/graalvm.tar.gz https://download1073.mediafire.com/a8vdf6gsd3mg8oozgStPQTd7Uysbxa3LJqRFIaSY46n_tLQyDjKNdeIX1JuMoIB7ihZTHUxRoZE0cDevgOU5ZsOBS-e7hGJWFk__85XiBIxwoXMT-ete6T5wzDVhukQH6l_sziC59NLM31hIlc-DNICYTCvXjXz7OB9B8KrkXmSayQ/6atnvrn7du7me30/graalvm-jdk-21_linux-x64_bin.tar.gz / && mkdir -p /opt/java/graalvm \
  && tar -xf /tmp/graalvm.tar.gz -C /opt/java/graalvm --strip-components=1 \
  && rm -rf /var/lib/apt/lists/* /tmp/graalvm.tar.gz

ENV JAVA_HOME=/opt/java/graalvm \
    PATH="/opt/java/graalvm/bin:$PATH"

RUN useradd -d /home/container -m container

USER container
ENV USER=container HOME=/home/container
WORKDIR /home/container

COPY ./entrypoint.sh /entrypoint.sh

CMD ["/bin/bash", "/entrypoint.sh"]
