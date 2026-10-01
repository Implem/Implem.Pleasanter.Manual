---
title: view.SearchTypes
icon: material/alpha-p-box
category: サーバスクリプト
order: '4000'
status: ''
parts: ''
urlstring: server-script-view-search-types
translationKey: server-script-view-search-types
shortname: view.SearchTypes
created: 2022-09-09
updated: 2023-11-15
---

## 概要

[view](index.md)オブジェクトの「SearchTypes」です。[サーバスクリプト](../index.md)で部分一致や完全一致など項目の検索方法を指定する際に使用します。

## 使用方法

SearchTypesに指定できる値は以下のとおりです。分類項目の形式によって指定するSearchTypesが異なりますので、詳細は下記の「分類項目の形式ごとの指定について」を参照してください。

|No|SearchTypes|説明|
|:----|:----|:----|
|1|PartialMatch|部分一致でフィルタします。|
|2|ExactMatch|完全一致でフィルタします。|
|3|ForwardMatch|前方一致でフィルタします。|
|4|PartialMatchMultiple|配列指定の場合、部分一致でフィルタします。|
|5|ExactMatchMultiple|配列指定の場合、完全一致でフィルタします。|
|6|ForwardMatchMultiple|配列指定の場合、前方一致でフィルタします。|

### 分類項目の形式ごとの指定について

下表は分類項目の形式ごとに、指定すべきSearchTypesを表しています。フリーテキストは、自由入力欄として分類項目を使用しているケースを指します。選択肢一覧は、選択肢一覧に選択肢を入力して設定しているケースを指します。リンク設定は、リンクしたテーブルからデータを読み込んで選択肢としているケースを指します。意図通り検索できるものは「◯」となります。

|SearchTypes|フリーテキスト|選択肢一覧|リンク設定|
|:----|:----:|:----:|:----:|  
|PartialMatch|〇|×|×|
|ExactMatch|〇|×|×|
|ForwardMatch|〇|×|×|
|PartialMatchMultiple|〇|〇|×|
|ExactMatchMultiple|〇|〇|〇|
|ForwardMatchMultiple|〇|〇|×|

分類項目がフリーテキストの場合、`MatchMultiple`フィルタは配列指定した場合のみ正常に表示されます。

## サンプルデータ

以下の使用例では下記のテーブル、レコード情報をもとに記述しております。

??? note "社員テーブル（クリックすると詳細が表示されます）"

    |レコードID|社員名(タイトル)|最寄り駅(分類A)|所属|連絡先|
    |:--:|:--:|:--:|:--:|:--:|
    |10|阿部一馬|新中野|総務部|123-123-123|
    |11|安藤桜|北千住|総務部|111-111-111|
    |12|加藤美緒|町田|総務部|456-456-456|
    |13|斎藤和正|目黒|経理部|789-789-789|
    |14|佐藤優樹|新宿|営業部|999-999-999|
    |15|三浦裕子|葛西|経理部|333-333-333|
    |16|山崎史郎|高田馬場|営業部|555-555-555|
    |17|山田太郎|中野|営業部|258-258-258|

### 使用例①

以下の例では、分類Aの形式がフリーテキストで、値が「中野」を含む文字列のレコードを表示します。

##### JavaScript

``` javascript linenums="1"
view.Filters.ClassA = '中野';
view.SearchTypes.ClassA = 'PartialMatch';
```

##### フィルタ結果

??? note "社員テーブル（クリックすると詳細が表示されます）"

    |レコードID|社員名(タイトル)|最寄り駅(分類A)|所属|連絡先|
    |:--:|:--:|:--:|:--:|:--:|
    |10|阿部一馬|新中野|総務部|123-123-123|
    |17|山田太郎|中野|営業部|258-258-258|

### 使用例②

以下の例では、分類Aの形式がフリーテキストで、値が「中野」または「目黒」を含む文字列のレコードを表示します。

##### JavaScript

``` javascript linenums="1"
view.Filters.ClassA = '["中野","目黒"]';
view.SearchTypes.ClassA = 'PartialMatchMultiple';
```

##### フィルタ結果

??? note "社員テーブル（クリックすると詳細が表示されます）"

    |レコードID|社員名(タイトル)|最寄り駅(分類A)|所属|連絡先|
    |:--:|:--:|:--:|:--:|:--:|
    |10|阿部一馬|新中野|総務部|123-123-123|
    |13|斎藤和正|目黒|経理部|789-789-789|
    |17|山田太郎|中野|営業部|258-258-258|

### 使用例③

以下の例では、分類Aの[選択肢一覧](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/index.md)にリストを設定しており、「中野」の文字列が含まれる選択肢を設定しているレコードを表示します。

##### JavaScript

``` javascript linenums="1"
view.Filters.ClassA = '["中野"]';
view.SearchTypes.ClassA = 'PartialMatchMultiple';
```

##### フィルタ結果

??? note "社員テーブル（クリックすると詳細が表示されます）"

    |レコードID|社員名(タイトル)|最寄り駅(分類A)|所属|連絡先|
    |:--:|:--:|:--:|:--:|:--:|
    |10|阿部一馬|新中野|総務部|123-123-123|
    |17|山田太郎|中野|営業部|258-258-258|

### 使用例④

以下の例では、分類Aが下記「社員テーブル」への[リンク](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-link.md)が設定されており、「中野」もしくは「目黒」のレコードを表示します。  

|親テーブル|子テーブル|
|:--:|:--:|
|社員テーブル|最寄り駅テーブル|

##### 子テーブル

??? note "駅テーブル（クリックすると詳細が表示されます）"

    |レコードID|社員名(タイトル)|最寄り駅(分類A)|交通費|電車通勤の有無|
    |:--:|:--:|:--:|:--:|:--:|
    |20|阿部一馬|新中野|￥680|〇|
    |21|安藤桜|北千住|￥890|〇|
    |22|加藤美緒|町田|￥720|〇|
    |23|斎藤和正|目黒|￥680|〇|
    |24|佐藤優樹|新宿|￥580|〇|
    |25|三浦裕子|葛西|￥0|×|
    |26|山崎史郎|高田馬場|￥0|×|
    |27|山田太郎|中野|￥0|×|

下記のサンプルコードは「最寄り駅テーブル(子)」に設定します。  
フィルタの設定値には「社員テーブル(親)」の対象レコードのID(配列形式)を指定します。
ここでは、13(目黒)と17(中野)を指定しております。
また、リンクしたレコードIDでのフィルタは完全一致するレコードのみ表示される仕様となっております。

##### JavaScript 

``` javascript linenums="1"
let list = ["13","17"]
view.SearchTypes.ClassA = 'ExactMatchMultiple';
view.Filters.ClassA = JSON.stringify(list);
```

##### フィルタ結果

??? note "駅テーブル（クリックすると詳細が表示されます）"

    |レコードID|社員名(タイトル)|最寄り駅(分類A)|交通費|電車通勤の有無|
    |:--:|:--:|:--:|:--:|:--:|
    |20|阿部一馬|新中野|￥680|〇|
    |23|斎藤和正|目黒|￥680|〇|
    |27|山田太郎|中野|￥0|×|

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [選択肢一覧](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/index.md)
-   [リンク](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-link.md)
