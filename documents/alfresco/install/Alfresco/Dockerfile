FROM ubuntu

RUN mkdir /opt/alfresco

RUN apt-get update \
  && apt-get -y install openjdk-11-jdk \
  && apt-get -y install software-properties-common \
       curl \
       unzip \
       wget

RUN wget -O /opt/alfresco/alfresco-content-services-community-distribution-6.1.2-ga.zip "https://download.alfresco.com/cloudfront/release/community/201901-GA-build-205/alfresco-content-services-community-distribution-6.1.2-ga.zip" \
  && unzip /opt/alfresco/alfresco-content-services-community-distribution-6.1.2-ga.zip -d /opt/alfresco \
  && rm /opt/alfresco/alfresco-content-services-community-distribution-6.1.2-ga.zip
RUN wget -O /opt/alfresco/alfresco-search-services-1.3.0.1.zip "https://download.alfresco.com/cloudfront/release/community/SearchServices/1.3.0.1/alfresco-search-services-1.3.0.1.zip" \
  && unzip /opt/alfresco/alfresco-search-services-1.3.0.1.zip -d /opt/alfresco \
  && rm /opt/alfresco/alfresco-search-services-1.3.0.1.zip
RUN wget -O /opt/alfresco/alfresco-file-transfer-receiver-6.2.1.zip "https://download.alfresco.com/cloudfront/release/community/201808-EA-build-00140/alfresco-file-transfer-receiver-6.2.1.zip" \
  && unzip /opt/alfresco/alfresco-file-transfer-receiver-6.2.1.zip -d /opt/alfresco \
  && rm /opt/alfresco/alfresco-file-transfer-receiver-6.2.1.zip
