FROM openjdk:8-jdk

ENV GRADLE_VERSION 4.7
ENV PROTOC_VERSION 3.4.1-r1
ENV GRPC_VERSION 1.9.0

ARG GRADLE_SHA=fca5087dc8b50c64655c000989635664a73b11b9bd3703c7d6cabd31b7dcdb04
RUN apt-get install git curl bash gcc g++ protobuf-dev

# install gradle
RUN cd /usr/lib \
 && curl -fl https://downloads.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip -o gradle-bin.zip \
 && echo "$GRADLE_SHA  gradle-bin.zip" | sha256sum -c - \
 && unzip "gradle-bin.zip" \
 && ln -s "/usr/lib/gradle-${GRADLE_VERSION}/bin/gradle" /usr/bin/gradle \
 && rm "gradle-bin.zip"

# manually compile protoc grpc plugin
RUN cd / \
  && git clone https://github.com/grpc/grpc-java.git \
  && cd grpc-java/compiler \
  && git checkout v${GRPC_VERSION} \
  && gradle --no-daemon java_pluginExecutable \
  && ln -s /grpc-java/compiler/build/exe/java_plugin/protoc-gen-grpc-java /usr/bin/protoc-gen-grpc-java