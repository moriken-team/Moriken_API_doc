# もりけんAPIリファレンス
もりけんのAPIリファレンスです。
全てのAPIのResponce FormatがJSONになります。

## UserAddAPI・・・ユーザ登録API

### Summary
問題解答結果を記録(answer_historisへの記録)をするAPI

### Resource URL
create.json

### Resource Information
- Method: POST  
- Requires Authentication: No

### Request Parameter

|フィールド|説明|型|必須|
|:------------:|:----------|:---|:----------:|
|kentei_id|どの検定の回答履歴か(1:もりけんweb,2:iOSapp,3:Androidapp,4:ガンライザー検定,5:たきざわ検定web,6:たきざわ検定app)|intger|◯|
|user_id|回答したユーザーのID|integer|◯|
|problem_id|回答した問題のID|integer|◯|
|answer_flag|正解したか(1:正解,2:不正解)|integer|◯|

### Responce Parameter

|フィールド|説明|型|必須|
|:------------:|:----------|:---|:----------:|
|status|APIの処理結果(成功:201,失敗:500)|integer|◯|
|kentei_id|どの検定の回答履歴か(1:もりけんweb,2:iOSapp,3:Androidapp,4:ガンライザー検定,5:たきざわ検定web,6:たきざわ検定app)|intger|◯|
|user_id|回答したユーザーのID|integer|◯|
|problem_id|回答した問題のID|integer|◯|
|answer_flag|正解したか(1:正解,2:不正解)|integer|◯|


### Example Request
http://~/create.json
post_data:kentei_id=1&user_id=10&problem_id=5&answer_flag=1

### Example Responce
{
    "response" : {
        "status" : 201
        "kentei_id" : 1
        "user_id" : 10
        "problem_id" : 5
        "answer_flag" : 1
    }
}
