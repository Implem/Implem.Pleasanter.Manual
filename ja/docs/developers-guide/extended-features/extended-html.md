---
title: 拡張HTML
category: 拡張機能
order: '0'
status: ''
parts: ''
urlstring: extended-html
translationKey: extended-html
shortname: ''
created: 2020-08-12
updated: 2025-01-30
---

## 利用上の注意

本機能を利用するにはHTMLの知識が必要です。誤った設定を行うとプリザンターが利用できなくなる可能性がありますので、十分なテストを行った上でご利用ください。

## 拡張スタイルの設定方法

.¥Pleasanter¥App_Data¥Parameters¥ExtendedHtmls¥ 配下にHTMLを記載したテキストファイルを作成し、IISを再起動してください。  
 ExtendedHtmls配下はフォルダで階層化することが可能です。この場合、配下全てのHTMLファイルが読み込まれます。

![ExtendedHtmlsフォルダ配下にHTMLファイルを配置した状態](https://pleasanter.org/files/images/ja/developers-guide/extended-features/assets/1d86202014f34f7abe55e88b8a753ca4.png)

## 表示ブロックとファイル名

現在ご利用できる、拡張HTMLのファイルの一覧を下記に記載します。

| No. | 表示ブロックID                     | ファイル名                                 | 挿入場所                         |
| --- | ---------------------------------- | ------------------------------------------ | -------------------------------- |
| 1   | LoginGuideTop                      | LoginGuideTop_ja.html                      | ログイン画面入力フォームの上部   |
| 2   | LoginGuideBottom                   | LoginGuideBottom_ja.html                   | ログイン画面入力フォームの下部   |
| 3   | SecondaryAuthenticationGuideTop    | SecondaryAuthenticationGuideTop_ja.html    | 二段階認証コード入力エリアの上部 |
| 4   | SecondaryAuthenticationGuideBottom | SecondaryAuthenticationGuideBottom_ja.html | 二段階認証コード入力エリアの下部 |
| 5   | HtmlHeaderTop                      | HtmlHeaderTop_ja.html                      | HTMLヘッダタグの先頭             |
| 6   | HtmlHeaderBottom                   | HtmlHeaderBottom_ja.html                   | HTMLヘッダタグの最後             |
| 7   | ColumnTop                          | ColumnTop_ja.html                          | 編集画面の項目の上部             |
| 8   | ColumnBottom                       | ColumnBottom_ja.html                       | 編集画面の項目の下部             |
| 9   | HtmlBodyTop                        | HtmlBodyTop_ja.html                        | HTML bodyタグの先頭              |
| 10  | HtmlBodyBottom                     | HtmlBodyBottom_ja.html                     | HTML bodyタグの最後              |

![拡張HTMLの表示ブロックの挿入場所を示す図](https://pleasanter.org/files/images/ja/developers-guide/extended-features/assets/bd61e08ec9a04219bd6ddce2c7a2d901.png)

![拡張HTMLの表示ブロックの挿入場所を示す図（続き）](https://pleasanter.org/files/images/ja/developers-guide/extended-features/assets/2d1da8b6f3264defb0848fc5e92ab5ca.png)

## 使用例

LoginGuideTop_ja.htmlを設置した場合。

``` html linenums="1"
<span style="color: red; font-size: 2em; display: inline-block; width: 100%; text-align: center; margin-bottom: 1em;">
ログインに関する説明など。<br>
HTMLタグも使用可能です。
</span>
```

![LoginGuideTop_ja.htmlを設置したログイン画面](https://pleasanter.org/files/images/ja/developers-guide/extended-features/assets/ca668d2c3a6e474eb1b876877e04bb62.png)
