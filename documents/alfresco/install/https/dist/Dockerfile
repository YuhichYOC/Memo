FROM ubuntu

RUN mkdir /opt/alfresco

RUN apt-get update \
  && apt-get -y install openjdk-11-jdk \
  && apt-get -y install software-properties-common \
       curl \
       unzip \
       wget

RUN wget -O /opt/alfresco/apache-tomcat-9.0.34.zip "http://ftp.kddilabs.jp/infosystems/apache/tomcat/tomcat-9/v9.0.34/bin/apache-tomcat-9.0.34.zip" \
  && unzip /opt/alfresco/apache-tomcat-9.0.34.zip -d /opt/alfresco/ \
  && rm /opt/alfresco/apache-tomcat-9.0.34.zip

RUN chmod 754 /opt/alfresco/apache-tomcat-9.0.34/bin/catalina.sh
RUN chmod 754 /opt/alfresco/apache-tomcat-9.0.34/bin/startup.sh
RUN chmod 754 /opt/alfresco/apache-tomcat-9.0.34/bin/shutdown.sh

RUN wget -O /opt/alfresco/alfresco-content-services-community-distribution-6.1.2-ga.zip "https://download.alfresco.com/cloudfront/release/community/201901-GA-build-205/alfresco-content-services-community-distribution-6.1.2-ga.zip" \
  && unzip /opt/alfresco/alfresco-content-services-community-distribution-6.1.2-ga.zip -d /opt/alfresco/ \
  && rm -rf /opt/alfresco/apache-tomcat-9.0.34/webapps/* \
  && mv /opt/alfresco/alfresco-content-services-community-distribution-6.1.2-ga/web-server/webapps/* /opt/alfresco/apache-tomcat-9.0.34/webapps/ \
  && mv /opt/alfresco/alfresco-content-services-community-distribution-6.1.2-ga/web-server/conf/Catalina/localhost/* /opt/alfresco/apache-tomcat-9.0.34/conf/ \
  && mv /opt/alfresco/alfresco-content-services-community-distribution-6.1.2-ga/web-server/lib/* /opt/alfresco/apache-tomcat-9.0.34/lib/ \
  && rm -rf /opt/alfresco/alfresco-content-services-community-distribution-6.1.2-ga \
  && rm /opt/alfresco/alfresco-content-services-community-distribution-6.1.2-ga.zip

RUN mkdir -p /opt/alfresco/apache-tomcat-9.0.34/shared/classes
RUN mkdir -p /opt/alfresco/apache-tomcat-9.0.34/shared/lib

COPY ./catalina.properties /opt/alfresco/
COPY ./server.xml /opt/alfresco/
COPY ./alfresco-global.properties /opt/alfresco/

RUN mv -f /opt/alfresco/catalina.properties /opt/alfresco/apache-tomcat-9.0.34/conf/catalina.properties
RUN mv -f /opt/alfresco/server.xml /opt/alfresco/apache-tomcat-9.0.34/conf/server.xml
RUN mv -f /opt/alfresco/alfresco-global.properties /opt/alfresco/apache-tomcat-9.0.34/shared/classes/alfresco-global.properties

RUN mkdir -p /opt/alfresco/repo/keystore
