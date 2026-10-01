---
title: 通知 - メッセージ本文
category: 通知
order: '0'
status: ''
parts: ''
urlstring: table-management-notification-messagebody
translationKey: table-management-notification-messagebody
shortname: ''
created: 2025-06-18
updated: 2026-02-09
---

## 概要

通知機能で送信されるメッセージ本文を指定します。通知の本文は、次の要素を指定できます。

- 固定文字列
- 文字列を置き換える(プレースホルダ)
- 書式指定文字列

## デフォルトメッセージ

デフォルトのメッセージ文として、次の書式の内容が送信されます。

```text
{Url}
{"Name":"[項目名N]"}

{UserName}<{MailAddress}
```

※ "[項目名N]" はテーブルの全ての項目が列挙される繰り返し項目です。

## メッセージ本文をカスタマイズする

通知設定で「カスタムデザイン」をオンにすると、メッセージ本文をカスタマイズできます。

設定例

![「カスタムデザイン」でメッセージ本文を編集した設定例](https://pleasanter.org/files/images/ja/managers-guide/manage-table/notifications/assets/b477755e58f74bb18a4b737ae572aee2.png)

出力結果

```text
以下の情報が更新されました！
http://servername/items/999/edit
★タイトル ☆ ネットワーク要件を確認する ◆ ネットワーク要件と機器を確認する
コメント : 要件定義書の作成、完了しました。成果物は所定のフォルダに格納済です。
山口太郎< taro@yamaguchi123.co.jp >
```

## 固定文字列を指定する

- 任意の文字列を固定文字列として記載可能です。
- 「書式指定文字列」とは別の行とする必要があります。

## 指定項目を挿入する(プレースホルダ)

- 以下のプレースホルダを記述すると、 指定項目を挿入して通知されます。
- 固定文字列およびプレースホルダは、同一行に混在可能です。
- プレースホルダの波括弧および英字は、本マニュアルの記述と厳密に一致させる必要があります。

|プレースホルダ|置換文字列|
|----|----|
|{Url}|レコードのURLに置換されます|
|{LoginId}|操作したユーザのログインIDに置換されます|
|{UserName}|操作したユーザの名前に置換されます|
|{MailAddress}|操作したユーザのメールアドレスに置換されます|

## 書式指定文字列

次の属性で構成される JSON オブジェクトを 1 行の文字列として記述することで、データ項目を本文に展開できます。

### 書式指定文字列の例

```json
{"Name":"[作業工程]","Prefix":"■","Delimiter":" : ","Allow":" => ","Always":true}  
```

出力結果：変更がある場合

```text
■作業工程 : 設計 => 開発
```

出力結果：変更がない場合

```text
■作業工程 : 設計
```

### 記述上の注意

- 書式指定文字列は、行単位で処理されるため、改行を含まないように記述します。
- 同一行に複数の書式指定文字列を配置、プレースホルダ・固定文字列を混在はできません。
- 属性名を省略した場合は既定値を使用します。
- 属性名は、大文字小文字を正確に記述する必要があります。
- Name属性にID項目を指定することはできません。

### 利用できる属性名

|属性名|挙動|
|--|--|
|Name|出力したい項目の表示名を[表示名]と記述します。必須 ※1|
|Prefix|出力する項目の先頭にプレフィックスを付与することができます。既定値は空文字列です|
|Delimiter|項目の表示名の後に表示する区切り文字です。既定値は“ : ”です|
|Always|変更がない場合でも出力する場合はtrueにします。既定値はfalseです|
|ValueOnly|項目名および Delimiter を表示せず、項目の値のみ表示します。既定値はfalseです|
|ConsiderMultiline|MarkDown形式の項目で、項目名 Delimiter の直後および Allow の前後で改行します。既定値はtrueです|
|DiffTypes|更新前後の差分の表示方式を指定します。<br>・Standard: 古い値と新しい値を個別に表示します。<br>・DiffMatchPatch: 値の差分（追加、削除された部分）で表現します。<br>既定値は Standardです。|
|DisplayTypes|DiffTypesがStandardの場合に、更新した際に古い値と新しい値の両方を表示するか(BeforeAndAfterChange)、古い値のみを表示するか(BeforeChange)、新しい値のみを表示するか(AfterChange)選択して指定します。既定値は“BeforeAndAfterChange”です。|
|Allow|DiffTypesがStandardの場合に、更新した際に古い値と新しい値の間に表示する区切り文字です。既定値は“ => ”です。|
|StartBracket|DiffTypesがDiffMatchPatchの場合に、差分表記の開始を表す文字列を指定します。既定値は"("です。|
|EndBracket|DiffTypesがDiffMatchPatchの場合に、差分表記の終了を表す文字列を指定します。既定値は")"です。|
|DeletePrefixSymbol|DiffTypesがDiffMatchPatchの場合に、削除された部分の開始を表す文字列を指定します。既定値は"-"です。|
|DeleteSuffixSymbol|DiffTypesがDiffMatchPatchの場合に、削除された部分の終了を表す文字列を指定します。既定値は""(空文字)です。|
|AddPrefixSymbol|DiffTypesがDiffMatchPatchの場合に、追加された部分の開始を表す文字列を指定します。既定値は"+"です。|
|AddSuffixSymbol|DiffTypesがDiffMatchPatchの場合に、追加された部分の終了を表す文字列を指定します。既定値は""(空文字)です。|

※1 Name は必須です。

## 属性名：DiffTypesによる出力の違いについて

更新前後の差分の表示方式を指定する属性名のDiffTypesは、出力結果を次のように変更できます。

### DiffTypesがStandardの場合

設定内容

```json
{"Name":"[タイトル]"}  
```

出力結果

```
タイトル : ドキュメント作成 => 設計書作成作業
```

### DiffTypesがDiffMatchPatchの場合

設定内容

```json
{"Name":"[タイトル]","DiffTypes":"DiffMatchPatch"}  
```

出力結果

```
タイトル : (-ドキュメント)(+設計書)作成(+作業)
```

### DiffMatchPatchの書式をカスタマイズした場合

設定内容

```json
{"Name":"[タイトル]", "DiffTypes":"DiffMatchPatch", "StartBracket":"[", "EndBracket":"]", "DeletePrefixSymbol":"del:", "DeleteSuffixSymbol":"/del", "AddPrefixSymbol":"add:", "AddSuffixSymbol":"/add"}  
```

出力結果

```
タイトル : [del:ドキュメント/del][add:設計書/add]作成[add:作業/add]
```

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.2.26.0 以降|作成後／更新後／削除後の通知タイミングを追加|
|1.3.2.0 以降|コピー後／一括更新後／一括削除後の通知タイミングを追加|
|1.3.3.0 以降|インポート後の通知タイミングを追加|
|1.3.9.0 以降|ユーザ/組織/グループでの動的な宛先指定としてアドレスに分類項目を指定する機能を追加|
|1.3.10.0 以降|ユーザ/組織/グループでの動的な宛先指定としてアドレスにIDを直接指定する機能を追加|
|1.3.17.0 以降|HTTPクライアントを利用した通知機能を追加|
|1.4.8.0 以降|DiffMatchPatch形式で値の差分を表示する機能を追加|
|1.4.10.0 以降|メールの宛先にCc、Bccを追加|
