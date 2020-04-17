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
  && mv /opt/alfresco/alfresco-content-services-community-distribution-6.1.2-ga/web-server/shared/classes/alfresco-global.properties.sample /opt/alfresco/apache-tomcat-9.0.34/shared/classes/alfresco-global.properties \
  && rm -rf /opt/alfresco/alfresco-content-services-community-distribution-6.1.2-ga \
  && rm /opt/alfresco/apache-tomcat-9.0.34/webapps/alfresco-content-services-community-distribution-6.1.2-ga.zip

RUN echo '<Connector port="8443" protocol="org.apache.coyote.http11.Http11Protocol"' | tee -a /opt/alfresco/apache-tomcat-9.0.34/conf/server.xml
RUN echo '    SSLEnabled="true" maxThreads="150" scheme="https"'                     | tee -a /opt/alfresco/apache-tomcat-9.0.34/conf/server.xml
RUN echo '    keystoreFile="xxxxx"'                                                  | tee -a /opt/alfresco/apache-tomcat-9.0.34/conf/server.xml
RUN echo '    keystorePass="password" keystoreType="JCEKS"'                          | tee -a /opt/alfresco/apache-tomcat-9.0.34/conf/server.xml
RUN echo '    secure="true" connectionTimeout="240000"'                              | tee -a /opt/alfresco/apache-tomcat-9.0.34/conf/server.xml
RUN echo '    truststoreFile="xxxxx"'                                                | tee -a /opt/alfresco/apache-tomcat-9.0.34/conf/server.xml
RUN echo '    truststorePass="password" truststoreType="JCEKS"'                      | tee -a /opt/alfresco/apache-tomcat-9.0.34/conf/server.xml
RUN echo '    clientAuth="want" sslProtocol="TLS" />'                                | tee -a /opt/alfresco/apache-tomcat-9.0.34/conf/server.xml

RUN wget -O /opt/alfresco/apache-tomcat-9.0.34/webapps/alfresco-search-services-1.3.0.1.zip "https://download.alfresco.com/cloudfront/release/community/SearchServices/1.3.0.1/alfresco-search-services-1.3.0.1.zip" \
  && unzip /opt/alfresco/apache-tomcat-9.0.34/webapps/alfresco-search-services-1.3.0.1.zip -d /opt/alfresco/apache-tomcat-9.0.34/webapps \
  && rm /opt/alfresco/apache-tomcat-9.0.34/webapps/alfresco-search-services-1.3.0.1.zip

RUN wget -O /opt/alfresco/apache-tomcat-9.0.34/webapps/alfresco-file-transfer-receiver-6.2.1.zip "https://download.alfresco.com/cloudfront/release/community/201808-EA-build-00140/alfresco-file-transfer-receiver-6.2.1.zip" \
  && unzip /opt/alfresco/apache-tomcat-9.0.34/webapps/alfresco-file-transfer-receiver-6.2.1.zip -d /opt/alfresco/apache-tomcat-9.0.34/webapps \
  && rm /opt/alfresco/apache-tomcat-9.0.34/webapps/alfresco-file-transfer-receiver-6.2.1.zip
