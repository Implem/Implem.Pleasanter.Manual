# 用語と表記

同じものを指す言葉が揺れると、読み手が別のものだと受け取ります。ここに挙げるものは**過去に実際に揺れて直したもの**です。

## 製品とサービスの名前

| 正 | 誤りやすい例 |
| :--- | :--- |
| プリザンター（日本語版の本文） | プリザンダー |
| Pleasanter（英語版の本文） | Plesanter, Pleisanter, Pleasnater, Pleasaner, Presenter, Prizanter, Prisanter, Prezenter |
| CodeDefiner | CodeDifiner, CodeDefine |
| Pleasanter Extensions | Pleasanter Extentions |
| Enterprise Edition | Enterpise, Enterpisee |

### Pleasanter.net の大小文字には規則があります

| 書き方 | どんなとき |
| :--- | :--- |
| `pleasanter.net` | **アドレスの一部**のとき（`https://pleasanter.net/fs/...`、ディレクトリ名 `FAQ/pleasanter.net/`） |
| `Pleasanter.net` | **クラウドサービスを指す固有名詞**のとき |

## 他社の製品名

| 正 | 誤りやすい例 |
| :--- | :--- |
| PostgreSQL | PostgresSQL |
| SQL Server | SQLServer（**パラメータの値や環境変数名としての `SQLServer` はそのまま**） |
| SQL Server Management Studio | SQLServer Management Studio |
| JavaScript | Java Script |
| Windows | Winodws, Windowos |
| ActiveDirectory | ActiveDirecotry |
| Rocket.Chat | Rocket. Chat |

> [!warning]
> **設定ファイルの値・環境変数名・ファイル名は、綴りが「誤り」に見えても直さないでください。**
> 例: `"Dbms": "SQLServer"`、`Implem_Pleasanter_Rds_SQLServer_UserConnectionString`、`table-management-updator.md`。
> 直すと動かなくなったり、URL が変わったりします。

## 画面の項目名

**画面に出ている文字をそのまま書きます。**マニュアル側で言い換えないでください。

- 日本語版は日本語の画面、英語版は英語の画面に合わせます
- 迷ったら、実際の画面かエクスポートしたファイルで確かめてください
- 例: グループのエクスポートで出る CSV の列名は `Members are administrators` です。マニュアル側で `Member is a Manager` のように書き換えると、実物と食い違います

## 表記の揺れで過去に直したもの

| 正 | 誤 |
| :--- | :--- |
| リマインダー | リマインダ |
| パーツ（画面部品） | パース（※ 解析の意味の「パース」は正しい） |
| 除数（割る数） | 序数 |
| 適用されます | 適応されます |
| 英小文字 | 英子文字 |

## 英語版で気をつけるもの

- **アポストロフィ** … 本文では `'`（`Pleasanter's`）。**front matter の `title: '…'` の中だけは `''` と二重に書く**のが YAML の正しい書き方です（`title: 'Pleasanter''s DB'` → `Pleasanter's DB` と表示されます）
- **全角文字の混入** … `Ｍanagement` のように、全角の英字が紛れていたことがあります

## 直すときの注意

**短い誤字は、正しい語の一部でもあります。**一括置換をしないでください。

| 誤字 | これを含む正しい語 |
| :--- | :--- |
| `cur` | `curl`, `current` |
| `serve` | `server` |
| `Of` | `Off`, `Offset` |
| `Docke` | `Docker` |
| `Studi` | `Studio` |

必ず前後を見て、1 件ずつ直してください。
