---
title: esempio di script di PowerShell aaaAzure - instradare il traffico attraverso un dispositivo di rete virtuale | Documenti Microsoft
description: Esempio di script di Azure PowerShell - Instradare il traffico attraverso un'appliance virtuale di rete di tipo firewall.
services: virtual-network
documentationcenter: virtual-network
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 3b999f3289d654c00d5becb973e2883896457d52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a><span data-ttu-id="fad64-103">Instradare il traffico attraverso un'appliance virtuale di rete</span><span class="sxs-lookup"><span data-stu-id="fad64-103">Route traffic through a network virtual appliance</span></span>

<span data-ttu-id="fad64-104">Questo script di esempio crea una rete virtuale con subnet front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="fad64-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="fad64-105">Viene inoltre creata una macchina virtuale con IP inoltro del traffico tra due subnet hello tooroute abilitato.</span><span class="sxs-lookup"><span data-stu-id="fad64-105">It also creates a VM with IP forwarding enabled tooroute traffic between hello two subnets.</span></span> <span data-ttu-id="fad64-106">Dopo l'esecuzione di script hello è possibile distribuire il software di rete, ad esempio un'applicazione di firewall, toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fad64-106">After running hello script you can deploy network software, such as a firewall application, toohello VM.</span></span>

<span data-ttu-id="fad64-107">Se necessario, installare Azure PowerShell utilizzando l'istruzione hello trovato in hello hello [Guida di Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), quindi eseguire `Login-AzureRmAccount` toocreate una connessione con Azure.</span><span class="sxs-lookup"><span data-stu-id="fad64-107">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="fad64-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="fad64-108">Sample script</span></span>


[!code-powershell[main](../../../powershell_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.ps1 "Route traffic through a network virtual appliance")]

## <a name="clean-up-deployment"></a><span data-ttu-id="fad64-109">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="fad64-109">Clean up deployment</span></span> 

<span data-ttu-id="fad64-110">Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="fad64-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```
## <a name="script-explanation"></a><span data-ttu-id="fad64-111">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="fad64-111">Script explanation</span></span>

<span data-ttu-id="fad64-112">Questo script utilizza hello toocreate i comandi seguenti a un gruppo di risorse, rete virtuale e gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="fad64-112">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="fad64-113">Ogni comando nella documentazione di hello tabella collegamenti toocommand specifica.</span><span class="sxs-lookup"><span data-stu-id="fad64-113">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="fad64-114">Comando</span><span class="sxs-lookup"><span data-stu-id="fad64-114">Command</span></span> | <span data-ttu-id="fad64-115">Note</span><span class="sxs-lookup"><span data-stu-id="fad64-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fad64-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="fad64-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | <span data-ttu-id="fad64-117">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="fad64-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="fad64-118">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="fad64-118">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="fad64-119">Consente di creare una rete virtuale e una subnet front-end di Azure.</span><span class="sxs-lookup"><span data-stu-id="fad64-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="fad64-120">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="fad64-120">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="fad64-121">Consente di creare le subnet back-end e di rete perimetrale.</span><span class="sxs-lookup"><span data-stu-id="fad64-121">Creates back-end and DMZ subnets.</span></span> |
| [<span data-ttu-id="fad64-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="fad64-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="fad64-123">Crea un hello VM tooaccess indirizzo pubblico di IP da Internet hello.</span><span class="sxs-lookup"><span data-stu-id="fad64-123">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="fad64-124">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="fad64-124">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="fad64-125">Consente di creare un'interfaccia di rete virtuale e attiva l'inoltro IP.</span><span class="sxs-lookup"><span data-stu-id="fad64-125">Creates a virtual network interface and enable IP forwarding for it.</span></span> |
| [<span data-ttu-id="fad64-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="fad64-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="fad64-127">Consente di creare un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="fad64-127">Creates a network security group (NSG).</span></span> |
| [<span data-ttu-id="fad64-128">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="fad64-128">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="fad64-129">Crea regole del gruppo che consentono le porte HTTP e HTTPS in ingresso toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fad64-129">Creates NSG rules that allow HTTP and HTTPS ports inbound toohello VM.</span></span> |
| [<span data-ttu-id="fad64-130">Set-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="fad64-130">Set-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig)| <span data-ttu-id="fad64-131">Associa hello NSGs e toosubnets nelle tabelle di route.</span><span class="sxs-lookup"><span data-stu-id="fad64-131">Associates hello NSGs and route tables toosubnets.</span></span> |
| [<span data-ttu-id="fad64-132">New-AzureRmRouteTable</span><span class="sxs-lookup"><span data-stu-id="fad64-132">New-AzureRmRouteTable</span></span>](/powershell/module/azurerm.network/new-azurermroutetable)| <span data-ttu-id="fad64-133">Consente di creare una tabella di route per tutte le route.</span><span class="sxs-lookup"><span data-stu-id="fad64-133">Creates a route table for all routes.</span></span> |
| [<span data-ttu-id="fad64-134">New-AzureRMRouteConfig</span><span class="sxs-lookup"><span data-stu-id="fad64-134">New-AzureRMRouteConfig</span></span>](/powershell/module/azurerm.network/new-azurermrouteconfig)| <span data-ttu-id="fad64-135">Crea route tooroute il traffico tra subnet e hello Internet tramite hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fad64-135">Creates routes tooroute traffic between subnets and hello Internet through hello VM.</span></span> |
| [<span data-ttu-id="fad64-136">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="fad64-136">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="fad64-137">Crea una macchina virtuale e collega tooit NIC hello.</span><span class="sxs-lookup"><span data-stu-id="fad64-137">Creates a virtual machine and attaches hello NIC tooit.</span></span> <span data-ttu-id="fad64-138">Questo comando specifica inoltre toouse immagine di macchina virtuale hello e le credenziali amministrative.</span><span class="sxs-lookup"><span data-stu-id="fad64-138">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="fad64-139">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="fad64-139">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup)  | <span data-ttu-id="fad64-140">Consente di eliminare un gruppo di risorse e tutte le risorse in esso contenute.</span><span class="sxs-lookup"><span data-stu-id="fad64-140">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fad64-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fad64-141">Next steps</span></span>

<span data-ttu-id="fad64-142">Per ulteriori informazioni su hello Azure PowerShell, vedere [documentazione di Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fad64-142">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="fad64-143">Ulteriori esempi di script di PowerShell remota sono reperibile in hello [documentazione Cenni preliminari sulle reti di Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fad64-143">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
