FROM ubuntu

RUN mkdir /opt/alfresco \
      && mkdir /opt/alfresco/repo

RUN apt-get update \
      && apt-get -y install openjdk-11-jdk \
      && apt-get -y install software-properties-common \
           curl \
           unzip \
           wget

RUN wget -O /opt/alfresco/apache-tomcat-9.0.34.zip "http://ftp.kddilabs.jp/infosystems/apache/tomcat/tomcat-9/v9.0.34/bin/apache-tomcat-9.0.34.zip" \
      && unzip /opt/alfresco/apache-tomcat-9.0.34.zip -d /opt/alfresco/ \
      && rm /opt/alfresco/apache-tomcat-9.0.34.zip

RUN wget -O /opt/alfresco/alfresco-content-services-community-distribution-6.1.2-ga.zip "https://download.alfresco.com/cloudfront/release/community/201901-GA-build-205/alfresco-content-services-community-distribution-6.1.2-ga.zip" \
      && unzip /opt/alfresco/alfresco-content-services-community-distribution-6.1.2-ga.zip -d /opt/alfresco/ \
      && mkdir -p /opt/alfresco/apache-tomcat-9.0.34/shared/classes \
      && mkdir -p /opt/alfresco/apache-tomcat-9.0.34/shared/lib \
      && mkdir /opt/alfresco/apache-tomcat-9.0.34/amps \
      && mkdir /opt/alfresco/apache-tomcat-9.0.34/amps_share \
      && mkdir /opt/alfresco/apache-tomcat-9.0.34/work \
      && rm -rf /opt/alfresco/apache-tomcat-9.0.34/webapps/* \
      && mv /opt/alfresco/alfresco-content-services-community-distribution-6.1.2-ga/web-server/webapps/* /opt/alfresco/apache-tomcat-9.0.34/webapps/ \
      && mv /opt/alfresco/alfresco-content-services-community-distribution-6.1.2-ga/web-server/conf/Catalina/localhost/* /opt/alfresco/apache-tomcat-9.0.34/conf/ \
      && mv /opt/alfresco/alfresco-content-services-community-distribution-6.1.2-ga/web-server/lib/* /opt/alfresco/apache-tomcat-9.0.34/lib/ \
      && mv /opt/alfresco/alfresco-content-services-community-distribution-6.1.2-ga/amps/alfresco-share-services.amp /opt/alfresco/apache-tomcat-9.0.34/amps/ \
      && mv /opt/alfresco/alfresco-content-services-community-distribution-6.1.2-ga/bin/alfresco-mmt.jar /opt/alfresco/apache-tomcat-9.0.34/bin/ \
      && rm -rf /opt/alfresco/alfresco-content-services-community-distribution-6.1.2-ga \
      && rm /opt/alfresco/alfresco-content-services-community-distribution-6.1.2-ga.zip

RUN chmod 754 /opt/alfresco/apache-tomcat-9.0.34/bin/catalina.sh \
      && chmod 754 /opt/alfresco/apache-tomcat-9.0.34/bin/startup.sh \
      && chmod 754 /opt/alfresco/apache-tomcat-9.0.34/bin/shutdown.sh

COPY ./catalina.properties /opt/alfresco/
COPY ./server.xml /opt/alfresco/
COPY ./alfresco-global.properties /opt/alfresco/
COPY ./apply_amps.sh /opt/alfresco/
COPY ./clean_tomcat.sh /opt/alfresco/

RUN mv -f /opt/alfresco/catalina.properties /opt/alfresco/apache-tomcat-9.0.34/conf/catalina.properties \
      && mv -f /opt/alfresco/server.xml /opt/alfresco/apache-tomcat-9.0.34/conf/server.xml \
      && mv -f /opt/alfresco/alfresco-global.properties /opt/alfresco/apache-tomcat-9.0.34/shared/classes/alfresco-global.properties \
      && mv /opt/alfresco/apply_amps.sh /opt/alfresco/apache-tomcat-9.0.34/bin/apply_amps.sh \
      && chmod 754 /opt/alfresco/apache-tomcat-9.0.34/bin/apply_amps.sh \
      && mv /opt/alfresco/clean_tomcat.sh /opt/alfresco/apache-tomcat-9.0.34/bin/clean_tomcat.sh \
      && chmod 754 /opt/alfresco/apache-tomcat-9.0.34/bin/clean_tomcat.sh
