﻿---
title: 'Lync Server 2013: DNS の概要 - 単一統合エッジ (NAT によるプライベート IP アドレスを使用)'
TOCTitle: DNS の概要 - 単一統合エッジ (NAT によるプライベート IP アドレスを使用)
ms:assetid: a7e5d792-f397-45e5-af85-20d0f4bf405f
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg412787(v=OCS.15)
ms:contentKeyID: 48273208
ms.date: 03/09/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# DNS の概要 - Lync Server 2013 の単一統合エッジ (NAT によるプライベート IP アドレスを使用)

 

_**トピックの最終更新日:** 2017-03-09_

Lync Server 2013 へのリモート アクセスに対する DNS レコード要件は、証明書やポートに対する要件と比べかなり簡単です。また、 Lync 2013 を実行するクライアントの構成方法およびフェデレーションを有効にするかどうかに応じて、多くのレコードがオプションになります。

Lync 2013 の DNS 要件の詳細については、「[Lync Server 2013 の DNS の要件を確認する](lync-server-2013-determine-dns-requirements.md)」を参照してください。

Lync 2013 を実行するクライアントの自動構成の詳細については、「[Lync Server 2013 の DNS の要件を確認する](lync-server-2013-determine-dns-requirements.md)」の「スプリットブレイン DNS なしの自動構成」を参照してください。

次の表に、単一統合エッジ トポロジの図に示される単一統合エッジ トポロジのサポートに必要な DNS レコードの概要を示します。特定の DNS レコードは Lync 2013 および Lync 2010 クライアントの自動構成に対してのみ必要であることに注意してください。 Lync クライアントの構成にグループ ポリシー オブジェクト (GPO) の使用を計画している場合は、関連付けられたレコードは不要です。

## 重要: エッジ サーバーのネットワーク アダプターの要件

ルーティングの問題を回避するには、 エッジ サーバーに 2 つ以上のネットワーク アダプターを搭載し、デフォルト ゲートウェイが外部インターフェイスに関連付けられたネットワーク アダプター上にのみ設定する必要があります。たとえば、「[Lync Server 2013 におけるプライベート IP アドレスと NAT を用いた単一統合エッジ](lync-server-2013-single-consolidated-edge-with-private-ip-addresses-and-nat.md)」の単一統合エッジ トポロジの図のように、デフォルト ゲートウェイは外部ファイアウォール (10.45.16.1) をポイントします。

エッジ サーバーでは、2 つのネットワーク アダプターを次のように構成できます。

  - **ネットワーク アダプター 1 (内部インターフェイス)**
    
    172.25.33.10 が割り当てられた内部インターフェイス。
    
    デフォルト ゲートウェイは定義されません。
    
    エッジの内部インターフェイスを含むネットワークから、 Lync Server 2013 を実行するサーバーまたは Lync Server 2013 クライアントを含むネットワークへのルート (たとえば、172.25.33.0 から 192.168.10.0 まで) があることを確認します。

  - **ネットワーク アダプター 2 (外部インターフェイス)**
    
    このネットワーク アダプターには、3 つのプライベート IP アドレスが割り当てられます (たとえば、アクセス エッジの 10.45.16.10、Web 会議エッジの 10.45.16.20、音声ビデオ エッジの 10.45.16.30)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412781.note(OCS.15).gif" title="note" alt="note" />注:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>お勧めはできませんが、3 つのエッジ サービス インターフェイスすべてに 1 つの IP アドレスを使用できます。これによって IP アドレスを節約できますが、サービスごとに異なるポート番号が必要です。既定のポート番号は 443/TCP で、リモート ファイアウォールの大部分がトラフィックを許可します。ポートの値を (たとえば) アクセス エッジは 5061/TCP、Web 会議エッジは 444/TCP、AV エッジは 443/TCP に変更すると、5061/TCP および 444/TCP 経由のトラフィックを許可していないファイアウォールの外側にいるリモート ユーザーに問題が生じる可能性があります。また、3 つの異なる IP アドレスを使用する方が、IP アドレスでフィルター処理できるので、トラブルシューティングが簡単です。</td>
    </tr>
    </tbody>
    </table>
    
    アクセス エッジ IP アドレスは、デフォルト ゲートウェイを統合ルーター (10.45.16.1) に設定した、プライマリ アドレスです。
    
    Web 会議エッジ IP アドレスと音声ビデオ エッジ IP アドレスはセカンダリ アドレスです。


> [!TIP]
> 1 つ目の方法は、2 つのネットワーク アダプターを備えた エッジ サーバーを構成することです。もう 1 つの方法は、 エッジ サーバーの内部側用に 1 つのネットワーク アダプターを使用し、外部側用に 3 つのネットワーク アダプターを使用することです。この方法の主なメリットは、 エッジ サーバーサービスごとにネットワーク アダプターが異なるため、トラブルシューティングが必要な場合にデータをより正確に収集できる可能性があることです。



### 単一統合エッジ (NAT によるプライベート IP アドレスを使用) で必要な DNS レコード (例)

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>場所/種類/ポート</th>
<th>FQDN/DNS レコード</th>
<th>IP アドレス/FQDN</th>
<th>マッピング先/コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>外部 DNS/A</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>131.107.155.10</p></td>
<td><p>アクセス エッジ外部インターフェイス (Contoso)。すべての SIP ドメインと Lync が有効なユーザーについて必要なだけ繰り返します。</p></td>
</tr>
<tr class="even">
<td><p>外部 DNS/A</p></td>
<td><p>webcon.contoso.com</p></td>
<td><p>131.107.155.20</p></td>
<td><p>Web 会議エッジ外部インターフェイス</p></td>
</tr>
<tr class="odd">
<td><p>外部 DNS/A</p></td>
<td><p>av.contoso.com</p></td>
<td><p>131.107.155.30</p></td>
<td><p>音声ビデオ エッジ外部インターフェイス</p></td>
</tr>
<tr class="even">
<td><p>外部 DNS/SRV/443</p></td>
<td><p>sip._tls.contoso.com</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>アクセス エッジ外部インターフェイス。 Lync 2013 クライアントと Lync 2010 クライアントの自動構成が外部で機能するために必要。必要に応じて、Lync が有効なユーザーを持つすべての SIP ドメインに対してこの手順を繰り返します。</p></td>
</tr>
<tr class="odd">
<td><p>外部 DNS/SRV/5061</p></td>
<td><p>sipfederationtls._tcp.contoso.com</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>&quot;許可済み SIP ドメイン&quot; (以前のリリース１では拡張フェデレーションと呼ばれました) という名前のフェデレーション パートナーの自動 DNS 検出に必要</p></td>
</tr>
<tr class="even">
<td><p>内部 DNS/A</p></td>
<td><p>lsedge.contoso.net</p></td>
<td><p>172.25.33.10</p></td>
<td><p>統合エッジ内部インターフェイス</p></td>
</tr>
</tbody>
</table>



> [!IMPORTANT]
> スプリットブレイン DNS を使用しない場合、前の表に示されるレコードは、そのレコードが存在する必要があるゾーンを強調するため、"<EM>.net</EM>" または "<EM>.com</EM>" のいずれかの拡張子が付いています。スプリットブレイン DNS を使用する場合は、すべてのレコードが同じ "<EM>.com</EM>" ゾーンに存在します。ただし、内部または外部 DNS ゾーン バージョンの区別だけは存在します。詳細については、「<A href="lync-server-2013-determine-dns-requirements.md">Lync Server 2013 の DNS の要件を確認する</A>」を参照してください。



## フェデレーションに必要なレコード


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>場所/種類/ポート</th>
<th>FQDN</th>
<th>IP アドレス/FQDN ホスト レコード</th>
<th>マッピング先/コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>外部 DNS/SRV/5061</p></td>
<td><p>sipfederationtls._tcp.contoso.com</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>&quot;許可済み SIP ドメイン&quot; (以前のリリースでは拡張フェデレーションと呼ばれました) という名前の、他のフェデレーション パートナーへのフェデレーションの自動 DNS 検出に必要な SIP アドレス エッジ外部インターフェイス。すべての SIP ドメインと Lync が有効なユーザーについて必要なだけ繰り返します。</p>
<div class="alert">

> [!IMPORTANT]
> この SRV レコードは、モビリティおよび Push Notification Clearing House に必要です。


</div></td>
</tr>
</tbody>
</table>


## DNS の概要 - パブリック インスタント メッセージング接続


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>場所/種類/ポート</th>
<th>FQDN/DNS レコード</th>
<th>IP アドレス/FQDN</th>
<th>マッピング先/コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>外部 DNS/A</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>アクセス エッジ サービス インターフェイス</p></td>
<td><p>アクセス エッジ外部インターフェイス (Contoso)。すべての SIP ドメインと Lync が有効なユーザーについて必要なだけ繰り返します。</p></td>
</tr>
</tbody>
</table>


## XMPP の DNS の概要


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>場所/種類/ポート</th>
<th>FQDN</th>
<th>IP アドレス/FQDN ホスト レコード</th>
<th>マッピング先/コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>外部 DNS/SRV/5269</p></td>
<td><p>_xmpp-server._tcp.contoso.com</p></td>
<td><p>xmpp.contoso.com</p></td>
<td><p>アクセス エッジ サービスまたは エッジ プールの XMPP プロキシの外部インターフェイス。グローバル ポリシー、ユーザーが配置されているサイトのサイト ポリシー、または Lync が有効なユーザーに適用されているユーザー ポリシーによる外部アクセス ポリシーの構成を通じて XMPP の連絡先との連絡が許可されている、すべての内部 SIP ドメインと Lync が有効なユーザーについて必要なだけ繰り返します。許可された XMPP ドメインは、XMPP フェデレーション パートナー ポリシーでも構成されている必要があります。詳細については、「<strong>関連項目</strong>」のトピックを参照してください。</p></td>
</tr>
<tr class="even">
<td><p>外部 DNS/A</p></td>
<td><p>xmpp.contoso.com (例)</p></td>
<td><p>XMPP プロキシをホストする エッジ サーバーまたは エッジ プールの アクセス エッジ サービスの IP アドレス</p></td>
<td><p>XMPP プロキシ サービスをホストする アクセス エッジ サービスまたは エッジ プールを参照します。通常、作成する SRV レコードは、このホスト (A または AAAA) レコードを参照します。</p></td>
</tr>
</tbody>
</table>

