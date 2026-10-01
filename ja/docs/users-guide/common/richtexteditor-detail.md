---
title: リッチテキストエディタ：ツールの詳細
category: 共通機能
order: '2'
status: ''
parts: ''
urlstring: richtexteditor-detail
translationKey: richtexteditor-detail
shortname: 共通機能：リッチテキストエディタ：ツールの詳細
created: 2025-08-21
updated: 2026-08-12
---

[リッチテキストエディタ](richtexteditor.md)のツールについて詳細を解説します。

## このページのテーブルという用語について

このページ内のテーブルという用語は、リッチテキストエディタで作成できる表を意味しています。プリザンターのテーブルと混同しないでください。

## フォント

選択した文字列のフォントを、既定では16種類のフォントから選択できるように設定されています。ただし、これらのフォントがユーザ環境（OS）で使えることが条件となります。ここで選択できるフォントを変更する方法については、以下の「フォントとサイズの設定を変更する」を参照してください。

<details markdown="1">
<summary>見本を見る</summary>

![フォントを変えた見本](https://pleasanter.org/files/images/ja/users-guide/common/assets/1ce5d3ef18314596b74e41b973f4ee60.png)

</details>

## サイズ

選択した文字列の文字サイズを、既定では16種類のサイズから選択できます。

<details markdown="1">
<summary>見本を見る</summary>

![文字の大きさを変えた見本](https://pleasanter.org/files/images/ja/users-guide/common/assets/71e772442ce14a41bf2b5576f75aad22.png)

</details>

## フォントとサイズの設定を変更する

パラメータファイルTextEditorUI.jsonを書き換えることで、フォントとサイズを変更できます。この機能はオンプレミス環境でのみご利用いただけます。

<details markdown="1">
<summary>TextEditorUI.json（初期値）</summary>

```
{
    "RichTextEditor": {
        "DefaultFont": [
            "Meiryo",
            "Hiragino Kaku Gothic Pro",
            "Yu Gothic",
            "Helvetica Neue",
            "Helvetica",
            "Arial",
            "sans-serif"
        ],
        "FontList": [
            "游ゴシック",
            "BIZ UDPゴシック",
            "Noto Sans",
            "游明朝",
            "BIZ UDP明朝",
            "Noto Serif JP",
            "Arial",
            "Segoe UI",
            "Calibri",
            "Helvetica",
            "Impact",
            "Times New Roman",
            "ＭＳ ゴシック",
            "ＭＳ Ｐゴシック",
            "ＭＳ 明朝",
            "ＭＳ Ｐ明朝"
        ],
        "FontSize": [ 8, 9, 10, 11, 12, 14, 16, 18, 20, 22, 24, 26, 28, 36, 48, 72 ]
    }
}
```

各パラメータの意味や設定例は[TextEditorUI.json](../../setup/parameters/texteditorui-json.md)を確認してください。また、設定変更にあたっては[パラメータ変更時の確認事項](../../setup/parameters/parameter-edit.md)を必ず確認してください。
</details>

## 段落形式

カーソルを置いた段落に対して、9種類の段落形式（書式）を設定します。

<details markdown="1">
<summary>見本を見る</summary>

![段落形式を変えた見本](https://pleasanter.org/files/images/ja/users-guide/common/assets/56b5c9823b794082a294071ded8497cc.png)

</details>

## 文字列の装飾とテキストスタイル

選択した文字列に様々な装飾を施せます。

| 太字 | 下線 | イタリック | 取り消し線 | 下付き | 上付き | 文字色 | 文字の背景色 | テキストスタイル |
| :-: | :-: | :-: | :-: | :-: | :-: |:-: | :-: | :-: |
| ![「太字」のアイコン](https://pleasanter.org/files/images/ja/users-guide/common/assets/add0be19efb1450ba97e3806e216f63a.png) | ![「下線」のアイコン](https://pleasanter.org/files/images/ja/users-guide/common/assets/e979efc7898c4c609a4cfa4280020265.png) | ![「イタリック」のアイコン](https://pleasanter.org/files/images/ja/users-guide/common/assets/2deafd967567450d8de9dae11b1a33cb.png) | ![「取り消し線」のアイコン](https://pleasanter.org/files/images/ja/users-guide/common/assets/4ecb7fb19f0c41f9917fafa5a7ecfc30.png) | ![「下付き」のアイコン](https://pleasanter.org/files/images/ja/users-guide/common/assets/f9bb1743543047a28d234955e375440c.png) | ![「上付き」のアイコン](https://pleasanter.org/files/images/ja/users-guide/common/assets/220fefbbc1d94959939116f46e2400ba.png) | ![「文字色」のアイコン](https://pleasanter.org/files/images/ja/users-guide/common/assets/e3ce92d4a0c34e6ca1fb0ac6e2097ddc.png) | ![「文字の背景色」のアイコン](https://pleasanter.org/files/images/ja/users-guide/common/assets/43da13392be248ad996e3c5ffdb03dfa.png) | ![「テキストスタイル」のアイコン](https://pleasanter.org/files/images/ja/users-guide/common/assets/77152145d72d4714ac4f1dd51a876554.png) |

太字、下線、イタリック、取り消し線、下付き、上付き、文字色、文字の背景色の反映結果や、3種類のテキストスタイルの反映結果は見本をご覧ください。

<details markdown="1">
<summary>見本を見る</summary>

![文字列の装飾とテキストスタイルの見本](https://pleasanter.org/files/images/ja/users-guide/common/assets/d31b8090b30a4beba55bf468de724a65.png)

</details>

## 文字色、文字の背景色

文字列を選択後、文字色ボタン、文字の背景色ボタンをクリックするとカラーパレットが表示されます。

| 文字色| 文字の背景色 |
| :-: | :-: |
| ![カラーパレットを開く「文字色」ボタンのアイコン](https://pleasanter.org/files/images/ja/users-guide/common/assets/e3ce92d4a0c34e6ca1fb0ac6e2097ddc.png) | ![カラーパレットを開く「文字の背景色」ボタンのアイコン](https://pleasanter.org/files/images/ja/users-guide/common/assets/43da13392be248ad996e3c5ffdb03dfa.png) |

### カラーパレット

![文字色や文字の背景色を指定するカラーパレット](https://pleasanter.org/files/images/ja/users-guide/common/assets/4e6c8dae95d94a098daf9f4d9351ce33.png)

パレットから色を選択するか、16進カラーコードを入力することで文字色や、文字の背景色を指定できます。指定後、確認ボタンをクリックすると指定が反映されます。形式を削除ボタンをクリックするとデフォルトカラーに戻ります。

| 確認 | 形式を削除 |
| :-: | :-: |
| ![「確認」のアイコン](https://pleasanter.org/files/images/ja/users-guide/common/assets/ebb77b0c12b9439c996742f6c4c7ba10.png) | ![「形式を削除」のアイコン](https://pleasanter.org/files/images/ja/users-guide/common/assets/401caa1243af460883cb145a82641cb3.png) |

文字色と文字の背景色のデフォルトカラーは次の通りです。

| 対象 | デフォルトカラー|
| :-- | :-- |
| 文字色|#333333|
| 文字の背景色|#ffffff|

## ブロック表示

ブロック構造を可視化して、わかりやすく表示します。

| ブロック表示 |
| :-: |
| ![「ブロック表示」のアイコン](https://pleasanter.org/files/images/ja/users-guide/common/assets/271f587638a448ffbe872a18a687e3d2.png) |

<details markdown="1">
<summary>見本を見る</summary>

![ブロック表示を有効にした見本](https://pleasanter.org/files/images/ja/users-guide/common/assets/025ab9ac8ee34c398abf61fbbc8ac3b7.png)

</details>

## インデント

インデントを深くしたり、浅くしたりできます。

| インデント（右へ） | インデント（左へ） |
| :-: | :-: |
| ![「インデント（右へ）」のアイコン](https://pleasanter.org/files/images/ja/users-guide/common/assets/dd621a287fee401eb51df40eb4a04a07.png) | ![「インデント（左へ）」のアイコン](https://pleasanter.org/files/images/ja/users-guide/common/assets/cbf637e8f847494ca614a32641ed6f5d.png) |

<details markdown="1">
<summary>見本を見る</summary>

![インデントを付けた見本](https://pleasanter.org/files/images/ja/users-guide/common/assets/e68d9f5b9c8b48208b318a64880c0dda.png)

</details>

## ソート

カーソルを置いた段落の行揃えを変更するツールが表示されます。

| ソート |
| :-: |
| ![「ソート」のアイコン](https://pleasanter.org/files/images/ja/users-guide/common/assets/4468a40808cd4e04bbec97470b5fad1f.png) |

**左揃え**、**中央揃え**、**右揃え**、または**両端揃え**に変更可能です。両端揃えは単語間のスペース幅が自動調節されます。

| 左揃え | 中央揃え | 右揃え | 両端揃え |
| :-: | :-: | :-: | :-: |
| ![「左揃え」のアイコン](https://pleasanter.org/files/images/ja/users-guide/common/assets/ffdfbfcea2dd4f9ea475458340d88ecf.png) | ![「中央揃え」のアイコン](https://pleasanter.org/files/images/ja/users-guide/common/assets/a2c6e774dd43441fb4b04a8f6bbeb679.png) | ![「右揃え」のアイコン](https://pleasanter.org/files/images/ja/users-guide/common/assets/cf79a36ff3ca4331867e256d47b092ca.png) | ![「両端揃え」のアイコン](https://pleasanter.org/files/images/ja/users-guide/common/assets/3f3e5a62604c4beb8051c4645ba24d32.png) |

<details markdown="1">
<summary>見本を見る</summary>

![ソート（配置）を変えた見本](https://pleasanter.org/files/images/ja/users-guide/common/assets/acdbf24077fe406b8b6da247d705d755.png)

</details>

## 水平線を挿入

水平線を親ブロックの幅いっぱいに描画します。水平線の種類には**実線**、**ダッシュ**、**点線**が用意されています。ダッシュと点線の違いは、破線の長さと間隔です。点線の方が短く、狭い破線です。

| 水平線を挿入 |
| :-: |
| ![「水平線を挿入」のアイコン](https://pleasanter.org/files/images/ja/users-guide/common/assets/52219c592be84bb9b88539c787ea1636.png) |

<details markdown="1">
<summary>見本を見る</summary>

![水平線を挿入した見本](https://pleasanter.org/files/images/ja/users-guide/common/assets/914cc105575b4a0b89715003b59e09f9.png)

</details>

## リスト（箇条書き）

選択した行をリスト（箇条書き）に変更するツールが表示されます。

| リスト |
| :-: |
| ![「リスト」のアイコン](https://pleasanter.org/files/images/ja/users-guide/common/assets/5d3e3dbe264b4952adcdabd1e62c92af.png) |

**数値ブリット**（順序付き箇条書き）と**円形ブリット**（順序なし箇条書き）の2種類から選択できます。

| 数値ブリット | 円形ブリット |
| :-: | :-: |
| ![「数値ブリット」のアイコン](https://pleasanter.org/files/images/ja/users-guide/common/assets/4da4b689d76940f2a00ec7c557dc5d5a.png) | ![「円形ブリット」のアイコン](https://pleasanter.org/files/images/ja/users-guide/common/assets/8479f83b23774be7a181c1e910a6fdfa.png) |

リストにインデントを設定すると、3レベル目までは、行頭の数字や記号が変化します。4レベル目以降は3レベル目の数字や記号が使われます。アルファベット小文字のzの次はaa、zzの次はaaaと桁上がりします。

<details markdown="1">
<summary>見本を見る</summary>

![リスト（箇条書き）の見本](https://pleasanter.org/files/images/ja/users-guide/common/assets/b74da8546f5040a3873880c350ce29af.png)

</details>

## 行の高さ

行の高さをデフォルトの1.5から、**1**、**1.15**、**2**のいずれかに変更できます。

| 行の高さ |
| :-: |
| ![「行の高さ」のアイコン](https://pleasanter.org/files/images/ja/users-guide/common/assets/c97579c472fc4218a8820b8aec50ca62.png) |

<details markdown="1">
<summary>見本を見る</summary>

![行の高さを変えた見本](https://pleasanter.org/files/images/ja/users-guide/common/assets/50dade63bb814dc4a6963a4516094e17.png)

</details>

## テーブル（表）の作成

テーブルボタンをクリックすると、10列×10行までのテーブル（表）を簡便に作成できるメニューが表示されます。たとえば、6列×9行のテーブル（表）を作成するときは、次の状態でクリックします。

![テーブル（表）の大きさを選ぶメニュー。6列×9行を選んだ状態](https://pleasanter.org/files/images/ja/users-guide/common/assets/fb6576c660bb46d3b4ac3ef862bbaea1.png)

11列以上、11行以上のテーブル（表）を作成したい場合は、以下を参考に行や列を分割してください。

### セルの選択・複数のセルの選択

テーブル（表）内の任意のセルをクリックすると、セルを選択できます。選択されたセルは、ボーダー（境界線）が青くなります。

テーブル（表）内でクリック＆ドラッグすると、複数のセルを選択できます。Shiftキーを押しながら離れた2つのセルをクリックすることで、複数のセルを矩形選択することもできます。

### 既存のテーブル（表）の編集

作成したテーブル（表）のセルを選択すると、選択したセルの上と下に、2つのフローティングツールバーが表示されます。

#### テーブル（表）全体の設定

上側のフローティングツールバーでは、テーブル（表）全体に関わる設定を編集できます。

![テーブル（表）全体の設定を編集するフローティングツールバー](https://pleasanter.org/files/images/ja/users-guide/common/assets/184392146b324841b5f3c6d7989d8dfd.png)

| 名前 | 概要 |
| --- | ---- |
| 最小サイズ / 最大サイズ | テーブル（表）は、最初、最大サイズ（表示領域幅）で作成されます。最小サイズをクリックすると、テーブル（表）の幅がセル内のコンテンツサイズにフィッティングされます。 |
| 固定列幅 | 固定列幅をONにすると、現在の設定で列幅を固定します。**列幅の固定後、後述するセルの分割・結合を行っても、一度固定した列幅は変わりません。** |
| 表のヘッダ | テーブル（表）の先頭行の上にヘッダ（見出し行）を追加します。**ヘッダは通常の行とは別扱いであることに注意**してください。ヘッダ行にはグレーの背景色が設定されます。ヘッダ行と通常の行とのボーダー（境界線）は通常の境界線よりも一回り太く表示されます。 |
| 削除 | テーブル（表）全体を削除します。誤って削除してしまった場合は、ツールバーから元に戻すを選択してください。 |

#### 行・列・セルの編集

下側のフローティングツールバーでは、行、列、セルに関わる設定を編集できます。

![行・列・セルの設定を編集するフローティングツールバー](https://pleasanter.org/files/images/ja/users-guide/common/assets/ac599387c4504e6caddcc40984013eb3.png)

※上の画面は説明のため、すべてのボタンがアクティブになるよう合成した画面です。

| 名前 | 概要 |
| --- | --- |
| 上に行を挿入 | 選択したセルの上側に行を挿入します。 |
| 下に行を挿入 | 選択したセルの下側に行を挿入します。 |
| 左に列を挿入 | 選択したセルの左側に列を挿入します。 |
| 右に列を挿入 | 選択したセルの右側に列を挿入します。 |
| 行の削除 | 選択したセルを含む行を削除します。ヘッダ行にカーソルを置いた場合は、ヘッダ行が削除されます。 |
| 列を削除する  | 選択したセルを含む列を削除します。 |
| セルの結合 | 複数のセルを選択した状態でクリックすると、選択したセルを結合します。 |
| セルの分割－垂直分割 | 選択したセルを垂直分割します（2列になる）。複数のセルを分割することはできません。 |
| セルの分割－横分割   | 選択したセルを横分割します（2行になる）。複数のセルを分割することはできません。 |

## リンクの挿入画面

リンクボタンをクリックするとリンクの挿入画面が開きます。

| リンク |
| :-: |
| ![「リンク」のアイコン](https://pleasanter.org/files/images/ja/users-guide/common/assets/a46869cecefe4a238a56efd805e1005b.png) |

![リンクの挿入画面](https://pleasanter.org/files/images/ja/users-guide/common/assets/28e82b575cba4767bd69674984094cff.png)

| 名前 | 概要 |
| ---- | --- |
| インターネットアドレス | リンク先のURLを入力します。 |
| ブックマーク | 項目内の要素をブックマークしたり、既存のブックマークへのリンクを呼び出したりします。**タイトル**を適用した段落は自動的にブックマークされます。 |
| 画面のテキスト | Pleasanterの画面に表示されるテキストを入力します。 |
| 別ウィンドウで開く | 一覧画面では、「編集モードの切り替え」スイッチのON・OFFに関わらず、同じタブで開きます。編集画面では、「編集モードの切り替え」スイッチがOFFのとき、別のタブで開きます。 |
| 確認 | リンクの挿入を完了します。リンクの挿入をキャンセルするには、画面右上の「×」をクリックしてください。挿入したリンクの挙動を確認するときは、忘れずに「編集モードの切り替え」スイッチをOFFにしてください。 |

### 既存のリンクの編集

既存のリンクにカーソルを置くと、フローティングツールバーが表示されます。

![既存のリンクを編集するフローティングツールバー](https://pleasanter.org/files/images/ja/users-guide/common/assets/2b79621e0c0a43c08466e311c5c124df.png)

| 名前       | 概要                                               |
| ---------- | -------------------------------------------------- |
| 編集       | リンクの挿入画面が表示されます。                   |
| リンク解除 | 設定済みのリンクを解除します。                     |
| 削除       | リンクと、リンクが設定されたテキストを削除します。**誤って削除してしまった場合は、ツールバーから元に戻すを選択してください。** |

## 画像の挿入画面

画像ボタンをクリックすると画像の挿入画面が開きます。

| 画像 |
| :-: |
| ![「画像」のアイコン](https://pleasanter.org/files/images/ja/users-guide/common/assets/b3a9de2d954d49f7a7bcb86bb7d66519.png) |

![画像の挿入画面](https://pleasanter.org/files/images/ja/users-guide/common/assets/87930107d3d8496abf208d9e7706f235.png)

| 名前 | 概要 |
| ---- | ---- |
| ファイルの選択 | クリックすると、挿入する画像を選択するダイアログボックスが表示されます。 |
| ×                  | （「ファイルを選択」の右側の）「×」ボタンをクリックすると、選択を解除できます。                                                          |
| イメージアドレス   | 画像のアドレス（URL）を指定します。「ファイルの選択」で挿入する画像ファイルを選択した際は使用できません。                                                |
| 置換文字列         | 画像が表示されなかった場合の代替えテキストを指定できます。                                                                               |
| 横                 | 画像を表示するときの幅を指定できます。指定しない場合は、元の画像の幅が自動設定されます（auto）。                                         |
| 縦                 | 画像を表示するときの高さを指定できます。指定しない場合は、元の画像の幅が自動設定されます（auto）。                                       |
| の割合カスタマイズ | オンにした状態で、横（幅）または縦（高さ）のいずれか一方を指定し、他方をautoにすると、元の画像の縦横比を維持したまま、拡大・縮小します。 |
| 元に戻す           | 横（幅）、縦（高さ）の直前の変更を取り消します。                                                                                         |
| 説明付け           | オンにすると、画像に説明文を追加できます。この説明文は代替えテキストとは異なり、画像の直下に表示される説明文（キャプション）です。                   |
| 基本               | 画像を標準的なブロック要素として挿入します（左揃え）。画像の右側に回り込みは発生しません。                                               |
| 左                 | 画像を行内で左揃えにします。画像の後続要素が画像の右側へ回り込むように表示されます（フロート効果）。                                     |
| 中央               | 画像を標準的なブロック要素として挿入します（中央揃え）画像の左右に回り込みは発生しません。                                               |
| 右                 | 画像を行内で右揃えにします。画像の後続要素が画像の左側へ回り込むように表示されます（フロート効果）。                                     |
| 確認               | 画像の挿入を完了します。画像の挿入をキャンセルするには、画面右上の「×」ボタンをクリックしてください。                                    |

### 既存の画像の編集

挿入済みの画像を選択すると、フローティングツールバーが表示されます。

![既存の画像を編集するフローティングツールバー](https://pleasanter.org/files/images/ja/users-guide/common/assets/fb782c8f662f493d924d84bb8cf4db70.png)

| 名前         | 概要                                                                                                 |
| ------------ | ---------------------------------------------------------------------------------------------------- |
| 100%サイズ   | 選択した画像の幅を100％（表示領域幅いっぱい）に設定します。                                      |
| 75%サイズ    | 選択した画像の幅を（表示領域幅の）75％に設定します。                                             |
| 50%サイズ    | 選択した画像の幅を（表示領域幅の）50％に設定します。                                             |
| 自動サイズ   | 選択した画像の幅をautoに設定します。                                                                 |
| 左へ回転     | 選択した画像を反時計回りに90度回転します。                                                           |
| 右へ回転     | 選択した画像を時計回りに90度回転します。                                                             |
| 左右反転     | 選択した画像を左右反転します。                                                                       |
| 上下反転     | 選択した画像を上下反転します。                                                                       |
| ソート－基本 | 画像を標準的なブロック要素として挿入します（左揃え）。画像の右側に回り込みは発生しません。           |
| ソート－左   | 画像を行内で左揃えにします。画像の後続要素が画像の右側へ回り込むように表示されます（フロート効果）。 |
| ソート－中央 | 画像を標準的なブロック要素として挿入します（中央揃え）画像の左右に回り込みは発生しません。           |
| ソート－右   | 画像を行内で右揃えにします。画像の後続要素が画像の左側へ回り込むように表示されます（フロート効果）。 |
| 説明付け     | この説明文は代替えテキストとは異なり、画像の直下に表示される説明文（キャプション）です。             |
| 元に戻す     | 横（幅）、縦（高さ）の直前の変更を取り消します。                                                     |
| 編集         | 画像の挿入画面が表示されます。                                                                       |
| 削除         | 選択した画像を削除します。誤って削除してしまった場合は、ツールバーから元に戻すを選択してください。 |

## 画像のプレビュー

以下のいずれかの状態で、リッチテキスト中の画像をクリックすると、画像がポップアップして拡大表示されます。

1. レコードの一覧画面
2. レコードの編集画面で、編集モードをOFFにした状態

1つの項目に対して複数の画像を挿入している場合は、ポップアップした画像の右下に前後の画像を見るためのコントロールが表示されます。画像の大きさによりコントロールの表示位置が変わりますので、注意してください。画像の拡大表示を閉じるには、画像右上の×ボタンをクリックします。

<details markdown="1">
<summary>操作の詳細</summary>

![ポップアップした画像の右下に表示される、前後の画像を見るコントロール](https://pleasanter.org/files/images/ja/users-guide/common/assets/157880b397494ef1a07e828b862cde59.png)

</details>

## 関連情報

[リッチテキストエディタ](richtexteditor.md)
