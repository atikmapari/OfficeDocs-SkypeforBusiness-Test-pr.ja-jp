﻿---
title: ベスト プラクティス アナライザーによるレポートの表示
TOCTitle: ベスト プラクティス アナライザーによるレポートの表示
ms:assetid: 7217a47b-36b1-4923-81ea-df754cff29bb
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg607690(v=OCS.15)
ms:contentKeyID: 48272447
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# ベスト プラクティス アナライザーによるレポートの表示

 

_**トピックの最終更新日:** 2012-09-21_

ベスト プラクティス アナライザーを使用して環境をスキャンする場合は、スキャンの名前を指定します。ベスト プラクティス アナライザーは、スキャンを完了すると、スキャン結果をレポートに格納し、それらをスキャンの名前で保存します。スキャンの完了後、\[**このベスト プラクティス スキャンのレポートを表示する**\] を \[**スキャンが完了しました**\] ページから直接クリックすることで、そのスキャンに対して生成されたレポートを表示できます。後でそのスキャンまたは以前のスキャンからのレポートを表示することもできます。スキャンが実行されたローカル コンピューターでレポートを表示すること、別のコンピューターからスキャン結果をインポートすること、またはスキャン結果をエクスポートしてベスト プラクティス アナライザーがインストールされている別のコンピューターでレポートを表示することができます。

スキャン結果は次の種類のレポートで提示されます。

  - リスト レポート

  - ツリー レポート

  - その他のレポート

これらのレポートには、エラー、警告、およびその他の情報が含まれます。これらの各種類のレポートと問題の詳細については、「[ベスト プラクティス アナライザーで作成したレポートについて](lync-server-2013-understanding-reports-created-by-best-practices-analyzer.md)」を参照してください。

ベスト プラクティス アナライザーで以前に生成されたスキャン結果を表示するには次の手順を使用します。

## 以前のスキャンからのレポートを表示するには

1.  ローカルの User アカウントのメンバーであるアカウントを使用して、ベスト プラクティス アナライザーがインストールされているコンピューターにログオンします。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412781.note(OCS.15).gif" title="note" alt="note" />注:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>ローカルの Administrators グループのメンバーであるアカウントを使用してスキャンの結果を表示することもできますが、適切なユーザー権限とアクセス許可がない限りスキャンを実行できません。詳細については、「<a href="lync-server-2013-group-memberships-and-user-rights-requirements-for-best-practices-analyzer.md">グループ メンバーシップおよびベスト プラクティス アナライザーのユーザー権限</a>」を参照してください。</td>
    </tr>
    </tbody>
    </table>


2.  \[**スタート**\] ボタンをクリックし、\[**すべてのプログラム**\] をポイントして \[**Microsoft Lync Server 2013**\] をクリックし、\[**ベスト プラクティス アナライザー**\] をクリックします。

3.  \[**ようこそ**\] 画面で \[**Select the scan results to view**\] をクリックします。

4.  \[**表示するベスト プラクティス スキャンを選択する**\] ページで、次のいずれかを行います。
    
      - ローカルに保存されたスキャン結果の一覧からレポートを表示するには、スキャンの名前をクリックし、\[**このスキャンのレポートを表示する**\] をクリックします。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg412781.note(OCS.15).gif" title="note" alt="note" />注:</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>ベスト プラクティス アナライザーにより、フォルダー <em>&lt;systemDrive&gt;</em>\Documents and Settings\<em>&lt;user&gt;</em>\Application Data\Microsoft\RtcBPA にあるローカル ファイルの一覧が作成されます。</td>
        </tr>
        </tbody>
        </table>
    
      - 別の場所に保存されているスキャンの結果のレポートを表示するには、\[**スキャンのインポート**\] をクリックし、スキャン結果を含むファイルを特定して \[**開く**\] をクリックします。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg412781.note(OCS.15).gif" title="note" alt="note" />注:</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>このコンピューター上のベスト プラクティス アナライザーのバージョンがインポートされたファイル内のデータの収集に使用されたバージョンと一致しない場合、コンピューター上のツールはインポート後にファイルを再び分析することがあります。</td>
        </tr>
        </tbody>
        </table>


5.  \[**ベスト プラクティス レポートの表示**\] ページで、次のいずれかの操作を行います。
    
      - サーバー コンポーネントによって編成された一覧内のレポートを表示するには、\[**レポートを一覧表示**\] をクリックしてから、\[**すべての問題**\] タブまたは \[**情報項目**\] タブをクリックします。
    
      - 結果の種類別に編成された階層リストとしてレポートを表示するには、\[**ツリー レポート**\] をクリックし、\[**詳細表示**\] タブまたは \[**概要ビュー**\] タブをクリックします。
    
      - 他のレポートを表示するには、\[**Other Reports**\] をクリックします。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412781.note(OCS.15).gif" title="note" alt="note" />注:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>ベスト プラクティス アナライザー レポートとそれらによって識別される問題の詳細については、「<a href="lync-server-2013-viewing-and-working-with-reports-created-by-best-practices-analyzer.md">ベスト プラクティス アナライザーで作成したレポートの表示および作業</a>」および「<a href="lync-server-2013-analyzing-and-resolving-issues-identified-by-best-practices-analyzer.md">ベスト プラクティス アナライザーで識別された問題の分析と解決</a>」を参照してください。</td>
    </tr>
    </tbody>
    </table>
