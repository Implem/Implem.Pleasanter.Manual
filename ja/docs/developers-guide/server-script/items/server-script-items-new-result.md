---
title: items.NewResult
icon: material/alpha-m-box
category: サーバスクリプト
order: '10000'
status: ''
parts: ''
urlstring: server-script-items-new-result
translationKey: server-script-items-new-result
shortname: items.NewResult
created: 2023-07-31
updated: 2026-02-02
---

## 概要

[サーバスクリプト](../index.md)で「記録テーブル」に対する「apiModelオブジェクト」の新規インスタンスを作成します。

## 構文

```
items.NewResult()
```

## 戻り値

「記録テーブル」の「apiModelオブジェクト」を返却します。

## 使用例

下記の例では、サイトID 3 の「記録テーブル」にタイトルが "プリザンターのバージョンアップについて" のレコードを作成します。

##### JavaScript

```
let siteId = 3;
let item = items.NewResult();
item.Title = 'プリザンターのバージョンアップについて';
items.Create(siteId, item);
context.Log(item.ResultId); // 作成したレコードのIDを出力
```

## サンプルコード

??? note "1. 親テーブルにリンクする子テーブルのレコードを作成する"

    案件を管理する「案件管理」テーブル(親)と、それにリンクする「タスク管理」テーブル(子)を用意します。  

    親の案件管理レコード作成時に定型タスクとして、「'要件定義', '設計', '開発', 'テスト', 'リリース'」をリンクさせた形で作成します。  

    そのため、案件管理レコード作成後にレコードIDを取得。そのIDをタスク管理レコードに登録することで、親子関係のリンクを保持したレコードが作成できます。

    ##### JavaScript
    条件：作成後、更新後 等
    ```javascript
    // サイトIDキャッシュ
    const _siteIdCache = new Map();
    // サイト名からSiteIdを取得（キャッシュ）
    function getSiteIdOrNull(siteName) {
        if (_siteIdCache.has(siteName)) return _siteIdCache.get(siteName);
        const site = items.GetClosestSite(siteName);
        if (!site || !site.SiteId) {
            logs.LogInfo(`${siteName} サイト情報取得失敗`);
            return null;
        }
        _siteIdCache.set(siteName, site.SiteId);
        return site.SiteId;
    }
    // レコード作成共通処理
    function createAndGetId(siteId, apiModel, fields) {
        // fields を apiModel に流し込む
        for (const [key, value] of Object.entries(fields)) {
            apiModel[key] = value;
        }
        try {
            apiModel.Create(siteId);
        } catch (e) {
            logs.LogException(
                `apiModel.Create Error: ${e && e.stack ? e.stack : e}`
            );
            return null;
        }
        // IDを返却
        const id = apiModel.ResultId ?? apiModel.IssueId ?? null;
        logs.LogInfo(`created id: ${id}`);
        return id;
    }
    // メイン処理
    // 親（案件管理）を作成
    const caseSiteId = getSiteIdOrNull('案件管理');
    if (!caseSiteId) {
        logs.LogException('案件管理サイトの取得に失敗しました。');
        return;
    }
    const caseId = createAndGetId(caseSiteId, items.NewResult(), {
        Title: 'サンプル案件',
        Status: '200',
        ClassA: '顧客管理システムの刷新',
        DateA: '2025/01/10',
        NumA: 5,
    });
    if (!caseId) {
        logs.LogException('案件の作成に失敗しました。');
        return;
    }
    // 子（タスク管理）を作成（リンク項目に親IDをセット）
    const taskSiteId = getSiteIdOrNull('タスク管理');
    if (!taskSiteId) {
        logs.LogException('タスク管理サイトの取得に失敗しました。');
        return;
    }
    const taskList = ['要件定義', '設計', '開発', 'テスト', 'リリース'];
    for (const task of taskList) {
        const taskId = createAndGetId(taskSiteId, items.NewIssue(), {
            Title: 'サンプル案件',
            ClassA: task,
            ClassD: String(caseId),
        });
        if (!taskId) {
            logs.LogException('タスクの作成に失敗しました。');
            return;
        }
    }
    ```

    ##### 実行結果
    ```
    (Info):created id: 9001
    (Info):created id: 9002
    (Info):created id: 9003
    (Info):created id: 9004
    (Info):created id: 9005
    (Info):created id: 9006
    ```

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)