# Alfresco インストール  
  
## 1. Docker インストール  
```bash  
sudo apt install docker.io  
```  
  
## 2. Docker Compose インストール  
```bash  
sudo apt install docker-compose  
```  
  
## 3. Alfresco チェックアウト  
```bash  
git clone https://github.com/Alfresco/acs-community-deployment.git  
```  
  
## 4.  
```bash  
cd acs-community-deployment/  
```  
  
## 5.  
```bash  
git checkout 2.2.0  
```  
  
## 6.  
```bash  
cd docker-compose  
```  
  
## 7.  
```bash  
docker-compose up  
```  
  
## 8.  
docker グループに Alfresco 起動ユーザーを追加  
/var/run/docker.sock ( unix ドメインソケット ) への書き込み権限を付与する  
```bash  
usermod -aG docker [ユーザー]  
```  
  
  
## XX.  
LogicalDOC コンテナ取得 & 開始  
```bash  
docker run -d --name=mysql-ld --env="MYSQL_ROOT_PASSWORD=mypassword" --env="MYSQL_DATABASE=logicaldoc" --env="MYSQL_USER=ldoc" --env="MYSQL_PASSWORD=changeme" mysql:8.0  
docker run -d -p 8080:8080 --link mysql-ld logicaldoc/logicaldoc-ce  
```  
  
## XX.  
docker サービス開始  
```bash  
systemctl start docker  
```  
  
## XX.  
コンテナ開始  
```bash  
docker run [イメージ]  
```  
  
## XX.  
コンテナ停止  
```bash  
docker stop [イメージ]  
```  
  
## XX.  
マウント  
```bash  
docker run -d -p 8080:8080 -v /media/pi/images/docker:/media/docker --link mysql-ld logicaldoc/logicaldoc-ce  
```  
  
## XX.  
実行中コンテナへアタッチ  
```bash  
docker exec -i -t [コンテナ] /bin/bash  
```  
  
## XX.  
ディスク使用量の表示 ( ディレクトリ全体 )  
```bash  
du -sm [パス]  
```  
  
## XX.  
docker イメージを格納しているディレクトリ  
/var/lib/docker/overlay2 ( Ubuntu18.04 )  
  
## XX.  
イメージ格納先変更  
/lib/systemd/system/docker.service  
ExecStart=/usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock -g /media/pi/images/docker  
  
## XX.  
コンテナ一覧の確認  
```bash  
docker ps  
```  
コンテナ一覧 ( 停止中を含む ) の確認  
```bash  
docker ps -a  
```  
  
## XX.  
docker コンテナ削除  
```bash  
docker rm [コンテナ]  
```  
  
## XX.  
docker イメージ削除  
```bash  
docker rmi [イメージ]  
```  
  
## XX.  
logicalDOC コンテナ起動  
```bash  
docker run -p 8080:8080 [イメージ]  
```  
  
## XX.  
LogicalDOC アドレス  
http://localhost:8080/logicaldoc/login.jsp  
