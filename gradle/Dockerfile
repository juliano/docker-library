FROM openjdk:7-alpine
MAINTAINER Juliano Alves <von.juliano@gmail.com>

RUN apk update && apk --no-cache add wget bash

ENV GRADLE_VERSION=3.2
ENV GRADLE_HOME /usr/local/gradle
ENV PATH $PATH:$GRADLE_HOME/bin
ENV GRADLE_USER_HOME /gradle

WORKDIR /usr/local

RUN wget https://services.gradle.org/distributions/gradle-$GRADLE_VERSION-bin.zip && \
    unzip -q gradle-$GRADLE_VERSION-bin.zip && \
    rm -f gradle-$GRADLE_VERSION-bin.zip && \
    ln -s gradle-$GRADLE_VERSION gradle

RUN mkdir -p /app
WORKDIR /app

ENTRYPOINT ["gradle"]
CMD ["--version"]
