﻿---
title: 'Lync Server 2013: 通話受付管理の組織要件の収集の例'
TOCTitle: '例: 通話受付管理の組織要件の収集'
ms:assetid: 3363ac53-b7c4-4a59-aea1-b2f3ee016ae1
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg425827(v=OCS.15)
ms:contentKeyID: 48271692
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 例: Lync Server 2013 での通話受付管理の組織要件の収集

 

_**トピックの最終更新日:** 2015-03-09_

この例では、通話受付管理 (CAC) の計画および実装方法を示します。これは大まかに次の作業で構成されます。

1.  すべてのネットワーク ハブおよびバックボーン (*ネットワーク地域*とも呼ばれます) を特定します。

2.  各ネットワーク地域で CAC を管理する Lync Server 中央サイトを特定します。

3.  各ネットワーク地域に接続される *ネットワーク サイト* を特定および定義します。

4.  各ネットワーク サイトで WAN への接続に帯域幅の制限がある場合、WAN 接続の帯域幅容量と、該当する場合は、ネットワーク管理者が Lync Server メディア トラフィックに設定した帯域幅制限を説明します。WAN への接続に帯域幅の制限がないサイトは含める必要はありません。

5.  ネットワークの各サブネットをネットワーク サイトに関連付けます。

6.  ネットワーク地域間のリンクをマップします。各リンクで、帯域幅容量と、ネットワーク管理者が Lync Server メディア トラフィックに設定した帯域幅制限を説明します。

7.  ネットワーク地域のすべてのペア間のルートを定義します。

## 必要な情報の収集

通話受付管理の準備を行うには、次の手順で示されている情報を収集します。

1.  ネットワーク地域を特定します。 ネットワーク地域とは、ネットワーク バックボーンまたはネットワーク ハブを示します。
    
    ネットワーク バックボーンまたはネットワーク ハブとは、異なる LAN またはサブネット間の情報交換用パスを提供して、ネットワークの様々な部分を相互接続するコンピューター ネットワーク インフラストラクチャの一部です。 バックボーンは、小規模ロケーションから地理的に広範囲な地域まで、様々なネットワークを繋ぐことができます。 通常、バックボーンの処理能力はバックボーンに接続するネットワークの処理能力よりも高くなっています。
    
    このトポロジ例では、3 つのネットワーク地域が存在します。 北アメリカ、EMEA、および APAC。 ネットワーク地域にはネットワーク サイトのコレクションが含まれます。 ネットワーク管理者と協力して、組織のネットワーク地域を定義します。

2.  各ネットワーク地域が関連付けられている中央サイトを特定します。中央サイトには少なくとも 1 台の フロント エンド サーバーが含まれ、ネットワーク地域の WAN 接続を通過するすべてのメディア トラフィックの CAC を管理する、Lync Server が展開されています。
    
    **3 つのネットワーク地域に分けられたエンタープライズ ネットワークの例**
    
    ![3 つのネットワーク地域が含まれるネットワーク トポロジの例](images/Gg425827.08937347-250f-488f-ba5f-c256e6afcd8b(OCS.15).jpg "3 つのネットワーク地域が含まれるネットワーク トポロジの例")  
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412781.note(OCS.15).gif" title="note" alt="note" />注:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Multiprotocol Label Switching (MPLS) ネットワークは、それぞれの地理的な場所が対応するネットワーク サイトを有する、ネットワーク地域として表される必要があります。詳細については、「計画」のドキュメントの「<a href="lync-server-2013-call-admission-control-on-an-mpls-network.md">Lync Server 2013 による MPLS ネットワーク上の通話受付管理</a>」を参照してください。</td>
    </tr>
    </tbody>
    </table>
    
    前述のネットワーク トポロジの例では、3 つのネットワーク地域が存在し、それぞれが CAC を管理する Lync Server 中央サイトを有しています。ネットワーク地域の適切な中央サイトは、地理的な近さによって選択されます。メディア トラフィックはネットワーク地域内で最も重くなるため、所有権が地理的な近さで決まることで自己完結型となり、その他の中央サイトが使用できなくなった場合でも、機能し続けます。
    
    この例では、シカゴと呼ばれる Lync Server 展開が北アメリカ地域の中央サイトです。
    
    北アメリカのすべての Lync ユーザーは、シカゴ展開のサーバーに所属します。次の表に 3 つすべてのネットワーク地域の中央サイトを示します。
    
    ### ネットワーク地域と関連付けられた中央サイト
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>ネットワーク地域</th>
    <th>中央サイト</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>北アメリカ</p></td>
    <td><p>シカゴ</p></td>
    </tr>
    <tr class="even">
    <td><p>EMEA</p></td>
    <td><p>ロンドン</p></td>
    </tr>
    <tr class="odd">
    <td><p>APAC</p></td>
    <td><p>北京</p></td>
    </tr>
    </tbody>
    </table>
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412781.note(OCS.15).gif" title="note" alt="note" />注:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Lync Server トポロジに応じて、同じサイトを複数のネットワーク地域の中央サイトに割り当てることも可能です。</td>
    </tr>
    </tbody>
    </table>


3.  それぞれのネットワーク地域で、帯域幅に制限がない WAN 接続を有するネットワーク サイト (オフィスまたは場所) すべてを特定します。 これらのサイトは帯域幅の制限がないため、CAC 帯域幅ポリシーを適用する必要はありません。
    
    次の表に示されている例では、3 つのネットワークサイトには帯域幅の制限がある WAN リンクがありません: ニューヨーク、シカゴ、およびデトロイト。
    
    ### WAN 帯域幅による制限がないネットワーク サイト
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>ネットワーク サイト</th>
    <th>ネットワーク地域</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>ニューヨーク</p></td>
    <td><p>北アメリカ</p></td>
    </tr>
    <tr class="even">
    <td><p>シカゴ</p></td>
    <td><p>北アメリカ</p></td>
    </tr>
    <tr class="odd">
    <td><p>デトロイト</p></td>
    <td><p>北アメリカ</p></td>
    </tr>
    </tbody>
    </table>


4.  それぞれのネットワーク地域で、帯域幅の制限がある WAN リンクを介してネットワーク地域に接続しているすべてのネットワーク サイトを特定します。
    
    音声およびビデオの品質を確実なものにできるように、これらの帯域幅の制限があるネットワーク サイトは、WAN を監視し、ネットワーク地域への、およびネットワーク地域からのメディア (音声またはビデオ) トラフィック フローを制限する CAC 帯域幅ポリシーを使用することをお勧めします。
    
    次の表に示されている例では、WAN 帯域幅による制限がある 3 つのネットワーク サイトが存在します。 ポートランド、リノ、およびアルバカーキ。
    
    ### WAN 帯域幅による制限があるネットワーク サイト
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>ネットワーク サイト</th>
    <th>ネットワーク地域</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>アルバカーキ</p></td>
    <td><p>北アメリカ</p></td>
    </tr>
    <tr class="even">
    <td><p>リノ</p></td>
    <td><p>北アメリカ</p></td>
    </tr>
    <tr class="odd">
    <td><p>ポートランド</p></td>
    <td><p>北アメリカ</p></td>
    </tr>
    </tbody>
    </table>
    
    **帯域幅の制限がない 3 つのネットワーク サイト (シカゴ、ニューヨーク、デトロイト) および WAN 帯域幅の制限がある 3 つのネットワーク サイト (ポートランド、リノ、アルバカーキ) を持つ CAC ネットワーク地域、北アメリカ**
    
    ![WAN 帯域幅による制限があるネットワーク サイトの例](images/Gg425827.d9d1f231-db4d-4dd7-8fbc-eb0b6d1e705d(OCS.15).jpg "WAN 帯域幅による制限があるネットワーク サイトの例")  

5.  帯域幅の制限がある WAN リンクに対して、次の項目を決定します。
    
      - すべての同時音声セッションに対して設定したい全体的な帯域幅制限。新しい音声セッションがこの制限を超過するような場合は、Lync Server はこのセッションを開始させません。
    
      - それぞれ個別の音声セッションに対して設定したい帯域幅制限。既定の CAC 帯域幅制限は 175 kbps ですが、管理者はこれを変更することができます。
    
      - すべての同時ビデオ セッションに対して設定したい全体的な帯域幅制限。新しいビデオ セッションがこの制限を超過するような場合は、Lync Server はこのセッションを開始させません。
    
      - それぞれ個別のビデオ セッションに対して設定したい帯域幅制限。 既定の CAC 帯域幅制限は 700 kbps ですが、管理者はこれを変更することができます。
    
    ### WAN 帯域幅制限情報 (帯域幅は kbps で表示) とネットワーク サイト
    
    <table style="width:100%;">
    <colgroup>
    <col style="width: 14%" />
    <col style="width: 14%" />
    <col style="width: 14%" />
    <col style="width: 14%" />
    <col style="width: 14%" />
    <col style="width: 14%" />
    <col style="width: 14%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>ネットワーク サイト</th>
    <th>ネットワーク地域</th>
    <th>BW 制限</th>
    <th>音声制限</th>
    <th>音声セッション制限</th>
    <th>ビデオ制限</th>
    <th>ビデオ セッション制限</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>アルバカーキ</p></td>
    <td><p>北アメリカ</p></td>
    <td><p>5,000</p></td>
    <td><p>2,000</p></td>
    <td><p>175</p></td>
    <td><p>1,400</p></td>
    <td><p>700</p></td>
    </tr>
    <tr class="even">
    <td><p>リノ</p></td>
    <td><p>北アメリカ</p></td>
    <td><p>10,000</p></td>
    <td><p>4,000</p></td>
    <td><p>175</p></td>
    <td><p>2,800</p></td>
    <td><p>700</p></td>
    </tr>
    <tr class="odd">
    <td><p>ポートランド</p></td>
    <td><p>北アメリカ</p></td>
    <td><p>5,000</p></td>
    <td><p>4,000</p></td>
    <td><p>175</p></td>
    <td><p>2,800</p></td>
    <td><p>700</p></td>
    </tr>
    <tr class="even">
    <td><p>ニューヨーク</p></td>
    <td><p>北アメリカ</p></td>
    <td><p>(制限なし)</p></td>
    <td><p>(制限なし)</p></td>
    <td><p>(制限なし)</p></td>
    <td><p>(制限なし)</p></td>
    <td><p>(制限なし)</p></td>
    </tr>
    <tr class="odd">
    <td><p>シカゴ</p></td>
    <td><p>北アメリカ</p></td>
    <td><p>(制限なし)</p></td>
    <td><p>(制限なし)</p></td>
    <td><p>(制限なし)</p></td>
    <td><p>(制限なし)</p></td>
    <td><p>(制限なし)</p></td>
    </tr>
    <tr class="even">
    <td><p>デトロイト</p></td>
    <td><p>北アメリカ</p></td>
    <td><p>(制限なし)</p></td>
    <td><p>(制限なし)</p></td>
    <td><p>(制限なし)</p></td>
    <td><p>(制限なし)</p></td>
    <td><p>(制限なし)</p></td>
    </tr>
    </tbody>
    </table>


6.  ネットワークのすべてのサブネットに対し、関連付けられるネットワーク サイトを指定します。
    

    > [!IMPORTANT]
    > すべてのサブネットは、たとえネットワーク サイトに帯域幅の制限がない場合でも、ネットワーク サイトに関連付けられる必要があります。 これは、通話受付管理はサブネット情報を使用してエンドポイントがどのネットワーク サイトに配置されているかを判断するためです。 セッションにおける両者の場所が決定した時、通話受付管理は通話を確立するのに十分な帯域幅があるかどうかを判断します。 帯域幅の制限がないリンクを介してセッションが確立した時、通知が生成されます。<BR>音声ビデオ エッジ サーバーを展開する場合、各エッジ サーバーのパブリック IP アドレスは、エッジ サーバーが展開されたネットワーク サイトに関連付けられる必要があります。 音声ビデオ エッジ サーバーのそれぞれのパブリック IP アドレスは、32 サブネットマスクのサブネットとして、ネットワーク構成に追加される必要があります。 パブリック IP アドレスの詳細については、「計画」のドキュメントの「<A href="lync-server-2013-determine-external-a-v-firewall-and-port-requirements.md">Lync Server 2013 の外部の音声ビデオ ファイアウォールおよびポートの要件を決定する</A>」を参照してください。

    
    <table>
    <colgroup>
    <col style="width: 100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412781.note(OCS.15).gif" title="note" alt="note" />注:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>主要状態インジケーター (KHI) 通知が発行され、ネットワークに存在している IP アドレスの一覧を指定します。ここで指定される一覧は、サブネットと関連付けられていないか、IP アドレスを含むサブネットがネットワーク サイトと関連付けられていません。 この通知は 8 時間に 1 回しか発行されません。 関連する通知の情報および例は以下の通りです。<br />
    <strong>ソース :</strong> CS 帯域幅ポリシー サービス (コア)<br />
    <strong>イベント番号 :</strong> 36034<br />
    <strong>レベル :</strong> 2<br />
    <strong>概要 :</strong> 次の IP アドレスのサブネット: &lt;IP アドレスのリスト&gt; は構成されていないか、またはサブネットがネットワークサイトに関連付けられていません。<br />
    <strong>原因 :</strong> 対応する IP アドレスのサブネットがネットワーク構成設定にないか、サブネットがネットワーク サイトに関連付けられていません。<br />
    <strong>解決方法 :</strong> 前述の IP アドレスのリストに対応するサブネットをネットワーク構成設定に追加し、すべてのサブネットをネットワーク サイトに関連付けます。<br />
    たとえば、通知に表示された IP アドレス リストが 10.121.248.226 および 10.121.249.20 であった場合、これらの IP アドレスがサブネットに関連付けられていないか、または関連付けられているサブネットがネットワーク サイトに属していないかのどちらかになります。10.121.248.0/24 および 10.121.249.0/24 がこれらのアドレスに対応するサブネットである場合、次の手順でこの問題を解決することができます。
    <ol>
    <li><p>IP アドレス 10.121.248.226 が 10.121.248.0/24 サブネットに関連付けられていること、および IP アドレス 10.121.249.20 が 10.121.249.0/24 サブネットに関連付けられていることを確認します。</p></li>
    <li><p>10.121.248.0/24 および 10.121.249.0/24 サブネットがそれぞれネットワーク サイトに関連付けられていることを確認します。</p></li>
    </ol></td>
    </tr>
    </tbody>
    </table>
    
    ### ネットワーク サイトと関連付けられたサブネット (帯域幅は kbps で表示)
    
    <table>
    <colgroup>
    <col style="width: 12%" />
    <col style="width: 12%" />
    <col style="width: 12%" />
    <col style="width: 12%" />
    <col style="width: 12%" />
    <col style="width: 12%" />
    <col style="width: 12%" />
    <col style="width: 12%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>ネットワーク サイト</th>
    <th>ネットワーク地域</th>
    <th>BW 制限</th>
    <th>音声制限</th>
    <th>音声セッション制限</th>
    <th>ビデオ制限</th>
    <th>ビデオ セッション制限</th>
    <th>サブネット</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>アルバカーキ</p></td>
    <td><p>北アメリカ</p></td>
    <td><p>5,000</p></td>
    <td><p>2,000</p></td>
    <td><p>175</p></td>
    <td><p>1,400</p></td>
    <td><p>700</p></td>
    <td><p>172.29.79.0/23, 157.57.215.0/25, 172.29.90.0/23, 172.29.80.0/24</p></td>
    </tr>
    <tr class="even">
    <td><p>リノ</p></td>
    <td><p>北アメリカ</p></td>
    <td><p>10,000</p></td>
    <td><p>4,000</p></td>
    <td><p>175</p></td>
    <td><p>2,800</p></td>
    <td><p>700</p></td>
    <td><p>157.57.210.0/23, 172.28.151.128/25</p></td>
    </tr>
    <tr class="odd">
    <td><p>ポートランド</p></td>
    <td><p>北アメリカ</p></td>
    <td><p>5,000</p></td>
    <td><p>4,000</p></td>
    <td><p>175</p></td>
    <td><p>2,800</p></td>
    <td><p>700</p></td>
    <td><p>172.29.77.0/24 10.71.108.0/24, 157.57.208.0/23</p></td>
    </tr>
    <tr class="even">
    <td><p>ニューヨーク</p></td>
    <td><p>北アメリカ</p></td>
    <td><p>(制限なし)</p></td>
    <td><p>(制限なし)</p></td>
    <td><p>(制限なし)</p></td>
    <td><p>(制限なし)</p></td>
    <td><p>(制限なし)</p></td>
    <td><p>172.29.80.0/23, 157.57.216.0/25, 172.29.91.0/23, 172.29.81.0/24</p></td>
    </tr>
    <tr class="odd">
    <td><p>シカゴ</p></td>
    <td><p>北アメリカ</p></td>
    <td><p>(制限なし)</p></td>
    <td><p>(制限なし)</p></td>
    <td><p>(制限なし)</p></td>
    <td><p>(制限なし)</p></td>
    <td><p>(制限なし)</p></td>
    <td><p>157.57.211.0/23, 172.28.152.128/25</p></td>
    </tr>
    <tr class="even">
    <td><p>デトロイト</p></td>
    <td><p>北アメリカ</p></td>
    <td><p>(制限なし)</p></td>
    <td><p>(制限なし)</p></td>
    <td><p>(制限なし)</p></td>
    <td><p>(制限なし)</p></td>
    <td><p>(制限なし)</p></td>
    <td><p>172.29.78.0/24 10.71.109.0/24, 157.57.209.0/23</p></td>
    </tr>
    </tbody>
    </table>


7.  Lync Server 通話受付管理では、ネットワーク地域間の接続は*地域リンク*と呼ばれます。各地域リンクに対し、ネットワーク サイトでしたように、次の項目を決定します。
    
      - すべての同時音声セッションに対して設定したい全体的な帯域幅制限。新しい音声セッションがこの制限を超過するような場合は、Lync Server はこのセッションを開始させません。
    
      - それぞれ個別の音声セッションに対して設定したい帯域幅制限。既定の CAC 帯域幅制限は 175 kbps ですが、管理者はこれを変更することができます。
    
      - すべての同時ビデオ セッションに対して設定したい全体的な帯域幅制限。新しいビデオ セッションがこの制限を超過するような場合は、Lync Server はこのセッションを開始させません。
    
      - それぞれ個別のビデオ セッションに対して設定したい帯域幅制限。 既定の CAC 帯域幅制限は 700 kbps ですが、管理者はこれを変更することができます。
    
    **関連付けられた帯域幅制限とネットワーク地域リンク**
    
    ![3 つの地域間の制限の例](images/Gg425827.25259afa-ee7c-4d26-bc41-92ba9cb56dec(OCS.15).jpg "3 つの地域間の制限の例")  
    
    ### 地域リンク帯域幅情報 (帯域幅は kbps で表示)
    
    <table>
    <colgroup>
    <col style="width: 12%" />
    <col style="width: 12%" />
    <col style="width: 12%" />
    <col style="width: 12%" />
    <col style="width: 12%" />
    <col style="width: 12%" />
    <col style="width: 12%" />
    <col style="width: 12%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>地域リンク名</th>
    <th>第 1 の地域</th>
    <th>第 2 の地域</th>
    <th>BW 制限</th>
    <th>音声制限</th>
    <th>音声セッション制限</th>
    <th>ビデオ制限</th>
    <th>ビデオ セッション制限</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>NA-EMEA-LINK</p></td>
    <td><p>北アメリカ</p></td>
    <td><p>EMEA</p></td>
    <td><p>50,000</p></td>
    <td><p>20,000</p></td>
    <td><p>175</p></td>
    <td><p>14,000</p></td>
    <td><p>700</p></td>
    </tr>
    <tr class="even">
    <td><p>EMEA-APAC-LINK</p></td>
    <td><p>EMEA</p></td>
    <td><p>APAC</p></td>
    <td><p>25,000</p></td>
    <td><p>10,000</p></td>
    <td><p>175</p></td>
    <td><p>7,000</p></td>
    <td><p>700</p></td>
    </tr>
    </tbody>
    </table>


8.  ネットワーク地域のすべてのペア間のルートを定義します。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412781.note(OCS.15).gif" title="note" alt="note" />注:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>北アメリカと APAC の間のルートには、両者を直接接続する地域リンクがないため、2 つのリンクが必要になります。</td>
    </tr>
    </tbody>
    </table>
    
    ### 地域ルート
    
    <table>
    <colgroup>
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>地域ルート名</th>
    <th>第 1 の地域</th>
    <th>第 2 の地域</th>
    <th>地域リンク</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>NA-EMEA-ROUTE</p></td>
    <td><p>北アメリカ</p></td>
    <td><p>EMEA</p></td>
    <td><p>NA-EMEA-LINK</p></td>
    </tr>
    <tr class="even">
    <td><p>EMEA-APAC-ROUTE</p></td>
    <td><p>EMEA</p></td>
    <td><p>APAC</p></td>
    <td><p>EMEA-APAC-LINK</p></td>
    </tr>
    <tr class="odd">
    <td><p>NA-APAC-ROUTE</p></td>
    <td><p>北アメリカ</p></td>
    <td><p>APAC</p></td>
    <td><p>NA-EMEA-LINK, EMEA-APAC-LINK</p></td>
    </tr>
    </tbody>
    </table>


9.  単一のリンク (*サイト間* リンクと呼ばれます) で直接接続されているネットワーク サイトのペアに対して、次の項目を決定します。
    
      - すべての同時音声セッションに対して設定したい全体的な帯域幅制限。新しい音声セッションがこの制限を超過するような場合は、Lync Server はこのセッションを開始させません。
    
      - それぞれ個別の音声セッションに対して設定したい帯域幅制限。既定の CAC 帯域幅制限は 175 kbps ですが、管理者はこれを変更することができます。
    
      - すべての同時ビデオ セッションに対して設定したい全体的な帯域幅制限。新しいビデオ セッションがこの制限を超過するような場合は、Lync Server はこのセッションを開始させません。
    
      - それぞれ個別のビデオ セッションに対して設定したい帯域幅制限。 既定の CAC 帯域幅制限は 700 kbps ですが、管理者はこれを変更することができます。
    
    **リノとアルバカーキ間のサイト間リンクに対する帯域幅処理能力および帯域幅制限を示すCAC ネットワーク地域、北アメリカ**
    
    ![WAN 帯域幅による制限があるネットワーク サイトの例](images/Gg425827.063e5e1d-b6c8-4e8c-98db-c227c78f671d(OCS.15).jpg "WAN 帯域幅による制限があるネットワーク サイトの例")  
    
    ### 2 つのネットワーク サイト間のサイト間リンクの帯域幅情報 (帯域幅は kbps で表示)
    
    <table>
    <colgroup>
    <col style="width: 12%" />
    <col style="width: 12%" />
    <col style="width: 12%" />
    <col style="width: 12%" />
    <col style="width: 12%" />
    <col style="width: 12%" />
    <col style="width: 12%" />
    <col style="width: 12%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>サイト間リンク名</th>
    <th>第 1 のサイト</th>
    <th>第 2 のサイト</th>
    <th>BW 制限</th>
    <th>音声制限</th>
    <th>音声セッション制限</th>
    <th>ビデオ制限</th>
    <th>ビデオ セッション制限</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Reno-Albu-Intersite-Link</p></td>
    <td><p>リノ</p></td>
    <td><p>アルバカーキ</p></td>
    <td><p>20,000</p></td>
    <td><p>12,000</p></td>
    <td><p>175</p></td>
    <td><p>5,000</p></td>
    <td><p>700</p></td>
    </tr>
    </tbody>
    </table>


## 次のステップ

必要な情報を収集した後、Lync Server 管理シェルまたは Lync Server コントロール パネルのどちらかを使用して CAC 展開を実行することができます。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412781.note(OCS.15).gif" title="note" alt="note" />注:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lync Server コントロール パネルを使用すればネットワーク構成タスクの大部分を行うことができますが、サブネットおよびサイト間リンクを作成するには、Lync Server 管理シェルを使用する必要があります。詳細については、<strong>New-CsNetworkSubnet</strong> および <strong>New-CsNetworkIntersitePolicy</strong> コマンドレットの「Lync Server 管理シェル」のドキュメントを参照してください。</td>
</tr>
</tbody>
</table>

