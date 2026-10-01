---
title: APIで200レコードを超えるデータを取得したい
category: FAQ：開発者向け機能
order: '0'
status: ''
parts: ''
urlstring: faq-api-paging
translationKey: faq-api-paging
shortname: API,PageSize
created: 2022-11-29
updated: 2024-04-29
---

## 回答

POSTするパラメータで「Offset」を指定してください

---

## 概要

複数レコードを取得する際、APIからの応答に含まれるレコードの件数は[Api.json](../../setup/parameters/api-json.md)のPageSize（デフォルトで200）が最大となります。

Offsetを指定するとことで、後続のレコードを取得することができます。

## 注意事項

1.  システム全体の負荷とならないよう、基本的にはViewパラメータによって、取得件数を絞ることを検討してください。
1.  [Api.json](../../setup/parameters/api-json.md)のPageSizeを大きくすることでの対応は、一度に多量のデータを応答することになり、サーバ側およびクライアント側の処理の負荷を増大させる可能性があります。

## 操作手順

1.  レスポンスのTotalCountが、レスポンスのPageSizeを超えている場合、取得できていないレコードが存在します。
2.  Offsetを追加したリクエストをすることで、後続のレコードを取得します。

### レコード件数の確認

以下のようなリクエストを行うと、レコードの件数の情報が取得できます。

このとき`(開始位置 + 一度に取得できる件数) > 全件`となっているかをチェックすることで、未取得のレコードがあることをコード的に判定できます。

``` js title="JavaScript" linenums="1"
const siteId = 123456;  // レコードを取得するサイトのサイトID
$p.apiGet({
    id: siteId,
    done: (e) => console.log({
        '全件':e.Response.TotalCount, 
        '一度に取得できる件数':e.Response.PageSize, 
        '開始位置':e.Response.Offset
    })
});
```

### オフセットを指定したレコードの取得

以下のようにdataとしてOffsetを指定することで、結果取得位置を繰り下げることができます。

``` js title="JavaScript" linenums="1" hl_lines="4"
const siteId = 123456; // レコードを取得するサイトのサイトID
$p.apiGet({
    id: siteId,
    data: {Offset:200},
    done: (e) => console.log(e.Response.Data);
});
```

前述のように、レスポンスのOffsetとPageSizeの和とTotalCount以上となった場合に末尾まで取得できたことを判定できるため、この条件を満たすまで繰り返し実行することで、ページング処理を実施できます。
実業務においては、ページング処理中にデータ更新が行われることにるデータの並び順の変更や新規作成、削除により、単純にページングを実施しても全てのレコードをスキャンできない可能性があることを考慮してください。

## 関連情報

-   [パラメータ設定：Api.json](../../setup/parameters/api-json.md)
