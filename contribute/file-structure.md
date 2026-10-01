# 各ファイルの構造

PUMを構成するMarkdownファイル1つ1つが、どのような要素でできているかを学びます。ディレクトリ全体の構成については、先に[プリザンターユーザマニュアルの構造](pum-structure.md)を読んでおいてください。

## 1ディレクトリの中身

1つのカテゴリディレクトリは、おおむね以下のファイル・フォルダで構成されています。

```
users-guide/table/record-authoring/create-records/
├── .nav.yml                          ナビゲーション設定
├── index.md                          このカテゴリの入口ページ
├── table-record-new.md               個別ページ
├── table-record-import.md            個別ページ
├── table-record-import-and-link.md   個別ページ
└── assets/                           このディレクトリのページが使う画像
```

`.nav.yml`と`index.md`の役割は[プリザンターユーザマニュアルの構造](pum-structure.md)を参照してください。

## ファイル名

ページのファイル名は、日本語の内容であっても**英語の小文字とハイフン**（kebab-case）で付けます。

``` text
table-record-import-and-link.md
```

既存のファイルは、旧CMSからの移行時に`urlstring`（後述）がそのままファイル名になったものが多く、内容から見て少し長めの名前もあります。新規ページでも、既存の命名に揃えて構いません。

## front matter（ファイル先頭のメタ情報）

ファイルの先頭には、`---`で囲んだYAML形式のfront matterを置きます。既存ページには、旧CMSから移行した項目が残っていることがあります。

``` md
---
title: レコードのインポートとマスタデータのリンク
category: テーブル機能
order: '202'
status: ''
parts: ''
urlstring: table-record-import-and-link
translationKey: table-record-import-and-link
shortname: インポート,リンク
---
```

| キー | 役割 |
| :--- | :--- |
| `title` | ページタイトル。`<title>`タグとナビゲーション表示に使われる**必須項目** |
| `category` `order` `parts` `urlstring` `shortname` | 旧CMSからの移行時に持ち込まれた項目。現行のMkDocsビルドの表示・挙動には使われていません。新規ページでは付けなくて構いません |
| `translationKey` | 旧CMSでのページ対応付けに使われていたIDの名残。現行ビルドでは参照されていません。言語切替と`hreflang`は、**両言語で同じパスにページがあるか**で相手を決めています（#190。[日本語版と英語版](translations.md)を参照） |
| `status` | 値を入れると`new`（新規作成）・`deprecated`（非推奨）のバッジを表示できます（空文字なら非表示） |
| `hide` | `navigation`・`toc`などを指定すると、左ナビゲーションやページ内目次を非表示にできます |

index.mdのようなカテゴリの入口ページは、`title`だけを持つ、より単純なfront matterになっていることが多いです。

``` md
---
title: アクセス制御
---
```

front matterで使える項目の一覧は[front matterリファレンス](markdown-howto.md)を参照してください。

> [!note]
> `category` `order` `parts` `urlstring` `shortname`のような移行時の名残の項目は、既存ページを編集するときに**消す必要はありません**。新規ページで新たに付ける必要もない、という意味です。

## 本文の構造

本文は、多くのページで次のような構成を取っています。

1. `#`（H1見出し）は本文には置かない（front matterの`title`がページタイトルの役割を兼ねる）
1. `## 概要`から書き始め、そのページで説明する内容を要約する
1. 以降は`##`・`###`で見出しを分けて説明する

カテゴリの入口ページ（`index.md`）では、「概要」の直後に配下ページへのカードリンク一覧を置くのが定型です。

``` md
## 概要

本カテゴリは以下の内容を含みます。

<div class="grid cards" markdown>

-   [アクセス制御の概要](access-controls.md)
-   [レコードのアクセス制御（レコードの編集）](table-record-access-control.md)

</div>
```

## 画像

画像の実体はこのリポジトリに含まれていません（別のストレージで管理しています）。Markdown上は、ページと同じ階層の`assets/`フォルダへの**相対参照**で記述します。

``` md
![顧客管理（親テーブル）のエクセルデータの例](assets/70e23bda75be4c668322cb58ae4b6bbe.png)
```

ファイル名はGUID（32桁の英数字）です。画像の追加・差し替えについては、このガイドの対象外です。ISSUEでお知らせください。

## ページ間のリンク

同じ言語プロジェクト内の他ページへは、リンク元のファイルからの相対パスで、Markdownファイルの拡張子（`.md`）を含めてリンクします。

``` md
[インポート](../../../../managers-guide/department-administration/dept-import.md)
```

## 表・箇条書き

表はパイプ区切り（`|`）で記述します。番号付きリストは、見た目の連番に関わらず**すべて`1.`で書いてください**（`markdownlint`のMD029ルールに合わせたもので、ビルド後は自動的に連番で表示されます）。

``` md
1. 手順1
1. 手順2
1. 手順3
```

## 保存前の確認

保存前に、Visual Studio Codeの`markdownlint`拡張機能が示す警告に目を通してください。セットアップ方法は[Visual Studio Codeのセットアップ](setup-vscode.md)を参照してください。
