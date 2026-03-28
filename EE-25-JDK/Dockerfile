FROM ubuntu:22.04

ARG TARGETPLATFORM

MAINTAINER RikoDEV <kontakt@riko.dev>

ENV DEBIAN_FRONTEND=noninteractive
ENV LANG='en_US.UTF-8' LANGUAGE='en_US:en' LC_ALL='en_US.UTF-8'

RUN apt-get update -y \
  && apt-get install -y curl ca-certificates openssl git tar sqlite3 fontconfig tzdata locales iproute2 \
  && echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen \
  && locale-gen en_US.UTF-8 \
  && curl --retry 3 -Lfso /tmp/graalvm.tar.gz https://download1523.mediafire.com/g15hpfdma9jgWa-FEB6y2he3gr9zJ6bZpQgx6dkp8QE70KPP6RXxaGBLuVaMb8H4XXSUHBVED9LahA_xsh-RnlWr0fBZgUM8u6YyPKG7ZVhCgy5VQSuu9XPhJU_A6NDWWmBXyqS1smG4bfCSPFU9YI0eUnhrchhlbZlcd8HWD-jlpg/lpvojd47kdh5icp/graalvm-jdk-25_linux-x64_bin.tar.gz \
  && mkdir -p /opt/java/graalvm \
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
