---
title: Esempio di script di Azure PowerShell - Creare una rete per applicazioni multilivello | Microsoft Docs
description: Esempio di script di Azure PowerShell - Creare una rete virtuale per applicazioni multilivello.
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
ms.openlocfilehash: ab49e78ef17b093d2bbe4e3276a1ece3a4247f91
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a><span data-ttu-id="ac908-103">Creare una rete per applicazioni multilivello</span><span class="sxs-lookup"><span data-stu-id="ac908-103">Create a network for multi-tier applications</span></span>

<span data-ttu-id="ac908-104">Questo script di esempio crea una rete virtuale con subnet front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="ac908-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="ac908-105">Il traffico verso la subnet front-end è limitato a HTTP e SSH, mentre il traffico verso la subnet back-end è limitato a MySQL sulla porta 3306.</span><span class="sxs-lookup"><span data-stu-id="ac908-105">Traffic to the front-end subnet is limited to HTTP and SSH, while traffic to the back-end subnet is limited to MySQL, port 3306.</span></span> <span data-ttu-id="ac908-106">Dopo aver eseguito lo script saranno presenti due macchine virtuali, una in ogni subnet in cui è possibile distribuire server Web e software MySQL.</span><span class="sxs-lookup"><span data-stu-id="ac908-106">After running the script, you will have two virtual machines, one in each subnet that you can deploy web server and MySQL software to.</span></span>

<span data-ttu-id="ac908-107">Se necessario, installare Azure PowerShell usando l'istruzione presente nella [Guida di Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) e quindi eseguire `Login-AzureRmAccount` per creare una connessione con Azure.</span><span class="sxs-lookup"><span data-stu-id="ac908-107">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="ac908-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="ac908-108">Sample script</span></span>


<span data-ttu-id="ac908-109">[!code-powershell[main](../../../powershell_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.ps1  "Rete virtuale per applicazioni multilivello")]</span><span class="sxs-lookup"><span data-stu-id="ac908-109">[!code-powershell[main](../../../powershell_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.ps1  "Virtual network for multi-tier application")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="ac908-110">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="ac908-110">Clean up deployment</span></span> 

<span data-ttu-id="ac908-111">Eseguire questo comando per rimuovere il gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="ac908-111">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="ac908-112">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="ac908-112">Script explanation</span></span>

<span data-ttu-id="ac908-113">Questo script usa i comandi seguenti per creare un gruppo di risorse, una rete virtuale e i gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="ac908-113">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="ac908-114">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="ac908-114">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="ac908-115">Comando</span><span class="sxs-lookup"><span data-stu-id="ac908-115">Command</span></span> | <span data-ttu-id="ac908-116">Note</span><span class="sxs-lookup"><span data-stu-id="ac908-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ac908-117">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ac908-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="ac908-118">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="ac908-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ac908-119">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="ac908-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="ac908-120">Consente di creare una rete virtuale e una subnet front-end di Azure.</span><span class="sxs-lookup"><span data-stu-id="ac908-120">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="ac908-121">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="ac908-121">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="ac908-122">Consente di creare una subnet back-end.</span><span class="sxs-lookup"><span data-stu-id="ac908-122">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="ac908-123">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="ac908-123">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="ac908-124">Consente di creare un indirizzo IP pubblico per accedere alla VM da Internet.</span><span class="sxs-lookup"><span data-stu-id="ac908-124">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="ac908-125">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="ac908-125">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="ac908-126">Consente di creare interfacce di rete virtuale e di associarle alle subnet front-end e back-end della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="ac908-126">Creates virtual network interfaces and attaches them to the virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="ac908-127">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="ac908-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="ac908-128">Consente di creare gruppi di sicurezza di rete associati alle subnet front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="ac908-128">Creates network security groups (NSG) that are associated to the front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="ac908-129">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="ac908-129">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) |<span data-ttu-id="ac908-130">Consente di creare regole del gruppo di sicurezza di rete che consentono o bloccano porte specifiche su subnet specifiche.</span><span class="sxs-lookup"><span data-stu-id="ac908-130">Creates NSG rules that allow or block specific ports to specific subnets.</span></span> |
| [<span data-ttu-id="ac908-131">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="ac908-131">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="ac908-132">Consente di creare macchine virtuali e associa una NIC a ogni VM.</span><span class="sxs-lookup"><span data-stu-id="ac908-132">Creates virtual machines and attaches a NIC to each VM.</span></span> <span data-ttu-id="ac908-133">Questo comando specifica anche l'immagine della macchina virtuale da usare e le credenziali di amministrazione.</span><span class="sxs-lookup"><span data-stu-id="ac908-133">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="ac908-134">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ac908-134">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="ac908-135">Consente di eliminare un gruppo di risorse e tutte le risorse in esso contenute.</span><span class="sxs-lookup"><span data-stu-id="ac908-135">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ac908-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ac908-136">Next steps</span></span>

<span data-ttu-id="ac908-137">Per altre informazioni su Azure PowerShell, vedere la [documentazione di Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ac908-137">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="ac908-138">Altri esempi di script di PowerShell per la rete sono disponibili nella [documentazione con la panoramica delle reti di Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ac908-138">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>