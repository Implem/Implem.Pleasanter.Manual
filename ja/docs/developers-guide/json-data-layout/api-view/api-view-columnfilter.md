---
title: ColumnFilterの指定方法
category: JSONデータレイアウト
order: '10000'
status: ''
parts: ''
urlstring: api-view-columnfilter
translationKey: api-view-columnfilter
shortname: ''
created: 2025-07-14
updated: 2026-10-01
---

## 概要

[API](../../api/basics/api.md)や「[サーバスクリプト](../../server-script/index.md)」でレコードを操作する際、JSON形式フォーマットで「フィルタ」を指定します。

## ColumnFilterHashの指定方法

- ColumnFilterHashは、カラムの値を指定して絞り込み検索します。
- ColumnFilterHashの値は、選択肢有りの分類、数値、日付は、配列で複数指定可能です。
- 複数の値を指定した場合は、OR検索となります。
- 日付および数値の場合、カンマ区切りの文字列で範囲の指定が可能です。  
- 複数の検索条件を指定した場合は、AND検索となります。  

### 分類Aが "みかん" or "ブドウ"

```JSON
"ClassA":"[\"みかん\",\"ブドウ\"]"
```

### 数値Aが 10 or 20 or 30

```JSON
"NumA":[10,20,30]
```

### 数値Aが 5〜10 or 15

```JSON
"NumA":"[\"5,10\",15]"
```

### 数値Aが 100以下

```JSON
"NumA":"[\",100\"]"
```

### 日付Aが 2021/1/31(終日)

```JSON
"DateA":"[\"2021/01/31 00:00:00,2021/01/31 23:59:59\"]"

```

### 日付Aが 2021/1/1以降

```JSON
"DateA":"[\"2021/01/01 00:00:00,\"]"
```

### 分類と数値が混在

分類Aが "りんご" or "バナナ"、かつ 数値Aが 10 or 20 or 30

```JSON
"ColumnFilterHash":{
    "ClassA":"[\"りんご\",\"バナナ\"]",
    "NumA":[10,20,30]
}
```

### 数値・日付が混在

数値Aが300〜900 or 200、かつ 日付Aが2021/1/1〜2021/1/31、かつ 数値Bが100以下、かつ 日付Bが2021/3/1以降

```JSON
"ColumnFilterHash":{
    "NumA":["300,990",200],
    "DateA":"[\"2021/01/01 00:00:00,2021/01/31 23:59:59\"]",
    "NumB":[",100"],
    "DateB":"[\"2021/03/01 00:00:00,\"]"
}
```

### 未設定を設定する場合

ドロップダウンリストの(未設定)のレコードをフィルタリングする場合は、タブ文字を指定します。

```JSON
"ColumnFilterHash":{
    "ClassA":"[\"\t\"]"
}
```

### 未入力を絞り込む場合

分類や説明項目で未入力のレコードをフィルタリングする場合は、半角スペースを指定します。

```JSON
"ColumnFilterHash":{
    "ClassA":" "
}
```

### 日付項目で未入力を絞り込む場合

日付項目で未入力のレコードをフィルタリングする場合は、タブ文字を指定します。

```JSON
"ColumnFilterHash":{
    "DateA":"[\"\t\"]"
}
```

### ログインユーザ自身でレコードを絞り込む場合

「[選択肢一覧](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/index.md)」にUsersまたはDeptsを指定している項目で、ログインユーザまたは所属している組織で絞り込む場合は、Ownを指定します。

```JSON
"ColumnFilterHash": {
    "ClassA": "[\"Own\"]"
}
```

### OR条件,AND条件を設定する場合

ColumnFilterHashに or_ または and_ で始まる任意名のプロパティを追加し、検索条件のJSONを文字列化した値を設定することで、OR条件またはAND条件により「フィルタ」できます。  

下記の例は、次の条件のレコードを抽出するJSONデータを生成します。

```
分類A が "設計" かつ 分類D が "3" のレコード、または、分類B が "テスト" かつ 分類D が "7" 
```

```JavaScript
let data1 = {};
data1.ClassA = '["設計"]';
data1.ClassD = '["3"]';
let data2 = {};
data2.ClassA = '["テスト"]';
data2.ClassD = '["7"]';
let data = {};
data.and_Filter1 = JSON.stringify(data1); // and_で始まる名前なのでAND条件になる。条件のJSONを文字列化して代入する必要がある。
data.and_Filter2 = JSON.stringify(data2); // 上行と同等。
let filter = JSON.stringify(data);
let send_json = { //APIで送信するJSONデータの生成
    ApiVersion: 1.1,
    ApiKey: 'efe7...',
    View: {
        ApiDataType: 'KeyValues',
        GridColumns: ['Title','ClassA','ClassD'],
        ColumnFilterHash: {
            'or_Filter': filter // or_で始まる名前なのでOR条件になる
        },
        ColumnFilterSearchTypes:{
            ClassA: 'ExactMatch', 
            ClassD: 'ExactMatch'
        },
    }
};
```

## ColumnFilterSearchTypesの指定方法

- 検索方法を指定します。
- タイトル、内容、説明、分類項目、の各項目の検索に利用できます。
- ColumnFilterHashと共に使用します。

### 検索方法

|検索方法|ColumnFilterSearchTypesの設定値|
|:----|:----|
|部分一致|"PartialMatch"|
|完全一致|"ExactMatch"|
|前方一致|"ForwardMatch"|

### 検索文字列を1つ指定する場合

ColumnFilterHashに文字列を1つ指定し、ColumnFilterSearchTypesに検索方法を指定します。

次の例では、タイトル項目の値が"中野"で始まるレコードにマッチします。

```JSON
ColumnFilterHash: {
    Title:  "中野"
},
ColumnFilterSearchTypes:{
    Title:  "ForwardMatch"
}
```

### 検索文字列を複数指定する場合

ColumnFilterHashに文字列を配列で指定し、ColumnFilterSearchTypesに検索方法を指定します。ColumnFilterHashに指定した複数の文字列のいずれかとマッチするor条件となります。

次の例では、タイトル項目の値が"中野"または"新宿"で始まるレコードにマッチします。

```JSON
ColumnFilterHash: {
    Title:  "[\"中野\",\"新宿\"]"
},
ColumnFilterSearchTypes:{
    Title:  "ForwardMatchMultiple"
},
```

## ColumnFilterNegativesの指定方法

否定条件にする項目を指定します。こちらのパラメータはColumnFileterHashと併用します。

次の例では、状況項目が未設定(100)以外でレコードの絞り込みを行います。

```JSON
ColumnFilterHash: {
    Status: "[\"100\"]"
},
ColumnFilterNegatives: [
    "Status"
]
```

**本プロパティを使用する場合は「[否定フィルタを使用する](../../../managers-guide/manage-table/filter/table-management-filter-use-negative-filter.md)」を有効化する必要があります。また、ユーザ、グループ、組織を選択肢に設定している項目には使用できません。**

## ColumnSorterHashの指定方法

- ソート順を asc(昇順)/desc(降順) のどちらかで指定します。  
- JSONでは{"項目名":"ソート順"}のペア{"DateA":"asc", "ClassA":"desc"}で指定します。  

```JSON
"ColumnSorterHash":{
    "DataA":"asc",
    "Title":"asc"
}
```

## 制限事項

使用するデータベースによって検索結果が異なる場合があります。

- SQL Server：LIKE句またはフルテキスト検索が使用されます。
- PostgreSQL：ILIKE句またはpg_trgmによるフルテキスト検索が使用されます。
