---
title: TextEditorUI.json
category: パラメータ設定
order: '0'
status: ''
parts: ''
urlstring: texteditorui-json
translationKey: texteditorui-json
shortname: TextEditorUI.json
created: 2025-08-25
updated: 2025-09-09
---

## 注意事項

パラメータ変更時は[パラメータ変更時の確認事項](parameter-edit.md)を確認してください。

## 設定値

本パラメータファイルの設定値は下記の通りです。  

|パラメータ名|設定例|説明|
|:--|:--|:--|
|RichTextEditor|（省略）|以下の3つの配列DefaultFont、FontList、FontSizeを格納するオブジェクトです|
|DefaultFont|"DefaultFont":["sans-serif"]|リッチテキストエディタのデフォルトフォントを定義します。DefaultFontには、様々な環境（OS）から使われることを想定したフォントが設定されています。特別な理由がない限り変更しないでください。|
|FontList|"FontList": ["Yu Gothic", "BIZ UDPGothic"]|リッチテキストエディタで使いたいフォントを追加してください。ただし、ユーザ環境（OS）に存在しないフォントを指定して使うことはできません。|
|FontSize|"FontSize": [16, 18]|リッチテキストエディタで使用できる文字サイズのバリエーションを定義します。|

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.20.0以降|TextEditorUI.jsonを追加|

## 関連情報

-   [パラメータ設定：パラメータ変更時の確認事項](parameter-edit.md)
