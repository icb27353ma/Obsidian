---
title: "【個人開発】家で勉強できない私が「勉強場所の検索サービス」を作成しました ✍️ - Qiita"
source: "https://qiita.com/yuki31100725/items/9cf603f9ac08b850c2d7?utm_campaign=popular_items&utm_medium=feed&utm_source=popular_items"
author:
  - "[[yuki31100725]]"
published: 2024-11-10
created: 2024-11-12
description: "はじめに初めまして。ゆうき(@yuki31100725)と申します。現在、プログラミングスクールRUNTEQに通ってRuby on Railsを学習しております。今回、スクールの卒業制作として「LearnLocato…"
tags:
  - "clippings"
---
## はじめに

初めまして。ゆうき([@yuki31100725](https://qiita.com/yuki31100725 "yuki31100725"))と申します。

現在、プログラミングスクールRUNTEQに通ってRuby on Railsを学習しております。

今回、スクールの卒業制作として「**LearnLocator**」という、勉強場所(自習室・コワーキングスペース)の検索サービスを作成しました。

### サービスはこちら

### GitHubリポジトリはこちら

[![Image from Gyazo](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2F519b19ef929e67ddbfafb8e564683bd3.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=8cf95d033889676e1fe60708dba718b0)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2F519b19ef929e67ddbfafb8e564683bd3.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=8cf95d033889676e1fe60708dba718b0)

本サービスとロゴに込めた思い

このロゴは、羽根ペンで筆を走らせるようなイメージと、LearnLocatorの「 L 」を組み合わせたデザインにしています。

また、サービス全体で「 白 」を基調としたデザインを採用しており、真っ白な紙に文字を書いていくような " 勉強 " のイメージを表現しています。

一方で、サービスを利用していただくと " 赤・青・黄・緑 " の4色が画面上に登場します。  
( 赤：いいね / 青：口コミ / 黄：評価 / 緑：ブックマーク )

以上から、本サービスがあなたの " 勉強 " をサポートし、 " 彩り豊かな未来 " に羽ばたくきっかけとなって欲しいという思いを込めました。

## 1\. 概要

家以外で勉強できる場所(自習室・コワーキングスペース)を検索できるサービスです。

- 現在の位置情報から、近くの勉強場所を検索
- 住所や施設のタイプから、勉強場所を検索
- 施設に対する口コミから、勉強場所を検索

## 2\. 開発した理由

開発者である私自身が、「勉強する際に家では集中できない」と思っており、自習室やコワーキングスペースをネット検索で調査していたのですが、「もう少し簡単に調べられるアプリケーションが欲しい」と感じたのがサービス作成のきっかけでした。

また、下記のような課題を感じ、それを改善できるサービス作成をすることを決めました。

- そもそも自習室とコワーキングスペースの違いがわからず、利用する前にハードルを感じていたこと
- 自習室とコワーキングスペースの情報を一元管理しているようなサービスが見当たらなかったこと
- 施設ごとにHPが乱立しており、各施設の情報に辿り着くまでに手間がかかること
- 利用者の生の声(口コミ)は、Google Mapのレビューなどを見に行かないと確認できないこと
- 「興味がある」と感じた施設についても、別途Google Mapなどで経路情報を調べる手間があること

## 3\. 機能

### メイン機能(ユーザー登録不要)

|  |  |
| --- | --- |
| (1) 場所検索 | (2) 一覧検索 |
| [![Image from Gyazo](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2F4164b0da4f85d187c34373b0cd1fc6a1.gif?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=d9ae688ad5afc8b01fbc760c6d622815)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2F4164b0da4f85d187c34373b0cd1fc6a1.gif?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=d9ae688ad5afc8b01fbc760c6d622815) | [![Image from Gyazo](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2F82b4f5844dc1459e2756a71022cde53e.gif?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=2da2e2f190bfdad20c162ddc985bdc0c)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2F82b4f5844dc1459e2756a71022cde53e.gif?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=2da2e2f190bfdad20c162ddc985bdc0c) |
| 現在地近くの勉強場所がわかります。   地名などから周辺の場所を検索することもできます。 | 口コミの一覧から条件を設定し検索できます。   結果の並べ替えも可能です。 |

|  |  |
| --- | --- |
| (3) 口コミ検索 | (4) 施設情報の確認 |
| [![Image from Gyazo](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2F615afa46380fc2686519ea6912ab224e.gif?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=7e0290f705a3eb8288287719694147c8)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2F615afa46380fc2686519ea6912ab224e.gif?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=7e0290f705a3eb8288287719694147c8) | [![Image from Gyazo](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2Fa53b0e31de95b99e6432fb8da7dd630d.gif?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=34eff9beeda40d4e66184f9128de8a1c)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2Fa53b0e31de95b99e6432fb8da7dd630d.gif?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=34eff9beeda40d4e66184f9128de8a1c) |
| 勉強場所の口コミを検索できます。   他のユーザーが投稿した口コミを閲覧できます。 | 口コミ・施設情報の確認のほか、   経路情報も確認できます。 |

### サブ機能(ユーザー登録必要)

|  |  |
| --- | --- |
| (5) ブックマーク | (6) 口コミ投稿 |
| [![Image from Gyazo](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2Fe1f9e33e553c15b7f72eb63de2d074b3.gif?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=1a893c92fdc41c1db8c1a3734ab80087)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2Fe1f9e33e553c15b7f72eb63de2d074b3.gif?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=1a893c92fdc41c1db8c1a3734ab80087) | [![Image from Gyazo](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2F67b7613d3c0cc31ea93cb3c08b88df1a.gif?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=e2f6f2d1a74c29768beead989147211e)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2F67b7613d3c0cc31ea93cb3c08b88df1a.gif?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=e2f6f2d1a74c29768beead989147211e) |
| 施設のブックマークを登録できます。 | 口コミを投稿できます。   投稿したことをXでシェアできます。   投稿した口コミはマイページから確認できます。 |

|  |  |
| --- | --- |
| (7) 口コミへのいいね | (8) マイページ |
| [![Image from Gyazo](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2F3dfe5741323094769521aa4255ac79a3.gif?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=1e997b42180a8b63be9edf66149520f0)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2F3dfe5741323094769521aa4255ac79a3.gif?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=1e997b42180a8b63be9edf66149520f0) | [![Image from Gyazo](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2Fceb2e8c89660190242fdea4e2dd63453.gif?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=a20dc2d4d1eaf0c7ea06d2b7b03760a4)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2Fceb2e8c89660190242fdea4e2dd63453.gif?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=a20dc2d4d1eaf0c7ea06d2b7b03760a4) |
| 口コミへのいいねができます。   いいねした口コミはマイページから確認できます。 | マイページで「ユーザー情報の編集・退会」   や「投稿・いいねした口コミ」の確認ができます。 |

### その他

- Google認証によるユーザー登録・ログイン機能
- パスワードリセット機能
- 検索時のオートコンプリート(施設名)
- Xシェア機能
- 施設情報
- 口コミ投稿
- 様々なタイプでのソート機能
- 施設の「口コミ数」「googleレビュー」
- 口コミの「投稿日」「いいね数」
- トップページに使用方法や施設の違いなどを表示
- ヘッダーにQRコード表示でスマホからの利用を誘導
- 未ログイン者がログイン必要な機能に触れると「ログイン誘導モーダル」表示
- 存在しないURLに対するエラーハンドリング(idを含むもの・その他)
- XSS対策
- お問い合わせフォーム
- 利用規約
- プライバシーポリシー
- PWA対応
- SEO対策
- GitHub Actionsによるテスト自動化(RSpec・RuboCop)

## 4\. 技術構成

### 使用技術

| カテゴリ | 技術スタック |
| --- | --- |
| フロントエンド | Rails 7.1.3.4 (Hotwire/Turbo/Stimulus), JavaScript, Tailwind CSS, daisyUI |
| バックエンド | Rails 7.1.3.4 (Ruby 3.2.3) |
| データベース | PostgreSQL |
| インフラ | Render.com, Amazon S3 |
| 開発環境 | Docker |
| 認証 | Sorcery, Googleログイン |
| API | Google Maps API, Google Places API |

### 画面遷移図

### ER図

[![Image from Gyazo](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2F3df832f88ab47e8f3cda4b5963107802.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=42c8d446ac22a4942c103a1a52445b3a)](https://gyazo.com/3df832f88ab47e8f3cda4b5963107802)

[詳細URLはこちら](https://www.mermaidchart.com/raw/b6d7e76d-8d55-429f-98b9-ca6ed3a8d236?theme=dark&version=v0.1&format=svg)

## 5\. こだわった点

## 5.1 スマホ利用を想定した機能設計

### ボトムナビゲーションの採用

ボトムナビゲーションを画面下部に配置し、主要なページ・機能に1アクションで辿り着けるようにしました。

[![Image from Gyazo](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2F6f94076faadadc92b40368c7572917bd.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=682744e1ead4f8e5f27cfe582fdf0652)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2F6f94076faadadc92b40368c7572917bd.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=682744e1ead4f8e5f27cfe582fdf0652)

### QRコード表示でスマホからのアクセスを易化

QRコードをヘッダーのドロワー内に配置し、スマホでのアクセスが容易にできるよう心掛けました。  
主に下記のような状況下でメリットを発揮すると想定しています。

- PC利用者がスマホで利用する場合
- 複数人で勉強場所を探している際に、本サービスのリンクをシェアする場合

[![Image from Gyazo](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2F1fcf68683a09cfce862f43418c8fb2a8.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=a93ae92eec315de69548a237c08b01e2)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2F1fcf68683a09cfce862f43418c8fb2a8.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=a93ae92eec315de69548a237c08b01e2)

なお、このQRコードのアイデアについては、スクールの先輩受講生のアプリ「SpeakUP」を参考にさせて頂きました。

- アプリのURL：[https://speakup-app.com/](https://speakup-app.com/)
- リポジトリのURL：[https://github.com/erika328/SpeakUp](https://github.com/erika328/SpeakUp)

### スマホでの操作を考慮したMap表示

「場所検索」ページでは、画面の縦幅を取得し、可能な限りMapの表示エリアを広げる設計にしています。

[![Image from Gyazo](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2F13a92b7377c37bb988ae911ef0a34b92.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=c59181c7517bd76f25723dc9f0238fe5)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2F13a92b7377c37bb988ae911ef0a34b92.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=c59181c7517bd76f25723dc9f0238fe5)

「施設の詳細情報」ページでも同様に、指でのピンチイン・ピンチアウトが十分にできるだけの幅を確保した設計にしています。

[![Image from Gyazo](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2Fe6e352f1e382ffc34819f344dc6d7370.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=80dd6959ed6303165e40d6563a5a1773)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2Fe6e352f1e382ffc34819f344dc6d7370.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=80dd6959ed6303165e40d6563a5a1773)

## 5.2 ユーザビリティの向上

### PWA(プログレッシブウェブアプリ)対応

PWA対応により、PCやスマホでネイティブアプリのような使い勝手を提供します。

＜PCで利用の場合＞  
例えばMacBookの場合、Dockに配置して利用できます。  
画面表示もスッキリします。

[![Image from Gyazo](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2F13895edf74e5fb68d90563edbbdbf0e8.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=7176254dd13649dc744583b4fd1ec07f)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2F13895edf74e5fb68d90563edbbdbf0e8.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=7176254dd13649dc744583b4fd1ec07f) [![Image from Gyazo](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2F526e79809e821d0b1bf6cc8be61c167b.jpg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=84c1449127097548975f9271a9d2edcc)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2F526e79809e821d0b1bf6cc8be61c167b.jpg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=84c1449127097548975f9271a9d2edcc)

＜スマホで利用の場合＞  
スマホも同様、ホーム画面に追加できます。  
画面表示も広くなり、利用しやすくなります。

[![Image from Gyazo](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2F90077af30fd9ccfca00f3487ad509ed0.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=f60da3e772a4bc5d5441c47c00147d7e)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2F90077af30fd9ccfca00f3487ad509ed0.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=f60da3e772a4bc5d5441c47c00147d7e) [![Image from Gyazo](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2F44dcbf7b2050d32bb3632355d3e64548.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=f6e6ae1cefd587238d34718e456f28f2)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2F44dcbf7b2050d32bb3632355d3e64548.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=f6e6ae1cefd587238d34718e456f28f2)

### プラスαの情報はモーダル・ドロップダウンを利用

必ずしも全ユーザーに見せる必要がないようなプラスαの情報などは、モーダル・ドロップダウンを利用するなどしています。  
これにより画面内はなるべくスッキリさせ、ユーザーを迷わせないようにしています。

[![Image from Gyazo](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2Fbfff237ba95f9ee71f9b0378df13d151.gif?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=9031fa5945831e3fb74a9300cb8c17af)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2Fbfff237ba95f9ee71f9b0378df13d151.gif?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=9031fa5945831e3fb74a9300cb8c17af) [![Image from Gyazo](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2F10321732808aedfa3bd9719f04874aa8.gif?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=ffa7aa16149eb04247c365007f53ec2d)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2F10321732808aedfa3bd9719f04874aa8.gif?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=ffa7aa16149eb04247c365007f53ec2d)

### 入力文字数のリアルタイム表示

本サービスの口コミ投稿フォームでは、300文字の入力制限を設けています。  
その際、入力文字数をリアルタイム表示し、文字数確認できるようにしています。

[![Image from Gyazo](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2F13c657dfa6ccacb92b9bfa6256c7ab7a.gif?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=533a9bec91e3f8da3b2dd2ff11cc5b7e)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2F13c657dfa6ccacb92b9bfa6256c7ab7a.gif?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=533a9bec91e3f8da3b2dd2ff11cc5b7e)

### 1アクションで辿り着けないページには「戻る」ボタンを表示

ヘッダーやボトムナビゲーションから1アクションで辿り着けないような"階層が深い"ページには「戻る」ボタンを設置し、遷移前のURL情報を利用するなどして、元のページへ戻れるようにしています。

[![Image from Gyazo](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2Fb703290c2ddef1108b60db42584cff86.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=95ebe6c2e591a3aa3868408e01f4b231)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2Fb703290c2ddef1108b60db42584cff86.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=95ebe6c2e591a3aa3868408e01f4b231)

### 未ログイン者に対し、ストレスなくログインに誘導

未ログイン者に対してもログインが必要な機能(ブックマーク、口コミへの投稿・いいね)は露出させ、ログインへの誘導を図っています。  
また、ログインページに遷移させるのではなく、モーダル表示によって「そのページに留まるか」「ログインするか」を選択できるようにし、ストレスのない利用ができるよう心掛けています。

[![Image from Gyazo](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2Fe28a6e1f76b6baa271bff7f23a206349.gif?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=be32c194f74391a0c534df0a39a191c7)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2Fe28a6e1f76b6baa271bff7f23a206349.gif?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=be32c194f74391a0c534df0a39a191c7)

### 検索フォームでのオートコンプリート

検索フォームにオートコンプリート機能をつけることで、ユーザーの文字入力の手間を省き、快適な検索を可能にしています。

[![Image from Gyazo](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2F4852e5ca4abb688cecc4b0a3c7374dcd.gif?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=4e1e205abace5883b57bd29e5c505d5f)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2F4852e5ca4abb688cecc4b0a3c7374dcd.gif?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=4e1e205abace5883b57bd29e5c505d5f)

## 5.3 エラーハンドリング・セキュリティなど

### XSS対策

今回、ユーザーがテキストを入力できる「口コミ」に関しては、HTMLタグやスクリプトを無効化し、XSS攻撃を防止しています。

[![Image from Gyazo](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2F839e37689e96bcb7582d4c7987cad49c.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=8ce6f1bbe2b29e133efded7633087da6)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2F839e37689e96bcb7582d4c7987cad49c.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=8ce6f1bbe2b29e133efded7633087da6)

### idを含むURLのエラーハンドリング

「施設情報」や「口コミ詳細」ページはidを含んだURLとなっているため、存在しないid(又は削除された口コミのid)が入力された際はトップページへリダイレクトするようにしています。

[![Image from Gyazo](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2Fb6ad1f783cfd747835828db4d7fe0799.gif?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=619e49c3d802db6aa4a44aefe16dc9b5)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2Fb6ad1f783cfd747835828db4d7fe0799.gif?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=619e49c3d802db6aa4a44aefe16dc9b5)

### 404ページのカスタマイズ

ユーザーがURLを間違えて入力した際に表示する404エラーページもカスタマイズしています。

[![Image from Gyazo](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2F37d348df5eb73979130b23e2c6b53e6c.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=258cb2166968e66e72b5d12602eea422)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fi.gyazo.com%2F37d348df5eb73979130b23e2c6b53e6c.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=258cb2166968e66e72b5d12602eea422)

## 6\. 今後の展望

### 対応エリア・施設数の拡大

現在、総務省統計局の公表している「大都市」に分類される地域を含んだ、15都道府県の約600施設を登録しています。  
今後はこれを日本全国に拡大していきたいと考えています。  
[大都市について(総務省統計局)](https://www.stat.go.jp/data/kokusei/2010/users-g/word7.htm#:~:text=%E3%80%8C%E5%A4%A7%E9%83%BD%E5%B8%82%E3%80%8D%E3%81%A8%E3%81%AF%EF%BC%8C,%E5%8C%BA%E9%83%A8%E3%82%92%E3%81%84%E3%81%84%E3%81%BE%E3%81%99%E3%80%82&text=%E5%B9%B3%E6%88%9022%E5%B9%B4%E8%AA%BF%E6%9F%BB%E3%81%A7%E3%81%AF,%E5%B9%B4%E3%81%AB%E6%96%B0%E3%81%9F%E3%81%AB%E8%A8%AD%E5%AE%9A%EF%BC%89%E3%80%82)

### 施設種類・診断機能の追加

施設の種類を「(学習が可能な)図書館」などにも拡張し、オススメの勉強場所を診断する機能も追加したいと考えています。

### テストコードの拡充

本記事執筆時点では、RSpecによるテストコードのうち、モデルスペックしか書けていなかったので、これからシステムスペックも記述することでカバレッジ率を上げていきたいです。

## 7\. 最後に

今回のアプリ作成にあたり、お力添え頂いた全ての方々に心よりお礼申し上げます🙇‍♂️

10ヶ月程プログラミング学習をしてみて、学習前とは見える世界が一変したように感じますし、同時に知識不足も実感していて、まだまだ勉強し続けていくのだろうなと感じています📚

本サービスについては、今後も「学ぶ人をサポートするサービス」として価値提供できるよう、機能のブラッシュアップを図りたいと思います。

最後までご覧頂きありがとうございました！

※ X(旧Twitter)もやっているので、よろしければフォローして頂けると嬉しいです。