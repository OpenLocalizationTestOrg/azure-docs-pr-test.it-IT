---
title: esempio di script di PowerShell aaaAzure - il traffico di rete VM filtro | Documenti Microsoft
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
ms.openlocfilehash: 39eae6a43a8dc7f9fc616ef3ec50f95443fd3547
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a><span data-ttu-id="5d741-103">Filtrare il traffico della VM in ingresso e in uscita</span><span class="sxs-lookup"><span data-stu-id="5d741-103">Filter inbound and outbound VM network traffic</span></span>

<span data-ttu-id="5d741-104">Questo script di esempio crea una rete virtuale con subnet front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="5d741-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="5d741-105">Il traffico di rete in ingresso subnet front-end toohello è limitato tooHTTP e toohello Internet dalla subnet di back-end hello non è consentito il traffico HTTPS, mentre in uscita.</span><span class="sxs-lookup"><span data-stu-id="5d741-105">Inbound network traffic toohello front-end subnet is limited tooHTTP, and HTTPS, while outbound traffic toohello Internet from hello back-end subnet is not permitted.</span></span> <span data-ttu-id="5d741-106">Dopo l'esecuzione di script hello, si disporrà di una macchina virtuale con due schede di rete.</span><span class="sxs-lookup"><span data-stu-id="5d741-106">After running hello script, you will have one virtual machine with two NICs.</span></span> <span data-ttu-id="5d741-107">Ogni scheda è connessa tooa diverse subnet.</span><span class="sxs-lookup"><span data-stu-id="5d741-107">Each NIC is connected tooa different subnet.</span></span>

<span data-ttu-id="5d741-108">Se necessario, installare Azure PowerShell utilizzando l'istruzione hello trovato in hello hello [Guida di Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), quindi eseguire `Login-AzureRmAccount` toocreate una connessione con Azure.</span><span class="sxs-lookup"><span data-stu-id="5d741-108">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="5d741-109">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="5d741-109">Sample script</span></span>


[!code-powershell[main](../../../powershell_scripts/virtual-network/filter-network-traffic/filter-network-traffic.ps1  "Filter VM network traffic")]

## <a name="clean-up-deployment"></a><span data-ttu-id="5d741-110">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="5d741-110">Clean up deployment</span></span> 

<span data-ttu-id="5d741-111">Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="5d741-111">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="5d741-112">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="5d741-112">Script explanation</span></span>

<span data-ttu-id="5d741-113">Questo script utilizza hello toocreate i comandi seguenti a un gruppo di risorse, rete virtuale e gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="5d741-113">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="5d741-114">Ogni comando nella documentazione di hello tabella collegamenti toocommand specifica.</span><span class="sxs-lookup"><span data-stu-id="5d741-114">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="5d741-115">Comando</span><span class="sxs-lookup"><span data-stu-id="5d741-115">Command</span></span> | <span data-ttu-id="5d741-116">Note</span><span class="sxs-lookup"><span data-stu-id="5d741-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5d741-117">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5d741-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="5d741-118">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="5d741-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5d741-119">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="5d741-119">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="5d741-120">Crea un oggetto di configurazione di subnet</span><span class="sxs-lookup"><span data-stu-id="5d741-120">Creates a subnet configuration object</span></span> |
| [<span data-ttu-id="5d741-121">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="5d741-121">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="5d741-122">Consente di creare una rete virtuale e una subnet front-end di Azure.</span><span class="sxs-lookup"><span data-stu-id="5d741-122">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="5d741-123">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="5d741-123">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="5d741-124">Crea toobe regole di sicurezza assegnato tooa gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="5d741-124">Creates security rules toobe assigned tooa network security group.</span></span> |
| [<span data-ttu-id="5d741-125">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="5d741-125">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) |<span data-ttu-id="5d741-126">Crea regole del gruppo che consentono o Blocca subnet toospecific porte specifiche.</span><span class="sxs-lookup"><span data-stu-id="5d741-126">Creates NSG rules that allow or block specific ports toospecific subnets.</span></span> |
| [<span data-ttu-id="5d741-127">Set-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="5d741-127">Set-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="5d741-128">Associa NSGs toosubnets.</span><span class="sxs-lookup"><span data-stu-id="5d741-128">Associates NSGs toosubnets.</span></span> |
| [<span data-ttu-id="5d741-129">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="5d741-129">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="5d741-130">Crea un hello VM tooaccess indirizzo pubblico di IP da Internet hello.</span><span class="sxs-lookup"><span data-stu-id="5d741-130">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="5d741-131">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="5d741-131">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="5d741-132">Consente di creare interfacce di rete virtuale e lo connette le subnet front-end e back-end della rete virtuale toohello.</span><span class="sxs-lookup"><span data-stu-id="5d741-132">Creates virtual network interfaces and attaches them toohello virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="5d741-133">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="5d741-133">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="5d741-134">Crea una configurazione di VM.</span><span class="sxs-lookup"><span data-stu-id="5d741-134">Creates a VM configuration.</span></span> <span data-ttu-id="5d741-135">Questa configurazione include informazioni quali il nome della VM, il sistema operativo e le credenziali amministrative.</span><span class="sxs-lookup"><span data-stu-id="5d741-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="5d741-136">configurazione di Hello viene utilizzato durante la creazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5d741-136">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="5d741-137">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="5d741-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="5d741-138">Creare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5d741-138">Create a virtual machine.</span></span> |
|[<span data-ttu-id="5d741-139">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5d741-139">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="5d741-140">Rimuove un gruppo di risorse e tutte le risorse contenute al suo interno.</span><span class="sxs-lookup"><span data-stu-id="5d741-140">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5d741-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5d741-141">Next steps</span></span>

<span data-ttu-id="5d741-142">Per ulteriori informazioni su hello Azure PowerShell, vedere [documentazione di Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5d741-142">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="5d741-143">Ulteriori esempi di script di PowerShell remota sono reperibile in hello [documentazione Cenni preliminari sulle reti di Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5d741-143">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
