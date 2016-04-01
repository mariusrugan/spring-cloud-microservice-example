FROM frolvlad/alpine-oraclejdk8:latest

RUN apk update && apk add curl && apk add bash

# Install gosu as replacement for sudo
RUN curl -o /usr/local/bin/gosu -sSL "https://github.com/tianon/gosu/releases/download/1.7/gosu-amd64" && chmod +sx /usr/local/bin/gosu

# Add non-root user
RUN addgroup -g 1000 docker && adduser docker -u 1000 -G docker -D -s /bin/bash

VOLUME /tmp

ADD discovery-microservice-0.1.0.jar discovery-microservice-0.1.0.jar
#ADD discovery-microservice.jks discovery-microservice.jks
RUN bash -c 'touch /discovery-microservice-0.1.0.jar'
#RUN bash -c 'touch /discovery-microservice.jks'

USER docker

EXPOSE 5006
EXPOSE 8761

ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=5006","-jar","/discovery-microservice-0.1.0.jar"]%