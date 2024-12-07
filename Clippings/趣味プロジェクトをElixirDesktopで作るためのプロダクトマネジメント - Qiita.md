---
title: "趣味プロジェクトをElixirDesktopで作るためのプロダクトマネジメント - Qiita"
source: "https://qiita.com/the_haigo/items/e9976202d5c0a9c625ce?utm_campaign=popular_items&utm_medium=feed&utm_source=popular_items"
author:
  - "[[the_haigo]]"
published: 2024-11-22
created: 2024-11-23
description: "はじめにこの記事はElixirアドベントカレンダー2024のシリーズ２、4日目の記事ですhttps://qiita.com/advent-calendar/2024/elixirElixirD…"
tags:
  - "clippings"
---
## はじめに

この記事はElixirアドベントカレンダー2024のシリーズ２、4日目の記事です

ElixirDesktopでモバイルアプリを作る際の１人PdMでプロダクトの作成についてざっくりと実際にやっていきます

## 参考にするもの

プロダクトを作るにあたって色々考えないといけないことがあり、  
プロダクトマネジメントのすべての以下の章を参考に進めていきたいと思います

第２部 プロダクトを育てる

- ４章プロダクトの４階層
- ５章プロダクトのCore
- ６章プロダクトのWhy
- ７章プロダクトのWhat
- ８章プロダクトのHow

## プロダクトの４階層

プロダクトの解消は以下の４つがあり、関係は下図のようになっています

- Core プロダクトの世界観、企業への貢献
- Why 「誰」を「どんな状態にしたいか」、なぜ自社がするのか
- What ユーザー体験、ビシネスモデル、ロードマップ
- How　どのように実装するのか

それぞれを決めていきましょう  
趣味プロなのでざっくりと

## プロダクトのCore

ここで決めることは大きく２つの項目があります

- プロダクトの世界観を構築する ->　ミッション・ビジョン
- 企業への貢献 ->　事業戦略

ミッション、ビジョン、事業戦略をそれぞれ考えてみました

### ビジョン

旅に関する情報の収集・整理と再利用

### ミッション

すぐに流れていってしまうフロー型の情報を貯蔵していくストック型の情報にし  
振り返り、再利用、新たなインサイトを得ることにつなげていく

### 事業戦略

ドメイン  
ブログやSNS経由のアフェリエイト

ドメインでの勝ち筋  
登山やキャンプ、ダイビングなど装備が多く継続して行う趣味において、  
次の候補地の収集、ルートの選定、装備の見直しはよく行われるが大体が本人の記憶、メモツールで行われる

それを特定にフォーマットを作成して継続的な改善や共有を通して製品の販売足品に繋げたい

通常のブログだとレビュー内容の商品のリンクだけを貼ることが多いが、装備リスト・持ち物リストをアバターとして貼ることでより多くの商品に対して導線を増やすことができる。

## プロダクトのWhy

ここで決めるのは大きく２つの項目があります

- 「誰」を「どんな状態にしたいか」 -> ターゲットユーザー、ペインとゲイン
- なぜ自社がやるのか -> 市場分析、競合分析

ターゲットユーザー、ペインとゲイン、市場分析、競合分析を考えてみます

## ターゲットユーザー

ユーザー１ 行ってみたい場所やってみたいことが多くあり日頃から情報収集を行う人  
ユーザー２ キャンプや登山など持っていくものが多く継続的に行う趣味を持っていて、ブログ等でキャンプ用品のレビューを行っている

## ペインとゲイン

### ユーザー１

### ペイン

テレビや雑誌、会話、SNS等で知ったお店を後から行ってみようと思っていても思い出せない、そもそも存在を忘れている事が多々ある

### ゲイン

その場ですぐに探せて保存できる  
後々今日はカレーの気分だから前保存したカレーフォルダから選ぶということができる

### ユーザー２

### ペイン

キャンプ、登山はシーズンごとに持っていくものが違い、次回行くのは１年後だったりするので  
前回何を持っていって、使わなかった、また持っていきたい、これが必要というのを忘れがち

持っていった商品のレビュー記事を書く場合、アフェリエイトリンクはレビューした商品と関連商品に限られる

### ゲイン

定番の装備を保存して、次回のキャンプのときに持ち物チェックリストとして使用する  
キャンプ時の持っていった消耗品と途中で購入したものを記録し、前回買いすぎだったから今回は控えめにして置こうと振り返りとか営繕を行う

定番の装備と所持品をアバターとしてブログに表示し、今回の装備や所持品もアフェリエイトリンクとして楽に記載でき、複数の導線からアフェリエイト報酬を得やすくする

## 市場分析

いろいろあるが、STP（セグメンテーション、ターゲッティング、ポジショニング）を行う

### セグメンテーション

ライト 旅行、食べ歩き、映えスポット -> 流行り物が好き  
ヘビー　キャンプ、登山、ダイビング -> アウトドア趣味

### ターゲッティング

大学生(ライト勢）-> とりあえず広く使ってもらうために、行ってみたい場所をストックしてもらうことをメイン  
会社員（ガチ勢） ->　キャンプや登山の振り返りや持ち物の管理を行うことをメイン

### ポジショニング

交流の場やプラットフォームではなく、個人の記録をメインとする  
個人の記録（装備や持ち物）をSNSやブログ等で共有するためのサポートツール

## 競合分析

GoogleMap

地図、検索、ナビゲーション、お気に入り登録

メイン機能は地図なので、お気に入り登録等は使いにくい

ヤマップ

検索、サジェスト、グッズ、ロギング

主に山を限定としている、行ったところを記録したりできる。  
グッズの販売等も行っているが、登山に持っていった装備を管理する機能はない

なっぷ

いった、いきたいの記録、予約、検索

主にキャンプ場を限定している、行った・行きたいところを記録したりできる。  
キャンプ用品の販売もしているが、キャンプに持っていった装備を管理する機能はない

まとめると  
汎用的な行きたい場所のストックが強いものはなく、  
自分の持ち物、装備を管理する機能はない

## 誰をどんな状態にしたいか？

全体としては、行ってみたい場所を見つけたときに、すぐに記録できるようにしたい  
使い込むユーザーとしては、装備の管理をできるようにし、旅の振り返り・共有を楽にしたい

## プロダクトのWhat

ここで決めるのは大きく3つの項目があります

- ユーザー体験 -> メンタルモデル、カスタマージャーニー
- ビジネスモデル -> コスト構造、収益モデル
- ロードマップ -> 指標、マイルストーン

収益モデルとかはまだ特に考えていないのでスキップして  
メンタルモデル、カスタマージャーニー、マイルストーンを考えていきます

## メンタルモデル

### ペルソナ１ ライトユーザー

性別：女性  
職業：大学生  
家族構成:一人暮らし  
年収:仕送り込みで200万

興味のあるカテゴリ  
料理、旅行、カフェ、スイーツ

情報源  
インスタグラム、tiktok、Twitter、友人、旅行雑誌、テレビ

### ペルソナ２　ヘビーユーザー

性別：男性  
職業：IT企業  
家族構成：一人暮らし  
年収：500万

興味のあるカテゴリ  
キャンプ、ツーリング、バイク、コーヒー、料理

情報源  
キャンプ専門誌、ネット、Twitter

## カスタマージャーニー

### ペルソナ１

友人との会話で気になったお店をストックする

|  | `検索` | `お店の詳細` | `ストック` |
| --- | --- | --- | --- |
| 行動 | アプリを開き、友人におすすめされたお店を検索 | 検索結果の該当するお店の詳細を閲覧 | お店を行きたいリストとしてストック |
| 思考 | おすすめされたお店がどんなところかを知りたい | 外観、内装、場所を知りたい | 今度行ってみたい |
| 接点 | 検索画面 | 検索結果詳細画面 | 検索結果詳細画面 |
| プロダクト | 検索機能 | 詳細画面表示   Webページを開く   地図アプリを開く | 行きたいリストに追加   フォルダに追加 |
| 強み   弱み | ストックすることがメインの機能なので登録・閲覧がしやすい | 外観と場所が確認でき、Webページや地図アプリで更に詳細に知ることができる | 単純に行きたいリストだけではなくカフェやイタリアンなどフォルダごとにストックできる |

休日にストックしたお店へ向かう

|  | `ストックした中からお店を探す` | `お店までの道を調べる` |
| --- | --- | --- |
| 行動 | アプリを開き、行きたいリストを表示し該当のお店を探す | お店の詳細画面から地図アプリを開く |
| 思考 | この前言ってたたお店どれだっけ | どこらへんにあったっけ |
| 接点 | ストック済み一覧画面、詳細画面 | 詳細画面,他社地図アプリ |
| プロダクト | ストック済み一覧表示、詳細 | 詳細画面、地図アプリの起動 |
| 強み   弱み | 行きたいリストだけではなく、各フォルダも一覧される | 使い慣れたアプリで開ける |

- 行動
- 思考
- 接点プロダクト
- 強み/弱み

### ペルソナ２

候補地の収集

|  | `検索` | `キャンプ場の詳細` | `ストック` |
| --- | --- | --- | --- |
| 行動 | アプリを開き、雑誌でおすすめされてたキャンプ場を検索 | 検索結果の該当するキャンプ場の詳細を閲覧 | キャンプ場を行きたいリストとしてストック |
| 思考 | おすすめされたキャンプ場がどんなところかを知りたい | ロケーション、周辺施設、場所を知りたい | 今度行ってみたい |
| 接点 | 検索画面 | 検索結果詳細画面 | 検索結果詳細画面 |
| プロダクト | 検索機能 | 詳細画面表示   Webページを開く   地図アプリを開く | 行きたいリストに追加   フォルダに追加 |
| 強み   弱み | ストックすることがメインの機能なので登録・閲覧がしやすい | 外観と場所が確認でき、Webページや地図アプリで更に詳細に知ることができる | 単純に行きたいリストだけではなくキャンプ場や温泉などフォルダごとにストックできる |

キャンプの計画を立てる

|  | `ルートの作成` | `持ち物リストを作成` | `持ち物のチェック` |
| --- | --- | --- | --- |
| 行動 | アプリを開き、ルートの作成し、寄る場所を追加していく | 持ち物を一覧から装備リストに追加 | 持ち物リストをもとに準備をする |
| 思考 | こことここもついでに行ってみたいな | 前回何持っていったっけ | これ前回足りなかったから多めに持っていこう |
| 接点 | ルート一覧、作成画面 | アバター一覧、編集 | アバター詳細 |
| プロダクト | ルート作成機能 | 持ち物リストの作成、編集、持ち物追加、削除 | 持ち物リスト詳細、消耗品管理 |
| 強み   弱み | ルートごとにピンを立てられる | アクティビティ事に持って行くものリストを作って前回何を持っていったかを確認できる | チェックリストとして使え、消耗品をどのくらい使ったか、残っているかをチェックできる |

休日にキャンプをしにいく

|  | `計画したルートを開く` | `キャンプ場を目的地に設定する` | `移動のGPSログを記録する` |
| --- | --- | --- | --- |
| 行動 | アプリを開き、計画したルートを開く | 地図画面を開いて、キャンプ場へのナビゲーションを開始 | ロギングを開始ボタンを押して移動開始 |
| 思考 | よしいくか！ | どこらへんにあったっけ | この道混んでるから次は迂回路探そう |
| 接点 | ルート一覧、詳細画面 | 詳細画面（地図） | 詳細画面（地図） |
| プロダクト | ルート一覧表示、詳細 | ルート詳細画面、ナビゲーション機能 | GPSロギング |
| 強み   弱み | 行きたいリストだけではなく、各フォルダも一覧される | ナビゲーションが他の地図アプリに比べて貧弱 | GPSログを後から見ることができ、次回はこの道行ってみようと振り返りができる |

大体必要な機能が見えてきましたね

## マイルストーン

初期リリース（今回のアドカレ）  
行きたい場所の検索、ストック  
旅行計画、遂行

次回リリース  
持ち物管理

以降  
各機能のブラッシュアップ

## プロダクトのHow

主に決めることは１つで

どのように実現するのか -> ユーザーインターフェース、設計と実装、Go to Market

ユーザーインターフェースと設計と実装を決めていきます  
Go to Marketはアプリ審査ということにしておいてスキップ

## ユーザーインターフェース

作ったのはこんな感じ

[![スクリーンショット 2024-11-22 15.50.23.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F64198%2F6260598c-755e-ed2a-1680-da98d1388de2.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=f29616065a73be02487a346e4b042130)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F64198%2F6260598c-755e-ed2a-1680-da98d1388de2.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=f29616065a73be02487a346e4b042130)

## 設計と実装

このアプリで実装したい機能は以下

1. 管理ダッシュボードのWebアプリ
2. ユーザー登録・ログイン機能
3. 行きたい場所・いった場所を検索・保存
4. GPSログの記録・描画
5. 旅行のプランを組み立て・遂行
6. アクティビティ事にアバターを設定
7. アバターに装備・持ち物・乗り物等をセットできる
8. 旅行のルートと使用したアバターをSNS等で公開できる
9. 旅行のルートと使用したアバターをブログパーツとして使用できる

規模的に1~4+アプリ申請をアドベントカレンダーで実装と解説を行います

## アプリ構成

実際にユーザーが操作するモバイルアプリ  
モバイルアプリのWebUI（スポット管理、GPSログの閲覧、旅行プランの組み立て）  
モバイルアプリのデータを保存するためのDB+メール送信等を行う管理ダッシュボード

WebUIと管理ダッシュボードは同一サーバーで動作する。

[![スクリーンショット 2024-11-02 23.40.01.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F64198%2Fbac35150-d084-faab-f51a-59310d771cfb.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=7a7b3accff40d5c4f07494015df40724)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F64198%2Fbac35150-d084-faab-f51a-59310d771cfb.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=7a7b3accff40d5c4f07494015df40724)

以下を今回フェーズ１で実装する機能とする

## モバイルアプリ

アプリ全体として必要な対応

- プロジェクトの作成
- i18n対応
- 500エラーからの復帰
- エラートラッキング
- Github Actions
- リリース
- ロゴの作成

## 管理ダッシュボード

機能

- プロジェクトの作成
- ログイン機能
- パスワードリセットのメール送信
- デプロイ

## ユーザー登録・ログイン機能

ここで関連するモデル  
ユーザー

機能

- アプリ起動時にスプラッシュイメージを表示する
- 起動後新規登録とログインへのリンクが有るWelcomeページを表示
- ユーザー登録
- ユーザー登録後のオンボーディング
- ログイン
- ログアウト
- ゲストユーザー登録
- ゲストユーザーからのアップグレード
- ユーザーの削除
- メールアドレスの変更
- パスワードの変更
- パスワードリセット

## 行きたい場所・行った場所

ここで関連するモデル  
フォルダ -> スポットのグルーピングを行う  
スポット -> 行きたい場所・行った場所を扱う

機能

- フォルダの作成
- フォルダ名の編集
- フォルダの削除
- フォルダを一覧し、配下のスポットをサムネイル表示
- クリックするとスポット一覧に移動
- スポットを検索する
- スポットを検索結果から登録する
- 登録時に作成済みのフォルダに振り分ける
- スポットにメモを追記できる
- 星を1~5で付けられる
- 行った、行きたいを切り替える

## GPSログの記録・描画

ここで関連するモデル  
ルート -> GPSログを記録する箱  
ポジション -> GPSログ

機能

- ルートの一覧
- ルートの作成
- ルートの設定の変更
- ルートの削除
- ルートの詳細
- - 地図の表示
- - 地図の操作（zoom in,out)
- - 現在位置の取得
- - ユーザーの移動に追従
- - ロギング開始
- - ロギング終了

## 最後に

大分ざっくりやって飛ばした箇所も多々ありますが  
軽くやるだけでも新たな発見や機能の精緻化につながったのでやってよかったと思います

本当はリーンキャンバスやSWOT分析とかやるべきなんでしょうけど趣味プロかつ分量が膨大になってしまうので一旦これで完了としておきたいと思います

次は実際にアプリを作っていこうと思います、本記事は以上になりますありがとうございました