## Solr の起動時 ... ポート 8983 の開放  
  
```bash
sudo ufw allow to any port 8983 proto tcp from any
```
  
## Solr の停止後 ... ポート 8983 の閉鎖  
  
```bash
sudo ufw delete allow to any port 8983 proto tcp from any
```
