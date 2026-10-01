---
title: ワークスペースに既存のjsconfig.jsonがある場合の設定
category: Pleasanter Code Assist
order: '4200'
status: ''
parts: ''
urlstring: pleasanter-code-assist-how-to-use-code-completion-jsconfig
translationKey: pleasanter-code-assist-how-to-use-code-completion-jsconfig
shortname: ワークスペースに既存のjsconfig.jsonがある場合の設定
created: 2026-09-03
updated: 2026-09-11
---

## 概要

[Pleasanter Code Assist](index.md) 1.4.0以降でコード補完機能を利用する場合、以下のセットアップが必要です。

1. 型定義ファイルのインストール
1. jsconfig.jsonの作成と型定義ファイルへの参照の追加

これらは通常Pleasanter Code Assistにより自動的に実行されます。しかし、ワークスペース内に既存のjsconfig.jsonが存在する場合、Pleasanter Code Assistは型定義ファイルを作成するものの、既存のjsconfig.jsonに型定義ファイルへの参照を追加しません。既存のjsconfig.jsonを上書きしてしまうと、ユーザが設定した対象ファイル、JavaScriptのバージョン、ライブラリ、パスなどが失われる可能性があるためです。

##### コード補完に必要な型定義ファイル

-   .pleasanter/pleasanter-script.d.ts  
-   .pleasanter/pleasanter-server-script.d.ts

この場合、ユーザ自身が既存の設定を残したまま、対応する型定義ファイルへの参照をjsconfig.jsonに手動で追記する必要があります。本マニュアルではその手順を説明します。

### 確認対象のファイル

確認対象と参照する型定義ファイルは以下のとおりです。4つの対象フォルダから.pleasanterまでの相対パスは、いずれも../../.pleasanterです。

|jsconfig.jsonの場所 | 追加する型定義 |
| --- | --- |
|sites/scripts/jsconfig.json|../../.pleasanter/pleasanter-script.d.ts|
|extensions/scripts/jsconfig.json|../../.pleasanter/pleasanter-script.d.ts|
|sites/serverscripts/jsconfig.json|../../.pleasanter/pleasanter-server-script.d.ts|
|extensions/serverscripts/jsconfig.json|../../.pleasanter/pleasanter-server-script.d.ts|

### 既存のjsconfig.jsonにincludeがある場合

既存のincludeの内容を削除せず、配列の末尾に型定義ファイルを追加してください。以下はsites/scripts/jsconfig.jsonが以下の内容だった場合の一例です。

```json
{
    "compilerOptions": {
        "target": "ES2020"
    },
    "include": [
        "src/**/*.js"
    ]
}
```

"include"にスクリプトの型定義ファイルへの相対パス"../../.pleasanter/pleasanter-script.d.ts"を追加してください。

```json
{
    "compilerOptions": {
        "target": "ES2020"
    },
    "include": [
        "src/**/*.js",
        "../../.pleasanter/pleasanter-script.d.ts"
    ]
}
```

targetなど、ユーザが設定している他の項目は変更しないでください。extensions/scriptsの場合も、追加するパスは同じです。

サーバスクリプトの場合は、"include"にサーバスクリプトの型定義ファイルへの相対パス"../../.pleasanter/pleasanter-server-script.d.ts"を追加してください。

```json
{
    "compilerOptions": {
        "target": "ES2020"
    },
    "include": [
        "src/**/*.js",
        "../../.pleasanter/pleasanter-server-script.d.ts"
    ]
}
```

### 既存のjsconfig.jsonにincludeがない場合

既存のjsconfig.jsonにincludeがない場合は、JavaScriptファイルと型定義ファイルの両方を追加します。型定義ファイルだけを指定すると、同じフォルダ内のJavaScriptファイルがプロジェクトの対象から外れる可能性があります。

スクリプト用の例は以下のとおりです。

```json
{
    "compilerOptions": {
        "allowJs": true,
        "checkJs": false,
        "target": "ES2022",
        "lib": [
            "ES2022",
            "DOM"
        ]
    },
    "include": [
        "**/*.js",
        "../../.pleasanter/pleasanter-script.d.ts"
    ]
}
```

サーバスクリプト用の例は以下のとおりです。サーバスクリプトではブラウザのDOMを使用しないため、libにDOMを追加しません。

```json
{
    "compilerOptions": {
        "allowJs": true,
        "checkJs": false,
        "target": "ES2022",
        "lib": [
            "ES2022"
        ]
    },
    "include": [
        "**/*.js",
        "../../.pleasanter/pleasanter-server-script.d.ts"
    ]
}
```

上記は、既存設定がほとんどない場合の例です。既にcompilerOptionsがある場合は、既存の設定を削除せず、まずincludeへの型定義追加だけを行います。

Pleasanter Code Assistの型定義はincludeから直接読み込むため、コード補完を有効にする目的だけで既存のtypesを変更する必要はありません。ユーザが@types/nodeなどを使用している可能性を考慮し、既存のtypesを空配列へ変更しないでください。

### 既存のjsconfig.jsonがfilesを使用している場合

既存のjsconfig.jsonがincludeではなくfilesで対象ファイルを1件ずつ指定している場合は、対応する型定義ファイルをfilesに追加します。

```json
{
    "files": [
        "sample.js",
        "../../.pleasanter/pleasanter-script.d.ts"
    ]
}
```

この場合、includeに**/*.jsを追加すると、ユーザが意図していなかったJavaScriptファイルまで対象に含めてしまう可能性があります。既存のfilesを維持する方法を優先してください。

### 変更後の確認

設定の変更が済んだら、以下の手順で、コード補完が正しく動作することを確認してください。

1. jsconfig.jsonを編集し、保存してください。
2. 対象のスクリプトファイルを開いてください。
3. スクリプトでは$p.、サーバスクリプトではitems.またはcontext.を入力してください。
4. 補完候補と説明が表示されることを確認してください。

コード補完がすぐに表示されない場合は、Visual Studio Codeのコマンドパレット（Ctrl＋Shift＋P）から「TypeScript: Restart TS Server」を実行してください。

それでも表示されない場合は、includeまたはfilesの相対パス、JSONの構文エラー、excludeで.pleasanterを除外していないかを確認してください。

## 対応バージョン

|対応バージョン|内容|
|---|---|
|プリザンター1.5.8.0 以降|コード補完機能を追加|
