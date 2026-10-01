# front matterリファレンス

Markdownファイルの先頭に `---` で囲んで置く、ページのメタ情報の一覧です。

**実際の書き方と、よく使うキーの意味**は[各ファイルの構造](file-structure.md)にあります。ここは「**テーマが解釈できるキーの一覧**」で、迷ったときに引くためのものです。本文の記法は[本文の記法](markup-guide.md)を参照してください。

> [!note]
> ここに挙げたキーの多くは、**PUM では使っていません。**使われている数を添えてあります（日本語版 / 英語版、2026-09 時点）。新しいキーを使い始める前に、既存ページとの見え方の統一を決めてください。

## 通常のページで使っているもの

| キー | 使用数 | 役割 |
| :--- | ---: | :--- |
| `title` | 1365 / 1273 | ページの題名。`<title>`と左サイドナビに使われる**必須項目** |
| `status` | 1263 / 1172 | `new`（新規）・`deprecated`（非推奨）のバッジ。**空文字なら非表示**で、ほとんどが空 |
| `hide` | 4 / 3 | 要素を隠す。下の表を参照 |
| `keywords` | 1 / 1 | サイト内検索に拾わせたい語 |

`category` `order` `parts` `urlstring` `shortname` `translationKey` は**旧CMSからの移行で持ち込まれたもの**で、現行のビルドでは使われていません（[各ファイルの構造](file-structure.md)）。

### hide で隠せるもの

```yaml
hide:
  - navigation   # 左サイドナビ
  - toc          # 右の目次
  - path         # パンくずリスト
  - feedback     # フィードバックの欄
  - tags         # タグの欄
```

## 更新情報（ブログ）のページで使うもの

`ja/docs/update-info/posts/` 配下の記事だけが使います。**通常のページでは使いません。**

| キー | 使用数 | 役割 |
| :--- | ---: | :--- |
| `date` | 236 / 232 | 公開日・更新日 |
| `draft` | 236 / 232 | `true` で本番のビルドから除外 |
| `categories` | 236 / 232 | 記事の分類 |
| `authors` | 1 / 0 | `.authors.yml` で定義した書き手 |

```yaml
---
date:
  created: 2026-05-26
  updated: 2026-05-26
draft: false
categories:
  - プリザンター
---
```

## 使えるが、PUM では使っていないもの

いずれも**使用数 0** です。使い始める場合は、サイト全体の見え方に関わるため先に相談してください。

| キー | 役割 | 必要なもの |
| :--- | :--- | :--- |
| `description` | 検索エンジン・OGP 用の説明文 | — |
| `icon` | 題名の横に出すアイコン | テーマの `navigation.icons` |
| `tags` | タグ付け | `tags` プラグイン |
| `search` | 検索の重み付け（`boost`）・除外（`exclude`） | `search` プラグイン |
| `template` | ページ単位でテンプレートを変える | `custom_dir: overrides` |
| `comments` | コメント欄 | 外部サービスとの統合 |
| `pin` `slug` `readtime` `links` | ブログ記事の固定・URL・読了時間・関連リンク | `blog` プラグイン |

## 関連

- [各ファイルの構造](file-structure.md) — front matterの実例と、ファイルの組み立て方
- [本文の記法](markup-guide.md) — 本文で使う記法
- [YAMLマニュアル](yaml-howto.md) — `.nav.yml` の書き方
