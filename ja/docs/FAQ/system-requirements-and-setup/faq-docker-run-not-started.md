---
title: DockerHubからpullしたプリザンター1.4.0.0を起動したが、ブラウザで応答がない
category: FAQ：動作環境、セットアップ
order: '0'
status: ''
parts: ''
urlstring: faq-docker-run-not-started
translationKey: faq-docker-run-not-started
shortname: ''
created: 2024-06-03
updated: 2025-03-27
---

## 回答

**※DockerHubからpullしたプリザンターの起動手順はver.1.4.6.0リリース以降より内容を刷新したため、今後新たにDockerでプリザンターの運用を開始する場合、本FAQの回答は無効です。今後新たにDockerでプリザンターの運用を開始する場合は、過去のバージョン番号を指定しプリザンターを起動する場合も含め、最新の[Dockerで起動する手順](../../setup/installation/running-with-docker/getting-started-pleasanter-docker.md)を参照してください。**

---

**※以下は、ver.1.4.6.0リリースより前からDockerでプリザンターを立ち上げて運用しており、現在も同環境を継続利用している場合のみご覧ください。**

## 概要

[DockerHub](https://hub.docker.com/r/implem/pleasanter)からpullしたプリザンターを起動する場合、プリザンターをスタートさせるコマンドはバージョンによって以下の通りとなります。

### ～ver.1.3.50.2まで

```
docker compose run -p 50001:80 pleasanter
```

### ver.1.4.0.0～1.4.5.0

```
docker compose run -p 50001:8080 pleasanter
```

### ver.1.4.6.0以降～

最新の[Dockerで起動する手順](../../setup/installation/running-with-docker/getting-started-pleasanter-docker.md)を参照してください。

## 関連情報  

[Dockerで起動する](../../setup/installation/running-with-docker/getting-started-pleasanter-docker.md)