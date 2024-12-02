---
title: "小売業における数理最適化事例 - Qiita"
source: "https://qiita.com/mizoguchi_ryosuke/items/80a86b5ada2c41687a3b?utm_campaign=popular_items&utm_medium=feed&utm_source=popular_items"
author:
  - "[[mizoguchi_ryosuke]]"
published: 2024-12-01
created: 2024-12-02
description: "はじめにTRIAL＆RetailAI Advent Calendar 2024 の 2日目の記事です。昨日は @rockmetoou さんの『Safely sync database clust…"
tags:
  - "clippings"
---
9一度削除した記事は復旧できません。

この記事の編集中の下書きも削除されます。

削除してよろしいですか？

- [はじめに](https://qiita.com/mizoguchi_ryosuke/items/?utm_campaign=popular_items&utm_medium=feed&utm_source=popular_items#%E3%81%AF%E3%81%98%E3%82%81%E3%81%AB)
- [数理最適化とは？](https://qiita.com/mizoguchi_ryosuke/items/?utm_campaign=popular_items&utm_medium=feed&utm_source=popular_items#%E6%95%B0%E7%90%86%E6%9C%80%E9%81%A9%E5%8C%96%E3%81%A8%E3%81%AF)
- [達成したいイメージ](https://qiita.com/mizoguchi_ryosuke/items/?utm_campaign=popular_items&utm_medium=feed&utm_source=popular_items#%E9%81%94%E6%88%90%E3%81%97%E3%81%9F%E3%81%84%E3%82%A4%E3%83%A1%E3%83%BC%E3%82%B8)
- [お題](https://qiita.com/mizoguchi_ryosuke/items/?utm_campaign=popular_items&utm_medium=feed&utm_source=popular_items#%E3%81%8A%E9%A1%8C)
- [設定](https://qiita.com/mizoguchi_ryosuke/items/?utm_campaign=popular_items&utm_medium=feed&utm_source=popular_items#%E8%A8%AD%E5%AE%9A)
- [条件：期間ごとの最大需要数](https://qiita.com/mizoguchi_ryosuke/items/?utm_campaign=popular_items&utm_medium=feed&utm_source=popular_items#%E6%9D%A1%E4%BB%B6%E6%9C%9F%E9%96%93%E3%81%94%E3%81%A8%E3%81%AE%E6%9C%80%E5%A4%A7%E9%9C%80%E8%A6%81%E6%95%B0)
- [アプローチ：凸二次計画問題](https://qiita.com/mizoguchi_ryosuke/items/?utm_campaign=popular_items&utm_medium=feed&utm_source=popular_items#%E3%82%A2%E3%83%97%E3%83%AD%E3%83%BC%E3%83%81%E5%87%B8%E4%BA%8C%E6%AC%A1%E8%A8%88%E7%94%BB%E5%95%8F%E9%A1%8C)
- [最適化結果](https://qiita.com/mizoguchi_ryosuke/items/?utm_campaign=popular_items&utm_medium=feed&utm_source=popular_items#%E6%9C%80%E9%81%A9%E5%8C%96%E7%B5%90%E6%9E%9C)
- [まとめ](https://qiita.com/mizoguchi_ryosuke/items/?utm_campaign=popular_items&utm_medium=feed&utm_source=popular_items#%E3%81%BE%E3%81%A8%E3%82%81)
- [参考文献](https://qiita.com/mizoguchi_ryosuke/items/?utm_campaign=popular_items&utm_medium=feed&utm_source=popular_items#%E5%8F%82%E8%80%83%E6%96%87%E7%8C%AE)

## はじめに

[TRIAL＆RetailAI Advent Calendar 2024](https://qiita.com/advent-calendar/2024/retail-ai) の 2日目の記事です。

昨日は [@rockmetoou](https://qiita.com/rockmetoou) さんの『[Safely sync database cluster to a standalone database for local usage](https://qiita.com/rockmetoou/items/3c8d2dee50623bde0675)』という記事でした。

運用上の負担軽減いい感じですね🙌

本日は、**『小売業における数理最適化事例』** です  
小売業での応用事例のイメージが少しでも伝わればと思っております🙇

## 数理最適化とは？

数理最適化は、最適な資源配分を行う数学的手法です

- 限られた資源を効率的に使い、最大の効果を引き出します
- 企業経営や交通、エネルギー管理などで活用されています
- 線形計画法や整数計画法などの具体的な手法があります

[![](https://qiita-user-contents.imgix.net/https%3A%2F%2Forsj.org%2Fwp-content%2Fuploads%2F2021%2F02%2FEmqZkzUUcAANeXx.jpg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=75931aa97d66fde02aaeab6746114b45)](https://qiita-user-contents.imgix.net/https%3A%2F%2Forsj.org%2Fwp-content%2Fuploads%2F2021%2F02%2FEmqZkzUUcAANeXx.jpg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=75931aa97d66fde02aaeab6746114b45)

図引用：[ORを探せ！](https://orsj.org/?page_id=3362)

## 達成したいイメージ

**『 ある数量の、ある商品を、特定の期間で、店舗ごとの規模感や、季節性(需要)などを加味して店舗別に配分したい 』**

*モチベーション* ⇨ 多くの必要としている方にできるだけ行き渡るようにしたい💪

## お題

**『 合計「1,000個」のある商品「〇〇〇」を「5期間」に「5店舗」で、いい感じに配分する 』**

## 設定

- ある商品：架空の１商品(「〇〇〇」)
- 合計数量：1,000個
- 特定の期間：5期間
- 店舗数：5店舗
- large：1店舗
- middle：3店舗(middle1，middle2，middle3)
- small：1店舗
- 規模感
- large：middleの2倍の需要
- small：middleの0.5倍の需要
- 季節性(需要)：以下の図にある３パターン
- 各店舗は、以下のパターンで売れていくとする
- pt1：large，middle1，small
- pt2：middle2
- pt3：middle3

[![figure1.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3618314%2Fb0c1fac0-cd96-32f2-1616-bc79c4bcd559.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=869d9dac32be9d46a722539100b2f7ad)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3618314%2Fb0c1fac0-cd96-32f2-1616-bc79c4bcd559.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=869d9dac32be9d46a722539100b2f7ad)

## 条件：期間ごとの最大需要数

今回、各フォーマットごとの各期間における需要数の上限値は以下のものとする

- middle
- 期間1,2,3,4,5 ＝　\[100, 50, 50, 50, 20\]
- 期間1の最大需要数：100個、期間2の最大需要数：50個、...
- large：middleの2倍の需要
- 期間1,2,3,4,5 ＝　\[200, 100, 100, 100, 40\]
- small：middleの0.5倍の需要
- 期間1,2,3,4,5 ＝　\[50, 25, 25, 25, 10\]

## アプローチ：凸二次計画問題

凸二次計画問題は、目的関数が二次関数で制約条件が線形の最適化問題です

- 目的は、与えられた制約の中でこの二次関数の値を最小化または最大化することです
- この問題は、ポートフォリオ最適化や機械学習など多くの分野で応用されます
- 効率的なアルゴリズムが存在し、数理的に解きやすい特徴があります

## 最適化結果

以下の3つの条件を元に最適化します

- 需要(パターン)
- 各期間の最大需要数(例：middle⇨\[100, 50, 50, 50, 20\])
- 全体の数量(= 1,000個)

最適化結果

- それぞれのフォーマットで各期間の最大需要数を超えることがないです
- パターンと同じイメージの配分になっています
- 5店舗、5期間の合計が1,000個になっています

[![ローカル画像](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3618314%2Fecd2fcfb-edef-ad43-319e-9859997bfca4.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=806012411ae880ae8d27ec03dc807d4b)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3618314%2Fecd2fcfb-edef-ad43-319e-9859997bfca4.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=806012411ae880ae8d27ec03dc807d4b) [![](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3618314%2F01fcd63f-b079-9593-2a9b-b71733bdca1e.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=a4c96ab519d7aa7dd17f7154b4390775)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F3618314%2F01fcd63f-b079-9593-2a9b-b71733bdca1e.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=a4c96ab519d7aa7dd17f7154b4390775)

最適化結果の個人的な解釈

- largeがmiddle1,middle2の約2倍、smallの約4倍の配分になっていて、いい感じです
- middle3が全体で129個であり、まだ配分出来そうなので合計数量はもう少し多くても良さそうです
- わかりやすく1,000個にしてみました⇨この条件なら1,100個でも良さそうです

## まとめ

実務では、様々な制約に悪戦苦闘しながら日々頑張っています💪

明日は、[@yang\_zaiqi](https://qiita.com/yang_zaiqi)さんの「俺のAndroid™ スマートフォンで大規模言語AIモデルを動かせるの？」という記事です。お楽しみに！

RetailAIとTRIALではエンジニアを募集しています。  
興味がある方はご連絡ください！

## 参考文献

- しっかり学ぶ数理最適化

- Pythonではじめる数理最適化（第2版）

9

一度削除した記事は復旧できません。

この記事の編集中の下書きも削除されます。

削除してよろしいですか？