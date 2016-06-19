# 4 診断方法について
## 4.1 Proxy機能
### 4.1.1 Proxyを利用した通信キャプチャ
一般的なクライアントProxytoolに関する説明
MITMやっているようなお決まりの絵と内容を説明をするイメージ
見るだけじゃなくて変更もできるよ。SSLもイケますよ。みたいなことを書く。

### 4.1.2 Proxyタブの構成
Proxyタブを構成する各タブに関する簡単な概要の説明
- Intercept
- HTTP history
- WebSockets history
- Options

## 4.2 Burp Suiteによる通信のキャプチャ
### 4.2.1 通信をキャプチャしてみよう！
Burp Suiteでブラウザの通信をキャプチャするためにブラウザで行ったProxy設定にあったIPアドレスおよびポートを設定する必要があります。Burp SuiteでのProxy設定は、「Proxy」-「Options」-「Proxy Listeners」で通信を受け付ける待ち受け用のIPアドレスおよびポートを設定します。デフォルトでは127.0.0.1の8080番で待ち受けるようになっています。

※Proxy Listenersの画像

Burp Suiteのデフォルトはブラウザからのリクエストはインターセプト(止める)する設定になっています。デフォルトで「Proxy」-「Intercept」で「Intercept is On」になっています。ボタンをクリックすると「Intercept is Off」になり、インターセプトされないようになります。

リクエストをインターセプトした場合、サーバにはリクエストが送信されていないため、レスポンスは表示されません。その場合、「Forward」をクリックするか、「Intercept is On」をクリックして「Intercept is Off」にするとインターセプトされていたリクエストがサーバに送信されます。

「Proxy」-「HTTP history」には、Burp ProxyがProxyしたHTTPログが一覧で表示されます。以下の項目が表示されます。

    - Host
    - Method
    - URL
    - Params
    - Edited
    - Status
    - Length
    - MIME type
    - Extension
    - title
    - Comment
    - SSL
    - IP
    - Cookies
    - Time
    - Listener port

また、各HTTPログを選択すると下部に選択したHTTPログのリクエストおよびレスポンスが表示されます。RequestタブおよびResponseタブにそれぞれに以下のタブがあり、表示形式を変更して内容を確認することができます。※はResponseタブでのみ表示されます。

    - Raw
    - Params
    - Headers
    - Hex
    - HTML ※
    - Render ※

「HTTP history」の一覧の各カラムをクリックすると降順または昇順での並び替えができます。例えば「Params」をクリックするとHTTPログの中でパラメータが存在するHTTPログが上部に表示されます。
FilterをクリックするとHTTPログを設定する条件に応じてフィルタすることができます。正規表現でのフィルタ機能だけProfessinal Editioinのみ利用可能です。

- Filter by request type
スコープ内のログのみ表示やパラメータが存在するリクエストのみ表示するなど指定することができます。

- Filter by MIME type
HTMLやCSS、ScriptなどのMIMEタイプを指定することができます。

- Filte by status code
レスポンスのステータスコードを指定することができます。

- Filter by file extension
URLの拡張子を指定することができます。

- Filter by annotation
HTTPログの「comment」や「highlight」したもののみ表示するなど指定することができます。

### 4.2.2 値を書き換えて送信してみよう！
リクエストを改変する場合は「Intercept is On」でインターセプトしたリクエストの内容を変更します。Postデータを変更して送信されるContent-Lengthが変更された場合、Burp Suiteが変更後の内容をもとにContent-Lengthを再計算しセットするため、意識する必要はありません。

「Foward」はインターセプトしたリクエストをサーバへ送信します。複数のリクエストがインターセプトされている場合、1リクエストづつに「Foward」をクリックする必要があります。

「Drop」はインターセプトしたリクエストを破棄します。サーバへは送信されません。

「Intercept is On」/「Intercept is Off」でインターセプトをするかどうかを設定します。ステータスを「Intercept is Off」に変更するとインターセプトされているすべてのリクエストがサーバに送信されます。

「Actions」ではインターセプトしてリクエストに対するアクションを設定することができます。特定の条件のリクエストをインターセプトしない設定やレスポンスを設定するなど指定することができます。

インターセプトしてリクエストの内容を変更した場合、「Proxy」-「HTTP history」の該当ログで「Edited」にチェックされます。また、下部のタブに「Original request」と「Edited request」が表示され、変更前と変更後のリクエストの内容を確認することができます。レスポンスを変更した場合は「Original response」と「Edited response」が表示され、変更前と変更後のレスポンスを確認することができます。


## 4.3 その他

### 4.3.1 リクエストの再送信

検査では、リクエストを多数送信します。Repeaterを使用することで、HTTP Historyからコピーしたリクエストを送信したり、新規に作成したリクエストを送信することが出来ます。

#### 4.3.1.1 Historyからリクエストのコピー
1. Repeaterにコピーしたいリクエストを「HTTP History」で選択します。
2. 「Send To Repeater」を選択し、Repeaterにリクエストをコピーします。
3. Repeaterを開きます。

#### 4.3.1.2 リクエストの新規作成
1. Repeaterの「...」タブを選択します。
2. 右上にある「Target」をクリックします。接続先を入力する画面が表示されます。「Host」、「Port」を入力し、「OK」ボタンを押します。HTTPSでの接続を行う場合は、「Use HTTPS」にチェックを入れます。

#### 4.3.1.3 リクエストの編集、送信
1. 編集したいリクエストのタブを選択します。
2. 「Request」の「RAW」タブでは生のHTTPリクエストを直接編集できます。
「Request」の「Params」タブではパラメーターを表形式で表示し、変更できます。「Type」を変更することで、パラメーターの位置を変更できます。例えば、「Type」を「Body」から「Cookie」に変更することで、ボディパラメーターをCookieに移動することが出来ます。「Add」ボタンを押すとパラメーターを追加できます。「Remove」ボタンを押すと選択しているパラメーターを削除できます。「Up」ボタン、「Down」ボタンを押すとパラメーターを送信する順番を変更できます。
「Request」の「Headers」タブではヘッダーを表形式で表示し、変更できます。「Add」ボタンを押すとヘッダーを追加できます。「Remove」ボタンを押すと選択しているヘッダーを削除できます。「Up」ボタン、「Down」ボタンを押すとヘッダーを送信する順番を変更できます。
「Request」の「Hex」タブではリクエストをHexで確認、編集できます。
3. 右上にある「Target」をクリックすると、接続先を変更できます。
4. 「Go」ボタンを押し、リクエストを送信します。

#### 4.3.1.4 レスポンスの確認
1. 「Response」の「Raw」タブでは生のHTTPレスポンスを確認できます。
2. 「Response」の「Headers」タブではヘッダーを表形式で表示します。
「Response」の「Hex」タブではレスポンスをHexで表示します。
「Response」の「Render」タブではResponseがHTMLの場合、レスポンスをレンダリングし表示します。

### 4.3.2 Scope設定

検査対象外のアプリケーションに対して検査を実施してはいけません。誤って検査対象外のサーバー、URLを検査しないようにScopeを設定します。
Scopeを設定することで、Burpの動作に以下のような制限がかかります。

・Scopeで設定した条件を満たさないリクエストをProxy Historyに表示しないように出来ます。
・Scopeで設定した条件を満たすリクエストのみをInterceptして、リクエストの改ざんが出来るようにします。
・Scopeで設定した条件を満たさないリクエストをSpiderの開始URLとしようとすると、Scopeに追加することを確認するポップアップが表示されます。

Include in scope
ここに記述された条件はスコープ内として認識されます。

Exclude from scan
ここに記述された条件を満たすリクエストはスコープ外として認識されます。

#### 4.3.2.1 Scopeへの追加
Scopeの追加は2つ方法があります。
1. 「Add」ボタンを使用する
2. 「Paste URL」ボタンを使用する

「Add」ボタンを使用する
1. 「Add」ボタンを押します。
2. 「Host or IP range」、「Port」、「File」を正規表現で記述します。
3. 「OK」ボタンを押します。

「Paste URL」ボタンを使用する
1. スコープに含めたいURLをCntl+Cでコピーします。
2. 「Paste URL」ボタンを押します。

#### 4.3.2.1 Scopeからの削除
1. 削除したい条件を選択します。
2. 「Remove」ボタンを押します。

### 4.3.3 サーバ証明書設定

暗号化通信（https://～）が必要なWebアプリケーションに、デフォルト設定のBurp Suiteでアクセスすると、ブラウザに送信された証明書が不正であることを伝えるセキュリティ警告画面が表示されます。

![Firefoxのセキュリティ警告画面](./img/chapter4.3.3-before_CA_install_firefox.png "Firefoxのセキュリティ警告画面")

図4-3-3-a Firefoxのセキュリティ警告画面

セキュリティ警告画面が表示される原因は、Burp Suiteが起動時に独自に生成したCA証明書により署名された自己署名証明書を接続に使用しているためです。

一時的に例外としてBurp Suite独自の証明書を受け入れると、暗号化されている通信内容をBurp Suite上で平文で確認することが可能になります。しかし、警告のたびに操作をするのは煩わしいうえに、Webアプリケーションの設定によっては、自己署名証明書を使用して接続できない場合があります。

そのため、暗号化通信を効率よく取り扱うために、Burp Suiteの独自CA証明書をOSあるいはブラウザにインポートする必要があります。

なお、FirefoxはCA証明書を独自に管理しています。そのため、WindowsとOS XおよびFirefoxの3パターンについて解説します。

#### 独自CA証明書の保存

すべてのパターンで共通する操作はBurp Suiteが生成した独自CA証明書の保存です。

1. ブラウザのプロキシ設定がBurp Suiteに接続するようになっていることを確認
1. http://burp/ にアクセスして「CA certificate」リンクをクリック
1. 任意の名前でCA証明書を保存

#### Windows

1. Windowsの「インターネットオプション」（inetcpl.cpl）→「コンテンツ」→「証明書」ボタンをクリック
1. 「インポート...」をクリックして証明書ファイルを選択し、証明書ストアから「信頼されたルート証明機関」を選択してインポート
1. 「セキュリティ警告」ダイアログで「はい」をクリック

#### OS X

OS Xの場合は「キーチェーンアクセス」アプリにより設定します。

1. 「Launchpad」→「その他」から「キーチェーンアクセス」アプリを起動
1. 左上の南京錠が閉じている場合はクリックしてパスワードを入力してロックを解除
1. 「キーチェーン」で「ログイン」を選択し、「分類」で「証明書」を選択
1. 「ファイル」→「読み込む...」で保存したCA証明書を読み込み
1. 読み込んだ「PortSwigger CA」をダブルクリック
1. 「▶信頼」を展開し、「この証明書を使用するとき」プルダウンリストで「常に信頼」を選択
1. パスワードを入力して「設定をアップデート」ボタンをクリック

#### Firefox

1. ブラウザの設定「オプション」→「詳細」→「証明書」→「証明書を表示...」クリックで「証明書マネージャ」を表示
1. 「インポート...」ボタンをクリックして保存した証明書を「開く」
1. 「証明書のインポート」ダイアログで「この認証局によるWebサイトの識別を信頼する」にチェックを入れて「OK」ボタンをクリック

### 4.3.4 ログ保存設定

1.[Options]-[Misc]-Logging]の設定
ALLとToolsの使い分け、RequestとResponse

2.ログの見方

3.[参考]Logger++の紹介

### 4.3.5 アップストリームProxy設定

1.背景
- 社内Proxyの図
  - Proxy Host
  - Proxy Port

2.設定
  - 具体的な設定値例(図)
    - Desitination Hostに*(ワイルドカード)入れる話は必須
    - 認証方式、ID/PWD

3.Burp特有の問題と対策
  - 名前解決遅くなる問題
  - Connection timeout待ちで遅い問題

### 4.3.6 Intruder

1.自動化の必要性

2.使い方
  - Instuderへの渡し方
    - History右クリックからのsend IntruderあるいはCtrl+i
  - Positions設定
    - 自動設定
    - 手動設定(微調整)
  - Payloads
    - Payload Type
    - Payload Options(Simple List)
  - 実行結果と見方

3.便利な使い方
  - Grep Match
  - Automatic Payload Position

### 4.3.7 Extender

Burp Suiteは、ユーザ自身、または第三者が独自に開発した拡張機能を取り込み、様々な機能の拡張ができます。
例えば、HTTPリクエスト・レスポンスの修正、UIのカスタマイズ、外部ツールとの連携、Intruderの独自ペイロードの作成、Scannerのシグネチャ追加（Professional版用）などです。
これらの拡張機能の取り込みや管理をするためのツールが、Extenderです。

Burp Suiteで拡張機能を利用するには、２つの方法があります。拡張機能のファイルを用意し登録する方法と、BApp Storeを利用する方法です。
まずは、BApp Storeを利用する方法を説明します。

#### BApp Storeを利用する
[BApp Store](https://portswigger.net/bappstore/)は、Burp Suiteのユーザが開発した拡張機能を登録し公開できるサービスです。
2016/06時点で、約80個の拡張機能が公開されています。

BApp Storeで公開されている拡張機能は、Burp SuiteのUI上から簡単に取り込めるようになっています。
「Extender」の「BApp Store」タブを開きます。

![Burp SuiteのBApp Store画面]()

この画面で、拡張機能名と詳細情報が確認できます。
一部の拡張機能は、Professional版でのみ利用可能で、Detail列にその旨記載があります。

それでは、「Logger++」という拡張機能をインストールしてみましょう。
この拡張機能は、Burp Suiteの様々なツールが送受信したHTTPメッセージを、ProxyのHTTP historyのようなインタフェースで表示できる拡張機能です。

左側の一覧表から、「Logger++」を選択します。すると右側のペインにLogger++の詳細情報が表示されます。
一番下の「Install」ボタンをクリックしてください。インストールが進み、ボタンが「Reinstall」に変われば、インストールは完了です。

拡張機能によってBurp Suiteのどこを拡張するかは様々です。
カスタムタブの追加、コンテキストメニューへのアイテム追加、メッセージエディターへのタブ追加など、UIに反映される箇所は異なり、またUI上では変化が分からないものもありますので、拡張機能の詳細情報で確認してください。
Logger++の場合は、カスタムタブが追加されています。
Logger++の詳細には触れませんので、様々なサイトにアクセスしてどのようなログが取れるか確認してください。

![Logger++画面]()

#### 拡張機能ファイルを登録する

拡張機能は、BApp Store以外からも入手できます。自身で拡張機能を開発した場合も、この手順で取り込むことになります。

今回は「OgaCopy」という拡張機能をインストールしてみましょう。
Burp Suiteはマルチバイト文字の取扱が不得意で、メッセージエディターなどで日本語を含むテキストをコピーしてペーストすると、文字化けをしてしまいます。
OgaCopyはこれを補正して、文字化けせずコピーができる拡張機能です。

OgaCopy（[http://www.geocities.jp/burplogviewer/burpextender.html](http://www.geocities.jp/burplogviewer/burpextender.html)）

まず上記のサイトにアクセスし、JARファイルをダウンロードします（2016/06時点で最新はv1.1）。保存場所は任意の場所でかまいません。

![OgaCopyサイトのスクショ]()

Burp SuiteのUIで「Extender」の「Extensions」タブを開きます。
上部のペインには、インストールされている拡張機能が表示されています。
前述の手順でBApp StoreからLogger++をインストールしているばあいは、ここに表示されているはずです。

![Extender Extensions]()

左側から「Add」ボタンをクリックすると、「Load Burp Extension」ダイアログボックスが開きます。

![Load Burp Extensionダイアログボックス]()

Extension typeに「Java」が選択されていることを確認し、「Select file...」ボタンをクリックします。
ここで、先程ダウンロードしておいた、OgaCopy_v1.1.jarを選択します。

「Next」ボタンをクリックすると、拡張機能が読み込まれます。
「Output」と「Errors」というタブがあり。ここには拡張機能が出力するログが表示されます。
OgaCopy の場合は、Outputタブに、"OgaCopy v1.1 Load OK!"と表示されているはずです。
右下の「Close」ボタンをクリックして、このダイアログボックスを閉じてしまってかまいません。
すべてうまくいっていれば、拡張機能一覧テーブルにOgaCopy v1.1 が追加され、Loaded列にチェックボックスがついているはずです。

OgaCopyは、コンテキストメニューに項目が追加されるタイプの拡張機能です。
Proxyの履歴などで日本語を含むレスポンスを探してメッセージエディターで開いてください。
コンテキストメニューを表示させると、OgaCopyの項目が３つ追加されています。
今まで通りテキストを選択して「Ctrl+C」でコピーした場合と、OgaCopyでコピーした場合と、ペーストした結果を見比べてみてください。

#### 拡張機能の管理

「Extender」の「Extensions」タブで、インストールされている拡張機能の管理ができます。

拡張機能を無効化するには、「Loaded」列のチェックボタンをオフにしてください。
無効化するとBurp Suiteを再起動しても自動的に有効になりませんので、再度使いたい場合はチェックボックスをオンにしてください。

拡張機能をBurp Suiteから完全に削除するには、削除する拡張機能を選択して、左側から「Remove」ボタンをクリックしてください。

#### PythonやRubyで開発された拡張機能

拡張機能は、JavaだけではなくPythonやRubyで開発もできます。
BApp Storeで公開されている拡張機能にも、PythonやRubyで開発されたものがあります。
これらの拡張機能を利用するには、Jython・JRubyをインストールしておく必要があります。

* Python

[Jythonダウンロードサイト](http://www.jython.org/downloads.html) から、Standalone Jar（2016/06時点で最新は2.7.0）をダウンロードします。

Burp SuiteのUIで「Extender」の「Options」タブを開きます。
「Python Environment」セクションの「Location of Jython standalone JAR file:」で、ダウンロードしたjython-standalone-2.7.0.jarを選択します。

* Ruby

[JRubyダウンロードサイト](http://jruby.org/download) から、JRuby Complete .jar（2016/06時点で最新は9.1.2.0）をダウンロードします。

Burp SuiteのUIで「Extender」の「Options」タブを開きます。
「Ruby Environment」セクションの「Location of JRuby JAR file:」で、ダウンロードしたjruby-complete-9.1.2.0.jarを選択します。

#### 拡張機能の開発

Burp Suiteや様々な拡張機能を使い込んでいくと、自分でも拡張機能を作ってみたくなることでしょう。
「Extender」の「APIs」では、拡張機能の開発で使うJava インタフェースのソースコードが確認できます。
また、以下のドキュメントが参考になりますので、拡張機能を開発する際は参照してください。

- Burp Extender [https://portswigger.net/burp/extender/](https://portswigger.net/burp/extender/)
- Burp API Javadoc [https://portswigger.net/burp/extender/api/](https://portswigger.net/burp/extender/api/)

