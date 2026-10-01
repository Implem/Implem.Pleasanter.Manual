---
title: 選択肢一覧に特定のユーザのみ表示したい
category: FAQ：編集画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-user-choices
translationKey: faq-user-choices
shortname: ''
created: 2020-07-21
updated: 2024-11-25
---

## 回答

選択肢一覧の[フィルタ](../../users-guide/hands-on/advanced/advanced-operations-link.md)と「View」の「ColumnFilterSearchTypes」を組み合わせて使用します。

---

## 概要

指定した文字列から始まるユーザや指定した文字列を含むユーザを選択肢に表示する場合には、選択肢一覧の[フィルタ](../../users-guide/hands-on/advanced/advanced-operations-link.md)機能を使用します。

### ユーザ（絞り込みなし）

![絞り込みをしていない状態のユーザの選択肢一覧](https://pleasanter.org/files/images/ja/FAQ/editor/assets/d74c7b37bad84e8ead21ba6499547d1d.png)

### 例1. 氏名が「山」から始まるユーザ

選択肢一覧の[フィルタ](../../users-guide/hands-on/advanced/advanced-operations-link.md)機能で選択肢を絞り込みます。その際に「View」の「ColumnFilterSearchTypes」に"ForwardMatch（前方一致）"を指定するとColumnFilterHashで指定したName（名前）が"山"で始まるユーザが表示対象となります。

``` json linenums="1"
[
    {
        "TableName": "Users",
        "View": {
            "ColumnFilterHash": {
                "Name": "山"
            },
            "ColumnFilterSearchTypes":{
                "Name":  "ForwardMatch"
            }
        }
    }
]
```

### 表示結果

![氏名が「山」から始まるユーザだけに絞り込まれた選択肢](https://pleasanter.org/files/images/ja/FAQ/editor/assets/f461f1b4ca084213babf4fe330fe7df3.png)

### 例2. 氏名に「一」が含まれるユーザ

例1と同様に選択肢一覧の[フィルタ](../../users-guide/hands-on/advanced/advanced-operations-link.md)機能で選択肢を絞り込みます。この例では「View」の「ColumnFilterSearchTypes」に"PartialMatch（部分一致）"を指定したため、ColumnFilterHashで指定したName（名前）に"一"が含まれるユーザが表示対象となります。

``` json linenums="1"
[
    {
        "TableName": "Users",
        "View": {
            "ColumnFilterHash": {
                "Name": "一"
            },
            "ColumnFilterSearchTypes":{
                "Name":  "PartialMatch"
            }
        }
    }
]
```

### 表示結果

![氏名に「一」が含まれるユーザだけに絞り込まれた選択肢](https://pleasanter.org/files/images/ja/FAQ/editor/assets/268abe63736c4048ae7ccd3b319777bc.png)

## 関連情報

-   [応用編：リンク](../../users-guide/hands-on/advanced/advanced-operations-link.md)
