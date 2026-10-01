---
title: items.Count
icon: material/alpha-m-box
category: サーバスクリプト
order: '10000'
status: ''
parts: ''
urlstring: server-script-items-count
translationKey: server-script-items-count
shortname: items.Count
created: 2021-01-27
updated: 2026-07-08
---

## 概要

[itemsオブジェクト](index.md)の「Countメソッド」です。指定したテーブルのレコード数を集計します。  選択条件を指定して集計対象のレコードを絞り込むことができます。

## 構文

```
items.Count(siteId, view)
```

## パラメータ

|パラメータ|型|必須|説明|
|:----------|:----------|:---:|:---------------------------|
|siteId|object|○|対象テーブルのサイトIDを指定|
|view|string|-|選択するレコードの条件を指定|

## 戻り値

レコードの件数を返却します。

## 使用例①

以下の例は、サイトIDが 2 のテーブルに登録されているレコード件数を集計します。

##### JavaScript

```
let count = items.Count(2);
```

## 使用例②

以下の例は、サイトIDが 2 のテーブル登録されているレコードで、Status(状況)が900(完了)のレコードの件数を集計します。

##### JavaScript

```
let view = {
    "View": {
        "ColumnFilterHash": {
            "Status": "[\"900\"]"
        }
    }
};
let count = items.Count(2, JSON.stringify(view));
context.Log(count);
```

## サンプルコード

??? note "1. 3階層以上のサマリ処理"

    ##### 概要

    標準機能では実現できない、3階層以上のサマリ処理を実現します。このサンプルでは、作業実績→プロジェクト→部門の3テーブルを用意し、実績工数をタスク単位→プロジェクト単位→部門単位とサマリしていきます。

    サマリのイメージは以下のとおりで、サーバスクリプトは孫である作業実績テーブルへ設定します。

    ![3階層のサマリのイメージ図。作業実績テーブルからプロジェクトテーブル、部門テーブルへと工数を積み上げる](https://pleasanter.org/files/images/ja/developers-guide/server-script/items/assets/f7b1e7480006442ea155dff0483f90c5.png)

    ##### 使用テーブル

    以下のようなテーブルを用意します。

    〇部門テーブル

    | 項目 |表示名 | 備考 |
    |---|---|---|
    | Title | 部門 |  |
    | NumA | 月間総工数（時間） | 積み上げ先 |
    | NumB | 月間予算工数（時間） | 手動入力 |

    〇プロジェクトテーブル

    | 項目 |表示名 | 備考 |
    |---|---|---|
    | Title |プロジェクト |  |
    | ClassA | 部門 | 部門テーブルへのリンク項目 |
    | NumA | プロジェクト総工数（時間）| 積み上げ先 |

    〇作業実績テーブル

    | 項目 |表示名 | 備考 |
    |---|---|---|
    | Title |タスク名 |  |
    | ClassA | プロジェクト | プロジェクトテーブルへのリンク項目 |
    | NumA | 作業時間（時間）| 入力値

    **サンプルコード内で、サイト名「プロジェクトテーブル」「作業実績テーブル」で制御しているため、実際のテーブル設定に合わせて調整してください。**

    ##### HIERARCHY_CONFIG 仕様

    **HIERARCHY_CONFIG** は階層サマリの動作をすべて制御する定義体です。この配列のみを編集することで、テーブル構成・集計内容・階層数を自由にカスタマイズできるようになっています。

    〇構造

    ```javascript
    const HIERARCHY_CONFIG = [
        // 第1階層（最下位テーブルから1つ上へ）
        {
            childSiteName: '集計元テーブル名',
            linkColumn:    '親へのリンク列名',
            operations: [
                { 
                    aggregateType: AGGREGATE_TYPE.SUM, 
                    sourceColumn: '集計列名', 
                    writeColumn: '書き込み列名' 
                },
            ],
        },
        // 第2階層（さらに1つ上へ）
        {
            childSiteName: '集計元テーブル名',
            linkColumn:    '親へのリンク列名',
            operations: [
                {
                    aggregateType: AGGREGATE_TYPE.SUM, 
                    sourceColumn: '集計列名', 
                    writeColumn: '書き込み列名' },
            ],
        },
        // 以降、必要な階層数だけ追加
    ];
    ```

    〇階層レベルのプロパティ

    | プロパティ | 型 | 必須 | 説明 |
    |---|---|:---:|---|
    | childSiteName | string | ✓ | 集計元テーブルのサイト名。items.GetClosestSite() で解決される |
    | linkColumn | string | ✓ | 子テーブルが親レコードを指すリンク列名。次の階層への辿りにも使用される |
    | operations | array | ✓ | 同階層内で実行する集計操作の一覧（1件以上） |

    〇operations のプロパティ

    | プロパティ | 型 | 必須 | 説明 |
    |---|---|:---:|---|
    | aggregateType | 定数 | ✓ | 集計種別。AGGREGATE_TYPE 定数を使用する |
    | sourceColumn | string | △ | 集計対象の数値列名。AGGREGATE_TYPE.COUNT の場合は省略可 |
    | writeColumn | string | ✓ | 集計結果を書き込む親テーブル側の列名 |

    〇AGGREGATE_TYPE 定数

    | 定数 | 処理内容 | sourceColumn |
    |---|---|:---:|
    | AGGREGATE_TYPE.COUNT | レコード件数を集計 | 省略可 |
    | AGGREGATE_TYPE.SUM | 数値列の合計を集計 | 必須 |
    | AGGREGATE_TYPE.AVERAGE | 数値列の平均を集計 | 必須 |
    | AGGREGATE_TYPE.MIN | 数値列の最小値を集計 | 必須 |
    | AGGREGATE_TYPE.MAX | 数値列の最大値を集計 | 必須 |

    ##### 動作の仕様

    -   配列は **下位テーブルから上位テーブルへの順** に記述する
    -   linkColumn は「子が親を絞り込む列」と「親から次の親IDを辿る列」を兼ねる
    -   いずれかの階層でエラーが発生した場合、以降の階層処理は中断される

    ##### 設定例：同一階層で複数の集計を行う場合

    ```javascript
    {
        childSiteName: '作業実績',
        linkColumn:    'ClassA',
        operations: [
            { 
                aggregateType: AGGREGATE_TYPE.SUM,     
                sourceColumn: 'NumA', 
                writeColumn: 'NumA' 
            }, // 合計
            { 
                aggregateType: AGGREGATE_TYPE.AVERAGE, 
                sourceColumn: 'NumA', 
                writeColumn: 'NumB' 
            }, // 平均
            { 
                aggregateType: AGGREGATE_TYPE.COUNT,
                writeColumn: 'NumD' 
            }, // 件数
        ],
    },
    ```

    ##### JavaScript

    条件：作成後、更新後

    ```javascript
    // ============================================================
    // 集計種別定数
    // ============================================================
    const AGGREGATE_TYPE = {
        COUNT: 'count',
        SUM: 'sum',
        AVERAGE: 'average',
        MIN: 'min',
        MAX: 'max',
    };
    // ============================================================
    // 配列の各要素が1つの「階層（レベル）」を表す。
    // 同じ階層に複数の操作を並べても、親レコードの取得・更新は1回にまとめて実行される。
    // 階層の追加・変更はこの定義のみ修正すればよい。
    // ============================================================
    const HIERARCHY_CONFIG = [
        // 第1階層: 作業実績 → プロジェクト
        {
            childSiteName: '作業実績',
            linkColumn: 'ClassA',
            operations: [
                {
                    aggregateType: AGGREGATE_TYPE.SUM,
                    sourceColumn: 'NumA',
                    writeColumn: 'NumA',
                },
            ],
        },
        // 第2階層: プロジェクト → 部門
        {
            childSiteName: 'プロジェクト',
            linkColumn: 'ClassA',
            operations: [
                {
                    aggregateType: AGGREGATE_TYPE.SUM,
                    sourceColumn: 'NumA',
                    writeColumn: 'NumA',
                },
            ],
        },
        // 第3階層以上に拡張する場合はここに追加する
    ];
    // ============================================================
    // サイトID取得（キャッシュ付き）
    // ============================================================
    const _siteIdCache = new Map();
    function getSiteIdOrNull(siteName) {
        if (_siteIdCache.has(siteName)) return _siteIdCache.get(siteName);
        const site = items.GetClosestSite(siteName);
        if (!site || !site.SiteId) {
            logs.LogUserError(
                `サイト情報取得失敗: ${siteName}`,
                getSiteIdOrNull.name,
            );
            return null;
        }
        _siteIdCache.set(siteName, site.SiteId);
        return site.SiteId;
    }
    // ============================================================
    // 集計種別ディスパッチ
    // ============================================================
    function aggregate(type, siteId, sourceColumn, view) {
        switch (type) {
            case AGGREGATE_TYPE.COUNT:
                return items.Count(siteId, view) || 0;
            case AGGREGATE_TYPE.SUM:
                return items.Sum(siteId, sourceColumn, view) || 0;
            case AGGREGATE_TYPE.AVERAGE:
                return items.Average(siteId, sourceColumn, view) || 0;
            case AGGREGATE_TYPE.MIN:
                return items.Min(siteId, sourceColumn, view) || 0;
            case AGGREGATE_TYPE.MAX:
                return items.Max(siteId, sourceColumn, view) || 0;
            default:
                logs.LogUserError(`不明な aggregateType: ${type}`, aggregate.name);
                return null;
        }
    }
    // ============================================================
    // 階層サマリ実行
    // ============================================================
    function runHierarchySummary(config, startParentId) {
        let currentParentId = startParentId;
        for (const level of config) {
            if (!currentParentId) {
                logs.LogUserError(
                    '親IDが取得できないため処理を中断します',
                    runHierarchySummary.name,
                );
                break;
            }
            const siteId = getSiteIdOrNull(level.childSiteName);
            if (!siteId) break;
            // 親レコードを階層ごとに1回だけ取得する
            const parent = Array.from(items.Get(Number(currentParentId)))[0];
            if (!parent) {
                logs.LogUserError(
                    `親レコード取得失敗: ID=${currentParentId}`,
                    runHierarchySummary.name,
                );
                break;
            }
            // 同階層の全operationsを集計し、親レコードに値をセット
            let hasError = false;
            for (const op of level.operations) {
                const view = {
                    View: {
                        ColumnFilterHash: {
                            [level.linkColumn]: `["${currentParentId}"]`,
                        },
                    },
                };
                const total = aggregate(
                    op.aggregateType,
                    siteId,
                    op.sourceColumn,
                    JSON.stringify(view),
                );
                if (total === null) {
                    hasError = true;
                    break;
                }
                parent[op.writeColumn] = total;
            }
            if (hasError) break;
            // 全operationsが完了したら親レコードを1回だけ更新
            parent.Update();
            // 次の階層へ: linkColumn を辿って親の親IDを取得
            currentParentId = parent[level.linkColumn];
        }
    }
    // ============================================================
    // エントリポイント
    // ============================================================
    runHierarchySummary(HIERARCHY_CONFIG, model.ClassA);
    ```

## 注意事項

こちらは[サーバスクリプト](../index.md)で使用するメソッドです。[スクリプト](../../../managers-guide/manage-table/scripts/index.md)では使用できません。

## 関連情報

-   [開発者ガイド：サーバスクリプト：items](index.md)
-   [開発者ガイド：サーバスクリプト](../index.md)
-   [テーブルの管理：スクリプト](../../../managers-guide/manage-table/scripts/index.md)