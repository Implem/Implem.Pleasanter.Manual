---
title: KVSのインストール
category: 関連ソフトウェアのインストール
order: '900'
status: ''
parts: ''
urlstring: kvs-install
translationKey: kvs-install
shortname: KVS
created: 2024-10-22
updated: 2026-01-13
---

## 概要

KVSを利用するための設定を行います。本ページでは例として、Azure、Windows、Linux(Ubuntu)へ「Redis」をインストールする手順について説明します。ご利用環境に合わせて手順を参照してください。

## 制限事項

1. ローカル上でSSL/TLS接続を利用する場合は、別途ユーティリティの設定が必要になります。
1. 現在、動作確認が完了しているのはRedisのみとなっています。Redis以外のデータベースアプリケーションをご利用の場合は、予期せぬ動作が発生する可能性がありますのであらかじめご注意ください。

## 操作手順

ご利用環境に合わせて以下手順を参照ください。  
[Azureへ「Redis」をインストールする手順](#section1)
[Windowsへ「Redis」をインストールする手順](#section2)
[Ubuntuへ「Redis」をインストールする手順](#section3)

<a id="section1"></a>
<br>

## Azureへ「Redis」をインストールする手順

1. Azureの検索ボックスから「Azure Cache for Redis」を開きます。
![Azure ポータルの検索ボックスで「Azure Cache for Redis」を探したところ](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/df66d2b809754a06a02c4e24d7bd51d9.png)

1. 「Azure Cache for Redis」の画面左上にある「作成」をクリックします。
![「Azure Cache for Redis」の一覧画面。左上に「作成」がある](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/b6560d102ffa44029bc540669d7781b7.png)

1. プリザンターをインストール時に作成した「サブスクリプション」、「リソースグループ」を設定します。
それぞれ任意の値で「DNS名」、「場所」、「キャッシュ SKU」、「キャッシュ サイズ」を設定します。
「次：ネットワーク」をクリックします。
![Azure Cache for Redis の作成画面。サブスクリプションや DNS 名などを設定する](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/54e913c2dcae4f51a676d1e0aab20c5f.png)

1. 「ネットワーク接続」を設定します。
「次：詳細」をクリックします。
![Azure Cache for Redis の作成画面の「ネットワーク」の設定](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/c68181d37b734e1d90a39eda950957fc.png)

1. 「詳細」を設定します。
「次：タグ」をクリックします。
![Azure Cache for Redis の作成画面の「詳細」の設定](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/dd807434f71140c99d8ec9a1818512ab.png)

1. 「タグ」を任意で設定します。
「次：レビューと作成」をクリックします。
![Azure Cache for Redis の作成画面の「タグ」の設定](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/e2744edcfacc4a349106b54440b2421f.png)

1. 「作成」をクリックします。
![Azure Cache for Redis の作成内容を確認する画面。「作成」ボタンがある](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/128093e68cc94134b885776ff7dd4603.png)

1. デプロイの進行を待ちます。
![デプロイの進行状況を表示している画面](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/34347f46830e4560954935241c3c20f7.png)

1. デプロイが完了後、 App Serviceにてインスタンスを再起動します。

<a id="section2"></a>
<br>

## Windowsへ「Redis」をインストールする手順

1. GithubにあるMicrosoftの[Redisのリリースページ](https://github.com/MicrosoftArchive/redis/releases)から最新バージョンの.msiファイルをダウンロードします。
![GitHub 上の Microsoft の Redis のリリースページ。.msi ファイルが置かれている](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/5bdef4a6525746568a5189390f4dc21b.png)

1. エクスプローラーを開き、ダウンロードした.msiファイルを起動します。

1. 「Next」をクリックします。
![Windows 版 Redis のインストーラの最初の画面。「Next」ボタンがある](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/6b79b82bff8b458fb72f586f389bc15e.png)

1. ライセンスに同意し、「Next」をクリックします。
![Redis のインストーラのライセンスに同意する画面](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/d43213517f7c420c90b90bd5bd2aa3ec.png)

1. Redisを配置する場所を設定し、「Next」をクリックします。
![Redis を配置する場所を指定する画面](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/fcaae5df05a74aa2887af74955a54813.png)

1. デフォルトのポート番号を設定し、チェックボックスにチェックを付けて「Next」をクリックします。
![Redis のポート番号を指定する画面。チェックボックスがある](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/7f3916991ae04a0da7a266664875ff9c.png)

1. 「Next」をクリックします。
![Redis のインストーラの設定画面。「Next」ボタンがある](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/f4278e27d1864845b338f0c4981b3445.png)

1. 「Install」をクリックします。
![インストールの開始を確認する画面。「Install」ボタンがある](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/9c3215021caf4bae80865e9e1c770bad.png)

1. インストールが完了したら「Finish」をクリックして画面を閉じます。
![Redis のインストールの完了画面。「Finish」ボタンがある](https://pleasanter.org/files/images/ja/setup/installation/install-database/assets/64aa278170e94cb9a2837e257dc268ba.png)

<a id="section3"></a>
<br>

## Ubuntuへ「Redis」をインストールする手順

1. 下記コマンドを実行し、パッケージ情報を更新します。
```
sudo apt update
```

1. 下記コマンドを実行し、Redisをインストールします。
```
sudo apt install redis-server
```

1. /etc/redis/redis.conf を任意のテキストエディタで開き、以下の設定を編集します。
```
# Note: these supervision methods only signal "process is ready."
#       They do not enable continuous liveness pings back to your supervisor.
supervised systemd
```

1. 下記コマンドを実行し、Redisを再起動して設定を反映します。
```
sudo systemctl restart redis.service
```