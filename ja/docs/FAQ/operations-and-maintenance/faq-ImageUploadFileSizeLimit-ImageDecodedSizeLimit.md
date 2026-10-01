---
title: 「ファイルサイズが大きすぎます。」が表示され、レコードを更新できない。
category: FAQ：運用、メンテナンス
order: '0'
status: ''
parts: ''
urlstring: faq-ImageUploadFileSizeLimit-ImageDecodedSizeLimit
translationKey: faq-ImageUploadFileSizeLimit-ImageDecodedSizeLimit
shortname: ''
created: 2026-06-22
updated: 2026-07-14
---

## 回答

以下のいずれかの対応を行ってください。

1.  貼り付ける画像ファイルのサイズを小さくする
1.  BinaryStorage.jsonのImageUploadFileSizeLimitとImageDecodedSizeLimitを見直す

---

## 概要

内容や説明項目、コメントに画像を貼り付けた場合、画像のファイルサイズが設定値を超える場合は「ファイルサイズが大きすぎます。」のエラーになります。
ファイルサイズの設定値は[BinaryStorage.json](../../setup/parameters/binary-storage-json.md)でクライアント側、サーバ側でそれぞれ指定します。

| パラメータ名             | 説明                                                                               |
| :----------------------- | :--------------------------------------------------------------------------------- |
| ImageUploadFileSizeLimit | クライアント側のチェック上限値。貼り付ける画像ファイルのサイズの上限値（単位：MB） |
| ImageDecodedSizeLimit    | サーバ側のチェック上限値。画像ファイルをデコードしたサイズの上限値（単位：MB）     |

画像ファイルをデコードするとファイルサイズは大きくなるため、ImageDecodedSizeLimitにはImageUploadFileSizeLimitよりも大きな値を設定してください。  
デコード後のファイルサイズはファイル種別によって異なります。以下の計算を参考にしてください。

-   静止画

    展開後のメモリサイズは解像度と色数に依存します。（解像度×色数）

    | 画像形式  | 解像度    | 色数      | 展開後のメモリ |
    | :-------- | :-------- | :-------- | :------------- |
    | JPEG      | 3000×4000 | 3（RGB）  | 約36MB         |
    | PNG       | 3000×4000 | 4（RGBA） | 約48MB         |
    | 静止画GIF | 1920×1080 | 1～4      | 約8MB          |

-   GIFアニメ

    展開後にフレーム数を更に乗算します。

    | 画像形式  | 解像度    | 色数 | フレーム数  | 展開後のメモリ |
    | :-------- | :-------- | :--- | :---------- | :------------- |
    | GIFアニメ | 1920×1080 | 1～4 | 100フレーム | 約800MB        |

## 対応バージョン

| 対応バージョン | 内容                                 |
| :------------- | :----------------------------------- |
| 1.5.6.0 以降   | 高負荷画像のサイズチェック機能を追加 |

## 関連情報

-   [BinaryStorage.json](../../setup/parameters/binary-storage-json.md)
