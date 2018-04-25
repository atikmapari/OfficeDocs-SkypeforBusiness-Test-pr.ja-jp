﻿---
title: 仮想スマート カード用の Windows 8 の構成
TOCTitle: 仮想スマート カード用の Windows 8 の構成
ms:assetid: 4916c167-4ee3-4f3e-b65c-33e588595112
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn308564(v=OCS.15)
ms:contentKeyID: 56270067
ms.date: 12/10/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 仮想スマート カード用の Windows 8 の構成

 

_**トピックの最終更新日:** 2016-12-08_

2 要素認証とスマート カード テクノロジを展開する場合に考慮する必要がある要素の 1 つは、実装コストです。Windows 8には多数の新しいセキュリティ機能があり、最も関心が高い新機能の 1 つは仮想スマート カードのサポートです。

バージョン 1.2 仕様を満たす Trusted Platform Module (TPM) チップを搭載したコンピューターでは、ハードウェアの追加費用をかけずにスマート カード ログオンを活用できるようになりました。詳細については、Windows 8 での仮想スマート カードの使用に関する記事 ([http://go.microsoft.com/fwlink/p/?LinkId=313365](http://go.microsoft.com/fwlink/p/?linkid=313365)) を参照してください。

## Windows 8 を仮想スマート カード用に構成するには

1.  Lync が有効なユーザーの資格情報を使用して Windows 8 コンピューターにログインします。

2.  Windows 8 のスタート画面で、画面の右下隅にカーソルを移動します。

3.  \[**検索**\] オプションを選択し、「**コマンド プロンプト**」を検索します。

4.  \[**コマンド プロンプト**\] を右クリックし、\[**管理者として実行**\] をクリックします。

5.  次のコマンドを実行して、Trusted Platform Module (TPM) 管理コンソールを開きます。
    
        Tpm.msc

6.  TPM 管理コンソールで、TPM 仕様バージョンが 1.2 以上であることを確認します。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412781.note(OCS.15).gif" title="note" alt="note" />注:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>相互運用性のある Trust Platform Module (TPM) が見つからないことを示すダイアログが表示された場合は、相互運用性のある TPM モジュールがコンピューターにインストールされていること、およびシステム BIOS で有効になっていることを確認します。</td>
    </tr>
    </tbody>
    </table>


7.  TPM 管理コンソールを閉じる

8.  コマンド プロンプトで、次のコマンドを使用して新しい仮想スマート カードを作成します。
    
        TpmVscMgr create /name MyVSC /pin default /adminkey random /generate
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412781.note(OCS.15).gif" title="note" alt="note" />注:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>仮想スマート カードを作成するときにカスタム PIN 値を指定するには、代わりに /pin プロンプトを使用します。</td>
    </tr>
    </tbody>
    </table>


9.  コマンド プロンプトから、次のコマンドを実行してコンピューター管理コンソールを開きます。
    
        CompMgmt.msc

10. コンピューター管理コンソールで、\[**デバイス管理**\] をクリックします。

11. \[**スマート カード リーダー**\] を展開します。

12. 新しい仮想スマート カード リーダーが正しく作成されていることを確認します。
