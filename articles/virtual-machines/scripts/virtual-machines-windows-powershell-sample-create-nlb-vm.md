---
title: Script di PowerShell di esempio - aaaAzure creare una macchina virtuale di Windows NLB | Documenti Microsoft
description: Esempio di script di Azure PowerShell - Creare una VM Windows NLB
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/05/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 60a48c5f243c8ff3ab886437ae45b21ce069ea4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-traffic-between-highly-available-virtual-machines"></a><span data-ttu-id="9e43a-103">Bilanciare il carico del traffico tra macchine virtuali a disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="9e43a-103">Load balance traffic between highly available virtual machines</span></span>

<span data-ttu-id="9e43a-104">In questo esempio di script crea tutti gli elementi necessari toorun diverse macchine virtuali di Windows Server 2016 configurati a disponibilità elevata e carico bilanciato di configurazione.</span><span class="sxs-lookup"><span data-stu-id="9e43a-104">This script sample creates everything needed toorun several Windows Server 2016 virtual machines configured in a highly available and load balanced configuration.</span></span> <span data-ttu-id="9e43a-105">Tre macchine virtuali, tooan aggiunti a un Set di disponibilità di Azure, sarà necessario dopo l'esecuzione dello script, hello e accessibile tramite un servizio di bilanciamento del carico di Azure.</span><span class="sxs-lookup"><span data-stu-id="9e43a-105">After running hello script, you will have three virtual machines, joined tooan Azure Availability Set, and accessible through an Azure Load Balancer.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="9e43a-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="9e43a-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.ps1 "Create VM NLB")]

## <a name="clean-up-deployment"></a><span data-ttu-id="9e43a-107">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="9e43a-107">Clean up deployment</span></span> 

<span data-ttu-id="9e43a-108">Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="9e43a-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="9e43a-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="9e43a-109">Script explanation</span></span>

<span data-ttu-id="9e43a-110">Questo script utilizza hello dopo la distribuzione di comandi toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="9e43a-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="9e43a-111">Ogni elemento nella documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="9e43a-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="9e43a-112">Comando</span><span class="sxs-lookup"><span data-stu-id="9e43a-112">Command</span></span> | <span data-ttu-id="9e43a-113">Note</span><span class="sxs-lookup"><span data-stu-id="9e43a-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9e43a-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9e43a-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="9e43a-115">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="9e43a-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9e43a-116">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="9e43a-116">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="9e43a-117">Crea una configurazione di subnet.</span><span class="sxs-lookup"><span data-stu-id="9e43a-117">Creates a subnet configuration.</span></span> <span data-ttu-id="9e43a-118">Questa configurazione viene utilizzata con processo di creazione di hello rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="9e43a-118">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="9e43a-119">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="9e43a-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="9e43a-120">Crea una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="9e43a-120">Creates a virtual network.</span></span> |
| [<span data-ttu-id="9e43a-121">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="9e43a-121">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="9e43a-122">Crea un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="9e43a-122">Creates a public IP address.</span></span> |
| [<span data-ttu-id="9e43a-123">New-AzureRmLoadBalancerFrontendIpConfig</span><span class="sxs-lookup"><span data-stu-id="9e43a-123">New-AzureRmLoadBalancerFrontendIpConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) | <span data-ttu-id="9e43a-124">Crea una configurazione IP front-end per un servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="9e43a-124">Creates a front-end IP configuration for a load balancer.</span></span> |
| [<span data-ttu-id="9e43a-125">New-AzureRmLoadBalancerBackendAddressPoolConfig</span><span class="sxs-lookup"><span data-stu-id="9e43a-125">New-AzureRmLoadBalancerBackendAddressPoolConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) | <span data-ttu-id="9e43a-126">Crea una configurazione del pool di indirizzi back-end per un servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="9e43a-126">Creates a backend address pool configuration for a load balancer.</span></span> |
| [<span data-ttu-id="9e43a-127">New-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="9e43a-127">New-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) | <span data-ttu-id="9e43a-128">Crea la configurazione di una porta probe per un servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="9e43a-128">Creates a probe configuration for a load balancer.</span></span> |
| [<span data-ttu-id="9e43a-129">New-AzureRmLoadBalancerRuleConfig</span><span class="sxs-lookup"><span data-stu-id="9e43a-129">New-AzureRmLoadBalancerRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) | <span data-ttu-id="9e43a-130">Crea la configurazione di una regola per un servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="9e43a-130">Creates a rule configuration for a load balancer.</span></span> |
| [<span data-ttu-id="9e43a-131">New-AzureRmLoadBalancerInboundNatRuleConfig</span><span class="sxs-lookup"><span data-stu-id="9e43a-131">New-AzureRmLoadBalancerInboundNatRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerinboundnatruleconfig) | <span data-ttu-id="9e43a-132">Crea la configurazione di una regola NAT in ingresso per un servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="9e43a-132">Creates an inbound NAT rule configuration for a load balancer.</span></span> |
| [<span data-ttu-id="9e43a-133">New-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="9e43a-133">New-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancer) | <span data-ttu-id="9e43a-134">Crea un servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="9e43a-134">Creates a load balancer.</span></span> |
| [<span data-ttu-id="9e43a-135">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="9e43a-135">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="9e43a-136">Crea una configurazione di regola del gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="9e43a-136">Creates a network security group rule configuration.</span></span> <span data-ttu-id="9e43a-137">Questa configurazione è toocreate utilizzata una regola di gruppo quando hello gruppo viene creato.</span><span class="sxs-lookup"><span data-stu-id="9e43a-137">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="9e43a-138">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="9e43a-138">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="9e43a-139">Crea un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="9e43a-139">Creates a network security group.</span></span> |
| [<span data-ttu-id="9e43a-140">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="9e43a-140">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="9e43a-141">Ottiene informazioni sulla subnet.</span><span class="sxs-lookup"><span data-stu-id="9e43a-141">Gets subnet information.</span></span> <span data-ttu-id="9e43a-142">Queste informazioni vengono usate durante la creazione di un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="9e43a-142">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="9e43a-143">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="9e43a-143">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="9e43a-144">Crea un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="9e43a-144">Creates a network interface.</span></span> |
| [<span data-ttu-id="9e43a-145">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="9e43a-145">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="9e43a-146">Crea una configurazione di VM.</span><span class="sxs-lookup"><span data-stu-id="9e43a-146">Creates a VM configuration.</span></span> <span data-ttu-id="9e43a-147">Questa configurazione include informazioni quali il nome della VM, il sistema operativo e le credenziali amministrative.</span><span class="sxs-lookup"><span data-stu-id="9e43a-147">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="9e43a-148">configurazione di Hello viene utilizzato durante la creazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9e43a-148">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="9e43a-149">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="9e43a-149">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="9e43a-150">Creare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9e43a-150">Create a virtual machine.</span></span> |
|[<span data-ttu-id="9e43a-151">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9e43a-151">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="9e43a-152">Rimuove un gruppo di risorse e tutte le risorse contenute al suo interno.</span><span class="sxs-lookup"><span data-stu-id="9e43a-152">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9e43a-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9e43a-153">Next steps</span></span>

<span data-ttu-id="9e43a-154">Per ulteriori informazioni sul modulo di Azure PowerShell hello, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9e43a-154">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="9e43a-155">Esempi di script di PowerShell di macchina virtuale aggiuntiva sono reperibile in hello [documentazione macchina virtuale Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9e43a-155">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
