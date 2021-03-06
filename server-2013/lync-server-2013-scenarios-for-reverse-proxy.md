﻿---
title: 'Lync Server 2013: リバース プロキシのシナリオ'
TOCTitle: リバース プロキシのシナリオ
ms:assetid: 13108f59-a660-4ff1-8404-079d1cb646f2
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ204691(v=OCS.15)
ms:contentKeyID: 48271329
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 のリバース プロキシのシナリオ

 

_**トピックの最終更新日:** 2013-01-21_

会議およびダイヤルイン用の簡易 URL、アドレス帳、会議コンテンツ、配布リストの拡張、モビリティ サービスなど、サービスおよびリソースへのアクセスを提供するには、Lync Server 2013 でリバース プロキシが必要です。Lync Server 2013 のリバース プロキシの一般的なシナリオとして、外部クライアント (デスクトップ クライアント、Lync Web App クライアントなど) が ディレクターまたは フロント エンド サーバーの外部 Web サービスにアクセスできるようにすることがあります。

**リバース プロキシと外部 Web サービス**

![リバース プロキシおよび外部 Web サービス](images/JJ204932.13142405-d5c9-45b7-a8b7-a8c89f09c97c(OCS.15).jpg "リバース プロキシおよび外部  Web サービス")

計画フェーズ中に、Lync Server 2013 展開のリバース プロキシの要件を定義します。リバース プロキシを使用すると、以下の外部クライアントの機能にアクセスできます。

  - Microsoft Lync 2013 デスクトップ クライアント

  - Microsoft Lync Web App

  - Microsoft Lync Mobile

  - Lync Windows ストア アプリ

Lync Server 2013 展開を計画するときに、Lync Server 2013 の実際の要件をリバース プロキシの機能にマップします。

1.  外部クライアントはポート TCP 443 でリバース プロキシに接続し、Secure Socket Layer (SSL) またはトランスポート層セキュリティ (TLS) を使用します。Microsoft Lync Mobile クライアントはポート TCP 80 で接続できます (ただし、Lync 自動検出サービスへの初期接続の実行時に、管理者が適切なドメイン ネーム システム (DNS) CNAME (またはエイリアス) レコードを構成しており、この通信が暗号化されないことを受け入れる場合のみ)。

2.  Lync Server 2013 の外部 Web サービス (フロント エンド サーバーまたは ディレクターに展開される) は、ポート TCP 4443 でのリバース プロキシからの接続を期待し、接続が SSL/TLS で行われることを期待します。
    

    > [!IMPORTANT]
    > 外部 Web サービス用の既定のリッスン ポートとして、HTTP トラフィック用に TCP 8080、HTTPS トラフィック用に TCP 4443 をお勧めします。トポロジ ビルダーでは、既定を上書きし、外部 Web サービス用の独自のリッスン ポートを定義できます。リバース プロキシが外部 Web サービスと通信を行い、外部クライアントがリバース プロキシと通信を行うことに注意してください。外部クライアントはポート TCP 443 でリバース プロキシと通信しますが、リバース プロキシが外部 Web サービスと通信するポートを再定義できます。トポロジ ビルダーのオプションを使用し、Web サービス用の既定のリッスン ポートを上書きすることで、ユーザーのインフラストラクチャで発生する場合があるリッスン ポートの競合を解決できます。



3.  Lync Server 2013 の外部 Web サービスは、クライアントが使用を試みているサービスと Web サーバー ディレクトリを特定するために、クライアントからの変更されていないホスト ヘッダーを期待します。要求はリバース プロキシから送信されたように見えます。

4.  外部 Web サービスは、定義済みの Web サーバー仮想ディレクトリ (vDir) を使用して、要求されたサービスをクライアントに提供します。外部的に識別可能な特定の Web サービスを以下に示します。
    
      - "Meet" vDir: Web 会議用
    
      - "Dialin" vDir: 電話アクセスおよび電話会議用
    
      - "Autodiscover" vDir: Lync Windows ストア アプリ、Lync Mobile、およびデスクトップ クライアントの Lync 2013 用。Lync Server 2013 の自動検出は DNS 名 "lyncdiscover" によって認識されます。
    
      - 定義されていないサービスは、外部 Web サービスへの直接呼び出しによって外部クライアントによりアクセスされます。たとえば、配布グループ拡張 (DLX) とアドレス帳サービス (ABS) は、外部 Web サービスおよび関連付けられた vDir への直接呼び出しによってアクセスされます。クライアントは vDir への実際のパスを認識し、その情報に基づいて URL (Uniform Record Locator) を構成します。クライアントは、`https://externalweb.contoso.com/abs/handler` のような URL を使用してアドレス帳サービスにアクセスします。
    
      - Office Web Apps サーバー: 会議が Lync Server トポロジの一部として定義および構成されている場合
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg412781.note(OCS.15).gif" title="note" alt="note" />注:</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Office Web Apps サーバー は独立した役割サーバーであり、外部 Web サービスの一部として構成されません。このサーバーはクライアント アクセス用に別途公開されます。</td>
        </tr>
        </tbody>
        </table>


5.  サービスごとに SSL ブリッジを定義します。外部ポート TCP 443 を外部 Web サービス ポートの TCP 4443 にマップします。暗号化されていない HTTP のために、ポート TCP 80 を外部 Web サービス ポートの TCP 8080 にマップします。

6.  Web サーバー リソースを公開するようにリバース プロキシ リスナーを計画します

7.  提供するサービスに基づいてリバース プロキシ用の証明書を要求して構成します。適切なサブジェクトの別名を使用して構成した場合、この証明書を、リバース プロキシ サーバー上に構成されたすべてのリスナーで共有できます。

リバース プロキシの展開を計画するために使用できるリソースを次に示します。

  - [Lync Server 2013 のデータの収集](lync-server-2013-data-collection.md)

  - [証明書の概要 - Lync Server 2013 リバース プロキシ](lync-server-2013-certificate-summary-reverse-proxy.md)

  - [ポートの概要 - Lync Server 2013 のリバース プロキシ](lync-server-2013-port-summary-reverse-proxy.md)

  - [DNS の概要 - Lync Server 2013 でのリバース プロキシ](lync-server-2013-dns-summary-reverse-proxy.md)

