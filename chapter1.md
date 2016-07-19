# 1 Burp Suite 概要

## 1.1 Burp Suiteとは

Burp SuiteはPortSwigger社がJavaで作成した、ローカルProxyを中心に構成されたWebアプリケーションのセキュリティ診断に特化したツールです。ローカルProxyは、会社や学校などで使用されているProxyとは異なり、Webアプリケーションのセキュリティ診断やデバックなどに活用されます。同様のツールとしてBurp Suite以外にもOWASP ZAPやFiddlerなどが存在しています。

Burp Suite　 [http://portswigger.net/](http://portswigger.net/)

![Burp Suite](./img/logo.png "Burp Suite")

## 1.2 特徴

Burp Suiteは、プロフェッショナル版（Professional Edition）とフリー版（Free Edition）の2種類あります。最新バージョンは、フリー版v1.7.03で、プロフェッショナル版v1.7.03です（2016年7月19日時点）。

Burp Suiteは以下の機能で構成されており、プロフェッショナル版でしか利用できない機能もあります。

| 機能 | 概要 |
|:-----------|:------------|
| Target | 対象サイトの詳細情報を収集するsite mapの作成やターゲットとなるスコープを設定します。 |
| Proxy | ブラウザとWebサーバの間でリクエストやレスポンスを仲介し、内容変更などの制御を行います。 |
| Spider | 事前に設定されたスコープ内で自動巡回し、コンテンツの洗い出しを行います。 |
| Scanner | プロフェッショナル版の機能で、アクティブスキャン(動的解析)およびパッシブスキャン(静的解析)による脆弱性スキャンを行います。 |
| Intruder | 定型化されたパターンによる自動的なスキャンを行います。Scannerとは異なり、結果の分析は行いません。　|
| Repeater | リクエストを手動で修正し再送付します。 |
| Sequencer | トークンなどのランダム性を解析します。 |
| Decoder | BASE64などのエンコード・デコードやhash算出を行います。 |
| Comparer | リクエスト、レスポンスの差分を表示します。 |
| Extender | BApp Storeや独自の拡張プログラムを制御します。 |
| User Options | UIなどBurp Suiteの実行環境に関するオプションを設定します。 |
| Project Options | Projectに関するオプションを設定します。 |
| Alerts | エラーメッセージなどを出力します。 |
| その他 | Userオプション、Projectオプションの保存や読み込みなどを行います。 |

## 1.3 診断プロセス

Burp Suiteを使って効果的に診断するには、手動と自動による診断を組み合わせる必要があります。ブラウザを用いて対象となるアプリケーションへアクセスし、情報を収集します。収集した情報を分析し、必要に応じてBurp Suiteの設定を変更します。設定後、脆弱性スキャンを行います。

![ワークフロー](./img/burp_workflow.png "ワークフロー")

- 対象アプリケーションの調査(Recon and Analysis)
- 各機能の設定(Tool Configuration)
- 脆弱性スキャン(Vulnerability Detection and Exploitation)

### 対象アプリケーションの調査(Recon and Analysis)

このフェーズでは、手動でブラウザを操作し、対象アプリケーションをマッピングします。Proxy historyとTargetのsite mapにブラウザでアクセス下すべてのリクエストが登録されていきます。site mapは、レスポンスのリンクやフォームなどからコンテンツの存在を予測します。存在しているがまだアクセスしていないコンテンツを見つけ、ブラウザでアクセスしていきます。

### 各機能の設定(Tool Configuration)

対象となるアプリケーションでBurp Suiteが動作するように、Burp Suiteの設定を確認、変更します。以下の設定がポイントです。

#### ディスプレイ

HTTPログを表示するためのフォントや文字コードを変更します。日本語に対応していないフォントの場合、日本語が正常に表示されないため、対応したフォントなどを選択してください。

#### スコープ

対象とする範囲(スコープ)を設定します。設定するとProxy historyやTarget site mapでの表示内容のフィルタや、インターセプトするリクエスト・レスポンスの実行範囲を制限できます。この設定により、誤ってほかの環境へアクセスするミスを抑制します。

#### 認証

BASIC認証などの認証を設定します。

#### ログの保存

Loggingまたはextensionなどの拡張機能を用いてログを保存します。
フリー版の場合、stateファイルおよびProjectファイルの作成ができないため、特に重要です。

### 脆弱性スキャン(Vulnerability Detection and Exploitation)

対象アプリケーションを調査し必要な設定を実施後、脆弱性スキャンを実施します。フリー版ではProxyでインターセプトしたリクエストを変更するか、IntruderやRepeaterを利用します。プロフェッショナル版ではScannerも利用できます。
