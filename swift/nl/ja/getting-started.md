---

copyright:
  years: 2017
lastupdated: "2017-09-06"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}

# 入門チュートリアル

* {: download} Hello World サンプル・アプリケーションが {{site.data.keyword.Bluemix}} に正常にデプロイされました。入門として、このステップバイステップのガイドに従って作業してください。または、<a class="xref" href="http://bluemix.net" target="_blank" title="(サンプル・コードのダウンロード)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="アプリケーション・コードのダウンロード" />サンプル・コードをダウンロード</a>して、ご自身で探索してください。

このチュートリアルに従って、開発環境のセットアップ、ローカルおよび {{site.data.keyword.Bluemix}} でのアプリケーションのデプロイ、および {{site.data.keyword.Bluemix}} データベース・サービスのアプリケーションへの統合を行います。

## 始める前に
{: #prereqs}
* [Git ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://git-scm.com/downloads){: new_window}
* [Cloud Foundry CLI ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* ご使用のプラットフォーム用の [Swift コンパイラー ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://swift.org/download/)。

## ステップ 1: サンプル・アプリケーションを複製する
{: #clone}

単純な Swift アプリケーションの操作を開始する準備ができました。リポジトリーを複製して、サンプル・アプリケーションがあるディレクトリーに変更します。
  ```
git clone https://github.com/IBM-Bluemix/get-started-swift
  ```
  {: pre}

  ```
cd get-started-swift
  ```
  {: pre}

  *get-started-swift* ディレクトリー内のファイルを詳細に調べて、内容をよく理解します。

## ステップ 2: アプリケーションをローカルで実行する
{: #run_locally}

Swift コンパイラーをインストールして、この Git リポジトリーを複製したら、次はアプリケーションをコンパイルして実行することができます。ご使用のシステム上でこのリポジトリーのルート・ディレクトリーに移動して、以下のコマンドを発行します。
```
swift build
```
{: pre}

このコマンドの実行には数分かかることがあります。

アプリケーションが正常にコンパイルされたら、Swift コンパイラーによって生成された実行可能ファイルを実行できます。
```
.build/debug/kitura-helloworld
```
{: pre}

以下のような出力が表示されます。

```
Server is listening on port: 8080
```
{: screen}

http://localhost:8080 でアプリケーションを表示します。

## ステップ 3: デプロイメントのためにアプリケーションを準備する
{: #prepare}

{{site.data.keyword.Bluemix_notm}} にデプロイするには、manifest.yml ファイルをセットアップすると役に立つことがあります。manifest.yml には、アプリケーションに関する基本的な情報 (名前、各インスタンス用に割り振るメモリー量、経路など) が含まれます。`get-started-swift` ディレクトリーにサンプルの manifest.yml ファイルが用意されています。

manifest.yml ファイルを開き、`name` を `GetStartedSwift` からご使用のアプリケーション名 <var class="keyword varname" data-hd-keyref="app_name">app_name</var> に変更します。
{: download}

  ```
  applications:
   - name: GetStartedSwift
     random-route: true
     memory: 256M
     command: kitura-helloworld
     buildpack: swift_buildpack
  ```
  {: codeblock}

この manifest.yml ファイル内の **random-route: true** は、アプリケーション用にランダムな経路を生成して、経路が他と衝突するのを回避します。任意のホスト名を指定して、**random-route: true** を **host: myChosenHostName** に置き換えることも選択できます。[詳細はこちら...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## ステップ 4: アプリケーションをデプロイする
{: #deploy}

Cloud Foundry CLI を使用してアプリケーションをデプロイできます。

API エンドポイントを選択します。
  ```
cf api <API-endpoint>
   ```
  {: pre}

コマンド内の *API-endpoint* は以下のリストにある API エンドポイントのいずれかで置き換えてください。

|地域|API エンドポイント|
|:---------------|:-------------------------------|
| 米国南部|https://api.ng.bluemix.net|
| 英国| https://api.eu-gb.bluemix.net|
| シドニー| https://api.au-syd.bluemix.net|
| フランクフルト     | https://api.eu-de.bluemix.net | 

{{site.data.keyword.Bluemix_notm}} アカウントにログインします。

   ```
cf login
```
   {: pre}
   
フェデレーテッド・ユーザー ID を使用しているために `cf login` または `bx login` のコマンドを使用してログインできない場合は、`cf login --sso` または `bx login --sso` のコマンドを使用し、シングル・サインオン ID を使ってログインしてください。詳しくは、[『フェデレーテッド ID を使用したログイン』](https://console.bluemix.net/docs/cli/login_federated_id.html#federated_id)を参照してください。

*get-started-swift* ディレクトリー内から、アプリケーションを {{site.data.keyword.Bluemix_notm}} にプッシュします。
   ```
cf push
```
   {: pre}

これには時間がかかることがあります。デプロイメント・プロセスでエラーが発生した場合、`cf logs <Your-App-Name> --recent` コマンドを使用してトラブルシューティングすることができます。

デプロイメントが完了すると、アプリケーションが実行中であることを示すメッセージが表示されます。push コマンドの出力にリストされている URL でアプリケーションを表示します。また、`cf apps` コマンドを発行して、アプリケーションの状況と URL を確認することもできます。

## ステップ 5: データベースを追加する
{: #add_database}

次に、NoSQL データベースをこのアプリケーションに追加して、ローカルおよび {{site.data.keyword.Bluemix_notm}} 上で実行できるようにアプリケーションをセットアップします。

1. ご使用のブラウザーで {{site.data.keyword.Bluemix_notm}} にログインします。`「ダッシュボード」`を参照します。`「名前」`列でアプリケーション名をクリックして、そのアプリケーションを選択します。
2. `「接続」`、`「新規に接続」`の順にクリックします。
3. `「データおよび分析」`セクションで、`「Cloudant NoSQL DB」`を選択します。
4. 料金プランを選択します。Bluemix は、開始するために十分な容量を持ったクラウド・サービスの選択したコレクションに対して無料の`ライト`・プランを提供します。
5. プロンプトが出されたら、`「再ステージ」`を選択します。{{site.data.keyword.Bluemix_notm}} はアプリケーションを再始動し、`VCAP_SERVICES` 環境変数を使用してデータベース資格情報をアプリケーションに提供します。この環境変数は、アプリケーションが {{site.data.keyword.Bluemix_notm}} で実行されている場合にのみアプリケーションで使用できます。

環境変数を使用すると、デプロイメント設定をソース・コードと分離することができます。例えば、データベース・パスワードをハードコーディングする代わりに、環境変数にそれを保管して、ソース・コードではその環境変数を参照するようにできます。[詳細はこちら...](/docs/manageapps/depapps.html#app_env)
{: tip}

## ステップ 6: データベースを使用する
{: #use_database}

次に、このデータベースを指すようにローカル・コードを更新します。アプリケーションが使用するサービスの資格情報を保管する json ファイルを作成します。このファイルは、アプリケーションがローカルで実行されている場合にのみ使用されます。{{site.data.keyword.Bluemix_notm}} で実行されているときには、資格情報は VCAP_SERVICES 環境変数から読み取られます。

`Sources` ディレクトリーに、次の内容の `config.json` というファイルを作成します (config.json.example を参照)。
 ```
 {
    "vcap":{
       "services":{
          "cloudantNoSQLDB":[
             {
                "credentials":{
                   "host":"<host>",
                   "password":"<password>",
                   "port":443,
                   "url":"<url>",
                   "username":"<username>"
                },
                "label":"cloudantNoSQLDB",
                "name": "CloudantService"
             }
          ]
       }
    }
 }
 ```
{: pre}

このサンプル・アプリケーションでは、Swift-cfenv パッケージを使用して Bluemix と対話して、環境変数を構文解析します。[詳細はこちら...](https://packagecatalog.com/package/IBM-Swift/Swift-cfenv)
{{site.data.keyword.Bluemix_notm}} UI に戻って、「アプリ」->「接続」->「Cloudant」->「資格情報の表示」を選択します。

資格情報のみをコピーして、ローカルの config.json ファイルの対応するフィールドに貼り付けます。

アプリケーションをビルドして、ローカルで実行します。
 ```
swift build
 ```
 {: pre}

  ```
.build/debug/kitura-helloworld
 ```
 {: pre}

http://localhost:8080 でアプリケーションを表示します。アプリケーションに入力するすべての名前がデータベースに追加されるようになります。このサンプル・アプリケーションでは、Kitura-CouchDB パッケージを使用して Cloudant と対話します。[詳細はこちら...](https://packagecatalog.com/package/IBM-Swift/Kitura-CouchDB)
{: tip}

ローカル・アプリケーションと {{site.data.keyword.Bluemix_notm}} アプリケーションは、データベースを共有しています。上の push コマンドの出力にリストされている URL で {{site.data.keyword.Bluemix_notm}} アプリケーションを表示します。いずれかのアプリケーションから追加した名前は、ブラウザーを最新表示すると両方に表示されます。予期しない課金が発生しないように、アプリケーションを稼働中にしておく必要がない場合は停止することを忘れないでください。
{: tip}
