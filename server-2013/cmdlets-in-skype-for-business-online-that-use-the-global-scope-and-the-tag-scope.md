﻿---
title: グローバル スコープとタグ スコープを使用するコマンドレット
TOCTitle: グローバル スコープとタグ スコープを使用するコマンドレット
ms:assetid: 1e2bc055-8a72-425e-967b-e253add7018c
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362774(v=OCS.15)
ms:contentKeyID: 56270054
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# グローバル スコープとタグ スコープを使用するコマンドレット

 

_**トピックの最終更新日:** 2015-06-22_

Skype for Business Online では、ポリシーはグローバル スコープとタグ スコープ (またはユーザーごとのスコープ) のいずれかで構成できます。**Get-Cs** コマンドレットを使用する場合はスコープまたは ID を指定する必要はありません。パラメーターを指定せずにこれらのコマンドレットのいずれかを呼び出すと、関連するすべての項目が返されます。たとえば、次のコマンドは、すべての外部アクセス ポリシーに関する情報を返します。

    Get-CsExternalAccessPolicy

返されるデータを制限する場合、含める必要があるのは Identity パラメーターまたは Filter パラメーターのみです。たとえば、グローバル ポリシーのみを返すには、次のコマンドを使用します。

    Get-CsExternalAccessPolicy -Identity "global"

ID "RedmondAccessPolicy" が含まれるユーザーごとのポリシーを返すには、次のコマンドを使用します。

    Get-CsExternalAccessPolicy -Identity "RedmondAccessPolicy"

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412781.note(OCS.15).gif" title="note" alt="note" />注:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ユーザーごとのポリシーを参照する場合、タグ <strong>プレフィクス</strong>は省略可能です。プレフィクスが含まれる次の構文も有効です。<br />
Get-CsExternalAccessPolicy –Identity &quot;tag:RedmondAccessPolicy&quot;</td>
</tr>
</tbody>
</table>


グローバル ポリシーを除くすべてのポリシー (つまり、すべてのユーザーごとのポリシー) を返すには、次のコマンドを使用します。

    Get-CsExternalAccessPolicy -Filter "tag:*"

次のコマンドレットは、グローバル スコープとユーザーごと (タグ) スコープの両方に対して機能します。

  - [Get-CsClientPolicy](get-csclientpolicy.md)

  - [Get-CsConferencingPolicy](get-csconferencingpolicy.md)

  - [Get-CsDialPlan](get-csdialplan.md)

  - [Get-CsExternalAccessPolicy](get-csexternalaccesspolicy.md)

  - [Get-CsHostedVoicemailPolicy](get-cshostedvoicemailpolicy.md)

  - [Get-CsPresencePolicy](get-cspresencepolicy.md)

  - [Get-CsVoicePolicy](get-csvoicepolicy.md)

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412781.note(OCS.15).gif" title="note" alt="note" />注:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>ダイヤル プランは、名前とは異なり、機能的にはポリシーです。たとえば、ダイヤル プランという用語はダイヤル ポリシーの代わりに使用されていますが、これは以前のバージョンの Lync Server で使用された用語を保持するためです。</td>
</tr>
</tbody>
</table>


## 関連項目

#### 概念

[ID、スコープ、およびテナント](identities-scopes-and-tenants-in-skype-for-business-online.md)  
[Lync Online のコマンドレット](the-skype-for-business-online-cmdlets.md)

