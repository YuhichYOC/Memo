FROM ubuntu

RUN mkdir /opt/alfresco

RUN apt-get update \
  && apt-get -y install openjdk-11-jdk \
  && apt-get -y install software-properties-common \
       curl \
       unzip \
       wget

RUN wget -O /opt/alfresco/apache-tomcat-9.0.34.zip "http://ftp.kddilabs.jp/infosystems/apache/tomcat/tomcat-9/v9.0.34/bin/apache-tomcat-9.0.34.zip" \
  && unzip /opt/alfresco/apache-tomcat-9.0.34.zip -d /opt/alfresco \
  && rm /opt/alfresco/apache-tomcat-9.0.34.zip

RUN cat /opt/alfresco/apache-tomcat-9.0.34/conf/catalina.properties | sed 's@^shared\.loader\=@shared.loader=${catalina.base}/shared/classes@g' > /opt/alfresco/apache-tomcat-9.0.34/conf/catalina.properties.2
RUN cat /opt/alfresco/apache-tomcat-9.0.34/conf/catalina.properties.2 > /opt/alfresco/apache-tomcat-9.0.34/conf/catalina.properties
RUN rm /opt/alfresco/apache-tomcat-9.0.34/conf/catalina.properties.2

RUN mkdir -p /opt/alfresco/apache-tomcat-9.0.34/shared/classes
RUN mkdir -p /opt/alfresco/apache-tomcat-9.0.34/shared/lib

RUN wget -O /opt/alfresco/alfresco-content-services-community-distribution-6.1.2-ga.zip "https://download.alfresco.com/cloudfront/release/community/201901-GA-build-205/alfresco-content-services-community-distribution-6.1.2-ga.zip" \
  && unzip /opt/alfresco/alfresco-content-services-community-distribution-6.1.2-ga.zip -d /opt/alfresco \
  && rm -rf /opt/alfresco/apache-tomcat-9.0.34/webapps/* \
  && mv /opt/alfresco/alfresco-content-services-community-distribution-6.1.2-ga/web-server/webapps/* /opt/alfresco/apache-tomcat-9.0.34/webapps/ \
  && mv /opt/alfresco/alfresco-content-services-community-distribution-6.1.2-ga/web-server/conf/Catalina/localhost/* /opt/alfresco/apache-tomcat-9.0.34/conf/ \
  && mv /opt/alfresco/alfresco-content-services-community-distribution-6.1.2-ga/web-server/lib/* /opt/alfresco/apache-tomcat-9.0.34/lib/ \
  && rm -rf /opt/alfresco/alfresco-content-services-community-distribution-6.1.2-ga \
  && rm /opt/alfresco/alfresco-content-services-community-distribution-6.1.2-ga.zip

COPY ./server.xml.append /opt/alfresco/
COPY ./alfresco-global.properties.sample /opt/alfresco/

RUN cat /opt/alfresco/server.xml.append | tee -a /opt/alfresco/apache-tomcat-9.0.34/conf/server.xml
RUN mv /opt/alfresco/alfresco-global.properties.sample /opt/alfresco/apache-tomcat-9.0.34/shared/classes/alfresco-global.properties
