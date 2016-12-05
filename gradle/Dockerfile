FROM anapsix/alpine-java:jdk7
MAINTAINER Juliano Alves <von.juliano@gmail.com>

ENV GRADLE_VERSION=3.2
ENV GRADLE_HOME /usr/local/gradle
ENV PATH $PATH:$GRADLE_HOME/bin

WORKDIR /usr/local

RUN apk update && \
    apk --no-cache add wget bash libstdc++ && \
    rm -rf /var/cache/apk/* && \
    wget https://services.gradle.org/distributions/gradle-$GRADLE_VERSION-bin.zip && \
    unzip -q gradle-$GRADLE_VERSION-bin.zip && \
    rm -f gradle-$GRADLE_VERSION-bin.zip && \
    ln -s gradle-$GRADLE_VERSION gradle && \
    mkdir -p /app

WORKDIR /app

ENTRYPOINT ["gradle"]
CMD ["--version"]
