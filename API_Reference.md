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
|username|ユーザ名|text|◯|
|email|メールアドレス|text|◯|
|password|パスワード|text||
|image|アイコン画像|text||
|twitter_id|ツイッターID|int||
|twitter_access_token|ツイッターアクセストークン|text||
|twitter_access_token_secret|ツイッターシークレットトークン|text||
|facebook_id|FacebookID|int||
|facebook_access_token|Facebookアクセストークン|text||

### Responce Parameter

|フィールド|説明|型|
|:------------:|:----------|:---|
|code|ステータスコード|int|
|message|メッセージ|text|
|token|トークン|text


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
|username|ログイン用ユーザ名|text|◯（emailといずれか）|
|email|ログイン用メールアドレス|text|◯（usernameといずれか）|
|password|パスワード|text||
|twitter_access_token|Twitterアクセストークン|text||
|facebook_access_token|Facebookアクセストークン|text||

### Responce Parameter

|フィールド|説明|型|
|:------------:|:----------|:---|
|code|ステータスコード|int|
|message|メッセージ|text|
|id|ユーザID|int|
|username|ユーザ名|text|
|email|メールアドレス|text|
|image|アイコン画像|text|
|moriken_auth_id|権限|int|


### Example Request
sample request cord

### Example Responce

```text:Success
{
 "code": 200,
 "message": "リクエストに成功しました。",
 "users": {
	"id": 1,
	"username": "username",
	"email": "example@gmail.com",
	"image": "ImageURL",
	"moriken_auth_id": 1
  } 
}
```

```text:Failed
{
 "code": 400,
 "message": "未入力の項目があるか、入力内容が間違っています。"
}
```
