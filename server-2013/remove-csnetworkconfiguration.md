﻿---
title: Remove-CsNetworkConfiguration
TOCTitle: Remove-CsNetworkConfiguration
ms:assetid: d6945015-67f7-4f04-87ae-7cb977650d96
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398938(v=OCS.15)
ms:contentKeyID: 48273708
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsNetworkConfiguration

 

_**トピックの最終更新日:** 2015-03-09_

Resets all the network configuration settings for a Lync Server deployment to the default values. This deletes an entire call admission control (CAC) deployment and related E9-1-1 configuration. このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Remove-CsNetworkConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Examples

## EXAMPLE 1

This example removes all CAC, location, E9-1-1 network, and media bypass settings. The Confirm parameter is used so you’ll be prompted to verify you really want to do this before everything is deleted.

    Remove-CsNetworkConfiguration -Identity Global -Confirm

## Detailed Description

WARNING: Running this cmdlet will delete an entire network configuration, including CAC, E9-1-1 regions and sites, and media bypass.

Who can run this cmdlet: By default, members of the following groups are authorized to run the **Remove-CsNetworkConfiguration** cmdlet locally: RTCUniversalServerAdmins. To return a list of all the role-based access control (RBAC) roles this cmdlet has been assigned to (including any custom RBAC roles you have created yourself), run the following command from the Windows PowerShell prompt:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsNetworkConfiguration"}

## パラメーター


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Parameter</th>
<th>Required</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Required</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>This will always be Global.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。 It is recommended that you always use this parameter with this cmdlet.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Suppresses any confirmation prompts that would otherwise be displayed before making changes.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>実際にコマンドを実行しなくてもコマンドの実行結果がわかります。</p></td>
</tr>
</tbody>
</table>


## Input Types

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkConfigurationSettings object. Accepts pipelined input of a network configuration object.

## Return Types

This cmdlet does not return an object. It removes an object of type Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkConfigurationSettings object.

## 関連項目

#### その他のリソース

[Set-CsNetworkConfiguration](set-csnetworkconfiguration.md)  
[Get-CsNetworkConfiguration](get-csnetworkconfiguration.md)  
[Get-CsNetworkSite](get-csnetworksite.md)  
[Get-CsNetworkRegionLink](get-csnetworkregionlink.md)  
[Get-CsNetworkInterSitePolicy](get-csnetworkintersitepolicy.md)  
[Get-CsNetworkInterRegionRoute](get-csnetworkinterregionroute.md)  
[Get-CsNetworkRegion](get-csnetworkregion.md)  
[Get-CsNetworkSubnet](get-csnetworksubnet.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)

