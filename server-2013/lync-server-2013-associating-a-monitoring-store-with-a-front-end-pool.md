﻿---
title: フロントエンド プールへの監視ストアの関連付け
TOCTitle: フロントエンド プールへの監視ストアの関連付け
ms:assetid: d3a20d5e-3f24-4cff-bc9b-4f84fea30e6b
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ205271(v=OCS.15)
ms:contentKeyID: 48273670
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# フロントエンド プールへの監視ストアの関連付け

 

_**トピックの最終更新日:** 2013-04-22_

Microsoft Lync Server 2013 の監視データは監視ストアが関連付けられているフロントエンド プールでのみ収集できます。関連付けは、一般的にはトポロジ ビルダーでフロントエンド プールを定義するときに行うタスクです。監視ストアを新しいフロントエンド プールに関連付けるには、新しいフロントエンド プールの定義ウィザードの \[**機能の選択**\] ページで、\[**監視を有効にする (通話詳細記録と QoE 指標ロギング)**\] オプションを選択するようにします。このオプションを選択した場合、ウィザードを完了するには SQL ストアも指定する必要があることに注意してください。ただし、このストアはウィザードを実行している時点では存在している必要はありません。つまり、先にプールを監視ストアに関連付けておき、後からそのストアを設定および構成することができます。

この他に、以下の手順を行うことにより既存のフロントエンド プールを新しいまたは別の監視ストアに関連付けることもできます。

1.  \[**スタート**\]、\[**すべてのプログラム**\]、\[**Microsoft Lync Server 2013**\]、\[**Lync Server トポロジ ビルダー**\] の順にクリックします。

2.  \[**トポロジ ビルダー**\] ダイアログ ボックスで、\[**既存の展開からトポロジをダウンロードする**\] を選択して \[**OK**\] をクリックします。

3.  \[**名前を付けて保存**\] ダイアログ ボックスで、現在のトポロジ用のファイル名を入力し、\[**保存**\] をクリックします。

4.  トポロジ ビルダーで、\[**Lync Server 2013**\] を展開します。さらに、フロントエンド プールを含むサイトの名前を展開し、\[**Enterprise Edition フロントエンド プール**\] をクリックして開きます。

5.  監視ストアに関連付けるプールの名前を右クリックし、\[**プロパティの編集**\] をクリックします。

6.  \[**プロパティの編集**\] ダイアログ ボックスの \[**全般**\] タブで、\[**監視 (CDR と QoE 指標)**\] オプションを選択し、既存の SQL Server データベースを \[**監視 SQL Server ストア**\] ドロップダウン リストから選択します (または、\[**新規**\] をクリックしてプールを新しいデータベース ストアに関連付けます。) 新しいデータベース ストアを使用するように選択した場合は、\[**新しい SQL ストアの定義**\] ダイアログ ボックスで、SQL Server コンピューターの完全修飾ドメイン名を \[**SQL Server の FQDN**\] ボックスに入力します。ストアに既定の SQL Server インスタンスを使用する場合は、\[**既定のインスタンス**\] を選択します。それ以外の場合は \[**名前付きインスタンス**\] をクリックし、インスタンス名を \[**名前付きインスタンス**\] ボックスに入力します。
    
    \[**プロパティの編集**\] ダイアログ ボックスでは、監視データベースの SQL ミラーを作成するオプションを指定することもできます (SQL ミラーは、監視データベースの 2 つのコピーを保持することを可能にします。1 つのコピーは監視ストア コンピューターに保管され、もう 1 つは SQL ミラー コンピューターに保管されます)。ミラーリングを有効にするには、\[**この SQL インスタンスはミラーリングの関係にある**\] を選択し、ミラー サーバーのポート番号を \[**ミラー ポート番号**\] ボックスに入力します。

7.  \[**プロパティの編集**\] ダイアログ ボックスで、\[**OK**\] をクリックします。

監視ストアをフロントエンド プールに関連付けたら、新しいトポロジを公開する必要があります。これを行うまで変更は有効になりません。新しいトポロジを公開するには、トポロジ ビルダーで以下の手順を行います。

1.  \[**操作**\] をクリックし、\[**トポロジ**\] をポイントし、\[**公開**\] をクリックします。

2.  トポロジの公開ウィザードの \[**トポロジの公開**\] ページで、\[**次へ**\] をクリックします。

3.  \[**公開ウィザード完了**\] ページで、\[**完了**\] をクリックします。

トポロジが公開されたら、監視ストアをホストするコンピューターに監視データベースをインストールします。監視データベースは Lync Server 管理シェルおよび Windows PowerShell を使用してインストールできます。データベースをローカルにインストールする場合 (Lync Server 管理シェルを実行するコンピューターと同じコンピューターにデータベースをインストールする場合) は、そのコンピューター上で管理シェルを開始し、以下のコマンドを入力して Enter キーを押します。

    Install-CsDatabase -LocalDatabases

上記のコマンドを実行すると、Install-CsDatabase が現在の Lync Server トポロジを読み取り、ローカル コンピューターにインストールする必要のあるデータベースを判別し、その各データベースを自動的にインストールして構成します。

データベースをリモート コンピューター (管理シェルを実行するコンピューターとは別のコンピューター) にインストールする場合は、少なくとも 2 つのパラメーター (ConfiguredDatabases パラメーターと、SqlServerFqdn パラメーター) を含める必要があります。これらのパラメーターが指定されると、Install-CsDatabase コマンドレットは Lync Server トポロジを取得してから、SqlServerFqdn パラメーターで指定されたコンピューターに必要なデータベースをインストールして構成します。SqlServerFqdn パラメーターには、データベースのインストール先となるコンピューターの完全修飾ドメイン名を表すパラメーター値を使用する必要があります。

たとえば、次のコマンドは監視データベースを atl-sql-001.litwareinc.com というコンピューターにインストールします。

    Install-CsDatabase -ConfiguredDatabases -SqlServerFqdn atl-sql-001.litwareinc.com

また、監視データベースは、監視ストアをホストするコンピューターで Lync Server 展開ウィザードを実行することによってもインストールできます。このためには、該当のコンピューターにログオンし、以下の手順を行います。

1.  \[**スタート**\]、\[**すべてのプログラム**\]、\[**Microsoft Lync Server 2013**\]、\[**Lync Server 展開ウィザード**\] の順にクリックします。

2.  展開ウィザードで、\[**Lync Server システムのインストールまたは更新**\] をクリックします。

3.  \[**展開**\] ページの \[**手順 2: Lync Server コンポーネントの設定または削除**\] の下で、\[**再実行**\] をクリックします。

4.  Lync Server コンポーネントのセットアップ ウィザードの \[**Lync Server コンポーネントのセットアップ**\] ページで、\[**次へ**\] をクリックします。

5.  \[**MSI へのパスの指定**\] ページで、Ocscore.msi ファイル (Lync Server インストール メディアに同梱のファイル) へのパス入力し、\[**次へ**\] をクリックします。

6.  \[**コマンドを実行しています**\] ページで、\[**完了**\] をクリックします。

必要な Lync Server サービスが確実にすべて開始されるようにするには、\[**展開**\] ページで、\[**ステップ 4: サービスの開始**\] という見出しの下の \[**実行**\] をクリックします。

