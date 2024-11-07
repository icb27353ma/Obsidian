---
title: "先輩社員がどうやって不具合を解決しているのか - Qiita"
source: "https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417"
author:
  - "[[opengl-8080]]"
published: 2024-10-27
created: 2024-11-06
description: "自己紹介opengl-8080たまに Qiita で技術メモを書いたり関西在住・SIer 勤務はじめにシステム開発をしていると、いろいろな場面で不具合と遭遇する当然、不具合は解決しなけれ…"
tags:
  - "clippings"
---
![](https://relay-dsp.ad-m.asia/dmp/sync/bizmatrix?pid=c3ed207b574cf11376&d=x18o8hduaj&uid=160909)

449一度削除した記事は復旧できません。

この記事の編集中の下書きも削除されます。

削除してよろしいですか？

- [自己紹介](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E8%87%AA%E5%B7%B1%E7%B4%B9%E4%BB%8B)
- [はじめに](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E3%81%AF%E3%81%98%E3%82%81%E3%81%AB)
- [話すこと・対象者・前提](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E8%A9%B1%E3%81%99%E3%81%93%E3%81%A8%E5%AF%BE%E8%B1%A1%E8%80%85%E5%89%8D%E6%8F%90)
- [ざっくりとした流れ](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E3%81%96%E3%81%A3%E3%81%8F%E3%82%8A%E3%81%A8%E3%81%97%E3%81%9F%E6%B5%81%E3%82%8C)
- [何が起こっているかを正確に把握する](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E4%BD%95%E3%81%8C%E8%B5%B7%E3%81%93%E3%81%A3%E3%81%A6%E3%81%84%E3%82%8B%E3%81%8B%E3%82%92%E6%AD%A3%E7%A2%BA%E3%81%AB%E6%8A%8A%E6%8F%A1%E3%81%99%E3%82%8B)
- [「正確に」把握することの重要さ](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E6%AD%A3%E7%A2%BA%E3%81%AB%E6%8A%8A%E6%8F%A1%E3%81%99%E3%82%8B%E3%81%93%E3%81%A8%E3%81%AE%E9%87%8D%E8%A6%81%E3%81%95)
- [ざっくりとした流れ](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E3%81%96%E3%81%A3%E3%81%8F%E3%82%8A%E3%81%A8%E3%81%97%E3%81%9F%E6%B5%81%E3%82%8C-1)
- [不具合を再現させる](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E4%B8%8D%E5%85%B7%E5%90%88%E3%82%92%E5%86%8D%E7%8F%BE%E3%81%95%E3%81%9B%E3%82%8B)
- [できればローカルで再現させる](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E3%81%A7%E3%81%8D%E3%82%8C%E3%81%B0%E3%83%AD%E3%83%BC%E3%82%AB%E3%83%AB%E3%81%A7%E5%86%8D%E7%8F%BE%E3%81%95%E3%81%9B%E3%82%8B)
- [再現させられない場合](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E5%86%8D%E7%8F%BE%E3%81%95%E3%81%9B%E3%82%89%E3%82%8C%E3%81%AA%E3%81%84%E5%A0%B4%E5%90%88)
- [ざっくりとした流れ](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E3%81%96%E3%81%A3%E3%81%8F%E3%82%8A%E3%81%A8%E3%81%97%E3%81%9F%E6%B5%81%E3%82%8C-2)
- [例外がスローされる不具合の場合](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E4%BE%8B%E5%A4%96%E3%81%8C%E3%82%B9%E3%83%AD%E3%83%BC%E3%81%95%E3%82%8C%E3%82%8B%E4%B8%8D%E5%85%B7%E5%90%88%E3%81%AE%E5%A0%B4%E5%90%88)
- [ざっくりとした流れ](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E3%81%96%E3%81%A3%E3%81%8F%E3%82%8A%E3%81%A8%E3%81%97%E3%81%9F%E6%B5%81%E3%82%8C-3)
- [例外の発生箇所を特定する](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E4%BE%8B%E5%A4%96%E3%81%AE%E7%99%BA%E7%94%9F%E7%AE%87%E6%89%80%E3%82%92%E7%89%B9%E5%AE%9A%E3%81%99%E3%82%8B)
- [スタックトレース](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E3%82%B9%E3%82%BF%E3%83%83%E3%82%AF%E3%83%88%E3%83%AC%E3%83%BC%E3%82%B9)
- [スタックトレースの読み方](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E3%82%B9%E3%82%BF%E3%83%83%E3%82%AF%E3%83%88%E3%83%AC%E3%83%BC%E3%82%B9%E3%81%AE%E8%AA%AD%E3%81%BF%E6%96%B9)
- [スタックトレースの読み方２（Caused by）](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E3%82%B9%E3%82%BF%E3%83%83%E3%82%AF%E3%83%88%E3%83%AC%E3%83%BC%E3%82%B9%E3%81%AE%E8%AA%AD%E3%81%BF%E6%96%B9%EF%BC%92caused-by)
- [スタックトレースの読み方・まとめ](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E3%82%B9%E3%82%BF%E3%83%83%E3%82%AF%E3%83%88%E3%83%AC%E3%83%BC%E3%82%B9%E3%81%AE%E8%AA%AD%E3%81%BF%E6%96%B9%E3%81%BE%E3%81%A8%E3%82%81)
- [ざっくりとした流れ](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E3%81%96%E3%81%A3%E3%81%8F%E3%82%8A%E3%81%A8%E3%81%97%E3%81%9F%E6%B5%81%E3%82%8C-4)
- [例外の直接原因を特定する](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E4%BE%8B%E5%A4%96%E3%81%AE%E7%9B%B4%E6%8E%A5%E5%8E%9F%E5%9B%A0%E3%82%92%E7%89%B9%E5%AE%9A%E3%81%99%E3%82%8B)
- [例外の発生箇所を確かめる](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E4%BE%8B%E5%A4%96%E3%81%AE%E7%99%BA%E7%94%9F%E7%AE%87%E6%89%80%E3%82%92%E7%A2%BA%E3%81%8B%E3%82%81%E3%82%8B)
- [直接原因で止まってはいけない](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E7%9B%B4%E6%8E%A5%E5%8E%9F%E5%9B%A0%E3%81%A7%E6%AD%A2%E3%81%BE%E3%81%A3%E3%81%A6%E3%81%AF%E3%81%84%E3%81%91%E3%81%AA%E3%81%84)
- [ざっくりとした流れ](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E3%81%96%E3%81%A3%E3%81%8F%E3%82%8A%E3%81%A8%E3%81%97%E3%81%9F%E6%B5%81%E3%82%8C-5)
- [例外の根本原因を特定する](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E4%BE%8B%E5%A4%96%E3%81%AE%E6%A0%B9%E6%9C%AC%E5%8E%9F%E5%9B%A0%E3%82%92%E7%89%B9%E5%AE%9A%E3%81%99%E3%82%8B)
- [根本原因を特定する方法](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E6%A0%B9%E6%9C%AC%E5%8E%9F%E5%9B%A0%E3%82%92%E7%89%B9%E5%AE%9A%E3%81%99%E3%82%8B%E6%96%B9%E6%B3%95)
- [デバッガの仕組み](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E3%83%87%E3%83%90%E3%83%83%E3%82%AC%E3%81%AE%E4%BB%95%E7%B5%84%E3%81%BF)
- [デバッグ接続可能な状態でJVMを起動する](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E3%83%87%E3%83%90%E3%83%83%E3%82%B0%E6%8E%A5%E7%B6%9A%E5%8F%AF%E8%83%BD%E3%81%AA%E7%8A%B6%E6%85%8B%E3%81%A7jvm%E3%82%92%E8%B5%B7%E5%8B%95%E3%81%99%E3%82%8B)
- [IDE でデバッガを起動する](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#ide-%E3%81%A7%E3%83%87%E3%83%90%E3%83%83%E3%82%AC%E3%82%92%E8%B5%B7%E5%8B%95%E3%81%99%E3%82%8B)
- [デバッガの使い方](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E3%83%87%E3%83%90%E3%83%83%E3%82%AC%E3%81%AE%E4%BD%BF%E3%81%84%E6%96%B9)
- [ブレークポイントを設定する](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E3%83%96%E3%83%AC%E3%83%BC%E3%82%AF%E3%83%9D%E3%82%A4%E3%83%B3%E3%83%88%E3%82%92%E8%A8%AD%E5%AE%9A%E3%81%99%E3%82%8B)
- [デバッガの見方](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E3%83%87%E3%83%90%E3%83%83%E3%82%AC%E3%81%AE%E8%A6%8B%E6%96%B9)
- [操作方法](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E6%93%8D%E4%BD%9C%E6%96%B9%E6%B3%95)
- [変数の値を管理する](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E5%A4%89%E6%95%B0%E3%81%AE%E5%80%A4%E3%82%92%E7%AE%A1%E7%90%86%E3%81%99%E3%82%8B)
- [任意の式を実行する](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E4%BB%BB%E6%84%8F%E3%81%AE%E5%BC%8F%E3%82%92%E5%AE%9F%E8%A1%8C%E3%81%99%E3%82%8B)
- [条件付きブレークポイント](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E6%9D%A1%E4%BB%B6%E4%BB%98%E3%81%8D%E3%83%96%E3%83%AC%E3%83%BC%E3%82%AF%E3%83%9D%E3%82%A4%E3%83%B3%E3%83%88)
- [例外がスローされたら一時停止する](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E4%BE%8B%E5%A4%96%E3%81%8C%E3%82%B9%E3%83%AD%E3%83%BC%E3%81%95%E3%82%8C%E3%81%9F%E3%82%89%E4%B8%80%E6%99%82%E5%81%9C%E6%AD%A2%E3%81%99%E3%82%8B)
- [フィールドの値が変更されたら一時停止する](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E3%83%95%E3%82%A3%E3%83%BC%E3%83%AB%E3%83%89%E3%81%AE%E5%80%A4%E3%81%8C%E5%A4%89%E6%9B%B4%E3%81%95%E3%82%8C%E3%81%9F%E3%82%89%E4%B8%80%E6%99%82%E5%81%9C%E6%AD%A2%E3%81%99%E3%82%8B)
- [その他にも便利そうな機能が色々](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E3%81%9D%E3%81%AE%E4%BB%96%E3%81%AB%E3%82%82%E4%BE%BF%E5%88%A9%E3%81%9D%E3%81%86%E3%81%AA%E6%A9%9F%E8%83%BD%E3%81%8C%E8%89%B2%E3%80%85)
- [例外がスローされる不具合の場合 まとめ](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E4%BE%8B%E5%A4%96%E3%81%8C%E3%82%B9%E3%83%AD%E3%83%BC%E3%81%95%E3%82%8C%E3%82%8B%E4%B8%8D%E5%85%B7%E5%90%88%E3%81%AE%E5%A0%B4%E5%90%88-%E3%81%BE%E3%81%A8%E3%82%81)
- [ざっくりとした流れ](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E3%81%96%E3%81%A3%E3%81%8F%E3%82%8A%E3%81%A8%E3%81%97%E3%81%9F%E6%B5%81%E3%82%8C-6)
- [例外がスローされない不具合の場合](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E4%BE%8B%E5%A4%96%E3%81%8C%E3%82%B9%E3%83%AD%E3%83%BC%E3%81%95%E3%82%8C%E3%81%AA%E3%81%84%E4%B8%8D%E5%85%B7%E5%90%88%E3%81%AE%E5%A0%B4%E5%90%88)
- [ざっくりとした流れ](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E3%81%96%E3%81%A3%E3%81%8F%E3%82%8A%E3%81%A8%E3%81%97%E3%81%9F%E6%B5%81%E3%82%8C-7)
- [問題の発生に関わる値を特定する](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E5%95%8F%E9%A1%8C%E3%81%AE%E7%99%BA%E7%94%9F%E3%81%AB%E9%96%A2%E3%82%8F%E3%82%8B%E5%80%A4%E3%82%92%E7%89%B9%E5%AE%9A%E3%81%99%E3%82%8B)
- [ざっくりとした流れ](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E3%81%96%E3%81%A3%E3%81%8F%E3%82%8A%E3%81%A8%E3%81%97%E3%81%9F%E6%B5%81%E3%82%8C-8)
- [問題の値を処理している箇所を特定する](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E5%95%8F%E9%A1%8C%E3%81%AE%E5%80%A4%E3%82%92%E5%87%A6%E7%90%86%E3%81%97%E3%81%A6%E3%81%84%E3%82%8B%E7%AE%87%E6%89%80%E3%82%92%E7%89%B9%E5%AE%9A%E3%81%99%E3%82%8B)
- [ざっくりとした流れ](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E3%81%96%E3%81%A3%E3%81%8F%E3%82%8A%E3%81%A8%E3%81%97%E3%81%9F%E6%B5%81%E3%82%8C-9)
- [問題の値が生成される直接原因を特定する](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E5%95%8F%E9%A1%8C%E3%81%AE%E5%80%A4%E3%81%8C%E7%94%9F%E6%88%90%E3%81%95%E3%82%8C%E3%82%8B%E7%9B%B4%E6%8E%A5%E5%8E%9F%E5%9B%A0%E3%82%92%E7%89%B9%E5%AE%9A%E3%81%99%E3%82%8B)
- [ざっくりとした流れ](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E3%81%96%E3%81%A3%E3%81%8F%E3%82%8A%E3%81%A8%E3%81%97%E3%81%9F%E6%B5%81%E3%82%8C-10)
- [問題の値が生成される根本原因を特定する](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E5%95%8F%E9%A1%8C%E3%81%AE%E5%80%A4%E3%81%8C%E7%94%9F%E6%88%90%E3%81%95%E3%82%8C%E3%82%8B%E6%A0%B9%E6%9C%AC%E5%8E%9F%E5%9B%A0%E3%82%92%E7%89%B9%E5%AE%9A%E3%81%99%E3%82%8B)
- [例外がスローされない不具合の場合・まとめ](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E4%BE%8B%E5%A4%96%E3%81%8C%E3%82%B9%E3%83%AD%E3%83%BC%E3%81%95%E3%82%8C%E3%81%AA%E3%81%84%E4%B8%8D%E5%85%B7%E5%90%88%E3%81%AE%E5%A0%B4%E5%90%88%E3%81%BE%E3%81%A8%E3%82%81)
- [ざっくりとした流れ](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E3%81%96%E3%81%A3%E3%81%8F%E3%82%8A%E3%81%A8%E3%81%97%E3%81%9F%E6%B5%81%E3%82%8C-11)
- [対策を講じる・不具合が解消していることを確認する](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E5%AF%BE%E7%AD%96%E3%82%92%E8%AC%9B%E3%81%98%E3%82%8B%E4%B8%8D%E5%85%B7%E5%90%88%E3%81%8C%E8%A7%A3%E6%B6%88%E3%81%97%E3%81%A6%E3%81%84%E3%82%8B%E3%81%93%E3%81%A8%E3%82%92%E7%A2%BA%E8%AA%8D%E3%81%99%E3%82%8B)
- [失敗例](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E5%A4%B1%E6%95%97%E4%BE%8B)
- [思い込みは最大の敵](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E6%80%9D%E3%81%84%E8%BE%BC%E3%81%BF%E3%81%AF%E6%9C%80%E5%A4%A7%E3%81%AE%E6%95%B5)
- [まとめ](https://qiita.com/opengl-8080/items/56d31fe80b45773dc808?utm_source=Qiita+%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=4d32e5d259-Qiita_newsletter_643_11_06_2024&utm_medium=email&utm_term=0_e44feaa081-4d32e5d259-33537417/#%E3%81%BE%E3%81%A8%E3%82%81)

## 先輩社員がどうやって不具合を解決しているのか

- [Java](https://qiita.com/tags/java)
- [debug](https://qiita.com/tags/debug)

最終更新日 2024年10月27日投稿日 2024年10月27日

## 先輩社員がどうやって不具合を解決しているのか

## 自己紹介

[![](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.amazonaws.com%2F0%2F28302%2F63d28421-104b-3066-2712-768e6aded5f7.jpeg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=14b9df4cdc735b8cab9b2adf1471ce8e)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.amazonaws.com%2F0%2F28302%2F63d28421-104b-3066-2712-768e6aded5f7.jpeg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=14b9df4cdc735b8cab9b2adf1471ce8e)

- opengl-8080
- たまに Qiita で技術メモを書いたり
- 関西在住・SIer 勤務

---

## はじめに

- システム開発をしていると、いろいろな場面で不具合と遭遇する
- 当然、不具合は解決しなければならない
- 下に若手がついて一緒に開発をすることがあるが、不具合の解決方法が分からないと相談を受けることがよくある
- 経験が浅いと、不具合調査のために何から着手すればいいか分からない
- ある程度パターン化された手順を踏むことで、多くの不具合は解決できるという経験的な認識がある
- 私がどういう手順で、何を考えながら不具合の解決を行っているかを整理・説明することで、若手の成長に繋がれば幸い

[![](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2Fc0947066-73e2-d88a-7489-daac25a0230d.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=abe767efa7f7e23726c71da3a4ce589c)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2Fc0947066-73e2-d88a-7489-daac25a0230d.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=abe767efa7f7e23726c71da3a4ce589c)

---

## 話すこと・対象者・前提

- Java でシステム開発をしていて不具合に遭遇したときにどうやって解決するか
- 基本的な手順や考え方
- デバッグに役立つ知識（スタックトレースの読み方やデバッガの使い方）
- 不具合解決で気を付けること
- 1, 2年目くらいの若手が対象
- 不具合対応となると何からすればいいか分からない
- スタックトレースの読み方が分からない
- デバッガを使ってない（使えない）
- Java の Web アプリ（サーバー側）で不具合が起こった場合を例として説明
- フロントエンドやDB・ビルドツールでの不具合は対象外
- ただし、考え方とかは技術要素や範囲が異なっても適用できる（はず）

---

## ざっくりとした流れ

- **何が起こっているかを正確に把握する**
- 不具合を再現させる
- 例外がスローされる不具合の場合
- 例外の発生箇所を特定する
- 例外の直接原因を特定する
- 例外の根本原因を特定する
- 例外がスローされない不具合の場合
- 問題の発生に関わる値を特定する
- 問題の値を処理している箇所を特定する
- 問題の値が生成される直接原因を特定する
- 問題の値が生成される根本原因を特定する
- 対策を講じる
- 不具合が解消していることを確認する

---

## 何が起こっているかを正確に把握する

- 誰が、いつ、どういう条件で、どういう操作をしたら、何が起こったのか、問題（期待する結果との差）は何か
- 例
- お客様が、昨日の夕方、○○という条件で、××の検索を行ったら、検索結果が０件になった、本当なら１件出力されるはず
- 後輩が、さっき、ローカルで動かしている開発中のシステムで、Webアプリを起動したら、エラーが起こってアプリが起動しなかった、本当ならアプリが起動して欲しい

[![](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F99b65c97-f7c0-9dda-7c1e-15280c7e446f.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=af6cf6cf7188cc4b9e344b4978e1f715)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F99b65c97-f7c0-9dda-7c1e-15280c7e446f.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=af6cf6cf7188cc4b9e344b4978e1f715)

---

## 「正確に」把握することの重要さ

- 見切り発車で調査を開始すると、関係ないことを調べたりして時間を無駄にすることがある
- 例
- 「エラーになった」と言われたので例外がスローされているのかなとログを見に行ったが何も出力されてなかった（実際には入力値不正でエラーメッセージが出力されていた）
- 「アプリを起動したらエラーになった」と言われてログを見に行ったが何も出力されてなかった（実際にはコンパイルの時点でエラーになっており、起動すらしていなかった）
- 「アプリが動かない」と言われて色々しらべてみたが問題が再現せず。実は今ではなくメンテでDBを停止していた時間帯の話だった

[![](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2Fd8bf6bb7-bd92-943f-4549-00c9ddf05b21.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=86a66b07d7b397890273914932b39b5a)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2Fd8bf6bb7-bd92-943f-4549-00c9ddf05b21.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=86a66b07d7b397890273914932b39b5a)

---

## ざっくりとした流れ

- 何が起こっているかを正確に把握する
- **不具合を再現させる**
- 例外がスローされる不具合の場合
- 例外の発生箇所を特定する
- 例外の直接原因を特定する
- 例外の根本原因を特定する
- 例外がスローされない不具合の場合
- 問題の発生に関わる値を特定する
- 問題の値を処理している箇所を特定する
- 問題の値が生成される直接原因を特定する
- 問題の値が生成される根本原因を特定する
- 対策を講じる
- 不具合が解消していることを確認する

---

## 不具合を再現させる

- 不具合の条件を正確に把握するため
- 不具合が起こる条件・起こらない条件を把握することで、原因が特定しやすくなる
- 原因調査をしやすくするため
- 再現できる = 何度でも試せる
- 何度も試して、様々な情報を収集できる
- 修正後に動作確認するため
- 修正後に不具合が解消していることを確実に検証できる

[![](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2Fc34cc1f2-dc0c-24af-0874-5d281b9f98e5.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=74204540eb280f3ca2a3ce9abe2c501b)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2Fc34cc1f2-dc0c-24af-0874-5d281b9f98e5.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=74204540eb280f3ca2a3ce9abe2c501b)

---

## できればローカルで再現させる

- ローカルであれば他の開発メンバーに影響しないので調査がしやすい
- デバッガで1ステップずつ動きを確認できる
- 様々な条件で何度も試せる

---

## 再現させられない場合

- 不具合が起こったときの状況をもう一度詳しく聞く
- どういう操作をしたのか
- どういう入力をしたのか
- 全く同じ条件で再現を試みているか？
- 不具合が起こる環境と起こらない環境はないか？
- もしある場合、２つの環境や操作内容に差はないか？
- 固定観念を捨てて、隅々まで条件が同じかチェックする
- 「当然同じだろう」と思っているところが案外違ったりする
- 例
- 同じバージョンのソースを使っているか？
- DBの中は同じ状態か？
- 入力値は一字一句全く同じか？
- etc...

[![](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F6b9ceaea-7858-b1ac-7521-20fb5cd7d75b.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=7b5be125908ea46d6d0b602261a9dd5c)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F6b9ceaea-7858-b1ac-7521-20fb5cd7d75b.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=7b5be125908ea46d6d0b602261a9dd5c)

---

## ざっくりとした流れ

- 何が起こっているかを正確に把握する
- 不具合を再現させる
- **例外がスローされる不具合の場合**
- 例外の発生箇所を特定する
- 例外の直接原因を特定する
- 例外の根本原因を特定する
- 例外がスローされない不具合の場合
- 問題の発生に関わる値を特定する
- 問題の値を処理している箇所を特定する
- 問題の値が生成される直接原因を特定する
- 問題の値が生成される根本原因を特定する
- 対策を講じる
- 不具合が解消していることを確認する

---

## 例外がスローされる不具合の場合

- Java の Web アプリで発生する不具合は大きく以下の２つに分けられる（気がする）
- 例外がスローされる不具合
- 例外がスローされない不具合
- 例外 = `java.lang.Exception` およびそのサブクラス
- 例外がスローされる不具合
- 非業務エラー
- システムが想定してないエラー
- 「障害が発生しました」「システム管理者に問い合わせてください」といったメッセージを出すような状態
- 例：ぬるぽ・DB通信エラーなど

[![](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F6b16544a-59f0-f806-e20b-c5340e6853b5.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=d7fa8865dda39b819b72332ee5899614)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F6b16544a-59f0-f806-e20b-c5340e6853b5.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=d7fa8865dda39b819b72332ee5899614)

---

## ざっくりとした流れ

- 何が起こっているかを正確に把握する
- 不具合を再現させる
- 例外がスローされる不具合の場合
- **例外の発生箇所を特定する**
- 例外の直接原因を特定する
- 例外の根本原因を特定する
- 例外がスローされない不具合の場合
- 問題の発生に関わる値を特定する
- 問題の値を処理している箇所を特定する
- 問題の値が生成される直接原因を特定する
- 問題の値が生成される根本原因を特定する
- 対策を講じる
- 不具合が解消していることを確認する

---

## 例外の発生箇所を特定する

- まずは例外がスローされた箇所（ソースコード上の場所）を特定する
- 普通はログに例外の**スタックトレース**が出力されている

スタックトレースの例

```
java.lang.RuntimeException: test
	at sandbox.debug.Fuga.fugaMethod(Fuga.java:6)
	at sandbox.debug.Hoge.hogeMethod(Hoge.java:7)
	at sandbox.debug.Main.main(Main.java:7)
```

---

## スタックトレース

[![jjugccc2024.jpg](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2Ff3c62e18-74ad-0773-7941-68cf52995139.jpeg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=e90027bb59e0f2ded5a8f4e39475d20f)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2Ff3c62e18-74ad-0773-7941-68cf52995139.jpeg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=e90027bb59e0f2ded5a8f4e39475d20f)

スタックトレース

```
java.lang.RuntimeException: test
	at sandbox.debug.Fuga.fugaMethod(Fuga.java:6)      (3)
	at sandbox.debug.Hoge.hogeMethod(Hoge.java:7)      (2)
	at sandbox.debug.Main.main(Main.java:7)            (1)
```

- Java はスレッドごとにメソッドの呼び出しをスタックで管理している
- スタック = LIFOのデータ構造
- 例外を `new` すると、その時点のスタックの情報が例外に記録される
- スタックトレースは、このスタックの情報を出力したもの
- トレース = trace = 追跡
- スタックを追跡するためのもの
- スタックトレースを読むと、その例外を投げたスレッドがどのようにプログラムを通り、どこで例外をスローしたかが分かる

---

## スタックトレースの読み方

[![jjugccc2024.jpg](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2Fae3e03fa-87dd-0883-6c3d-8b57271ff778.jpeg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=05c06e6e66eebe09a854194a3c7585f0)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2Fae3e03fa-87dd-0883-6c3d-8b57271ff778.jpeg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=05c06e6e66eebe09a854194a3c7585f0)

- 初めて長大なスタックトレースを見るとビックリしてしまうかもしれないが、全部を読む必要は無い
- 「例外の発生箇所を特定する」という目的に対しては、一番重要なのはスタックトレースの先頭だけ
- スタックトレースの先頭行は、その例外が生成された場所
- 普通は `throw new Exceptin()` のように、生成と同時に例外をスローするので、例外が生成された場所＝例外がスローされた場所、になる

---

## スタックトレースの読み方２（Caused by）

[![jjugccc2024.jpg](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F96271b65-e282-4600-1fe9-04b3edade6b3.jpeg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=f2e9d3ad3ff8e004e414fd4ba9e84636)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F96271b65-e282-4600-1fe9-04b3edade6b3.jpeg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=f2e9d3ad3ff8e004e414fd4ba9e84636)

- 例外には **原因(cause)** を設定できる
- その例外がスローされる原因となった別の例外
- コンストラクタで指定できる
- 原因が設定されている場合、スタックトレースには `Caused by` と書かれたものが追加される
- 原因のスタックトレースが別途出力される
- 原因は何重にも入れ子になっている可能性がある
- その場合、大本の原因にたどり着くまで再帰的に `Caused by` が出力される
- つまり、「例外の発生箇所を特定する」ためには、**一番最後に出力された `Caused by` の先頭の行**を見ればいい

---

## スタックトレースの読み方・まとめ

「例外の発生箇所を特定する」ためには、

- Caused by がない場合
- スタックトレースの先頭を見る

[![jjugccc2024.jpg](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F8511d6d2-ea6a-c9ab-9172-446f8386e755.jpeg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=09d73aa0a199a5c7080fcb219ccf0987)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F8511d6d2-ea6a-c9ab-9172-446f8386e755.jpeg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=09d73aa0a199a5c7080fcb219ccf0987)

- Caused by がある場合
- 最後の Caused by ブロックのスタックトレースの先頭を見る

[![jjugccc2024.jpg](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2Fee4a9b03-e06a-2d50-0d37-87600d08469c.jpeg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=fde67d4ec2d91920825d97762432c272)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2Fee4a9b03-e06a-2d50-0d37-87600d08469c.jpeg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=fde67d4ec2d91920825d97762432c272)

---

## ざっくりとした流れ

- 何が起こっているかを正確に把握する
- 不具合を再現させる
- 例外がスローされる不具合の場合
- 例外の発生箇所を特定する
- **例外の直接原因を特定する**
- 例外の根本原因を特定する
- 例外がスローされない不具合の場合
- 問題の発生に関わる値を特定する
- 問題の値を処理している箇所を特定する
- 問題の値が生成される直接原因を特定する
- 問題の値が生成される根本原因を特定する
- 対策を講じる
- 不具合が解消していることを確認する

---

## 例外の直接原因を特定する

- 例外がスローされた直接原因は、例外の型やメッセージからある程度推測できる
- 例外の型から推測
- `NullPointerException`: null参照が起こった
- 例外の型とメッセージから推測
- 例外が `SocketException` でメッセージが `Socket is closed`: 切断されたソケットで通信しようとした
- 例外が `SQLException` でメッセージが `ERROR: syntax error at or near "\".`: SQL に文法違反がある
- いずれもスタックトレースに出力されている情報なので、スタックトレースをしっかり読むこと
- 英語でも怯えない
- 分からなければググるか機械翻訳にかければいい

[![jjugccc2024.jpg](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F5cb708c0-5cca-c10a-2793-ee393f297288.jpeg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=0c7772f51ff50210e241b984b9af4e94)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F5cb708c0-5cca-c10a-2793-ee393f297288.jpeg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=0c7772f51ff50210e241b984b9af4e94)

- ただし、例外の型やメッセージだけでは直接原因が分からないこともよくある

---

## 例外の発生箇所を確かめる

```
int length = obtainString().length();
```

- 発生した原因の例外が `NullPointerException` で、発生箇所を見ると上記のような実装になっていたとする
- この場合、 `obtainString` の戻り値が `null` だったことが直接原因になる

[![](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F8e4ec841-543a-b3b8-2e87-759b9095ecfd.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=c6f25fe5c8880ba4ef04020961bb85f0)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F8e4ec841-543a-b3b8-2e87-759b9095ecfd.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=c6f25fe5c8880ba4ef04020961bb85f0)

---

## 直接原因で止まってはいけない

```
String string = obtainString();
int length = string == null ? 0 : string.length();
```

- 原因究明を直接原因の特定で終わってしまうと、上記のような修正で満足してしまう恐れがある
- 確かに `NullPointerException` は発生しなくなるが、そもそも `obtainString` が `null` を返すこと自体がおかしい場合、根本原因は解決していないことになる
- 他に `obtainString` を使っている場所で同じ問題が起こるかもしれない

[![](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F562f8d1d-3f35-c55e-2900-283803af5671.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=946cf2599cdcb706e64168c5e078c04c)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F562f8d1d-3f35-c55e-2900-283803af5671.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=946cf2599cdcb706e64168c5e078c04c)

---

## ざっくりとした流れ

- 何が起こっているかを正確に把握する
- 不具合を再現させる
- 例外がスローされる不具合の場合
- 例外の発生箇所を特定する
- 例外の直接原因を特定する
- **例外の根本原因を特定する**
- 例外がスローされない不具合の場合
- 問題の発生に関わる値を特定する
- 問題の値を処理している箇所を特定する
- 問題の値が生成される直接原因を特定する
- 問題の値が生成される根本原因を特定する
- 対策を講じる
- 不具合が解消していることを確認する

---

## 例外の根本原因を特定する

- 発生した例外の直接原因がそのまま根本原因となることもあれば、そうでないこともある
- 根本原因でなかった場合、間違った対策を講じるおそれがある
- 必ず、特定した直接原因とは別に根本原因が無いか検討する必要がある
- 例
- 設定値を参照しているところで `NullPointerException` が発生したが、そもそも設定値が `null` になること自体がおかしい
- システムの設定に不備があることが根本原因だった
- SQL のシンタックスエラーが出ているが、そもそもSQLは自動生成しているはずなのでシンタックスエラーになるのは不自然
- SQLの自動生成ツールの設定不備が根本原因だった
- HTTPの通信エラーになっているが、そもそもこの機能ではHTTP通信は必要ないはず
- 実装が設計書通りになっていないのが根本原因だった

[![](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F2daec02f-a209-1b11-7cdb-b9ca6c154596.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=f767a0a3998ef7c3aa5caa651344c3d6)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F2daec02f-a209-1b11-7cdb-b9ca6c154596.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=f767a0a3998ef7c3aa5caa651344c3d6)

---

## 根本原因を特定する方法

- 正直難しい
- 場合によっては使っているフレームワークやミドルウェア、通信プロトコルなど様々な知識が必要となる
- 知識に関しては地道に経験を積んで、学んでいくしかないかと
- 使えるツール
- デバッガ
- 処理をステップ実行して変数の状態を確認できるので、原因究明がしやすい
- その他の方法
- 机上デバッグ
- 大変・ミスしがち
- デバッグログを差し込む
- 面倒・時間がかかる
- デバッガを使うのが一番の近道

[![](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F77fe38a5-dcaf-4ccc-7c6d-822c945fa660.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=3dc763112ed3b17f93cc029c6d0e6748)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F77fe38a5-dcaf-4ccc-7c6d-822c945fa660.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=3dc763112ed3b17f93cc029c6d0e6748)

---

## デバッガの仕組み

[![gomi.jpg](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F1a380d45-a596-bcd2-794a-7913a330cd51.jpeg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=9247ee9cee1ef44ff80c461a9989c0fa)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F1a380d45-a596-bcd2-794a-7913a330cd51.jpeg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=9247ee9cee1ef44ff80c461a9989c0fa)

- JVM をデバッグ接続可能な状態で起動しておく
- 接続先の JVM を指定してデバッガ(IntelliJ とか Eclipse などが提供)を起動する
- 通信は、基本的には TCP で行われる（共有メモリとかもあるらしいが割愛）
- TCP 通信ができるのであればリモートマシン上で動いているJVMでも接続可能

---

## デバッグ接続可能な状態でJVMを起動する

```
java -agentlib:jdwp=transport=dt_socket,server=y,address=8000,suspend=y ...
```

- `-agentlib:jdwp` オプションを付けることでデバッグ接続が可能になる
- 検索すると `-Xdebug` および `-Xrunjdwp` を使った方法が出てくるが、これらは J2SE 5.0 より前の古い方法になる
- 各オプションの意味は以下の通り
- `transport`
- 接続の方法
- `dt_socket` ならソケット通信(TCP)
- `server`
- `y`: デバッガからの接続受け付ける
- `n`: デバッガに接続しにいく
- `address`
- `server=y` なら、接続を待ち受けるアドレス
- 上の例(`address=8000`)はポート番号だけを指定している
- `server=n` なら、接続先のデバッガのアドレス
- `suspend`
- デバッガとの接続が完了するまで JVM を一時停止するなら `y`

---

## IDE でデバッガを起動する

- IDE から直接アプリケーションを起動できる場合
- デバッグ起動を利用する

**IntelliJ**

[![jjugccc2024.jpg](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2Fc15640a3-a75c-737a-ef0c-5475569d4566.jpeg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=63982daf7487dabc0158397b04483631)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2Fc15640a3-a75c-737a-ef0c-5475569d4566.jpeg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=63982daf7487dabc0158397b04483631)

**Eclipse**

[![jjugccc2024.jpg](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F5ad26632-d819-8cff-3f44-7c7386d1f79d.jpeg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=7a98d0d9be6ea52b2301d8da2c3f4bae)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F5ad26632-d819-8cff-3f44-7c7386d1f79d.jpeg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=7a98d0d9be6ea52b2301d8da2c3f4bae)

- IDE から直接アプリケーションを起動できない場合
- リモートデバッグを利用する
- Maven とかもデバッグできる

**IntelliJ**

[![jjugccc2024.jpg](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F3597b18e-2a57-787d-103d-068cc57dbaad.jpeg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=5e4b249614cad5ce3faaaa16beb96fdc)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F3597b18e-2a57-787d-103d-068cc57dbaad.jpeg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=5e4b249614cad5ce3faaaa16beb96fdc)

**Eclipse**

[![jjugccc2024.jpg](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F8fae4bbf-e546-6e71-deb0-043798b9bb45.jpeg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=d9c25d208482a544f7d00c92e907ddf8)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F8fae4bbf-e546-6e71-deb0-043798b9bb45.jpeg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=d9c25d208482a544f7d00c92e907ddf8)

---

## デバッガの使い方

- IntelliJ の場合で説明するが、Eclipse もだいたい同じ機能を提供している

### ブレークポイントを設定する

[![image.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2Fd7f48d34-148d-1289-857d-7bd75f080f2c.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=bcba69e392f33349020ba850ff7e96a7)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2Fd7f48d34-148d-1289-857d-7bd75f080f2c.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=bcba69e392f33349020ba850ff7e96a7)

- 行番号のところをクリックすると**ブレークポイント**を設定できる
- もう一回クリックしたらブレークポイントを削除できる
- プログラムの処理がブレークポイントに達すると、そこで処理が一時停止する
- 気になる処理の手前などにブレークポイントを設定しておいて、続くステップ実行を利用してプログラムの挙動を確認する

### デバッガの見方

[![jjugccc2024.jpg](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F36ab50b6-754f-59a3-2528-742dddbfb3ac.jpeg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=7359c8b5239b1fbeb5c3e468f846a590)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F36ab50b6-754f-59a3-2528-742dddbfb3ac.jpeg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=7359c8b5239b1fbeb5c3e468f846a590)

### 操作方法

[![jjugccc2024.jpg](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2Fb8218c78-731c-2a1f-a33c-c0bdba5b5f1c.jpeg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=5065236b3d8a096a257bc35e9182cc60)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2Fb8218c78-731c-2a1f-a33c-c0bdba5b5f1c.jpeg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=5065236b3d8a096a257bc35e9182cc60)

- ステップオーバー
- 処理を次の行に進める
- 1行ずつ処理を進めていきたいときに使う
- ステップイン
- 現在の行から呼び出されるメソッドの中に入る
- 呼び出し先のメソッドの中まで処理を追いたいときに使う
- ステップアウト
- スタックを１つ戻る（処理は進む）
- 現在のメソッドの処理を終わらせて呼び出し元へ戻りたいときに使う
- 再開(F9)・ステップオーバー(F8)・ステップイン(F7)はよく使うので、ショートカットを覚えておくと捗る

### 変数の値を管理する

[![image.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2Fbda79c02-4bfe-7501-44f5-135cd3b7dec1.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=15d44508b99848f361bb0999beafd6c9)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2Fbda79c02-4bfe-7501-44f5-135cd3b7dec1.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=15d44508b99848f361bb0999beafd6c9)

- デバッガに表示されている変数を右クリックすると、メニューが開く
- 変数の中身の値をコピーしたり、変数の中身の値を任意に書き換えたりできる
- デバッグ目的ではあまり書き換えは使わないが、無理やり `null` を代入して例外を発生させて挙動を見る、みたいなことができる

### 任意の式を実行する

[![image.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2Ffce3a404-0b82-d315-35f1-e474ede2b888.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=827c78a5df4c09ff7d8fb312f6e26b18)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2Ffce3a404-0b82-d315-35f1-e474ede2b888.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=827c78a5df4c09ff7d8fb312f6e26b18)

- デバッガの変数を表示しているところを右クリックしてメニューを開き、 \[Evaluate Expression\] を選択する

[![image.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2Fb193ce32-bdeb-3030-f63a-9f85aeb3e4bd.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=7856fd8cfe26086e5e1ddcae909bd670)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2Fb193ce32-bdeb-3030-f63a-9f85aeb3e4bd.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=7856fd8cfe26086e5e1ddcae909bd670)

- 現在のスコープから参照できる変数を利用して任意の式を実行できる

### 条件付きブレークポイント

[![image.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F91bca52b-095b-37b8-7085-fbe6f378fb23.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=08a9bf874d2846e2139eebe07ae988ad)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F91bca52b-095b-37b8-7085-fbe6f378fb23.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=08a9bf874d2846e2139eebe07ae988ad)

- ブレークポイントを右クリックすると、 \[Condition\] で一時停止する条件を指定できる
- デフォルトでは処理がブレークポイントに到達すると無条件に一時停止する
- しかし、それだとループ中の特定の条件のときだけ一時停止したい、といった場合に非常に不便
- 条件を入れることで、例外が起こるであろう条件が満たされたときだけ処理を一時停止させるようなことができる

### 例外がスローされたら一時停止する

[![jjugccc2024.jpg](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F58ec1f97-b115-b832-79b2-66676c77db45.jpeg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=5219dc9d0a67bb53938bf99e18422a77)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F58ec1f97-b115-b832-79b2-66676c77db45.jpeg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=5219dc9d0a67bb53938bf99e18422a77)

- デバッガメニューのブレークポイントの管理(View Breakpoints)を選択し、管理用のダイアログを開く
- 左上の \[+\] から \[Java Exception Breakpoints\] を選択する

[![image.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F89ca458b-d785-aa87-102b-210c072b8cdb.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=667cfd83088eef856d8024eef01fb84c)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F89ca458b-d785-aa87-102b-210c072b8cdb.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=667cfd83088eef856d8024eef01fb84c)

- スローされたら一時停止させたい例外を選択する

[![image.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F9c40122e-ceaa-fb97-10cf-7d6a6e63db54.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=3b46b4965e92de4ae61719f61d51d7ff)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F9c40122e-ceaa-fb97-10cf-7d6a6e63db54.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=3b46b4965e92de4ae61719f61d51d7ff)

- 以上の設定で、 `NullPointerException` がスローされたら、そのタイミング（スローしている行）で処理が一時停止するようになる
- デフォルトで存在している \[Any Exception\] のチェックをオンにすると、任意の例外がスローされた場合でも一時停止が可能になる
- 例外が握りつぶされるなどしてスタックトレースが確認できない、みたいな悲しいケースで利用できる

### フィールドの値が変更されたら一時停止する

[![image.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F6c385581-a3e5-aaf3-00f5-6864e6c09431.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=264b3ea412725fd3d202b3a293ef36aa)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F6c385581-a3e5-aaf3-00f5-6864e6c09431.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=264b3ea412725fd3d202b3a293ef36aa)

- フィールド宣言の行番号部分をクリックすると、目のアイコンのブレークポイントが作成される
- デフォルトでは、フィールドに値が代入されたら処理が一時停止する
- 目のアイコンを右クリックしてメニューを表示し \[Watch\] > \[Field access\] を選択すると、フィールドにアクセスされたら処理を一時停止させられるようもできる

[![jjugccc2024.jpg](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2Fda76dea2-4c78-36fb-5251-0e44c143ccd6.jpeg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=bb1f44d37f4ea442b394778917b8a1c4)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2Fda76dea2-4c78-36fb-5251-0e44c143ccd6.jpeg?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=bb1f44d37f4ea442b394778917b8a1c4)

### その他にも便利そうな機能が色々

[![image.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2Fbda430d0-b035-92a7-2df9-dbe754ab4c1b.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=55859cf4e6456050c1c30be3ad87ef5a)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2Fbda430d0-b035-92a7-2df9-dbe754ab4c1b.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=55859cf4e6456050c1c30be3ad87ef5a)

- Run to Cursor
- カーソル位置までステップを進める
- Reset Frame
- フレーム（スタックの位置）を1つ前に戻す（処理をやり直せる）
- Throw Exception
- 任意の例外をスローする

---

## 例外がスローされる不具合の場合 まとめ

- 例外がスローされる不具合の場合は、まずは例外の発生箇所を特定する
- 例外の発生箇所はスタックトレースを見ればわかる
- 例外やメッセージ、発生箇所の情報から例外の直接原因を特定する
- 直接原因だけでなく、根本原因が無いか注意深く調査する
- 調査にはデバッガを使うのが近道

---

## ざっくりとした流れ

- 何が起こっているかを正確に把握する
- 不具合を再現させる
- 例外がスローされる不具合の場合
- 例外の発生箇所を特定する
- 例外の直接原因を特定する
- 例外の根本原因を特定する
- **例外がスローされない不具合の場合**
- 問題の発生に関わる値を特定する
- 問題の値を処理している箇所を特定する
- 問題の値が生成される直接原因を特定する
- 問題の値が生成される根本原因を特定する
- 対策を講じる
- 不具合が解消していることを確認する

---

## 例外がスローされない不具合の場合

- 例外はスローされないが、システムが期待した動きをしていない状態
- 例
- 計算結果・検索結果が期待値と異なる
- 正しい値を入力しているはずなのに入力エラー扱いになる
- 表示されるべき画面項目が空になっている
- いつまで待っても画面が表示されない
- etc...
- 原因究明のアプローチが、例外がスローされる場合と異なる

[![](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2Fa1cc11f9-759b-1275-4f8d-ec2ae455b7cf.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=f55db87f72fa9d9bee60a0c234b7f0a3)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2Fa1cc11f9-759b-1275-4f8d-ec2ae455b7cf.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=f55db87f72fa9d9bee60a0c234b7f0a3)

---

## ざっくりとした流れ

- 何が起こっているかを正確に把握する
- 不具合を再現させる
- 例外がスローされる不具合の場合
- 例外の発生箇所を特定する
- 例外の直接原因を特定する
- 例外の根本原因を特定する
- 例外がスローされない不具合の場合
- **問題の発生に関わる値を特定する**
- 問題の値を処理している箇所を特定する
- 問題の値が生成される直接原因を特定する
- 問題の値が生成される根本原因を特定する
- 対策を講じる
- 不具合が解消していることを確認する

---

## 問題の発生に関わる値を特定する

- 問題の発生に関わる何かしらの**値**が存在するはずなので、それを特定する
- 例
- 計算結果・検索結果が期待値と異なる
- 計算結果、検索結果
- 正しい値を入力しているはずなのに入力エラー扱いになる
- エラーとなった入力値
- 表示されるべき画面項目が空になっている
- 画面項目の値
- いつまで待っても画面が表示されない
- レスポンス

[![](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2Ff8a6fcb7-cfe2-ca1d-2846-56455c43bbd3.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=c0e64bbb3f1b847b45ed4016296d6473)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2Ff8a6fcb7-cfe2-ca1d-2846-56455c43bbd3.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=c0e64bbb3f1b847b45ed4016296d6473)

---

## ざっくりとした流れ

- 何が起こっているかを正確に把握する
- 不具合を再現させる
- 例外がスローされる不具合の場合
- 例外の発生箇所を特定する
- 例外の直接原因を特定する
- 例外の根本原因を特定する
- 例外がスローされない不具合の場合
- 問題の発生に関わる値を特定する
- **問題の値を処理している箇所を特定する**
- 問題の値が生成される直接原因を特定する
- 問題の値が生成される根本原因を特定する
- 対策を講じる
- 不具合が解消していることを確認する

---

## 問題の値を処理している箇所を特定する

- 問題の値を処理している箇所があるはずなので、その場所を特定する
- 入口または出口から辿って行って、問題の値を処理しているところを見つけ出す
- 入口
- リクエストを受け付ける場所
- 出口
- レスポンスを返す場所
- Spring MVC でいうとコントローラのメソッド
- 例
- 検索結果があるはずなのに無い
- レスポンスに書き出された検索結果の値が問題なので出口の方から辿る
- レスポンスを返しているところで検索結果が期待通り設定されているか確認する
- →設定されていない
- なぜ設定されていないのかを確かめるため、検索結果を設定している箇所を実装をさかのぼって見つけ出す
- デバッガを使って、問題の値がどのタイミングで変な状態になったのかを特定する
- 机上デバッグだと勘違いする恐れがあるので、デバッガを使って確実に調査する

```
@GetMapping("/hello")
public String hello(Model model, @RequestParam String condition) {
    List<Result> result = service.search(condition);
    model.addAttribute("result", result);
    return "hello";
}
```

---

## ざっくりとした流れ

- 何が起こっているかを正確に把握する
- 不具合を再現させる
- 例外がスローされる不具合の場合
- 例外の発生箇所を特定する
- 例外の直接原因を特定する
- 例外の根本原因を特定する
- 例外がスローされない不具合の場合
- 問題の発生に関わる値を特定する
- 問題の値を処理している箇所を特定する
- **問題の値が生成される直接原因を特定する**
- 問題の値が生成される根本原因を特定する
- 対策を講じる
- 不具合が解消していることを確認する

---

## 問題の値が生成される直接原因を特定する

- 問題の値が設定されている箇所が特定できたら、なぜ変な値が設定されてしまったのか直接原因を特定する
- 例
- 問題 → 検索結果が空
- 直接原因 → DBアクセスの結果が空だったため

```
public List<Result> search(String condition) {
    // 入力値チェックとか...

    // DB検索
    List<HoegEntity> list = dao.find(condition);

    // 変換して返却
    return convert(list);
}
```

---

## ざっくりとした流れ

- 何が起こっているかを正確に把握する
- 不具合を再現させる
- 例外がスローされる不具合の場合
- 例外の発生箇所を特定する
- 例外の直接原因を特定する
- 例外の根本原因を特定する
- 例外がスローされない不具合の場合
- 問題の発生に関わる値を特定する
- 問題の値を処理している箇所を特定する
- 問題の値が生成される直接原因を特定する
- **問題の値が生成される根本原因を特定する**
- 対策を講じる
- 不具合が解消していることを確認する

---

## 問題の値が生成される根本原因を特定する

- 例外がスローされる不具合の場合と同様に、問題の直接原因が分かったら次は根本原因が無いか調査する
- 例
- 問題 → 検索結果が空
- 直接原因 → DBアクセスの結果が空だったため
- 根本原因 → 検索条件のパラメータがサーバーに渡せていなかった
- こちらも、原因究明にはデバッガの利用が効率的

---

## 例外がスローされない不具合の場合・まとめ

- 発生している不具合に直接関係している**値**を特定する
- その値が生成されている箇所を特定する
- システムの入口・出口から辿っていく
- デバッガを使って確実に調べるのが良い
- 問題の値が、なぜ期待していない値になっているのかの直接原因を特定する
- 根本原因を特定する

---

## ざっくりとした流れ

- 何が起こっているかを正確に把握する
- 不具合を再現させる
- 例外がスローされる不具合の場合
- 例外の発生箇所を特定する
- 例外の直接原因を特定する
- 例外の根本原因を特定する
- 例外がスローされない不具合の場合
- 問題の発生に関わる値を特定する
- 問題の値を処理している箇所を特定する
- 問題の値が生成される直接原因を特定する
- 問題の値が生成される根本原因を特定する
- **対策を講じる**
- **不具合が解消していることを確認する**

---

## 対策を講じる・不具合が解消していることを確認する

- 根本原因が特定できたら、どう対処するかを検討する
- 検討内容を適用してみて、不具合が解消していることを確認する
- このとき、不具合の再現ができていると確認を確実に実施できる

[![](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F4022bfee-3211-17b6-043b-2a0640461593.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=a9a0bb67bb29005ce916026d08377f61)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F4022bfee-3211-17b6-043b-2a0640461593.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=a9a0bb67bb29005ce916026d08377f61)

---

## 失敗例

- 報告された不具合内容から原因を推測して調査を開始
- 関係ないところを調べて時間を浪費
- 根本原因を推測するも、確証を得ずに対策を検討
- 推測内容に誤りがあり、時間が無駄に

[![](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F969e2c25-f99d-6110-7961-727ab347744a.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=680931155626e0127414ed80f9acfe59)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F969e2c25-f99d-6110-7961-727ab347744a.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=680931155626e0127414ed80f9acfe59)

---

## 思い込みは最大の敵

- 不具合解決において **思い込み** は最大の敵
- タイポはないはず
- 設定値は正しい値が設定されているはず
- 利用している環境は同じはず
- etc...
- いずれのステップも「思い込み」を排除して「事実」を積み重ねていく
- デバッガを使って処理の流れ、変数の値を確実にチェックする
- 面倒かもしれないが、些細なことも一つずつ確実に確認しながら進めることが不具合解決の一番の近道

[![](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F2bb287d1-2230-63f1-3856-8a81edefa710.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=a3021c2cba0ad97ee5a1cd628eadb902)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F28302%2F2bb287d1-2230-63f1-3856-8a81edefa710.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=a3021c2cba0ad97ee5a1cd628eadb902)

---

## まとめ

- まずは起こっていることを正確に把握する
- 不具合を再現させる
- まずは直接原因を特定する
- 例外のスタックトレースを読めば直接原因は簡単に特定できる
- 例外がスローされない場合は問題の値を処理している箇所を特定する
- 直接原因が分かったら、必ず根本原因まで掘り下げる
- 特定にはデバッガの利用が楽
- 根本原因が分かったら対策を講じ、不具合が解消されることを確認する
- いずれのステップも「思い込み」を排除して「事実」を着実に積み上げていくことが一番の近道

## Qiita Conference 2024 Autumn 11月14日(木)~15(金)開催！

![](https://cdn.qiita.com/assets/public/official_campaigns/qiita_conference_2024_autumn/image-under_article-c092ea0d42603790520f0858acf803a7.png)

Qiita Conferenceは、Qiita最大規模のテックカンファレンスです！

基調講演ゲスト(敬称略)

安野 貴博、藤本 真樹、まつもとゆきひろ（Matz）、上杉 周作 / 石原 ニコラス（Vercel Inc.）

[イベント詳細を見る](https://qiita.com/official-campaigns/conference/2024-autumn?utm_source=qiita&utm_medium=banner&utm_campaign=article_footer_banner_default&utm_content=default)

449

一度削除した記事は復旧できません。

この記事の編集中の下書きも削除されます。

削除してよろしいですか？