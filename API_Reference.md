# もりけんAPIリファレンス

## 共通仕様
### Responce Format
JSON

### Status Code

|ステータスコード|メッセージ|
|:------------|:---|
|200（OK）|リクエストに成功しました。|
|400（BadRequest）|未入力の項目があるか、入力内容が間違っています。|
|401（AuthorizationRequired）|認証が失敗しているか、未認証の状態です。|
|403（Forbidden）|権限がありません。|
|404（NotFound）|リソースが存在しません。|
|409（Conflict）|重複しています。|
|500（InternalServerError）|サーバエラーです。|
|503（ServiceUnavailable）|メンテナンス中か、サーバがダウンしています。|


## UserAddAPI・・・ユーザ登録API

### Summary
ユーザの登録APIです。

### Resource URL
useradd.json

### Resource Information
- Method: POST	
- Requires Authentication: No

### Request Parameter

|フィールド|説明|型|必須|
|:------------:|:----------|:---|:----------:|
|username|ユーザ名|text|◯|
|email|メールアドレス|text|◯|
|password|パスワード|text|◯|
|image|アイコン画像|file||

### Responce Parameter

|フィールド|説明|型|
|:------------:|:----------|:---|
|code|ステータスコード|Number|
|message|メッセージ|Text|


### Example Request
sample request cord

### Example Responce
sample Responce cord


## LoginAPI・・・ログインAPI
### Summary
ユーザのログインAPIです。

### Resource URL
login.json

### Resource Information
- Method: POST	
- Requires Authentication: No

### Request Parameter

|フィールド|説明|型|必須|
|:------------:|:----------|:---|:----------:|
|username|ログイン用ユーザ名|text|◯（emailといずれか）|
|email|ログイン用メールアドレス|text|◯（usernameといずれか）|
|password|パスワード|text|◯|

### Responce Parameter

|フィールド|説明|型|
|:------------:|:----------|:---|
|code|ステータスコード|Number|
|message|メッセージ|Text|


### Example Request
sample request cord

### Example Responce
sample Responce cord
