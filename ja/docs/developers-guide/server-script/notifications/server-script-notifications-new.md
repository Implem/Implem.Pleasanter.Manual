---
title: notifications.New
icon: material/alpha-m-box
category: サーバスクリプト
order: '50000'
status: ''
parts: ''
urlstring: server-script-notifications-new
translationKey: server-script-notifications-new
shortname: notifications.New
created: 2021-02-16
updated: 2026-07-27
---

## 概要

通知のオブジェクトを生成します。生成したオブジェクトに通知設定を追加し、任意のタイミングで送信することができます。

## 構文

```
notifications.New()
```

## 戻り値

notificationオブジェクトを返却します。

## 使用例

以下の例では、下記宛先へタイトルが "通知テスト"、内容が "サーバスクリプトから通知しています" の通知を行います。

-   To: xxxxx@example.com
-   Cc: yyyyy@example.com
-   Bcc: zzzzz@example.com

##### JavaScript

```
let notification = notifications.New();
notification.Address = 'xxxxx@example.com';
notification.CcAddress = 'yyyyy@example.com';
notification.BccAddress = 'zzzzz@example.com';
notification.Title = '通知テスト';
notification.Body = 'サーバスクリプトから通知しています。';
notification.Send();
```  

## サンプルコード

??? note "1. 状況・内容に応じて動的なメール通知を行う"

    ##### 概要

    購買申請の状態（ステータス）と申請内容に応じて、件名・本文を動的に組み立て、対象者へメール通知を送信するサンプルコードです。通知は任意で登録したプロセスから起動する想定です。

    ##### 使用フィールド一覧

    以下のような項目を使用します。

    | フィールド | ctx プロパティ | 内容 |
    |---|---|---|
    | model.Title | title | 案件名 |
    | model.ClassA | applicant | 申請者（ユーザIDから氏名に変換） |
    | model.ClassD | creatorMail | 申請者メールアドレス |
    | model.ClassB | - | 承認者 |
    | model.ClassE | approverAddr | 承認者メールアドレス |
    | model.ClassC | - | 購買担当 |
    | model.ClassF | purchaseMgr | 購買担当メールアドレス |
    | model.NumA | amount | 申請金額 |
    | model.DateA | deadline | 希望納期（yyyy/mm/dd 形式に変換） |
    | model.DateB | approved_at | 承認日時（yyyy/mm/dd 形式に変換） |
    | model.Status | status | ステータス（下表参照） |
    | model.CheckA | isUrgent | 至急フラグ |
    | model.CheckB | isReapply | 再申請フラグ |
    | model.DescriptionA | comment | コメント |

    ##### ステータス値の意味

    | 値 | 意味 |
    |---|---|
    | 100 | 承認待ち |
    | 200 | 承認済み |
    | 300 | 差し戻し |
    | 900 | 納品確認待ち |

    ##### メール文面/宛先の編集条件

    件名、ヘッダ、本文、フッタ、宛先を以下の条件で編集します。メール本文は、ヘッダ＋本文＋フッタの構成になります。

    1. 件名

    | 条件 | 件名 |
    |---|---|
    | 至急フラグ ON | 【至急】購買申請の承認依頼：{案件名} |
    | 申請金額 50万円以上 | 【高額案件】購買申請の承認依頼：{案件名} |
    | 上記以外 | 【承認依頼】購買申請：{案件名} |

    > 複数条件が成立する場合は、上から順に最初に一致したものを採用。

    2. ヘッダ

    | 条件 | ヘッダ文面 |
    |---|---|
    | 至急フラグ ON | 緊急対応が必要な購買申請が提出されました。速やかにご確認のうえ、承認または差し戻しをお願いします。 |
    | 申請金額 50万円以上 | 高額な購買申請が提出されました。慎重にご確認のうえ、承認または差し戻しをお願いします。 |
    | 再申請フラグ ON | 前回差し戻しされた申請が修正・再提出されました。変更内容をご確認のうえ、ご対応をお願いします。 |
    | 上記以外 | 新しい購買申請が提出されました。内容をご確認のうえ、ご対応をお願いします。 |

    > 複数条件が成立する場合は、上から順に最初に一致したものを採用。

    3. 本文

    | 条件（ステータス） | 本文内容 |
    |---|---|
    | 100：承認待ち | 申請内容（案件名・申請者・申請金額・希望納期） |
    | 200：承認済み | 承認結果（案件名・申請金額・承認日時） |
    | 300：差し戻し | 差し戻し通知（案件名・申請金額・コメント参照を促す） |
    | 900：納品確認 | 納品確認依頼（案件名・申請金額・納品日） |

    > comment フィールドに値がある場合は、本文末尾に「■ コメント」セクションを追加。

    4. フッタ

    | 送信対象 | フッタ文面 |
    |---|---|
    | 承認者 | 承認はシステムにログインして行ってください。期限までに対応がない場合は自動リマインドが送信されます。 |
    | 申請者 | 申請内容の確認・修正はシステムよりお願いします。不明な点は購買担当までお問い合わせください。 |
    | 購買担当 | 発注処理はシステムの購買管理画面から行ってください。対応期限にご注意ください。 |

    5. 宛先

    | 送信対象 | 送信条件 |
    |---|---|
    | 承認者（ClassE） | ステータスが 100（承認待ち）または 300（差し戻し）、かつアドレスが設定されている |
    | 申請者（ClassD） | ステータスが 200（承認済み）または 300（差し戻し）、かつアドレスが設定されている |
    | 購買担当（ClassF） | ステータスが 200（承認済み）または 900（納品確認）、かつアドレスが設定されている |

    > 条件を満たす宛先が複数ある場合は、それぞれに個別のメールが送信される（ステータス 200 では申請者・購買担当の両方に送信）。

    ##### 送信メールイメージ

    ```text
    ＊＊件名＊＊

    【承認依頼】購買申請：モニター購入（開発部10台）

    ＊＊内容＊＊

    新しい購買申請が提出されました。
    内容をご確認のうえ、ご対応をお願いします。

    ■ 申請内容
      案件名　：モニター購入（開発部10台）
      申請者　：高橋 一郎
      申請金額：480,000 円
      希望納期：2026/04/15

    承認はシステムにログインして行ってください。
    期限までに対応がない場合は自動リマインドが送信されます。
    ```

    ##### JavaScript
    ```javascript
    // ----------------------------------------------------------------
    // 【定義体】件名・ヘッダ・本文内容・フッタの文面
    // ----------------------------------------------------------------
    const SUBJECT_DEF = {
        urgent: (vars) => `【至急】購買申請の承認依頼：${vars.title}`,
        high_amount: (vars) => `【高額案件】購買申請の承認依頼：${vars.title}`,
        normal: (vars) => `【承認依頼】購買申請：${vars.title}`,
    };
    const HEADER_DEF = {
        urgent:
            '緊急対応が必要な購買申請が提出されました。\n' +
            '速やかにご確認のうえ、承認または差し戻しをお願いします。\n',
        high_amount:
            '高額な購買申請が提出されました。\n' +
            '慎重にご確認のうえ、承認または差し戻しをお願いします。\n',
        reapply:
            '前回差し戻しされた申請が修正・再提出されました。\n' +
            '変更内容をご確認のうえ、ご対応をお願いします。\n',
        normal:
            '新しい購買申請が提出されました。\n' +
            '内容をご確認のうえ、ご対応をお願いします。\n',
    };
    const BODY_DEF = {
        waiting: (vars) =>
            '■ 申請内容\n' +
            `  案件名　：${vars.title}\n` +
            `  申請者　：${vars.applicant}\n` +
            `  申請金額：${vars.amount} 円\n` +
            `  希望納期：${vars.deadline}\n`,
        approved: (vars) =>
            '■ 承認結果\n' +
            '  ステータス：承認済み\n' +
            `  案件名　　：${vars.title}\n` +
            `  申請金額　：${vars.amount} 円\n` +
            `  承認日時　：${vars.approved_at}\n`,
        rejected: (vars) =>
            '■ 差し戻し通知\n' +
            `  案件名　：${vars.title}\n` +
            `  申請金額：${vars.amount} 円\n` +
            '  差し戻し理由・修正依頼は下記コメントをご確認ください。\n',
        delivery: (vars) =>
            '■ 納品確認依頼\n' +
            `  案件名　：${vars.title}\n` +
            `  申請金額：${vars.amount} 円\n` +
            `  納品日　：${vars.deadline}\n` +
            '  ※ 納品確認後、速やかに検収処理をお願いします。\n',
    };
    const FOOTER_DEF = {
        approver:
            '\n承認はシステムにログインして行ってください。\n' +
            '期限までに対応がない場合は自動リマインドが送信されます。\n',
        applicant:
            '\n申請内容の確認・修正はシステムよりお願いします。\n' +
            '不明な点は購買担当までお問い合わせください。\n',
        purchase_mgr:
            '\n発注処理はシステムの購買管理画面から行ってください。\n' +
            '対応期限にご注意ください。\n',
    };
    // ----------------------------------------------------------------
    // 【定義体】キー判定ルール（RULE_DEF）
    // ----------------------------------------------------------------
    const RULE_DEF = {
        // 件名の判定ルール（3パターン）
        subject: {
            fallback: 'normal',
            rules: [
                {
                    key: 'urgent',
                    when: (ctx) => ctx.isUrgent,
                },
                {
                    key: 'high_amount',
                    when: (ctx) => ctx.amount >= 500000,
                },
            ],
        },
        // ヘッダの判定ルール（4パターン）
        header: {
            fallback: 'normal',
            rules: [
                {
                    key: 'urgent',
                    when: (ctx) => ctx.isUrgent,
                },
                {
                    key: 'high_amount',
                    when: (ctx) => ctx.amount >= 500000,
                },
                {
                    key: 'reapply',
                    when: (ctx) => ctx.isReapply,
                },
            ],
        },
        // 本文内容の判定ルール（4パターン）
        body: {
            fallback: 'waiting',
            rules: [
                {
                    key: 'waiting',
                    when: (ctx) => ctx.status === 100,
                },
                {
                    key: 'approved',
                    when: (ctx) => ctx.status === 200,
                },
                {
                    key: 'rejected',
                    when: (ctx) => ctx.status === 300,
                },
                {
                    key: 'delivery',
                    when: (ctx) => ctx.status === 900,
                },
            ],
        },
        // 送信先ごとのフッタ・送信条件の定義（3パターン）
        recipients: [
            {
                footerKey: 'approver',
                address: (ctx) => ctx.approverAddr,
                sendWhen: (ctx) =>
                    (ctx.status === 100 || ctx.status === 300) &&
                    !!ctx.approverAddr,
            },
            {
                footerKey: 'applicant',
                address: (ctx) => ctx.creatorMail,
                sendWhen: (ctx) =>
                    (ctx.status === 200 || ctx.status === 300) && !!ctx.creatorMail,
            },
            {
                footerKey: 'purchase_mgr',
                address: (ctx) => ctx.purchaseMgr,
                sendWhen: (ctx) =>
                    (ctx.status === 200 || ctx.status === 900) && !!ctx.purchaseMgr,
            },
        ],
    };
    // ユーティリティ
    function toYmd(d) {
        const y = d.getFullYear();
        const m = String(d.getMonth() + 1).padStart(2, '0');
        const day = String(d.getDate()).padStart(2, '0');
        return `${y}/${m}/${day}`;
    }
    function getUserName(userId) {
        const user = users.Get(userId);
        return user.Name;
    }
    // ================================================================
    // 汎用エンジン：ルール定義を走査してキーを決定する
    // ================================================================
    function resolveKey(ruleDef, ctx) {
        for (const rule of ruleDef.rules) {
            if (rule.when(ctx)) {
                return rule.key;
            }
        }
        return ruleDef.fallback;
    }
    // ================================================================
    // メイン処理
    // ================================================================
    function sendMailMain() {
        // --- コンテキスト（レコード値）をまとめる ---
        const ctx = {
            title: model.Title,
            applicant: getUserName(model.ClassA),
            approverAddr: model.ClassE,
            purchaseMgr: model.ClassF,
            amount: model.NumA,
            deadline: toYmd(model.DateA),
            approved_at: toYmd(model.DateB),
            status: model.Status,
            isUrgent: model.CheckA,
            isReapply: model.CheckB,
            comment: model.DescriptionA,
            creatorMail: model.ClassD,
        };
        // --- プレースホルダ用の値マップ ---
        const vars = {
            title: ctx.title,
            applicant: ctx.applicant,
            amount: Number(ctx.amount).toLocaleString('ja-JP'),
            deadline: ctx.deadline,
            approved_at: ctx.approved_at,
        };
        // --- ルールエンジンでキーを決定 ---
        const subjectKey = resolveKey(RULE_DEF.subject, ctx);
        const headerKey = resolveKey(RULE_DEF.header, ctx);
        const bodyKey = resolveKey(RULE_DEF.body, ctx);
        // --- 件名を生成 ---
        const subject = SUBJECT_DEF[subjectKey](vars);
        logs.LogInfo(`生成した件名: ${subject}`, 'MainProcess');
        // --- 本文を組み立てる関数（フッタキーを引数で切り替え）---
        function buildBody(footerKey) {
            let body = HEADER_DEF[headerKey] + '\n' + BODY_DEF[bodyKey](vars);
            if (ctx.comment && ctx.comment.trim() !== '') {
                body += '\n■ コメント\n  ' + ctx.comment + '\n';
            }
            body += FOOTER_DEF[footerKey];
            return body;
        }
        // --- 送信先ルールをループして通知送信 ---
        for (const r of RULE_DEF.recipients) {
            if (!r.sendWhen(ctx)) continue;
            const n = notifications.New();
            n.Address = r.address(ctx);
            n.Title = subject;
            n.Body = buildBody(r.footerKey);
            n.Send();
        }
    }
    switch (context.ControlId) {
        // ControlIdで実行されたプロセスを判断
        case 'Process_1':
            // プロセスID：1の処理
            sendMailMain();
            break;
        default:
            // 何もしない
            break;
    }
    ```

## 注意事項

こちらは[サーバスクリプト](../index.md)で使用するメソッドです。[スクリプト](../../../managers-guide/manage-table/scripts/index.md)では使用できません。

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.4.10.0 以降|notificationオブジェクトにプロパティCcAddress、BccAddressを追加|

## 関連情報

-   [テーブルの管理：サーバスクリプト](../../../managers-guide/manage-table/server-script/index.md)  
-   [オブジェクトごとの実行タイミング](../basics/server-script-conditions.md)  
-   [notificationsオブジェクト](index.md)   
-   [notificationオブジェクト](../notification/index.md)  
-   [notifications.Getメソッド](server-script-notifications-get.md)