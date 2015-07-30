# Dockerfile for the Apache Mesos-utils
# Outputs a jar file

FROM ubuntu:14.04
MAINTAINER EMC Rubicon <autobots@emc.com>

RUN locale-gen --no-purge en_US.UTF-8
ENV LC_ALL en_US.UTF-8

ENV BUILD_WORKPLACE /var/workplace
ENV BUILD_OUTPUT $BUILD_WORKPLACE/target/

RUN echo "deb http://dl.bintray.com/sbt/debian /" > /etc/apt/sources.list.d/sbt.list

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y --force-yes \
    build-essential \
    git \
    openjdk-7-jdk \
    openjdk-7-jre-headless \
    sbt

ADD ./ $BUILD_WORKPLACE

RUN cd $BUILD_WORKPLACE && sbt update

CMD cd $BUILD_WORKPLACE && sbt 'release with-defaults' && sbt publishLocal
