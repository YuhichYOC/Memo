FROM ubuntu

RUN mkdir /opt/activemq

RUN apt update \
 && apt -y upgrade \
 && apt -y install openjdk-11-jdk \
 && apt -y install software-properties-common \
      curl \
      unzip \
      wget

RUN wget -O /opt/activemq/apache-activemq-5.15.2-bin.tar.gz "http://www.apache.org/dyn/closer.cgi?filename=/activemq/5.15.2/apache-activemq-5.15.2-bin.tar.gz&action=download" \
 && tar xzf /opt/activemq/apache-activemq-5.15.2-bin.tar.gz \
 && rm /opt/activemq/apache-activemq-5.15.2-bin.tar.gz

RUN chmod 744 /opt/activemq/apache-activemq-5.15.2/bin/activemq
RUN ln -s /opt/activemq/apache-activemq-5.15.2/bin/activemq /opt/activemq
