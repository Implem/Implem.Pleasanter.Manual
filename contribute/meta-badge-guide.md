# メタバッジ：セットアップと使用方法

メタバッジは、ドキュメントページのパラメータや機能の説明に
対応バージョン・試験的機能・デフォルト値などの属性を示すバッジを埋め込む仕組みです。
MkDocs のフック機能を使い、追加ライブラリなしで動作します。

バッジのデザインは Material for MkDocs 本家の `mdx-badge` に準拠しています。
カラーはテーマの accent 色（`--md-accent-fg-color`）に追従し、
型の区別はアイコンの形のみで行います。

---

## セットアップ

### 1. ファイルの配置

以下の 2 ファイルをプロジェクトに配置します。

```
プロジェクトルート/
├── docs/
│   ├── hooks/
│   │   └── main.py          ← フック本体
│   └── stylesheets/
│       └── extra.css        ← バッジスタイル
└── mkdocs.yml
```

### 2. mkdocs.yml への追記

`hooks:` と `extra_css:` にそれぞれ追記します。

```yaml
hooks:
  - docs/hooks/main.py

extra_css:
  - stylesheets/extra.css
```

### 3. 依存パッケージの確認

`main.py` は `material` パッケージの SVG アイコンファイルを直接読み込みます。
`mkdocs-material`（または `mkdocs-materialx`）がインストール済みであれば追加インストールは不要です。

```bash
pip show mkdocs-material
```

---

## 使用方法

### 基本構文

Markdown ファイルの任意の行に HTML コメントとして記述します。

```markdown
<!-- meta フラグ1 フラグ2 ... -->
```

記法の決まりは 4 つです。

-   **`<!-- meta` のあとの空白と、`-->` の前の空白まで含めて一致させます。**
    `<!--meta experimental-->` のように空白を詰めると展開されず、コメントのまま残ります
-   **1 行で書きます。** 途中で改行したものは展開されません
-   フラグはスペース区切りで並べます。**並べる順序は出来上がりに影響しません**（順序はマクロ側で固定）
-   **認識されないフラグだけを書くと、バッジのない空の段落が出ます。**
    なお `<!-- meta -->` のように中身が空のものは展開されず、コメントのまま残ります

### バリエーション（全 12 種）

値を取るフラグは 2 つです。値は `"` か `'` で囲みます。

| フラグ | アイコン | バッジに出る文字 | 説明 |
|--------|---------|------------------|------|
| `version="x.x.x.x"` | タグ | 指定した値 | 対応バージョン |
| `default="値"` | 歯車 | 指定した値 | デフォルト値 |

残りの 10 は、書くだけで有効になるフラグです。

| フラグ | アイコン | バッジに出る文字 | 説明 |
|--------|---------|------------------|------|
| `default_none` | 歯車 | （なし） | デフォルト値なし |
| `default_computed` | 歯車 | `computed` | デフォルト値は自動計算 |
| `experimental` | フラスコ | （なし） | 試験的機能 |
| `required` | アラート | （なし） | 必須値 |
| `feature` | トグルスイッチ | （なし） | オプション機能 |
| `plugin` | フロッピー | （なし） | プラグイン |
| `extension` | Markdown | （なし） | Markdown 拡張 |
| `customization` | ブラシ | （なし） | カスタマイズ |
| `multiple` | 受信トレイ | （なし） | 複数インスタンス対応 |
| `metadata` | リストボックス | （なし） | メタデータプロパティ |

**文字が出るのは `version` `default` `default_computed` の 3 つだけ**で、ほかはアイコンだけのバッジになります。

### 出来上がりの並び順

書いた順序ではなく、次の順に並びます。

`version` → `experimental` → `default` → `default_none` → `default_computed` → `required` →
`feature` → `plugin` → `extension` → `customization` → `multiple` → `metadata`

### 値の書き方で気をつけること

-   **引用符を省くと展開されません。** `<!-- meta version=1.5.4.0 -->` はバッジが出ず、
    エラーにもならないので気づきにくいです
-   **値の中にフラグ名と同じ語を書くと、余分なバッジが出ます。** マクロはフラグを文字列として
    探すためです。`default="feature"` は歯車（feature）とトグルスイッチの 2 個になります
-   `default="値"` `default_none` `default_computed` は**排他ではありません。**
    3 つ並べると歯車のバッジが 3 個出ます

### 記述例

12 種を 1 つずつ書いた例です。

```markdown
<!-- meta version="1.4.3.0" -->

<!-- meta default="false" -->

<!-- meta default_none -->

<!-- meta default_computed -->

<!-- meta experimental -->

<!-- meta required -->

<!-- meta feature -->

<!-- meta plugin -->

<!-- meta extension -->

<!-- meta customization -->

<!-- meta multiple -->

<!-- meta metadata -->
```

組み合わせた例です。

```markdown
<!-- meta version="1.4.3.0" experimental -->

<!-- meta version="1.4.3.0" default="false" -->

<!-- meta version="1.4.3.0" experimental default="false" -->

<!-- meta plugin multiple -->
```

### ページ内での配置

パラメータ名の見出し直下に置くことを推奨します。

```markdown
## DisableAllUserCreation

<!-- meta version="1.3.0.0" default="false" -->

`true` を設定すると、管理者を含むすべてのユーザーによる
ユーザー作成を無効にします。
```

バッジは `<p class="mdx-badge-block">` という**段落として出力される**ため、
文中に混ぜて使うことはできません。行を分けて書きます。

---

## カラーの仕組み

バッジの色は `extra.css` で明示的に指定せず、
Material for MkDocs テーマが設定する CSS カスタムプロパティに任せています。

| CSS 変数 | 用途 |
|---------|------|
| `--md-accent-fg-color` | アイコン色 |
| `--md-accent-fg-color--transparent` | アイコン背景色・テキスト枠色 |
| `--md-default-fg-color` | テキスト色 |

Pleasanter ドキュメントの `mkdocs.yml` では `accent: indigo`（ライトモード）・
`accent: cyan`（ダークモード）を設定しているため、
モード切り替えに合わせてバッジの色が自動で変わります。

---

## トラブルシューティング

### 起動時に `FileNotFoundError` が出る

`main.py` が Material パッケージの SVG ファイルを読み込めていません。
以下を PowerShell で実行してアイコンファイルの場所を確認します。

```powershell
python -c "import material, os; print(os.path.join(os.path.dirname(material.__file__), 'templates', '.icons', 'material'))"
```

出力されたパスに `tag-outline.svg`、`flask-outline.svg`、`cog.svg` が存在するか確認します。

```powershell
Get-ChildItem "<上記のパス>" -Filter "*tag*"
```

ファイル名が異なる場合は、`main.py` の `_ICONS` 辞書内のパス文字列を実際のファイル名に合わせます。

### バッジが表示されずコメントがそのまま残る

`mkdocs.yml` の `hooks:` セクションを確認します。

```yaml
hooks:
  - docs/hooks/main.py   # プロジェクトルートからの相対パス
```

`mkdocs serve` を Ctrl+C で停止してから再起動します。
`__pycache__` が残っている場合は削除します。

```powershell
Remove-Item -Recurse -Force docs\hooks\__pycache__
```

### バッジは出るがアイコンが表示されない

開発者ツールで `<span class="mdx-badge__icon">` の中身を確認します。
`:material-tag-outline:` のような文字列が残っている場合は、
古いバージョンの `main.py` が読み込まれています。
`__pycache__` を削除して再起動します。
