---
title: Azure VPN Gateway:ゲートウェイ接続を確認する
description: この記事では、仮想ネットワーク VPN Gateway の接続を確認する方法を説明します。
services: vpn-gateway
author: cherylmc
ms.service: vpn-gateway
ms.topic: article
ms.date: 05/16/2017
ms.author: cherylmc
ms.openlocfilehash: 40417b078577424b1ba13ce60f4f773a1c8fd4dc
ms.sourcegitcommit: 2ec4b3d0bad7dc0071400c2a2264399e4fe34897
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/27/2020
ms.locfileid: "75780149"
---
# <a name="verify-a-vpn-gateway-connection"></a>VPN Gateway 接続の確認

この記事では、クラシック デプロイ モデルと Resource Manager デプロイ モデルの両方での VPN ゲートウェイ接続を確認する方法について説明します。

## <a name="azure-portal"></a>Azure portal

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="powershell"></a>PowerShell

PowerShell を使用して Resource Manager デプロイ モデルでの VPN ゲートウェイ接続を確認するには、[Azure Resource Manager PowerShell コマンドレット](/powershell/azure/overview)の最新バージョンをインストールします。

[!INCLUDE [PowerShell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="azure-cli"></a>Azure CLI

Azure CLI を使用して Resource Manager デプロイ モデルでの VPN ゲートウェイ接続を確認するには、[CLI コマンドレット](https://docs.microsoft.com/cli/azure/install-azure-cli)の最新バージョン (2.0 以降) をインストールします。

[!INCLUDE [CLI](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]


## <a name="azure-portal-classic"></a>Azure Portal (クラシック)

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

## <a name="powershell-classic"></a>PowerShell (クラシック)

PowerShell を使用してクラシック デプロイ モデルでの VPN ゲートウェイ接続を確認するには、Azure PowerShell コマンドレットの最新バージョンをインストールします。 [Service Management](https://docs.microsoft.com/powershell/azure/servicemanagement/install-azure-ps?view=azuresmps-4.0.0#azure-service-management-cmdlets) モジュールをダウンロードし、インストールしてください。 'Add-AzureAccount' を使用して、クラシック デプロイ モデルにログインします。

[!INCLUDE [Classic PowerShell](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

## <a name="next-steps"></a>次のステップ

* 仮想ネットワークに仮想マシンを追加できます。 手順については、 [仮想マシンの作成](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) に関するページを参照してください。
