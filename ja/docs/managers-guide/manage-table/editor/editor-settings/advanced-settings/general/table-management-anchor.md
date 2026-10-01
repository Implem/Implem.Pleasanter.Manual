---
title: アンカー
category: エディタ
order: '6500'
status: ''
parts: ''
urlstring: table-management-anchor
translationKey: table-management-anchor
shortname: アンカー
created: 2022-07-15
updated: 2024-04-09
---

## 概要

[分類項目](../../columns/table-management-class.md)にHTMLのAタグ(リンク)を設定できます。

## 制限事項

1. [分類項目](../../columns/table-management-class.md)でのみ設定できます。
1. [分類項目](../../columns/table-management-class.md)はフリーテキスト形式である必要があります。

## 前提条件

1. 設定を行うには「サイトの管理権限」が必要です。

## 設定内容

![分類項目の詳細設定のアンカー関連の設定欄](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/700c3a121c194a82a51cb077bafbcb14.png)
"アンカー"チェックボックスをオンにします。  
"アンカー書式"にhref属性に設定する文字列を記入します。文字列として"{Value}"を入力した部分は、その分類項目の値で置換されます。
"アンカーを新しいタブで開く"チェックボックスをオンにすることで、アンカーをクリックすると新しいタブで開くことができるようになります。

## 動作イメージ

![アンカーを設定した分類項目。値がリンクとして表示される](https://pleasanter.org/files/images/ja/managers-guide/manage-table/editor/editor-settings/advanced-settings/general/assets/cf3c01837bc3482da397ecaf20b894ef.png)

"アンカー"にチェックを入れた項目では、その分類項目に記入した文字がハイパーリンクとしてクリック可能となります。上の鉛筆アイコンをクリックして編集モードにすると、リンクは解除され通常の入力欄となります。

## 活用例

### 分類項目の入力値を URL のパラメータとして使う

アンカー書式を以下のような形式とすることで  URL のパラメータとして利用することができます。
```
https://example.com/?q={Value}
```

### メールを開く

アンカー書式を以下のような形式とすることで、分類項目に入力したメールアドレスを宛先としたメールの作成画面を起動することができます。
```
mailto:{Value}
```

※ OS/ブラウザの対応状況によって動作が異なります。

### 電話を掛ける

アンカー書式を以下のような形式とすることで、分類項目に入力した電話番号を架電先とした電話の発信画面を起動することができます。
```
tel:{Value}
```

※ OS/ブラウザの対応状況によって動作が異なります。

これらの他にも Slack など URL スキームに対応するアプリケーションを起動可能な場合がございます。URL リンクによって特定のアプリケーションを起動する方法の有無、パラメータ指定方法は、各アプリケーションの開発元に確認してください。

## 関連情報

-   [テーブルの管理：項目：分類](../../columns/table-management-class.md)
