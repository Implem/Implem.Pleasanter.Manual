---
title: context
icon: material/alpha-o-box
category: サーバスクリプト
order: '2000'
status: ''
parts: ''
urlstring: server-script-context
translationKey: server-script-context
shortname: context
created: 2021-01-22
updated: 2026-03-17
---

## 概要

[サーバスクリプト](../index.md)でユーザID、サイトIDなどの、ユーザ要求に関する情報を参照する際に使用します。また、スクリプト間のデータ共有、ログ出力、メッセージ出力に使用します。

## プロパティ

|No|Name|Get|Set|Type|Description|
|:----|:----|:----|:----|:----|:----|
|1|[UserData](server-script-context-user-data.md)|〇|〇|ExpandoObject|スクリプト間でデータの共有が可能|
|2|[QueryStrings](server-script-context-query-strings.md)|〇|-|Object|URLのクエリパラメータの値を取得可能|
|3|[Forms](server-script-context-forms.md)|○|-|Forms|フォームの情報を取得可能|
|4|FormStringRaw|○|-|string|フォーム（項目）に入力した情報|
|5|FormString|○|-|string|フォーム（項目）に入力した情報|
|6|Ajax|○|-|bool|Ajaxでリクエストしたかどうかのフラグ|
|7|Mobile|○|-|bool|Mobileでリクエストしたかどうかのフラグ|
|8|ApplicationPath|○|-|string|アプリケーションパス|
|9|AbsoluteUri|○|-|string|絶対URI|
|10|AbsolutePath|○|-|string|絶対パス|
|11|Url|○|-|string|URL|
|12|UrlReferrer|○|-|string|前回要求したURL|
|13|Controller|○|-|string|コントローラ名|
|14|Query|○|-|string|URLクエリパラメータ|
|15|Action|○|-|string|アクション名|
|16|TenantId|○|-|int|テナントID|
|17|SiteId|○|-|long|サイトID|
|18|Id|○|-|long|レコードID|
|19|Groups|○|-|IEnumerable<int>|所属するグループのグループIDのコレクション|
|20|TenantTitle|○|-|string|テナントのタイトル|
|21|SiteTitle|○|-|string|サイトのタイトル|
|22|RecordTitle|○|-|string|レコードのタイトル|
|23|DeptId|○|-|int|組織ID|
|24|UserId|○|-|int|ユーザID|
|25|LoginId|○|-|string|ログインID|
|26|Language|○|-|string|設定言語|
|27|TimeZoneInfo|○|-|string|タイムゾーン|
|28|HasPrivilege|○|-|bool|操作しているユーザが特権ユーザかどうかのフラグ|
|29|ApiVersion|○|-|decimal|APIのバージョン|
|30|ApiRequestBody|○|-|string|APIのリクエスト内容|
|31|RequestDataString|○|-|string|リクエストデータ|
|32|ContentType|○|-|string|レスポンスヘッダの種類|
|33|ServerScript.ScriptDepth|○|-|int|サーバスクリプトが実行された回数|
|34|ControlId|○|-|string|要求元コントロールのID|
|35|Condition|○|-|string|サーバースクリプトの条件の名称|
|36|ReferenceType|○|-|string|テーブル種別。記録テーブルの場合'Results'、期限付きテーブルの場合'Issues'を返却|
|37|HttpMethod|○|-|string|リクエストのHTTP Method|

## メソッド

|No|Name|Description|
|:----|:----|:----|
|1|[AddMessage](server-script-context-add-message.md)|ブラウザの画面下部にメッセージを出力します。|
|2|[Error](server-script-context-error.md)|ユーザが要求した作成、更新、削除の操作をキャンセルし、エラーメッセージを出力します。|
|3|[Log](server-script-context-log.md)|ブラウザのコンソールにログを出力します。|
|4|[Redirect](server-script-context-redirect.md)|ブラウザにページ遷移を実行させます。|
|5|[AddResponse](server-script-context-add-response.md)|任意のクライアントレスポンスを返却します。|
|6|[ResponseSet](server-script-context-response-set.md)|フォームに情報を格納します。|

## 使用例①

下記の例では、ログインユーザのユーザIDが1以外の場合には、作成者が自分自身のレコードのみ表示するようフィルタします。条件は「ビュー処理時」にチェックします。

``` javascript linenums="1"
if (context.UserId !== 1) {
    view.Filters.Creator = context.UserId;
}
```

## 使用例②

下記の例では、ログインユーザの所属する全てのグループのグループIDをログに出力します。

``` javascript linenums="1"
for (let groupId of context.Groups){
    context.Log(groupId);
}
```

## 使用例③

下記の例では、条件：更新後に設定した場合に初回更新後のみClassAに1234を入力し再度更新します。

``` javascript linenums="1"
// 無限に更新を繰り返すためcontext.ServerScript.ScriptDepthで実行回数をチェックする
if(context.ServerScript.ScriptDepth === 0){
    model.ClassA = '1234';
    model.UpdateOnExit = true;
}
```

## サンプルコード

!!! warning "注意事項"
    コード内の`【 ... 】`は適宜修正してください。

??? note "1. 任意のプロセス実行時にサーバスクリプトを起動する"

    `context.ControlId`で、実行されたプロセスを判定し、任意のサーバスクリプト処理を実行します。

    ``` javascript linenums="1"
    function itemsUpsert() {
        // サイト名を指定
        const siteName = '【サイト名】';
        // サイト情報を取得
        const site = items.GetClosestSite(siteName);
        if (!site) {
            logs.LogInfo(`${siteName} サイト情報取得失敗`);
            return false;
        }
        // 1対1同期のための「外部キー」
        // ※転記元レコード(ResultId)を転記先テーブルの ClassB に保存し、UpsertのKeysに指定する
        const sourceId = model.ResultId;
        // リクエストを生成
        const data = {
            Keys: ['ClassB'], // 外部キー項目（この値で更新/新規を判定）
            Title: model.Title,
            Status: model.Status,
            ClassHash: {
                ClassA: model.ClassA,
                ClassB: sourceId, // 外部キー（転記元ID）
            },
        };
        // レコードを作成/更新
        const result = items.Upsert(site.SiteId, JSON.stringify(data));
        if (result) {
            logs.LogInfo(`Upsert成功（外部キー=${sourceId}）`);
        } else {
            logs.LogUserError(`Upsert失敗（外部キー=${sourceId}）`);
        }
    }
    logs.LogInfo(`ControlId=${context.ControlId}`);
    switch (context.ControlId) {
        // ControlIdで実行されたプロセスを判断
        case 'Process_1':
            // プロセスID：1の処理
            itemsUpsert();
            break;
        default:
            // 何もしない
            break;
    }
    ```

    ### 実行結果

    ``` text title="実行結果"
    (Info):ControlId=Process_1
    (Info):Upsert成功（外部キー=9999）
    ```

??? note "2. ログインユーザの属性による画面項目制御"

    ログインユーザの属性（`context.HasPrivilege`、`context.Groups`で判定）と、状況により画面項目の制御（`columns.ReadOnly,Hide`で制御）を行います。サンプルコードでは以下のような仕様で実装しています。

    **制御パターン判定**

    | ユーザ種類 | 状況 | 制御パターン |
    |---|---|---|
    | 特権ユーザ | － | パターンA |
    | 管理者グループ所属ユーザ(ID1,2) | － | パターンB |
    | 上記以外のユーザ | 完了(900) or 保留(910) | パターンC |
    | 上記以外のユーザ | 以外 | パターンD |

    　

    **画面項目制御**

    | 画面項目 | 項目ID | パターンA | パターンB | パターンC | パターンD |
    |---|---|---|---|---|---|
    | タイトル | Title | 編集可 | 編集可 | 読取専用 | 編集可 |
    | 内容 | Body | 編集可 | 編集可 | 読取専用 | 編集可 |
    | 状況 | Status | 編集可 | 編集可 | 読取専用 | 編集可 |
    | 分類A | ClassA | 編集可 | 編集可 | 読取専用 | 編集可 |
    | 分類B | ClassB | 編集可 | 読取専用 | 非表示 | 非表示 |
    | 日付A | DateA | 編集可 | 読取専用 | 読取専用 | 編集可 |
    | 説明A | DescriptionA | 編集可 | 編集可 | 非表示 | 非表示 |

    ### JavaScript

    条件：画面表示の前

    ``` javascript linenums="1"
    // 設定
    const ADMIN_GROUP_IDS = new Set([1, 2]);
    const STATUS_PATTERN_C = new Set([900, 910]); // 完了/保留
    const PATTERN_RULES = {
        // パターンA: 何もしない（全編集可）
        A: [],
        // パターンB: ClassB, DateA を読取専用
        B: [
            ['ClassB', 'ReadOnly'],
            ['DateA', 'ReadOnly'],
        ],
        // パターンC: タイトル/内容/状況/分類A/日付Aは読取専用、ClassB/説明Aは非表示
        C: [
            ['Title', 'ReadOnly'],
            ['Body', 'ReadOnly'],
            ['Status', 'ReadOnly'],
            ['ClassA', 'ReadOnly'],
            ['DateA', 'ReadOnly'],
            ['ClassB', 'Hide'],
            ['DescriptionA', 'Hide'],
        ],
        // パターンD: ClassB, DescriptionA を非表示
        D: [
            ['ClassB', 'Hide'],
            ['DescriptionA', 'Hide'],
        ],
    };
    const DEBUG = true;
    // 判定（業務ルール）
    function decidePattern() {
        if (context.HasPrivilege) return 'A';
        // context.Groups は Iterable のため Set化して判定をシンプルに
        const userGroupIds = new Set(context.Groups);
        const isAdminGroupUser = [...ADMIN_GROUP_IDS].some((id) =>
            userGroupIds.has(id)
        );
        if (isAdminGroupUser) return 'B';
        // 上記以外のユーザ
        return STATUS_PATTERN_C.has(model.Status) ? 'C' : 'D';
    }
    // 適用（UI制御）
    function applyPattern(pattern) {
        const rules = PATTERN_RULES[pattern] ?? [];
        for (const [columnName, control] of rules) {
            // サンプルとして：列が存在しない場合も落とさずスキップ
            if (!columns[columnName]) continue;
            columns[columnName][control] = true;
        }
    }
    // 実行
    const pattern = decidePattern();
    if (DEBUG) context.Log(`pattern=${pattern}`);
    applyPattern(pattern);
    ```

    ### 実行結果

    ``` text title="実行結果"
    (Info):pattern=C
    ```

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.17.0 以降| サーバスクリプトにcontext.ReferenceTypeプロパティを追加 |
|1.4.17.0 以降| サーバスクリプトにcontext.HttpMethodプロパティを追加 |

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [開発者ガイド：サーバスクリプト：context.UserData](server-script-context-user-data.md)
-   [開発者ガイド：サーバスクリプト：context.QueryStrings](server-script-context-query-strings.md)
-   [開発者ガイド：サーバスクリプト：context.Forms](server-script-context-forms.md)
-   [開発者ガイド：サーバスクリプト：context.AddMessage](server-script-context-add-message.md)
-   [開発者ガイド：サーバスクリプト：context.Error](server-script-context-error.md)
-   [開発者ガイド：サーバスクリプト：context.Log](server-script-context-log.md)
-   [開発者ガイド：サーバスクリプト：context.Redirect](server-script-context-redirect.md)
-   [開発者ガイド：サーバスクリプト：context.AddResponse](server-script-context-add-response.md)
-   [開発者ガイド：サーバスクリプト：context.ResponseSet](server-script-context-response-set.md)
