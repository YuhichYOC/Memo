# 1. パッケージダウンロード  
  
## 1-1. ダウンロード用パッケージのインストール  
  
```bash  
yum -y install yum-utils  
```  
  
## 1-2. 必須 RPM パッケージ  
  
```bash  
yumdownloader ImageMagick.x86_64  
yumdownloader ImageMagick-devel.x86_64  
yumdownloader OpenEXR-libs.x86_64  
yumdownloader apr.x86_64  
yumdownloader apr-devel.x86_64  
yumdownloader apr-util.x86_64  
yumdownloader apr-util-devel.x86_64  
yumdownloader bzip2-devel.x86_64  
yumdownloader cpp.x86_64  
yumdownloader cyrus-sasl-devel.x86_64  
yumdownloader expat-devel.x86_64  
yumdownloader freetype-devel.x86_64  
yumdownloader gcc.x86_64  
yumdownloader gcc-c++.x86_64  
yumdownloader glibc-devel.x86_64  
yumdownloader glibc-headers.x86_64  
yumdownloader httpd.x86_64  
yumdownloader httpd-devel.x86_64  
yumdownloader httpd-tools.x86_64  
yumdownloader ilmbase.x86_64  
yumdownloader ipa-pgothic-fonts.noarch  
yumdownloader jasper-devel.x86_64  
yumdownloader kernel-headers.x86_64  
yumdownloader keyutils-libs-devel.x86_64  
yumdownloader krb5-devel.x86_64  
yumdownloader libICE-devel.x86_64  
yumdownloader libSM-devel.x86_64  
yumdownloader libXext-devel.x86_64  
yumdownloader libXt-devel.x86_64  
yumdownloader libcom_err-devel.x86_64  
yumdownloader libcurl-devel.x86_64  
yumdownloader libdb-devel.x86_64  
yumdownloader libgcrypt-devel.x86_64  
yumdownloader libgpg-error-devel.x86_64  
yumdownloader libgs-devel.x86_64  
yumdownloader libjpeg-turbo-devel.x86_64  
yumdownloader libpng-devel.x86_64  
yumdownloader libselinux-devel.x86_64  
yumdownloader libsepol-devel.x86_64  
yumdownloader libstdc++-devel.x86_64  
yumdownloader libtiff-devel.x86_64  
yumdownloader libverto-devel.x86_64  
yumdownloader libwmf-lite.x86_64  
yumdownloader libxml2-devel.x86_64  
yumdownloader libxslt-devel.x86_64  
yumdownloader libyaml-devel.x86_64  
yumdownloader mailcap.noarch  
yumdownloader ncurses-devel.x86_64  
yumdownloader openldap-devel.x86_64  
yumdownloader openssl-devel.x86_64  
yumdownloader pcre-devel.x86_64  
yumdownloader postgresql.x86_64  
yumdownloader postgresql-devel.x86_64  
yumdownloader postgresql-libs.x86_64  
yumdownloader postgresql-server.x86_64  
yumdownloader readline-devel.x86_64  
yumdownloader xz-devel.x86_64  
yumdownloader zlib-devel.x86_64  
```  
  
## 1-3. ruby 2.4.1  
  
```bash  
curl -O https://cache.ruby-lang.org/pub/ruby/2.4/ruby-2.4.1.tar.gz  
```  
  
## 1-4. redmine 本体  
  
ruby 2.4.1 を使用する場合は redmine-4.0.4.tar.gz (md5: 35a4f60b35fed2b10d14cb12fc8aef50) を使うこと  
Gemfile の記述と bundler のバージョンが合わなくなる  
以下のサイトから Web ブラウザでダウンロード  
http://www.redmine.org/projects/redmine/wiki/Download  
  
## 1-5. bundler  
  
以下のサイトから Web ブラウザでダウンロード  
https://rubygems.org/gems/bundler/versions/2.0.2  
  
## 1-6. rack  
  
以下のサイトから Web ブラウザでダウンロード  
https://rubygems.org/gems/rack/versions/2.0.7  
  
## 1-7. passenger  
  
以下のサイトから Web ブラウザでダウンロード  
https://rubygems.org/gems/passenger/versions/6.0.4  
  
  
# 2. bundle 作成機での手順  
  
## 2-1. SELinux の無効化  
  
このステップの直後に再起動が必要  
```bash  
/etc/sysconfig/selinux  
SELINUX=disabled  
```  
  
## 2-2. firewall ルールを作成 http を許可  
  
```bash  
firewall-cmd --zone=public --add-service=http --permanent  
firewall-cmd --reload  
```  
  
## 2-3. 必須パッケージのインストール  
  
1-2 でダウンロードしたパッケージを配置したディレクトリで以下のコマンドを実行する  
```bash  
yum -y localinstall ./*.rpm  
```  
  
## 2-4. ruby のインストール  
  
1-3 でダウンロードしたアーカイブを配置したディレクトリで以下のコマンドを実行する  
```bash  
tar xvf ruby-2.4.1.tar.gz  
cd ruby-2.4.1  
./configure --disable-install-doc  
make  
make install  
```  
  
## 2-5. bundler のインストール  
  
1-5 でダウンロードした gem ファイルを配置したディレクトリで以下のコマンドを実行する  
```bash  
gem install --local bundler --no-rdoc --no-ri  
```  
  
## 2-6. redmine 本体の解凍  
  
1-4 でダウンロードしたアーカイブを配置したディレクトリで以下のコマンドを実行する  
```bash  
tar xvf redmine-4.0.4.tar.gz  
cd redmine-4.0.4  
```  
  
## 2-7. ./config/database.yml の作成  
  
2-8 : bundle install で DBMS ドライバがインストールされるためこの時点で使用する RDBMS を特定しなければならない  
2-6 で解凍した redmine 本体を配置したディレクトリで以下のコマンドを実行する  
```bash  
cp ./config/database.yml.example ./config/database.yml  
```  
  
### 2-7-1. MySQL を使う場合  
  
MySQL 関連の設定を編集  
  
### 2-7-2. PostgreSQL を使う場合  
  
MySQL 関連の設定を削除もしくはコメントアウト  
PostgreSQL 関連の設定をコメントより復帰  
  
## 2-8. bundle 化  
  
nokogiri だけ特別扱いしなければならない  
このステップだけはオンラインで実行しなければならない  
2-6 で解凍した redmine 本体を配置したディレクトリで以下のコマンドを実行する  
```bash  
bundle config build.nokogiri --use-system-libraries  
bundle install --without development test --path ./vendor/bundle  
```  
  
## 2-9. 稼働機へ送るファイルをまとめる  
  
2-8 完了時点の redmine 本体を配置したディレクトリをアーカイブする  
  
  
# 3. redmine 稼働機  
  
## 3-1. SELinux の無効化  
  
このステップの直後に再起動が必要  
```bash  
/etc/sysconfig/selinux  
SELINUX=disabled  
```  
  
## 3-2. firewall ルールの作成 http を許可  
  
```bash  
firewall-cmd --zone=public --add-service=http --permanent  
firewall-cmd --reload  
```  
  
## 3-3. 必須パッケージのインストール  
  
1-2 でダウンロードしたパッケージを配置したディレクトリで以下のコマンドを実行する  
```bash  
yum -y localinstall ./*.rpm  
```  
  
## 3-4. ruby のインストール  
  
1-3 でダウンロードしたアーカイブを配置したディレクトリで以下のコマンドを実行する  
``` bash  
tar xvf ruby-2.4.1.tar.gz  
cd ruby-2.4.1  
./configure --disable-install-doc  
make  
make install  
```  
  
## 3-5. bundler のインストール  
  
1-5 でダウンロードした gem ファイルを配置したディレクトリで以下のコマンドを実行する  
```bash  
gem install --local bundler --no-rdoc --no-ri  
```  
  
## 3-6. rack のインストール  
  
1-6 でダウンロードした gem ファイルを配置したディレクトリで以下のコマンドを実行する  
```bash  
gem install --local rack --no-rdoc --no-ri  
```  
  
## 3-7. passenger のインストールと初期化  
  
1-7 でダウンロードした gem ファイルを配置したディレクトリで以下のコマンドを実行する  
```bash  
gem install --local passenger --no-rdoc --no-ri  
passenger-install-apache2-module  
```  
  
passenger 初期化時に /etc/httpd/conf.d に redmine.conf を以下の内容で作成  
```bash  
<Directory "/var/www/redmine/redmine-4.0.4">  
  Require all granted  
</Directory>  
  
LoadModule passenger_module /usr/local/lib/ruby/gems/2.4.0/gems/passenger-6.0.4/buildout/apache2/mod_passenger.so  
<IfModule mod_passenger.c>  
  PassengerRoot /usr/local/lib/ruby/gems/2.4.0/gems/passenger-6.0.4  
  PassengerDefaultRuby /usr/local/bin/ruby  
</IfModule>  
  
Header always unset "X-Powered-By"  
Header always unset "X-Runtime"  
  
PassengerMaxPoolSize 20  
PassengerMaxInstancesPerApp 4  
PassengerPoolIdleTime 864000  
PassengerHighPerformance on  
PassengerStatThrottleRate 10  
PassengerSpawnMethod smart  
PassengerFriendlyErrorPages off  
```  
  
## 3-8. postgresql の初期化と設定  
  
### 3-8-1. 以下のコマンドを実行する  
  
```bash  
postgresql-setup initdb  
```  
  
postgresql のデフォルトでは peer もしくは ident 認証が最優先となっている, パスワードを使った認証が不可能で多分オーバーライドもできない  
この時点では redmine ユーザーで postgresql へログインできない ( OS ユーザーに redmine がいないため )  
なので全ユーザーを md5 認証に切り替える  
  
### 3-8-2. postgres ユーザーのパスワード設定  
  
sudo -u postgres psql  
alter user postgres password 'postgres';  
  
### 3-8-3. /var/lib/pgsql/data/pg_hba.conf 以下 3 行変更  
  
local   all             all                                     peer  
host    all             all             127.0.0.1/32            ident  
host    all             all             ::1/128                 ident  
local   all             all                                     md5  
host    all             all             127.0.0.1/32            md5  
host    all             all             ::1/128                 md5  
  
### 3-8-4. /var/lib/pgsql/data/pg_hba.conf 以下追記  
  
host    redmine         redmine         127.0.0.1/32            md5  
host    redmine         redmine         ::1/128                 md5  
  
### 3-8-5. postgresql 起動, 自動起動設定  
  
```bash  
systemctl start postgresql.service  
systemctl enable postgresql.service  
```  
  
### 3-8-6. 以下の 2 行実行  
  
```bash  
sudo -u postgres createuser -P redmine  
sudo -u postgres createdb -E UTF-8 -l ja_JP.UTF-8 -O redmine -T template0 redmine  
```  
  
## 3-9. 移送ファイルの解凍, DBMS 設定の記入  
  
### 3-9-1. 2-9 で作成したアーカイブを /var/lib/redmine 以下に配置, 解凍する  
  
### 3-9-2. /var/lib/redmine/redmine-4.0.4/config/database.yml へ稼働機用の設定を記入  
  
production:  
  adapter: postgresql  
  database: redmine  
  host: localhost  
  username: redmine  
  password: "redmine"  
  encoding: utf8  
  
## 3-10. セッション改ざん防止用秘密鍵の作成  
  
3-9 で redmine 本体を配置したディレクトリで以下のコマンドを実行する  
```bash  
bundle exec rake generate_secret_token  
```  
  
## 3-11. postgresql 初期データ作成  
  
3-9 で redmine 本体を配置したディレクトリで以下のコマンドを実行する  
```bash  
RAILS_ENV=production bundle exec rake db:migrate  
RAILS_ENV=production REDMINE_LANG=ja bundle exec rake redmine:load_default_data  
```  
  
## 3-10. apache2 ⇔ passenger の設定  
  
### 3-10-1. redmine 実行ユーザーを apache に変更  
  
```bash  
chown -R apache:apache /var/lib/redmine  
```  
  
### 3-10-2. URL : http://[サーバー]/ ではなく http://[サーバー]/redmine で redmine へ接続できるようにリンク作成  
  
```bash  
ln -s /var/lib/redmine/redmine-4.0.4/public /var/www/html/redmine  
```  
  
### 3-10-3. http リクエストリダイレクト設定の記入  
  
/etc/httpd/conf.d/redmine.conf に以下の内容を追記  
RackBaseURI /redmine  
  
### 3-10-4. apache2 再起動  
  
```bash  
service httpd configtest # サーバー名の設定内容について警告が出る / 文法チェックは OK となる  
service httpd restart  
```  
