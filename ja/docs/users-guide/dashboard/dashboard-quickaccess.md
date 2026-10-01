---
title: クイックアクセス
category: ダッシュボード機能
order: '20'
status: ''
parts: ''
urlstring: dashboard-quickaccess
translationKey: dashboard-quickaccess
shortname: ダッシュボード,パーツ,クイックアクセス
created: 2023-07-11
updated: 2025-04-25
---

## 概要

[ダッシュボード](dashboard-add-parts.md)にクイックアクセスを追加します。設定したサイト（[フォルダ](../folder/index.md)、[テーブル](../table/index.md)、[Wiki](../wiki/index.md)、[ダッシュボード](dashboard-add-parts.md)）へのリンクを一覧表示します。

## 設定手順

### 全般タブ

![クイックアクセスの設定画面の全般タブ](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/2916e7d69c9f41a5a05dc5c88e0094bf.png)

| 項目名               | 説明                                                                                                                                                                                                           |
| :------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| タイトル             | パーツの名称です。                                                                                                                                                                                             |
| タイトルを表示する   | タイトルを表示させる場合にチェックします。                                                                                                                                                                     |
| サイトID             | 表示したいサイトID、サイト名、サイトグループ名をカンマ区切りで入力します。入力した順番で表示します。トップ画面を指定する場合は0を入力してください。JSON形式での入力も可能です。                                |
| レイアウト           | クイックアクセスパーツのレイアウトを選択します。                                                                                                                                                               |
| 非同期読み込みしない | このチェックボックスにチェックを付けた場合、非同期読み込みの設定に関わらず非同期読み込みを行いません。非同期読み込みの設定については[ダッシュボード機能：パーツの追加](dashboard-add-parts.md)を参照ください。 |
| CSS                  | クイックアクセスパネルの要素にCSSを適用する場合に使用します。CSSクラス名を指定することで、各項目に任意のクラス名を指定し、[スタイル](../../developers-guide/style/index.md)を適用することができます。          |

### アクセス制御タブ

![クイックアクセスの設定画面のアクセス制御タブ](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/036b468061eb4c28901aa2aa651ca51a.png)

クイックアクセスに対する参照権限を設定します。参照権限のないユーザがダッシュボードを開いた場合、このパーツは非表示となります。

<a id="site-icon"></a>

## 表示内容

### サイトのアイコン

サイトIDで指定したサイトの種類に応じてサイト名の前に自動的にアイコンが表示されます。後述する[JSON形式によるサイトIDの指定](#site-icon-by-json)でアイコンを変更することができます。

| サイト種別       | アイコン                                         |
| :--------------- | :----------------------------------------------- |
| フォルダ         | ![「フォルダ」のアイコン](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/485198d6f34f4229872b9b55a087259d.png) |
| 期限付きテーブル | ![「期限付きテーブル」のアイコン](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/d6ccb0b6175d451e94d71af88a97b69d.png) |
| 記録テーブル     | ![「記録テーブル」のアイコン](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/a25dace04a264a1cbd139df50a30c7f1.png) |
| Wiki             | ![「Wiki」のアイコン](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/d8cb486a33e04a12aa6aba6d9a799273.png) |
| ダッシュボード   | ![「ダッシュボード」のアイコン](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/36f7ddc76ca84df782e3de1154304247.png) |

![サイト種別ごとのアイコンが付いたクイックアクセスの表示例](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/3088a408795c441aa13f90417eb6d6ca.png)

### レイアウト

レイアウトは縦方向、横方向のいずれかを選択します。

| レイアウト | 内容                                                                                     |
| :--------- | :--------------------------------------------------------------------------------------- |
| 縦方向     | サイトを縦に並べて表示します。パーツ自体の高さを狭くすると縦スクロールバーが表示します。 |
| 横方向     | サイトを横に並べて表示します。パーツ自体の幅を狭くすると折り返して表示します。           |

=== "レイアウト：縦方向"

    ![レイアウトが縦方向のクイックアクセスの表示例](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/4d5e9aac490249dabbc0ea9ae998fa8c.gif)

=== "レイアウト：横方向"

    ![レイアウトが横方向のクイックアクセスの表示例](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/aae2389f509546f6b4d2c5632a0daf46.gif)

<a id="site-icon-by-json"></a>

## JSON形式によるサイトID指定

JSON形式でサイトIDを指定することで、表示サイト毎にアイコンの変更やサイトごとにCSSを指定することができます。

| 項目名       | 説明                                                                                                                                                                                            |
| :----------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Id           | サイトIDを指定します。Urlが設定されていない場合は必須です。Urlが設定されている場合は無視されます                                                                                                |
| Url          | 任意のリンク先をURLで指定します。Idが設定されていない場合は必須です                                                                                                                             |
| Icon         | サイト名の前に表示するアイコンを設定します。指定文字は[Material Symbols(※1)](#material-symbols)を参照してください。Iconは省略可能です。省略時は[サイトのアイコン](#site-icon)の内容で表示します |
| Css          | cssのクラス名を設定します。あらかじめ[スタイル](../../developers-guide/style/index.md)タブや「拡張CSS」にて指定したクラスに対してスタイルを設定してください。Cssは省略可能です                  |
| Title        | ボタンのキャプションとして表示する文字列を設定します。Titleは省略可能です。省略時はサイトIDを指定した場合はサイト名、Urlを指定した場合はUrlが表示されます                                       |
| ViewMode     | 表示するサイトのViewModeを指定します。ViewModeは省略可能です。詳細は下記ViewModeの項目を参照してください                                                                                        |
| OpenInNewTab | リンク先を新しいタブで開く場合にtrueを設定します。OpenInNewTabは省略可能です。省略時はfalseとなります                                                                                           |

### ViewMode

ViewModeに指定可能な値は下記の通りです。

| 表示                 | ViewMode   |
| :------------------- | :--------- |
| 一覧                 | Index      |
| カレンダー           | Calendar   |
| クロス集計           | Crosstab   |
| ガントチャート       | Gantt      |
| バーンダウンチャート | Burndown   |
| 時系列チャート       | Timeseries |
| 分析チャート         | Analy      |
| カンバン             | Kamban     |
| 画像ライブラリ       | Imagelib   |

### 設定例

１つのサイトに対し[カンバン](../table/record-authoring/data-visualize/table-kanban-chart.md)で開くボタンと、[カレンダー](dashboard-calendar.md)で開くボタンを追加する例です。また、どちらも「新しいタブで開く」設定としています。

``` json linenums="1"
[
    {
        "Id": 123,
        "Title": "WBS(カンバン)",
        "ViewMode": "Kamban",
        "OpenInNewTab": true
    },
    {
        "Id": 123,
        "Title": "WBS(カレンダー)",
        "ViewMode": "Calendar",
        "OpenInNewTab": true
    }
]
```

![カンバンとカレンダーで開く2つのボタンを並べた表示例](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/1ae930f6910d404585aea15fe1ffe9a7.png)

サイトIDおよびCSSを以下のように設定した場合の表示結果は下記の通りです。

``` json linenums="1"
[
    {
        "Id": 123,
        "Icon": "check_circle",
        "Css": "bgcolorPink"
    },
    {
        "Id": 456,
        "Icon": "check_circle"
    },
    {
        "Id": 789,
        "Css": "bgcolorPink"
    }
]
```

``` css linenums="1"
.bgcolorPink {
      background-color: pink;
}
```

##### 表示結果

![アイコンと背景色のCSSを指定したクイックアクセスの表示結果](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/4263bee057b04e4282e8b6a41bcd0282.png)

<a id="material-symbols"></a>

### ※1 Material Symbolsからの指定文字検索方法

JSON形式によるサイトIDの指定においてIconに設定する文字は以下手順で確認してください。

1.  [Material Symbols](https://fonts.google.com/icons)のページを開く

    ![Material Symbols のアイコン一覧ページ](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/314622ec222b444eb3091c9cb4538c96.png)

1.  利用したいアイコンをクリックする

    ![Material Symbols で利用したいアイコンを選んだところ](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/4df30fc6a80e419d9b6663eedd48e414.png)

1.  画面右に表示する「Inserting the icon」欄のspanタグに囲まれた文字列をIconに設定する。

    ![画面右の「Inserting the icon」欄に表示されるspanタグの文字列](https://pleasanter.org/files/images/ja/users-guide/dashboard/assets/42db7ceb711b4d98a164d65219f0fcbc.png)

## 対応バージョン

| 対応バージョン | 内容                                                                 |
| :------------- | :------------------------------------------------------------------- |
| 1.4.10.0 以降  | JSON形式によるサイトID指定にUrl、Title、ViewMode、OpenInNewTabを追加 |

## 関連情報

-   [ダッシュボード機能：パーツの追加](dashboard-add-parts.md)
-   [フォルダ機能](../folder/index.md)
-   [テーブル機能](../table/index.md)
-   [Wiki機能](../wiki/index.md)
-   [開発者ガイド：スタイル](../../developers-guide/style/index.md)
-   [テーブル機能：レコードのカンバン表示](../table/record-authoring/data-visualize/table-kanban-chart.md)
-   [ダッシュボード機能：パーツの追加：カレンダー](dashboard-calendar.md)
-   [Material Symbols](https://fonts.google.com/icons)
