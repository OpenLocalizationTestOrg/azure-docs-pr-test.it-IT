---
title: script di PowerShell di esempio - aaaAzure creare una rete per applicazioni multilivello | Documenti Microsoft
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
ms.openlocfilehash: 46d6d16dc5dbc8be467359f31346f017727b1abe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a><span data-ttu-id="61838-103">Creare una rete per applicazioni multilivello</span><span class="sxs-lookup"><span data-stu-id="61838-103">Create a network for multi-tier applications</span></span>

<span data-ttu-id="61838-104">Questo script di esempio crea una rete virtuale con subnet front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="61838-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="61838-105">Subnet con traffico toohello front-end è limitato tooHTTP e SSH, mentre il traffico toohello subnet back-end è limitato tooMySQL, porta 3306.</span><span class="sxs-lookup"><span data-stu-id="61838-105">Traffic toohello front-end subnet is limited tooHTTP and SSH, while traffic toohello back-end subnet is limited tooMySQL, port 3306.</span></span> <span data-ttu-id="61838-106">Dopo l'esecuzione dello script hello, si avrà a disposizione due macchine virtuali, una in ogni subnet che è possibile distribuire server web e software MySQL.</span><span class="sxs-lookup"><span data-stu-id="61838-106">After running hello script, you will have two virtual machines, one in each subnet that you can deploy web server and MySQL software to.</span></span>

<span data-ttu-id="61838-107">Se necessario, installare Azure PowerShell utilizzando l'istruzione hello trovato in hello hello [Guida di Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), quindi eseguire `Login-AzureRmAccount` toocreate una connessione con Azure.</span><span class="sxs-lookup"><span data-stu-id="61838-107">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="61838-108">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="61838-108">Sample script</span></span>


[!code-powershell[main](../../../powershell_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.ps1  "Virtual network for multi-tier application")]

## <a name="clean-up-deployment"></a><span data-ttu-id="61838-109">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="61838-109">Clean up deployment</span></span> 

<span data-ttu-id="61838-110">Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="61838-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="61838-111">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="61838-111">Script explanation</span></span>

<span data-ttu-id="61838-112">Questo script utilizza hello toocreate i comandi seguenti a un gruppo di risorse, rete virtuale e gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="61838-112">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="61838-113">Ogni comando nella documentazione di hello tabella collegamenti toocommand specifica.</span><span class="sxs-lookup"><span data-stu-id="61838-113">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="61838-114">Comando</span><span class="sxs-lookup"><span data-stu-id="61838-114">Command</span></span> | <span data-ttu-id="61838-115">Note</span><span class="sxs-lookup"><span data-stu-id="61838-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="61838-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="61838-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="61838-117">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="61838-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="61838-118">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="61838-118">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="61838-119">Consente di creare una rete virtuale e una subnet front-end di Azure.</span><span class="sxs-lookup"><span data-stu-id="61838-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="61838-120">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="61838-120">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="61838-121">Consente di creare una subnet back-end.</span><span class="sxs-lookup"><span data-stu-id="61838-121">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="61838-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="61838-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="61838-123">Crea un hello VM tooaccess indirizzo pubblico di IP da Internet hello.</span><span class="sxs-lookup"><span data-stu-id="61838-123">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="61838-124">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="61838-124">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="61838-125">Consente di creare interfacce di rete virtuale e lo connette le subnet front-end e back-end della rete virtuale toohello.</span><span class="sxs-lookup"><span data-stu-id="61838-125">Creates virtual network interfaces and attaches them toohello virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="61838-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="61838-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="61838-127">Crea gruppi di sicurezza di rete (gruppo) che sono subnet front-end e back-end di toohello associato.</span><span class="sxs-lookup"><span data-stu-id="61838-127">Creates network security groups (NSG) that are associated toohello front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="61838-128">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="61838-128">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) |<span data-ttu-id="61838-129">Crea regole del gruppo che consentono o Blocca subnet toospecific porte specifiche.</span><span class="sxs-lookup"><span data-stu-id="61838-129">Creates NSG rules that allow or block specific ports toospecific subnets.</span></span> |
| [<span data-ttu-id="61838-130">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="61838-130">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="61838-131">Crea le macchine virtuali e la collega tooeach una scheda di rete VM.</span><span class="sxs-lookup"><span data-stu-id="61838-131">Creates virtual machines and attaches a NIC tooeach VM.</span></span> <span data-ttu-id="61838-132">Questo comando specifica inoltre toouse immagine di macchina virtuale hello e le credenziali amministrative.</span><span class="sxs-lookup"><span data-stu-id="61838-132">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="61838-133">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="61838-133">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="61838-134">Consente di eliminare un gruppo di risorse e tutte le risorse in esso contenute.</span><span class="sxs-lookup"><span data-stu-id="61838-134">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="61838-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="61838-135">Next steps</span></span>

<span data-ttu-id="61838-136">Per ulteriori informazioni su hello Azure PowerShell, vedere [documentazione di Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="61838-136">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="61838-137">Ulteriori esempi di script di PowerShell remota sono reperibile in hello [documentazione Cenni preliminari sulle reti di Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="61838-137">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
