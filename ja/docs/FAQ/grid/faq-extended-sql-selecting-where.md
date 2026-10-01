---
title: 一覧表示するレコードを所属組織別に分けたい
category: FAQ：一覧画面の操作・設定
order: '0'
status: ''
parts: ''
urlstring: faq-extended-sql-selecting-where
translationKey: faq-extended-sql-selecting-where
shortname: OnSelectingWhere
created: 2020-10-12
updated: 2024-07-12
---

## 回答

[拡張SQL](../../developers-guide/extended-features/extended-sql/index.md)の「OnSelectingWhere」を使用してください。

---

## 概要

事前に作成した組織・グループ別にレコード一覧画面に表示するレコードを制御します。このページでは本社(組織)に所属するユーザは登録された全てのレコードを閲覧することができ、その他の組織に所属するユーザは同グループ内で登録されたレコードのみを閲覧することができるようになります。

## 事前準備

(1) システム管理者でログイン後、下記の表を参考に[管理]-[ユーザの管理]、[組織の管理]、[グループの管理]からグループと組織情報を含めたユーザ情報を作成してください。ここでは本社に所属するユーザと各営業店に所属するユーザを想定し、組織とグループを構成します。下記にその構成を表に記載いたします。

|ユーザ|組織|グループ|
|:--|:--|:--|  
|branch-user1|営業店1|グループ１|  
|branch-user2|営業店2|〃|  
|branch-user3|営業店3|グループ２|
|head-user1|本社|-|  

![ユーザの管理画面。表のとおりにユーザを作成した状態](https://pleasanter.org/files/images/ja/FAQ/grid/assets/c622ae4f8480482fa3f3fccc02fa8262.png)
![組織の管理画面。本社と各営業店を作成した状態](https://pleasanter.org/files/images/ja/FAQ/grid/assets/f2f3aac7a0b24023af67d3664ec52da9.png)
![グループの管理画面。2つのグループを作成した状態](https://pleasanter.org/files/images/ja/FAQ/grid/assets/405924daf52142d6956048fb035b624e.png)

(2)[管理]-[テーブルの管理]-[エディタ]より分類Bを任意の表示名にして(ここでは”店番”,わかりやすいように分類Cを”店名”に設定)、[一覧]タブからそれぞれを有効化してください。  

(3) 各ユーザでレコードを少なくても1つ作成してください。  
![各ユーザで作成したレコードが並ぶ一覧画面](https://pleasanter.org/files/images/ja/FAQ/grid/assets/66ffd687bd1d45cbabe4775853193322.png)
(4) 以下のサンプルコード(Sql)の@_Dの値とサンプルコード(JSON)のSiteIdListの値を環境に合わせ、変更してください。  
      この例では@_Dの値は21,SiteIdListの値は1166になります。  
![サンプルコードに設定する @_D と SiteIdList の値を確認する画面](https://pleasanter.org/files/images/ja/FAQ/grid/assets/a96b06665b064ac9aef73383cee48bfe.png)

(5) Extensionsテーブルに(3)で作成したサンプルコードとその他の項目を記入してください。  
　　拡張SQLについてはこちらをご確認ください(/manual/extended-sql)

(6)プリザンターを再起動してください。

##### Sql

```
(
    @_U = 1 or @_D = 1 --システム管理者のユーザIDまたは本社組織の組織ID
    or [ClassB] in (
        select [Depts].[DeptCode]
        from [GroupMembers]
        left join [Depts] 
        on Depts.DeptId = GroupMembers.DeptId
            and ([GroupMembers].[GroupId] in(
                select [GroupId] 
                from [GroupMembers] 
                where [DeptId] = @_D))
        where [Depts].[DeptCode] is not null)
)
```

##### JSON

```
{
    "SiteIdList": [2],
    "OnSelectingWhere": true
}
```

## 結果

以下のようにユーザ毎に所属するグループまたは組織によって表示(取得)されるレコードが変わります。 

-   本社ユーザでログインした場合

    ![本社ユーザでログインしたときの一覧画面](https://pleasanter.org/files/images/ja/FAQ/grid/assets/f90e12dbeb844fd38c1afcaeb41d99c1.png)

-   営業店2に所属するユーザでログインした場合

    ![営業店2に所属するユーザでログインしたときの一覧画面](https://pleasanter.org/files/images/ja/FAQ/grid/assets/699a299bab30493f81483846ea897704.png)

-   営業店3に所属するユーザでログインした場合

    ![営業店3に所属するユーザでログインしたときの一覧画面](https://pleasanter.org/files/images/ja/FAQ/grid/assets/43c665f261264fb3b6d9760ab2bbf540.png)

## 関連情報

-   [開発者ガイド：拡張機能：拡張SQL](../../developers-guide/extended-features/extended-sql/index.md)