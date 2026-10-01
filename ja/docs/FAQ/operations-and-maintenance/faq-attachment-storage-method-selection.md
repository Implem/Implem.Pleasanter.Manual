---
title: 添付ファイル格納方式の選択基準を知りたい
category: FAQ：運用、メンテナンス
order: '0'
status: ''
parts: ''
urlstring: faq-attachment-storage-method-selection
translationKey: faq-attachment-storage-method-selection
shortname: ''
created: 2026-04-10
updated: 2026-04-10
---

## 回答

[添付ファイル](../../users-guide/table/record-authoring/edit-records/table-record-attachment-delete.md)の格納方式は、設定ファイル[BinaryStorage.json](../../setup/parameters/binary-storage-json.md)のパラメータProviderで設定できます。Providerの値はRdsまたはLocalから選択します。

以下の比較表と本ページの説明を参考に検討してください。

| 項目           | Rds（データベース格納）             | Local（ローカルストレージ格納）         |
| -------------- | :--------------------------: | :----------------------------: |
| 推奨規模       | 10 Gバイト未満               | 数十Gバイト以上                |
| 整合性         | 高<br>（トランザクション保証）   | 中<br>（運用でカバー）             |
| バックアップ   | シンプル<br>（データベースのみ） | 複雑<br>（データベース＋ファイル） |
| クラスタ対応   | 容易                         | 共有ストレージ必須             |
| パフォーマンス | ファイル増加で低下           | データベース 負荷を軽減        |

---

## 概要

[添付ファイル](../../users-guide/table/record-authoring/edit-records/table-record-attachment-delete.md)の格納方式は、設定ファイル[BinaryStorage.json](../../setup/parameters/binary-storage-json.md)のパラメータProviderで設定できます。Providerの値はRdsまたはLocalから選択します。

1. **Rds（データベース格納）**  
   添付ファイルをデータベースのBinariesテーブルのBin列に格納します（初期値）。
1. **Local（ローカルストレージ格納）**  
   添付ファイルをファイルシステムに格納し、管理情報のみをデータベースのBinariesテーブルに格納します。

添付ファイルが少ない場合はRds（データベース格納）のままで問題ありませんが、添付ファイルが多い場合はLocal（ローカルストレージ格納）への変更を検討してください。

## Rds（データベース格納）の特性

#### ①メリット

1. ファイルとメタデータがトランザクション内で一貫管理される
1. バックアップはデータベースのみで完結するため、運用がシンプル
1. データベース権限のみでアクセス制御が可能

#### ②デメリット

1. 大容量ファイルによりBinariesテーブルが肥大化する
1. バックアップ・リストアの所要時間が長くなる
1. 大量ファイル操作時にデータベースリソースを圧迫する
1. データベースごとに異なる容量制限（後述）を受ける

#### ③推奨するケース

1. 添付ファイルの総容量が数Gバイト未満
1. 1ファイルあたりの容量が10Mバイト以下が中心
1. データの整合性を最優先したい
1. バックアップ運用をシンプルに保ちたい

![Rds（データベース格納）の構成を示した図](https://pleasanter.org/files/images/ja/FAQ/operations-and-maintenance/assets/d4a1eac2aea64162860f713b09d8bc53.png)

## ローカルストレージ格納（Local）の特性

#### ①メリット

1. Binariesテーブルは数Kバイト程度のメタデータのみとなり、データベースを軽量に保てる
1. ファイル容量の制約がOS・ファイルシステム依存になる
1. ファイル入出力とデータベース入出力を別ディスクに分離できる
1. 共有ストレージへ拡張しやすい

#### ②デメリット

1. データベースとファイルストレージを別々にバックアップする必要がある
1. 複数Webサーバ構成では共有ストレージが必須

#### ③推奨するケース

1. 添付ファイルの総容量が数十Gバイト以上
1. 1ファイルあたりの容量が数百Mバイト以上を扱う
1. バックアップ時間を短縮したい
1. データベースのパフォーマンスを優先したい
1. 複数Webサーバ構成で共有ストレージが利用可能

![ローカルストレージ格納（Local）の構成を示した図](https://pleasanter.org/files/images/ja/FAQ/operations-and-maintenance/assets/c60c9f4a9955472e92fccb9e6fbfee8c.png)

## データベースごとの容量制約

各データベースでのバイナリデータ格納には、以下の容量制約があります。

| データベース | データ型 | 理論上の上限容量 | 実用上の推奨容量       |
| ------------ | -------- | -----------: | ------------------ |
| SQL Server   | IMAGE    | 2 Gバイト    | 数百Mバイト以下    |
| PostgreSQL   | BYTEA    | 1 Gバイト    | 数百Mバイト以下    |
| MySQL        | LONGBLOB | 4 Gバイト    | 数百Mバイト以下 <span class="pl-attention">＊</span> |

<span class="pl-attention">＊</span>MySQL環境で大容量ファイルを扱う場合はmax_allowed_packetの設定を調整する必要があります。

<details markdown="1">

<summary>my.cnfまたはmy.iniでの設定例</summary>

```ini
[mysqld]
max_allowed_packet = 256M
```

上記はデータ型の制約です。実際には各データベースのページサイズ、バッファ設定、ネットワーク設定なども影響します。数百Mバイト以上のファイルを頻繁に扱う場合は、データベースパフォーマンスの観点からLocal（ローカルストレージ格納）を推奨します。

</details>

## 運用上のベストプラクティス

各格納方式において、以下の実施を推奨します。

#### Rds（データベース格納）の場合

1. Binariesテーブルの容量を定期的に監視する
1. 定期的なVACUUM実行（PostgreSQL）またはインデックス再構築（SQL Server）を実施する
1. バックアップ所要時間を継続的に監視する

#### Local（ローカルストレージ格納）の場合

1. ファイル格納ディレクトリは、データベースのバックアップと同頻度・同タイミングでバックアップする
1. 孤児ファイルの定期的なクリーンアップを実施する
1. 共有ストレージの容量IOPSを監視する
1. ファイルシステムとデータベースの整合性を定期的に確認する

## クラスタ構成下での設定

クラスタ構成下での設定については、以下のマニュアルを確認してください。

[パラメータ設定：BinaryStorage.json](../../setup/parameters/binary-storage-json.md)  
[追加設定：クラスタ化への備え：バックグラウンドサービスを複数インスタンス構成に対応させる](../../setup/additional/ready-for-clustering/service-clustering.md)  
[追加設定：クラスタ化への備え：添付ファイルのアップロード・登録に関する設定](../../setup/additional/ready-for-clustering/clustering-attachment-item-settings.md)  
[追加設定：クラスタ化への備え：添付ファイルをローカルストレージ格納する設定](../../setup/additional/ready-for-clustering/clustering-attachments-store-local-storage.md)
[パラメータ設定：Quartz.json](../../setup/parameters/quartz-json.md)