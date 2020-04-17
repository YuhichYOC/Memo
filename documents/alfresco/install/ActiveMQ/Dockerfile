FROM ubuntu

RUN mkdir /opt/activemq

RUN apt-get update \
  && apt-get -y install openjdk-11-jdk \
  && apt-get -y install software-properties-common \
       curl \
       unzip \
       wget

RUN wget -O /opt/activemq/apache-activemq-5.15.12-bin.tar.gz "http://www.apache.org/dyn/closer.cgi?filename=/activemq/5.15.12/apache-activemq-5.15.12-bin.tar.gz&action=download" \
  && tar xzf /opt/activemq/apache-activemq-5.15.12-bin.tar.gz -C /opt/activemq/ \
  && rm /opt/activemq/apache-activemq-5.15.12-bin.tar.gz

RUN chmod 744 /opt/activemq/apache-activemq-5.15.12/bin/activemq
RUN ln -s /opt/activemq/apache-activemq-5.15.12/bin/activemq /opt/activemq
