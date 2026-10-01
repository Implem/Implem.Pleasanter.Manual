---
title: サービスのアナウンスを表示する
category: アナウンス機能
order: '0'
status: ''
parts: ''
urlstring: announcement-siteid
translationKey: announcement-siteid
shortname: アナウンス
created: 2022-12-15
updated: 2026-02-09
---

## 概要

システムがメンテナンスに入る日時など、利用者全体にアナウンスを出したい場合に利用できるのが「アナウンス機能」です。

アナウンス機能を制御する「期限付きテーブル」を作成し、設定することで機能のオン・オフやデザインの変更などを行えます。以下は、ユーザへの注意喚起のため、赤の背景でアナウンスを掲載した画面例です。

アナウンスが表示された状態（レコードの編集画面）

![赤の背景でアナウンスを掲載したレコードの編集画面](https://pleasanter.org/files/images/ja/users-guide/announcement/assets/d56b42272d954edab6cb19097eef12da.png)

アナウンスはログイン画面にも表示できるため、ログインしていないユーザへの情報伝達も可能です。

アナウンスが表示された状態（ログイン画面）

![画面上部にアナウンスを掲載したログイン画面](https://pleasanter.org/files/images/ja/users-guide/announcement/assets/65571782404e400988728b3ea62e9a10.png)

## 制限事項

Pleasanter.netのフリープラン、ライトプラン、スタンダードプランでは本機能はご利用いただけません。

## アナウンス機能の設定

アナウンス機能を利用するには、以下の準備が必要です。

1.  期限付きテーブルを作成し、以下の項目を設定してください。

    |No.|項目|内容|既定値|
    |:-:|:----|:----|:---:|
    |➊|内容|公開する内容（HTML）|（空欄）|
    |➋|状況|公開状況|200|
    |➌|チェックA|ログイン画面とトップ画面にのみ表示|オフ|
    |➍|チェックB|ログイン画面に表示しない|オフ|
    |➎|チェックC|トップ画面に表示しない|オフ|
    |❻|チェックD|閉じるボタンを表示する|オフ|

2.  ➋[状況項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)の詳細設定で、選択肢を以下のように設定してください。

    ```text
    200,公開中,公,status-inprogress
    900,公開終了,終,status-closed
    ```

3.  設定ファイル[Service.json](../../setup/parameters/service-json.md)のパラメータ「AnnouncementSiteId」を以下のように修正して保存してください。{サイトID}には作成した期限付きテーブルのサイトIDを入力してください。

    ```json
    {
        ～～ 中略 ～～
        "AnnouncementSiteId": {サイトID}, 
        ～～ 中略 ～～
    }
    ```

4.  パラメータファイルの修正が完了したら、プリザンターを再起動してください。
5.  アナウンス用に作成した期限付きテーブルに以下のレコードを作成してください。

    |No.|項目|設定値|
    |:-:|:----|:----|
    |－|タイトル|定期メンテナンスのお知らせ|
    |➊|内容|後述のHTMLの内容|
    |－|開始|公開を開始する日時|
    |－|完了|公開を終了する日時|
    |➋|状況|公開中|
    |➌|ログイン画面とトップ画面にのみ表示|オフ|
    |➍|ログイン画面に表示しない|オフ|
    |➎|トップ画面に表示しない|オフ|
    |❻|閉じるボタンを使用する|オフ|

    内容項目に設定するHTML

    ```html
    <div style="background-color:red;color:white;padding:5px;font-weight:bold;">
        定期メンテナンスのため、2024年8月14日 9:00～12:00 はサービスを停止します。
    </div>
    ```

6.  画面上部にアナウンスが表示されます。HTMLの内容を変更すると表示が変わります。

    ![アナウンス用のレコードを作成した状態](https://pleasanter.org/files/images/ja/users-guide/announcement/assets/fe770065c430497fa20ab3fff2bdb97f.png)

7.  [状況項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)を「公開終了」にすると、アナウンスは非公開となります。

    ![状況項目を公開終了にした状態](https://pleasanter.org/files/images/ja/users-guide/announcement/assets/6535d9946bb94f86a230327d364c347f.png)

    [状況項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-status.md)が「公開中」でも「開始」～[完了項目](../../managers-guide/manage-table/editor/editor-settings/columns/table-management-completion-time.md)の時間に入っていない場合、アナウンスは非公開となります。そのため、開始時間を過ぎると自動的に公開され、完了時間を過ぎると自動的に非公開となります。

## アナウンス機能のオプション

アナウンス機能には、4つのオプション機能があります。オプション機能のオン/オフは、追加した「チェックA」（➌）～「チェックD」（❻）のオン/オフでそれぞれ切り替えられます。

### ➌ログイン画面とトップ画面にのみ表示

アナウンスが全ての画面に表示されると、画面のスクリーンショットを利用する業務の邪魔になる可能性があります。「ログイン画面とトップ画面にのみ表示」のチェックをオンにすると、ログイン画面とトップ画面以外にアナウンスが表示されなくなります。

### ➍ログイン画面に表示しない

アナウンスによっては、ログインしていないユーザに見せたくない場合があります。そのようなケースでは「ログイン画面に表示しない」のチェックをオンにすると、ログイン画面にアナウンスが表示されなくなります。「ログイン画面とトップ画面にのみ表示」と併用することで、トップ画面にのみアナウンスを表示することができます。

### ➎トップ画面に表示しない

アナウンスをトップ画面に表示したくない場合に使用します。「トップ画面に表示しない」のチェックをオンにすると、トップ画面にアナウンスが表示されなくなります。「ログイン画面とトップ画面にのみ表示」と併用することで、ログイン画面にのみアナウンスを表示することができます。

### ➏閉じるボタンを使用する

表示されているアナウンスをユーザの操作によって閉じることを許可したい場合があります。「閉じるボタンを使用する」をオンにして、HTMLに閉じる用のボタンを設置すると、一度確認したアナウンスを非表示にすることができます。HTMLを下図のように書き換えると、画面の右に「×」アイコンが表示されます。 data-id="405"の部分は、レコードのIDにする必要がありますので、一度、作成ボタンを押してIDが割り当てられたあとに修正してください。

```html
<span class="ui-icon ui-icon ui-icon-closethick close-announcement" data-id="405"
    onClick="$p.closeAnnouncement($(this));" 
    style="float:right;margin-right:2px;margin-top:2px;cursor:pointer;" ></span>
<div style="background-color:red;color:white;padding:5px;font-weight:bold;">
　定期メンテナンスのため、2024年8月14日 9:00～12:00 はサービスを停止します。
</div>
```

「×」アイコンをクリックすると、ログアウトするまでの間、アナウンスは表示されなくなります。ログイン画面では「×」アイコンは表示されないため、ログイン画面で非表示にすることはできません。

閉じるボタンを使用するを設定した状態

![「×」アイコンが表示されたアナウンス](https://pleasanter.org/files/images/ja/users-guide/announcement/assets/acda5e9a7fe74e309e92c23936d250cc.png)
