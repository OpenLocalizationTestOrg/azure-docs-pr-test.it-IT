---
title: 'Esempio di script di Azure PowerShell: filtrare il traffico di rete della VM | Microsoft Docs'
description: 'Esempio di script di Azure PowerShell: filtrare il traffico di rete della VM in ingresso e in uscita.'
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
ms.openlocfilehash: e871ba2f370157936c2aaabc804dc9f5aea6d7ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a><span data-ttu-id="4f546-103">Filtrare il traffico della VM in ingresso e in uscita</span><span class="sxs-lookup"><span data-stu-id="4f546-103">Filter inbound and outbound VM network traffic</span></span>

<span data-ttu-id="4f546-104">Questo script di esempio crea una rete virtuale con subnet front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="4f546-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="4f546-105">Il traffico di rete in ingresso alla subnet front-end è limitato a HTTP e HTTPS, mentre il traffico in uscita verso Internet dalla subnet back-end non è consentito.</span><span class="sxs-lookup"><span data-stu-id="4f546-105">Inbound network traffic to the front-end subnet is limited to HTTP, and HTTPS, while outbound traffic to the Internet from the back-end subnet is not permitted.</span></span> <span data-ttu-id="4f546-106">Dopo aver eseguito lo script sarà presente una macchina virtuale con due NIC.</span><span class="sxs-lookup"><span data-stu-id="4f546-106">After running the script, you will have one virtual machine with two NICs.</span></span> <span data-ttu-id="4f546-107">Ogni NIC è collegata a una subnet diversa.</span><span class="sxs-lookup"><span data-stu-id="4f546-107">Each NIC is connected to a different subnet.</span></span>

<span data-ttu-id="4f546-108">Se necessario, installare Azure PowerShell usando l'istruzione presente nella [Guida di Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) e quindi eseguire `Login-AzureRmAccount` per creare una connessione con Azure.</span><span class="sxs-lookup"><span data-stu-id="4f546-108">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="4f546-109">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="4f546-109">Sample script</span></span>


<span data-ttu-id="4f546-110">[!code-powershell[main](../../../powershell_scripts/virtual-network/filter-network-traffic/filter-network-traffic.ps1  "Filtrare il traffico di rete della VM")]</span><span class="sxs-lookup"><span data-stu-id="4f546-110">[!code-powershell[main](../../../powershell_scripts/virtual-network/filter-network-traffic/filter-network-traffic.ps1  "Filter VM network traffic")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="4f546-111">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="4f546-111">Clean up deployment</span></span> 

<span data-ttu-id="4f546-112">Eseguire questo comando per rimuovere il gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="4f546-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="4f546-113">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="4f546-113">Script explanation</span></span>

<span data-ttu-id="4f546-114">Questo script usa i comandi seguenti per creare un gruppo di risorse, una rete virtuale e i gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="4f546-114">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="4f546-115">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="4f546-115">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="4f546-116">Comando</span><span class="sxs-lookup"><span data-stu-id="4f546-116">Command</span></span> | <span data-ttu-id="4f546-117">Note</span><span class="sxs-lookup"><span data-stu-id="4f546-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4f546-118">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4f546-118">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="4f546-119">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="4f546-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4f546-120">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="4f546-120">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="4f546-121">Crea un oggetto di configurazione di subnet</span><span class="sxs-lookup"><span data-stu-id="4f546-121">Creates a subnet configuration object</span></span> |
| [<span data-ttu-id="4f546-122">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="4f546-122">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="4f546-123">Consente di creare una rete virtuale e una subnet front-end di Azure.</span><span class="sxs-lookup"><span data-stu-id="4f546-123">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="4f546-124">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="4f546-124">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="4f546-125">Crea regole di sicurezza da assegnare a un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="4f546-125">Creates security rules to be assigned to a network security group.</span></span> |
| [<span data-ttu-id="4f546-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="4f546-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) |<span data-ttu-id="4f546-127">Consente di creare regole del gruppo di sicurezza di rete che consentono o bloccano porte specifiche su subnet specifiche.</span><span class="sxs-lookup"><span data-stu-id="4f546-127">Creates NSG rules that allow or block specific ports to specific subnets.</span></span> |
| [<span data-ttu-id="4f546-128">Set-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="4f546-128">Set-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="4f546-129">Consente di associare i gruppi di risorse di rete alla subnet.</span><span class="sxs-lookup"><span data-stu-id="4f546-129">Associates NSGs to subnets.</span></span> |
| [<span data-ttu-id="4f546-130">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="4f546-130">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="4f546-131">Consente di creare un indirizzo IP pubblico per accedere alla VM da Internet.</span><span class="sxs-lookup"><span data-stu-id="4f546-131">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="4f546-132">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="4f546-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="4f546-133">Consente di creare interfacce di rete virtuale e di associarle alle subnet front-end e back-end della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="4f546-133">Creates virtual network interfaces and attaches them to the virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="4f546-134">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="4f546-134">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="4f546-135">Crea una configurazione di VM.</span><span class="sxs-lookup"><span data-stu-id="4f546-135">Creates a VM configuration.</span></span> <span data-ttu-id="4f546-136">Questa configurazione include informazioni quali il nome della VM, il sistema operativo e le credenziali amministrative.</span><span class="sxs-lookup"><span data-stu-id="4f546-136">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="4f546-137">La configurazione viene usata durante la creazione della VM.</span><span class="sxs-lookup"><span data-stu-id="4f546-137">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="4f546-138">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="4f546-138">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="4f546-139">Creare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4f546-139">Create a virtual machine.</span></span> |
|[<span data-ttu-id="4f546-140">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4f546-140">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="4f546-141">Rimuove un gruppo di risorse e tutte le risorse contenute al suo interno.</span><span class="sxs-lookup"><span data-stu-id="4f546-141">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4f546-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4f546-142">Next steps</span></span>

<span data-ttu-id="4f546-143">Per altre informazioni su Azure PowerShell, vedere la [documentazione di Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4f546-143">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="4f546-144">Altri esempi di script di PowerShell per la rete sono disponibili nella [documentazione con la panoramica delle reti di Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4f546-144">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>