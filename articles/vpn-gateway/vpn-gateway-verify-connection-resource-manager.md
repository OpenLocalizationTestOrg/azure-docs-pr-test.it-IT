---
title: una connessione VPN Gateway aaaVerify | Documenti Microsoft
description: Questo articolo illustra come tooverify un virtuale connessione Gateway VPN di rete.
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
ms.openlocfilehash: 0d3da94a76b36251d629f82b1575328c7ac10b26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="verify-a-vpn-gateway-connection"></a><span data-ttu-id="c540a-103">Verificare una connessione di Gateway VPN</span><span class="sxs-lookup"><span data-stu-id="c540a-103">Verify a VPN Gateway connection</span></span>

<span data-ttu-id="c540a-104">In questo articolo illustra come tooverify una connessione gateway VPN per hello classic e modelli di distribuzione di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="c540a-104">This article shows you how tooverify a VPN gateway connection for both hello classic and Resource Manager deployment models.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="c540a-105">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c540a-105">Azure portal</span></span>

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="powershell"></a><span data-ttu-id="c540a-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c540a-106">PowerShell</span></span>

<span data-ttu-id="c540a-107">tooverify una connessione gateway VPN per la distribuzione di gestione risorse di hello del modello tramite PowerShell, installare la versione più recente di hello di hello [i cmdlet PowerShell di gestione risorse di Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c540a-107">tooverify a VPN gateway connection for hello Resource Manager deployment model using PowerShell, install hello latest version of hello [Azure Resource Manager PowerShell cmdlets](/powershell/azure/overview).</span></span>

[!INCLUDE [PowerShell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="azure-cli"></a><span data-ttu-id="c540a-108">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="c540a-108">Azure CLI</span></span>

<span data-ttu-id="c540a-109">tooverify una connessione gateway VPN per la distribuzione di gestione risorse di hello del modello utilizzando l'interfaccia CLI di Azure, installare la versione più recente di hello di hello [i comandi CLI](https://docs.microsoft.com/cli/azure/install-azure-cli) (2.0 o versione successiva).</span><span class="sxs-lookup"><span data-stu-id="c540a-109">tooverify a VPN gateway connection for hello Resource Manager deployment model using Azure CLI, install hello latest version of hello [CLI commands](https://docs.microsoft.com/cli/azure/install-azure-cli) (2.0 or later).</span></span>

[!INCLUDE [CLI](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]


## <a name="azure-portal-classic"></a><span data-ttu-id="c540a-110">Portale di Azure (classico)</span><span class="sxs-lookup"><span data-stu-id="c540a-110">Azure portal (classic)</span></span>

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

## <a name="powershell-classic"></a><span data-ttu-id="c540a-111">PowerShell (versione classica)</span><span class="sxs-lookup"><span data-stu-id="c540a-111">PowerShell (classic)</span></span>

<span data-ttu-id="c540a-112">tooverify la connessione del gateway VPN per la distribuzione classica hello del modello tramite PowerShell, installare versioni più recenti di hello di hello cmdlet di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c540a-112">tooverify your VPN gateway connection for hello classic deployment model using PowerShell, install hello latest versions of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="c540a-113">Hello toodownload e installazione assicurarsi di essere [gestione dei servizi](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0) modulo.</span><span class="sxs-lookup"><span data-stu-id="c540a-113">Be sure toodownload and install hello [Service Management](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0) module.</span></span> <span data-ttu-id="c540a-114">Utilizzare il modello di distribuzione classica toohello toolog 'Add-AzureAccount'.</span><span class="sxs-lookup"><span data-stu-id="c540a-114">Use 'Add-AzureAccount' toolog in toohello classic deployment model.</span></span>

[!INCLUDE [Classic PowerShell](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

## <a name="next-steps"></a><span data-ttu-id="c540a-115">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c540a-115">Next steps</span></span>

* <span data-ttu-id="c540a-116">È possibile aggiungere macchine virtuali tooyour le reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="c540a-116">You can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="c540a-117">Per i passaggi, vedere [Creare la prima macchina virtuale](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) .</span><span class="sxs-lookup"><span data-stu-id="c540a-117">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>
