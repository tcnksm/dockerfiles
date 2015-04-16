FROM debian:jessie

RUN apt-get update && apt-get install -y \
                              openjdk-7-jre-headless \
                              wget \
            && rm -rf /var/lib/apt/lists/*

ENV ZK_VERSION 3.4.6
RUN wget -q \
         http://apache.mirrors.pair.com/zookeeper/zookeeper-${ZK_VERSION}/zookeeper-${ZK_VERSION}.tar.gz \
         -O /tmp/zk.tar.gz \
         && tar -xzf /tmp/zk.tar.gz -C /opt/ \
         && rm /tmp/zk.tar.gz \
         && mv /opt/zookeeper-${ZK_VERSION} /opt/zookeeper

ENV JAVA_HOME /usr/lib/jvm/java-7-openjdk-amd64

EXPOSE 2181 2888 3888
WORKDIR /opt/zookeeper

RUN cp /opt/zookeeper/conf/zoo_sample.cfg /opt/zookeeper/conf/zoo.cfg

ENTRYPOINT ["/opt/zookeeper/bin/zkServer.sh"]
CMD ["start-foreground"]
