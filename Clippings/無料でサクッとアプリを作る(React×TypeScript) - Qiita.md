---
title: "無料でサクッとアプリを作る(React×TypeScript) - Qiita"
source: "https://qiita.com/shotaqiita/items/934b01c542d2b12b8761?utm_campaign=popular_items&utm_medium=feed&utm_source=popular_items"
author:
  - "[[shotaqiita]]"
published: 2024-11-14
created: 2024-11-15
description: "はじめに本記事は無料でサクッとアプリが作れる技術スタックの紹介と、使ってみての感想です。具体的なセットアップは範囲外にしています。技術スタック・React・TypeScript・Supa…"
tags:
  - "clippings"
---
## はじめに

本記事は無料でサクッとアプリが作れる技術スタックの紹介と、使ってみての感想です。  
具体的なセットアップは範囲外にしています。

## 技術スタック

・React  
・TypeScript  
・Supabase(データベース)  
・Firebase(デプロイ)

使用しているものはすべて無料です。  
データベースはSupabaseを選びました。  
プロジェクトインスタンスが2個まで無料で利用できます。

作成したアプリをWeb上に公開したいのでホスティングサービスとしてFirebaseを選びました。  
毎月一定の利用量に達するまでは無料で利用可能です。

## 今回作成したアプリ

デジタル名刺アプリです。  
以下の機能があります。  
・idで名刺を検索して閲覧する  
・名刺を新規作成する  
・各項目のバリデーション

[![ezgif.com-video-to-gif-converter.gif](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3810842%2Ff619b251-2934-aaeb-329c-331d055732b9.gif?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=bde4309bbc45770b40113eb068de93d6)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3810842%2Ff619b251-2934-aaeb-329c-331d055732b9.gif?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=bde4309bbc45770b40113eb068de93d6)

## サクッと作るために

### プロジェクト立ち上げ

viteというビルドツールを使って1つのコマンドでプロジェクトを立ち上げることができます。  
プロジェクトを作成したいディレクトリに移動し、  
`npm create vite@latest`を打つ。あとは指示に従うだけです。

### デザイン

UIはほぼ時間をかけていません。  
[Chakra-UI](https://www.chakra-ui.com/)というCSSライブラリを使用しています。  
Buttonなどが簡単に作成でき、ローディングアイコン等もChakra-UIで完結します。

### バリデーション機能

React Hook Formを使用し、フォームの入力に不備がある時の挙動を簡単に実装できました。  
[![スクリーンショット 2024-11-14 23.24.10.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3810842%2Fd5a09aa9-3821-7bff-8301-0cc278f626b5.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=132945296dc9dd241acf17cf18e36683)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3810842%2Fd5a09aa9-3821-7bff-8301-0cc278f626b5.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=132945296dc9dd241acf17cf18e36683)

## 使ってみての感想

プロジェクトを立ち上げてFirebaseでデプロイするだけなら1時間もかからずにWeb上でサイトを公開できました。  
Herokuも数年前に有料になってしまったので、Firebaseが今のところ個人開発で使うのに勝手がいいのではと思っています。