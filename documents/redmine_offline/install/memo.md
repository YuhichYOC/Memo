1. bundle 作成機での手順  
  
1-1. SELinux の無効化  
```bash  
/etc/sysconfig/selinux  
SELINUX=disabled  
```  
![01](https://github.com/YuhichYOC/Memo/blob/master/img/redmine_offline/bundle/01.png)  
![02](https://github.com/YuhichYOC/Memo/blob/master/img/redmine_offline/bundle/02.png)  
  
1-2. firewall http を許可  
```bash  
firewall-cmd --zone=public --add-service=http --permanent  
firewall-cmd --reload  
```  
![03](https://github.com/YuhichYOC/Memo/blob/master/img/redmine_offline/bundle/03.png)  
  
1-3. 必須パッケージのインストール  
```bash  
yum -y install gcc gcc-c++  
yum -y install httpd httpd-devel  
yum -y install openssl-devel readline-devel zlib-devel  
yum -y install libyaml libyaml-devel  
yum -y install libcurl-devel  
yum -y install libxslt-devel  
```  
![04](https://github.com/YuhichYOC/Memo/blob/master/img/redmine_offline/bundle/04.png)  
  
1-4. ruby のインストール  
```bash  
curl -O https://cache.ruby-lang.org/pub/ruby/2.4/ruby-2.4.1.tar.gz  
tar xvf ruby-2.4.1.tar.gz  
cd ruby-2.4.1  
./configure --disable-install-doc  
make  
make install  
```  
![05](https://github.com/YuhichYOC/Memo/blob/master/img/redmine_offline/bundle/05.png)  
![06](https://github.com/YuhichYOC/Memo/blob/master/img/redmine_offline/bundle/06.png)  
![07](https://github.com/YuhichYOC/Memo/blob/master/img/redmine_offline/bundle/07.png)  
![08](https://github.com/YuhichYOC/Memo/blob/master/img/redmine_offline/bundle/08.png)  
  
1-5. bundler のインストール  
```bash  
gem install bundler --no-rdoc --no-ri  
```  
![09](https://github.com/YuhichYOC/Memo/blob/master/img/redmine_offline/bundle/09.png)  
  
1-6. redmine 本体のダウンロード  
ruby 2.4.1 を使用する場合は redmine-4.0.4.tar.gz (md5: 35a4f60b35fed2b10d14cb12fc8aef50) を使うこと  
Gemfile の記述と bundler のバージョンが合わなくなる  
http://www.redmine.org/projects/redmine/wiki/Download  
![10](https://github.com/YuhichYOC/Memo/blob/master/img/redmine_offline/bundle/10.png)  
  
1-7. 解凍, bundle 化  
```bash  
bundle config build.nokogiri --use-system-libraries   ... 薄汚いノコギリめ  
bundle install --without development test rmagick --path ./vendor/bundle  
```  
![11](https://github.com/YuhichYOC/Memo/blob/master/img/redmine_offline/bundle/11.png)  
![12](https://github.com/YuhichYOC/Memo/blob/master/img/redmine_offline/bundle/12.png)  
![13](https://github.com/YuhichYOC/Memo/blob/master/img/redmine_offline/bundle/13.png)  
![14](https://github.com/YuhichYOC/Memo/blob/master/img/redmine_offline/bundle/14.png)  
  
1-8. パッケージング  
```bash  
bundle package  
```  
![15](https://github.com/YuhichYOC/Memo/blob/master/img/redmine_offline/bundle/15.png)  
  
1-9. 稼働機へ移送するファイルをまとめる  
Gemfile  
Gemfile.lock  
./config/database.yml   ... 稼働機用に書き直すけど骨組みだけ持っていく  
./vendor/cache/*  
![16](https://github.com/YuhichYOC/Memo/blob/master/img/redmine_offline/bundle/16.png)  
![17](https://github.com/YuhichYOC/Memo/blob/master/img/redmine_offline/bundle/17.png)  
![18](https://github.com/YuhichYOC/Memo/blob/master/img/redmine_offline/bundle/18.png)  
![19](https://github.com/YuhichYOC/Memo/blob/master/img/redmine_offline/bundle/19.png)  
![20](https://github.com/YuhichYOC/Memo/blob/master/img/redmine_offline/bundle/20.png)  
![21](https://github.com/YuhichYOC/Memo/blob/master/img/redmine_offline/bundle/21.png)  
  
2. redmine 稼働機  
  
2-1. SELinux の無効化  
```bash  
/etc/sysconfig/selinux  
SELINUX=disabled  
```  
  
2-2. firewall http を許可  
```bash  
firewall-cmd --zone=public --add-service=http --permanent  
firewall-cmd --reload  
```  
  
## ↓↓↓ *.rpm を拾ってくる必要がある ↓↓↓ ##  
  
2-3. 必須パッケージのインストール  
```bash  
yum -y install gcc gcc-c++  
yum -y install httpd httpd-devel  
yum -y install postgresql-server postgresql-devel  
yum -y install openssl-devel readline-devel zlib-devel  
yum -y install libyaml libyaml-devel  
yum -y install libcurl-devel  
yum -y install libxslt-devel  
```  
  
2-4. ruby のインストール  
``` bash  
curl -O https://cache.ruby-lang.org/pub/ruby/2.4/ruby-2.4.1.tar.gz  
tar xvf ruby-2.4.1.tar.gz  
cd ruby-2.4.1  
./configure --disable-install-doc  
make  
make install  
```  
  
2-5. bundler のインストール  
```bash  
gem install bundler --no-rdoc --no-ri  
```  
  
2-6. passenger のインストール  
```bash  
gem install passenger --no-rdoc --no-ri  
passenger-install-apache2-module  
```  
  
## ↑↑↑ *.rpm を拾ってくる必要がある ↑↑↑ ##  
  
2-7. 移送ファイルの解凍  
  
2-8. bundle をインストール？これで表現正しい？  
```bash  
bundle config build.nokogiri --use-system-libraries   ... 薄汚いノコギリめ  
bundle install --without development test rmagick --path vendor/bundle --local  
```  
  
2-9. postgresql の設定  
```bash  
postgresql-setup initdb  
```  
  
/var/lib/pgsql/data/pg_hba.conf に以下追記  
host    redmine         redmine         127.0.0.1/32            md5  
host    redmine         redmine         ::1/128                 md5  
  
```bash  
systemctl start postgresql.service  
systemctl enable postgresql.service  
```  
  
cd /var/lib/pgsql へ移動, 以下の 2 行実行  
```bash  
sudo -u postgres createuser -P redmine  
sudo -u postgres createdb -E UTF-8 -l ja_JP.UTF-8 -O redmine -T template0 redmine  
```  
  
./config/database.yml へ稼働機用の設定を記入  
production:  
  adapter: postgresql  
  database: redmine  
  host: localhost  
  username: redmine  
  password: "********"  
  encoding: utf8  
  
2-10. apache2 ⇔ passenger の設定  
  
