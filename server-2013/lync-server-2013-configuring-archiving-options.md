﻿---
title: アーカイブ オプションの構成
TOCTitle: アーカイブ オプションの構成
ms:assetid: b2f7f74d-e1ad-494e-9d46-5eb0efe5fb29
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ205182(v=OCS.15)
ms:contentKeyID: 48273312
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# アーカイブ オプションの構成

 

_**トピックの最終更新日:** 2012-10-10_

Lync Server 2013 コントロール パネルでアーカイブ構成を使用して、アーカイブの実装方法を指定します。これには、次のアーカイブ構成が含まれます。

  - Lync Server 2013 を展開するときに既定で作成されるグローバル構成。

  - 特定のサイトまたはプールに対するアーカイブの実装方法を指定するために作成して使用できる、オプションのサイトレベルおよびプールレベルのポリシー。

アーカイブ構成は、最初はアーカイブの展開時にセットアップしますが、展開後に変更、追加、および削除できます。Lync Server 2013 コントロール パネルで、\[**アーカイブおよび監視**\] グループの \[**アーカイブ構成**\] ページを使用して、構成をグローバル レベル、サイト レベル、およびプール レベルで管理できます。指定できるオプションやアーカイブ構成の階層など、アーカイブ構成の実装方法の詳細については、「計画」のドキュメント、「展開」のドキュメント、または「操作」のドキュメントの「[Lync Server 2013 でのアーカイブのしくみ](lync-server-2013-how-archiving-works.md)」を参照してください。展開後に構成を管理する方法の詳細については、「操作」のドキュメントの「[Lync Server 2013 での組織、サイト、およびプールのアーカイブ構成オプションの管理](lync-server-2013-managing-archiving-configuration-options-for-your-organization-sites-and-pools.md)」を参照してください。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412781.note(OCS.15).gif" title="note" alt="note" />注:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>アーカイブを使用するには、アーカイブ ポリシーを構成し、Lync Server 2013 に所属するユーザーに対して、内部通信、外部通信、またはその両方についてアーカイブを有効にするかどうかを指定する必要があります。既定では、アーカイブは内部通信および外部通信のどちらに対しても有効になっていません。ポリシーでアーカイブを有効にする前に、このセクションの説明に従って、展開に対して、また必要に応じて特定のサイトやプールに対して、適切なアーカイブ構成を指定する必要があります。アーカイブの有効化の詳細については、「展開」のドキュメントの「<a href="lync-server-2013-configuring-and-assigning-archiving-policies.md">アーカイブ ポリシーの構成と割り当て</a>」を参照してください。<br />
展開内のすべてのユーザーについて Microsoft Exchange 統合を使用しない場合、内部通信、外部通信、またはその両方のアーカイブを有効にするかどうかを指定するためのアーカイブ ポリシーを構成する必要があります。Lync Server 2013 アーカイブ データベースを使用する場合のデータのアーカイブでは、内部通信についても外部通信についてもアーカイブは既定では有効ではありません。ポリシーでアーカイブを有効にする前に、このセクションの説明に従って、展開および必要に応じて特定のサイトやプールに対して適切なアーカイブ構成を指定する必要があります。Lync Server 2013 アーカイブ データベースで使用するためのアーカイブの有効化の詳細については、「展開」のドキュメントの「<a href="lync-server-2013-configuring-and-assigning-archiving-policies.md">アーカイブ ポリシーの構成と割り当て</a>」を参照してください。</td>
</tr>
</tbody>
</table>


## このセクション中

  - [グローバル レベルでのアーカイブ オプションの構成](lync-server-2013-configuring-archiving-options-at-the-global-level.md)

  - [サイトのアーカイブ オプションの構成](lync-server-2013-configuring-archiving-options-for-a-site.md)

  - [プールのアーカイブ オプションの構成](lync-server-2013-configuring-archiving-options-for-a-pool.md)

