## Application Service > API Gateway > Enumコード

## Enumコード
API v1.0ガイド文書で参照されるEnumコード文書です。

### API Gatewayリージョン
- API Gatewayサーバーが位置するリージョンを意味します。

| 名前 | 説明 |
| --- | --- |
| KR1 | 韓国(パンギョ)リージョン |


### API Gatewayサービスタイプ
- パブリック(Shared)または専用(Dedicated)区分に基づくAPI Gatewayのサービスタイプです。 
- 現在はパブリックAPI Gatewayサービスタイプのみサポートされます。 

| 名前 | 説明 |
| --- | --- |
| SHARED | パブリックAPI Gatewayサービスタイプ |


### HTTPメソッドタイプ
- サポートされるHTTPメソッドタイプです。

| 名前 | 説明 |
| --- | --- |
| GET | HTTP GETメソッド |
| POST | HTTP POSTメソッド | 
| DELETE | HTTP DELETEメソッド | 
| PUT | HTTP PUTメソッド | 
| OPTIONS | HTTP OPTIONSメソッド | 
| HEAD | HTTP HEADメソッド | 
| PATCH | HTTP PATCHメソッド | 


### リソースプラグインタイプ
- リソースに設定可能なプラグインタイプです。

| 名前 | 説明 |
| --- | --- |
| HTTP | API Gatewayに受信したリクエストを定義されたバックエンドエンドポイントURLパスへ渡します。 |
| MOCK | API Gatewayに受信したリクエストに対して定義されたレスポンスを返します。 | 
| CORS | Cross-Site方式内でXMLHttpRequest APIを呼び出せるようにします。 | 
| SET_REQUEST_HEADER | リクエストヘッダの追加または変更を行います。  | 
| SET_RESPONSE_HEADER | バックエンドレスポンスにヘッダを追加または変更します。 | 
| ADD_REQUEST_QUERY_PARAMETER | バックエンドエンドポイントリクエストにクエリ文字列パラメータを追加します。   | 


### リソースリクエスト/レスポンスパラメータデータ型
- リソースリクエスト/レスポンスパラメータで設定できるデータ型です。

| 名前 | 説明 |
| --- | --- |
| STRING | Stringデータ型 |
| BOOLEAN | Booleanデータ型 | 
| INTEGER | Integerデータ型 | 
| LONG | Longデータ型 | 
| FLOAT | Floatデータ型 | 
| DOUBLE | Doubleデータ型 | 
| FILE | Fileデータ型。リクエストパラメータ > フォームデータでのみ設定可能。 | 


### ステージリソース > プラグインタイプ
- ステージリソースパスまたはメソッドに設定可能なプラグインタイプです。 

| 名前 | 説明 |
| --- | --- |
| IP_ACL | IPアクセス制限プラグイン | 
| HMAC | HMACリクエスト検証プラグイン |
| JWT | JWTトークン検証プラグイン | 
| API_KEY | API Key検証プラグイン | 
| PRE_API | 事前呼び出しAPIプラグイン | 
| RATE_LIMIT | リクエスト数制限プラグイン | 


### JWT > 暗号化アルゴリズム 
- JWTトークンの署名に使用する暗号化アルゴリズムです。

| 名前 | 説明 |
| --- | --- |
| HS256 | 対称鍵アルゴリズムです。HS256(HMAC with SHA-256)アルゴリズムを使用してトークンを署名します。  |
| RS256 | 非対称鍵アルゴリズムです。公開/秘密鍵を使用してRSA256(RSA Signature with SHA-256)アルゴリズムを使用してトークンを署名します。 | 


### JWT > クレームデータ型 
- JWTクレームのデータ型です。

| 名前 | 説明 |
| --- | --- |
| Array | 配列形式のデータ型です。  |
| String | 文字列形式のデータ型です。 | 
| NumericDate | ミリ秒を無視して1970-01-01T00:00:00Z UTCから指定されたUTC日/時間までの秒数を表すデータ型です。 |


### JWT > RS256暗号化アルゴリズム > Public Key Type 
- RS256は公開鍵/秘密鍵ベースの暗号化アルゴリズムを使用します。公開鍵設定方式を設定します。

| 名前 | 説明 |
| --- | --- |
| RSA_PUBLIC_KEY | PEM形式の公開鍵を設定する方式です。 |
| JWKS_URI | 公開鍵を照会できるJson Web Key Sets URIに設定する方式です。|


### リクエスト数制限 > 制限キー
- リクエスト数制限が適用されるキーです。

| 名前 | 説明 |
| --- | --- |
| DEFAULT | リソースメソッドのリクエスト数制限を適用します。 |
| IP | クライアントIPごとにリソースメソッドのリクエスト数制限を適用します。 |
| HEADER | 指定されたヘッダ名の値ごとにリソースメソッドのリクエスト数制限を適用します。 |
| PATH_VARIABLE | パス変数ごとにリソースメソッドのリクエスト数制限を適用します。 |


### ステージ配布 > 配布状態
- ステージ配布作業の状態です。

| 名前 | 説明 |
| --- | --- |
| DEPLOYING | 配布進行中 | 
| COMPLETE | 配布完了(成功) | 
| FAILURE | 配布失敗 | 


### 使用量プラン > 割り当て量期間単位
- 割り当て量が初期化される期間単位です。

| 名前 | 説明 |
| --- | --- |
| DAY | 日単位で呼び出し量を制限。毎日UTC 00:00:00に初期化。| 
| MONTH | 月単位で呼び出し量を制限。毎月1日UTC 00:00:00に初期化。 | 


### API Keyの状態
- API Keyの状態です。
- 無効になっているAPI Keyは、API Keyの認証に失敗してAPIを呼び出せません。

| 名前 | 説明 |
| --- | --- |
| ACTIVE | 有効状態 | 
| INACTIVE | 無効状態 |


### API Keyタイプ
- 発行されたAPI KeyのPrimary API KeyとSencondary API Keyのタイプです。 

| 名前 | 説明 |
| --- | --- |
| PRIMARY | Primary API Key | 
| SECONDARY | Secondary API Key |


### API Keyの購読状態
- API Keyの購読状態です。

| 名前 | 説明 |
| --- | --- |
| APPROVAL | 承認状態 | 
