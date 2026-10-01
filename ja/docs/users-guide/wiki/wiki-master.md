---
title: 選択肢一覧のマスタデータとして使用する
category: Wiki機能
order: '0'
status: ''
parts: ''
urlstring: wiki-master
translationKey: wiki-master
shortname: ''
created: 2020-07-21
updated: 2024-06-18
---

## 概要

Wikiをマスターとして使用することで、複数の状況、分類項目に共通の選択肢を設定する際に一覧を共通化できます。

## 操作手順

1.  任意のフォルダ内にWikiを作成します。
1.  分類に記載する選択肢一覧をWikiに改行区切りで記載します。

    ![選択肢一覧を改行区切りで記載したWiki](https://pleasanter.org/files/images/ja/users-guide/wiki/assets/00d2c3d636b1423e82605dca2dc256ee.png)

1.  Wikiの「サイトID」を控えます。Wikiの「サイトID」は、Wikiの画面上で「管理」→「Wikiの管理」を開き、下図赤枠に表示された数字です。

    ![Wikiの管理画面で赤枠に示されたサイトID](https://pleasanter.org/files/images/ja/users-guide/wiki/assets/60e81004d9774b81b23b18139654bfdb.png)

    !!! warning "よくある勘違い"
        内容を記載する際の下記画面に表示されたIDとは異なります。

        ![内容を記載する画面に表示されるID。サイトIDとは異なる](https://pleasanter.org/files/images/ja/users-guide/wiki/assets/0c588ea89cf845878c51a6041aad4553.png)

        上記、Wikiの管理で表示されるサイトIDを控えてください。

1.  分類項目を作りたいテーブルのテーブルの管理を開きます。
1.  エディタタブを開き分類項目の詳細設定を開きます。
1.  選択肢一覧に`[[12232]]`を入力します。`12232`の部分には「Wikiの管理」画面の「サイトID」を入力します。

    ![分類項目の選択肢一覧にWikiのサイトIDを入力した画面](https://pleasanter.org/files/images/ja/users-guide/wiki/assets/bb756ac4670443eda2aef85040dc90fe.png)

1.  「更新」ボタンを押します。同様に他のテーブルにも`[[12232]]`を設定します。
1.  上記の設定によりWikiに記載した選択肢を複数のテーブルで共有して使用することができます。Wikiを更新すれば全てのテーブルの選択肢が変化します。
