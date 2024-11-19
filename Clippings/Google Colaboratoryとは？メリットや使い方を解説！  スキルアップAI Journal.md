---
title: "Google Colaboratoryとは？メリットや使い方を解説！ | スキルアップAI Journal"
source: "https://www.skillupai.com/blog/tech/google-colaboratory-1/"
author:
  - "[[スキルアップAI事務局]]"
published: 2022-01-18JST10:26
created: 2024-11-19
description: "Google Colaboratoryとは、Google社が提供している、ブラウザから直接Pythonを記述、実行できるサービスです。この記事では、Google Colaboratoryを使用するメリットや使い方について紹介しています。プログラミング初心者の方などは、ぜひ参考にしてください。"
tags:
  - "clippings"
---
こんにちは。スキルアップAIの東です。

機械学習にチャレンジしてみようと思ったものの、Pythonを実行するための環境構築がうまくできずに困ったことはありませんか。プログラミング初心者がいざ学習をやってみようと思っても、その前段階の環境構築で時間がかかってしまうことは珍しくありません。

そこでおすすめなのが、面倒な環境構築を行わずに使用できる[Google Colaboratory](https://colab.research.google.com/?hl=ja)です。Google Colaboratoryを使用することで、**ブラウザから直接Pythonを記述・実行できます。** また、環境構築の手間が省けるだけでなく、たくさんの優れた機能を兼ね備えています。  
本ブログでは、Google Colaboratoryの特徴や使い方について紹介するので、ぜひ参考にしてください。

<目次>

1. [Google Colaboratoryとは？](https://www.skillupai.com/blog/tech/google-colaboratory-1/#no1)
2. [Google Colaboratoryの特徴・メリット](https://www.skillupai.com/blog/tech/google-colaboratory-1/#no2)
3. [Google Colaboratoryの使い方](https://www.skillupai.com/blog/tech/google-colaboratory-1/#no3)
4. [おわりに](https://www.skillupai.com/blog/tech/google-colaboratory-1/#no4)

  

## 1.Google Colaboratoryとは？

Google Colaboratoryとは、[Google社](https://about.google/)が提供している、**ブラウザから直接Pythonを記述、実行できるサービス**です。Googleドライブに保存されるJupyterノートブック環境のようなもので、Googleドライブ上でコードの記述や実行、共有ができます。ノートブックのドキュメントはセルで構成されており、各セルにコードやテキスト・画像などを含められます。

![](https://www.skillupai.com/wp-content/uploads/2022/01/google-colaboratory-1.png)

図1. Google Colaboratoryの使用例

## 2.Google Colaboratoryの特徴・メリット

Google Colaboratoryには、以下の3つの特徴・メリットがあります。

1. Pythonの開発環境を構築せずに利用できる
2. 簡単に他ユーザとコードの共有ができる
3. GPUやTPUといったハードウェア機能を無料で使用できる

  

### 1.Pythonの開発環境を構築せずに利用できる

一般的に、コンピュータ上でPythonの開発・実行を行おうとすると、まず環境の構築から行わなければなりません。例えば、Jupyterノートブックを使用するとなると、まずはAnaconda等のツールをインストールしてPythonを使用できる環境を整えたうえで、それからJupyterノートブックをコンピュータにインストールするという作業が必要です。この環境構築がプログラミング初心者には特に難しく、この段階でつまずいてしまうことが多々あります。しかし、Google Colaboratoryを使用すれば**面倒で難しい環境構築を行わずともブラウザ上でPythonを使用できます。**Googleアカウントを用意するだけで手軽にPythonを実行することができるのです。

### 2.簡単に他ユーザとコードの共有ができる

一般的に、Pythonのコードを記述したプログラムファイルを他のユーザと共有する際は、いちいちメールに添付して転送したりしなければなりません。しかし、Google ColaboratoryのノートブックはGoogleのサービス上で作成されるので、**Googleドライブの共有機能を使って簡単に他のGoogleユーザと共有することが可能**です。また、ノートブックをGitHubにエクスポートして共有することもできます。作成したノートブックはJupyterノートブック形式で保存されるようになっており、Jupyterノートブック等の互換性のあるフレームワークでは閲覧や実行などが行えます。そのため、**Googleユーザ以外のJupyterノートブック等を使用している方とのファイルの共有も可能**です。

### 3.GPUやTPUといったハードウェア機能を無料で使用できる

大量のデータを必要とする機械学習においては、効率的に学習を行うためにGPUやTPUのようなハードウェアが必要になります。GPUやTPUを使用することで、高速での並列処理が可能となり、モデルの学習時間が大幅に短縮されるでしょう。 GPUやTPUを利用するには通常、1時間あたり数百円くらいかかります。Google Colaboratoryでは、**GPUとTPUを一定の条件において無料で使用できます。**GPUやTPUの利用の際は、設定タブにてGPUやTPUに切り替えるだけなので、非常に簡単です。

## 3.Google Colaboratoryの使い方

Google Colaboratoryを使用する際、Pythonの記述は「Colabノートブック」と呼ばれるノートブック上で行います。このColabノートブックのコードセルにPythonのコードを入力することで、Pythonを実行できます。

さらにこのコラムでは、以下2つの方法について紹介していきましょう。

- Colabノートブックの作成方法
- TensorFlowのインストール方法

  

### Colabノートブックの作成方法

では、実際にColabノートブックを作成する方法を解説していきます。

Colabノートブックの作成はGoogleドライブから行います。Googleアカウントでログイン後Googleドライブにアクセスし、左上の「新規」をクリックします。

![](https://www.skillupai.com/wp-content/uploads/2022/04/google-colaboratory-3_01-526x475.png)

次にリストの中から「その他」を選択し、「Google Colaboratory」をクリックします。  
もし「その他」の中に「Google Colaboratory」が表示されない場合はGoogle Colaboratoryがインストールされていませんので下側にある「アプリを追加」からGoogle Colaboratoryをインストールしてください。

![](https://www.skillupai.com/wp-content/uploads/2022/04/google-colaboratory-3_02-499x475.png)

この方法で、Colabノートブックが作成されます。ノートブック上に新しいコードセルが用意されており、このセルにPythonコードを入力すればPythonを実行できます。

このようにGoogle Colaboratory では、Googleドライブにログインするだけでノートブックを簡単に作成できます。

![](https://www.skillupai.com/wp-content/uploads/2022/04/google-colaboratory-3_03-900x161.png)

### TensorFlowのインストール方法

Google Colaboratoryでは、使用したいライブラリをインストールできます。その一例として、ここではTensorFlowをインストールする方法を解説します。なおTensorFlowではCPUバージョンとGPUバージョンの2種類が用意されていますが、今回はGPUバージョンのTensorFlowをインストールしてみましょう。

まず、全てのランタイムをリセットし、ランタイムをGPUに設定します。下の図のようにメニューから「ランタイム」をクリックし「ランタイムを出荷時設定にリセット」をクリックしてください。

![](https://www.skillupai.com/wp-content/uploads/2022/04/google-colaboratory-3_04-664x475.png)

リセットした後再び「ランタイム」をクリックし「ランタイムのタイプを変更」をクリックします。

![](https://www.skillupai.com/wp-content/uploads/2022/04/google-colaboratory-3_05-664x475.png)

Colabの環境をGPUに設定するため、「ハードウェア アクセラレータ」を「GPU」に変更して「保存」をクリックします。これで、Colabの実行環境がGPUに設定されました。

![](https://www.skillupai.com/wp-content/uploads/2022/04/google-colaboratory-3_06-484x475.png)

次に、pipコマンドを使用してTensorFlowのインストールを行います。

```
!pip install tensorflow-gpu
```

このようにコードセルにインストールコマンドを入力します。コマンドを入力後、図の赤枠で示したボタンをクリックすれば、インストールコマンドが実行されます。

![](https://www.skillupai.com/wp-content/uploads/2022/04/google-colaboratory-3_07-900x130.png)

これでTensorFlowがインストールできました。TensorFlowのインストールにかかった時間は約1分と、インストール自体はとても簡単です。

![](https://www.skillupai.com/wp-content/uploads/2022/04/google-colaboratory-3_08-900x390.png)

次に、TensorFlowが正常にインストールされたか確認するため、インストールされたバージョンを出力してみます。

```
import tensorflow as tf
print(tf.__version__)
```

![](https://www.skillupai.com/wp-content/uploads/2022/04/google-colaboratory-3_09-900x166.png)

このようにコードセルに入力し、コードを実行します。バージョンが出力されれば、TensorFlowは正常にインストールされています。

![](https://www.skillupai.com/wp-content/uploads/2022/04/google-colaboratory-3_10-900x69.png)

## 4.おわりに

本コラムでは、Google Colaboratoryの概要やメリット、使い方について紹介しました。

Google Colaboratoryには、以下3つのメリットがあります。

- Pythonの開発環境を構築せずに利用できる
- 簡単に他ユーザとコードの共有ができる
- GPUやTPUといったハードウェア機能を無料で使用できる

Google ColaboratoryはGoogleアカウントをもっているだけで簡単に使用できます。ぜひ一度気軽に触れてみてはいかがでしょうか。

スキルアップAIでは、関連講座として「[機械学習のためのPython入門講座](https://www.skillupai.com/python/)」を開講中です。本講座では、**Pythonプログラミング未経験レベルから、scikit-learnを用いて機械学習モデルを構築することを目指します。**

また、毎週水曜日には実践的AI勉強会「[スキルアップAIキャンプ](https://www.skillupai.com/skillupai-camp/)」を開催。勉強会では、Google Colaboratoryを使用したハンズオンなども行っています。興味がある方は、ぜひご参加ください！

[有料版Google Colab Proとは？特徴やメリットを解説！](https://www.skillupai.com/blog/tech/google-colaboratory-2/)

![](https://www.skillupai.com/wp-content/uploads/2019/07/C2-4-08-e1564459964113-500x475.jpg)

### 【監修】スキルアップAI 取締役CTO 小縣信也

AI指導実績は国内トップクラス。「太陽光発電発電量予測および異常検知」など、多数のAI開発案件を手掛けている。日本ディープラーニング協会主催2018E資格試験 優秀賞受賞、2019#1E資格試験優秀賞受賞。著書「徹底攻略ディープラーニングE資格エンジニア問題集」（インプレス）。

[![](https://www.skillupai.com/wp-content/uploads/2021/12/173ad6e8f75dc47e05fd0133fec8eded-580x181.png)](https://www.youtube.com/AIBusinessChannel/)

[![スキルアップAI 公式LINEアカウント](https://www.skillupai.com/assets/images/common/linebanner_pc.jpg)![](https://www.skillupai.com/assets/images/common/linebanner_pc.jpg)](https://lin.ee/0tFjgVZ)

スキルアップAIのメールマガジンでは会社のお知らせや講座に関するお得な情報を配信しています。  
配信を希望される方は[こちら](https://share.hsforms.com/1_XlReV-4Te-zcxCl9lhffA2mtef)

また、SNSでも様々なコンテンツをお届けしています。興味を持った方は是非チェックしてください♪