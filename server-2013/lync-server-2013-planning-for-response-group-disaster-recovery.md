﻿---
title: 'Lync Server 2013: 応答グループの障害復旧の計画'
TOCTitle: 応答グループの障害復旧の計画
ms:assetid: 14e0f5dc-77cd-42cd-a9c9-4d0da38fb1cf
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ204699(v=OCS.15)
ms:contentKeyID: 48271353
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server 2013 での応答グループの障害復旧の計画

 

_**トピックの最終更新日:** 2015-03-09_

このセクションでは、応答グループの障害復旧を準備する方法について説明し、障害復旧プロセスの概要を示します。

## 応答グループの障害復旧の準備

障害復旧手順を準備および実施する場合、次の点を考慮してください。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412781.note(OCS.15).gif" title="note" alt="note" />注:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>共存環境では、このドキュメントで説明する障害復旧手順がサポートされるのは Lync Server 2013 の応答グループのみです。</td>
</tr>
</tbody>
</table>


  - 障害復旧の計画は、処理能力の計画時に行います。障害復旧の処理能力については、ペアにしたプールのそれぞれのプールで、両方のプールのすべての応答グループの負荷を処理できる必要があります。応答グループの処理能力の計画の詳細については、「[Lync Server 2013 の応答グループの処理能力の計画](lync-server-2013-capacity-planning-for-response-group.md)」を参照してください。

  - このドキュメントで説明しているエクスポート手順を使用して、応答グループ アプリケーションを展開したすべての フロント エンド プールのすべての応答グループ構成の定期的なバックアップを行います。詳細については、「[Lync Server 2013 の応答グループの障害復旧手順](lync-server-2013-response-group-disaster-recovery-procedures.md)」を参照してください。そのバックアップは安全な場所に保管します。

  - 録音ファイル、保留音ファイルなど、応答グループ アプリケーションに使用したすべてのオリジナル オーディオ ファイルのバックアップを別途保管します。そのバックアップ ファイルは安全な場所に保管します。

  - Lync Server 2013 の障害復旧では、すべての 応答グループ設定が展開内で固有の名前を持つ必要があります。この要件は、ワークフロー、キュー、エージェント グループ、休日セット、および営業時間に適用されます。プライマリ プールとバックアップ プールがまだアクティブで、フェールオーバー手順の開始が必要になる前に、この要件が満たされていることを確認する必要があります。バックアップ プールに応答グループ データをインポートするときに名前の競合が発生するとインポートは失敗します。インポートとフェールオーバー手順を完了するには、バックアップ プールの応答グループ オブジェクトの名前を変更して名前の競合を解決するか、**Import-CsRgsConfiguration** コマンドレットに -ResolveNameConflicts パラメーターを使用することによって応答グループ オブジェクトに一意の識別番号を追加する方法で競合を自動解決する必要があります。

  - 一般に、毎日バックアップを行うことをお勧めしますが、変更が多い場合は、より頻度の高いバックアップのスケジュールが必要になることもあります。障害発生時に失われる情報の量は、バックアップの頻度および変更の頻度と量に左右されます。

  - 障害またはフェールオーバー処理が発生する前に、応答グループをバックアップ プールにインポートしておくことができます。応答グループを事前にインポートしておくと、通話がバックアップ プールにルーティングされたとき即座にバックアップ プールに Lync Server 応答グループ サービスを復元できるので、ダウンタイムを短縮できます。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412781.note(OCS.15).gif" title="note" alt="note" />注:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>非アクティブ プールに所属するエージェントには、フェールオーバーが完了するまで、応答グループ アプリケーションからは到達できません。その間、応答グループ アプリケーションでは、そのエージェントが使用不可であるかのように通話が処理されます。</td>
    </tr>
    </tbody>
    </table>


## 応答グループの障害復旧プロセス

障害が発生した場合、次の回復アプローチで応答グループを回復できます。

  - バックアップ プールにフェールオーバーし、次に元のプールにフェールバックします。

  - バックアップ プールにフェールオーバーし、異なる完全修飾ドメイン名 (FQDN) を持つ新しいプールを作成し、その新しいプールに応答グループをインポートします。

障害復旧のフェールオーバー フェーズ中、応答グループは (使用できない) プライマリ プールとバックアップ プールという複数のプールに存在します。どちらのプールでも応答グループの名前と所有者 (プライマリ プール) は同じですが、その親は異なります。

異なる FQDN を持つ新しいプールを作成して回復する場合、応答グループをインポートするときにその所有者として新しいプールを割り当てる必要があります。**Import-CsRgsConfiguration** コマンドレットに -OverwriteOwner パラメーターを指定して所有権を明示的に割り当て直さない限り、応答グループの所有権は引き続き元のプールにあります。

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412781.note(OCS.15).gif" title="note" alt="note" />注:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>回復中にプールを構築し直した場合 (応答グループ データベースが空の場合) も、同じ FQDN を使用するかどうかに関係なく、-OverwriteOwner パラメーターを使用する必要があります。プールを構築し直さなかった場合には -OverwriteOwner パラメーターを使用する必要はありませんが、応答グループをプライマリ プールにインポートして戻す場合はこのパラメーターを使用することが許容されます。</td>
</tr>
</tbody>
</table>


アプリケーション レベルの 応答グループの構成設定は、プールごとに 1 セットずつのみ定義できます。このような設定として、既定の保留音の構成、既定の保留音オーディオ ファイル、エージェントかけ直し猶予期間、呼び出しコンテキストの構成があります。これらの構成設定を表示するには、**Get-CsRgsConfiguration** コマンドレットを実行します。**Get-CsRgsConfiguration** コマンドレットの詳細については、「[Get-CsRgsConfiguration](get-csrgsconfiguration.md)」を参照してください。

これらのアプリケーション レベル設定は、**Import-CsRgsConfiguration** コマンドレットに -ReplaceExistingSettings パラメーターを指定するとプールから別のプールへ転送できますが、それによって転送先プールの設定はオーバーライドされます。


> [!IMPORTANT]
> 設定を別のプールへ転送する場合のこの制約は、アプリケーション レベル設定と既定の保留音オーディオ ファイルのみに適用されます。エージェント グループ、キュー、ワークフロー、営業時間、および休日セットには適用されません。



障害時にバックアップ プールのアプリケーション レベル設定を置き換えないようにすると、プライマリ プールを回復できない場合にプライマリ プールのアプリケーション レベル設定は失われます。回復時にプライマリ プールを置き換えるために新しいプールを作成する必要がある場合、それが同じ FQDN を持つか異なる FQDN を持つかに関係なく、元のアプリケーション レベル設定は回復できません。この場合、新しいプールにこれらの設定を構成し、保留音オーディオ ファイルを含める必要があります。

障害時に **Import-CsRgsConfiguration** コマンドレットを使用してプライマリ プールからバックアップ プールにアプリケーション レベル設定を転送する場合は、その後の回復時に、プライマリ プールからバックアップ プールに転送したときと同じ方法でバックアップ プールから新しいプールに設定を転送できます。

応答グループを回復するステップの概要を次の表に示します。

これらのステップを実行する方法の詳細については、「[Lync Server 2013 の応答グループの障害復旧手順](lync-server-2013-response-group-disaster-recovery-procedures.md)」を参照してください。

### 応答グループの障害復旧ステップ

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>フェーズ</th>
<th>ステップ</th>
<th>必要なグループおよび役割</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>停止前</p></td>
<td><p>ルーチンごとに、<strong>Export-CsRgsConfiguration</strong> コマンドレットを実行して、応答グループ アプリケーションが展開されているすべての フロント エンド プールのすべての 応答グループ構成のバックアップを作成します。</p></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsResponseGroupAdministrator</p></td>
</tr>
<tr class="even">
<td><p>停止中</p></td>
<td><p><strong>Import-CsRgsConfiguration</strong> コマンドレットを実行して、バックアップ済みの Lync Server 応答グループ サービス構成をプライマリ プールからバックアップ プールへインポートします。</p>
<div class="alert">
<table>
<thead>
<tr class="header">
<th><img src="images/Gg412781.note(OCS.15).gif" title="note" alt="note" />注:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>プライマリ プールのアプリケーション レベル 応答グループ設定でバックアップ プールの設定を置き換えるには、-ReplaceExistingSettings パラメーターを使用します。プライマリ プールのアプリケーション レベル設定をバックアップ プールに転送しないと、プライマリ プールを回復できない場合にプライマリ プールの設定は失われます。</td>
</tr>
</tbody>
</table>

</div></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsResponseGroupAdministrator</p></td>
</tr>
<tr class="odd">
<td><p>インポート後</p></td>
<td><p>応答グループ のコマンドレットに -ShowAll パラメーター (すべての応答グループを表示する場合) または -Owner パラメーター (インポートされた応答グループのみを表示する場合) を指定して実行し、すべての応答グループ構成がバックアップ プールにインポートされたことを確認します。</p>
<div class="alert">

> [!IMPORTANT]
> -ShowAll パラメーターも -Owner パラメーターも指定しない場合、バックアップ プールにインポートされた応答グループは、コマンドレットから返される結果に表示されません。


</div>
<p>次のコマンドレットを実行します。</p>
<ul>
<li><p><strong>Get-CsRgsWorkflow</strong></p></li>
<li><p><strong>Get-CsRgsQueue</strong></p></li>
<li><p><strong>Get-CsRgsAgentGroup</strong></p></li>
<li><p><strong>Get-CsRgsHoursOfBusiness</strong></p></li>
<li><p><strong>Get-CsRgsHolidaySet</strong></p></li>
</ul></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsResponseGroupAdministrator</p></td>
</tr>
<tr class="even">
<td><p>フェールオーバー後</p></td>
<td><ul>
<li><p>バックアップ プールにインポートした応答グループへテスト通話を行い、通話が適切に処理されることを確認します。</p></li>
<li><p>すべての公式エージェントは、バックアップ プール上の公式グループに再度サインインする必要があります。</p></li>
<li><p>構成の変更を管理します。</p>
<p>バックアップ プールにインポートされるかバックアップ プールに所有されているためにバックアップ プールに含まれる応答グループは、障害時にも通常どおりに変更できます。</p>
<div class="alert">

> [!IMPORTANT]
> バックアップ プールにインポートした応答グループを管理するには、Lync Server 管理シェルを使用する必要があります。そのような応答グループは、バックアップ プール内にある間に Lync Server コントロール パネルを使用して管理することはできません。


</div></li>
</ul></td>
<td><p>該当なし</p></td>
</tr>
<tr class="odd">
<td><p>回復後、フェールバック前</p></td>
<td><p>-Source パラメーターにバックアップ プール、-Owner パラメーターにプライマリ プールを指定して <strong>Export-CsRgsConfiguration</strong> コマンドレットを実行し、プライマリ プールに所有される応答グループをバックアップ プールからエクスポートします。</p></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsResponseGroupAdministrator</p></td>
</tr>
<tr class="even">
<td><p>フェールバック後</p></td>
<td><ul>
<li><p><strong>Import-CsRgsConfiguration</strong> コマンドレットを実行して、応答グループをプライマリ プールにインポートして戻します。</p>
<div class="alert">
<table>
<thead>
<tr class="header">
<th><img src="images/Gg412781.note(OCS.15).gif" title="note" alt="note" />注:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>プライマリ プールを回復できない場合に新しいプールを展開してそれを置き換えるには、-ReplaceExistingSettings パラメーターを使用してバックアップ プールのアプリケーション レベル設定を新しいプールに転送します。バックアップ プールから設定を転送しないと、新しいプールでは既定の設定が使用されます。</td>
</tr>
</tbody>
</table>

</div></li>
<li><p>次のコマンドレットに -ShowAll パラメーター (すべての応答グループを表示する場合) または -Owner パラメーター (インポートされた応答グループのみを表示する場合) を指定して実行し、すべての応答グループ構成がプライマリ プールに正常にインポートして戻されたことを確認します。</p>
<ul>
<li><p><strong>Get-CsRgsWorkflow</strong></p></li>
<li><p><strong>Get-CsRgsQueue</strong></p></li>
<li><p><strong>Get-CsRgsAgentGroup</strong></p></li>
<li><p><strong>Get-CsRgsHoursOfBusiness</strong></p></li>
<li><p><strong>Get-CsRgsHolidaySet</strong></p></li>
</ul></li>
<li><p>プライマリ プールにインポートして戻した応答グループへテスト通話を行い、通話が適切に処理されることを確認します。</p></li>
<li><p>必要に応じて、バックアップ プールで -RemoveExportedConfiguration パラメーターを指定して <strong>Export-CsRgsConfiguration</strong> コマンドレットを実行して、プライマリ プールに所有されている応答グループをバックアップ プールから削除します。</p></li>
</ul></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsResponseGroupAdministrator</p></td>
</tr>
</tbody>
</table>

