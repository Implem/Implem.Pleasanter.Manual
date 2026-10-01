---
title: プリザンターに設定した日本語の表示名でデータベースのビューを作成したい
category: FAQ：開発者向け機能
order: '0'
status: ''
parts: ''
urlstring: faq-japanese-label-text-view
translationKey: faq-japanese-label-text-view
shortname: ''
created: 2021-04-21
updated: 2024-12-04
---

## 回答

SitesテーブルのSiteSettings列の内容からテーブル名および表示名を抽出し、ビューを作成します。

---

## 概要

プリザンターに保存された「サイト設定」の情報を元に日本語の項目名でSQL Serverのビューを作成するスクリプトについて説明します。プリザンター上でテーブル名や表示名を変更した後に再実行すると、新しい設定でビューを再作成します。

## 注意事項

1. データベースの操作を行いますので事前にデータベースのバックアップを取得してください。

## 制限事項

1. 本サンプルコードはSQL Serverの環境でのみ動作します。
1. 項目名が重複している場合にはビューの作成が失敗します。
1. テーブルのタイトルが重複している場合にはビューを削除して再作成します。

## 操作方法

1. サーバにリモートデスクトップ等で接続してください。
1. 下記のサンプルコードを「PleasanterViewCreator.ps1」等の拡張子ps1で作成し保存てください。
1. PowerShellでスクリプトを実行してください。

## サンプルコード

##### PowerShell

```
[object]$ConnectionString = New-Object -TypeName System.Data.SqlClient.SqlConnectionStringBuilder
[object]$ConnectionString['Data Source'] = "(local)"
[object]$ConnectionString['Initial Catalog'] = "Implem.Pleasanter"
[object]$ConnectionString['UID'] = "sa"
[object]$ConnectionString['PWD'] = "SetSaPWD"
[object]$ColumnNames = @{
    "IssueId" = "ID"
    "ResultId" = "ID"
    "Ver" = "バージョン"
    "Title" = "タイトル"
    "Body" = "内容"
    "StartTime" = "開始"
    "CompletionTime" = "完了"
    "WorkValue" = "作業量"
    "ProgressRate" = "進捗率"
    "Status" = "状況"
    "Manager" = "管理者"
    "Owner" = "担当者"
    "Comments" = "コメント"
    "CreatedTime" = "作成日時"
    "UpdatedTime" = "更新日時"
    "Creator" = "作成者"
    "Updator" = "更新者"
}
[object]$ExcludeNames = @(
    "RemainingWorkValue"
)

function Get-Site()
{
    [string]$SQLQuery = "select * from [Sites] where [ReferenceType] in ('Issues', 'Results');"
    [object]$ResultsDataTable = New-Object System.Data.DataTable
    [object]$SqlConnection = New-Object System.Data.SQLClient.SQLConnection($ConnectionString)
    [object]$SqlCommand = New-Object System.Data.SQLClient.SQLCommand($SQLQuery, $SqlConnection)
    [object]$SqlConnection.Open()
    [object]$ResultsDataTable.Load($SqlCommand.ExecuteReader())
    [object]$SqlConnection.Close()
    return $ResultsDataTable
}

function Mainte-View($Row)
{
    [object]$Ss = ConvertFrom-Json ([string]$row.SiteSettings)
    [object]$SqlColumns = New-Object System.Collections.Generic.List[string]
    [object]$EditorColumns = $ss.EditorColumns
    if ($EditorColumns.Count -eq 0)
    {
        $EditorColumns = New-Object System.Collections.ArrayList
        $EditorColumnHash = (ConvertConvertFrom-JsonPSCustomObjectToHash $ss.EditorColumnHash)
        foreach ($Key in $EditorColumnHash.Keys)
        {
            foreach ($Value in $EditorColumnHash[$Key])
            {
                [int]$Ret = $EditorColumns.Add($Value)
            }
        }
    }
    foreach ($ColumnName in $EditorColumns)
    {
        [string]$Alias = ""
        foreach ($Column in $Ss.Columns)
        {
            if ($Column.ColumnName -eq $ColumnName)
            {
                $Alias = $Column.LabelText
            }
        }
        if ($Alias -eq "")
        {
            $Alias = $ColumnNames[$ColumnName]
        }
        if ($Alias -eq "")
        {
            $Alias = $ColumnName
        }
        if ($ExcludeNames -notcontains $ColumnName)
        {
            $SqlColumns.Add("[$ColumnName] as [$Alias]")
        }
    }
    [string]$JoinedSqlColumns = $SqlColumns -join ","
    Delete-View $Row
    Create-View $Row $JoinedSqlColumns
}

function Create-View($Row, $JoinedSqlColumns)
{
    "ビュー作成：" + $Row.Title
    [string]$SQLQuery = @"
        create view [$([string]$Row.Title)]
        as
            select $JoinedSqlColumns
            from [$([string]$Row.ReferenceType)]
            where [SiteId]=$([long]$row.SiteId);
"@
    [object]$SqlConnection = New-Object System.Data.SQLClient.SQLConnection($ConnectionString)
    [object]$SqlCommand = New-Object System.Data.SQLClient.SQLCommand($SQLQuery, $SqlConnection)
    [object]$SqlConnection.Open()
    [int]$Ret = $SqlCommand.ExecuteNonQuery()
    [object]$SqlConnection.Close()
}

function Delete-View($Row)
{
    [string]$SQLQuery = @"
        if exists (select 1 from sysobjects where id = object_id('$([string]$row.Title)'))
        drop view [$([string]$row.Title)];
"@
    [object]$SqlConnection = New-Object System.Data.SQLClient.SQLConnection($ConnectionString)
    [object]$SqlCommand = New-Object System.Data.SQLClient.SQLCommand($SQLQuery, $SqlConnection)
    [object]$SqlConnection.Open()
    [int]$Ret = $SqlCommand.ExecuteNonQuery()
    [object]$SqlConnection.Close()
}

Function ConvertConvertFrom-JsonPSCustomObjectToHash($obj)
{
    $hash = @{}
    $obj | Get-Member -MemberType Properties | SELECT -exp "Name" | % {
        $hash[$_] = ($obj | SELECT -exp $_)
    }
    $hash
}

[object]$Table = Get-Site
foreach ($Row in $Table)
{
    Mainte-View $Row
}
```

## 実行結果

## Metabaseでの表示

作成したビューをMetabaseで表示すると下記のように日本語のビューを表示できます。
![作成したビューをMetabaseで表示し、項目名が日本語になっている状態](https://pleasanter.org/files/images/ja/FAQ/features-for-developers/assets/e4e6ff46a8b048dfb90e3f87531b7b8a.png)

一覧表やグラフも日本語で表示できます。
![Metabaseの一覧表とグラフが日本語で表示されている状態](https://pleasanter.org/files/images/ja/FAQ/features-for-developers/assets/cefd7381289b4be3aaf77d8d5b5677bc.png)

## テーブルの非表示設定

プリザンターに本来あるテーブルの表示が邪魔な場合、指定したテーブルを非表示にすることができます。
metabaseのホームの右上にある「管理者設定」から、「テーブル・メタデータ」を選択します。
![Metabaseのホーム右上にある「管理者設定」を開くところ](https://pleasanter.org/files/images/ja/FAQ/features-for-developers/assets/08ea2bf0cd774f1583ab5c3dbc23aa2e.png)
![管理者設定から「テーブル・メタデータ」を選ぶところ](https://pleasanter.org/files/images/ja/FAQ/features-for-developers/assets/c528f3a8338f4bfd96ec9f23417c4b4f.png)

非表示にするテーブルの右側にあるアイコンをクリックすることで非表示になります。
![テーブルの一覧。各テーブルの右側に非表示にするアイコンがある](https://pleasanter.org/files/images/ja/FAQ/features-for-developers/assets/ba09d4a1c4be4c7ba313b565da95a1ca.png)