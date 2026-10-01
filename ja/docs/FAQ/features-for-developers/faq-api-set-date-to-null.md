---
title: APIで日付項目をNULLに設定したい
category: FAQ：開発者向け機能
order: '0'
status: ''
parts: ''
urlstring: faq-api-set-date-to-null
translationKey: faq-api-set-date-to-null
shortname: ''
created: 2022-07-22
updated: 2024-04-29
---

## 回答

パラメータ[General.json](../../setup/parameters/general.json.md)の「MinTime」、「MaxTime」で設定した値の範囲外の値をセットしてください。

---

## 概要

プリザンター[API](../../developers-guide/api/basics/api.md)の「レコード更新」にて日付項目に[General.json](../../setup/parameters/general.json.md)の「MinTime」、「MaxTime」で設定した値の範囲外の値をセットすることで、NULLに更新できます。

## スクリプト

日付AをNULLに更新するスクリプトとなります。[General.json](../../setup/parameters/general.json.md)の「MinTime」、「MaxTime」を以下のように設定している場合、「1899/12/31」をセットします。
MinTime: "1900/1/1"  
MaxTime: "2100/1/1"  

##### javascript

```
$p.apiUpdate({
    id: 123456,
    data: {
        ApiVersion: 1.1,
        DateHash: {
            DateA: '1899/12/31'
        }
    },
    done: function (data) {
        console.log('success!');
        console.log(data);
    },
    fail: function (data) {
        console.log('fail...');
        console.log(data);
    }
});
```

## 関連情報

-   [パラメータ設定：General.json](../../setup/parameters/general.json.md)
-   [開発者ガイド：API](../../developers-guide/api/basics/api.md)

