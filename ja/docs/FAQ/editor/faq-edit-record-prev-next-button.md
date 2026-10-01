---
title: 編集画面のレコード移動ボタンが表示されない
category: FAQ：編集画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-edit-record-prev-next-button
translationKey: faq-edit-record-prev-next-button
shortname: ''
created: 2023-10-05
updated: 2024-07-01
---

## 回答

以下の対応内容を実施してください。
1. [General.json](../../setup/parameters/general.json.md)のSwitchTargetsLimitを見直す
1. 一覧画面での対象レコード件数をSwitchTargetsLimit以下になるように絞り込む

---

## 概要

通常、編集画面の右上部には「前」、「次」などのレコード移動ボタンが表示されます。
![編集画面の右上にレコード移動ボタンが表示されている状態](https://pleasanter.org/files/images/ja/FAQ/editor/assets/5352f8af7f914401a91bcc97e78e14db.png)

ただし[General.json](../../setup/parameters/general.json.md)のSwitchTargetsLimitで設定されたレコード数(既定値は500件)を超えたレコードが存在する場合、レコード移動ボタンは表示されず、再読込ボタンのみ表示されます。
![レコード数が上限を超え、再読込ボタンだけが表示されている状態](https://pleasanter.org/files/images/ja/FAQ/editor/assets/41c48607c2ba4e56891267c0f979b241.png)

テーブルのレコード総数がSwitchTargetsLimitで設定した数を超えた状態でレコード移動ボタンを表示したい場合は、一覧画面でフィルタ設定を行い対象レコード数を設定件数以下に絞り込むか、SwitchTargetsLimitの設定値を大きくしてください。

## 関連情報

-   [パラメータ設定：General.json](../../setup/parameters/general.json.md) 