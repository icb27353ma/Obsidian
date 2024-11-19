---
title: "Windows 11とLinuxを別ドライブでデュアルブートする方法"
source: "https://partition.aomei.jp/windows-11/dual-boot-windows-11-and-linux-on-separate-hard-drives-7868-tc.html"
author:
  - "[[ひとみ]]"
published: 2024-01-02
created: 2024-11-19
description: "この記事では、Windows 11とLinuxを別ドライブでデュアルブートする方法を説明します。"
tags:
  - "clippings"
---
**目次**

1. [別ドライブでデュアルブートした方がよいでしょうか？](https://partition.aomei.jp/windows-11/#h_0)
2. [Windows 11とLinuxをデュアルブートする準備](https://partition.aomei.jp/windows-11/#h_1)
3. [別ドライブでWindows 11とLinuxをデュアルブートする方法](https://partition.aomei.jp/windows-11/#h_2)
1. [パート1. Linuxインストール用のパーティションを作成する](https://partition.aomei.jp/windows-11/#h_3)
2. [パート2. Linuxの起動可能なUSBドライブを作成する](https://partition.aomei.jp/windows-11/#h_4)
3. [パート3. パーティションにLinuxをインストールする](https://partition.aomei.jp/windows-11/#h_5)
4. [パート4. Windows 11とLinuxのデュアルブートを設定する](https://partition.aomei.jp/windows-11/#h_6)
4. [詳細情報：Windowsシステムをバックアップして、システムデータを安全に保護する](https://partition.aomei.jp/windows-11/#h_7)
5. [まとめ](https://partition.aomei.jp/windows-11/#h_8)

## 別ドライブでデュアルブートした方がよいでしょうか？

UbuntuとWindowsの両方をデュアルブートでインストールする場合、同じハードドライブ上の異なるパーティションよりも2つの異なるハードドライブにインストールする方が良いでしょうか？

![Windows11とUbuntu](https://partition.aomei.jp/screenshot/dual-boot-windows-11-and-linux-on-separate-hard-drives/linux-windows11.png)

UbuntuとWindowsの両方をデュアルブートする場合、同じハードドライブの異なるパーティションにインストールするよりも、それぞれ別ドライブにインストールする方が一般的に効率的で整理されていると考えられています。各オペレーティングシステムを別のドライブに配置することには、いくつかの利点があります。

各オペレーティングシステムをそれぞれ専用のハードドライブに配置することで、パーティションテーブルが整理されます。

ドライブの容量に応じて、各オペレーティングシステムにより多くのスペースが提供され、パフォーマンスが向上します。

パーティションの管理はより簡単になり、混乱の可能性が低くなります。

データのバックアップと復元が簡単になります。別のドライブを介さずに、簡単に1つのドライブからデータをバックアップできます。

## Windows 11とLinuxをデュアルブートする準備

別のハードドライブにWindows 11とLinuxをデュアルブートする手順に入る前に、以下の点を確認することが重要です。

- 既にWindows 11が動作しているハードドライブのコンピュータ。
- Linux Ubuntuインストール専用に割り当てた別のハードドライブ。
- Linuxのインストールメディアが格納された起動可能なUSB（少なくとも8GB）またはCD／DVD。
- 重要なデータの包括的なバックアップ。理想的には、このプロセスではデータが削除されないはずですが、念のため予防措置をとることが賢明です。
- 両方のドライブに約50GBの空き容量があることを確認します。

## 別ドライブでWindows 11とLinuxをデュアルブートする方法

必要な準備が完了したら、次の4つの手順に従ってWindows 11とLinuxをデュアルブートする方法を実行できます（このガイドでは、WindowsがPCにインストールされていると仮定しています）。

**注：**以下の手順は特にWindows 11とLinuxのデュアルブートに適用されます。ただし、これらの手順は一般的であり、他のオペレーティングシステムのデュアルブートにも適用できます。

### パート1. Linuxインストール用のパーティションを作成する

Linuxのインストールを準備するために、セカンダリハードドライブに指定されたパーティションを作成する必要があります。以下のガイドラインを考慮してください。

① セカンダリドライブは使用する前に[初期化](https://partition.aomei.jp/help/initialize-disk.html)する必要があります。これにはドライブ上にパーティションを作成する作業が含まれます。

② 使用済みのドライブの場合、異なるLinuxディストリビューションの仕様に応じて、50GBから100GBのパーティションを持っているか確認してください。

③ 使用済みの2番目のドライブに1つのパーティションしか含まれていない場合は、Linuxのインストール用に追加のパーティションを作成する方が良いです。インストールプロセス中に既存のパーティションデータは削除されます。

特殊なLinux用にカスタマイズされた新しいパーティションを作成するために、「ディスクの管理」やより強力なサードパーティツールを利用できます。

#### 🌺方法1：「ディスクの管理」を使用してパーティションを作成する

「ディスクの管理」を使用してパーティションを作成するには、ディスク内の未割り当て領域が必要です。**ハードドライブに１つのパーティションしかない場合、そのパーティションを縮小して未割り当て領域を作成し、新しいパーティションを作成する必要があります。**

ヒント：第一パーティションの隣に十分な未割り当て領域がある場合は、最初の3つのステップをバイパスして、ステップ4からステップ6までの手順に従って新しいパーティションを直接作成できます。

**ステップ 1.** 下部の「**スタート**」メニューを右クリックし、「**ディスクの管理**」を選択します。

**ステップ 2.** 「ディスクの管理」ウィンドウで、十分な空き領域を持つプライマリパーティションを右クリックし、「**ボリュームの縮小**」を選択します。

[![ボリュームの縮小](https://partition.aomei.jp/screenshot/create-and-format-a-hard-disk-partition-windows-11/shrink.png)](https://partition.aomei.jp/screenshot/create-and-format-a-hard-disk-partition-windows-11/shrink.png?_di_c=ZGV2X2lkXzFjNGM1YjJkLWNlY2YtNGYzMy04MzQ2LTIyNGJmOWE0YzI2MA== "ボリュームの縮小")

**ステップ 3.** 縮小する領域のサイズを入力し、「**縮小**」をクリックします。この操作により、必要な未割り当て領域が生成されます。

[![縮小する領域のサイズ](https://partition.aomei.jp/screenshot/create-and-format-a-hard-disk-partition-windows-11/enter.png)](https://partition.aomei.jp/screenshot/create-and-format-a-hard-disk-partition-windows-11/enter.png?_di_c=ZGV2X2lkXzFjNGM1YjJkLWNlY2YtNGYzMy04MzQ2LTIyNGJmOWE0YzI2MA== "縮小する領域のサイズ")

**ステップ 4.** プライマリパーティションを縮小した後、それの隣に未割り当て領域が表示されます。未割り当て領域上で右クリックし、「**新しいシンプルボリューム**」を選択します。

[![新しいシンプルボリューム](https://partition.aomei.jp/screenshot/create-and-format-a-hard-disk-partition-windows-11/new-simple-volume.png)](https://partition.aomei.jp/screenshot/create-and-format-a-hard-disk-partition-windows-11/new-simple-volume.png?_di_c=ZGV2X2lkXzFjNGM1YjJkLWNlY2YtNGYzMy04MzQ2LTIyNGJmOWE0YzI2MA== "新しいシンプルボリューム")

**ステップ 5.** 「新しいシンプルボリュームウィザードの開始」ウィンドウで「**次へ**」をクリックします。

[![新しいシンプルボリュームウィザード](https://partition.aomei.jp/screenshot/partition-ntfs-hard-drive/create-3.png)](https://partition.aomei.jp/screenshot/partition-ntfs-hard-drive/create-3.png?_di_c=ZGV2X2lkXzFjNGM1YjJkLWNlY2YtNGYzMy04MzQ2LTIyNGJmOWE0YzI2MA== "新しいシンプルボリュームウィザード")

**ステップ 6.** ボリュームのサイズを設定した上、「次へ」をクリックします。そして、新しいボリュームのドライブ文字（例えばLinux）を割り当て、「次へ」をクリックします。

![ドライブ文字](https://partition.aomei.jp/screenshot/dual-boot-windows-11-and-linux-on-separate-hard-drives/windows-11-and-linux-dual-boot-7.png)

#### 🌺方法2：サードパーティソフトを使用してパーティションを作成する

もちろん、Windowsの「ディスクの管理」には制限があります。特に、FAT16、FAT32、exFATなどの一部のファイルシステムに対するサポートが不足しています。また、利用可能なスペースがあるにもかかわらず、[「ボリュームの縮小」オプションがグレーアウト](https://partition.aomei.jp/articles/shrink-ssd-volume.html)するという問題が発生することもあります。

これらの制限に対処するためには、[AOMEI Partition Assistant Standard](https://partition.aomei.jp/free-partition-manager.html)のような強力なパーティションマネージャーを使用することが推奨されています。この**フリーソフト**は、FAT16、FAT32、およびNTFSに限定されているexFATなど、複数のファイルシステムの移動やサイズ変更をサポートしています。[暗号化されたパーティションのサイズ変更](https://partition.aomei.jp/articles/resize-bitlocker-partition-windows-10.html)や既存のパーティション上に新しいパーティションを直接作成することもできます。

**ステップ 1.** AOMEI Partition Assistant Standardをインストールし、起動します。ホームインタフェースは、すべてのハードディスクとパーティションの情報を表示します。

**ステップ 2.** ターゲットパーティションを見つけ、それを右クリックし、「**パーティションをリサイズ／移動**」を選択します。

[![パーティションをリサイズ/移動](https://partition.aomei.jp/screenshot/std/shrink-volume/resize-partition.png)](https://partition.aomei.jp/screenshot/std/shrink-volume/resize-partition.png?_di_c=ZGV2X2lkXzFjNGM1YjJkLWNlY2YtNGYzMy04MzQ2LTIyNGJmOWE0YzI2MA== "パーティションをリサイズ/移動")

**ステップ 3.** ポップアップウィンドウで、右にドラッグしてパーティションを縮小します。次に、「**はい**」をクリックします。

[![パーティションを縮小](https://partition.aomei.jp/screenshot/std/shrink-volume/resizing.png)](https://partition.aomei.jp/screenshot/std/shrink-volume/resizing.png?_di_c=ZGV2X2lkXzFjNGM1YjJkLWNlY2YtNGYzMy04MzQ2LTIyNGJmOWE0YzI2MA== "パーティションを縮小")

**ステップ 4.** AOMEI Partition Assistantの主な画面で未割り当て領域を右クリックしてドロップダウンメニューから「**パーティションを作成**」を選択します。

[![パーティションを作成](https://partition.aomei.jp/help/images/create-partition/1.png)](https://partition.aomei.jp/help/images/create-partition/1.png?_di_c=ZGV2X2lkXzFjNGM1YjJkLWNlY2YtNGYzMy04MzQ2LTIyNGJmOWE0YzI2MA== "パーティションを作成")

**ステップ 5.** ポップアップウィンドウでパーティションサイズ、ドライブ文字を指定できます。ファイルシステムを選択できます。更に、「詳細」をクリックして、パーティションラベル、パーティションタイプなども設定できます。そして「はい」をクリックして続行します。

[![新規パーティションの設定](https://partition.aomei.jp/help/images/create-partition/2.png)](https://partition.aomei.jp/help/images/create-partition/2.png?_di_c=ZGV2X2lkXzFjNGM1YjJkLWNlY2YtNGYzMy04MzQ2LTIyNGJmOWE0YzI2MA== "新規パーティションの設定")

**ステップ 6.** これで、作成された新しいパーティションの情報が表示されます。ツールバーの「**適用**」をクリックして新規パーティションの作成を実行します。

[![適用](https://partition.aomei.jp/help/images/create-partition/3.png)](https://partition.aomei.jp/help/images/create-partition/3.png?_di_c=ZGV2X2lkXzFjNGM1YjJkLWNlY2YtNGYzMy04MzQ2LTIyNGJmOWE0YzI2MA== "適用")

この方法で、新しいパーティションが正常に作成され、2番目のドライブにLinuxをインストールすることができます。

### パート2. Linuxの起動可能なUSBドライブを作成する

両方のオペレーティングシステムをインストールする際には、通常USBドライブが使用されます。起動可能なUSBドライブを作成する手順に従ってください。

注意：適切なLinuxディストリビューションをダウンロードしてください（例えばUbuntu）。

**ステップ 1.** 公式のUbuntu[ダウンロードページ](https://.ubuntu.com/download)にアクセスし、希望するバージョンを選択し、「**ダウンロード**」をクリックします。

**ステップ 2.** ダウンロードされたISOファイルを保存します。ISOファイル拡張子のファイルが作成されます。

**注意：**Linuxディストリビューションをダウンロードした後、Linuxディストリビューションをダウンロードした後、[Rufus](https://rufus.ie/ja/)を使用して起動可能なUSBドライブを作成します。USB上のデータが削除されるため、バックアップを取っておくことを確認してください。

**ステップ 3.** USBドライブをWindows PCに接続します。

**ステップ 4.** Rufusを起動し、「**デバイス**」ドロップダウンメニューからUSBドライブを選択します。

**ステップ 5.** ダウンロードしたLinux ISOファイルを選択します。

**ステップ 6.** 正しい設定を確認し、「**スタート**」をクリックしてプロセスを開始します。ポップアップウィンドウで「**OK**」をクリックして確認します。

![Rufus](https://partition.aomei.jp/screenshot/dual-boot-windows-11-and-linux-on-separate-hard-drives/windows-11-and-linux-dual-boot-12.png)

完了すると、起動可能なLinux USB ドライブが作成されます。

### パート3. パーティションにLinuxをインストールする

新しく作成したパーティションにUbuntuをインストールするには、以下の手順に従ってください。ブート可能なLinux USBドライブを挿入した後にこれらの手順を実行します。

**ステップ 1.** コンピュータを再起動し、F2、F10、F12、Delete、またはESCキーを押してBIOS設定にアクセスします（BIOSのショットキーはPCのブランドによって異なります）。

![BIOS](https://partition.aomei.jp/screenshot/en/others/windows-11/dual-boot-windows-11-and-linux-on-separate-hard-drives/dual-boot-bios-settings.png)

**ステップ 2.** 矢印キーで「**Boot**」タブに移動し、USBドライブを一番目の起動デバイスとして設定します。

**ステップ 3.** 変更を保存して終了するために「**F10**」キーを押します。

**ステップ 4.** コンピュータはUSBドライブから起動するはずです。ブートメニューから「**Ubuntu**」を選択し、「**Enter**」キーを押して続行します。

**ステップ 5.** 「**言語**」を選択し、「**Ubuntuをインストール**」をクリックします。「**ディスクを削除して Ubuntu をインストール**」を選択して「**インストール**」をクリックします。

![ディスクを削除して Ubuntu をインストール](https://partition.aomei.jp/screenshot/dual-boot-windows-11-and-linux-on-separate-hard-drives/disk-sakujyo-ubuntu.png)

**ステップ 6.** 次の画面で、Ubuntuをインストールするハードドライブを選択します。

**ステップ 7.** パーティションがフォーマットされたことを警告するメッセージが表示されます。「**続ける**」をクリックします。

![警告メッセージ](https://partition.aomei.jp/screenshot/dual-boot-windows-11-and-linux-on-separate-hard-drives/keikokoku-messeji.png)

**ステップ 8.** インストールを開始する前に、タイムゾーンやログインの詳細などの設定をカスタマイズします。

![アカウント](https://partition.aomei.jp/screenshot/dual-boot-windows-11-and-linux-on-separate-hard-drives/installUbuntu.png)

**ステップ 9.** インストールが完了すると、GRUBブートローダーメニューが表示され、オペレーティングシステムの選択が可能です。

![GRUBブートローダーメニュー](https://partition.aomei.jp/screenshot/en/others/windows-11/dual-boot-windows-11-and-linux-on-separate-hard-drives/grub-bootloader-menu.png)

注意：もしコンピュータのメインOSがUbuntuの場合、インストール手順は「**Windowsのブート可能なUSBドライブを挿入して再起動** >> **ブートメニューに入る** >> **USBデバイスをブートドライブに選択** \>> **2番目のハードディスクにWindowsオペレーティングシステムをインストール** >> **インストールを完了するために画面の指示に従う**」となります。

これで、別ドライブにWindows 11とLinuxのデュアルブートを設定しました。コンピュータを起動するたびに、希望するオペレーティングシステムを選択する必要があることに注意してください。

### パート4. Windows 11とLinuxのデュアルブートを設定する

GRUBにブートした後、Windows 11とUbuntu OSの間で選択することができます。これで、別ドライブにWindows 11とLinuxのデュアルブートを設定しました。

ご注意ください：コンピュータを起動するたびに、ご希望のオペレーティングシステムを選択する必要があります。煩わしいと感じる場合は、デフォルトのOSを設定することもできます。

## 詳細情報：Windowsシステムをバックアップして、システムデータを安全に保護する

前述したように、Windows 11とLinuxを別ドライブでデュアルブートすることは複雑で難しいです。重要なデータを外付けハードディスクにバックアップすることが賢明です。最良のシステムバックアップ方法の1つは、システムからあらゆる情報をコピーするOSのクローンを作成することです。では、OSを再インストールせずにWindowsシステムのクローンを作成するにはどうすればよいでしょうか?

Windowsには組み込みのクローン作成ツールがないため、信頼できるサードパーティ製のクローン作成ソフトを選択することができます。Linux用のパーティションを作成する部分では、AOMEI Partition Assistant Standardを使用することをお勧めします。

これらの基本的なパーティション管理機能とは別に、すべてを再インストールせずにWindows 11 OSのクローンをMBR・GPTディスクに作成する「**OSの移行**」などのより高度な機能を利用するには、[Professional](https://partition.aomei.jp/partition-manager-pro-edition.html)版にアップグレードすることを検討してください。

**注：**デモ版は動作確認の目的でのみ使用されます。つまり、デモでは、すべての機能をプレビュー、すべての操作をシミュレートすることしかできません。

**ステップ 1.** AOMEI Partition Assistantをインストールして起動します。メイン画面でディスクパーティション情報が表示されます。上部の「**クローン**」→「**OSをSSDに移行**」をクリックし、ポップアップウィンドウで「**次へ**」をクリックします。

[![OSをSSDに移行](https://partition.aomei.jp/help/images/migrate-system-wizard/1.png)](https://partition.aomei.jp/help/images/migrate-system-wizard/1.png?_di_c=ZGV2X2lkXzFjNGM1YjJkLWNlY2YtNGYzMy04MzQ2LTIyNGJmOWE0YzI2MA== "OSをSSDに移行")

**ステップ 2.** 次のウィンドウで、**ターゲットディスク（SSDまたはHDD）上の未割り当て領域を選択**し、「**次へ**」をクリックします。または、「すべてのパーティションを削除して...」のチェックボックスをオンにして未割り当て領域を作成することもできます。

[![未割り当て領域を選択](https://partition.aomei.jp/help/images/migrate-system-wizard/2.png)](https://partition.aomei.jp/help/images/migrate-system-wizard/2.png?_di_c=ZGV2X2lkXzFjNGM1YjJkLWNlY2YtNGYzMy04MzQ2LTIyNGJmOWE0YzI2MA== "未割り当て領域を選択")

**ステップ 3.** このウィンドウで、移行先のパーティションのサイズ、位置、それにドライブ文字などを変更することができます。もちろん、デフォルト設定を維持してもいいです。

[![パーティションの編集](https://partition.aomei.jp/help/images/migrate-system-wizard/3.png)](https://partition.aomei.jp/help/images/migrate-system-wizard/3.png?_di_c=ZGV2X2lkXzFjNGM1YjJkLWNlY2YtNGYzMy04MzQ2LTIyNGJmOWE0YzI2MA== "パーティションの編集")

**ステップ 4.** 設定が完了した後、「**次へ**」をクリックして「OSブート」に関するノートを読みます。

[![ブートノート](https://partition.aomei.jp/help/images/migrate-system-wizard/4.png)](https://partition.aomei.jp/help/images/migrate-system-wizard/4.png?_di_c=ZGV2X2lkXzFjNGM1YjJkLWNlY2YtNGYzMy04MzQ2LTIyNGJmOWE0YzI2MA== "ブートノート")

**ステップ 5.** 「**完了**」をクリックしてメインインターフェイスに戻ります。ここで、変更をプレビューすることができます。「**適用**」ボタンをクリックして保留中の操作をコミットしてください。

[![適用](https://partition.aomei.jp/help/images/migrate-system-wizard/5.png)](https://partition.aomei.jp/help/images/migrate-system-wizard/5.png?_di_c=ZGV2X2lkXzFjNGM1YjJkLWNlY2YtNGYzMy04MzQ2LTIyNGJmOWE0YzI2MA== "適用")

## まとめ

この記事では、Windows 11とLinuxを別ドライブでデュアルブートする方法を紹介しました。1つのPCで2つのオペレーティングシステムを使用するためのステップバイステップガイドに従ってください。

ただし、データのセキュリティと整合性を考慮して、進む前にAOMEI Partition Assistant Professionalを使用してWindows OSをクローンしてバックアップすることをお勧めします。AOMEI Partition Assistantは、Windows 11／10／8／8.1／7／XPの実用的なWindows OSマネージャーです。[GPT・MBRに変換](https://partition.aomei.jp/help/convert-gpt-mbr-disk.html?_di_c=ZGV2X2lkXzFjNGM1YjJkLWNlY2YtNGYzMy04MzQ2LTIyNGJmOWE0YzI2MA==)したり、[ディスク全体をクローン](https://partition.aomei.jp/help/clone-hard-disk.html?_di_c=ZGV2X2lkXzFjNGM1YjJkLWNlY2YtNGYzMy04MzQ2LTIyNGJmOWE0YzI2MA==)したり、インストール済みアプリを移行したりすることもできます。また、Windows Serverユーザー向けには[Server版](https://partition.aomei.jp/partition-manager-server-edition.html?_di_c=ZGV2X2lkXzFjNGM1YjJkLWNlY2YtNGYzMy04MzQ2LTIyNGJmOWE0YzI2MA==)もあります。