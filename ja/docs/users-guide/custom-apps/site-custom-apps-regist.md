---
title: カスタムアプリの登録
category: カスタムアプリ機能
order: '11'
status: ''
parts: ''
urlstring: site-custom-apps-regist
translationKey: site-custom-apps-regist
shortname: カスタムアプリ,カスタムアプリの登録
created: 2024-09-03
updated: 2024-09-10
---

## 概要

サイトパッケージのエクスポートにより出力したサイトパッケージ（JSONファイル）をサイト新規作成ページに登録することによって、サイトパッケージを簡単に利用することができるようになります。ここではカスタムアプリの登録手順について説明します。

## 制限事項

1. 添付ファイルおよび画像はインポートできません。
1. スクリプトが埋め込まれていてサイトIDやレコードIDなどを指定している場合にはIDが変更になるため正しく動作しなくなる場合があります。スクリプトに記述されたIDは手動で変更していただく必要がございます。
1. 異なるプリザンターからエクスポートしたサイトパッケージをインポートする場合、レコードに格納された組織、グループ、ユーザの情報は、インポート先のIDに変換されません。
1. 「データを含める」、「サイトのアクセス制御を含める」、「レコードのアクセス制御を含める」、「項目のアクセス制御を含める」、「通知を含める」、「リマインダーを含める」の条件は全て「含める」側の条件が適用されます、インポートしたくない物はエクスポート時に条件として指定してください。
1. 説明項目には画像添付できません。

## 前提条件

1. 「テナント管理権限」が必要です。
1. カスタムアプリを有効にするためには設定が必要です。マニュアルを参照し事前に設定ください。
[パラメータ設定：CustomApps.json](../../setup/parameters/user-custom-apps-json.md)

## 操作手順

1. トップまたは任意のフォルダに移動しナビゲーションメニューから「新規作成」をクリックしてください。
![ナビゲーションメニューの「新規作成」](https://pleasanter.org/files/images/ja/users-guide/custom-apps/assets/80a962ce4db34fb6917a672145e68ffa.png)
1. [カスタムアプリ](index.md)タブを選択
1. インポートボタンをクリックしてください。
![カスタムアプリタブの「インポート」ボタン](https://pleasanter.org/files/images/ja/users-guide/custom-apps/assets/1dba1db09260493982b9574bf436941f.png)
1. ダイアログが表示されるのでサイトパッケージ（JSONファイル）を選択します。
1. 必要に応じてタイトルや説明などを変更します。
1. インポートボタンをクリックしてください。
![サイトパッケージを選んでタイトルや説明を入力するインポートのダイアログ](https://pleasanter.org/files/images/ja/users-guide/custom-apps/assets/ed5ab49abf7646e58d8515e4af638bb5.png)
1. 画面下に「"X"を登録しました。」とメッセージが表示されたら完了です。
![画面下に登録完了のメッセージが表示されたところ](https://pleasanter.org/files/images/ja/users-guide/custom-apps/assets/682f62b3dcc042979cea9026916776d5.png)

## 関連情報

-   [カスタムアプリ機能](index.md)
-   [カスタムアプリ機能：カスタムアプリの編集](site-custom-apps-edit.md)
-   [カスタムアプリ機能：カスタムアプリの削除](site-custom-apps-delete.md)
-   [テーブルの管理：サイトパッケージ：サイトパッケージのエクスポート](../../managers-guide/manage-table/site-package/site-package-export.md)
