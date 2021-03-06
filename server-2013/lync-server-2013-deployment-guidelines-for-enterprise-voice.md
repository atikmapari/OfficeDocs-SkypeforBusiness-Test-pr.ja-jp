﻿---
title: 'Lync Server 2013: エンタープライズ VoIP の展開ガイドライン'
TOCTitle: エンタープライズ VoIP の展開ガイドライン
ms:assetid: 8985bd93-7613-4cef-9c89-51df6049ed9b
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398694(v=OCS.15)
ms:contentKeyID: 48272806
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 のエンタープライズ VoIP の展開ガイドライン

 

_**トピックの最終更新日:** 2012-09-21_

ここでは、Lync Server 2013 および エンタープライズ VoIP のワークロードの展開を計画するときに考慮する前提条件とその他のガイドラインについて説明します。

## 展開に関する前提条件

エンタープライズ VoIP を最適に展開できるように、IT インフラストラクチャ、ネットワーク、およびシステムが、次の前提条件を満たしていることを確認します。

  - Lync Server 2013 Standard Edition または Enterprise Edition がネットワーク上にインストールされ、実行されていること。

  - 境界ネットワーク内にすべてのエッジ サーバー (アクセス エッジ サービス、音声ビデオ エッジ サービス、Web 会議エッジ サービス、およびリバース プロキシなどを備えたエッジ サーバー) が展開され、実行されていること。

  - 1 人以上のユーザーが作成され、Lync Server に対して有効化されていること。

  - Microsoft Exchange Server 2007 Service Pack 1 (SP1) 以上、または Microsoft Exchange Server 2010 がインストールされていること。Exchange ユニファイド メッセージング (UM) を Lync Server と統合し、優れた通話と通話ログ情報をクライアント エンドポイントに提供するには、これらのいずれかが必要です。

  - 一意の主要電話番号が指定され、正規化されており、エンタープライズ VoIP に対して有効化する各ユーザーの **msRTCSIP-line** 属性にコピーされていること。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412781.note(OCS.15).gif" title="note" alt="note" />注:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Lync Server では、E.164 番号に加え、Direct Inward Dialing (DID) 以外の番号がサポートされています。DID 以外の番号は、<strong>&lt;E.164&gt;;ext=&lt;extension&gt;</strong> 形式で、または数値の文字列で表記できます。数値の文字列を使用する場合は、個人用内線番号が企業内で一意である必要があります。たとえば、個人用内線番号が 1001 の場合は、<strong>+1425550100;ext=1001</strong> または <strong>1001</strong> と表記できます。<strong>1001</strong> と表記すると、その個人用内線番号が企業内で一意であると想定されます。</td>
    </tr>
    </tbody>
    </table>


  - エンタープライズ VoIP を展開する管理者が RTCUniversalServerAdmins グループのメンバーであること。

  - 少なくとも Office Communicator 2007 が正常に展開されていること。このリリースの新しい機能を使用するには、Lync 2013 を展開します。

  - マイクロソフトまたはサードパーティの CA (証明機関) インフラストラクチャのいずれかを使用して、MKI (Managed key infrastructure) が展開され、構成されていること。

  - 仲介サーバーをインストールする各コンピューターの要件は次のとおりです。
    
      - ドメインのメンバー サーバーであり、Active Directory ドメイン サービス 用に準備されていること。Active Directory ドメイン サービス の準備手順については、「展開」のドキュメントの「[Lync Server 2013 用の Active Directory ドメイン サービスの準備](lync-server-2013-preparing-active-directory-domain-services.md)」を参照してください。
    
      - 次のいずれかのオペレーティング システムを実行していること。
        
          -   
            64 ビット版の Windows Server 2008 Standard オペレーティング システム
        
          -   
            64 ビット版の Windows Server 2008 Enterprise オペレーティング システム

  - 公衆交換電話網 (PSTN) または構内交換機 (PBX) への接続に時分割多重 (TDM) 接続を使用する場合は、1 つ以上の PSTN ゲートウェイを展開できること (接続に SIP トランクを使用する場合、PSTN ゲートウェイは不要です)。

## 電力、ネットワーク、または電話サービスの停止

電力、ネットワーク、または電話サービスの停止、中断、障害などが発生すると、Lync Server の音声通話、インスタント メッセージング、プレゼンスなどの機能や、Lync Server に接続されるデバイスが正常に機能しなくなることがあります。

## エンタープライズ VoIP が、サーバーの可用性と VoIP クライアントおよびハードウェアの正常動作に依存する

Lync Server による音声通信は、サーバー ソフトウェアの可用性と、サーバー ソフトウェアに接続する VoIP クライアントまたはハードウェア電話デバイスの正常な動作に依存します。

## 緊急サービスへの代替アクセス手段

VoIP クライアントのインストール先 (Lync クライアントを実行するコンピューターや Lync Phone Edition デバイスなど) には、停電、ネットワーク接続の不具合、電話サービスの停止など、Lync Server、Lync、または Lync Phone Edition デバイスの動作を阻害する可能性のある問題が発生した場合に備え、ユーザーが緊急サービス (911 や 999 など) に連絡するためのバックアップ オプションを組み込むことをお勧めします。このような代替オプションには、標準公衆交換電話網回線に接続された電話、携帯電話などが含まれます。

## 緊急呼び出しと複数回線電話システム

複数回線電話システム (MLTS) を使用する場合は、緊急サービスに電話をかけたときに (911、999 など、緊急アクセス番号をダイヤルする場合など)、MLTS が発信者の電話番号、内線番号、または住所を該当する緊急サービスに知らせることを義務付ける米国の州や国の法令または他の国/地域の法令が適用される場合があります。このリリースでは、発信者の住所を緊急サービス プロバイダーに提供するように Lync Server を構成できます。この方法は、「[Lync Server 2013 での緊急サービス (E9-1-1) の計画](lync-server-2013-planning-for-emergency-services-e9-1-1.md)」に記載されています。Lync Server、Lync クライアント、および Lync Phone Edition デバイスの購入者が、自己の責任で MLTS 法令に準拠することが必要となります。

