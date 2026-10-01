---
title: columns.AddChoiceHash
icon: material/alpha-m-box
category: サーバスクリプト
order: '6010'
status: ''
parts: ''
urlstring: server-script-columns-add-choice-hash
translationKey: server-script-columns-add-choice-hash
shortname: columns.AddChoiceHash
created: 2021-09-26
updated: 2026-06-29
---

## 概要

[columns](index.md)オブジェクトの「AddChoiceHashメソッド」です。[サーバスクリプト](../index.md)で[項目](../../../managers-guide/manage-table/editor/editor-settings/columns/index.md)の[選択肢一覧](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)を動的に設定することができます。AddChoiceHashを複数回呼ぶことによって、選択肢を追加します。1回目のAddChoiceHashが呼ばれると[サーバスクリプト](../index.md)の実行前にセットされていた選択肢は全てクリアされます。

## 制限事項

1. [分類項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)のみ使用できます。

## 前提条件

1. 対象となる項目の選択肢一覧に、選択肢が1つ以上設定されている必要があります。
1. サーバスクリプトの[条件](../../../FAQ/editor/faq-condition-mode-range.md)が「画面表示の前」、「行表示の前」の場合に有効となります。

## 構文

``` javascript
columns.[カラム名].AddChoiceHash(key, value);
```

## パラメータ

パラメータvalueを省略した場合、AddChoiceHash(key, key)と解釈されます。

|No|パラメータ|型|必須|概要|
|:--|:--|:-:|:-:|:--|
|1|key|object|○|キー|
|2|value|object| - |値|

## 戻り値

戻り値はありません。

## 使用例

下記の例では、分類AにTEST1～TEST5までの選択肢一覧を設定します。

### valueを指定した場合

##### JavaScript

```js linenums="1"
for (let i = 1; i <= 5; i++) {
    columns.ClassA.AddChoiceHash(i, 'TEST' + i);
}
```

この場合、[分類項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)の[選択肢一覧](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)を以下のように指定した場合と同じ表示結果を得られます。

![valueを指定した場合と同じ結果になる選択肢一覧の設定](https://pleasanter.org/files/images/ja/developers-guide/server-script/columns/assets/996d50bfbff547c6a79518193503ea94.png)

### valueを省略した場合

##### JavaScript

```js linenums="1"
for (let i = 1; i <= 5; i++) {
    columns.ClassA.AddChoiceHash('TEST' + i);
}
```

この場合、[分類項目](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)の[選択肢一覧](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)を以下のように指定した場合と同じ表示結果を得られます。

![valueを省略した場合と同じ結果になる選択肢一覧の設定](https://pleasanter.org/files/images/ja/developers-guide/server-script/columns/assets/975c461c6a7b44b796f874cee682b4d5.png)

## サンプルコード

??? note "1. 選択肢を動的に制御"

    ある項目の入力値に応じて、選択肢を動的に制御します。

    このサンプルでは、分類Aに指定された値に応じ、スクリプト内で定義した条件にあわせ分類Bの選択肢を設定しています。

    ### テーブル設定

    分類Aの設定

    ![サンプルで使う分類Aの設定](https://pleasanter.org/files/images/ja/developers-guide/server-script/columns/assets/f648fbd79f2f475a83bcb067f1f0e5f7.png)

    分類Bの設定

    ![サンプルで使う分類Bの設定](https://pleasanter.org/files/images/ja/developers-guide/server-script/columns/assets/d8b091de94b8420b8ea02a2ab72aa93c.png)

    ### 未選択状態

    分類Bには何も表示されない

    ![分類Aが未選択で、分類Bに何も表示されない状態](https://pleasanter.org/files/images/ja/developers-guide/server-script/columns/assets/340cbb6b50e0483994811a00704e6ba7.png)

    ### 選択状態

    分類Aの選択に合わせ選択肢が表示される

    ![分類Aの選択に合わせて分類Bに選択肢が表示された状態](https://pleasanter.org/files/images/ja/developers-guide/server-script/columns/assets/80fbf46bdc4a4216b8309592b9bedbb7.png)

    ![分類Aの選択に合わせて分類Bに選択肢が表示された状態（別の例）](https://pleasanter.org/files/images/ja/developers-guide/server-script/columns/assets/71a27a3fbece460282ab77fff88875b0.png)

    ##### JavaScript

    ```js linenums="1"
    // 1) 選択肢セット（共通定義）
    const choiceSets = {
        G1: [
            { key: 1, value: '選択肢１' },
            { key: 2, value: '選択肢２' },
            { key: 3, value: '選択肢３' },
            { key: 4, value: '選択肢４' },
        ],
        G2: [
            { key: 2, value: '選択肢２' },
            { key: 4, value: '選択肢４' },
        ],
        G3: [
            { key: 4, value: '選択肢４' },
            { key: 5, value: '選択肢５' },
        ],
    };
    // 2) 選択肢セットキー
    const classAToSetKey = {
        1: 'G1',
        2: 'G2',
        3: 'G3',
        4: 'G3',
    };
    // 3) メイン処理
    // ClassB の選択肢をクリアしてから、ClassA に応じた選択肢をセット
    columns.ClassB.ClearChoiceHash();
    const setKey = classAToSetKey[model.ClassA];
    const choices = setKey && choiceSets[setKey] ? choiceSets[setKey] : [];
    for (const { key, value } of choices) {
        columns.ClassB.AddChoiceHash(key, value);
    }
    ```

??? note "2. グループ・組織に所属するメンバーを選択肢に設定する"

    グループ、組織を選択肢として設定しておき、その選択にあわせ所属するメンバーを別の選択肢項目へ設定します。

    このサンプルでは、以下のように制御しています。

    -   分類A：グループ → 所属メンバーを分類Bに設定
 
        テーブルの設定は以下のとおり。

        分類A

        ![サンプルで使う分類A（グループ）の設定](https://pleasanter.org/files/images/ja/developers-guide/server-script/columns/assets/8cb3a172f9684f388d4df831d99d422e.png)

        分類B

        ![サンプルで使う分類B（所属メンバー）の設定](https://pleasanter.org/files/images/ja/developers-guide/server-script/columns/assets/425caf0841a940d79a041ced9897c2e0.png)

    -   分類C：組織 → 所属メンバーを分類Dに設定

        テーブルの設定は以下のとおり。

        分類C

        ![サンプルで使う分類C（組織）の設定](https://pleasanter.org/files/images/ja/developers-guide/server-script/columns/assets/fccae7e0fff94b9b9b8aa4c052e6967e.png)

        分類D

        ![サンプルで使う分類D（所属メンバー）の設定](https://pleasanter.org/files/images/ja/developers-guide/server-script/columns/assets/e0b776befe7d4e04a21b10777e89fd24.png)

    ##### JavaScript

    ```js
    // グループ所属メンバーを取得して、選択肢にセット
    const group = groups.Get(Number(model.ClassA));
    if (group) {
        columns.ClassB.ClearChoiceHash();
        const members = group.GetMembers();
        for (const member of members) {
            // GetMembersではUserIdしか取れないので、users.Getでユーザ情報を取得
            const user = users.Get(member.UserId);
            columns.ClassB.AddChoiceHash(user.UserId, user.Name);
        }
    }
    // 部署所属メンバーを取得して、選択肢にセット
    const dept = depts.Get(Number(model.ClassC));
    if (dept) {
        columns.ClassD.ClearChoiceHash();
        const members = dept.GetMembers();
        for (const member of members) {
            columns.ClassD.AddChoiceHash(member.UserId, member.Name);
        }
    }
    ```

## 対応バージョン

|対応バージョン|内容|
|:--|:--|
|1.2.4.0 以降|機能追加|
|1.4.23.0 以降|パラメータvalueを省略可能に|

## 関連情報

-   [開発者ガイド：サーバスクリプト](../index.md)
-   [テーブルの管理：項目](../../../managers-guide/manage-table/editor/editor-settings/columns/index.md)
-   [テーブルの管理：エディタ：項目の詳細設定：選択肢一覧：組織](../../../managers-guide/manage-table/editor/editor-settings/advanced-settings/general/option-list/table-management-choices-text-depts.md)
-   [テーブルの管理：項目：分類](../../../managers-guide/manage-table/editor/editor-settings/columns/table-management-class.md)
-   [FAQ：プロセスなどの条件タブで数値や日付の条件を範囲指定したい](../../../FAQ/editor/faq-condition-mode-range.md)
