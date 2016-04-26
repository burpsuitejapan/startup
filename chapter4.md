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
1. ブラウザでアクセスする(※この時以下二点の設定状況を確認)
  - ブラウザ側で、3章で説明したProxy設定がされていること
  - 「Intercept」タブが「Intercept is off」と設定されていること
2. 「HTTP hisotry」タブで通信内容を閲覧  
  「HTTP hisotry」タブの画面構成及び見方について説明  
  上部フィールドについての説明(以下の情報が表示されている)
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

  選択すると下部タブにRequest＆Pesponseデータの詳細を閲覧できる  
  下部タブの詳細について説明(Requestタブと Pesponseタブ)  
  以下タブにて項目ごとにデータを表示可能
    - Raw
    - Params
    - Headers
    - Hex

  Filetr機能の説明

### 4.2.2 値を書き換えて送信してみよう！
1. ブラウザでアクセスする(※この時以下二点の設定状況を確認)
  - ブラウザ側で、3章で説明したProxy設定がされていること
  - 「Intercept」タブが「Intercept is on」と設定されていること
2. 「Intercept」タブで値を変更  
「Intercept」タブの画面構成及び見方について説明
  - 上部ボタン
    - Forward
    - Drop
    - Intercept on or off
    - Action
  - 下部タブ
    - Raw
    - Params
    - Headers
    - Hex
3. 「HTTP hisotry」タブで結果を閲覧  
「Edited request」のタブに関する説明    
requestだけじゃなくてresponseのインターセプトについても補足する

## 4.3 その他

### 4.3.1 リクエストの再送信

Repeaterの使い方

### 4.3.2 Scope設定

スコープ設定の必要性も。

### 4.3.3 サーバ証明書設定

サーバ証明書の設定が必要な理由

- 暗号化通信サイトにアクセスするとエラーが発生して画面が表示されない
-- BurpSuiteの「オレオレ証明書」がブラウザに弾かれる

1.Burpから取得した証明書をブラウザにインポート


### 4.3.4 ログ保存設定

Loggingについて。Free edition前提なので。

### 4.3.5 アップストリームProxy設定

なぜアップストリームを使うのかも含めて。

### 4.3.6 Intruder

一番ベーシックな使い方。結果の見方も。Grep matchいれたい。

### 4.3.7 Extender

Extenderがどういうものか。どういうことができるのか。
