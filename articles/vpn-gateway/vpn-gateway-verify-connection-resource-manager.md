---
title: Verificare una connessione di Gateway VPN | Documentazione Microsoft
description: Questo articolo descrive come verificare una connessione di Gateway VPN alla rete virtuale.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 7e3d1043-caa9-4472-96d3-832f4e2c91ee
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/16/2017
ms.author: cherylmc
ms.openlocfilehash: b2d702ecdd5e1fca342e7c84c6e75339097f0bcd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="verify-a-vpn-gateway-connection"></a><span data-ttu-id="f507d-103">Verificare una connessione di Gateway VPN</span><span class="sxs-lookup"><span data-stu-id="f507d-103">Verify a VPN Gateway connection</span></span>

<span data-ttu-id="f507d-104">Questo articolo illustra come verificare una connessione al gateway VPN nei modelli di distribuzione di Resource Manager e classico.</span><span class="sxs-lookup"><span data-stu-id="f507d-104">This article shows you how to verify a VPN gateway connection for both the classic and Resource Manager deployment models.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="f507d-105">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="f507d-105">Azure portal</span></span>

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="powershell"></a><span data-ttu-id="f507d-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f507d-106">PowerShell</span></span>

<span data-ttu-id="f507d-107">Per verificare una connessione al gateway VPN nel modello di distribuzione di Resource Manager tramite PowerShell, installare la versione più recente dei [cmdlet di PowerShell per Azure Resource Manager](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f507d-107">To verify a VPN gateway connection for the Resource Manager deployment model using PowerShell, install the latest version of the [Azure Resource Manager PowerShell cmdlets](/powershell/azure/overview).</span></span>

[!INCLUDE [PowerShell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="azure-cli"></a><span data-ttu-id="f507d-108">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="f507d-108">Azure CLI</span></span>

<span data-ttu-id="f507d-109">Per verificare una connessione al gateway VPN nel modello di distribuzione di Resource Manager tramite l'interfaccia della riga di comando di Azure, installare la versione più recente dei [comandi per l'interfaccia della riga di comando](https://docs.microsoft.com/cli/azure/install-azure-cli), ovvero la versione 2.0 o successiva.</span><span class="sxs-lookup"><span data-stu-id="f507d-109">To verify a VPN gateway connection for the Resource Manager deployment model using Azure CLI, install the latest version of the [CLI commands](https://docs.microsoft.com/cli/azure/install-azure-cli) (2.0 or later).</span></span>

[!INCLUDE [CLI](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]


## <a name="azure-portal-classic"></a><span data-ttu-id="f507d-110">Portale di Azure (classico)</span><span class="sxs-lookup"><span data-stu-id="f507d-110">Azure portal (classic)</span></span>

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

## <a name="powershell-classic"></a><span data-ttu-id="f507d-111">PowerShell (versione classica)</span><span class="sxs-lookup"><span data-stu-id="f507d-111">PowerShell (classic)</span></span>

<span data-ttu-id="f507d-112">Per verificare una connessione al gateway VPN nel modello di distribuzione classico tramite PowerShell, installare le versioni più recenti dei cmdlet di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f507d-112">To verify your VPN gateway connection for the classic deployment model using PowerShell, install the latest versions of the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="f507d-113">Assicurarsi di scaricare e installare il modulo [Gestione servizi](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="f507d-113">Be sure to download and install the [Service Management](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0) module.</span></span> <span data-ttu-id="f507d-114">Accedere al modello di distribuzione classica con "Add-AzureAccount".</span><span class="sxs-lookup"><span data-stu-id="f507d-114">Use 'Add-AzureAccount' to log in to the classic deployment model.</span></span>

[!INCLUDE [Classic PowerShell](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

## <a name="next-steps"></a><span data-ttu-id="f507d-115">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f507d-115">Next steps</span></span>

* <span data-ttu-id="f507d-116">È possibile aggiungere macchine virtuali alla rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="f507d-116">You can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="f507d-117">Per i passaggi, vedere [Creare una macchina virtuale](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) .</span><span class="sxs-lookup"><span data-stu-id="f507d-117">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>