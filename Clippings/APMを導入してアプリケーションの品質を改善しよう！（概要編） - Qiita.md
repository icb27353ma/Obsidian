---
title: "APMを導入してアプリケーションの品質を改善しよう！（概要編） - Qiita"
source: "https://qiita.com/nr-mito/items/74bf587bc97128403d9e?utm_campaign=popular_items&utm_medium=feed&utm_source=popular_items"
author:
  - "[[nr-mito]]"
published: 2024-11-22
created: 2024-11-22
description: "New Relic APMをアプリケーションに導入することで、アプリケーションの健全性をリアルタイムで観測し、システム障害やユーザー体験の劣化につながるアプリケーションのパフォーマンスやエラーの原因…"
tags:
  - "clippings"
---
New Relic APMをアプリケーションに導入することで、アプリケーションの健全性をリアルタイムで観測し、システム障害やユーザー体験の劣化につながるアプリケーションのパフォーマンスやエラーの原因特定と解決、改善に繋げることができます。

## APM とは

APM(Application Performance Monitoring)は、アプリケーションが想定通りのパフォーマンスを発揮しているかどうかを監視し、その改善に向けた原因の特定や、改修の迅速化を実現するためのプロセス、あるいはそのためのツールを指します。APMを導入することで、アプリケーションのパフォーマンス低下やエラーを検知し、その原因を素早く特定して対処することができるため、提供するサービスレベルの維持とユーザー体験の向上に繋げていくことができます。

## New Relic APM とは

New Relic APMは、アプリケーションの言語別に用意されているAPMエージェントをインストールすることで、アプリケーションのパフォーマンスデータを収集します。以下の主要な言語に対応したエージェントが用意されています。

[![image.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3485441%2F4f64701a-e74e-a133-5c95-33e1f6cd2f46.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=05ff71e356e86d1a9ec5921204c9601e)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3485441%2F4f64701a-e74e-a133-5c95-33e1f6cd2f46.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=05ff71e356e86d1a9ec5921204c9601e)

各言語の代表的なフレームワークをサポートしており、アプリケーションのパフォーマンスデータを計測するコードをエージェントが自動的に計装することで、アプリケーションのパフォーマンスやエラーの発生状況などリアルタイムで観測できるようになります。

[![image.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3485441%2F679597af-56dc-888f-dd7d-f80187da7c2a.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=d4edfffc15a1e05e32453d7e6068849c)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3485441%2F679597af-56dc-888f-dd7d-f80187da7c2a.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=d4edfffc15a1e05e32453d7e6068849c)

## どうやって導入するの？

APMエージェントのインストール方法は各言語で多少の違いはありますが、どの言語でもおおよそ以下の流れで簡単に導入することになります。

1. [インストール要件](https://docs.newrelic.com/jp/docs/new-relic-solutions/new-relic-one/install-configure/compatibility-requirements-new-relic-agents-products/?_gl=1*skbddj*_gcl_au*MjExMjUzMzg4NC4xNzMxMzc3ODcy*_ga*Mzc0MTY4NjAzLjE3MDgwNDU0Mzg.*_ga_R5EF3MCG7B*MTczMjI0NjgyOC42MjIuMS4xNzMyMjQ3MzQ3LjU1LjEuMTE2MzM0MzM0MA..)を確認
2. New Relic 画面上でガイドを受けながら、アプリケーションにAPMエージェントをインストール
3. アプリケーションを再起動し、トランザクションを発生させる
4. New Relic のAPMの画面上でデータを確認する

次回以降の記事でエージェントの導入の流れの詳細をご紹介します！

## その他

New Relicでは、**新しい機能やその活用方法**について、QiitaやXで発信しています！  
**無料でアカウント作成**も可能なのでぜひお試しください！