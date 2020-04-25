FROM ubuntu

RUN mkdir /opt/alfresco

RUN apt-get update \
      && apt-get -y install openjdk-11-jdk

RUN wget -O /opt/alfresco/alfresco-search-services-1.3.0.1.zip "https://download.alfresco.com/cloudfront/release/community/SearchServices/1.3.0.1/alfresco-search-services-1.3.0.1.zip" \
      && unzip /opt/alfresco/alfresco-search-services-1.3.0.1.zip -d /opt/alfresco/ \
      && rm /opt/alfresco/alfresco-search-services-1.3.0.1.zip

COPY ./shared.properties /opt/alfresco/
COPY ./solrcore.properties /opt/alfresco/
COPY ./solr.in.sh /opt/alfresco/

RUN mv -f /opt/alfresco/shared.properties /opt/alfresco/alfresco-search-services/solrhome/conf/shared.properties \
      && mv -f /opt/alfresco/solr.in.sh /opt/alfresco/alfresco-search-services/solr.in.sh \
      && mv -f /opt/alfresco/solrcore.properties /opt/alfresco/alfresco-search-services/solrhome/templates/rerank/conf/solrcore.properties
