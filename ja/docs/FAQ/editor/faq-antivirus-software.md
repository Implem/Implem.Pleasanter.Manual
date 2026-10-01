---
title: ウイルス対策ソフトを導入したサーバで稼働しているプリザンターにおいてファイルのアップロードに失敗する
category: FAQ：編集画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-antivirus-software
translationKey: faq-antivirus-software
shortname: ''
created: 2024-09-26
updated: 2024-09-26
---

## 回答

ウイルス対策ソフトの監視の除外設定を行うことで解消する可能性があります。

---

## 概要

以下のテンポラリファイル格納用フォルダをウイルス対策ソフトの監視から除外することで解消する可能性があります。

### 対象フォルダ

以下の対象フォルダは、マニュアルの記載どおりにセットアップした場合の一例です。

``` text title="テンポラリファイル格納用フォルダ"
C:\web\pleasanter\Implem.Pleasanter\App_Data\Temp
```
