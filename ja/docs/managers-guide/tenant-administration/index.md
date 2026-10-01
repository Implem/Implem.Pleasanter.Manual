---
title: テナント管理機能
category: テナント管理機能
order: '10'
status: ''
parts: ''
urlstring: tenant
translationKey: tenant
shortname: テナントの管理,テナント
created: 2019-04-30
updated: 2026-03-10
---

## テナントとは

サイト、組織、グループ、ユーザなど全てを含む入れ物です。

## テナントの管理

以下の操作でテナントの設定を変更することが可能です。この操作はテナント管理者権限が必要です。

![テナントの管理画面](https://pleasanter.org/files/images/ja/managers-guide/tenant-administration/assets/0a5f92ff53ad4544bd0e2739f2523080.png)

1.  「管理」メニューを開き「テナントの管理」をクリックしてください。
1.  下表の必要事項を入力してください。

    | 項目名                                 | 説明                                                                                       | 設定方法                                                                                                                                                                                                                                                               |
    | :------------------------------------- | :----------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | タイトル                               | 画面左上に表示されるテナントのタイトル                                                     | 任意のタイトルを入力                                                                                                                                                                                                                                                   |
    | ロゴタイプ                             | 画面左上に表示されるテナントのロゴ                                                         | 表示形式を画像のみ/画像とテキストを指定                                                                                                                                                                                                                                |
    | ダッシュボード                         | トップ画面として設定するダッシュボード                                                     | 作成済みダッシュボードから選択                                                                                                                                                                                                                                         |
    | テーマ                                 | テナントで適用するテーマ                                                                   | [ユーザインターフェースのテーマ](../user-administration/user-management-theme.md)を選択                                                                                                                                                                                |
    | 言語                                   | テナントで適用する言語                                                                     | 言語をドロップダウンから選択                                                                                                                                                                                                                                           |
    | タイムゾーン                           | テナントで適用するタイムゾーン                                                             | タイムゾーンをドロップダウンから選択                                                                                                                                                                                                                                   |
    | 全てのユーザのアクセス許可を使用しない | 全てのユーザのアクセス許可の使用を禁止                                                     | 複数の取引先と共有しているようなケースで「全てのユーザのアクセス許可」を利用したくない場合にはチェック                                                                                                                                                                 |
    | APIを無効化                            | API機能                                                                                    | チェックすると該当テナントでAPI機能が使用不可になる                                                                                                                                                                                                                    |
    | Extensions APIを許可する               | 拡張機能テーブル（Extensionsテーブル）の利用許可                                           | チェックすると[Pleasanter Code Assist](../../products-info/pleasanter-extensions/pleasanter-code-assist/pleasanter-code-assist-create-workfolder.md)の拡張機能テーブル（Extensionsテーブル）機能が利用可能になる。このチェックボックスは特権ユーザでログイン時のみ表示 |
    | スタートガイドを使用しない             | チェックするとナビゲーションメニューの「[ユーザ](../user-administration/index.md)」以下に「スタートガイドを表示」を表示しない | チェックする・しないを切り替える                                                                                                                                                                                                                                       |
    | ロゴ画像(ファイル)                     | テナントのロゴとして掲載する画像ファイル                                                   | 任意の画像ファイルをアップロード                                                                                                                                                                                                                                       |
    | HTMLタイトル(トップ)                   | サイトトップを表示した際のHTMLタイトル                                                     | 任意のタイトルを入力                                                                                                                                                                                                                                                   |
    | HTMLタイトル(サイト)                   | サイトを表示した際のHTMLタイトル                                                           | 任意のタイトルを入力                                                                                                                                                                                                                                                   |
    | HTMLタイトル(レコード)                 | サイトトップを表示した際のHTMLタイトル                                                     | 任意のタイトルを入力                                                                                                                                                                                                                                                   |
    | \[ProductName\]                        | 製品名（プリザンター）を表示                                                               |                                                                                                                                                                                                                                                                        |
    | \[TenantTitle\]                        | テナントのタイトルを表示                                                                   |                                                                                                                                                                                                                                                                        |
    | \[SiteTitle\]                          | サイトのタイトルを表示                                                                     |                                                                                                                                                                                                                                                                        |
    | \[RecordTitle\]                        | レコードのタイトルを表示                                                                   |                                                                                                                                                                                                                                                                        |
    | \[Action\]                             | 画面表示時のアクション名を表示(例：一覧、新規作成、編集、ガントチャート等)                 |                                                                                                                                                                                                                                                                        |
    | トップのスタイル                       | サイトトップを表示した際のスタイル                                                         | 任意のCSSを入力                                                                                                                                                                                                                                                        |
    | トップのスクリプト                     | サイトトップを表示した際に実行する任意のスクリプト                                         | 任意のスクリプトを入力                                                                                                                                                                                                                                                 |
    | LDAP同期                               | ボタン押下によりLDAP同期を実行する                                                         | [BackgroundService.json](../../setup/parameters/background-service-json.md)でSyncByLdapをtrueにした場合にボタンが表示される。                                                                                                                                          |

1.  「更新」ボタンをクリックしてください。

## ダッシュボード

作成した[ダッシュボード](../../users-guide/dashboard/dashboard-add-parts.md)をトップ画面として設定します。

### 本来のトップ画面の表示方法

[ダッシュボード](../../users-guide/dashboard/dashboard-add-parts.md)をトップ画面に設定後、本来のトップ画面を表示したい場合は下記の方法で表示してください。  

1.  サイトIDに0を設定した[クイックアクセス](../../users-guide/dashboard/dashboard-quickaccess.md)パーツを追加。
1.  URLを直接指定。`http://{サーバ名}/items/0/index` [^1]

[^1]:
    `{サーバ名}`の部分は、適宜、環境に合わせて編集してください。  
    Pleasanter.netの場合は以下の形式になります。  
　　`https://pleasanter.net/fs/items/0/index`

### Locations.jsonとの同時設定

[ダッシュボード](../../users-guide/dashboard/dashboard-add-parts.md)をトップ画面に設定した場合、[Locations.json](../../setup/parameters/locations-json.md)の設定内容は無視されます。

## 対応バージョン

| 対応バージョン | 内容                                               |
| :------------- | :------------------------------------------------- |
| 1.3.19.0 以降  | LDAP同期機能を追加                                 |
| 1.4.16.0 以降  | 「Extensions APIを許可する」チェックボックスを追加 |

## 関連情報

-   [テナント管理機能：ロゴ、タイトル、ロゴ画像](tenant-logo.md)
-   [テナント管理機能：HTMLタイトル](tenant-htmltitle.md)
-   [テナント管理機能：バックグラウンドサーバスクリプト](background-server-script.md)
-   [ユーザ管理機能：ユーザインターフェースのテーマをカスタマイズ](../user-administration/user-management-theme.md)
-   [Pleasanter Code Assist：コマンドによる作業フォルダ作成](../../products-info/pleasanter-extensions/pleasanter-code-assist/pleasanter-code-assist-create-workfolder.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：ユーザ](../manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-users.md)
-   [パラメータ設定：BackgroundService.json](../../setup/parameters/background-service-json.md)
-   [ダッシュボード機能：パーツの追加](../../users-guide/dashboard/dashboard-add-parts.md)
-   [ダッシュボード機能：パーツの追加：クイックアクセス](../../users-guide/dashboard/dashboard-quickaccess.md)
-   [パラメータ設定：Locations.json](../../setup/parameters/locations-json.md)
