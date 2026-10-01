---
title: 編集画面から添付ファイル付きのメールを送信したい
category: FAQ：編集画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-sendmail-with-attachments
translationKey: faq-sendmail-with-attachments
shortname: メール送信API
created: 2021-08-13
updated: 2026-08-17
---

## 回答

[スクリプト](../../managers-guide/manage-table/scripts/index.md)で[メール送信API](../../developers-guide/api/mail/index.md)、[添付ファイル取得API](../../developers-guide/api/table-operations/api-attachment-get.md)を使用してください。

---

## 概要

[メール送信API](../../developers-guide/api/mail/index.md)、[添付ファイル取得API](../../developers-guide/api/table-operations/api-attachment-get.md)を使用して[添付ファイル項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)(AttachmentsA)に登録されたファイルを添付してメールを送信するサンプルコードです。

## 前提条件

1.  [メールの送信設定](../../setup/additional/notifications/smtp-mail.md)が必要です。
1.  「Pleasanter.net」では「スタンダードプラン」のご契約が必要です。
1.  設定を行うには「サイトの管理権限」が必要です。

## 動作イメージ

送信処理は、拡張HTMLで設置した送信ボタンのクリック時に実行されます。To:、Cc:、Bcc:、件名、本文はそれぞれ該当する項目(同じ表示名の項目)の値がセットされます。

![拡張HTMLで送信ボタンを設置した編集画面の動作イメージ](https://pleasanter.org/files/images/ja/FAQ/editor/assets/34c7a795330846ac85a5ff9d0df69e9f.png)

## 操作手順

1.  テーブルを作成してください。
1.  [スクリプト](../../managers-guide/manage-table/scripts/index.md)を新規作成し、以下のスクリプトの内容を記載してください。 出力先には「編集」をチェックして追加ボタンをクリックします。
1.  [エディタ](../../users-guide/table/record-authoring/edit-records/table-editor.md)から、以下のサンプルコードにあわせて、添付ファイルAを有効化してください。
1.  添付ファイルAの詳細設定で[拡張HTML](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/extended-HTML/index.md)タブを開き、以下のHTMLを記載し、更新ボタンをクリックしてください。
1.  [+新規作成]ボタンをクリックし、新たにレコードを作成してください。
1.  添付ファイルに任意のファイルを登録し、作成ボタンをクリックしてください。
1.  送信ボタンをクリックし、メールが送信されることを確認してください。

## サンプルコード

``` html title="HTML" linenums="1"
<button id="SendOutgoingMail" type="button" class="clearfix add-btn ui-button ui-corner-all ui-widget">
    <span class="ui-button-icon ui-icon ui-icon-mail-closed"></span>
    <span class="ui-button-icon"></span>
    送信
</button>
```

``` js title="JavaScript" linenums="1"
$p.ex.sendMailWithAttachments = function () {
    const toString = 'To:';
    const ccString = 'Cc:';
    const bccString = 'Bcc:';
    const titleString = '件名';
    const bodyString = '本文';
    const mailFormaterElementName = 'メールフォーマット';
    const errorFormChanged = '送信前に更新ボタンを押してレコードの最新の内容を保存してください';
    const errorGetMail = 'メールデータ取得に失敗しました';
    const errorSendMail = 'メール送信処理に失敗しました';
    const errorSelectedMailFormat = '選択したメールフォーマットデータの取得に失敗しました/n進捗状況が変更されませんので営サポまでお声がけください';

    let postAttachmentsHash = [];

    if ($p.formChanged == 'undefined' || $p.formChanged) {
        alert(errorFormChanged);
        return;
    }

    if (window.confirm('以下の内容でメールを送信します')) {

        // 各項目のデータを取得
        let to = $p.getControl(toString).val();
        let cc = $p.getControl(ccString).val();
        let bcc = $p.getControl(bccString).val();
        let title = $p.getControl(titleString).val();
        let body = $p.getControl(bodyString).val();
        let attachments = [];
        let id = $p.id();
        let apiSendMailUrl = $p.apiSendMailUrl(id);
        let isOkResponseData = function(data) {
            let isOk = true;
            if(data == null || data == undefined 
                || data.Response == null || data.Response == undefined 
                || data.Response.Data[0] == null || data.Response.Data[0] == undefined) {
                isOk = false;
            }
            return isOk;
        }
        let isEmpty = function(str) {
            let isEmpty = false;
            if(str == null || str == undefined || str.trim().length <= 0) {
                isEmpty = true;
            }
            return isEmpty;
        }
        $p.apiGet({
            'id': id,
            'done': function (data) {
                if (!isOkResponseData(data)) {
                    alert(errorGetMail);
                    return;
                }
                // メールに添付する添付ファイルを格納する項目を定義
                let AttachmentsA = data.Response.Data[0].AttachmentsHash.AttachmentsA;
                let attachmentList = AttachmentsA;

                let createAttachments = async function () {
                    return new Promise((attachmentsResolve, attachmentsReject) => {
                        if (attachmentList.length == 0) {
                            attachmentsResolve();
                        }
                        try {
                            (async () => {
                                for (let i = 0; i < attachmentList.length; i++) {
                                    await new Promise((getResolve, reject) => {
                                        postAttachmentsHash[i] = {
                                            'Guid': attachmentList[i].Guid,
                                            'Deleted': 1,
                                        };
                                        // 下の変数urlのパスは環境によって異なりますので適宜変更してください。
                                        let url = '/binaries/' + attachmentList[i].Guid + '/download';
                                        let xhr = new XMLHttpRequest();
                                        xhr.open('GET', url, true);
                                        xhr.setRequestHeader('Content-Type','application/json');
                                        xhr.responseType = 'arraybuffer';
                                        xhr.onload = function (oEvent) {
                                            if (xhr.readyState == 4 && xhr.status == 200) {
                                                let bytes = new Uint8Array(xhr.response);
                                                let binaryString = '';
                                                for (let i = 0; i < bytes.byteLength; i++) {
                                                    binaryString += String.fromCharCode(bytes[i]);
                                                }
                                                let base64 = window.btoa(binaryString);
                                                let obj = {};
                                                obj.Name = attachmentList[i].Name;
                                                obj.Base64 = base64;
                                                obj.ContentType = xhr.getResponseHeader('content-type');
                                                attachments[i] = obj;
                                                getResolve();
                                                if (i == attachmentList.length - 1) {
                                                    attachmentsResolve();
                                                }
                                            }
                                        }
                                        xhr.send();
                                    });
                                }
                            })();
                        } catch (error) {
                            attachmentsReject(error);
                        }
                    })
                };

                createAttachments().then(function (value) {
                    let postData = {
                        To: to,
                        Cc: cc,
                        Bcc: bcc,
                        Title: isEmpty(title) ? ' ' : title,
                        Body: isEmpty(body) ? ' ' : body,
                        Attachments: attachments
                    };
                    console.log(postData);

                    $.ajax({
                        url: apiSendMailUrl,
                        type: 'post',
                        async: false,
                        cache: false,
                        data: JSON.stringify(postData),
                        contentType: 'application/json',
                        dataType: 'json'
                    })
                        .done(function (json, textStatus, jqXHR) {
                        })
                        .fail(function (jqXHR, textStatus, errorThrown) {
                            alert(errorSendMail);
                        })
                        .always(function () {
                        })
                })
            },
            'fail': function (data) {
                alert(errorGetMail);
            },
            'always': function (data) {
            },
            'async': false
        });
    }
}

// メール送信ボタンが押されたら処理を実行
$(document).on('click', "#SendOutgoingMail", function () {
    $p.ex.sendMailWithAttachments();
})
```

## 関連情報

-   [テーブルの管理：スクリプト](../../managers-guide/manage-table/scripts/index.md)
-   [開発者ガイド：API：メール：メール送信](../../developers-guide/api/mail/index.md)
-   [開発者ガイド：API：テーブル操作：添付ファイル取得](../../developers-guide/api/table-operations/api-attachment-get.md)
-   [テーブルの管理：項目：添付ファイル](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-attachments.md)
-   [プリザンターからメールを送信できるように設定する](../../setup/additional/notifications/smtp-mail.md)
-   [テーブル機能：レコードのエディタ画面](../../users-guide/table/record-authoring/edit-records/table-editor.md)
-   [テーブルの管理：エディタ：項目の詳細設定：拡張HTML](../../managers-guide/manage-table/editor/editor-settings/advanced-settings/extended-HTML/index.md)
