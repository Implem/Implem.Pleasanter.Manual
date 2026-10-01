---
title: 親<-子<-孫とテーブルをリンク設定しているとき、孫テーブルのサマリ結果が親テーブルに反映されない
category: FAQ：編集画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-multi-stage-summary
translationKey: faq-multi-stage-summary
shortname: ''
created: 2019-03-27
updated: 2024-04-29
---

## 回答

[スクリプト](../../managers-guide/manage-table/scripts/index.md)または[サーバスクリプト](../../developers-guide/server-script/index.md)を使用してください。

---

## 概要

親<-子<-孫といったテーブルのリンク設定をしているとき、子・孫テーブルでそれぞれサマリ設定を行っている場合、 孫テーブルでレコードを更新すると子テーブルにサマリ結果が反映されますが、親テーブルには反映されません。  
例）  

||親テーブル|子テーブル|孫テーブル|
|:-:|:-:|:-:|:-:|
|サマリ設定|設定なし|親テーブルの数値Aにサマリ結果を反映|子テーブルの数値Aにサマリ結果を反映|
|操作|自動更新されない|自動更新|★手動で更新|
|数値項目|数値A[0]|数値A[10]|数値A[10]|

サマリ機能は、1階層上のレコードに自レコードのデータを集計することができますが、孫->子->親のように複数階層を同時に処理することができません。親テーブルまでサマリ結果を反映させるには、孫テーブルの更新後処理として、子テーブルを更新するスクリプトまたはサーバスクリプトを設定する必要があります。子テーブルが更新されると、子テーブルのサマリ設定により親テーブルを更新することができます。  

例として「分類A」が子テーブルとのリンク項目となっている場合に孫テーブルを更新すると子テーブルも自動更新するサンプルコードを以下に記載します。

### 例1.スクリプト

孫テーブルに以下のスクリプトを設定します。出力先は「新規」、「編集」にチェックしてください。

##### JavaScript

```
// レコード作成処理後、画面反映前
$p.events.before_set_Create = function () {
    var recordId = $p.getControl('ClassA').val();
    $p.ex.Update(recordId);
};

// レコード更新処理後、画面反映前
$p.events.before_set_Update = function () {
    var recordId = $p.getControl('ClassA').val();
    $p.ex.Update(recordId);
};

// レコード削除処理後、画面反映前
$p.events.before_set_Delete = function () {
    var recordId = $p.getControl('ClassA');
    $p.ex.Update(recordId);
};

// 親レコードの更新を実行するメソッド（データは変更しない）
$p.ex.Update = function(recordId){
    $p.apiUpdate({
        'id': recordId,
        'data': {}
    });
};
```

### 例2.サーバスクリプト

孫テーブルに以下のサーバスクリプトを設定します。条件は「作成後」、「更新後」、「削除後」にチェックしてください。

##### JavaScript

```
const records = items.Get(model.ClassA);
if (records.Length === 1) {
    let record = records[0];
    record.Update();
}
```

