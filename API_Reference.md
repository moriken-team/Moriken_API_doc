# もりけんAPIリファレンス
もりけんのAPIリファレンスです。
全てのAPIのResponce FormatがJSONになります。

## 問題回答結果記録API

### Summary
問題解答結果を記録(answer_historisへの記録)をするAPI

### Resource URL
create.json

### Resource Information
- Method: POST  
- Contoroller#action : Problem#create
- Requires Authentication: No

### Request Parameter

|フィールド|説明|型|必須|
|:------------:|:----------|:---|:----------:|
|kentei_id|どの検定の回答履歴か(1:もりけんweb,2:iOSapp,3:Androidapp,4:ガンライザー検定,5:たきざわ検定web,6:たきざわ検定app)|int|◯|
|user_id|回答したユーザーのID|int|◯|
|problem_id|回答した問題のID|int|◯|
|answer_flag|正解したか(1:正解,2:不正解)|int|◯|

### Responce Parameter

|フィールド|説明|型|必須|
|:------------:|:----------|:---|:----------:|
|code|APIの処理結果ステータスコード|int|◯|
|message|APIの処理結果メッセージ|int|◯|
|kentei_id|どの検定の回答履歴か(1:もりけんweb,2:iOSapp,3:Androidapp,4:ガンライザー検定,5:たきざわ検定web,6:たきざわ検定app)|int|◯|
|user_id|回答したユーザーのID|int|◯|
|problem_id|回答した問題のID|int|◯|
|answer_flag|正解したか(1:正解,2:不正解)|int|◯|


### Example Request
http://~/create.json
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
}
```
