ARG BASE_IMAGE

# Start from a base image.
FROM $BASE_IMAGE

MAINTAINER jkp <jkp@163.com>

# RocketMQ version
ENV ROCKETMQ_VERSION 4.5.0
# RocketMQ home
ENV ROCKETMQ_HOME  /opt/rocketmq-${ROCKETMQ_VERSION}
ENV JAVA_OPT=" -Duser.home=/opt"

WORKDIR  ${ROCKETMQ_HOME}

RUN mkdir -p /opt/logs /opt/store

VOLUME /opt/logs /opt/store

WORKDIR ${ROCKETMQ_HOME}/bin

CMD sh mqnamesrv
