## Solr の起動時 ... ポート 8983 の開放  
  
```bash
sudo ufw allow to any port 8983 proto tcp from any
```
  
## Solr の停止後 ... ポート 8983 の閉鎖  
  
```bash
sudo ufw delete allow to any port 8983 proto tcp from any
```

## Solr 起動コマンド  
  
```bash
./solr/bin/solr start -a "-Dcreate.alfresco.defaults=alfresco,archive"
```
  
## Solr 起動コマンド ( sudo )  
  
```bash
sudo /opt/alfresco/alfresco-search-services/solr/bin/solr start -force -a "-Dcreate.alfresco.defaults=alfresco,archive"
```
