## Application Service > API Gateway > APIエラーコード

|エラーコード|エラーメッセージ|説明|
|---|---|---|
|0|SUCCESS|成功|
|-1|FAIL|失敗|
|400100000|Invalid request.|無効なリクエストです。|
|400100001|Invalid value in the request.|リクエストに無効な値があります。|
|400100002|Invalid header name.|無効な形式のヘッダ名です。|
|401100000|Invalid appKey.|無効なアプリケーションキーです。|
|401100001|Invalid uuid.|ユーザー情報が有効ではありません。|
|403100000|Not allowed user.|権限がありません。|
|409100000|Could not complete the request due to a duplicate request.|重複リクエストによりリクエストを完了できません。|
|500100000|DB query failed.|一時的なエラーです。エラーが続く場合はサポートへお問い合わせください。|
|400101000|Exceeded the maximum service count.|サービスの最大作成数を超えました。|
|404101000|Could not find API Gateway service.|API Gatewayサービスが存在しません。|
|400102000|There are no resources to stage.|作成されたリソースのメソッドがないため、ステージを作成できません。|
|400102005|Invalid x-nhncloud-apigateway plugins.|x-nhncloud-apigateway pluginsフィールドに無効な値があります。|
|400102012|Exceeded the maximum resource method count.|リソースメソッドの最大作成数を超えました。|
|400102013|There are no resources to create.|作成するリソースがありません。|
|400102014|Failed to delete root resource.|ルート('/')リソースは削除できません。|
|400102015|Invalid resource plugin configuration.|リソースプラグイン設定に誤りがあります。|
|409102000|Failed to create duplicated resources.|重複したパスリソースは作成できません。|
|400103000|Path variable cannot be used. Only variables declared for the selected path or above can be set.|無効なパス変数です。|
|400103001|Failed to update stage resource. Stage resource plugin's position is invalid.|リクエストしたリソースで設定できないステージプラグインです。|
|400103002|Failed to update stage resource. PRE_API's URL is not allowed to use stage URL.|無効な事前呼び出しのURL形式です。|
|400103003|Failed to update stage resource. Custom endpoint URL is not allowed at this stage resource path.|バックエンドエンドポイントURLの再定義を設定できないリソースです。|
|400103004|Failed to create or update stage. Invalid backend endpoint URL format.|無効なバックエンドエンドポイントURL形式です。|
|400103005|Failed to delete stage. The stage have connected usage plan.|ステージが関連付けられている使用量プランがあります。ステージの関連付けを削除した後にステージを削除できます。|
|400103006|Exceeded the maximum stage count.|ステージの最大作成数を超過しました。|
|404103000|Could not find stage.|ステージが存在しません。|
|404103001|Could not find stage resource.|ステージリソースが存在しません。|
|409103002|Failed to create duplicated stage name.|重複したステージ名は作成できません。|
|409103003|The latest resource has already been applied.|すでにステージに最新リソースが適用されています。|
|500103000|Invalid stage resource plugin configuration.|ステージ配布リクエストが失敗しました。しばらくしてから再度お試しください。|
|500103001|Failed to create stage. Please try again.|ステージの作成が失敗しました。しばらくしてから再度お試しください。|
|500103002|Could not find any server group.|ステージの作成に失敗しました。しばらくしてから再度お試しください。|
|500103003|Failed to delete stage URL.|ステージの削除が失敗しました。しばらくしてからお試しください。|
|400104000|Unable to delete base stage deploy history or the currently deployed stage deploy history.|現在配布された履歴とベースの配布履歴は削除できません。|
|400104001|Only possible to rollback stage for the completed deploy status.|ステージを元に戻せない配布状態の履歴です。|
|400104002|Empty stage resource for deploying.|作成されたリソースがないためステージを作成できません。|
|400104003|Empty path on stage resource for deploying.|作成されたリソースがないためステージを作成できません。|
|409104000|Unable to rollback stage. No difference with current stage.|すでに元に戻された配布履歴です。|
|409104001|Failed to deploy because current stage is deploying.|すでにステージの配布が進行中です。|
|409104002|Failed to deploy because stage is not changed.|すでに最新ステージが配布されています。|
|500104002|Failed to rollback to previous deploy data.|ステージの配布中にエラーが発生しました。復元を試みましたが復元に失敗しました。しばらくしてから再度配布をお試しください。|
|500104003|Could not find any routers for deploying.|ステージの配布リクエストが失敗しました。しばらくしてから再度お試しください。|
|500104004|Failed to convert stage resource list to string.|ステージの配布リクエストが失敗しました。しばらくしてから再度お試しください。|
|500104006|Failed to convert stage deploy JSON to stage resource list.|ステージ配布リクエストが失敗しました。しばらくしてから再度お試しください。|
|500104007|Failed to rollback stage.|ステージ配布リクエストが失敗しました。しばらくしてから再度お試しください。|
|500104008|Temporally failed to request stage deployment. Please try again later.|ステージ配布リクエストが失敗しました。しばらくしてから再度お試しください。|
|400105000|Failed to delete API key. The API key is in use.|関連付けられているAPI Keyは削除できません。関連付けを削除してから削除してください。|
|404105000|Could not find API key.|API Key情報が見つかりません。|
|500105000|Failed to regenerate API key.|API Keyを再発行できませんでした。|
|500105001|Failed to create API key by duplicated API key.|API Keyを作成できませんでした。|
|500105002|Failed to delete some API key data. Please check exception cause.|API Keyの関連付けを削除できませんでした。|
|500105003|Failed to delete API key.|API Keyを削除できませんでした。|
|400106000|Failed to change usage plan of API key. There is no stage connected to the usage plan you want to change or it is the same as the usage plan before the change.|変更しようとしている使用量プランにAPI Keyを関連付けることができるステージがありません。|
|400106001|Failed to delete usage plan. The usage plan has a connected stage.|関連付けられているたステージがあり、使用量プランを削除できませんでした。すべてのステージの関連付けを削除してから削除してください。|
|400106002|The stage has a connected API key. Please try after disconnecting.|ステージに関連付けられているAPI Keyがあります。API Keyの関連付けを削除するとステージを接続解除できます。|
|404106000|Could not find connected API Key.|関連付けられているAPI Keyが見つかりません。|
|409106000|Among the requested API keys, there is an API key already connected to the stage.|接続しようとしているAPI Keyの中にステージに関連付けられているAPI Keyがあります。|
|409106001|The stage is already connected to this usage plan.|すでに使用量プランに関連付けられているステージです。|
|500106000|Failed to connect API key to usage plan stage.|一部のAPI Keyに接続できませんでした。|
|500106001|Failed to disconnect API key from usage plan stage.|一部のAPI Keyの接続を解除できませんでした。|
|500106002|Failed to change usage plan of API key.|API Keyの使用量プランを変更できませんでした。|
|500106003|Failed to delete usage plan.|使用量プランを削除できませんでした。|
|404107000|Resource parameters can only be set on resource methods.|リソースパラメータはメソッドにのみ設定できます。|
|404107001|Resource parameters cannot be set on the OPTIONS method generated by CORS.|CORSにより作成されたメソッドにはリソースパラメータを設定できません。|
|400108001|Failed to delete model. There is referenced model.|使用中の場所があり、モデルの削除に失敗しました。|
|404108000|Could not find model.|モデル情報が見つかりません。|
|409108000|Failed to create model by duplicated name.|すでに存在するモデル名です。モデル名は重複できません。|
|404109000|Could not find API document's swagger.|API説明書が見つかりません。|
|404109001|Could not find stage for making API document.|API説明書の公開状態を変更できませんでした。|
|500109000|Failed to convert with documentable plugin.|API説明書の作成に失敗しました。|
|400110000|Invalid statistics query period.|無効な統計照会期間です。|
|401199000|Failed to authenticate with AppKey.|無効なアプリケーションキーです。|
|500197000|Could not find recordset name.|すでに削除たステージか、ステージ情報が見つかりません。|
