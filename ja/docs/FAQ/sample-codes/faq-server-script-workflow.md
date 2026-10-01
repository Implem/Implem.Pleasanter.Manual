---
title: 稟議申請などのワークフロー（承認プロセス）をサーバスクリプトで実現する
category: FAQ：サンプルコード集
order: '6'
status: ''
parts: ''
urlstring: faq-server-script-workflow
translationKey: faq-server-script-workflow
shortname: ''
created: 2021-02-19
updated: 2024-08-08
---

## 説明

稟議申請などで用いられる承認ワークフロー（プロセス管理）機能を、サーバスクリプトを用いて実装します。  
当ページでの説明は、申請者が所属している組織（部署）の、決裁者グループに所属しているユーザが承認処理を行うものとし、幹部社員はグループID：3、上級幹部社員はグループID：4となります。1,000,000円を超える稟議申請の場合、決裁者は役員となり、役員は組織ID：2に所属しているものとします。

※ここで説明するワークフロー機能を実装したテーブルは、サイトパッケージを公開しています。  
以下のページで、データのダウンロード、および使用手順を説明しております。  
[FAQ:稟議申請ワークフローの例のサイトパッケージをインポートする](faq-server-script-workflow-site-package.md)

## 概要

申請者の所属部署、申請金額に応じて承認ルートを自動で設定し、承認プロセスの管理を行います。  
決裁者は、申請金額が200,000円未満の場合は申請者が所属する部署の幹部社員のみ。200,000円以上、1,000,000円未満の場合は幹部社員に加えて上級幹部、1,000,000円以上の場合は更に役員の承認が必要となる承認ルートが設定されます。  
稟議申請が登録された時点で、該当する決裁者にはメールにて通知が送られます。  
処理のフローとしては以下となります。

1.  申請者の所属部署・申請金額から決裁ルートを自動設定
1.  決裁者へのメール通知
1.  承認時のプロセス更新（次の決裁者宛に更新）
1.  承認された申請を読取専用として更新

![申請から決裁までの処理の流れを示した図](https://pleasanter.org/files/images/ja/FAQ/sample-codes/assets/cd598f23a9c44774910395ba57bc82cb.png)

## スクリプト構成

ワークフロー機能の実装は以下6つのサーバスクリプトで構成されます。

| タイトル                 | 条件               |
| :----------------------- | :----------------- |
| 決裁ルートの自動選択     | レコード読み込み時 |
| 承認時のプロセス更新     | 更新前             |
| 自動メール通知           | 更新後             |
| 決裁ルートに伴う画面表示 | 画面表示の前       |
| 承認・否決ボタンの設置   | 画面表示の前       |
| 完了したものは読取専用   | 画面表示の前       |

![登録するサーバスクリプトの一覧](https://pleasanter.org/files/images/ja/FAQ/sample-codes/assets/247dd64577d94c81b109d699dc0d5470.png)

## 決裁ルートの自動選択

条件：レコード読み込み時

### 処理の流れ

-   入力された金額によって承認ルートを設定します。  
    →modelオブジェクト
-   幹部社員の所属するグループから、申請者が所属する組織の幹部ユーザを取得します。  
    →groupsオブジェクト、GetMembersメソッド
-   役員の承認が必要なルートの場合、役員の組織から役員ユーザを取得します。  
    →deptsオブジェクト、GetMembersメソッド
-   取得したユーザのIDを各承認者の分類項目にセットします。  
    →modelオブジェクト
-   最終承認時のステータスコードをメモリ上に保持します。  
    →context.UserData.FinCodeプロパティ

``` js linenums="1"
try {
    context.Log('決裁ルートの自動選択');
    if (model.NumA < 200000) {
        context.UserData.FinCode = 300;
        model.ClassB = manager(context.DeptId, 3).UserId;
    } else if (model.NumA < 1000000) {
        context.UserData.FinCode = 400;
        model.ClassB = manager(context.DeptId, 3).UserId;
        model.ClassC = manager(context.DeptId, 4).UserId;
    } else {
        context.UserData.FinCode = 900;
        model.ClassB = manager(context.DeptId, 3).UserId;
        model.ClassC = manager(context.DeptId, 4).UserId;
        model.ClassD = officer().UserId;
    }

    function manager(deptId, groupId) {
        let members = groups.Get(groupId).GetMembers();
        for (let member of members) {
            if (member.UserId > 0) {
                let user = users.Get(member.UserId);
                if (user.DeptId === context.DeptId) {
                    return user;
                }
            }
        }
    }

    function officer () {
        let users = depts.Get(2).GetMembers()
        for (let user of users) {
            return user;
        }
    }
} catch (e){
    context.Log(e.stack);
}
```

## 承認時のプロセス更新

条件：更新前

### 処理の流れ

-   ユーザが操作したボタンのID属性を取得して分岐します。  
    →context.ControlIdプロパティ
-   次のプロセスのステータスコードをセットします。  
    →model.Statusプロパティ
-   次のプロセスの決裁者をセットします。  
    →model.Managerプロパティ
-   決裁した日をセットします。  
    →model.DateXプロパティ
-   最終承認が行われた場合には現在位置を申請者に戻します。  
    →最終承認はcontext.UserData.FinCodeで確認

``` js linenums="1"
try {
    context.Log('承認時のプロセス更新');
    switch (context.ControlId) {
        case 'Approval':
            model.Status = 200;
            model.Manager = manager(model.ClassB);
            break;
        case 'ApprovalM1':
            model.Status = status(300);
            model.Manager = manager(model.ClassC);
            model.DateB = new Date();
            break;
        case 'ApprovalM2':
            model.Status = status(400);
            model.Manager = manager(model.ClassD);
            model.DateC = new Date();
            break;
        case 'ApprovalM3':
            model.Status = status(900);
            model.DateD = new Date();
            break;
    }
    if (model.Status === 900) {
        model.Manager = model.Owner;
    }

    function status(code) {
        if (context.UserData.FinCode === code) {
            return 900;
        } else {
            return code;
        }
    }

    function manager(userId) {
        var user = users.Get(userId);
        if (user) {
            return user.UserId;
        } else {
            return model.Manager;
        }
    }
} catch (e) {
    context.Log(e.stack);
}
```

## 自動メール通知

条件：更新後

### 処理の流れ

-   通知用のオブジェクトを作成します。  
    →notifications.New()メソッドで作成
-   現在のプロセスのユーザIDを指定しメールアドレスを取得します。  
    →notification.Address = ‘[User’ + user.UserId + ‘]’
-   承認依頼、可決、否決のプロセスで分岐しメッセージを設定します。  
    →model.Statusプロパティ
-   タイトル、本文を指定して通知メールを送信します。  
    →notification.Title、notification.Body、 notification.Send()

``` js linenums="1"
try {
    context.Log('自動メール通知');
    let user = users.Get(model.Manager);
    let notification = notifications.New();
    if (user.UserId > 0) {
        notification.Address = '[User' + user.UserId + ']';
        switch (model.Status) {
            case 200:
            case 300:
            case 400:
                notification.Title = '承認依頼：' + model.Title;
                notification.Body = user.Name + '殿：掲題の承認依頼が届いています。';
                notification.Send();
                break;
            case 900:
                notification.Title = '可決：' + model.Title;
                notification.Body = user.Name + '殿：掲題の申請が可決されました。';
                notification.Send();
                break;
            case 920:
                notification.Title = '否決：' + model.Title;
                notification.Body = user.Name + '殿：掲題の申請が否決されました。';
                notification.Send();
                break;
        }
    }
} catch (e){
    context.Log(e.stack);
}
```

## 決裁ルートに伴う画面表示

条件：画面表示の前

### 処理の流れ

-   最終承認時のステータスコードで分岐します。  
    →context.UserData.FinCodeプロパティ
-   承認に不要な決裁レベルの入力欄「セクション」を非表示にします。  
    →siteSettings.Sections[n].Hide = true

``` js linenums="1"
try {
    context.Log('決裁ルートに伴う画面表示');
    switch (context.UserData.FinCode) {
        case 300:
            siteSettings.Sections[3].Hide = true;
            siteSettings.Sections[4].Hide = true;
            break;
        case 400:
            siteSettings.Sections[4].Hide = true;
            break;
        case 900:
            break;
        default:
            siteSettings.Sections[2].Hide = true;
            siteSettings.Sections[3].Hide = true;
            siteSettings.Sections[4].Hide = true;
    }
} catch (e){
    context.Log(e.stack);
}
```

## 承認・否決ボタンの設置

条件：画面表示の前

### 処理の流れ

-   現在のプロセスで分岐します。  
    →model.Statusプロパティ
-   現在の承認レベルの欄にボタンを表示します。  
    →columns.ColumnName.ExtendedHtmlAfterFieldプロパ ティ
-   HtmlにボタンのID、Confirm、表示名、アイコンを入力します。

``` js linenums="1"
try {
    context.Log('承認・否決ボタンの設置');
    if (model.Manager === context.UserId) {
        switch (model.Status) {
            case 100:
                if (context.Action !== 'new') {
                    columns.AttachmentsA.ExtendedHtmlAfterField = buttons('', '申請');
                }
                break;
            case 200:
                columns.DescriptionB.ExtendedHtmlAfterField = buttons('M1', '幹部承認');
                break;
            case 300:
                columns.DescriptionC.ExtendedHtmlAfterField = buttons('M2', '上級幹部承認');
                break;
            case 400:
                columns.DescriptionD.ExtendedHtmlAfterField = buttons('M3', '役員承認');
                break;
        }
    }

    function buttons(suffix, text) {
        let html = '<div class="approval-control"><button id="Approval' + suffix + '" class="button button-icon validate" type="button" onclick="if (!confirm(\'' + text + 'してよろしいですか?\')) return false;$p.send($(this));" data-icon="ui-icon-circle-triangle-e" data-action="Update" data-method="put">' + text + '</button></div>';
        if (suffix !== '') {
            html += '<div class="approval-control"><button id="Veto' + suffix + '" class="button button-icon validate" type="button" onclick="if (!confirm(\'否決してしてよろしいですか?\')) return false;$p.send($(this));" data-icon="ui-icon-circle-close" data-action="Update" data-method="put">否決</button></div>';
        }
        return html;
    }
} catch (e){
    context.Log(e.stack);
}
```

## 完了したものは読取専用

条件：画面表示の前

### 処理の流れ

-   現在のプロセスで完了をチェックします。  
    →model.Statusプロパティ
-   完了の場合、読取専用をオンに設定します。  
    →model.ReadOnly = true

``` js linenums="1"
try {
    context.Log('完了したものは読取専用');
    if (model.Status === 900) {
        model.ReadOnly = true;
    }
} catch (e) {
    context.Log(e.stack);
}
```

## 注意事項

こちらは[サーバスクリプト](../../managers-guide/manage-table/server-script/index.md)機能で使用するメソッドです。[スクリプト](../../managers-guide/manage-table/scripts/index.md)機能では使用できません。

## 関連情報

-   [FAQ:稟議申請ワークフローの例のサイトパッケージをインポートする](faq-server-script-workflow-site-package.md)
-   [オブジェクトごとの実行タイミング](../../developers-guide/server-script/basics/server-script-conditions.md)
-   [siteSettingsオブジェクト](../../developers-guide/server-script/siteSettings/index.md)
-   [contextオブジェクト](../../developers-guide/server-script/context/index.md)
-   [itemsオブジェクト](../../developers-guide/server-script/items/index.md)
-   [modelオブジェクト](../../developers-guide/server-script/model/index.md)
-   [apiModelオブジェクト](../../developers-guide/server-script/apiModel/index.md)
-   [notificationsオブジェクト](../../developers-guide/server-script/notifications/index.md)
-   [FAQ:サーバスクリプトのログを出力する](../features-for-developers/faq-server-script-log.md)
