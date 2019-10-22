# LogicalDoc ce インストール  
  
## 1. PostgreSQL インストール  
```bash
sudo apt install postgresql-11
```
  
## 2. postgres ユーザーのパスワード変更
```bash
psql -U postgres
=> alter user postgres password ['パスワード'];
=> \q
```
  
## 3. peer 認証解除  
```bash
systemctl stop postgresql
sudo vi /etc/postgresql/11/pg_hba.conf
# redmine インストール手順参照
systemctl start postgresql
```
  
## 4. LogicalDoc 用ユーザー作成  
```bash
psql -U postgres
[パスワード入力]
=> create user logicaldoc password ['パスワード'];
=> \q
```
  
## 5. LogicalDoc データベース作成  
```bash
psql -U postgres
[パスワード入力]
=> create database logicaldoc owner=logicaldoc template=template0;
=> \q
```
  
## 6. LogicalDoc 8.3.2 tomcat bundle ダウンロード  
