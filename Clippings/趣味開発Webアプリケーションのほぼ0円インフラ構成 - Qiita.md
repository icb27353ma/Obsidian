---
title: "趣味開発Webアプリケーションのほぼ0円インフラ構成 - Qiita"
source: "https://qiita.com/mazrean/items/f4a48d43b2d680a92216?utm_campaign=popular_items&utm_medium=feed&utm_source=popular_items"
author:
  - "[[mazrean]]"
published: 2024-12-04
created: 2024-12-06
description: "この記事はDeNA 25新卒 Advent Calendar 2024の5日目の記事です！今後、様々な記事がアップロードされていくと思うのでぜひ登録とチェックをしてみてください！趣味でWebサ…"
tags:
  - "clippings"
---
趣味でWebサービスを作ったはいいものの、サーバーの運用にコストがかかり結局停止してしまった経験、ありませんか？  
これらの趣味で作ったサービスはアクセス数が少なく、数日に1人程度しかアクセスがないことも多いため、収益がない場合がほとんどです。  
しかし、せっかく開発したのだから動かし続けたい気持ちはあると思いますし、運用し続けることで機能追加などをしてさらに楽しめることもあると思います。

このような運用コストに悩みがちな趣味開発Webアプリケーションですが、自分は趣味で現在いくつかのWebアプリケーションを**月当たり2円**というほぼ無料と言ってよいインフラコストで運用しています。  
そこで、この記事では**趣味開発のための低コストなインフラ運用方法**を紹介します。

## 前提

今回紹介するインフラでは、SSG+CSRによる静的配信のみで問題ないフロントエンドと、データベースを使用するコンテナ化可能なバックエンドにより構成されるWebアプリケーションを想定してインフラを構成します。  
ただし、あくまでアクセス数やデータサイズなどの規模が小さいアプリケーションを想定し、ある程度パフォーマンスも犠牲にするのも許容して金銭的コスト削減を主眼を置いたインフラ構成となっています。  
そのため、アクセス数が増加した場合などは逆にコストが上がったり、重大なパフォーマンス低下につながる可能性のあることに注意してください。  
また、「止めるよりはせっかくだから動かしておきたい」程度の温度感の運用を想定しており、あまり安定性を重視していないため、プレビューリリースの機能を多用している点にも注意してください。

## 全体像

インフラ構成の全体像は以下のようになります。

[![architecture.drawio.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F478477%2F346aad9b-99e7-6f24-e7a4-ea36a0a5b80a.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=9a626c354b23243ab9f6e1113c6c8fc5)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F478477%2F346aad9b-99e7-6f24-e7a4-ea36a0a5b80a.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=9a626c354b23243ab9f6e1113c6c8fc5)

様々なクラウドが入り混じっている構成となっています。  
データベースとしては無料枠の大きいTiDB CloudのTiDB Serverlessを採用しています。  
また、バックエンドはCloud Runで実行し、フロントエンドの静的配信はCloud Storageから行います。  
そして、ここが大きなポイントとなるのですが、Cloud Load BalancingではなくCloudflareのDNS ProxyモードとCloud Connectorを組み合わせることで、リクエストのCloud Run、Cloud Storage間の振り分けを行います。

ここからは、それぞれの構成要素について工夫点などを説明します。

## データベース: TiDB Serverless(TiDB Cloud)

個人開発の大きなコスト的負担になりがちなデータベースですが、自分はTiDB Serverlessを使用しています。  
TiDB ServerlessはMySQL互換の分散RDBMSをフルマネージドで提供してくれるサービスです。  
TiDBは分散データベースなため、異なる役割をもつコンポーネントが複数のサーバーに分散して乗っており、それらが連携することで1つのクラスターとなりMySQL互換RDBとして動作します。

TiDB Serverlessは個人開発で使う場合に非常にうれしいポイントとして、クラスター5つまでストレージ5GiB、5000万リクエストユニットの無料枠があり、小規模サービスであれば**多くの場合この無料枠で運用可能**な点があります。  
リクエストユニットについては、CPUやネットワークなどの使用量を抽象化した単位で詳細は以下で説明されています。

実際に使用する際にはサービスごとの処理内容を踏まえて概算してみるのをお勧めしますが、適切にindexを貼っているWebアプリケーションであれば、1クエリあたり数十~数百リクエストユニットの消費に収まると思います。

注意点としては、今回紹介するインフラ構成においてはCloud RunとTiDB Serverless間の通信はGoogle Cloudからの外向き通信となるため、やり取りするデータサイズによってはGoogle Cloudのネットワーク面での料金がおおきくなります。  
自分がこれまで動かしていた小規模サービスでは極めて少ない料金しか発生していませんでしたが、アプリケーションによっては注意が必要なポイントになります。

## コンピューティングリソース: Cloud Run(Google Cloud)

コンピューティングリソースとしてはCloud Runを利用しています。  
Cloud RunはGoogle Cloudのフルマネージドのコンテナ実行環境です。  
コンテナイメージなどの設定を基にリクエスト数などに応じてコンテナ数を自動でスケールしてくれます。  
通常の使用方法でもかなり費用を抑えることもできますが、今回はリクエストが来ないときはゼロスケール、つまりコンテナ数を0にすることで無料枠に収めます。  
また、自分の管理するドメインの割り当てにプレビューリリース段階のCloud Run domain mappingを利用することで、Cloud Load Balancingの月当たり数千円程度の費用を浮かせます。

## ゼロスケール

Cloud Runでは「インスタンスの最小数」を設定でき、これを0にするとリクエストが来ない期間にインスタンス数が0となり費用が発生しなくなります。  
[![image.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F478477%2F58c6c475-0a42-2b32-70e2-0a9d735baf6d.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=0dd2b0e7a37b78fa7d7b313fd66a1974)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F478477%2F58c6c475-0a42-2b32-70e2-0a9d735baf6d.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=0dd2b0e7a37b78fa7d7b313fd66a1974)

このようにすると、リクエストの処理時間のみ料金が発生する状態となります。  
現状、Cloud Runにはアカウント当たり無料枠がメモリ360,000 GB秒、CPU180,000 vCPU秒ある<sup><a href="https://qiita.com/mazrean/items/?utm_campaign=popular_items&amp;utm_medium=feed&amp;utm_source=popular_items#fn-1" id="fnref-1">1</a></sup>ため、小規模サービスでは無料枠から足が出ない状態になります。

### コールドスタート対策

Cloud Runの設定で最小インスタンス数を0とする場合、大きな問題となるのがコールドスタートによるレスポンスが帰るまでの時間の大幅増加です。  
特に今回の構成の場合、ネットワーク的に距離のあるTiDB Serverlessとのコネクションの確立に時間がかかるため、自分の運用しているアプリケーションではコールドスタート時間が10秒程度という許容できない値となっていました。

そこで定期的にリクエストを投げることでCloud Runのアイドル状態を維持するようにします。  
Cloud Runは最低インスタンス数以外の要因でのアイドル状態では費用が発生しない<sup><a href="https://qiita.com/mazrean/items/?utm_campaign=popular_items&amp;utm_medium=feed&amp;utm_source=popular_items#fn-2" id="fnref-2">2</a></sup>ため、このようにすることで費用を抑えつつコールドスタートを回避できます。

定期的にリクエストを投げる方法はcronなどどのような方法でも問題ありませんが、Cloud Monitoringの稼働時間チェック機能を利用するのがお手軽です。

稼働時間チェック機能では指定した指定したURLなどに対して定期的にHTTPリクエストなどを投げることで、死活監視を行う機能です。  
本来は前述のとおり死活監視のための機能なのですが、定期的にHTTPリクエストを投げるためこれを設定することでCloud Runのアイドル状態を維持できます。  
また、レイテンシーも記録されるため、アイドル状態が解除されてしまった場合にアラートを出すことなどもできます.  
[![image.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F478477%2F491e67e2-8a1a-23db-a9a5-d3fa9873ff07.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=5b80590e2e410178c5d0a3ec3a1bd6a1)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F478477%2F491e67e2-8a1a-23db-a9a5-d3fa9873ff07.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=5b80590e2e410178c5d0a3ec3a1bd6a1)

このコールドスタート対策の注意すべき点として、Cloud Runの挙動の変化によりアイドル状態を維持できなくなる可能性があり、確実性の低い点があります。  
Cloud Runのインスタンスがアイドル状態で維持される期間は明示されていないため、挙動の変化により即座にインスタンスが停止してしまいアイドル状態を維持できなくなる可能性があります。  
そのため、コールドスタートをどうしても避けたいサービスでは費用は上がってしまいますが最小インスタンス数を1に設定して確実にコールドスタートを回避するのをおすすめします。

## Cloud Run domain mapping

Cloud Runにカスタムドメインを割り当てる際にCloud Load Balancingを前段に置くのがもっとも一般的だと思いますが、Cloud Load Balancingはルールを設定している時間分だけ費用が発生するため規模の小さい場合でも関係なく月当たり3000円程度の費用が掛かります。  
これを回避する方法として今回はCloud Runのサービス自体にドメインを割り当てられるCloud Run domain mappingを利用します。

Cloud Run domain mappingは自分の所有するドメインをCloud Runのサービスに対して割り当てることのできる機能です。  
ドメインの所有確認は[Google Search Console](https://search.google.com/search-console/welcome?hl=ja)にドメインが登録されているかで判断されます。

このCloud Run domain mappingですが、現状プレビューリリース段階なのもありいくつか問題があります。

まず1つ目がカスタムドメインの割り当てが有効となる前にDNSレコードをCloud Runへ向ける必要がある点です。  
Cloud Run domain mappingではDNSレコードがCloud Runに向けられ次第、TLSの証明書を発行しカスタムドメインの割り当てが有効になります。  
そのうえ、DNSレコードがCloud Runに向いたことが確認されるまでのラグが非常に大きく、数時間程度かかってしまいます。  
このため、設定時に避けることのできない数時間のダウンタイムが発生します。

また、2つ目の問題として、東京リージョンでレイテンシーの増加する問題が発生する点があります。  
Cloud Runの既知の問題一覧に記載されているのですが、Cloud Run domain mapping自体にレイテンシーの問題があり、東京リージョン(`asia-northeast1`)で顕著とあります。

実際、自分が運用しているアプリケーションでも300ms程度のレイテンシーの増加を確認しています<sup><a href="https://qiita.com/mazrean/items/?utm_campaign=popular_items&amp;utm_medium=feed&amp;utm_source=popular_items#fn-3" id="fnref-3">3</a></sup>。

これらの問題は多くのサービスで大きな問題となると思います。  
しかし、今回は「止めるよりはせっかくだから動かしておきたい」程度の温度感なためコストが低い分のトレードオフと判断し、影響が少ない時間帯を見計らって移行したり、CDNやブラウザのキャッシュを使用できるようにしてごまかしたりしつつ、妥協しています。

## 静的配信: Cloud Storage(Google Cloud)

フロントエンドの静的配信にはCloud Storageを利用します。  
この部分については特に工夫はなく、配信するコンテンツをバケットへアップロードし、一般公開の設定をするだけです。  
ただし、Cloud Storageの無料枠は5GiB<sup><a href="https://qiita.com/mazrean/items/?utm_campaign=popular_items&amp;utm_medium=feed&amp;utm_source=popular_items#fn-4" id="fnref-4">4</a></sup>なため、これを超えるサイズの画像などがページに含まれる場合は費用が発生する点だけ注意が必要です。

## リクエスト振り分け: DNS Proxyモード+Cloud Connector(Cloudflare)

ここまででAPIサーバーのホスティングとフロントエンドの静的配信が可能になりました。  
しかし、アプリケーションを動かすためにはリクエストをこの2つの間で振り分けたいです<sup><a href="https://qiita.com/mazrean/items/?utm_campaign=popular_items&amp;utm_medium=feed&amp;utm_source=popular_items#fn-5" id="fnref-5">5</a></sup>。  
また、前述のとおり金銭的負担を考えるとCloud Load Balancingの使用は避けたいです。  
この問題は、CloudflareのDNSプロキシモードとCloud Connectorを組み合わせることで解決します。

## DNS Proxyモードとは

CloudflareのDNSレコードを設定する際に行えるで、DNS Proxyというものがあります。  
[![image.png](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F478477%2Fc745fb83-72e0-38df-0aa5-1c9faa649168.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=9cb30c14a9297fc8895a74c11c4e9feb)](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F478477%2Fc745fb83-72e0-38df-0aa5-1c9faa649168.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&s=9cb30c14a9297fc8895a74c11c4e9feb)

この設定を行うと、「DNSのみ」の場合と異なり、DNSレコードとしてCloudflareのサーバーへのAnycast IPアドレスが返され、Cloudflareのサーバーが自分の設定したIPアドレスなどへプロキシするようになります。

詳細な説明の記事としては以下が分かりやすいです。

Cloudflareが間に入ることでCDNキャッシュなどがDNSの設定のみで機能するなど便利な機能です。  
ただ、今回の記事で重要なのはCloudflareが間に入ってプロキシのように動作する、つまりうまく設定すれば**リクエストの振り分けにも使える**ということです。

## Cloud Connectorとは

リクエストの振り分けにも使えるとはいえ、これまではCloudflare WorkerによりJava Scriptでリクエストの振り分けを記述する必要があり、手間がかかる作業でした。  
そこを大きく改善したのがCloud Connectorです。

この機能を利用すると、Cloudflareから簡単なコンソール上の設定のみで条件に合致するリクエストをオブジェクトストレージへ振り分けることが可能になります。  
ただし、この機能は現在ベータ版である点だけ注意が必要です。

## 具体的な設定

ここまで説明した内容を組み合わせて、APIサーバーとしてCloud Run、フロントエンドの静的配信をCloud Storageへ振り分ける設定をしていきます。

まず、DNSレコードに以下のようにCloud RunへのCNAMEレコードを設定します。

```
test.example.com.	300	IN	CNAME	ghs.googlehosted.com.
```

この際、このレコードに対してDNS Proxyモードを有効にします。

次に、Cloud Connectorでフロントエンドに該当するパスへのリクエストをCloud Storageへ向ける設定を行います。

この2手順のみで、CloudflareでCloud Load Balancingで従来行うようなリクエストの振り分けが実現できます。

## WAFの設定

ここまでの設定でリクエストの振り分けは可能なのですが、現実には各種クロールや攻撃のリクエストなどがアプリケーションに飛んでくるため、無駄なCloud Runの起動が多発します。

そこで、Cloudflare WAFを利用します。

Cloudflare WAFではFree Planでも条件で使える表現などに制約はありますがカスタムルールを設定できます。  
また、リクエストを脅威レベルやBotの種別などを用いたルールも作成できるため、活用するとよいです。

## まとめ

今回はCloudflareやCloud Runの機能やTiDB Serverlessを活用することで、ほぼ無料で趣味開発サービスを運用し続ける方法を紹介しました。  
参考にしていただけると幸いです。

[^fn-1]: [https://cloud.google.com/free/docs/free-cloud-features?hl=ja#cloud-run](https://cloud.google.com/free/docs/free-cloud-features?hl=ja#cloud-run) [↩](https://qiita.com/mazrean/items/?utm_campaign=popular_items&utm_medium=feed&utm_source=popular_items#fnref-1)

[^fn-2]: [https://cloud.google.com/run/pricing?hl=ja](https://cloud.google.com/run/pricing?hl=ja) の料金表参照 [↩](https://qiita.com/mazrean/items/?utm_campaign=popular_items&utm_medium=feed&utm_source=popular_items#fnref-2)

[^fn-3]: 検証できていないのですが、大阪リージョンはレイテンシーの問題が顕著なリージョンとなっていないため、大阪リージョンにCloud Runを配置することで改善する可能性もありそうです。 [↩](https://qiita.com/mazrean/items/?utm_campaign=popular_items&utm_medium=feed&utm_source=popular_items#fnref-3)

[^fn-4]: [https://cloud.google.com/storage/pricing?hl=ja#cloud-storage-always-free](https://cloud.google.com/storage/pricing?hl=ja#cloud-storage-always-free) [↩](https://qiita.com/mazrean/items/?utm_campaign=popular_items&utm_medium=feed&utm_source=popular_items#fnref-4)

[^fn-5]: CORSなどを適切に設定して別ドメインで運用するという手段もありますが、設定ミスなどのリスクを考え同一ドメインでの運用としています [↩](https://qiita.com/mazrean/items/?utm_campaign=popular_items&utm_medium=feed&utm_source=popular_items#fnref-5)