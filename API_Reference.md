# もりけんAPIリファレンス

## Common Specification
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

## UserAdd API

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

## Login API
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

## Get Exist Questions API

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
|type|問題形式（1. 四択問題 2. 記述式問題）|int|
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

## Get All Exist Questions API

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

## Making Question API

### Summary
問題を作成するAPIです。

### Resource URL
add.json

### Resource Information
- Method: POST
- Contoroller#action: Problems#add
- Requires Authentication: No

### Request Parameter

|フィールド|説明|型|必須|
|:------------:|:----------|:---|:----------:|
|kentei_id|どの検定の回答履歴か(1:もりけんweb,2:iOSapp,3:Androidapp,4:ガンライザー検定,5:たきざわ検定web,6:たきざわ検定app)|int|◯|
|user_id|問題作成者ID|int|◯|
|type|問題形式（1.四択問題 2.記述式問題）|int|◯|
|grade|過去問採用級|int|過去問作成時は◯|
|number|過去問設問番号|int|過去問作成時は◯|
|sentence|問題文|text|◯|
|right_answer|正解選択肢or正解文字列|text|◯|
|wrong_answer1|誤答選択肢1|text|四択問題時は◯|
|wrong_answer2|誤答選択肢2|text|四択問題時は◯|
|wrong_answer3|誤答選択肢3|text|四択問題時は◯|
|description|解説文|text|◯|
|other_answer|記述式問題の他の正解(カンマ区切り)|text||
|image|画像パス|text||
|latitude|経度・緯度情報|float||
|longitude|経度・緯度情報|float||
|spot_id|ガンライザー検定用スポットID|int||
|public_flag|問題の公開フラグ(非公開=0,公開=1) 過去問は公開,オリジナルは非公開|int|◯|
|category_id|カテゴリid|int|◯|
|subcategory_id|サブカテゴリid|int||

### Responce Parameter

|フィールド|説明|型|
|:------------:|:----------|:---|
|code|APIの処理結果ステータスコード|int|
|message|APIの処理結果メッセージ|text|
|kentei_id|どの検定の回答履歴か(1:もりけんweb,2:iOSapp,3:Androidapp,4:ガンライザー検定,5:たきざわ検定web,6:たきざわ検定app)|int|
|user_id|問題作成者ID|int|
|type|問題形式（1.四択問題 2.記述式問題）|int|
|grade|過去問採用級|int|
|number|過去問設問番号|int|
|sentence|問題文|text|
|right_answer|正解選択肢or正解文字列|text|
|wrong_answer1|誤答選択肢1|text|
|wrong_answer2|誤答選択肢2|text|
|wrong_answer3|誤答選択肢3|text|
|description|解説文|text|
|other_answer|記述式問題の他の正解(カンマ区切り)|text|
|image|画像パス|text|
|latitude|経度・緯度情報|float|
|longitude|経度・緯度情報|float|
|spot_id|ガンライザー検定用スポットID|int|
|public_flag|問題の公開フラグ(非公開=0,公開=1) 過去問は公開,オリジナルは非公開|int|
|category_id|カテゴリid|int|
|subcategory_id|サブカテゴリid|int|

### Example Request（選択形式）
http://sakumon.jp/LK_API/problems/add.json<br />
post_data:kentei_id=1&user_id=1&type=1&grade=1&number=1&sentence=テスト問題文&right_answer=テスト答え&wrong_answer1=テスト誤答&wrong_answer2=テスト誤答2&wrong_answer3=テスト誤答3&description=テスト解答&public_flag&category_id=1&subcategory_id=1

### Example Responce
```
{
    "meta": {
        "method": "POST",
        "url": "/LK_API/problems/add.json"
    },
    "response": {
        "code": 201,
        "message": "作成に成功しました。",
        "Problem": {
            "kentei_id": "1",
            "user_id": "1",
            "type": "1",
            "grade": "1",
            "number": "1",
            "sentence": "テスト問題文",
            "right_answer": "テスト答え",
            "wrong_answer1": "テスト誤答1",
            "wrong_answer2": "テスト誤答2",
            "wrong_answer3": "テスト誤答3",
            "description": "テスト解説",
            "public_flag": "1",
            "category_id": "1",
            "subcategory_id": "1"
        }
    }
}
```

### Example Request（一問一答形式）
http://sakumon.jp/LK_API/problems/add.json<br />
post_data:kentei_id=1&user_id=1&type=2&grade=1&number=1&sentence=テスト問題文&right_answer=テスト一問一答答え&description=テスト解答&public_flag&category_id=1&subcategory_id=1

### Example Responce
```
{
    "meta": {
        "method": "POST",
        "url": "/LK_API/problems/add.json"
    },
    "response": {
        "code": 201,
        "message": "作成に成功しました。",
        "Problem": {
            "kentei_id": "1",
            "user_id": "1",
            "type": "2",
            "grade": "1",
            "number": "1",
            "sentence": "テスト問題文",
            "right_answer": "テスト一問一答答え",
            "description": "テスト解説",
            "public_flag": "1",
            "category_id": "1",
            "subcategory_id": "1"
        }
    }
}
```

### Example Request（error）
・typeを1(4択問題)に設定しwrong_answerを設定しなかった場合
http://sakumon.jp/LK_API/problems/add.json<br />
post_data:kentei_id=1&user_id=1&type=1&grade=1&number=1&sentence=テスト問題文&right_answer=テスト一問一答答え&description=テスト解答&public_flag&category_id=1&subcategory_id=1

### Example Responce
```
{
    "meta": {
        "method": "POST",
        "url": "/LK_API/problems/add.json"
    },
    "error": {
        "code": "400",
            "message": "Validation Error",
            "validation": {
                "Problem": {
                    "wrong_answer1": "wrong_answer1を設定してください",
                    "wrong_answer2": "wrong_answer2を設定してください",
                    "wrong_answer3": "wrong_answer3を設定してください"
                }
            }
    }
}
```

## Add Answer History API

### Summary
問題解答結果を記録(answer_historisへの記録)をするAPI

### Resource URL
add.json

### Resource Information
- Method: POST
- Contoroller#action : AnswerHistories#add

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


### Example Request(success)
http://moriken_test.com/LK_API/answerHistories/add.json<br />
post_data:kentei_id=1&user_id=10&problem_id=5&answer_flag=1

### Example Responce
```
{
    "meta": {
        "method": "POST",
        "url": "/LK_API/answerHistories/add.json"
    },
    "response": {
        "code": 201,
        "message": "作成に成功しました。",
        "AnswerHistory": {
            "answer_flag": "1",
            "kentei_id": "1",
            "problem_id": "5",
            "user_id": "10"
        }
    }
}
```

### Example Request(error)
http://moriken_test.com/LK_API/answerHistories/add.json<br />
post_data:user_id=10&problem_id=5&answer_flag=1

```
{
    "meta": {
        "method": "POST",
        "url": "/LK_API/answerHistories/add.json"
    },
    "error": {
        "code": "400",
        "message": "Validation Error",
        "validation": {
            "AnswerHistory": {
                "kentei_id": "kentei_idを設定してください"
            }
        }
    }
}
```

## Index Answer History API

### Summary
問題解答結果を取得するAPI<br />
検定,ユーザー,正解フラグを抽出条件として実行する

### Resource URL
index.json

### Resource Information
- Method: GET
- Contoroller#action : AnswerHistories#index

|フィールド|説明|型|必須|
|:------------:|:----------|:---|:----------:|
|kentei_id|どの検定の回答履歴か(1:もりけんweb,2:iOSapp,3:Androidapp,4:ガンライザー検定,5:たきざわ検定web,6:たきざわ検定app)|int|◯|
|user_id|取得したい履歴のユーザーID|int|◯|
|answer_flag|正解フラグ(1:正解,2:不正解)|int||


### Responce Parameter

|フィールド|説明|型|
|:------------:|:----------|:---|
|code|APIの処理結果ステータスコード|int|
|message|APIの処理結果メッセージ|text|
|kentei_id|どの検定の回答履歴か(1:もりけんweb,2:iOSapp,3:Androidapp,4:ガンライザー検定,5:たきざわ検定web,6:たきざわ検定app)|int|
|user_id|指定した履歴のユーザーID|int|
|problem_id|回答した問題のID|int|
|answer_flag|正解したか(1:正解,2:不正解)|int|
|answer_text|不正解の場合の誤回答テキスト|text|
|created|履歴登録日|datetime|


### Example Request(success)
http://sakumon.jp/LK_API/answerHistories/index.json<br />
post_data:kentei_id=1&user_id=10

### Example Responce
```
{
    "meta": {
        "method": "GET",
        "url": "/LK_API/answerHistories/index.json"
    },
    "response": {
        "code": 200,
        "message": "リクエストに成功しました。",
        "0": {
            "AnswerHistory": {
                "id": "134979",
                "kentei_id": "1",
                "user_id": "10",
                "problem_id": "5",
                "answer_flag": "1",
                "answer_text": null,
                "created": "2015-02-07 21:56:57"
            }
        },
        "1": {
            "AnswerHistory": {
                "id": "134980",
                "kentei_id": "1",
                "user_id": "10",
                "problem_id": "5",
                "answer_flag": "1",
                "answer_text": null,
                "created": "2015-02-07 21:57:20"
            }
        },
        ・
        ・
        ・
    }
}
```

### Example Request(error)
http://sakumon.jp/LK_API/answerHistories/index.json<br />
post_data:kentei_id=1

```
{
    "meta": {
        "method": "GET",
        "url": "/LK_API/answerHistories/index.json"
    },
    "error": {
        "code": "400",
        "message": "Validation Error",
        "validation": {
            "AnswerHistory": {
                "user_id": "user_idを設定してください"
            }
        }
    }
}
```
