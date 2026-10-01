---
title: 拡張スタートガイド
category: 拡張機能
order: '0'
status: ''
parts: ''
urlstring: extended-startguide
translationKey: extended-startguide
shortname: 拡張スタートガイド
created: 2026-02-27
updated: 2026-03-10
---

## 概要

スタートガイドへのコンテンツ追加、コンテンツ削除等を行うための拡張機能です。

## 注意事項

1. パラメータ変更時は[パラメータ変更時の確認事項](../../setup/parameters/parameter-edit.md)を確認してください。

## 制限事項

1. 拡張スタートガイドのJSONファイルを更新した後は「プリザンターを再起動」するまで反映しません。
1. スタートガイドで使用する画像はImplem.Pleasanter\wwwroot\images\フォルダ内に配置してください。
1. 画像ファイル名の拡張子を省略することはできません。

## 設定方法

.\Pleasanter\App_Data\Parameters\ExtendedStartGuides\ 配下に以下の内容を含むJSONファイルを作成し、「アプリケーションを再起動」してください。JSONファイルの拡張子は必ずjsonにしてください。

ExtendedStartGuides配下はフォルダで階層化できます。この場合、ExtendedStartGuidesフォルダ配下の全てのJSONファイルが設定ファイルとして読み込まれます。

## パラメータリスト

JSONファイルに指定するパラメータは以下の通りです。

##### パラメータリスト

| パラメータ名 | 設定例 | 説明 |
|:----|:----|:----|
| Description | "この拡張スタートガイドは…を表示します" | 拡張スタートガイドの説明です。動作には影響しません。 |
| Disabled | false | trueの場合、拡張スタートガイドの設定は無効化されます。 |
| DeptIdList | [1,2,3] | 対象となる組織IDを配列形式で指定します。このパラメータは省略可能です。 |
| GroupIdList | [1,2,3] | 対象となるグループIDを配列形式で指定します。このパラメータは省略可能です。 |
| UserIdList | [1,2,3] | 対象となるユーザIDを配列形式で指定します。このパラメータは省略可能です。 |
| TargetId | "SgManual" | Actionで指定した操作をするときの操作対象IDを指定します。操作対象IDについては「TargetIdとして指定できるid属性値」を参考にしてください。 |
| Action | "Append" | 下記[Actionパラメータ](#Action)の説明を確認してください。 |
| StartGuides | [{…},{…},{…}] | 下記[StartGuidesパラメータ](#StartGuides)の説明を確認してください。 |

##### TargetIdとして指定できるid属性値

|機能解説<br>ユーザマニュアル|実践解説<br>アプリ作成ガイド|活用促進<br>お役立ちコンテンツ|機能拡張<br>Enterprise edition|安心運用<br>課題解決支援|
|:-:|:-:|:-:|:-:|:-:|
|SgManual|SgGoHandsOn|SgMaterials|SgExtensions|SgSupport|

![スタートガイドに並ぶ各項目](https://pleasanter.org/files/images/ja/developers-guide/extended-features/assets/c8033087332242f3b4965ba79a88ea6f.png)

<a id="Action"></a>

### Actionパラメータ  

スタートガイドの追加、削除などの操作を、[拡張ナビゲーションメニュー](extended-navigationmenus.md)と同じ書式で指定します。

| 変数 | 説明 |
|:----|:----|
| Append | TargetIdで指定したIDのスタートガイドの後ろにスタートガイドを追加します。 |
| Prepend | TargetIdで指定したIDのスタートガイドの前にスタートガイドを追加します。 |
| Remove | TargetIdで指定したIDのスタートガイドを削除します。 |
| Replace | TargetIdで指定したIDのスタートガイドを置換します。 |
| ReplaceAll | スタートガイドをすべて置換します。 |

<a id="StartGuides"></a>

### StartGuidesパラメータ

拡張するスタートガイドの定義を指定します。

| パラメータ名 | 設定例 | 説明 |
|:----|:----|:----|
| Id | "SgStartGuide" | 変更不可（スタートガイドのid属性の値を表します） |
| Text | "ヘルプはこちら" | リンクテキストを指定します。 |
| Url | "https://pleasanter.net" | リンク先のURLを指定します。 |
| ImgNameLight | "image.svg" | リンクテキストとともに表示する画像のファイル名を指定します。この画像は、テーマが「midnight」以外の場合に使用されます。<span class="pl-attention">※1</span> |
| ImgNameDark | "image-d.svg" | リンクテキストとともに表示する画像のファイル名を指定します。この画像は、テーマが「midnight」の場合に使用されます。<span class="pl-attention">※1</span>　<span class="pl-attention">※2</span> |
| Target | _blank | スタートガイドクリック時のターゲット属性を指定します。例の場合、遷移先の画面を別タブで表示します。 |
| Disabled | true | スタートガイドを無効化します。 |

<span class="pl-attention">※1</span>　ファイル名は拡張子を含めて指定してください。  
<span class="pl-attention">※2</span>　省略した場合、ImgNameLightと同じ画像が表示されます。

## サンプルコード

##### JSON（Append操作）

```json
{
    "Disabled": "false",
    "TargetId": "SgExtensions",
    "Action": "Append",
    "StartGuides": [
        {
            "Id": "sg-01-append",
            "Text": "テストガイド01",
            "Url": "https://pleasanter.net/",
            "ImgNameLight": "hayato2.png",
            "ImgNameDark": "hayato3.png",
            "Target": "_blank",
            "Disabled": "false"
        },
        {
            "Id": "sg-02-append",
            "Text": "テストガイド02",
            "Url": "https://pleasanter.org/ja/manual",
            "ImgNameLight": "hayato1.png",
            "ImgNameDark": "",
            "Target": "_blank",
            "Disabled": "false"
        },
        {
            "Id": "sg-03-append",
            "Text": "テストガイド03",
            "Url": "https://implem.co.jp/",
            "ImgNameLight": "",
            "ImgNameDark": "",
            "Target": "_blank",
            "Disabled": "false"
        },
        {
            "Id": "sg-04-append",
            "Text": "テストガイド04",
            "Url": "https://pleasanter.org/",
            "ImgNameLight": "",
            "ImgNameDark": "",
            "Target": "_blank",
            "Disabled": "true"
        }
    ]
}
```

## 関連情報

-   [パラメータ設定：パラメータ変更時の確認事項](../../setup/parameters/parameter-edit.md)
-   [開発者ガイド：拡張機能：拡張ナビゲーションメニュー](extended-navigationmenus.md)
