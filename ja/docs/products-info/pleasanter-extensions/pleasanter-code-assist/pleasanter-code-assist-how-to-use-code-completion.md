---
title: コード補完
category: Pleasanter Code Assist
order: '4100'
status: ''
parts: ''
urlstring: pleasanter-code-assist-how-to-use-code-completion
translationKey: pleasanter-code-assist-how-to-use-code-completion
shortname: ''
created: 2026-09-03
updated: 2026-09-11
---

## 概要

[Pleasanter Code Assist](index.md)のコード補完機能について説明します。

### コード補完の対象

コード補完の対象は、以下の4つのフォルダ配下に配置された「[スクリプト](../../../managers-guide/manage-table/scripts/index.md)」または「[サーバスクリプト](../../../managers-guide/manage-table/server-script/index.md)」です。

|種別|フォルダ|
|:--|:--|
|「[スクリプト](../../../managers-guide/manage-table/scripts/index.md)」|sites/scripts|
|「[サーバスクリプト](../../../managers-guide/manage-table/server-script/index.md)」|sites/serverscripts|
|「[拡張スクリプト](../../../developers-guide/extended-features/extended-script.md)」|extensions/scripts|
|「[拡張サーバスクリプト](../../../developers-guide/extended-features/extended-server-script.md)」|extensions/serverscripts|

### 補完される情報

Pleasanter Code Assistのコード補完機能で補完される情報は以下のとおりです。補完候補の表示に加え、マウスホバーによる説明表示や定義への移動が可能です。

##### スクリプトの場合

-   $pのメソッド、引数、戻り値、説明、使用例  
-   プリザンターでよく使う一部のjQueryメソッド

##### サーバスクリプトの場合

-   context、items、model、view、httpClient、$psなどのグローバルオブジェクト  
-   メソッドの引数、戻り値、レコードや配列の型

ユーザはPleasanter Code Assist 1.4.0以降に含まれる型定義ファイルをVisual Studio Codeのワークスペースへ適切に配置することで、Visual Studio Code標準のIntelliSense（インテリセンス）によるコード補完機能を利用できます。

##### スクリプトの編集時にコード補完を使用している様子

![スクリプトの編集中にコード補完が動作している様子](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-code-assist/assets/b80891bd56d34b77a5079364cd8745ce.png)

##### サーバスクリプトの編集時にコード補完を使用している様子

![サーバスクリプトの編集中にコード補完が動作している様子](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-code-assist/assets/1212508fa6b7474480a2beaa45ac559f.png)

## 制限事項

1. 何らかの理由により、既存のワークスペースにjsconfig.jsonが存在する場合、型定義ファイルとJavaScriptファイルとの関連付けをユーザが手動で行う必要があります。詳細は「[ワークスペースに既存のjsconfig.jsonがある場合の設定](pleasanter-code-assist-how-to-use-code-completion-jsconfig.md)」を参照してください。
1. スクリプトのコード補完では、プリザンターのAPIが返すjQueryオブジェクトに対して、よく使うメソッドのコード補完が表示されます。主な対象はval、attr、prop、text、css、data、addClass、removeClass、show、hide、on、findなどです。これらはjQueryの完全な型定義ではありません。未定義のjQueryメソッドも実行できますが、補完候補や詳しい説明は表示されません。

## 操作手順

### コード補完のセットアップ

#### Pleasanter Code Assist 1.4.0以降でワークスペースを新規作成する場合

Pleasanter Code Assist 1.4.0以降で「Pleasanter Code Assist：コマンドによる作業フォルダ作成」で説明されている手順を実施した場合、特別な設定は不要です。

#### 既存のワークスペースではじめてコード補完を使用する場合

[Pleasanter Code Assist](index.md)の起動時、ワークスペース内にconnectionSetting、sites、extensionsのいずれかが存在し、型定義ファイルが未配置の場合、以下のメッセージが表示されます。「**作成する**」を選択してください。

```text
コード補完用の型定義ファイルがワークスペースにありません。作成しますか？
```

![型定義ファイルを作成するかどうかを確認するメッセージ](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-code-assist/assets/b46120ac526445dd852186f682000b6a.png)

ユーザが選択できる選択肢は以下の2つです。いずれも選択せずに、メッセージを閉じただけの場合、「**作成する**」を選択した扱いとなります。

|選択肢|説明|
|:--|:--|
|作成する|必要なディレクトリ、型定義ファイル、jsconfig.jsonを作成する|
|今回はしない|今回は作成せず、同じバージョンのPleasanter Code Assistでは、次回以降も案内しない|

#### Pleasanter Code Assistのバージョンアップ後に型定義ファイルを更新する場合

新しいバージョンのPleasanter Code Assistに含まれる型定義ファイルと、ワークスペースへ配置済みの型定義ファイルが一致しない場合、Visual Studio Codeの起動時に以下のメッセージが表示されます。「**更新する**」を選択してください。

```text
Pleasanterの型定義が更新されています。ワークスペースの型定義ファイルを更新しますか？
```

![型定義ファイルを更新するかどうかを確認するメッセージ](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-code-assist/assets/34bdb89cdee34c1f8f7414279ef2c605.png)

ユーザが選択できる選択肢は以下の2つです。

|選択肢|説明|
|:--|:--|
|更新する|Pleasanter Code Assistが管理する型定義ファイルとjsconfig.jsonを最新の内容へ更新する|
|今回はしない|今回は更新せず、型定義の内容が次に変わるまで案内しない|

### 作成されたファイルを確認する

型定義ファイルを作成または更新すると、選択した作業フォルダに以下のファイルが作成されます。  
&nbsp;
```text
<作業フォルダ>
├─ .pleasanter
│  ├─ pleasanter-script.d.ts
│  └─ pleasanter-server-script.d.ts
├─ sites
│  ├─ scripts
│  │  └─ jsconfig.json
│  └─ serverscripts
│     └─ jsconfig.json
└─ extensions
   ├─ scripts
   │  └─ jsconfig.json
   └─ serverscripts
      └─ jsconfig.json
```

|各ファイルの説明|
|:--|
|・「.pleasanter」フォルダー内の2ファイルが型定義ファイルです。<br>・jsconfig.jsonは、対象フォルダのJavaScriptと型定義ファイルとを関連付けます。<br>・何らかの理由により、既存のワークスペースにjsconfig.jsonが存在する場合、型定義ファイルとの関連付けをユーザが手動で実施する必要があります。詳細は「[ワークスペースに既存のjsconfig.jsonがある場合の設定](pleasanter-code-assist-how-to-use-code-completion-jsconfig.md)」を参照してください。<br>・スクリプト用の設定はDOMの型情報を含みます。<br>・サーバスクリプト用の設定はDOMの型情報を含みません。<br>・jQueryの型定義はスクリプト用の型定義ファイルにのみ含まれます。<br>・作成されたファイルはPleasanter Code Assistが管理するファイルであることを示すコメントを含みます。|

Pleasanter Code AssistのパラメータhideGeneratedTypeFilesをfalseに設定すると、Visual Studio Codeの「エクスプローラー」でも確認できます。

![Visual Studio Codeのエクスプローラーに表示された型定義ファイル](https://pleasanter.org/files/images/ja/products-info/pleasanter-extensions/pleasanter-code-assist/assets/a2acfd7d861d4541b6e3a1cc01cf5f34.png)

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|プリザンター1.5.8.0 以降|コード補完機能を追加|
