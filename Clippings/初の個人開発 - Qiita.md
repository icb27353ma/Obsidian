---
title: "初の個人開発 - Qiita"
source: "https://qiita.com/purojyu/items/66abfd315093f36dacea?utm_campaign=popular_items&utm_medium=feed&utm_source=popular_items"
author:
  - "[[purojyu]]"
published: 2024-11-18
created: 2024-11-20
description: "はじめに今回は初めて個人でWEBサービスプロ野球投手VS野手対戦成績検索サービスをリリースしました。まだまだ改善点はあるものの、ひとまず形にはなったので、開発した経験について紹介します。少しでも参…"
tags:
  - "clippings"
---
## はじめに

今回は初めて個人でWEBサービス[プロ野球投手VS野手対戦成績検索サービス](https://baseball-pitcher-vs-batter.com/)をリリースしました。まだまだ改善点はあるものの、ひとまず形にはなったので、開発した経験について紹介します。少しでも参考になれば幸いです。

## 自己紹介

- 27歳
- 大卒(化学系)
- 公務員：1年半
- エンジニア：3年(現在)

## サービスの内容

プロ野球の特定の投手と野手の対戦成績を検索できるWEBアプリです。  
年度やチームを絞り込んで検索可能です(通算検索などいくつかの検索ができます)。  
[![スクリーンショット 2024-11-16 12.43.16.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3933685%2F20fc3491-e582-9e96-90b7-f82524e543ef.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=1878776abbb81e724f31e38ff5211462)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3933685%2F20fc3491-e582-9e96-90b7-f82524e543ef.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=1878776abbb81e724f31e38ff5211462)  
打率やOPSなどの検索結果をチームと打席数順に表示します。  
選手のリンク押下で、NPBの選手紹介ページに遷移します。  
[![スクリーンショット 2024-11-16 12.44.11.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3933685%2Ffa1822c2-c629-ad0d-f2a0-df74b950afe3.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=509bc4173a19a2404e19ab6232c55768)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3933685%2Ffa1822c2-c629-ad0d-f2a0-df74b950afe3.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=509bc4173a19a2404e19ab6232c55768)

## なぜ作ったか

日々の仕事では設計、実装、テスト、リリースの工程をアジャイル開発で繰り返してきましたが、全体の開発プロセスを経験したことがありませんでした。そのため、個人開発を通じて、開発プロセス全体を経験し、知識を深めることを目標にしていました。

自分が興味を持って取り組める題材にしたく、好きな野球をテーマにすることにしました。中継中に紹介される「投手と野手の対戦成績」を自分でも簡単に調べられたら野球をもっと楽しめるのではと考え、このシステムを作ることにしました。また、同様のサービスがほとんどなかったため、開発をスタートしました。

## 使用技術

このサービスでは以下の技術を使用しました

- **バックエンド**：Java、Spring Boot
- **フロントエンド**：Vue.js、JavaScript、Bootstrap、HTML、CSS
- **データベース**：MySQL
- **インフラ**：Heroku(basic)、RDS、CloudFlare

## 簡単な設計の紹介

- **フロントエンド**：Vueのcomputedやwatchを利用し、選手のプルダウンは選択した年度とチームに応じて動的に変化させました。multiselectをカスタムし、漢字やひらがなでプルダウンの選択肢を絞り込み可能にし、空白の有無も許容しました。
- **バックエンド**：ストリームやラムダ式を活用してデータ処理を効率化しました。セキュリティの向上も意識し、エンドポイントの設計に注力しました。また、データベースのインデックスを適切に付与し、初期表示と検索の処理速度を向上させました。
- **データ更新**：SpringのScheduledアノテーションを用いてNPB公式の試合結果を日次でスクレイピングし、常に最新の情報を提供しています。
- **ER図**：今後の改修に合わせて修正予定  
[![スクリーンショット 2024-11-16 14.02.25.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3933685%2Fa124e10b-9c08-de14-5727-c772e5008cfc.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=5aac22b4435c28b4be5dd08375611e17)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3933685%2Fa124e10b-9c08-de14-5727-c772e5008cfc.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=5aac22b4435c28b4be5dd08375611e17)

## 課題

個人開発を通じて、以下の課題が見えてきました

- **インフラの知識不足**：Heroku、RDS、CloudFlareを用いて簡易的にインフラ構築を行いました。インフラに関する知識があれば、よりパフォーマンス、セキュリティ、コスト面を考えられたインフラ設計ができたと感じています。
- **データ依存**：NPB公式サイトの構造に依存しているため、サイトの変更があった場合には改修が必要です。ただし、2005年以降大きな変更は1度のみなので、頻繁な対応は必要ないと見込んでいます。

## 改修

今後、以下の改修を行いたいと考えています

- **インフラ改善**：AWSなどのインフラ周りの知識を深め、パフォーマンス向上を図りたい。
- **機能追加**：一球ごとのデータを取り込み、投手と野手の得意・苦手ゾーンを可視化するなどの機能を実装したい。

## 今後（おわりに）

今回の個人開発を通じて、「自分が作りたいサービスを作る」という楽しさを再認識しました。しかし、事前の調査不足(スクレイピングするサイトの構成の理解やインフラ周りでの使用技術の選定)により手戻り作業が発生したため、開発前の調査の重要性を改めて感じました。

また、開発中に新しい機能のアイディアが出てきたことで、仕様が2転3転してしまったので、最初にプロジェクトの範囲を明確にしておくことの大切さも実感しました。

これからは、インフラ周り等の上流工程のスキルも身につけ、開発プロセス全体で貢献できるエンジニアを目指したいと思っています。

以上、初めての個人開発を通じての学びと経験です。最後までお読みいただきありがとうございました！!

---

Qiitaでの初投稿、温かいコメントやフィードバックをお待ちしています！