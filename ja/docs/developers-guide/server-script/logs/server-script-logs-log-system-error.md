---
title: logs.LogSystemError
icon: material/alpha-m-box
category: サーバスクリプト
order: '2500'
status: ''
parts: ''
urlstring: server-script-logs-log-system-error
translationKey: server-script-logs-log-system-error
shortname: logs.LogSystemError
created: 2025-01-07
updated: 2026-06-23
---

## 概要

[logsオブジェクト](index.md)の「LogSystemError」メソッドです。[サーバスクリプト](../index.md)でログの種類：SystemErrorとしてログを表示、出力します。

## 構文

``` javascript
logs.LogSystemError(message, method, console, syslogs)
```

## パラメータ

|パラメータ|型|必須|説明|
|:----------|:----------|:---:|:---------------------------|
|message|string|○|表示、出力するエラー内容を指定。|
|method|string||省略可能。既定値は空文字。|
|console|bool||省略可能。既定値はtrue。ブラウザの開発者ツールのコンソールに表示する場合はtrueを指定|
|syslogs|bool||省略可能。既定値はtrue。システムログに出力する場合はtrueを指定|

## 戻り値

ログを表示、出力できたらtrue、表示、出力できなかったらfalseを返却します。

## コンソール表示時の表示内容

##### 表示フォーマット

```
(SystemError):[Method]Message
```

|表示項目|表示内容|備考|
|:----------|:-------|:-------|
|Message|messageで設定した文字列||
|Method|methodで設定した文字列|method未指定時は角括弧（[]）も表示しない|

## システムログ出力時の出力先項目

|出力先項目|出力内容|備考|
|:----------|:-------|:-------|
|ErrMessage|messageで設定した文字列||
|Method|本来のMethodに記録される文字列に「:method」の形式で結合した文字列||
|SysLogType|80|80（SystemError）固定|

## 使用例

下記の例では、サイトID 2 の「期限付きテーブル」にタイトルが "プリザンターのバージョンアップについて" のレコードを作成し、作成に失敗した場合にログ出力します。

##### JavaScript

``` javascript linenums="1"
const siteId = 2;
const item = items.NewIssue();
item.Title = 'プリザンターのバージョンアップについて';
const ret = items.Create(siteId, item);
if (!ret) {
    logs.LogSystemError(`レコードの作成に失敗しました。サイトID:${siteId}`);
}
```

## サンプルコード

??? note "1. 汎用的なログ出力関数"

    `logs`オブジェクトの各メソッドをラップし、デバッグ時と本番時でログ出力を切り分けられる汎用ロガーのサンプルコードです。

    ##### 機能要件

    1.  デバッグフラグによる出力制御
        `DEBUG_MODE`（bool）を `true` にした場合のみ `logger.debug()` が出力される。`false` の場合は完全に抑制される。

    2.  出力先の一元管理

        `LOG_TARGET`（console / syslogs の bool）で、コンソールとシステムログへの出力をそれぞれ個別にオン・オフできる。設定はスクリプト全体に一括適用される。

    3.  ログレベルの提供

        以下の6メソッドを提供し、それぞれ対応する `logs` メソッドに委譲する。

        | メソッド | 委譲先 | 常時出力 |
        |---|---|:---:|
        | logger.debug() | LogInfo | ✗（デバッグ時のみ）|
        | logger.info() | LogInfo | ✓ |
        | logger.warn() | LogWarning | ✓ |
        | logger.userError() | LogUserError | ✓ |
        | logger.systemError() | LogSystemError | ✓ |
        | logger.exception() | LogException | ✓ |

    ##### JavaScript

    ```javascript linenums="1"
    // ============================================================
    // デバッグモード。true にすると debug() ログが出力される 
    // ============================================================
    const DEBUG_MODE = false;
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
    // ロガー本体
    // ============================================================
    const logger = (function (debugMode, target) {
        /**
         * 内部共通出力関数
         * @param {Function} logFn   - logs オブジェクトのメソッド
         * @param {string}   message - ログメッセージ
         * @param {string}   method  - メソッド名（省略可）
         * @param {boolean}  forceOutput - デバッグモードに関係なく常に出力するか
         */
        function _write(logFn, message, method, forceOutput) {
            if (!forceOutput && !debugMode) return;
            const m = method || '';
            logFn(message, m, target.console, target.syslogs);
        }
        return {
            /**
             * デバッグログ（DEBUG_MODE=true のときのみ Info として出力）
             * @param {string} message
             * @param {string} [method]
             */
            debug: function (message, method) {
                _write(
                    function (msg, mth, con, sys) {
                        logs.LogInfo(msg, mth, con, sys);
                    },
                    '[DEBUG] ' + message,
                    method,
                    false, // デバッグモード時のみ出力
                );
            },
            /**
             * 情報ログ（常に Info として出力）
             * @param {string} message
             * @param {string} [method]
             */
            info: function (message, method) {
                _write(
                    function (msg, mth, con, sys) {
                        logs.LogInfo(msg, mth, con, sys);
                    },
                    message,
                    method,
                    true, // 常に出力
                );
            },
            /**
             * 警告ログ（常に Warning として出力）
             * @param {string} message
             * @param {string} [method]
             */
            warn: function (message, method) {
                _write(
                    function (msg, mth, con, sys) {
                        logs.LogWarning(msg, mth, con, sys);
                    },
                    message,
                    method,
                    true,
                );
            },
            /**
             * ユーザエラーログ（常に UserError として出力）
             * @param {string} message
             * @param {string} [method]
             */
            userError: function (message, method) {
                _write(
                    function (msg, mth, con, sys) {
                        logs.LogUserError(msg, mth, con, sys);
                    },
                    message,
                    method,
                    true,
                );
            },
            /**
             * システムエラーログ（常に SystemError として出力）
             * @param {string} message
             * @param {string} [method]
             */
            systemError: function (message, method) {
                _write(
                    function (msg, mth, con, sys) {
                        logs.LogSystemError(msg, mth, con, sys);
                    },
                    message,
                    method,
                    true,
                );
            },
            /**
             * 例外ログ（常に Exception として出力）
             * catch ブロック内で利用する想定。
             * @param {Error|string} error   - Error オブジェクト、またはメッセージ文字列
             * @param {string}       [method]
             */
            exception: function (error, method) {
                var message;
                if (error && typeof error === 'object' && error.stack) {
                    message = error.message + '\n' + error.stack;
                } else {
                    message = String(error);
                }
                _write(
                    function (msg, mth, con, sys) {
                        logs.LogException(msg, mth, con, sys);
                    },
                    message,
                    method,
                    true,
                );
            },
        };
    })(DEBUG_MODE, LOG_TARGET);
    // ===============
    // 使用例
    // ===============
    // ─── 例1：デバッグ情報（DEBUG_MODE=true のときだけ出力） ───
    logger.debug('処理開始: siteId=' + 1000, 'MyScript');
    // ─── 例2：通常の情報ログ（常に出力） ───
    logger.info('レコードを作成しました。レコードID:' + 9999, 'CreateIssue');
    // ─── 例3：警告ログ ───
    logger.warn('対象レコードが見つかりませんでした。', 'FetchRecord');
    // ─── 例4：ユーザ起因エラー ───
    logger.userError('必須項目が未入力です。', 'Validate');
    // ─── 例5：システムエラー ───
    logger.systemError('APIへの接続に失敗しました。', 'CallApi');
    // ─── 例6：例外処理（catch と組み合わせて使う） ───
    try {
        const item = items.NewIssue();
        item.Title = 'テスト';
        items.Create(2, abcd); // 強制的に例外発生
        logger.info('作成成功', 'CreateIssue');
    } catch (e) {
        logger.exception(e, 'CreateIssue');
    }
    ```

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.12.0 以降|機能追加|

## 関連情報

-   [開発者ガイド：サーバスクリプト：logs](index.md)
-   [開発者ガイド：サーバスクリプト](../index.md)
