﻿---
title: 'Lync Server 2013: ネットワーク パフォーマンスの監視'
TOCTitle: ネットワーク パフォーマンスの監視
ms:assetid: bc3a01da-91eb-4c0c-9598-35e5e46b00f6
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn720923(v=OCS.15)
ms:contentKeyID: 62246649
ms.date: 12/10/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 でのネットワーク パフォーマンスの監視

 

_**トピックの最終更新日:** 2016-12-08_

Lync Server 2013 は、インスタント メッセージング (IM)、音声通話、ビデオ通話を介したユーザー間の通信を可能にするリアルタイム通信テクノロジであり、ネットワークに多くの部分を依存しています。そのため、ユーザーが選択した通信方法に可能な限り最高のエクスペリエンスを提供できるように、ネットワーク パフォーマンスを継続的に監視することが重要です。

ネットワーク パフォーマンスは、次の 2 つのレベルで測定できます。

  - **全体的なネットワーク パフォーマンス**   組織では、このレベルのパフォーマンス測定によりネットワークの "全体像" を把握することができ、通常、これは、サードパーティ製のネットワーク監視システムによって実現されます。これらのシステムでは、ルーターやスイッチなどのネットワーク全体のリモート ネットワーク デバイスからパフォーマンスや容量のデータを取得しており、管理者は、いつでも特定のネットワーク コンポーネントの状態を判断できます。

  - **個々のサーバーのパフォーマンス**   このレベルのパフォーマンス測定は、特定のサーバーに限定されます。特定のパフォーマンスに関する問題のトラブルシューティングを行う場合、容量計画プロセスの一環で各サーバーのパフォーマンスを一定期間計測する場合など、管理者が特定のサーバーのネットワーク パフォーマンスを計測するときに役立ちます。

ネットワークの監視には、以下のセクションで説明するツールを使用できます。

## 全体的なネットワーク パフォーマンスの監視用ツール

## System Center Operations Manager 2012

System Center Operations Manager には、エンド ツー エンドのサービス管理機能があります。カスタマイズと拡張が簡単で、IT 環境全体のサービス レベルを改善できます。このツールを使用して、運用チームと IT 管理チームは、分散した IT サービスの正常性に影響を及ぼす問題を特定し、解決することができます。エンド ツー エンドのサービス管理機能は、Microsoft ベースの環境に限定されるものではありません。Web Services for Management (WS-Management)、簡易ネットワーク管理プロトコル (SNMP)、パートナー ソリューションもサポートされているので、Microsoft 製のオペレーティング システムやハードウェアを実行していないシステムでも、System Center Operations Manager 2012 のサービス監視対象にすることができます。

## System Center Operations Manager 2012 とサードパーティ製ネットワーク管理ソリューション

**EMC Smarts**   EMC Solutions for Operations Manager を使用すると、サービス レベル全体に影響を及ぼす問題を迅速に解決できます。EMC Solutions for Operations Manager では、1 つの統合された自動ソリューションで、IT サービス チェーン全体の管理と監視を行うことができます。パフォーマンスと可用性に関する問題の根本原因を容易に特定し、迅速に解決できるので、影響が軽減され、コストも削減されます。主な利点は次のとおりです。

  - 高度で使いやすい管理機能   戦略的なビジネス価値の実現に集中できます。紛らわしいアラートを手動で並べ替えたり、フィルターしたりする必要はありません。

  - **迅速な解決**   IT の問題解決とビジネス ニーズへの対応が迅速になるので、影響が軽減され、コストも削減されます。

  - **わかりやすい操作**   複数の管理ツール、アプリケーション、端末を組み合わせることで、IT の煩雑さを回避します。

詳細情報:

[Microsoft System Center Operations Manager](http://go.microsoft.com/fwlink/p/?linkid=243651)

[Microsoft System Center Operations Manager 向けソリューション (英語)](http://www.emc.com/collateral/software/data-sheet/h6135-server-manager-ds.pdf)

## サードパーティ製ソリューション

**HP Network Management Center (旧称: HP OpenView)**   [HP Network Management Center](https://h10078.www1.hp.com/cda/hpms/display/main/hpms_content.jsp?zn=bto%26cp=1-11-15-119_4000_100__) の統合的な障害およびパフォーマンス管理機能は、ネットワークの可用性とパフォーマンスを改善させることができます。Network Management Center は、障害、パフォーマンス、構成、変更管理を統合する HP の自動ネットワーク管理ソリューションに含まれています。

**Cisco のネットワーク管理および自動化製品**   Cisco は、CiscoWorks LAN Management Solution、Cisco Network Analysis Module など、運用の効率を改善し、ネットワークのダウンタイムを短縮できるいくつかの管理製品をエンタープライズ向けに提供しています。これらの製品の詳細については、Cisco の Web サイト ([http://www.cisco.com/en/US/products/sw/netmgtsw/index.html](http://www.cisco.com/en/us/products/sw/netmgtsw/index.html)) を参照してください。

簡易ネットワーク管理プロトコル (SNMP)   簡易ネットワーク管理プロトコル (SNMP) は、ネットワーク管理の標準規格であり、TCP/IP ネットワークを管理するための戦略を定義しています。SNMP を使用すると、ネットワークの構成と状態に関する情報をキャプチャし、イベント監視用として指定したコンピューターにその情報を送信することができます。この標準ベースのネットワーク管理プロトコルでは、次のような分散アーキテクチャが使用されます。

  - 複数の管理対象ノードがあり、各ノードには、管理機器へのリモート アクセス機能を持つエージェントという SNMP エンティティがあります。

  - マネージャーと呼ばれる SNMP エンティティが少なくとも 1 つあり、管理アプリケーションを実行して、管理対象要素の監視と制御を行います。管理対象要素とは、ホスト、ルーターなどのデバイスです。管理情報にアクセスすることで、管理対象要素の監視と制御を行います。

  - 管理プロトコルである SNMP は、管理ステーションとエージェント間の管理情報の通信に使用されます。管理情報とは、管理情報ベース (MIB) という仮想情報ストアに格納されている管理対象オブジェクトのコレクションです。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412781.note(OCS.15).gif" title="note" alt="note" />注:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>上記は、サードパーティ製ネットワーク監視ソリューションの例です。ここに記載されたものは絶対的なものではなく、Microsoft は特定のベンダーのソリューションを推奨しません。それぞれの環境に最適なネットワーク監視ソリューションを判断する場合は、ネットワーク サービス プロバイダーや利用しているテクノロジのプロバイダーにご相談ください。</td>
</tr>
</tbody>
</table>


## 個々のサーバーのネットワーク パフォーマンスの監視用ツール

## System Center Operations Manager 2012

System Center Operations Manager 2012 では、管理者は、Windows Server 2012 管理パックを通じて個々のサーバーのネットワーク パフォーマンスを確認できます。Windows Server オペレーティング システム管理パックには "パフォーマンス" 管理パックが含まれており、管理者は、ネットワーク アダプターのパフォーマンスとアダプターの状態を監視できます。

## Windows ネットワーク モニター

サーバー上のリソースの使用状況を収集、表示、分析して、ネットワーク トラフィックを測定します。ネットワーク モニターはネットワーク アクティビティのみを監視します。ネットワーク データをキャプチャ、分析し、このデータをパフォーマンス ログとともに使用することで、ネットワークの使用状況の把握、ネットワークの問題の特定、将来的なネットワークのニーズの予測を行うことができます。

ネットワーク モニター 3.4 の詳細と、ネットワーク モニターのインストールと構成やデータのキャプチャと分析の方法については、ネットワーク モニター 3.3 の概要のセッションを参照してください。また、ネットワーク モニターのブログ (<http://blogs.technet.com/b/netmon/>) も参照してください。

