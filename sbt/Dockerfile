FROM anapsix/alpine-java:jdk8
MAINTAINER Juliano Alves <von.juliano@gmail.com>

ENV SBT_VERSION=0.13.13
ENV SBT_HOME /usr/local/sbt
ENV PATH $PATH:$SBT_HOME/bin

ENV http_proxy http://192.168.65.1:8099
ENV https_proxy http://192.168.65.1:8099

WORKDIR /usr/local

RUN apk update && \
    apk --no-cache add curl tar && \
    rm -rf /var/cache/apk/* && \
    mkdir sbt-$SBT_VERSION && \
    curl -sL "http://dl.bintray.com/sbt/native-packages/sbt/$SBT_VERSION/sbt-$SBT_VERSION.tgz" | gunzip | tar -x -C sbt-$SBT_VERSION --strip-components 1 && \
    rm -f sbt-$SBT_VERSION.tgz && \
    ln -s sbt-$SBT_VERSION sbt && \
    sbt info && \
    echo -ne "- with sbt $SBT_VERSION\n" >> /root/.built

WORKDIR /app

ENTRYPOINT "sbt"
CMD "about"
