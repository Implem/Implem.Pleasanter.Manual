# YAMLマニュアル

プリザンターユーザマニュアルでは、2つの目的でYAMLファイルを使っています。

-   プロジェクト設定 … 各言語の直下にある `mkdocs.yml`
-   ナビゲーション構築 … 各ディレクトリに置く `.nav.yml`

それぞれが**何を決めているか**は[プリザンターユーザマニュアルの構造](pum-structure.md)を参照してください。ここでは**書き方**を扱います。

## プロジェクト設定（mkdocs.yml）

`ja/mkdocs.yml` と `en/mkdocs.yml` の 2 つがあり、テーマ・プラグイン・拡張の設定が入っています。

> [!warning]
> **ページを足す・直すだけなら、`mkdocs.yml` を触る必要はありません。**ここを変えるとサイト全体の挙動が変わります。変更が要ると思ったら、先に issue で相談してください。

## ナビゲーション構築（.nav.yml）

各ディレクトリに置き、そのディレクトリの**表示名**と**並び順**を決めます。プラグインは `mkdocs-awesome-nav` です。

```yaml
title: ユーザガイド

nav:
  - index.md
  - useful-function.md
  - hands-on
  - custom-apps
```

| キー | 役割 |
| :--- | :--- |
| `title` | 左サイドナビでの、**このディレクトリ自身**の表示名 |
| `nav` | 配下のページ・ディレクトリを**並べたい順に**書く |

`nav` に書けるのは、ファイル名（`useful-function.md`）とディレクトリ名（`hands-on`）です。

### 表示名を変える

`表示名: パス` の形で書くと、左サイドナビでの表示名を変えられます。

```yaml
nav:
  - index.md
  - 一覧: grid
  - フィルタ: filter
  - $ps.JSON: ps-json
```

> [!warning]
> **表示名を書かないと、ディレクトリ名から自動で作られます**（ハイフンを空白に、先頭だけ大文字）。`grid` は `Grid`、`ps-json` は `Ps json` になります。`index.md` の `title` は**使われません**。日本語の表示名にしたいときは、必ずここに書いてください。

### グループにまとめる

項目が多いディレクトリでは、見出しでまとめられます。

```yaml
nav:
  - index.md
  - 日付/時刻:
    - formula-function-date.md
    - formula-function-day.md
  - 文字列操作:
    - formula-function-left.md
```

### 残りをまとめて出す

`"*"` と書くと、`nav` に挙げていないファイルがそこへ並びます。

```yaml
nav:
  - index.md
  - よく使うもの.md
  - "*"
```

## つまずきやすいところ

### `nav:` を書き忘れる

```yaml
title: ユーザガイド
  - index.md        # ← nav: が無い
```

**エラーになりません。**項目が `title` の値に畳み込まれ、ナビだけが静かに壊れます。配信前の関門（`deploy-gate.mjs`）が検出します。

### 知らないキーを書く

使えるキーは次の 8 つだけです。

```
title, hide, flatten_single_child_sections, preserve_directory_names,
use_index_title, sort, ignore, nav, append_unmatched
```

**これ以外のキーは黙って捨てられます。**打ち間違えても気づけないので、関門で検出しています。

### 実在しないファイルを指す

ビルドのログに次が出ます。

```
awesome-nav: The nav item '...' doesn't match any files or directories
```

**この警告は既知ではありません。必ず直してください。**放置すると、そのページは左のメニューから辿り着けなくなります（#229）。

### `nav` に書き忘れる

**`nav` に挙げていないファイルは、ナビから外れます。**このとき警告は出ません。ページを足したら、`.nav.yml` への追記を忘れないでください（`"*"` を使っているディレクトリを除く）。

## 関連

- [プリザンターユーザマニュアルの構造](pum-structure.md) — `.nav.yml` と `index.md` の役割
- [各ファイルの構造](file-structure.md) — front matter の書き方
- [受け入れの基準](review-and-ci.md) — 関門が何を見ているか
