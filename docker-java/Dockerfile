FROM alpine:latest

ARG url

ENV LANG C.UTF-8
ENV JAVA_URL ${url:-"http://download.oracle.com/otn-pub/java/jdk/8u171-b11/512cd62ec5174c3487ac17c61aaa89e8/jdk-8u171-linux-x64.tar.gz"}

ENV PACKAGES "curl openssl ca-certificates"
RUN apk add --update $PACKAGES && rm -rf /var/cache/apk/*

RUN wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://raw.githubusercontent.com/sgerrand/alpine-pkg-glibc/master/sgerrand.rsa.pub && \
    wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.27-r0/glibc-2.27-r0.apk && \
    apk add glibc-2.27-r0.apk && rm -f glibc-2.27-r0.apk

RUN mkdir -p /opt/java
RUN curl -o jdk.tar.gz -L -O -H "Cookie: oraclelicense=accept-securebackup-cookie" -k $JAVA_URL \
    && tar -xvf jdk.tar.gz -C /opt/java && rm -f jdk.tar.gz && cd /opt/java \
    && ln -s /opt/java/jdk* /opt/java/jdk

ENV JAVA_HOME=/opt/java/jdk \
    PATH=${PATH}:/opt/java/jdk/bin:/opt/java
