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
User.json

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
|code|ステータスコード|int|
|message|メッセージ|text|
|token|トークン|text

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
Users.json

### Resource Information
- Method: POST	
- Contoroller#action: Users#login
- Requires Authentication: No

### Request Parameter

|フィールド|説明|型|必須|
|:------------:|:----------|:---|:----------:|	
|username|ログイン用ユーザ名|text|◯（emailといずれか）|
|email|ログイン用メールアドレス|text|◯（usernameといずれか）|
|password|パスワード|text||
|twitter_access_token|Twitterアクセストークン|text||
|facebook_access_token|Facebookアクセストークン|text||
|code|ステータスコード|int|
|message|メッセージ|text|
|id|ユーザID|int|
|username|ユーザ名|text|
|email|メールアドレス|text|
|image|アイコン画像|text|
|moriken_auth_id|権限|int|

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

## 過去問題取得API（1問 or 5問）

### Summary
- 過去問題を取得するAPIです。
- 5問取得はランダムに取得します。

### Resource URL
Problem.json

### Resource Information
- Method: GET
- Contoroller#action: Problems#show
- Requires Authentication: No

### Request Parameter

|フィールド|説明|型|必須|
|:------------:|:----------|:---|:----------:|
|user_id|ユーザID|int|◯|
|employ|年度|int|◯|
|grade|級|int|◯|
|item|問題取得数|int|◯|

### Responce Parameter

|フィールド|説明|型|
|:------------:|:----------|:---|
|problem_id|問題ID|int|
|employ|過去問題採用年度|int|
|grade|過去問題採用級|int|
|number|過去問題設問番号|int|
|type|問題形式（1. 四択問題　2. 記述式問題）|int|
|category_name|カテゴリ名|text|
|subcategory_name|サブカテゴリ名|txet|
|sentence|問題文|text|
|right_answer|正解選択肢or正解文字列|text|
|wrong_answer1|誤答選択肢1|text|
|wrong_answer2|誤答選択肢2|text|
|wrong_answer3|誤答選択肢3|text|
|description|解説文|text|

### Example Requesc（1問取得）
http://...show.json?user_id=1&employ=2012&grade=3&item=1

###Example Request（5問取得）
http://...randomshow.json?user_id=1&employ=2012&grade=3&item=2

### Example Responce（1問取得）
```
{
	code: 200,
	message: "リクエストに成功しました。",
	"problem": {
		"problem_id": "1",
		"employ": "2012",
		"grade": "3",
		"number": "",
		"type": "",
		"category_name": "",
		"subcategory_name": "",
		"sentence": "",
		"right_answer": "",
		"wrong_answer1": "",
		"wrong_answer2": "",
		"wrong_answer3": "",
		"description": ""
	}
}
```

### Example Responce（5問取得）
```
{
	code: 200,
	message: "リクエストに成功しました。",
	"problem": [
		{
			"problem_id": "1",
			"employ": "2012",
			"grade": "3",
			"number": "",
			"type": "",
			"category_name": "",
			"subcategory_name": "",
			"sentence": "",
			"right_answer": "",
			"wrong_answer1": "",
			"wrong_answer2": "",
			"wrong_answer3": "",
			"description": ""
		},
		{
			"problem_id": "2",
			"employ": "2012",
			"grade": "3",
			"number": "",
			"type": "",
			"category_name": "",
			"subcategory_name": "",
			"sentence": "",
			"right_answer": "",
			"wrong_answer1": "",
			"wrong_answer2": "",
			"wrong_answer3": "",
			"description": ""
		},
		{
			"problem_id": "3",
			"employ": "2012",
			"grade": "3",
			"number": "",
			"type": "",
			"category_name": "",
			"subcategory_name": "",
			"sentence": "",
			"right_answer": "",
			"wrong_answer1": "",
			"wrong_answer2": "",
			"wrong_answer3": "",
			"description": ""
		},
		{
			"problem_id": "4",
			"employ": "2012",
			"grade": "3",
			"number": "",
			"type": "",
			"category_name": "",
			"subcategory_name": "",
			"sentence": "",
			"right_answer": "",
			"wrong_answer1": "",
			"wrong_answer2": "",
			"wrong_answer3": "",
			"description": ""
		},
		{
			"problem_id": "5",
			"employ": "2012",
			"grade": "3",
			"number": "",
			"type": "",
			"category_name": "",
			"subcategory_name": "",
			"sentence": "",
			"right_answer": "",
			"wrong_answer1": "",
			"wrong_answer2": "",
			"wrong_answer3": "",
			"description": ""
		}
	]
}
```

###Example Responce（リクエスト失敗時）
```
{
    "code" : 401,
    "message" : "認証が失敗しているか、未認証の状態です。"
}
```

## 過去問題取得API（全部）

### Summary
過去問題を取得するAPIです。

### Resource URL
Problem.json

### Resource Information
- Method: GET
- Contoroller#action: Problems#index
- Requires Authentication: No

### Request Parameter

|フィールド|説明|型|必須|
|:------------:|:----------|:---|:----------:|
|user_id|ユーザID|int|◯|
|employ|年度|int|◯|
|grade|級|int|◯|

### Responce Parameter

|フィールド|説明|型|
|:------------:|:----------|:---|
|problem_id|問題ID|int|
|employ|過去問題採用年度|int|
|grade|過去問題採用級|int|
|number|過去問題設問番号|int|
|type|問題形式（1. 四択問題　2. 記述式問題）|int|
|category_name|カテゴリ名|text|
|subcategory_name|サブカテゴリ名|txet|
|sentence|問題文|text|
|right_answer|正解選択肢or正解文字列|text|
|wrong_answer1|誤答選択肢1|text|
|wrong_answer2|誤答選択肢2|text|
|wrong_answer3|誤答選択肢3|text|
|description|解説文|text|

###Example Request
http://...index.json?problem_id=1&employ=2012&grade=3

### Example Responce
```
{
	code: 200,
	message: "リクエストに成功しました。",
	"problem": [
		{
			"problem_id": "1",
			"employ": "2012",
			"grade": "3",
			"number": "1",
			"type": "",
			"category_name": "",
			"subcategory_name": "",
			"sentence": "",
			"right_answer": "",
			"wrong_answer1": "",
			"wrong_answer2": "",
			"wrong_answer3": "",
			"description": ""
		},
					.
					.
					.
		{
			"problem_id": "100",
			"employ": "2012",
			"grade": "3",
			"number": "100",
			"type": "",
			"category_name": "",
			"subcategory_name": "",
			"sentence": "",
			"right_answer": "",
			"wrong_answer1": "",
			"wrong_answer2": "",
			"wrong_answer3": "",
			"description": ""
		}
	]
}
```

###Example Responce（リクエスト失敗時）
```
{
    "code" : 401,
    "message" : "認証が失敗しているか、未認証の状態です。"
}
```

## 問題作成API

### Summary
問題を作成するAPIです。

### Resource URL
Probrem.json

### Resource Information
- Method: POST
- Contoroller#action: Problem#creatquiz
- Requires Authentication: No

### Request Parameter

|フィールド|説明|型|必須|
|:------------:|:----------|:---|:----------:|
|user_id|ユーザID（facebook, twitter）|int|◯|
|sentence|問題文|text|◯|
|right_answer|正解選択肢or正解文字列|text|◯|
|wrong_answer1|誤答選択肢1|text||
|wrong_answer2|誤答選択肢2|text||
|wrong_answer3|誤答選択肢3|text||
|description|解説文|text|◯|
|category_id|カテゴリid|int|◯|
|subcategory_id|サブカテゴリid|int|◯|
|type|問題形式（1.四択問題　2.記述式問題）|int|◯|

### Responce Parameter

|フィールド|説明|型|
|:------------:|:----------|:---|
|code|APIの処理結果ステータスコード|text|
|message|APIの処理結果メッセージ|text|

### Example Request（選択形式）
http://...create_quiz.json?user_id=1&sentence=texttexttext&right_answer=test1&wrong_answer1=test2&wrong_answer2=test3&wrong_answer3=test4&description=texttexttext&category_id=2&subcategory_id=3&type=1

### Example Request（一問一答形式）
http://...create_quiz.json?user_id=1&sentence=texttexttext&right_answer=test&description=texttexttext&category_id=3&subcategory_id=4&type=2


### Example Responce（登録成功時）
```
{
	"code" : 201,
	"message" : "作成に成功しました。"
}
```

### Example Responce（登録失敗時）
```
{"
	"code" : 400,
	"message" : "未入力の項目があるか、入力内容が間違っています。"
}
```

### Example Responce（リクエスト失敗時）
```
{
	"code" : 401,
	"message" : "認証が失敗しているか、未認証の状態です。"
}
```

## 問題回答結果記録API

### Summary
問題解答結果を記録(answer_historisへの記録)をするAPI

### Resource URL
problems.json

### Resource Information
- Method: POST
- Contoroller#action : Problem#create

|フィールド|説明|型|必須|
|:------------:|:----------|:---|:----------:|
|kentei_id|どの検定の回答履歴か(1:もりけんweb,2:iOSapp,3:Androidapp,4:ガンライザー検定,5:たきざわ検定web,6:たきざわ検定app)|int|◯|
|user_id|回答したユーザーのID|int|◯|
|problem_id|回答した問題のID|int|◯|
|answer_flag|正解したか(1:正解,2:不正解)|int|◯|
|answer_text|不正解の場合の誤回答テキスト|text||


### Responce Parameter

|フィールド|説明|型|
|:------------:|:----------|:---|
|code|APIの処理結果ステータスコード|int|
|message|APIの処理結果メッセージ|int|
|kentei_id|どの検定の回答履歴か(1:もりけんweb,2:iOSapp,3:Androidapp,4:ガンライザー検定,5:たきざわ検定web,6:たきざわ検定app)|int|
|user_id|回答したユーザーのID|int|
|problem_id|回答した問題のID|int|
|answer_flag|正解したか(1:正解,2:不正解)|int|
|answer_text|不正解の場合の誤回答テキスト|text||


### Example Request
http://~/problems.json
post_data:kentei_id=1&user_id=10&problem_id=5&answer_flag=1

### Example Responce
```
{
    "code" : 201,
    "message" : "作成に成功しました",
    "kentei_id" : 1,
    "user_id" : 10,
    "problem_id" : 5,
    "answer_flag" : 1,
    "answer_text" : Null
}
```
