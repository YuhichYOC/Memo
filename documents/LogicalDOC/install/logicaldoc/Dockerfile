FROM ubuntu

RUN mkdir /opt/logicaldoc
RUN mkdir /opt/logicaldoc/repo

RUN apt-get update \
  && apt-get -y install openjdk-11-jdk \
  && apt-get -y install software-properties-common \
       curl \
       unzip \
       imagemagick \
       ghostscript \
       python-jinja2 \
       python-pip \
       mysql-client \
       postgresql-client \
       vim \
       nano

RUN curl -L https://sourceforge.net/projects/logicaldoc/files/distribution/LogicalDOC%20CE%208.3/logicaldoc-8.3.4-tomcat-bundle.zip/download \
    -o /opt/logicaldoc/logicaldoc-8.3.4-tomcat-bundle.zip \
  && unzip /opt/logicaldoc/logicaldoc-8.3.4-tomcat-bundle.zip -d /opt/logicaldoc \
  && rm /opt/logicaldoc/logicaldoc-8.3.4-tomcat-bundle.zip

RUN chmod 744 /opt/logicaldoc/logicaldoc-8.3.4-tomcat-bundle/tomcat/bin/catalina.sh
RUN chmod 744 /opt/logicaldoc/logicaldoc-8.3.4-tomcat-bundle/tomcat/bin/startup.sh
RUN chmod 744 /opt/logicaldoc/logicaldoc-8.3.4-tomcat-bundle/tomcat/bin/shutdown.sh
RUN ln -s /opt/logicaldoc/logicaldoc-8.3.4-tomcat-bundle/tomcat/bin/startup.sh /opt/logicaldoc/ldup
RUN ln -s /opt/logicaldoc/logicaldoc-8.3.4-tomcat-bundle/tomcat/bin/shutdown.sh /opt/logicaldoc/lddown

RUN pip install j2cli

EXPOSE 8080
