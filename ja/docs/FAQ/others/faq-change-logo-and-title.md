---
title: ロゴ画像やタイトルを変更したい
category: FAQ：その他画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-change-logo-and-title
translationKey: faq-change-logo-and-title
shortname: ''
created: 2020-07-30
updated: 2026-03-10
---

## 回答

[テナントの管理](../../managers-guide/tenant-administration/index.md)で変更します。画像ファイルを差し替えることでも変更できます。

---

## 概要

[テナント名](../../managers-guide/tenant-administration/tenant-logo.md)のロゴ、タイトルは[テナントの管理](../../managers-guide/tenant-administration/index.md)で変更します。また、画像ファイルを差し替えることでも変更できます。ここでは画像ファイルについて説明します。

## 画像ファイルについて

プリザンターで使用されているロゴ画像はImagesフォルダに格納されています。各ファイル名を変更せずにImagesフォルダ配下の画像を置き換えることで画像の変更が可能です。各画像の利用場所と使用目的の説明などを記載します。  

なお、一部の画像は元の画像サイズのまま表示されることがあります。サイズを調整してから差し替えてください。

| 画面                             | イメージファイル名                                 | サイズ(px) | 説明                                                                                                                                                      |
| :------------------------------- | :------------------------------------------------- | :--------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 全画面共通（ログイン画面を除く） | logo-corp.png                                      | H32×W33    | 「管理」→[テナントの管理](../../managers-guide/tenant-administration/index.md)を選択し、ロゴタイプを「画像とテキスト」に設定したときに表示されるHAYATOロゴ画像。                                             |
| 全画面共通                       | logo-corp-with-title.png                           | H32×W180   | 「管理」→[テナントの管理](../../managers-guide/tenant-administration/index.md)を選択し、ロゴタイプを「画像のみ」に設定したときに表示されるHAYATOとPleasanterの文字の画像。ログイン画面ではこの画像を表示する |
| トップ画面                       | hayato1.png<br>hayato2.png<br>hayato3.png<br>hayato4.png | H953×W725  | バージョン1.5.1.0以前のトップ画面に表示されるスタートガイド内のHAYATO画像。バージョン1.5.2.0以降では使用されません。                                                                                                                    |
| トップ画面                       | 下記参照| スケーラブル | バージョン1.5.2.0以降のトップ画面に表示されるスタートガイド内のロゴ画像。ファイル名末尾に-dが付くファイルは、第2世代インターフェースのテーマ「midnight」を選択した際に使われる画像。掲載サイズはH80×W80。 |
| バージョン確認画面               | logo-version.png                                   | H55×W248   | 「ヘルプ」→「バージョン」で表示されるバージョン情報の画像                                                                                                 |

#### トップ画面で使われるイメージファイル名（1.5.2.0以降）

1.5.2.0以降の[スタートガイド](../../users-guide/common/startguide.md)では以下のイメージファイルが使用されます。

![スタートガイドで使われるイメージファイルの位置を示した図](https://pleasanter.org/files/images/ja/FAQ/others/assets/9cffd98d69e9460c8314273471e3b075.png)

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.5.2.0以降|トップ画面のスタートガイド内画像の情報を更新|

## 関連情報

-   [テナント管理機能](../../managers-guide/tenant-administration/index.md)
-   [テナント管理機能：ロゴ、タイトル、ロゴ画像](../../managers-guide/tenant-administration/tenant-logo.md)
-   [共通機能：スタートガイド](../../users-guide/common/startguide.md)