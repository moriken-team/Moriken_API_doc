# もりけんAPIリファレンス

## 共通仕様
### Responce Format
JSON

### Status Code

|ステータスコード|メッセージ|
|:------------|:---|
|200（OK）|リクエストに成功しました。|
|201（Created）|作成に成功しました。|
|400（BadRequest）|未入力の項目があるか、入力内容が間違っています。|
|401（AuthorizationRequired）|認証が失敗しているか、未認証の状態です。|
|403（Forbidden）|権限がありません。|
|404（NotFound）|リソースが存在しません。|
|409（Conflict）|重複しています。|
|500（InternalServerError）|サーバエラーです。|
|503（ServiceUnavailable）|メンテナンス中か、サーバがダウンしています。|


## ユーザ登録API

### Summary
ユーザの登録APIです。
Twitter, Facebookでの登録も可能です。
Twitter, Facebookからはユーザ名，アイコンを取得します。

### Resource URL
useradd.json

### Resource Information
- Method: POST	
- Contoroller#action: Users#create
- Requires Authentication: No

### Request Parameter

|フィールド|説明|型|必須|
|:------------:|:----------|:---|:----------:|
|username|ユーザ名|Text|◯|
|email|メールアドレス|Text|◯|
|password|パスワード|Text||
|image|アイコン画像|File||
|twitter_id|ツイッターID|Number||
|twitter_access_token|ツイッターアクセストークン|Text||
|twitter_access_token_secret|ツイッターシークレットトークン|Text||
|facebook_id|FacebookID|Number||
|facebook_access_token|Facebookアクセストークン|Text||

### Responce Parameter

|フィールド|説明|型|
|:------------:|:----------|:---|
|code|ステータスコード|Number|
|message|メッセージ|Text|
|token|トークン|Text


### Example Request
sample request cord

### Example Responce

```Text:Success
{
 "code": 200,
 "message": "リクエストに成功しました。",
 "token": "examplehashtoken"
}
```

```text:Failed
{
 "code": 400,
 "message": "未入力の項目があるか、入力内容が間違っています。"
}
```


## ログインAPI
### Summary
ユーザのログインAPIです。
TwitterやFacebookからもログイン可能です．

### Resource URL
login.json

### Resource Information
- Method: POST	
- Contoroller#action: Users#login(?)
- Requires Authentication: No

### Request Parameter

|フィールド|説明|型|必須|
|:------------:|:----------|:---|:----------:|
|username|ログイン用ユーザ名|Text|◯（emailといずれか）|
|email|ログイン用メールアドレス|Text|◯（usernameといずれか）|
|password|パスワード|Text||
|twitter_access_token|Twitterアクセストークン|Text||
|facebook_access_token|Facebookアクセストークン|Text||

### Responce Parameter

|フィールド|説明|型|
|:------------:|:----------|:---|
|code|ステータスコード|Number|
|message|メッセージ|Text|
|id|ユーザID|Number|
|username|ユーザ名|Text|
|email|メールアドレス|Text|
|image|アイコン画像|Text|
|moriken_auth_id|権限|Number|


### Example Request
sample request cord

### Example Responce

```text:Success
{
 "code": 200,
 "message": "リクエストに成功しました。",
 "users":[
  {
	"id": 1,
	"username": "username",
	"email": "example@gmail.com",
	"image": "ImageURL",
	"moriken_auth_id": 1
  } 
]
}
```

```text:Failed
{
 "code": 400,
 "message": "未入力の項目があるか、入力内容が間違っています。"
}
```
