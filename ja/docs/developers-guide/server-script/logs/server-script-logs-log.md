---
title: logs.Log
icon: material/alpha-m-box
category: サーバスクリプト
order: '2500'
status: ''
parts: ''
urlstring: server-script-logs-log
translationKey: server-script-logs-log
shortname: logs.Log
created: 2025-01-07
updated: 2026-06-23
---

## 概要

[logsオブジェクト](index.md)の「Log」メソッドです。[サーバスクリプト](../index.md)で指定したログの種類でログを表示、出力します。

## 構文

``` javascript
logs.Log(type, message, method, console, syslogs)
```

## パラメータ

|パラメータ|型|必須|説明|
|:----------|:----------|:---:|:---------------------------|
|type|int|○|ログの種類を指定。指定可能な値は以下の通り<br>10：Info<br>50：Warning<br>60：UserError<br>80：SystemError<br>90：Exception|
|message|string|○|表示、出力するエラー内容を指定。|
|method|string||省略可能。既定値は空文字。|
|console|bool||省略可能。既定値はtrue。ブラウザの開発者ツールのコンソールに表示する場合はtrueを指定|
|syslogs|bool||省略可能。既定値はtrue。システムログに出力する場合はtrueを指定|

## 戻り値

ログを表示、出力できたらtrue、表示、出力できなかったら`false`を返却します。

## コンソール表示時の表示内容

##### 表示フォーマット

``` text
(SysLogType):[Method]Message
```

|表示項目|表示内容|備考|
|:----------|:-------|:-------|
|Message|messageで設定した文字列||
|Method|methodで設定した文字列|method未指定時は角括弧（[]）も表示しない|
|SysLogType|typeによって以下の文字列を表示<br>10：Info<br>50：Warning<br>60：UserError<br>80：SystemError<br>90：Exception||

## システムログ出力時の出力先項目

|出力先項目|出力内容|備考|
|:----------|:-------|:-------|
|Comments|messageで設定した文字列|typeが10（Info）、50（Warning）、60（UserError）の場合|
|ErrMessage|messageで設定した文字列|typeが80（SystemError）、90（Exception）の場合|
|Method|本来のMethodに記録される文字列に「:method」の形式で結合した文字列||
|SysLogType|type||

## 使用例

下記の例では、サイトID 2 の「期限付きテーブル」にタイトルが "プリザンターのバージョンアップについて" のレコードを作成し、その結果に応じてlogs.Logでログ出力します。

##### JavaScript

``` javascript linenums="1"
try {
    const siteId = 2;
    const item = items.NewIssue();
    item.Title = 'プリザンターのバージョンアップについて';
    const ret = items.Create(siteId, item);
    if (ret) {
        // Infoログ
        logs.Log(10, `レコードを作成しました。レコードID:${item.IssueId}`); 
    } else {
        // SystemErrorログ
        logs.Log(80, `レコードの作成に失敗しました。サイトID:${siteId}`); 
    }
} catch(e) {
    // Exceptionログ
    logs.Log(90, `例外発生\n ${e.stack}`);
}
```

## サンプルコード

??? note "1. 汎用的なログ出力関数"

    `logs.Log`メソッドをラップし、デバッグ時と本番時でログ出力を切り分けられる汎用ロガーのサンプルコードです。

    ### 機能要件

    1.  デバッグフラグによる出力制御

        `DEBUG_MODE`（bool）で Info（type=10）の出力を制御する。`false` のとき Info は抑制され、`true` のとき出力される。Warning（50）以上は `DEBUG_MODE` に関係なく常時出力する。

    2.  出力先の一元管理

        `LOG_TARGET`（console / syslogs の bool）で、コンソールとシステムログへの出力をそれぞれ個別にオン・オフできる。設定はスクリプト全体に一括適用される。

    3.  ログ種別定数の提供

        `logs.Log` の `type` 引数に対応する定数オブジェクト `LOG_TYPE` を提供し、数値の直書きによるミスを防ぐ。

        | 定数 | 値 | ログ種別 |
        |---|---|---|
        | LOG_TYPE.INFO | 10 | Info |
        | LOG_TYPE.WARNING | 50 | Warning |
        | LOG_TYPE.USER_ERROR | 60 | UserError |
        | LOG_TYPE.SYSTEM_ERROR | 80 | SystemError |
        | LOG_TYPE.EXCEPTION | 90 | Exception |

    4.  2つのメソッドの提供

        | メソッド | 説明 | DEBUG_MODE=false | DEBUG_MODE=true |
        |---|---|---|---|
        | logEx.log(type, message, method) | logs.Log の薄いラッパー。type=10 のみ抑制 | Warning 以上のみ出力 | 全て出力 |
        | logEx.debug(message, method) | デバッグ専用。Info（10）で出力 | 出力しない | 出力する |

    5.  method パラメータの透過渡し

        各メソッドの method 引数を **logs.Log** の method パラメータにそのまま渡せる。

    ##### JavaScript

    ```javascript linenums="1"
    // ============================================================
    // デバッグモード。true にすると debug() と type=10(Info) のログが出力される
    // ============================================================
    const DEBUG_MODE = true;
    /**
     * 出力先の制御
     *   console : ブラウザ開発者ツールのコンソールに出力するか
     *   syslogs : システムログ（SysLogs テーブル）に出力するか
     */
    const LOG_TARGET = {
        console: true,
        syslogs: true,
    };
    // ============================================================
    // ログ種別の定数（logs.Log の type 引数に対応）
    // ============================================================
    const LOG_TYPE = {
        INFO: 10,
        WARNING: 50,
        USER_ERROR: 60,
        SYSTEM_ERROR: 80,
        EXCEPTION: 90,
    };
    // ============================================================
    // ロガー本体
    // ============================================================
    const logEx = (function (debugMode, target) {
        /**
         * DEBUG_MODE=false のとき、Info（type=10）は抑制する。
         * Warning 以上（type>=50）は常に出力する。
         */
        function _isOutputAllowed(type) {
            if (type === LOG_TYPE.INFO && !debugMode) return false;
            return true;
        }
        return {
            /**
             * logs.Log をそのままラップしたメソッド。
             * type=10(Info) は DEBUG_MODE=true のときのみ出力される。
             * type=50 以上（Warning/UserError/SystemError/Exception）は常に出力される。
             *
             * @param {number} type    - ログ種別（LOG_TYPE 定数を推奨）
             * @param {string} message - ログメッセージ
             * @param {string} [method] - メソッド名（省略可）
             */
            log: function (type, message, method) {
                if (!_isOutputAllowed(type)) return;
                const m = method || '';
                logs.Log(type, message, m, target.console, target.syslogs);
            },
            /**
             * デバッグ専用ログ。DEBUG_MODE=true のときのみ Info（type=10）で出力。
             * 変数の中身確認や処理トレースなど、本番では不要な出力に使う。
             *
             * @param {string} message
             * @param {string} [method]
             */
            debug: function (message, method) {
                if (!debugMode) return;
                const m = method || '';
                logs.Log(
                    LOG_TYPE.INFO,
                    '[DEBUG] ' + message,
                    m,
                    target.console,
                    target.syslogs,
                );
            },
        };
    })(DEBUG_MODE, LOG_TARGET);
    // ======================
    // 使用例
    // ======================
    // ─── 例1：デバッグログ（DEBUG_MODE=true のときだけ出力） ───
    logEx.debug('処理開始: siteId=' + 1000, 'MyScript');
    // ─── 例2：INFO ログ（DEBUG_MODE=true のときだけ出力） ───
    logEx.log(LOG_TYPE.INFO, 'レコードを取得しました。', 'FetchRecord');
    // ─── 例3：WARNING ログ（常に出力） ───
    logEx.log(
        LOG_TYPE.WARNING,
        '対象レコードが見つかりませんでした。',
        'FetchRecord',
    );
    // ─── 例4：UserError ログ（常に出力） ───
    logEx.log(LOG_TYPE.USER_ERROR, '必須項目が未入力です。', 'Validate');
    // ─── 例5：SystemError ログ（常に出力） ───
    logEx.log(LOG_TYPE.SYSTEM_ERROR, 'APIへの接続に失敗しました。', 'CallApi');
    // ─── 例6：Exception ログ（catch と組み合わせて使う） ───
    try {
        const item = items.NewIssue();
        item.Title = 'テスト';
        items.Create(2, abcd); // 強制的に例外発生
        logEx.log(LOG_TYPE.INFO, '作成成功', 'CreateIssue');
    } catch (e) {
        logEx.log(LOG_TYPE.EXCEPTION, e.message + '\n' + e.stack, 'CreateIssue');
    }
    // ─── 例7：数値を直接指定することも可能 ───
    logEx.log(50, '直接指定の警告ログ', 'DirectType');
    ```

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.12.0 以降|機能追加|

## 関連情報

-   [開発者ガイド：サーバスクリプト：logs](index.md)
-   [開発者ガイド：サーバスクリプト](../index.md)
