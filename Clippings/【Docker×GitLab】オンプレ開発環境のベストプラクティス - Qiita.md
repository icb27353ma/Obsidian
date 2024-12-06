---
title: "【Docker×GitLab】オンプレ開発環境のベストプラクティス - Qiita"
source: "https://qiita.com/takoikakani/items/936faf23ee6bc286a270?utm_campaign=popular_items&utm_medium=feed&utm_source=popular_items"
author:
  - "[[takoikakani]]"
published: 2024-12-04
created: 2024-12-06
description: "はじめにこの記事ではオンプレ開発環境の私なりのベストプラクティスを紹介していきます。オンプレ開発環境の構築・更改にこれから携わる人の助けになれば嬉しいです。タイトルとしては\"オンプレ開発環境\"…"
tags:
  - "clippings"
---
## はじめに

この記事ではオンプレ開発環境の私なりのベストプラクティスを紹介していきます。  
オンプレ開発環境の構築・更改にこれから携わる人の助けになれば嬉しいです。

タイトルとしては"オンプレ開発環境"と書きましたが、より範囲を狭めて言うと、インターネット接続ができない現場での開発環境です。

要するにGitHubとかが使えない環境です。

そういった環境だと、自前でGitサーバや自動テストサーバを構築している場合が多いですね。

私もそういった現場をいくつか経験してきたのですが、その中でも、Docker×GitLabの組み合わせが個人的に一番使い勝手が良かったです。  
今回はDocker×GitLab(主にGitLab)の紹介とインターネットに繋がらない環境でのインストール方法を解説していきます。

## Docker×GitLab(主にGitLab)の紹介

今回Docker×GitLabのテーマではありますが、Dockerの良さについては多くの人が知る所なので、ここではGitLabをオンプレ開発環境に導入するメリットについて紹介していきます。

### ①GitLabの充実した機能

まずはGitLabでそもそも何ができるのか？というところが分からないと導入の俎上にも上がらないと思いますので、機能面から紹介していきます。

ざっくり言うと、開発環境のサーバ側に欲しい機能はGitLabを導入すると大体整います。

主要な機能についてそれぞれ少し掘り下げて紹介します。

#### Gitリポジトリ

GitLabは当然Gitサーバとして機能するのでソースコード管理ができます  
コミットのツリー表示やGUIベースでのプルリクエスト(マージリクエスト)やレビューコメントができます。  
GitHubライクな使い方が可能なのでレビューもサクサクです。

#### CI/CD

GitLabのうりの一つであるCI/CDも勿論オンプレ環境で実現可能です。  
「プッシュのタイミングでの自動テスト実行」や「masterへのマージでk8sのPodデプロイ」など、CI/CDで想像することはおよそできます。  
(こういう現場だと本番環境は更に隔離されていて...みたいなこともよくあるのでCDまでやっている所は少ないかもですが...)

自動テスト実行程度であれば、CI/CD定義の書き方も1日あれば習得可能なレベルなので、新しくCI/CDを始める場合にもお勧めです。

#### プロジェクト管理

イシュー管理やマイルストーン管理ができます。※イシュー=チケット

GitLabだけで実現できるので、これから新しく環境を構築する場合などは、GitLabに集約してプロジェクト管理のソフト導入の手間を削減することも可能です。  
(プロジェクト管理が主機能というわけではないので、Jiraとかと比べると劣る部分もありますが...)

また、イシューをコミットやマージリクエストと紐づけることができUIも分かり易いので、個人的にはExcelより使いやすいと思います。  
Excel管理から解放されたい人には凄くお勧めの機能で、特にレビューコメントの管理などはExcelで管理するよりも圧倒的に楽です。

※一応CSV出力とかもできるのでExcel納品系のルールがある現場でも使えそうな気はします。

#### (おまけ)業務の自動化

GitLabは種々の機能のAPIが公開されているので、例えば期限が過ぎたイシューのアラートメールを出したり、チャット等外部ツールトリガーでイシューを起票したりでき、業務自動化ツールを作ったりチャットbotと連携させたりできます。  
が、多少作りこみが必要なのと、オンプレ環境だと外部ツール入れたりネットワーク繋げたりが大変なことも多いので、ここについては導入のハードルは多少あるかと思います。

### ②オンプレ環境でも導入が簡単

GitLabは自前サーバ上に構築することができるのでオンプレ環境でも導入が可能で、インターネット接続不可の環境でも比較的簡単にインストールすることが可能です。

詳細は次章のインストール手順で記載していきます。

### ③日本語対応

デフォルトで日本語対応しています。  
(こういう環境はだいたい機械翻訳も使えないので日本語化は結構ありがたい)

また、GitLabのドキュメントもパートナー企業の方が日本語版を作成してくれていて凄く助かります。

## オンプレ環境でも簡単なインストール手順

ここではインターネットに接続できないオンプレでの環境構築を想定して、Docker, GitLabのインストール方法を紹介していきます。

### １．Dockerインストール

dockerのオフラインインストールは公式手順にもあるので、そちらを参考に頂ければと思いますが、  
　CentOS: [https://docs.docker.com/engine/install/centos/#install-from-a-package](https://docs.docker.com/engine/install/centos/#install-from-a-package)  
　Ubuntu: [https://docs.docker.com/engine/install/ubuntu/#install-from-a-package](https://docs.docker.com/engine/install/ubuntu/#install-from-a-package)  
例えば私のUbuntu環境だと以下の通りインストールが出来ます。

#### ①以下のリポジトリからパッケージをダウンロード

ダウンロード対象のパッケージ

- containerd.io\_\_.deb
- docker-ce\_\_.deb
- docker-ce-cli\_\_.deb
- docker-buildx-plugin\_\_.deb
- docker-compose-plugin\_\_.deb

※バージョンは特にこだわりなければ最新のもので良いです。

#### ②ダウンロードしたパッケージをオンプレサーバにアップロード

※最大で30MiB程度なのでCDメディアしかないようなヤバめの環境でも安心です。

#### ③インストール

インストールコマンド

```
sudo dpkg -i ./containerd.io_<version>_<arch>.deb \
  ./docker-ce_<version>_<arch>.deb \
  ./docker-ce-cli_<version>_<arch>.deb \
  ./docker-buildx-plugin_<version>_<arch>.deb \
  ./docker-compose-plugin_<version>_<arch>.deb
```

#### ④Docker起動

サービス開始コマンド

```
sudo service docker start
sudo docker run hello-world
```

### ２．GitLabインストール

続いてGitLabもインストールします。  
インストールといってもコンテナイメージを別端末でダウンロードして、それを１．でインストールしたオンプレサーバのDockerにロードするだけです。

#### ①コンテナイメージをダウンロード

```
docker pull gitlab/gitlab-ce
docker save <イメージID> > gitlab-ce.tar
```

#### ②ダウンロードしたファイルをオンプレサーバにアップロード

※ファイルサイズが3G超あるので、物理メディアでやり取りしている環境などでは少し工夫が必要かもしれません。

#### ③コンテナイメージのロード

```
docker load < gitlab-ce.tar
```

#### ④GitLabコンテナ起動

起動コマンドの例  
[https://docs.gitlab.com/ee/install/docker/installation.html#install-gitlab-by-using-docker-engine](https://docs.gitlab.com/ee/install/docker/installation.html#install-gitlab-by-using-docker-engine)

```
export GITLAB_HOME=/srv/gitlab
sudo docker run --detach \
   --hostname gitlab.example.com \
   --env GITLAB_OMNIBUS_CONFIG="external_url 'http://gitlab.example.com'" \
   --publish 443:443 --publish 80:80 --publish 22:22 \
   --name gitlab \
   --restart always \
   --volume $GITLAB_HOME/config:/etc/gitlab \
   --volume $GITLAB_HOME/logs:/var/log/gitlab \
   --volume $GITLAB_HOME/data:/var/opt/gitlab \
   --shm-size 256m \
   gitlab/gitlab-ce:latest
```

コマンドオプションは環境によりけりなので、お使いの環境に合わせて下さい、となってはしまいますが、どの環境でも共通して使う設定は以下かと思います。

GitLabのWebページを開く際のURL

```
--env GITLAB_OMNIBUS_CONFIG="external_url 'http://gitlab.example.com'"
```

※ブラウザからもIPアドレス形式でアクセスする場合([https://www.mathkuro.com/docker/expose-gitlab-on-different-ports/](https://www.mathkuro.com/docker/expose-gitlab-on-different-ports/))

ポート番号のバインド

```
--publish 50443:443 --publish 50080:80 --publish 50022:22
```

※<ホスト側のポート番号>:<コンテナ側のポート番号>となっているので、コンテナ側は変更しないでください。  
[https://qiita.com/kubocchi/items/dee7498ec2dabacc503f](https://qiita.com/kubocchi/items/dee7498ec2dabacc503f)

GitLabデータの保存先

```
export GITLAB_HOME=/srv/gitlab
```

※永続データの保存先です。リポジトリ・ログ・設定ファイル全て含まれるので、冗長化やバックアップが可能な場所が望ましいです。

#### ⑤初回ログイン

ログインはWebブラウザから行います。URLは④で設定したURLです。

構築時はrootユーザしか存在しないため、初回ログインはrootユーザを使用します。  
rootユーザの初期パスワードは以下のコマンドで取得できます。

```
sudo docker exec -it gitlab grep 'Password:' /etc/gitlab/initial_root_password
```

### ３．GitLab Runnerインストール(オプション)

必須ではないですが、GitLab Runnerも併せて導入しておくと、オンプレ環境でもCI/CDを回すことができるのでオススメです。

オンプレサーバにアップロードするまでの流れはGitLab同様です。  
①GitLab Runnerをダウンロード

```
docker pull gitlab/gitlab-runner
docker save <イメージID> > gitlab-runner.tar
```

②ダウンロードしたファイルをオンプレサーバにアップロード  
※ファイルサイズが3G超あるので、物理メディアでやり取りしている環境などでは少し工夫が必要かもしれません。

③コンテナイメージのロード

```
docker load < gitlab-runner.tar
```

④GitLabランナーのコンテナ作成

```
docker run -d --name gitlab-runner --restart always \
  -v /srv/gitlab-runner/config:/etc/gitlab-runner \
  -v /var/run/docker.sock:/var/run/docker.sock \
  gitlab/gitlab-runner:latest
```

GitLab本体同様、オプションは環境次第ではありますが、Executorにdockerを使用する場合は多くの環境でこのコマンドになるかと思います。  
※こだわりなければ、Executorはdockerが楽な気がします。

④GitLabにRunnerを登録  
Runner登録コマンドを実行

```
docker run --rm -it -v /srv/gitlab-runner/config:/etc/gitlab-runner gitlab/gitlab-runner register
```

このコマンドを実行すると以下の5つの質問がされます

```
Enter the GitLab instance URL (for example, https://gitlab.com/):
```

→GitLabコンテナ作成時に設定したURLで問題ありません

```
Enter the registration token:
```

→GitLabにブラウザからrootユーザでログインしてトークンを確認してください。  
・Runnerページを開く  
<GitLabのURL>/admin/runners  
・「新規インスタンスランナー」をクリック  
・項目を適宜入力し、「Runnerを作成」をクリック  
・ステップ1下部に「Runner認証トークン」が表示されるのでコピーして使用

```
Enter a name for the runner. This is stored only in the local config.toml file:
```

→任意の名称で問題ありません

```
Enter an executor: ssh, parallels, virtualbox, kubernetes, docker-autoscaler, instance, custom, shell, docker+machine, docker, docker-windows:
```

→特にこだわりなければdockerがこの記事で紹介している環境と親和性が高く、今後もオンプレ環境のCI/CDで使い勝手が良いのでオススメです。

```
Enter the default Docker image (for example, mcr.microsoft.com/windows/servercore:1809):
```

→任意のイメージ名で問題ありません。

これでRunnerがGitLabに登録され、ついにオンプレに高機能なCI/CD環境が整ったことになります。

GitLabでの具体的なCI/CDについてはこの記事では触れませんが、以下のように日本語の記事も多数存在しているので比較的容易に習得できるかと思います。  
[https://gitlab-docs.creationline.com/ee/tutorials/create\_register\_first\_runner/](https://gitlab-docs.creationline.com/ee/tutorials/create_register_first_runner/)

## 終わりに

今回は(インターネット接続不可の)オンプレ開発環境のベストプラクティスとしてDocker×GitLabを紹介しました。  
どれだけクラウド化が進んでもオンプレ環境として残ってしまう環境はあることでしょう。この記事を読んでくださった方の中には、今後そういったプロジェクトの立ち上げに携わることもあるかもしれません。そういった時にこの記事が何かの助けになれば幸いです。