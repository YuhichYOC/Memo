## 環境
Ubuntu 18.04  
openjdk-11-jdk  
mysql-server 1 月 30 日時点での最新版  
g++ 1 月 30 日時点での最新版  

***

## 0. インストール前作業
SonarQube 用の MySQL スキーマ・ユーザーを作成  
スキーマ = sonar  
ユーザー = sonar  
![](https://github.com/YuhichYOC/Memo/blob/master/img/sonar/install/1.png)  

***

## 1. SonarQube サーバー・Scanner・c/c++ 用プラグイン入手
1-1. SonarQube サーバー, Download ボタンから先に進む  
![](https://github.com/YuhichYOC/Memo/blob/master/img/sonar/install/2.png)  
Community Edition 7.6 を選択  
![](https://github.com/YuhichYOC/Memo/blob/master/img/sonar/install/3.png)  
  
1-2. c/c++ 用プラグインは GitHub より入手  
![](https://github.com/YuhichYOC/Memo/blob/master/img/sonar/install/4.png)  
![](https://github.com/YuhichYOC/Memo/blob/master/img/sonar/install/5.png)  
  
1-3. Scanner は以下のページより入手  
![](https://github.com/YuhichYOC/Memo/blob/master/img/sonar/install/6.png)  

***

## 2. SonarQube サーバーの準備
2-1. 手順 1-1 でダウンロードした SonarQube サーバーを任意のディレクトリに解凍  
2-2. SonarQube サーバー → MySQL へ接続するためユーザー名・パスワード・接続文字列を properties ファイルに記述  
サーバーの properties ファイルは以下の場所に存在する  
![](https://github.com/YuhichYOC/Memo/blob/master/img/sonar/install/7.png)  
修正前  
![](https://github.com/YuhichYOC/Memo/blob/master/img/sonar/install/8.png)  
修正後  
![](https://github.com/YuhichYOC/Memo/blob/master/img/sonar/install/9.png)  
2-3. プラグインの配置  
手順 1-2 でダウンロードした c/c++ 用プラグインを以下のディレクトリに配置  
![](https://github.com/YuhichYOC/Memo/blob/master/img/sonar/install/10.png)  
2-4. 手順 1-3 でダウンロードした Scanner を任意のディレクトリに解凍  
.profile もしくは .bashrc ファイルを修正し /bin ディレクトリのパスを通す  

***

## 3. SonarQube サーバーの起動
起動確認を行う  
9000 番ポートに Web ブラウザでアクセスすると SonarQube が用意したページを閲覧できる  
![](https://github.com/YuhichYOC/Memo/blob/master/img/sonar/install/11.png)  
![](https://github.com/YuhichYOC/Memo/blob/master/img/sonar/install/12.png)  
![](https://github.com/YuhichYOC/Memo/blob/master/img/sonar/install/13.png)  
MySQL への接続に失敗していると、トップページの一番下に黄色背景の警告メッセージが表示される  
![](https://github.com/YuhichYOC/Memo/blob/master/img/sonar/install/14.png)  

***

## 4. プロジェクト作成
解析対象のソースを格納するためのプロジェクトを新規作成する  
管理者ログインを行う  
ユーザー名・パスワードは、初期設定で admin / admin となっている  
![](https://github.com/YuhichYOC/Memo/blob/master/img/sonar/install/15.png)  
最初のプロジェクトは以下の画面中央のボタンより作成できる  
![](https://github.com/YuhichYOC/Memo/blob/master/img/sonar/install/16.png)  
プロジェクトの作成には Project Key, Display Name, Token の作成が必要  
Project Key, Display Name の設定  
![](https://github.com/YuhichYOC/Memo/blob/master/img/sonar/install/17.png)  
Token の発行画面  
![](https://github.com/YuhichYOC/Memo/blob/master/img/sonar/install/18.png)  
![](https://github.com/YuhichYOC/Memo/blob/master/img/sonar/install/19.png)  
![](https://github.com/YuhichYOC/Memo/blob/master/img/sonar/install/20.png)  
![](https://github.com/YuhichYOC/Memo/blob/master/img/sonar/install/21.png)  

***

## 5. Scanner 実行の準備
解析対象のソースコードを保管しているディレクトリに sonar-project.properties ファイルを作成  
![](https://github.com/YuhichYOC/Memo/blob/master/img/sonar/install/22.png)  

***

## 6. Scanner 実行
手順 5 で sonar-project.properties ファイルを作成したディレクトリで sonar-scanner コマンドを実行  
![](https://github.com/YuhichYOC/Memo/blob/master/img/sonar/install/23.png)  

***

## 出力 : Web ブラウザで解析結果を参照
![](https://github.com/YuhichYOC/Memo/blob/master/img/sonar/install/24.png)  
ほとんどの解析結果は出力されていない  
![](https://github.com/YuhichYOC/Memo/blob/master/img/sonar/install/25.png)  
![](https://github.com/YuhichYOC/Memo/blob/master/img/sonar/install/26.png)  
循環的複雑度の統計が取れていることを確認できる  
![](https://github.com/YuhichYOC/Memo/blob/master/img/sonar/install/27.png)  
