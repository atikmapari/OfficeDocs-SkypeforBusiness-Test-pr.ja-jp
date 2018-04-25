﻿---
title: 'Lync Server 2013: 場所に基づくルーティングの概要'
TOCTitle: 場所に基づくルーティングの概要
ms:assetid: 4aa494bd-0d66-4335-b9e8-f758d44a7202
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ994032(v=OCS.15)
ms:contentKeyID: 52056587
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 の場所に基づくルーティングの概要

 

_**トピックの最終更新日:** 2013-02-21_

場所に基づいたルーティングでは、国内および国際 PSTN 通話のルーティングを変更する新しいルール セットを導入して、課金回避を防止します。場所に基づいたルーティングによって、これらのルールを特定の地域、ゲートウェイ、ユーザー群のみに柔軟に適用できます。

次のシナリオでは、場所に基づいたルーティングによって強制できる制限の主な種類を説明します。

  - 発信 - 場所に基づいたルーティングでは、発信者と同じ地域にある PSTN ゲートウェイから発信が行われるように強制し、発信者と別の地域にある PSTN ゲートウェイから発信されないようにすることで、PSTN の課金回避を防ぐことができます。

  - 着信 - 場所に基づいたルーティングでは、着信をルーティングする PSTN ゲートウェイが発信先の Lync ユーザーと同じ地域にない場合、PSTN 着信によって Lync エンドポイントが呼び出されないようにすることができます。

  - 不明な地域 - 場所に基づいたルーティングでは、場所を特定できないユーザー (インターネットから接続していたり、不明な地域にいたりするリモート ユーザーなど) との間の PSTN 発着信が制限されます。

  - 国際的地域 - 場所に基づいたルーティングでは、ユーザーの場所でローカルなゲートウェイが見つからない場合、国際 PSTN ゲートウェイ経由の発信のルーティングが強制されます。

## 関連項目

#### その他のリソース

[Lync Server 2013 での場所に基づくルーティングの計画](lync-server-2013-planning-for-location-based-routing.md)
