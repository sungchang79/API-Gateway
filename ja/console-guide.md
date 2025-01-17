## Application Service > API Gateway > コンソール使用ガイド

## API Gatewayサービス 
API GatewayサービスはAPI GatewayでサービスするAPIを管理する単位です。 
API Gatewayサービスごとに1つのAPIリソースと複数のステージを管理でき、ダッシュボードからAPI指標を確認できます。

### API Gatewayサービス作成 
API Gatewayサービス情報を入力した後、作成ボタンを押すとAPI Gatewayサービスが作成されます。

* **サービス名**：サービスの名前です。
* **サービス説明**：サービスの説明です。
* **サービスID**：サービスごとに任意で発行された固有のIDです。 

> **[参考] API Gatewayサービス作成数制限**
> API Gatewayサービスはプロジェクトごとに**最大10個**まで作成できます。

### API Gatewayサービス照会 
* 登録されたAPI Gatewayサービスリストが表示されます。
* リストからサービスを選択すると、登録されたステージリストが表示されます。
* リソースを管理するにはサービス設定列の**リソース**ボタンを押します。
* ステージを管理するにはサービス設定列の**ステージ**ボタンを押します。

### API Gatewayサービスの削除
* 登録されているAPI Gatewayサービスリストが表示されます。
* リストからサービスを選択し、**削除**ボタンをクリックします。
* 確認ウィンドウが表示されたら**確認**ボタンをクリックします。削除されたデータは復旧できません。

> **[注意] API Gatewayサービスを削除できない場合**
> API Gatewayサービスのステージと接続された使用量計画が存在する場合はAPI Gatewayサービスを削除できません。

## リソース
リソースはAPI Gatewayを通してサービスするAPIを設計する画面です。
すべてのAPIリクエストクライアントはAPI Gatewayリソースに定義されたAPIに対してリクエストできます。
リソースはAPIのリソースパスとメソッドを管理します。

1. リソースパス：APIパス 
2. リソースメソッド：HTTPメソッド 
3. プラグイン：リソースパスまたはメソッドに付加機能を追加します。 

### リソース作成 
1. リソースを作成するには**リソース作成**ボタンを押すか、左側リソースツリー画面で右クリックすると表示されるメニューから**リソース作成**を押します。
2. **リソースパス**を作成します。作成されたリソースパスを含めてフルパスは255文字以内で作成する必要があります。
    - 例：/products/, /products/{productsId}, /{proxy+}
3. **パス変数**：リソースパスには中括弧を使用して**パス変数**を作成できます。
    - **パス変数**は**{variable}**、下位パスを含むパス変数は**{variable+}**と宣言できます。 
        - **パス変数**はプラグインとバックエンドエンドポイント設定で活用できます。
        - **{variable}**はパス変数が位置するパスの値を変数で宣言します。
            - 例：/members/{memberId} 
                - /members/id1リクエストの**{memberId}**パス変数値は**id1**になります。
        - **{variable+}**はパス変数が位置する下位パスを含めて変数で宣言します。下位パスを含む変数には下位リソースパスを作成できません。
            - 例：/{proxy+} 
                - **/members/id1**リクエストの**{proxy+}**パス変数値は**members/id1**になります。
- **プラグイン**：選択されたパスに追加されたプラグインを作成されたメソッドにも追加するにはチェックします。
- リソースを作成する時にメソッドも一緒に登録するにはHTTPメソッドを選択します。
- 登録していないリソースパスでAPI Gatewayにリクエストすると404 Not Foundレスポンスを返します。

### リソースのインポート
Swagger v2.0 [OpenAPI Specification](https://swagger.io/specification/v2/)形式のファイルでリソースでインポートできます。
1. **リソースインポート**ボタンをクリックします。
2. Swagger**ファイル選択**ボタンをクリックしてファイルを選択するか、Swaggerの内容を直接入力します。
3. **適用**ボタンをクリックします。

> **[注意]リソースのインポートを行うと、既存リソースとモデルを上書き** 
> リソースをインポートすると、既存のリソースは削除され、インポートしたリソースで上書きされます。
> リソースをインポートすると、該当サービスに作成されていた既存のモデルは全て削除され、インポートしたモデルで上書きします。

> **[参考] 2021-11-23以前ステージエクスポート(Export)ファイルのインポート失敗** 
> 2021-11-23以前にステージのエクスポートを行ってダウンロードしたファイルでリソースのインポートを行うと、失敗する可能性があります。
> ステージエクスポートを行って新しく作成されたファイルを利用してリソースのインポートを行うか、次の操作で既存ファイルを変更してください。
> 変更作業
>   1. ファイル内x-api-nhn-apigateway > pluginsのプラグイン設定文字列をJSONオブジェクトに変換する必要があります。
>   2. ファイル内リソースメソッド > x-api-nhn-apigateway > pluginsにCORSプラグイン設定文字列が存在する場合は削除する必要があります。リソースメソッドにはCORSプラグインを設定することができず、その上位のリソースパスにCORSプラグインが設定されている場合、リソースのインポート時に自動的に追加されます。
> ガイドの内容で解決しない場合はサポートへお問い合わせください。

<details>
<summary>2021-11-23以前のステージエクスポートファイルのインポート失敗例</summary>

```
- [例1]インポート失敗：2021-11-23以前のステージエクスポートファイルは、pluginsのプラグイン設定値がJSON形式の文字列で構成されています
{
... 
    "x-nhncloud-apigateway": {
        "plugins": {
            "HTTP": "{\"frontendEndpointPath\":\"/{proxy+}\",\"backendEndpointPath\":\"/anything/${request.path.proxy+}\"}",
        }
    }
...
}
```

```
- [例1]インポート成功：pluginsのプラグイン設定値でJSON形式の文字列をJSONオブジェクトに修正したステージエクスポートファイル
{
...
    "x-nhncloud-apigateway": {
        "plugins": {
            "HTTP": {
                "frontendEndpointPath": "/{proxy+}",
                "backendEndpointPath": "/anything/${request.path.proxy+}"
            }
        }
    }
...
}
```

```
- [例2]インポート失敗：2021-11-23以前のステージエクスポートファイルは、リソースパスにCORSプラグインが設定されている場合、サブリソースメソッドにCORSプラグイン設定値が含まれています
{
...
        "paths": {
            "/anything": {
                "get": {
                    ...
                    "x-nhncloud-apigateway": {
                        "plugins": {
                            "MOCK": {
                                "statusCode": 200
                            },
                            "CORS": {
                                "allowedMethods": ["GET", "POST", "DELETE", "PUT", "OPTIONS", "HEAD", "PATCH"],
                                "allowedHeaders": ["*"],
                                "allowedOrigins": ["*"],
                                "exposedHeaders": [],
                                "maxCredentialsAge": null,
                                "allowCredentials": false
                            }                            
                        }
                    }
                },
                "options": {
                    "summary": "CORS",
                    ...
                },
                "x-nhncloud-apigateway": {
                    "plugins": {
                        "CORS": {
                            "allowedMethods": ["GET", "POST", "DELETE", "PUT", "OPTIONS", "HEAD", "PATCH"],
                            "allowedHeaders": ["*"],
                            "allowedOrigins": ["*"],
                            "exposedHeaders": [],
                            "maxCredentialsAge": null,
                            "allowCredentials": false
                        }
                    }
                }
            }
        }
...
}
```

```
- [例2]インポート成功：リソースメソッドにCORSプラグイン設定値を削除したステージエクスポートファイル
{
...
        "paths": {
            "/anything": {
                "get": {
                    ...
                },
                "options": {
                    "summary": "CORS",
                    ...
                },
                "x-nhncloud-apigateway": {
                    "plugins": {
                        "CORS": {
                            "allowedMethods": ["GET", "POST", "DELETE", "PUT", "OPTIONS", "HEAD", "PATCH"],
                            "allowedHeaders": ["*"],
                            "allowedOrigins": ["*"],
                            "exposedHeaders": [],
                            "maxCredentialsAge": null,
                            "allowCredentials": false
                        }
                    }
                }
            }
        }
...
}
```
</details>

### メソッド作成 
- 選択されたリソースパスに**HTTPメソッド**を作成します。 
    - サポートHTTPメソッド：HEAD、OPTIONS、GET、POST、PUT、DELETE、PATCH
- **メソッド名**：メソッドのエイリアスです。名前はリソースツリー画面に表示されます。
- **メソッド説明**：メソッドの説明です。
- **バックエンドエンドポイントタイプ**
    - HTTP(S)：API Gatewayで受信したAPIリクエストを定義されたバックエンドエンドポイントURLパスへ伝達します。
    - ユーザー定義レスポンス：APIゲートウェイは受信したリクエストに対して定義されたレスポンスを返します。
- **バックエンドエンドポイントタイプ：HTTP(S)**
    - バックエンドエンドポイントURLパス：受信したAPIリクエストを伝達するバックエンドエンドポイントサービスのAPI URLを設定します。
        - ルート(/)で始まる必要があります。
        - パスにはリソースで作成したコンテキスト変数を設定できます。(コンテキスト変数の詳細については[コンテキスト変数](./console-guide/#_11)を参照してください。)
- **バックエンドエンドポイントタイプ：ユーザー定義レスポンス**
    - ユーザー定義レスポンスを設定します。 
    - レスポンスステータスコード：レスポンスHTTPステータスコードを入力します。(必須)
    - ヘッダ：レスポンスヘッダの名前と値を入力します。
    - レスポンス本文：レスポンス本文を入力します。
    - ヘッダとレスポンス本文にはリソースで作成したコンテキスト変数を設定できます。(コンテキスト変数の詳細については[コンテキスト変数](./console-guide/#_11)を参照してください。)

- **プラグイン**：選択されたパスに追加されたプラグインを作成されたメソッドにも追加するにはチェックします。
- 登録していないHTTPメソッドをAPI Gatewayにリクエストすると、404 Not Foundレスポンスを返します。

> **[参考]リソースメソッド作成制限数** 
> メソッドはすべてのリソースパスを含めて**最大100個**まで作成可能です。

### リソースとメソッド修正
- リソースパス修正
    - リソースパスは修正できません。パスを修正するには削除して再度作成する必要があります。
- メソッド修正 
    1. HTTPメソッドは修正できません。HTTPメソッドを修正するには削除して再度作成する必要があります。
    2. メソッド名、説明、バックエンドエンドポイント項目は修正できます。 
    3. 修正をするには左側リソースツリーからメソッドを選択します。
    4. 設定を変更した後、**変更内容保存**ボタンを押します。

> **[参考] CORSプラグインにより登録されたOPTIONSメソッドの修正**
> CORSプラグインにより登録されたOPTIONSメソッドは修正できません。 

### リソースとメソッド削除 
- 削除するリソースパスまたはメソッドを選択します。
    - **選択削除**ボタンを押すと削除確認ウィンドウが表示されます。
    - 左側リソースツリーで右クリックすると表示されるメニューからリソース削除またはメソッド削除を押すと確認ウィンドウが表示されます。 
- 削除するには**確認**ボタンを押します。削除されたデータは復旧できません。

> **[注意]リソースパス削除**
> リソースパスを削除すると、選択されたリソースのパスの下位リソースパスとメソッドが全て削除されます。

> **[参考] CORSプラグインにより登録されたOPTIONSメソッドの削除**
> CORSプラグインにより登録されたOPTIONSメソッドは削除できません。 


### ステージリソース適用 
リソースを変更した後、変更されたリソースをステージに適用するには**ステージリソース適用**を行う必要があります。

1. 変更されたリソースをステージに適用するには**ステージリソース適用**ボタンを押します。
2. 変更されたリソースを適用する**ステージ**を選択します。
3. **適用**ボタンを押します。


> **[注意]ステージリソース適用**
> - ステージリソースを適用するには1つ以上のステージが存在する必要があります。
> - ステージにリソースが適用された後は元に戻せません。
> - すでにステージに最新リソースが適用されている場合、ステージリソースの適用ができません。


### プラグイン追加と削除
プラグインを通してAPI Gatewayで提供する付加機能を追加できます。

- **プラグイン適用位置**
    - プラグインはリソースパスまたはメソッドに追加できます。
    - リソースパスにプラグインを追加すると、選択されたパスの下位メソッドにプラグインが一括適用されます。
    - メソッドにプラグインを追加すると、選択されたメソッドにのみプラグインが適用されます。
- **プラグイン適用段階**
    - プラグインは**バックエンドリクエスト事前作業**と**フロントエンドレスポンス事前作業**段階に追加できます。 
        - **バックエンドリクエスト事前作業** ：API Gatewayに受信したAPIリクエストをバックエンドに伝達する前にプラグインを適用します。
        - **フロントエンドレスポンス事前作業**：バックエンドから伝達されたレスポンスをフロントエンドに伝達する前にプラグインを適用します。
- **プラグイン追加**
    - バックエンドリクエスト事前作業とフロントエンドレスポンス事前作業の**+プラグイン**ボタンを押します。
        1. 追加するプラグインをクリックします。
        2. プラグインの設定内容を入力した後、**追加**ボタンを押します。
        3. 選択されたパスを含めて下位パスとメソッドにプラグインを一括適用するには**下位パスとメソッドに上書き**をチェックします。 
            - **!注意**：下位パスとメソッドに追加しようとしているプラグインがすでに登録されている場合、設定が変更されるため注意してください。
        4. **変更内容保存ボタン**を押します。
- **プラグイン削除**
    1. バックエンドリクエスト事前作業とフロントエンドレスポンス事前の登録されたプラグインを選択します。 
    2. 選択されたパスを含めて下位パスとメソッドにプラグインを一括削除するには**下位パスとメソッドに上書き**をチェックします。 
    3. **削除**ボタンを押します。
    4. **変更内容保存ボタン**を押します。

> **[注意]プラグイン追加後、変更事項を保存**
> プラグインを追加した後、**変更事項保存ボタン**を押すと設定が保存されます。


### リクエストパラメータ 
リソースメソッド別リクエストパラメータとレスポンス形式、コンテンツタイプの設定を行います。
設定した内容は[API説明書](./console-guide/#api_2)に適用されます。

1. リソースメソッドを選択します。
2. **リクエストパラメータ**タブをクリックします。
3. リクエストパラメータ項目を入力します。 
    - 項目を追加するには、項目の右側にある**+ボタン**をクリックします。
    - 項目を削除するには、項目の右側にある**-ボタン**をクリックします。
    - クエリ文字列、ヘッダ、フォームデータパラメータ
        - 名前：パラメータの名前を入力します。 
        - 説明：パラメータの説明を入力します。
        - データタイプ：パラメータのデータタイプを選択します。
        - 必須かどうか：パラメータが必須かどうかを選択します。
        - Arrayかどうか：パラメータのデータが配列かどうかを選択します。 
    - リクエスト本文パラメータ
        - 名前：リクエスト本文パラメータの名前を入力します。 
        - 説明：パラメータの説明を入力します。
        - モデル：リクエスト本文の[モデル](./console-guide/#_25)を選択します。
    - コンテンツタイプ
        - サーバーに転送する文書のコンテンツタイプ(例：application/json)を入力します。 
4. **変更内容保存ボタン**をクリックします。 

### レスポンス 
HTTPレスポンスステータスコード別ヘッダとリクエスト本文項目とコンテンツタイプを設定します。
設定した内容は[API説明書](./console-guide/#api_2)に適用されます。

1. リソースメソッドを選択します。
2. **レスポンス**タブをクリックします。
3. レスポンスHTTPステータスコードの**追加ボタン**をクリックすると追加入力画面が表示されます。 
4. 追加するレスポンスHTTPステータスコードと説明を入力します。
5. **作成ボタン**をクリックします。 
6. 追加されたレスポンスHTTPステータスコードの行を選択します。
7. 各レスポンスHTTPステータスコード別レスポンスヘッダ、レスポンス本文を入力します。 
    - ヘッダ
        - 名前：ヘッダの名前を入力します。 
        - 説明：ヘッダの説明を入力します。
        - データタイプ：レスポンスヘッダのデータタイプを選択します。
    - レスポンス本文 
        - 名前：レスポンス本文パラメータの名前を入力します。 
        - 説明：レスポンス本文パラメータの説明を入力します。
        - モデル：レスポンス本文のモデルを選択します。 
8. コンテンツタイプを入力します。 
    - クライアントにレスポンスされる文書のコンテンツタイプ(例：application/json)を入力します。 
9. **変更内容保存ボタン**をクリックします。 

## コンテキスト変数
リソースのメソッド作成およびプラグイン設定時に、以下に定義された変数を使用できます。

| コンテキスト変数 | 説明 |
| -- | -- |
| ${request.clientIp} | APIをリクエストしたクライアントのIP |
| ${request.path.variable-name} | リソースで宣言した単一パス変数{variable-name}値参照 |
| ${request.path.variable-name+} | リソースで宣言した下位パスを含むパス変数{variable-name+}値参照 |

> **[注意]パス変数**
> 選択されたパスと上位パスに宣言されたパス変数のみ使用できます。

## プラグイン 
### CORS 
Cross-Site方式内でXMLHttpRequest APIを呼び出せるようにします。

- **プラグイン適用可能な位置**：リソースパス
- **プラグイン適用段階**：バックエンド事前リクエスト作業
- **CORSプラグイン設定**
    - **Access-Control-Allow-Credentials**：資格証明でリクエストする場合はTrueに設定する必要があります。
    - **Access-Control-Max-Age**：事前伝達リクエスト(Preflight)に対するレスポンスをどれくらいの間キャッシュするか、秒単位で入力します。-1～86400の間の値を入力できます。
    - **Access-Control-Allow-Origin**：リソースにアクセスできる原本サーバーのドメインを入力します。 
        - \*と入力すると、すべてのドメインを許可します。(ただし、\*と指定すると資格証明をサポートしないため、許可原本(allowed origin)に具体的なドメインを指定する必要があります。) 
        - 複数のドメインを許可するには、(カンマ)で区切って入力します。
        - ドメインはURI(スキーム、ドメイン、ポート)形式で入力する必要があります(例：http://example.nhncloudservice.com:8080)。
    - **Access-Control-Allow-Methods**：リソースアクセスを許可するメソッドを設定します。複数のメソッドを指定する場合は','で区切って入力します。
    - **Access-Control-Allow-Headers**：リクエストで使用できるHTTPヘッダを設定します。複数のヘッダを設定する場合','で区切って入力します。
    - **Access-Control-Expose-Headers**：ブラウザ(クライアント)がアクセスできるヘッダを設定します。複数のヘッダを設定する場合は','で区切って入力します。
    - 詳しいCORSの規約はhttps://www.w3.org/TR/cors/を参照してください。

> **[注意] CORSプラグイン**
> - CORSプラグインを登録すると、選択されたパスのメソッドにOPTIONSメソッドが登録されます。
>	下位パスとメソッドに上書きオプションをチェックした場合は下位パスにも登録されます。 
>	OPTIONSメソッドがすでに登録されている場合、 CORSにより自動作成されるOPTIONSメソッドに変更されます。
> - CORSプラグインを通して登録されたOPTIONSメソッドはリソースツリーから選択できず、修正と削除ができません。
> - CORSプラグインを削除するとCORSプラグインにより自動作成されたOPTIONSメソッドは一括で削除されます。 

### リクエストヘッダ変更 
リクエストヘッダを追加または変更します。 

- **プラグイン適用可能な位置**：リソースパス、メソッド
- **プラグイン適用段階**：バックエンドリクエスト事前作業
- **リクエストヘッダ変更設定** 
    - **\+**ボタンを押すとヘッダリストを追加できます。
    - ヘッダ名と値を入力します。 
    - ヘッダ値にはリソースで宣言したコンテキスト変数を設定できます。(コンテキスト変数の詳細については[コンテキスト変数](./console-guide/#_11)を参照してください。)

> **[参考]リクエストヘッダ追加と変更**
> - 原本リクエストにないヘッダは追加されます。
> - 原本リクエストにあるヘッダはリクエストヘッダ変更プラグインに設定されたヘッダ値に変更されます。
> - 原本リクエストにあるヘッダの削除はできません。

### レスポンスヘッダ変更 
レスポンスヘッダ変更プラグインはバックエンドレスポンスにヘッダを追加または変更します。 

- **プラグイン適用可能な位置**：リソースパス、メソッド
- **プラグイン適用段階**：フロントエンドレスポンス事前作業
- **\+**ボタンを押すとヘッダリストを追加できます。
- ヘッダ名と値を入力します。 
- ヘッダ値にはリソースで宣言されたコンテキスト変数を設定できます。(コンテキスト変数の詳細については[コンテキスト変数](./console-guide/#_11)を参照してください。)


> **[参考]レスポンスヘッダ追加と変更**
> - バックエンドエンドポイントのレスポンスにないヘッダは追加されます。
> - バックエンドエンドポイントのレスポンスにあるヘッダはリクエストヘッダ変更プラグインに設定されたヘッダ値に変更されます。
    
### リクエストクエリ文字列パラメータ追加
バックエンドエンドポイントリクエストにクエリ文字列パラメータを追加します。  
例：パラメータ名と値をname、valueに設定すると、**name=value**クエリ文字列パラメータがバックエンドエンドポイントをリクエストする時に追加されます。 

- **プラグイン適用可能な位置**：リソースパス、メソッド
- **プラグイン適用段階**：バックエンドリクエスト事前作業
- **\+**ボタンをクリックするとパラメータリストを追加できます。
- パラメータ名と値を入力します。
- パラメータ値にはリソースで宣言されたコンテキスト変数を設定できます。 (コンテキスト変数の詳細は[コンテキスト変数](./console-guide/#_11)を参照してください。)

> **[参考]リクエストクエリ文字列パラメータ**
> - 「原本リクエストのクエリ文字列パラメータ」のようなキーを持つ「リクエストクエリ文字列パラメータ」は、「原本リクエストのクエリ文字列」を代替せずに追加されます。
> - クエリ文字列パラメータの値はエンコードされてバックエンドエンドポイントに伝達されます。


## ステージ 
ステージはリソースを配布する段階です。 

- ステージごとに固有のステージURLが発行されます。 
- ステージはサービスごと、または環境(Profile)ごとにサービスを区分したり、それ以外の用途で活用できます。

### ステージ作成

1. API Gatewayサービスリストから**ステージ設定**を押します。
2. ステージタブから**ステージ作成**ボタンを押します。 
3. ステージ情報を入力した後、**作成**ボタンを押します。
    - **ステージ名** 
        - 数字と英字(小文字)のみ入力でき、30文字以内で作成できます。
        - ステージ名はステージURLに含まれています。
        - 基本ステージはステージ名を作成していない場合に作成されるステージです。基本ステージのステージURLにはステージ名が含まれません。
    - **ステージURL**：API Gatewayに統合リクエストが可能なステージURLです。 
        - APIリクエストクライアントはステージURLを通してAPIをリクエストできます。
        - ステージURLは次のような形式で発行されます。 
            - 基本ステージ：{region}-{api-gateway-service-id}.api.nhncloudservice.com
                - {region}：パンギョリージョン(kr1)
                - {api-gateway-service-id}：API GatewayサービスID
            - 一般ステージ：{region}-{api-gateway-service-id}-{stage-name}.api.nhncloudservice.com
                - {region}：パンギョリージョン(kr1)
                - {api-gateway-service-id}：API GatewayサービスID
                - {stage-name} ：入力されたステージ名
    - バックエンドエンドポイントURL
        - API Gatewayに受信したリクエストを伝達するバックエンドエンドポイントURLを作成します。 
        - スキーム(http:// またはhttps://)を含めてURLを作成する必要があります。
        - ドメインアドレスのみ入力するか、下位パスを含めて作成できます。 
            - 例：https://api.nhn.com , https://api.nhn.com/apis


> **[参考]ステージ** 
> - ステージを作成するにはリソースメソッドが1つ以上登録されている必要があります。
> - ステージはAPI Gatewayサービスごとに**最大10個**まで作成できます。
> - API Gatewayに受信したリクエストをバックエンドエンドポイントへ伝達する時、基本的にステージに定義されたバックエンドエンドポイントURLにリクエストを伝達します。


### ステージ修正 
1. 修正するステージを選択します。 
2. **ステージ修正**ボタンを押します。
3. ステージ情報を修正します。修正可能な項目はステージ説明、バックエンドエンドポイントURLです。
4. 設定を変更した後、**修正**ボタンを押します。

> **[注意]ステージ配布** 
> 修正されたバックエンドエンドポイントURLをAPI Gatewayサービスに適用するにはステージを配布する必要があります。


### ステージ削除
1. 削除するステージを選択します。
2. **ステージ削除**ボタンを押します。
3. 削除確認ウィンドウで**確認**を押すと削除されます。この作業はキャンセルできません。 

> **[注意]ステージ削除**
> - サービスで使用中のステージを削除すると、API Gatewayにリクエストが入らなくなります。
> - 削除されたステージは復旧できないため、必ずサービスで使用中ではないか確認してから削除を行ってください。
> - ステージに接続された使用量計画が存在する場合はステージを削除できません。


### リソースのインポート
リソースを変更した後、変更されたリソースをステージに適用するには、ステージ管理画面でリソースのインポートを進行します。 

1. 変更されたリソースをステージに適用するには**リソースインポート**ボタンを押します。

> **[注意]リソースのインポート*
> - ステージにリソースが適用された後は元に戻せません。
> - リソースに変更された事項がない場合は、リソースのインポートボタンが無効になります。


### ステージ配布
ステージに設定されたリソースと設定をAPI Gatewayサービスに適用するには、ステージを配布する必要があります。

1. **ステージ**タブで配布するステージを選択します。 
2. **ステージ配布**ボタンを押します。
3. ステージ配布画面が表示されます。
4. ステージ配布について説明を作成します。 (選択事項)
5. **ステージ配布**ボタンを押します。 
6. ステージ配布状態から配布状態を確認できます。
    -  **配布成功** 状態は、正常に配布された状態です。
    -  **配布失敗**状態は、配布中に作業エラーが発生した状態です。配布失敗が発生した場合は配布を再試行してください。繰り返し失敗する場合はサポートへお問い合わせください。

### ステージ配布履歴
ステージ配布後、配布された履歴を確認できます。以前の配布設定でステージを復元できます。

1. **ステージ**タブでステージを選択します。
2. **配布履歴**タブを選択します。
3. ステージ配布履歴を確認できます。
    - **配布されたステージ**：現在API Gatewayサービスに適用されている配布履歴を意味します。 
    - **ベースステージ**：現在のステージ設定のベースになる配布履歴を意味します。ステージ配布とステージの復元を行うと変更されます。 
    - **ステージの復元**：現在のステージ設定が該当配布履歴のステージ設定に変更されます。
    - **削除**：不要な配布履歴を削除します。

> **[注意]以前の配布履歴でステージを復元する**
> - ステージの復元を行う時、これをAPI Gatewayサービスに適用するには、ステージを配布する必要があります。

### ステージのエクスポート 
1. **ステージ**タブでステージを選択します。
2. **ステージエクスポート**タブを選択します。 
3. **ステージエクスポート**ボタンをクリックして選択されたステージのリソースをSwaggerファイルで保存します。


### API説明書
**ステージ配布**を行って配布された形状をAPI説明書で確認できます。
詳細は[API説明書](./console-guide/#api_2)を参照してください。

###  IP ACL
IP ACLを使って、指定したクライアントIPに対してAPI Gatewayリクエストを許可/拒否できます。

1. **ステージ**タブでステージを選択します。
2. **設定**タブを選択します。 
3. ステージツリー画面でステージのルート(/)パスを選択します。 
4. IP ACLを**有効化(On)**します。 
5. IP ACLを設定します。 
    - **IPアクセス制御タイプ**
        - 許可：指定したIPのみアクセスを許可し、他のIPは全て拒否します。(ホワイトリスト方式)
        - 拒否：指定したIPのみアクセスを拒否し、他のIPは全て許可します。(ブラックリスト方式)
    - **IPアクセス対象**
        - 1件入力または大量入力方式を選択してIPリストを簡単に登録できます。
        - IPアクセス対象はIPv4の単一IPまたはCIDRで入力できます。
            - 単一IP：10.0.0.1
            - CIDR例：10.0.0.1/24


> **[参考] IP ACL登録数制限およびクライアントIPチェック** 
> - IP ACLのIPアクセス対象は**最大100個**まで入力できます。
> - ネットワークアドレス変換(NAT：Network Address Translation)によりクライアントのSource IPが変更された場合、変更されたIPを基準にIP ACLをチェックするため、注意してください。

### 認証 > HMAC
HMAC認証を使用すると、API Gatewayに受信したリクエストが途中で攻撃者により改ざんされることを防止し、リクエスト有効時間を設定してReply Attack攻撃を予防します。

1. **ステージ**タブでステージを選択します。
2. **設定**タブを選択します。
3. ステージツリー画面でステージのルート(/)パスを選択します。 
4. 認証で**HMAC**を選択します。
5. HMAC設定を入力します。 
    - 秘密鍵：SignToStringを暗号化する秘密鍵です。外部に流出しないように注意します。 
    - リクエスト有効時間(秒)：設定した有効時間の両方向時間(リクエスト時間の過去/未来時間前後)を超えたリクエストを拒否します。リクエスト有効時間を0秒に設定するとAPI Gatewayは有効時間チェックをしません。
    - 必須検証ヘッダリスト：APIリクエスト検証に必ず含めるヘッダリストを作成します。複数入力するにはカンマ(,)で区切って入力します。


> **[参考] HMAC認証失敗レスポンス**
> HMAC認証失敗時、401 Unauthorizedレスポンスが返されます。
>
> **[注意]リクエスト有効時間**
> - 0秒に設定すると、リクエスト有効時間をチェックしません。この場合はReply Attack攻撃に弱くなります。
> - 有効時間をあまりにも短く設定すると、APIGatewayがリクエストを検証する前に有効期限が切れてリクエストが拒否されることがあります。期待するリクエスト有効時間より10秒以上長く設定することを推奨します。
> - APIクライアントは時間同期化設定NTP (Network Time Protocol, NTP)が有効かを必ず検証してください。同期化されていない時間情報によりリクエストが拒否されることがあります。
>
> **[参考]必須検証ヘッダ**
> 必須検証ヘッダを設定した場合、APIリクエスト検証時に必須検証ヘッダがリクエストに含まれているか、signatureにも該当ヘッダが含まれる値かを検証します。
> 設定時、必須検証ヘッダがリクエストとsingature作成時に含まれていたかを確認してください。


#### HMAC認証のためのAPIクライアント作業 
HMAC認証を行うにはAPIリクエストクライアントは次の認証ヘッダとリクエスト時間ヘッダを含めてリクエストする必要があります。

| ヘッダ名 | ヘッダ値 |
| --- | --- |
| Authorization | hmac algorithm="<encrypt_algorithm\>", headers="<validation_headers\>", signature="<base64_digest\>" |
| x-nhn-date |  ISO8601形式の時間|

> **[参考] x-nhn-dateのISO8601形式** 
> - UTC表記：yyyy-MM-dd'T'HH:mm:ssZ
> - UTC基準タイムオフセット表記：yyyy-MM-dd'T'HH:mm:ss±hh:mm

- Authorizationまたはx-nhn-dateヘッダがリクエストに含まれていない場合、HMAC認証に失敗します。

- Authorizationヘッダ値は次のように作成します。

| Credential名前 | 値 |
| --- | --- |
| algorithm  | HmacSHA256またはHmacSHA1 |
| headers |  HMAC認証時に検証するヘッダリスト<br> コンソールでHMAC必須検証ヘッダに登録したヘッダは必ず含める必要があります。  |
| signature |  SiginToString文字列を暗号化した後、Base64エンコードした値 |

#### SignToString形式
```
[HTTP Method]\n
[Request URL]\n
[Request datetime]\n
[header1-name]:[value1]\n
[header2-name]:[value1,value2...]\n
...
```

#### SignToString例 

- HTTPリクエスト原文
```
GET /members?isEnable=false&type=public HTTP/1.1
Host: http://kr1-example.api.nhncloudservice.com
x-nhn-date: 2021-02-23T00:00:00+09:00
x-nhn-client-id: nhn
x-nhn-client-ip: 10.0.0.1,10.0.0.2
```

- HTTPリクエスト原文に対するSignToString 
```
GET
/members?isEnable=false&type=public
2021-02-23T00:00:00+09:00
host:kr1-example.api.nhncloudservice.com
x-nhn-client-id: nhn
x-nhn-client-ip: 10.0.0.1,10.0.0.2
```

- signature作成コード例(Java)：SignToStringをHMAC暗号化した後、Base64エンコードした値
```
String secretKey = "HMACに設定した秘密鍵";
// 暗号化アルゴリズムHmacSHA1またはHmacSHA256
SecretKeySpec signingKey = new SecretKeySpec(secretKey.getBytes(), "HmacSHA256");  
Mac mac = Mac.getInstance("HmacSHA256");
mac.init(signingKey);

String message = "StringToSign";
byte[] rawHmac;
rawHmac = mac.doFinal(message.getBytes());
String authorization = new String(Base64.encodeBase64(rawHmac));
```


- 完成したHMAC認証ヘッダ 
```
Authorization:hmac algorithm="HmacSHA256", headers="host,x-nhn-client-id,x-nhn-client-ip" , signature="V5Dye9kgG3tvZOOZertd5LXE0q8CcJGXCxEFCR71hUE="
x-nhn-date:2021-02-23T00:00:00+09:00
```


> **[注意] SignToString作成注意事項**
> - SignToStringの各フィールドは改行文字(\n)で区切ります。
> - headersに定義されたヘッダはSignToString作成時に含まれている必要があります。
> - headersに定義したヘッダがない場合、[header name]と[header value]はSignToStringの作成に含めません。
> - headersに定義したヘッダ順序通りにSignToStringを作成する必要があります。
>     - 例：headers="header1,header2"の場合、SignToStringを作成する時もheader1, header2の順序でヘッダを追加する必要があります。
> - SignToStringのヘッダ名は英字小文字(lowercase)で統一して作成します。 
>     - 例：X-NHN-Header →  x-nhn-header
> - ヘッダ値が複数の場合、カンマ(,)で区切ってヘッダ値を作成します。
>   - 例：header1-name:header1-value1,header1-value2
> - ヘッダ名と値はコロン(:)で区切ります。値を区切る時にスペースを含めません。

### 認証 > JWT 
JWTトークンの署名とクレームを検証します。ユーザーサービスではトークンを検証せずにトークン値を使用できます。

1. **ステージ**タブでステージを選択します。
2. **設定**タブを選択します。
3. ステージツリー画面でステージのルート(/)パスを選択します。 
4. 認証で**JWT**を選択します。
5. JWT設定を入力します。 
    - **トークン暗号化アルゴリズム**：トークンを署名する時に利用した暗号化アルゴリズムを選択します。暗号化アルゴリズムはHS256、RS256をサポートします。
        - HS256トークンアルゴリズム 
            - 秘密鍵：トークンを署名するのに使用した秘密鍵を入力します。長さが256以上の秘密鍵を使用することを推奨します。
        - RS256トークンアルゴリズム
            - 公開鍵(PEM)：トークンを検証することができる公開鍵を入力します。PEM形式で入力する必要があります。
            - JWKS URI：API Gatewayがトークン署名検証と暗号化に必要なJSON Web Key Set JsonオブジェクトをインポートするHTTP JWKS URIを入力します。
    - **クレーム検証条件**
        - トークンのペイロード(payload)の登録されたクレーム(registered claim)に対するクレーム検証条件を入力します。
        - 登録されたクレームの詳細については[RFC7519-4.1.Registered Claim Names](https://tools.ietf.org/html/rfc7519#section-4.1)を参照してください。
        - クレーム検証条件のうち、1つでも一致しない場合は、認証に失敗します。
        - **クレーム**：トークンのペイロード(payload)の登録されたクレーム(registered claim)名です。
        - **データタイプとクレーム値**：
            - Array：複数の文字列をカンマ(,)で区切って入力します。入力した文字列配列にリクエストトークンのクレーム値のうち1つでも含まれていたら検証をパスします。
            - String：単一の文字列を入力します。リクエストトークンのクレーム値と一致すれば検証をパスします。
        - **必須**：選択すると、リクエストトークンにクレームが存在しない場合、検証に失敗します。無効になっているチェックボックスは選択を変更できません。
        - **値検証**：選択すると、リクエストトークンにクレームが存在する場合、設定されたクレーム値に含まれるか、一致するかを検証します。無効になっているチェックボックスは選択を変更できません。
    - **検証有効時間(秒)**：リクエストトークンのnbp、expクレーム検証時、検証有効時間を適用して検証します。0～86400(秒)まで入力できます。
6. ステージ配布を行います。
7. API Gatewayリクエストする時、AuthorizationヘッダにJWTトークンを追加してリクエストします。

| ヘッダ名 | ヘッダ値 |
| --- | --- |
| Authorization | Bearer "<jwt-token\>" |

> **[参考] JWTトークン認証失敗レスポンス**
> JWTトークンの認証失敗時、401 Unauthorizedレスポンスが返されます。
> 詳細については[エラーコード](./error-code/)文書を参照してください。
>
> **[参考] JWTトークン作成**
> API GatewayはJWTトークンの署名とクレーム条件が一致するかだけを検証します。JWTトークンはユーザーのアプリケーションまたは認証サービスプロバイダーを通して作成する必要があります。
> 開発およびテスト目的のJWTトークンの作成は[JWTトークンのデバッグ](https://jwt.io/)を参照してください。
>
> **[参考] JWKS(JSON Web Key Set) URIの説明と注意事項**
> JWKSはAPI Gatewayがトークンの署名を検証するために必要なJWK(Json Web Key)暗号化キーのJSONデータです。
> JWKの詳細な内容と仕様は[RFC7515](https://tools.ietf.org/html/rfc7517)文書を参照してください。
> 設定されたJWKS URIはAPI Gatewayがアクセスできるように公開されている必要があり、ネットワーク、ファイアウォールなどにより遮断されないようにします。
> 設定されたJWKS URIは、API Gatewayが常にアクセスができるように運用されている必要があります。
>
> **[注意] JWKSキャッシュ**
> API Gatewayは、JWKS URIのレスポンスを5分間キャッシュします。
> API GatewayのキャッシュによりJWKSの変更事項がAPI Gatewayに反映されるまで最大5分以上かかることがあります。


### 事前呼び出しAPI(Pre-call API)
事前呼び出しAPIは、バックエンドエンドポイントを呼び出す前にユーザーが指定したAPIを呼び出して、呼び出しのレスポンスコードに応じてバックエンドエンドポイントを呼び出すかどうかを決定します。
API Gatewayを介して入ったリクエストヘッダを含めて事前呼び出しAPIを呼び出し、事前呼び出しAPIは渡されたヘッダの内容に基づいてレスポンスコードを返します。

事前呼び出しAPIのレスポンスコードが200の場合、バックエンドエンドポイントを呼び出し、レスポンスコードが200ではない場合、事前呼び出しAPIのレスポンス結果を返します。
事前呼び出しAPIの呼び出しに失敗するとエラーを返します。

バックエンドエンドポイントを呼び出す前に別途APIを呼び出して認証が必要な場合や、先に呼び出す必要があるAPIが存在するなどの場合に活用できます。

1. **ステージ**タブでステージを選択します。
2. **設定**タブを選択します。
3. ステージツリー画面で事前呼び出しAPIを適用するパスまたはメソッドを選択します。
    - パスで設定した事前呼び出しAPIは、下位に定義されたすべての下位パスとメソッドの呼び出しに対して適用されます。
    - メソッドで設定した事前呼び出しAPIは、そのメソッドを呼び出す時に適用され、ルートパスで設定された事前呼び出しAPIは適用されません。
4. 事前呼び出しAPIを有効化(on)します。
    - 事前呼び出しAPIのメソッドタイプとURLを入力します。
    - キャッシュの有効時間は最大86400秒まで入力できます。入力した数字(秒)の間、事前呼び出しAPI(Pre-call API)のレスポンス結果がキャッシュされます。
    - キャッシュの有効時間に0を入力した場合、事前呼び出しAPI(Pre-call API)のレスポンス結果がキャッシュされず、リクエストごとに事前呼び出しAPI(Pre-call API)を呼び出します。
  
> **[参考]事前呼び出しAPIのレスポンス結果のキャッシュ**
> 事前呼び出しAPIのレスポンス結果コードが200の場合にのみレスポンス結果がキャッシュされます。
> レスポンス結果コードが200ではない場合、キャッシュの有効時間が設定されていてもレスポンス結果がキャッシュされません。

### バックエンドエンドポイントURL再定義 

API Gatewayに受信したリクエストをバックエンドエンドポイントへ伝達する時、基本的にステージに定義されたバックエンドエンドポイントURLへリクエストを伝達します。
特定パスまたはメソッドに対してバックエンドエンドポイントURLを再定義するには、バックエンドエンドポイントURLの再定義を設定します。

1. **ステージ**タブでステージを選択します。
2. **設定**タブを選択します。
3. ステージツリー画面でバックエンドエンドポイントURLを再定義するパスまたはメソッドを選択します。
4. バックエンドエンドポイントURLの再定義を有効化(on)します。
    - API Gatewayに受信したリクエストを伝達するバックエンドエンドポイントURLを作成します。
    - 下位パスを含めて作成できます。 
        - 例：https://api.nhn.com , https://api.nhn.com/apis

### リクエスト数制限

リクエスト数制限を利用してAPI Gatewayに受信するリクエストの毎秒リクエスト数を調節できます。これを利用してバックエンドエンドポイントを保護できます。

1. **ステージ**タブでステージを選択します。
2. **設定**タブを選択します。
3. ステージツリー画面でステージのルート(/)パスまたはメソッドを選択します。
    - ルートパスに設定すると、ステージにリクエスト数制限が適用されます。
    - メソッドに設定すると、各メソッドにリクエスト数制限が適用されます。上位パスに設定したリクエスト数制限は無視されます。  
4. リクエスト数制限を**有効(On)**にします。 
5. リクエスト数制限を設定します。 
    - 毎秒リクエスト数：毎秒呼び出し可能な最大リクエスト数を入力します。
    - リクエスト制限キー：基本リクエスト制限キーは、ルートに設定した場合はステージで、メソッドに設定した場合は選択したメソッドです。基本リクエスト制限キーにリクエスト制限キーを追加できます。
        - None：基本リクエスト制限キーでリクエストを制限します。
        - パス変数：基本リクエスト制限キーとパス変数値ごとにリクエストを制限します。選択したメソッドのパスにパス変数がある場合にのみ設定できます。
        - IP：基本リクエスト制限キーとリクエストクライアントIPごとにリクエストを制限します。
        - ヘッダ：基本リクエスト制限キーと設定したヘッダ名の値ごとにリクエストを制限します。  

>
> **[参考]リクエスト数制限レスポンス**
> 毎秒リクエスト数を超過すると、429 Too Many Requestsレスポンスが返されます。
>       
> **[注意]リクエスト制限キー**
> リクエスト制限キーを使用する場合、リクエストに指定したキーが含まれている必要があります。例えばリクエスト制限キーにヘッダを選択し、X-NHN-CLOUD値を入力した場合、リクエストヘッダにはX-NHN-CLOUDが含まれている必要があります。
> リクエストにリクエスト制限キーが見つからない場合、リクエスト数制限が適用されません。
>
> **[注意]毎秒リクエスト数の正確度**
> - 設定された毎秒リクエスト数と許可される実際のリクエスト数は、リクエストがAPI Gatewayに受信する時間、リクエスト処理時間およびその他の要因によって正確に一致しないことがあります。


### API Key

API GatewayにAPIリクエストする時、指定されたAPI Keyのみリクエストできるように制限します。

- 有効なAPI Key値かどうかをチェックします。
- 使用量計画のステージに接続されたAPI KeyのみステージのAPIをリクエストできます。 (詳細な方法は[使用量計画 > 使用量計画にステージ接続](./console-guide/#_38)を参照してください。)
- API Keyが接続された使用量計画のリクエスト限度をチェックします。 (使用量計画のリクエスト限度を設定する詳しい方法は[使用量計画 > 使用量計画作成](./console-guide/#_35)を参照してください。)

> **[参考] API Key失敗レスポンス**
> API Key値がリクエストヘッダに含まれていないか、有効ではない、もしくは使用量限度を超過する場合にAPIリクエストが拒否されます。
> 詳細な内容は[エラーコード](./error-code/)文書を参照してください。
1. **ステージ**タブでステージを選択します。
2. **設定**タブを選択します。
3. ステージツリー画面でAPI Keyを有効にするパスまたはメソッドを選択します。
    - パスで設定したAPI Keyはサブ定義されたすべてのサブパスとメソッドの呼び出しに対して適用されます。
4. API Keyを有効化(on)します。
5. ステージを配布します。
6. APIリクエスト時にx-nhn-apikeyヘッダにAPI Key値を追加してリクエストします。

| ヘッダ名 | ヘッダ値 |
| --- | --- |
| x-nhn-apikey | <primary api keyまたはsecondary api key\> |


## モデル
モデルを定義してリクエストパラメータとレスポンスで使用できる本文の形態を指定できます。

### モデル作成
1. API Gatewayサービスリストからサービス設定列の**リソース**をクリックします。
2. **モデル**タブで**モデル作成**ボタンをクリックします。
3. モデル情報を入力した後、**作成**ボタンをクリックします。
    - **モデル名**：
        - モデルの名前です。すでに存在するモデルの名前は使用できません。
        - 英数字のみ入力可能で、最大50文字以内で作成できます。
    - **モデル説明**：モデルの説明です。 (任意事項)
    - **モデルスキーマ**：
        - モデルが持つことができる構造を定義します。
        - モデルスキーマ定義は[JSON Schema](https://json-schema.org/) draft-04を使用します。

### モデル修正
1. モデルリストから修正するモデルを選択します。
2. **修正**ボタンをクリックします。
3. モデル情報を修正します。修正可能な項目はモデル説明、モデルスキーマです。
4. 設定を変更した後、**修正**ボタンをクリックします。

### モデル削除
1. モデルリストから削除するモデルを選択します。
2. **削除**ボタンをクリックします。
    - モデルがリクエストパラメータまたはレスポンスで使用中の場合は削除できません。
3. 削除確認ウィンドウが表示されたら**確認**ボタンをクリックします。削除されたデータは復元できません。


## API呼び出し確認

1. **ステージ**タブ内**設定**タブでステージツリーのメソッドを選択します。
2. 右側のステージURLを確認します。
3. ステージURLを指定したHTTPメソッドでAPIを呼び出します。
    - 例：
        - メソッド: GET
        - ステージURL : https://kr1-xxxxx-test.api.nhncloudservice.com/example
    ```
    curl --request GET 'https://kr1-xxxxx-test.api.nhncloudservice.com/example'
    ```


> **[注意]ステージ配布** 
> APIを呼び出すには配布成功状態の配布されたステージが必要です。

> **[参考] API呼び出しが正常に行われない場合**
> - 404 NotFound HTTPステータスコードが返される場合 
>    1. ステージを配布状態が配布成功状態になっているかを確認します。
>    2. リクエストメソッドとステージURLおよびパスが正しいか確認します。
>    3. バックエンドエンドポイントサービスからバックエンドエンドポイントURLパスに対するリクエストURLが存在するかを確認します。 
> - その他のエラーコードは[エラーコード](./error-code/)文書を参照します。 


> **[注意] API呼び出し制約事項**
> - GatewayクライアントからAPI Gatewayへリクエストするサイズ制限は**最大10MB**です。この値は調整できません。 
> - API GatewayからGatewayクライアントへのレスポンスサイズ制限は**最大10MB**です。この値は調整できません。 
> - リクエストに対するレスポンスタイムアウトは**最大60秒**です。バックエンドエンドポイントサービスでレスポンスが遅延する場合はタイムアウトが発生することがあります。


> **[注意] API Gatewayリクエスト遮断ポリシー**
> - API Gatewayサービスとバックエンドエンドポイントサービスを保護する目的でバックエンドエンドポイントサービスが応答しなかったり、レスポンス遅延(60秒以上)が持続的に発生する場合、該当バックエンドエンドポイントサービスに対するリクエストを一時的に拒否します。 
> - バックエンドエンドポイントサービスの内部エラー(4xx, 5xxなど)では遮断されません。 
> - 正常に稼働中の状態ではないか、レスポンス遅延(Timeout)が60秒以上発生するバックエンドエンドポイントは連携しないことを推奨します。


## API説明書
API説明書を利用するとAPI Gatewayに登録されたAPIの仕様をWebページ文書で管理できます。

### API説明書掲示
API説明書を掲示するための手順を案内します。

1. リソース設定ページの**モデル**タブをクリックしてリクエスト、本文のモデルを登録します。
2. リソース設定ページでリソースメソッドを選択した後、リクエストパラメータとレスポンスを入力します。
3. **ステージリソース適用**ボタンをクリックして、ステージに変更されたリソース内容を適用します。
4. ステージ設定ページの**ステージ配布**ボタンをクリックします。 
5. ステージ設定ページの**API説明書タブ**をクリックします。
6. API説明書の掲示タイプを選択します。
    - **掲示タイプ**：API説明書のアクセス制限を設定できます。
        - **公開**：アクセス制限なくAPI説明書にアクセスできます。
        - **非公開**：コンソールにアクセスできるユーザーのみAPI説明書にアクセスできます。
7. **掲示リンク**に表示されるURLでAPI説明書を確認できます。 

> **[参考]ステージ配布とAPI説明書掲示**
> - API説明書は、最初のステージ配布以降に掲示され、最初の掲示タイプは非公開に設定されます。
> - API説明書はステージ配布時に配布される形でアップデートされます。
>
> **[注意]掲示されたAPI説明書でAPI呼び出しテスト時のCORS設定**
> - 掲示されたAPI説明書ドメインアドレスと呼び出すAPIのドメインアドレスが異なるため、API説明書内で呼び出しをテストしたい場合はCORS設定が必要な場合があります。
> - 例：
> Access-Control-Allow-Origin: https://docs-apigw.cloud.toast.com
> Access-Control-Allow-Method: GET, POST, DELETE, PUT, PATCH, HEAD, OPTIONS
> Access-Control-Allow-Headers: Authorization, x-nhn-apikey, x-nhn-date


## ダッシュボード 

ダッシュボードを通してAPI Gatewayサービス、API KeyごとにAPI統計指標を確認できます。

### ステージタブ

1. **ダッシュボード**タブへ移動します。 
2. **ステージ**タブに移動します。   
3. 統計を確認するAPI Gatewayサービスを選択します。 
4. 統計を確認するステージをリストから選択します。 
5. 下部の**ステージ統計**タブでは、ステージの統計指標を確認できます。 
6. 下部の**リソース統計**タブでは、HTTPメソッドとパスごとに統計指標を確認できます。 

### 統計データ参考事項 

- **最大検索期間**
    - 過去3か月間のデータのみ照会できます。
- **統計データ作成周期**
    - すべての時間単位(1分、10分、1時間、1日)の統計データは、毎分更新されます。 
    - 統計データは収集されるデータサイズによって作成が遅延することがあります。

### ステージ統計

- **グラフ表示基準**
    - 検索期間に応じて統計の単位は次のように表示されます。
        - 1時間以下：1分単位
        - 1時間超過～1日以下：10分単位
        - 1日超過～1週以下：1時間単位
        - 1週超過：1日単位
-  **統計グラフ**
    - API呼び出し成功数：返されたHTTPステータスコードが2XX、3XXのAPI呼び出し数
    - API呼び出し失敗数：返されたHTTPステータスコードが4XX、5XXのAPI呼び出し数
    - 平均レスポンス時間(ms)：API Gatewayにリクエストが入った後、APIリクエストクライアントにレスポンスを返すまでの平均時間(ms)
    - ネットワークアウトバウンドトラフィック：API GatewayからAPIリクエストクライアントへ返されたデータのバイトサイズ

### リソース統計 
リソースパスとHTTPメソッドごとに区切られた詳細な統計指標を確認できます。 

- **HTTPメソッド**：リクエストしたHTTPメソッド
- **パス**：リクエストとマッピングされたリソースパス 
- **API呼び出し成功数**：返されたHTTPステータスコードが2XX、3XXのAPI呼び出し数
- **API呼び出し失敗数**：返されたHTTPステータスコードが4XX、5XXのAPI呼び出し数
- **HTTP 2XX～5XXコード**：ステータスコードグループ別API呼び出し数
- **API Gatewayからすぐに返された数**：バックエンドエンドポイントサービスにリクエストを伝達せず、API Gatewayから返されたAPI呼び出し数
- **平均レスポンス時間(ms)**：API Gatewayにリクエストが入った後、APIリクエストクライアントに返すまでの平均時間(ms)
- **ネットワークアウトバウンドトラフィック**：API GatewayからAPIリクエストクライアントへ返されたデータのバイトサイズ

### API Key統計
API Keyごとに呼び出し数を日単位グラフで確認できます。

1. **ダッシュボード**タブに移動します。
2. **API Key**タブに移動します。
3. 統計を確認するAPI Keyを選択します。
    - **グラフ表示基準**
        - 検索期間設定は日単位にすることができ、1日単位で表示されます。
    - **統計グラフ**
        - **API呼び出し数**：API Keyが使用されたすべてのAPI呼び出し数
        - **API Gatewayから直接レスポンスされた数**：API Gatewayプラグインや使用量制限を通過できずにAPI GatewayからレスポンスされたAPI呼び出し数

## 使用量計画
使用量計画のステージに接続されたAPI KeyのみステージAPIをリクエストできるように制限することができ、使用量制御設定を行って接続されたAPI Keyごとに共通使用量制限を適用できます。

- 使用量計画をAPI Gatewayサービスに適用するには次のプロセスが必要です。
- `使用量計画作成 -> 使用量計画にステージ接続 -> 使用量計画が接続されたステージにAPI Key接続 -> ステージ設定でAPI Keyを有効化`
- 使用量計画の作成およびステージ、 API Keyの接続プロセスについての詳細な内容は以下を参照してください。

### 使用量計画の作成
1. 使用量計画リストで**使用量計画作成**ボタンをクリックします。
2. 使用量計画情報を入力した後、**作成**ボタンをクリックします。
    - **使用量計画の名前**：使用量計画の名前です。
    - **使用量計画の説明**:使用量計画の説明です(任意事項)。
    - **毎秒リクエスト数制限**：毎秒呼び出し可能な最大リクエスト数を入力します(任意事項)。
    - **割り当て量期間単位**：日/月別呼び出し可能な最大リクエスト数を入力します(任意事項)。
    - **リクエスト割り当て量**：割り当て量期間単位を設定すると入力することができ、指定された割り当て量期間に呼び出し可能な最大リクエスト数を入力します。

> **[参考]リクエスト割り当て量限度の再設定**
> リクエスト割り当て量は毎月1日(月別期間)、毎日(日別期間) UTC 00:00:00に再設定されます。
### 使用量計画の修正
1. 使用量計画リストから修正する使用量計画を選択します。
2. **修正**ボタンをクリックします。
3. 使用量計画情報を修正します。
4. 設定を変更した後、**修正**ボタンをクリックします。

> **[注意]使用量計画リクエスト制御設定の修正**
> 使用量計画で毎秒リクエスト数制限、リクエスト割り当て量を修正する場合、別途の配布手順を踏まなくても接続されたAPIに反映されます。
> 割り当て量期間の単位を「日」または「月」に修正すると、接続されたAPI Keyリクエスト割り当て量の使用量は維持されます。リクエスト割り当て量の限度を下げると使用量が超過することがあります。
> 割り当て量期間の単位を「なし」に修正すると、接続されたAPI Keyのリクエスト割り当て量使用量は初期化されます。



### 使用量計画の削除
1. 使用量計画リストから削除する使用量計画を選択します。
2. **削除**ボタンをクリックすると削除確認ウィンドウが表示されます。
3. 確認ウィンドウが表示されたら**確認**ボタンをクリックします。削除されたデータは復旧できません。

> **[参考]接続されたステージがある場合は使用量計画の削除不可**
> 使用量計画と接続されたステージを全て解除した後、使用量計画を削除できます。
### 使用量計画にステージ接続
API Keyがリクエスト可能なステージを定義するために使用量計画にステージを接続します。

1. 使用量計画リストから使用量計画名列の**名前**のリンクをクリックします。
2. **ステージ接続**ボタンをクリックします。
3. 接続するAPI Gatewayサービスとステージを選択した後、**確認**ボタンをクリックします。

> **[参考]すでに接続されたステージ**
> すでに接続されたステージは選択リストに表示されません。
### 使用量計画に接続されたステージの解除
1. 使用量計画リストから使用量計画名列の**名前**のリンクをクリックします。
2. 接続されたステージリストから接続解除するステージを選択します。
3. **ステージ接続解除**ボタンをクリックします。
4. 確認ウィンドウが表示されたら**確認**ボタンをクリックします。

> **[参考]接続されたAPI Keyがある場合はステージ解除不可**
> 使用量計画に接続されたステージを解除するにはステージに接続されたすべてのAPI Keyを解除する必要があります。
### API Key接続
使用量計画に接続されたステージのAPIを呼び出すためにAPI Keyを接続します。

1. 使用量計画リストから使用量計画名列の**名前**のリンクをクリックします。
2. 接続されたステージリストからAPI Keyを接続するステージを選択します。
3. 下部の**API Key接続**ボタンをクリックします。
4. 追加するAPI Keyを選択した後、**確認**ボタンをクリックします。

> **[参考]**他の使用量計画の同じステージに接続されたAPI Keyは選択できるリストに表示されず、接続できません。
### API Key接続解除
1. 使用量計画リストから使用量計画名列の**名前**のリンクをクリックします。
2. 接続されたステージリストからAPI Keyを接続解除するステージを選択します。
3. 下部のリストから接続解除するAPI Keyを選択した後、**API Key接続解除**ボタンをクリックします。
4. 確認ウィンドウが表示されたら**確認**ボタンをクリックします。

### API Keyの使用量計画の変更
1. 使用量計画リストから使用量計画名列の**名前**のリンクをクリックします。
2. 接続されたステージリストから使用量計画を変更するAPI Keyが存在するステージを選択します。
3. 下部のリストから使用量計画を変更するAPI Keyを選択した後、**使用量計画変更**ボタンをクリックします。
4. 変更する使用量計画を選択した後、**確認**ボタンをクリックします。

> **[参考]**選択したステージが接続された他の使用量計画にのみ変更できます。


> **[注意]** 使用量計画変更時、API Keyリクエスト割り当て量の使用量初期化
> 割り当て量期間の単位が「日」または「月」の使用量計画に変更すると、接続されたAPI Keyリクエスト割り当て量の使用量は維持されます。リクエスト割り当て量の限度が低い使用量計画に変更すると、使用量が超過することがあります。
> 割り当て量期間の単位が「なし」の使用量計画に変更すると、接続されたAPI Keyリクエスト割り当て量の使用量は初期化されます。


## API Key
- API Keyでは使用量計画、ステージと接続されてAPI GatewayサービスAPIにアクセスするための文字列値を管理します。
- APIをリクエストする時、API Keyの値でPrimary API Key、Secondary API Keyを使用できます。

### API Key作成
1. API Keyリストから**API Key作成**ボタンをクリックします。
2. API Key情報を入力した後、**作成**ボタンをクリックします。
    - **API Keyの名前**：API Keyの名前です。
    - **API Keyの説明**：API Keyの説明です。 (任意事項)
    - **API Keyの状態**：API Keyの有効化状態を選択します。
        - ACTIVE：API Keyが有効になっていて使用できる状態です。
        - INACTIVE：API Keyが無効になっていて使用できない状態です。

### API Keyの修正
1. API Keyリストから修正するAPI Keyを選択します。
2. **修正**ボタンをクリックします。
3. API Key情報を修正します。修正可能な項目はAPI Keyの名前、API Keyの説明、 API Keyの状態です。
4. 設定を変更した後、**修正**ボタンをクリックします。

> **[注意] API Keyの状態変更**
> API Keyの状態をINACTIVEに変更すると、該当API Keyを使用できません。
### API Keyの削除
1. API Keyリストから削除するAPI Keyを選択します。
2. **削除**ボタンをクリックすると削除確認ウィンドウが表示されます。
3. 確認ウィンドウが表示されたら**確認**ボタンをクリックします。削除されたデータは復旧できません。

> **[参考]接続された使用量計画、ステージがある場合は削除不可**
> 接続された使用量計画、ステージがある場合はAPI Keyを削除できません。
### API Keyの再発行
APIリクエスト時にAPI Key値として使用されるPrimary API Key、Secondary API Keyは再発行できます。

1. API KeyリストからAPI Keyを選択します。
2. 下部の**API Key**タブを選択します。
3. Primary API Key、Secondary API Key項目横の**再発行**ボタンをクリックすると確認ウィンドウが表示されます。
4. 確認ウィンドウが表示されたら**確認**ボタンをクリックします。
    - 再発行する場合、以前のAPI Key値は無効になります。

### API Keyと接続されたステージ
1. API KeyリストからAPI Keyを選択します。
2. 下部の**接続されたステージ**タブを選択します。
3. 接続されたステージリストを確認できます。
    - **ステージURL**：接続されているステージURLです。
    - **使用量計画**：接続されている使用量計画情報です。
