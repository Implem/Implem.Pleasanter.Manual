---
title: 基本設定
category: フォーム
order: '200'
status: ''
parts: ''
urlstring: table-management-form-operation1
translationKey: table-management-form-operation1
shortname: フォーム：基本設定
created: 2025-11-18
updated: 2026-08-12
---

<span style="font-weight:bold;">[≪ フォーム機能の解説](index.md)　|　[より安全に利用するための設定 ≫](table-management-form-operation2.md)</span>

## 1. フォーム機能を有効化する

設定ファイルForm.jsonのパラメータ"Enabled"の値をtrueに設定します。

##### Form.json

```
{
    "Enabled": true
}
```

本設定により、「[テーブルの管理](../index.md)」画面に[フォーム](index.md)タブが追加されます。

## 2. 公開用のテーブルを作成する

「[エディタ](../editor/index.md)」などを使い、公開用のテーブルを作成してください。

##### 公開用テーブルの作成例

![フォームで公開するために作成したテーブルの例](https://pleasanter.org/files/images/ja/managers-guide/manage-table/form/assets/f947c486066c4ea5a673aa70729ffcdb.png)

## 3. テーブルの公開機能を有効化する

1. 公開したいテーブルを開いてください。
2. ナビゲーションメニューの「管理」をクリックしてください。
3. 「[テーブルの管理](../index.md)」をクリックしてください。
   ![ナビゲーションメニューの「管理」から「テーブルの管理」を選ぶところ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/form/assets/2a0179c6f26046b892e710c942462a31.png)
4. [フォーム](index.md)タブをクリックしてください。
5. 「開始日時」に公開を開始する日時をUTC（JSTの9時間前）で設定してください。
6. 「終了日時」に公開を終了する日時をUTC（JSTの9時間前）で設定してください。
7. 「フォームを匿名ユーザに公開する」をクリックして、有効化してください。
8. 「フォームを匿名ユーザに公開する」の下に、公開アドレスが表示されます。
9. コマンドボタンエリアの「更新」ボタンをクリックしてください。
10. Webブラウザを開き、公開アドレスにアクセスしてください。「フォームを匿名ユーザに公開する」を一度オフにし、再度オンにした場合、公開アドレスは更新されるため注意してください。

### 「開始日時」と「終了日時」について

これらの項目を空（未設定）とすることもできます。また、一方のみを設定することもできます。

|開始日時|終了日時|設定結果|
|:--|:--|:--|
|空（未設定）|空（未設定）|期間を定めずに公開|
|特定の日時|空（未設定）|特定の日時以降、期間を定めずに公開|
|特定の日時|過去の日時を設定|一時的に公開停止|

## 4. カスタムメッセージの作成

### 4.1. 利用不可メッセージ

公開期間外の日時にアクセスしたユーザに対して表示するメッセージを作成できます。メッセージの編集には「[リッチテキストエディタ](../../../users-guide/common/richtexteditor.md)」を使えます。

以下は「利用不可メッセージ」の作成例です。

公開時には、次のように表示されます。

![作成した利用不可メッセージが公開ページに表示されたところ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/form/assets/f22667e06a9041eeaa41ca817b55d98c.png)

「利用不可メッセージ」が空の場合、App_Data\Displays内の「FormUnavailableMessageDefault.json」で定義されているメッセージが表示されます。

``` json title="FormUnavailableMessageDefault.json" linenums="1"
{
    "Id": "FormUnavailableMessageDefault",
    "Type": 110,
    "Languages": [
        {
            "Body": "Not available."
        },
        {
            "Language": "ja",
            "Body": "利用できません。"
        }
    ]
}
```

「[リッチテキストエディタ](../../../users-guide/common/richtexteditor.md)」を使用しているため、空に見えてもタグが残っている場合があります。このような場合、利用不可メッセージは空と識別されないため、見た目上何も表示されないページが表示されます。「[リッチテキストエディタ](../../../users-guide/common/richtexteditor.md)」の「ブロック表示」ボタンをクリックして何も表示されなければ、入力欄の内容を完全に削除できています。

![リッチテキストエディタで「ブロック表示」にして中身が空か確かめるところ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/form/assets/6d588430484d48d58bdb53cc722764db.png)

### 4.2. サンクスメッセージ

公開期間中にレコードを作成してくれたユーザに対して表示するメッセージを作成できます。メッセージの編集には「[リッチテキストエディタ](../../../users-guide/common/richtexteditor.md)」を使えます。

公開時には、次のように表示されます。

![作成したサンクスメッセージが公開ページに表示されたところ](https://pleasanter.org/files/images/ja/managers-guide/manage-table/form/assets/3ee9e6200eb445abaecd363a019c2d53.png)

「サンクスメッセージ」が空の場合、App_Data\Displays内の「FormThanksMessageDefault.json」で定義されているメッセージが表示されます。

``` json title="FormThanksMessageDefault.json" linenums="1"
{
    "Id": "FormThanksMessageDefault",
    "Type": 110,
    "Languages": [
        {
            "Body": "Thank you for your input."
        },
        {
            "Language": "ja",
            "Body": "ご入力ありがとうございました。"
        }
    ]
}
```

リッチテキストエディタを使用しているため、空に見えてもタグが残っている場合があります。このような場合、利用不可メッセージは空と識別されないため、見た目上何も表示されないページが表示されますので、注意してください。

<span style="font-weight:bold;">[≪ フォーム機能の解説](index.md)　|　[より安全に利用するための設定 ≫](table-management-form-operation2.md)</span>

## 関連情報

-   [テーブルの管理：フォーム](index.md)
-   [テーブルの管理：フォーム：より安全に利用するための設定](table-management-form-operation2.md)
