---
title: PowerShell:アプリのバックアップを復元する
description: Azure PowerShell を使用して App Service のデプロイと管理を自動化する方法について説明します。 このサンプルでは、アプリをバックアップから復元する方法を紹介しています。
author: msangapu-msft
tags: azure-service-management
ms.assetid: a2a27d94-d378-4c17-a6a9-ae1e69dc4a72
ms.topic: sample
ms.date: 11/21/2018
ms.author: msangapu
ms.custom: mvc, seodec18
ms.openlocfilehash: a10a451bff73c081d9b0c95c494acb8b2051bd84
ms.sourcegitcommit: 0947111b263015136bca0e6ec5a8c570b3f700ff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/24/2020
ms.locfileid: "80057740"
---
# <a name="restore-a-web-app-from-a-backup-using-azure-powershell"></a>Azure PowerShell を使用して Web アプリをバックアップから復元する

このサンプル スクリプトでは、既存の Web アプリから以前に完了したバックアップを取得し、コンテンツを上書きすることによってアプリを復元します。 

必要に応じて、[Azure PowerShell ガイド](/powershell/azure/overview)の手順に従って Azure PowerShell をインストールし、`Connect-AzAccount` を実行して、Azure との接続を作成します。 

## <a name="sample-script"></a>サンプル スクリプト

[!INCLUDE [updated-for-az](../../../includes/updated-for-az.md)]

[!code-azurepowershell-interactive[main](../../../powershell_scripts/app-service/backup-restore/backup-restore.ps1?highlight=1-2 "Restore a web app from a backup")]

## <a name="clean-up-deployment"></a>デプロイのクリーンアップ 

Web アプリが必要なくなったら、次のコマンドを使用して、リソース グループ、Web アプリ、およびすべての関連リソースを削除します。

```powershell
Remove-AzResourceGroup -Name $resourceGroupName -Force
```

## <a name="script-explanation"></a>スクリプトの説明

このスクリプトでは、次のコマンドを使用します。 表内の各コマンドは、それぞれのドキュメントにリンクされています。

| command | Notes |
|---|---|
| [Get-AzWebAppBackupList](/powershell/module/az.websites/get-azwebappbackuplist) | Web アプリのバックアップの一覧を取得します。 |
| [Restore-AzWebAppBackup](/powershell/module/az.websites/restore-azwebappbackup) | 以前に完了したバックアップから Web アプリを復元します。 |

## <a name="next-steps"></a>次のステップ

Azure PowerShell モジュールの詳細については、[Azure PowerShell のドキュメント](/powershell/azure/overview)を参照してください。

その他の Azure App Service Web Apps 用 Azure PowerShell サンプル スクリプトは、[Azure PowerShell サンプル](../samples-powershell.md)のページにあります。
