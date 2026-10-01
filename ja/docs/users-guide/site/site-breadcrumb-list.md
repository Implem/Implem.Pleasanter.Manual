---
title: 'パンくずリスト'
category: サイト機能
order: '0'
status: ''
parts: ''
urlstring: breadcrumb-list
translationKey: breadcrumb-list
shortname: パンくずリスト
created: 2025-10-30
updated: 2026-06-16
---

## 概要
サイト機能の1つである「パンくずリスト」について説明します。

「パンくずリスト」は、「トップ画面」から見た現在表示中のサイトの位置を階層的に表示します。 

![トップからの位置を階層的に示すパンくずリスト](https://pleasanter.org/files/images/en/legacy/assets/76a44bbe5290435ebb625d10ac313124.png)

### パンくずリストの機能
「トップ」を含め、各サイト名にはハイパーリンクが設定されており、クリックすると（「[既定のビュー](../../managers-guide/manage-table/grid/table-management-default-view.md)」の設定とは無関係に）次のURLへ遷移します。

```
http(s)://{サーバ名}/items/{サイトID}/index
```

サイト種別ごとの開く画面は、下表の通りです。

|サイト種別|開く画面|
|:--|:--|
|フォルダ|サイト一覧画面|
|テーブル|一覧画面|
|Wiki|Wikiの編集画面|
|ダッシュボード|ダッシュボード|

完全なサイト名が表示されるのは、トップを1階層目として5階層目までです。

![5階層目まで完全なサイト名が表示されたパンくずリスト](https://pleasanter.org/files/images/en/legacy/assets/05030f7271bf4daea124a8cc6e1ef3a8.png)

6階層目のサイトを開くと、2階層目のサイト名が省略表示されます。「…」にカーソルを置くと、完全なサイト名を確認できます。

![6階層目のサイトで2階層目のサイト名が「…」に省略されたパンくずリスト](https://pleasanter.org/files/images/en/legacy/assets/34e5556c69a74eccbe68b761838fa75f.png)

なお、5階層目までに長いサイト名が現れる場合は、表示の都合に合わせ、長いサイト名が末尾から省略表示されます。このときは「…」にカーソルを置いても完全なサイト名は表示されません（※[第1世代インターフェース](../../managers-guide/user-administration/user-management-theme.md)では、トップ画面から数えて6階層目以降を閲覧する場合も、サイト名の表示は省略されません）。

### 「トップ」のリンク先を変更する

パンくずリストの「トップ」のリンク先を変更することができます。  
詳細は「[FAQ：トップページを特定のページにしたい。](../../FAQ/top-screen-site-menu/faq-top-url-and-login-after-url.md)」を参照してください。

### 「現在の表示を共有」ボタン

サイト（フォルダ、テーブル、Wiki、ダッシュボード）を開くと、「パンくずリスト」の左端に、「現在の表示を共有」ボタンが表示されます。

![パンくずリストの左端にある「現在の表示を共有」ボタン](https://pleasanter.org/files/images/en/legacy/assets/053e27169aa7484fa95027c574fd9431.png)

「現在の表示を共有」ボタンをクリックすると、「[ビュー](../table/record-authoring/data-analysis/table-record-view.md)」で選択したビュー、フィルタや集計の結果を含んだURLがクリップボードにコピーされます。なお、フィルタ条件を多数設定した複雑なビューの場合、「現在の表示を共有」ボタンでコピーしたURLを開けないケースがあります。対処方法の詳細は[FAQ：フィルタ条件を多数選択した複雑なビューの場合は、「現在の表示を共有」ボタンでコピーしたURLが開けないケースがある](../../FAQ/others/faq-url-copy-bottun-maxquerystring.md)を参照してください。

### 横断検索でサイト名を検索できるように設定する

「テーブルの管理：検索：フルテキストの設定：パンくずリストを含める」を使うと、横断検索でサイト名を検索できるようになります。

## 制限事項
1. 「[情報公開機能](../../managers-guide/manage-table/publish/table-management-publish.md)」利用時は、パンくずリストは使用できません。
