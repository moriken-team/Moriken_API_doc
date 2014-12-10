# もりけんAPIリファレンス

## GetQuizAPI・・・過去問題取得API

### Summary
過去問題を取得するAPIです。

### Resource URL
getquiz.json

## Resource Information
- Method: GET
- Requires Authentication: No

### Request Parameter

|フィールド|説明|型|必須|
|:------------:|:----------|:---|:----------:|
|user_id|ユーザID（facebook, twitter）|int|◯|
|employ|年度|int||
|grade|級|int||
|category_id|カテゴリID|int||

### Responce Parameter

|フィールド|説明|型|
|:------------:|:----------|:---|
|employ|過去問題採用年度|int|
|grade|過去問題採用級|int|
|number|過去問題設問番号|int|
|type|問題形式（1.四択問題　2.記述式問題）|int|
|category_name|カテゴリ名|text|
|subcategory_name|サブカテゴリ名|txet|
|sentence|問題文|text|
|right_answer|正解選択肢or正解文字列|text|
|wrong_answer1|誤答選択肢1|text|
|wrong_answer2|誤答選択肢2|text|
|wrong_answer3|誤答選択肢3|text|
|description|解説文|text|

### Example Request

http://...getquiz.json?user_id=1&employ=2012&grade=3&category_id=2

### Example Responce

{

"response": {

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



## CreateQuizAPI・・・問題作成API

### Summary
問題を作成するAPIです。

### Resource URL
createquiz.json

### Resource Information
- Method: POST
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
|saved|問題作成に成功|text|
|error|問題作成に失敗|text|
|data is empty|データが送られてきていない|text|

### Example Request（選択形式）

http://...create_quiz.json?user_id=1&sentence=texttexttext&right_answer=test1&wrong_answer1=test2&wrong_answer2=test3&wrong_answer3=test4&description=texttexttext&category_id=2&subcategory_id=3&type=1

### Example Request（一問一答形式）

http://...create_quiz.json?user_id=1&sentence=texttexttext&right_answer=test&description=texttexttext&category_id=3&subcategory_id=4&type=2


### Example Responce（登録成功時）

{"response": "seved"}

### Example Responce（登録失敗時）

{"response": "error"}

### Example Responce（リクエスト失敗時）

{"response": "data is empty"}

