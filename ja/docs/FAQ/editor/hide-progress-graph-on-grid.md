---
title: 一覧画面の進捗率に表示されるグラフを非表示にしたい
category: FAQ：編集画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: hide-progress-graph-on-grid
translationKey: hide-progress-graph-on-grid
shortname: FAQ：一覧画面の進捗率に表示されるグラフを非表示にしたい
created: 2026-03-25
updated: 2026-08-17
---

## 回答

「[スクリプト](../../managers-guide/manage-table/scripts/index.md)」を使い「[一覧画面](../../users-guide/table/record-authoring/data-analysis/table-grid.md)」の「[進捗率](../../users-guide/table/record-authoring/edit-records/table-record-progression-rate.md)」に表示される帯グラフを非表示にできます。

---

## 概要

一部箇所（たとえば、予定帯グラフのみ）の表示・非表示を切り替える機能はありません。「[スクリプト](../../managers-guide/manage-table/scripts/index.md)」にて表示を書き換える必要があります。

## サンプルコード

以下のサンプルコードを、「期限付きテーブル」のスクリプトとして追加すると、「[進捗率](../../users-guide/table/record-authoring/edit-records/table-record-progression-rate.md)」に表示される予定帯グラフを非表示にします。「出力先」は「一覧 」に設定してください。

![サンプルコードを登録するスクリプトの設定画面](https://pleasanter.org/files/images/ja/FAQ/editor/assets/84b8c075db7f4cda9e1fffabbb15c36e.png)

##### スクリプト（出力先：一覧）

```js
// 予定帯グラフを非表示にするスクリプト
$p.events.on_grid_load = function () {

    // svg-progress-rateクラスを持つSVG要素を取得
    const svgs = document.querySelectorAll('td svg.svg-progress-rate');

    // 各SVG要素に対して操作を実行
    svgs.forEach(function(svg) {

      // 濃いグレーの<rect>要素を非表示にする
      svg.querySelector('rect:nth-of-type(1)').style.display = 'none';

      // 薄いグレーの<rect>要素を非表示にする
      svg.querySelector('rect:nth-of-type(2)').style.display = 'none';

      // グリーンまたはレッドの<rect>要素のy属性を20に設定
      svg.querySelector('rect:nth-of-type(3)').setAttribute('y', '20');

    });
}
```

上記のスクリプトにより、予定帯グラフを非表示とし、その下の帯グラフの高さを大きく（y属性を20に）しています。

希望の表示内容に応じて、修正してください。
