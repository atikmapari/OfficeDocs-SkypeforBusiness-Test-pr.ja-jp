﻿---
title: サイトのアーカイブ オプションの構成
TOCTitle: サイトのアーカイブ オプションの構成
ms:assetid: 59b48fd9-d5fc-40b4-abae-e9cf89ee5573
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ204930(v=OCS.15)
ms:contentKeyID: 48272165
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# サイトのアーカイブ オプションの構成

 

_**トピックの最終更新日:** 2012-10-09_

個々のサイトに適用するアーカイブ オプションを指定できます。それには、それらのサイトの各々について、アーカイブ構成でオプションを作成して構成します。サイト構成は、そのサイト構成で指定されたサイトについてのみ、グローバル構成よりも優先されます。プール構成はサイト構成よりも優先されます。

グローバル構成、サイト構成、およびプール構成の階層など、アーカイブ構成のしくみの詳細については、「計画」、「展開」、または「操作」のドキュメントの「[Lync Server 2013 でのアーカイブのしくみ](lync-server-2013-how-archiving-works.md)」を参照してください。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412781.note(OCS.15).gif" title="note" alt="note" />注:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>アーカイブを有効にする前に、アーカイブ構成で該当するオプションをすべて指定する必要があります。</td>
</tr>
</tbody>
</table>



> [!IMPORTANT]
> アーカイブを有効にするには、内部または外部の通信のアーカイブを管理するためのアーカイブ ポリシーを、グローバル レベル (必要に応じて、サイト レベルおよびユーザー レベル) で指定する必要があります。ユーザー レベルのポリシーを構成する場合は、ユーザー ポリシーをユーザーに割り当てる必要もあります。アーカイブ ポリシーの作成と構成の詳細については、「運用」ドキュメントの「<A href="lync-server-2013-managing-the-archiving-of-internal-and-external-communications.md">Lync Server 2013 での内部通信および外部通信のアーカイブの管理</A>」を参照してください。



## サイト レベルでアーカイブ オプションを構成するには

1.  CsArchivingAdministrator または CsAdministrator の役割に割り当てられているユーザー アカウントから、内部展開の任意のコンピューターにログオンします。

2.  ブラウザー ウィンドウを開き、管理 URL を入力して、Lync Server 2013 コントロール パネルを開きます。Lync Server 2013 コントロール パネルを起動する際に使用できるさまざまな方法の詳細については、「[Lync Server 2013 管理ツールを開く](lync-server-2013-open-lync-server-administrative-tools.md)」を参照してください。

3.  左側のナビゲーション バーで、\[**監視とアーカイブ**\] をクリックし、\[**アーカイブ構成**\] をクリックします。

4.  \[**アーカイブ構成**\] ページで、\[**新規作成**\] をクリックし、\[**サイト構成**\] をクリックします。

5.  \[**サイトの選択**\] で、アーカイブ用に構成するサイトを選択します。

6.  \[**新しいアーカイブ設定**\] の \[**アーカイブ設定**\] ドロップダウン リスト ボックスで、次のいずれかの操作を実行します。
    
      - インスタント メッセージング (IM) セッションのアーカイブだけを有効にするには、\[**IM セッションをアーカイブする**\] をクリックします。
    
      - IM セッションと会議の両方のアーカイブを有効にするには、\[**IM および Web 会議セッションをアーカイブする**\] をクリックします。
    
      - ポリシーのアーカイブを無効にするには、\[**アーカイブを無効にする**\] をクリックします。

7.  \[**新しいアーカイブ設定**\] で、次の操作も実行します。
    
      - アーカイブを使用できない場合にアクティビティを禁止するには、\[**アーカイブ失敗時はインスタント メッセージング (IM) または Web 会議セッションを禁止する**\] チェック ボックスをオンにします。
    
      - Microsoft Exchange Server を使用してアーカーブ データを格納するには、\[**Microsoft Exchange 統合**\] チェック ボックスをオンにします。
    
      - データの削除を有効にするには、\[**アーカイブ データの削除を有効にする**\] チェック ボックスをオンにし、次のどちらかの操作を実行します。
        
          - 一定の日数が経過した後に削除されるよう指定するには、\[**最大日数が経過したエクスポートおよび保存済みアーカイブ データを削除する**\] をクリックして、日数を指定します。
        
          - エクスポートされたアーカイブ データに削除対象を限定するには、\[**エクスポートされたアーカイブ データのみを削除する**\] をクリックします。

8.  \[**確定**\] をクリックします。

