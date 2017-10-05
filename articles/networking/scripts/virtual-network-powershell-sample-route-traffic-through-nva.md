---
title: Esempio di script di Azure PowerShell - Instradare il traffico attraverso un'appliance virtuale di rete | Microsoft Docs
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
ms.openlocfilehash: 883d28dac72a66c2186d222f72b04d68e532cead
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a><span data-ttu-id="702c9-103">Instradare il traffico attraverso un'appliance virtuale di rete</span><span class="sxs-lookup"><span data-stu-id="702c9-103">Route traffic through a network virtual appliance</span></span>

<span data-ttu-id="702c9-104">Questo script di esempio crea una rete virtuale con subnet front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="702c9-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="702c9-105">Crea anche una VM con inoltro IP attivato per instradare il traffico tra le due subnet.</span><span class="sxs-lookup"><span data-stu-id="702c9-105">It also creates a VM with IP forwarding enabled to route traffic between the two subnets.</span></span> <span data-ttu-id="702c9-106">Dopo aver eseguito lo script è possibile distribuire il software di rete, ad esempio un'applicazione firewall, nella VM.</span><span class="sxs-lookup"><span data-stu-id="702c9-106">After running the script you can deploy network software, such as a firewall application, to the VM.</span></span>

<span data-ttu-id="702c9-107">Se necessario, installare Azure PowerShell usando l'istruzione presente nella [Guida di Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) e quindi eseguire `Login-AzureRmAccount` per creare una connessione con Azure.</span><span class="sxs-lookup"><span data-stu-id="702c9-107">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="702c9-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="702c9-108">Sample script</span></span>


<span data-ttu-id="702c9-109">[!code-powershell[main](../../../powershell_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.ps1 "Instradare il traffico attraverso un'appliance virtuale di rete")]</span><span class="sxs-lookup"><span data-stu-id="702c9-109">[!code-powershell[main](../../../powershell_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.ps1 "Route traffic through a network virtual appliance")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="702c9-110">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="702c9-110">Clean up deployment</span></span> 

<span data-ttu-id="702c9-111">Eseguire questo comando per rimuovere il gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="702c9-111">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```
## <a name="script-explanation"></a><span data-ttu-id="702c9-112">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="702c9-112">Script explanation</span></span>

<span data-ttu-id="702c9-113">Questo script usa i comandi seguenti per creare un gruppo di risorse, una rete virtuale e i gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="702c9-113">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="702c9-114">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="702c9-114">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="702c9-115">Comando</span><span class="sxs-lookup"><span data-stu-id="702c9-115">Command</span></span> | <span data-ttu-id="702c9-116">Note</span><span class="sxs-lookup"><span data-stu-id="702c9-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="702c9-117">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="702c9-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | <span data-ttu-id="702c9-118">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="702c9-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="702c9-119">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="702c9-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="702c9-120">Consente di creare una rete virtuale e una subnet front-end di Azure.</span><span class="sxs-lookup"><span data-stu-id="702c9-120">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="702c9-121">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="702c9-121">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="702c9-122">Consente di creare le subnet back-end e di rete perimetrale.</span><span class="sxs-lookup"><span data-stu-id="702c9-122">Creates back-end and DMZ subnets.</span></span> |
| [<span data-ttu-id="702c9-123">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="702c9-123">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="702c9-124">Consente di creare un indirizzo IP pubblico per accedere alla VM da Internet.</span><span class="sxs-lookup"><span data-stu-id="702c9-124">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="702c9-125">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="702c9-125">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="702c9-126">Consente di creare un'interfaccia di rete virtuale e attiva l'inoltro IP.</span><span class="sxs-lookup"><span data-stu-id="702c9-126">Creates a virtual network interface and enable IP forwarding for it.</span></span> |
| [<span data-ttu-id="702c9-127">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="702c9-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="702c9-128">Consente di creare un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="702c9-128">Creates a network security group (NSG).</span></span> |
| [<span data-ttu-id="702c9-129">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="702c9-129">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="702c9-130">Consente di creare regole del gruppo di sicurezza di rete per le porte HTTP e HTTPS in ingresso alla VM.</span><span class="sxs-lookup"><span data-stu-id="702c9-130">Creates NSG rules that allow HTTP and HTTPS ports inbound to the VM.</span></span> |
| [<span data-ttu-id="702c9-131">Set-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="702c9-131">Set-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig)| <span data-ttu-id="702c9-132">Consente di associare il gruppo di sicurezza di rete e le tabelle di route alle subnet.</span><span class="sxs-lookup"><span data-stu-id="702c9-132">Associates the NSGs and route tables to subnets.</span></span> |
| [<span data-ttu-id="702c9-133">New-AzureRmRouteTable</span><span class="sxs-lookup"><span data-stu-id="702c9-133">New-AzureRmRouteTable</span></span>](/powershell/module/azurerm.network/new-azurermroutetable)| <span data-ttu-id="702c9-134">Consente di creare una tabella di route per tutte le route.</span><span class="sxs-lookup"><span data-stu-id="702c9-134">Creates a route table for all routes.</span></span> |
| [<span data-ttu-id="702c9-135">New-AzureRMRouteConfig</span><span class="sxs-lookup"><span data-stu-id="702c9-135">New-AzureRMRouteConfig</span></span>](/powershell/module/azurerm.network/new-azurermrouteconfig)| <span data-ttu-id="702c9-136">Consente di creare le route per instradare il traffico tra subnet e Internet attraverso la VM.</span><span class="sxs-lookup"><span data-stu-id="702c9-136">Creates routes to route traffic between subnets and the Internet through the VM.</span></span> |
| [<span data-ttu-id="702c9-137">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="702c9-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="702c9-138">Consente di creare una macchina virtuale e vi connette la NIC.</span><span class="sxs-lookup"><span data-stu-id="702c9-138">Creates a virtual machine and attaches the NIC to it.</span></span> <span data-ttu-id="702c9-139">Questo comando specifica anche l'immagine della macchina virtuale da usare e le credenziali di amministrazione.</span><span class="sxs-lookup"><span data-stu-id="702c9-139">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="702c9-140">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="702c9-140">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup)  | <span data-ttu-id="702c9-141">Consente di eliminare un gruppo di risorse e tutte le risorse in esso contenute.</span><span class="sxs-lookup"><span data-stu-id="702c9-141">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="702c9-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="702c9-142">Next steps</span></span>

<span data-ttu-id="702c9-143">Per altre informazioni su Azure PowerShell, vedere la [documentazione di Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="702c9-143">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="702c9-144">Altri esempi di script di PowerShell per la rete sono disponibili nella [documentazione con la panoramica delle reti di Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="702c9-144">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>