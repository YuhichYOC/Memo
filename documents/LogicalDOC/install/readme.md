# LogicalDoc ce インストール  
  
## 1. ufw インストール  
```bash
sudo apt install ufw
```
  
## 2. ufw 設定  
```bash
sudo ufw default deny
sudo ufw allow from 192.168.0.0/24
sudo ufw enable
```
  
## 3. PostgreSQL インストール  
```bash
sudo apt install postgresql-11
```
  
## 4. postgres ユーザーのパスワード変更
```bash
psql -U postgres
=> alter user postgres password ['パスワード'];
=> \q
```
  
## 5. peer 認証解除  
```bash
systemctl stop postgresql
sudo vi /etc/postgresql/11/pg_hba.conf
# redmine インストール手順参照
systemctl start postgresql
```
  
## 6. LogicalDoc 用ユーザー作成  
```bash
psql -U postgres
[パスワード入力]
=> create user logicaldoc password ['パスワード'];
=> \q
```
  
## 7. LogicalDoc データベース作成  
```bash
psql -U postgres
[パスワード入力]
=> create database logicaldoc owner=logicaldoc template=template0;
=> \q
```
  
## 8. LogicalDoc 8.3.2 tomcat bundle ダウンロード  
