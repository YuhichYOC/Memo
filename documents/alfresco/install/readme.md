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
docker run -p 8080:8080 logicaldoc/logicaldoc-ce762  
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
ExecStart=/usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock -g /media/y/images/docker  
  
## XX.  
docker イメージ削除  
```bash  
docker rm [イメージ]  
```  
  
## XX.  
logicalDOC コンテナ起動  
```bash  
docker run -p 8080:8080 [イメージ]  
```  
  
## XX.  
LogicalDOC アドレス  
http://localhost:8080/logicaldoc/login.jsp  
