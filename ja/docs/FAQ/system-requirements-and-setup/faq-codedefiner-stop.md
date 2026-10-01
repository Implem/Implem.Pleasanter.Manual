---
title: セットアップを自動化した際にCodeDefinerの処理が止まってしまう
category: FAQ：動作環境、セットアップ
order: '0'
status: ''
parts: ''
urlstring: faq-codedefiner-stop
translationKey: faq-codedefiner-stop
shortname: ''
created: 2024-10-01
updated: 2024-10-04
---

## 回答

CodeDefinerの実行コマンドの引数に「/y」をつけてください。

---

## 概要

セットアップを自動化している際に、Edition確認の入力待ちで処理が止まってしまう可能性があります。yを選択した状態で実行する場合は引数に「/y」を指定してください。

### コマンド

```
dotnet Implem.CodeDefiner.dll _rds /y
```

## 関連情報

[CodeDefinerのコマンド一覧](../../setup/codedefiner/codedefiner-command.md)
