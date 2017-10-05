---
title: Esempio di script di Azure PowerShell - Creare una VM Windows NLB | Microsoft Docs
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
ms.openlocfilehash: 25bcbbcd1615e01a384825d7bd1582a528e91f71
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="load-balance-traffic-between-highly-available-virtual-machines"></a><span data-ttu-id="e8e49-103">Bilanciare il carico del traffico tra macchine virtuali a disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="e8e49-103">Load balance traffic between highly available virtual machines</span></span>

<span data-ttu-id="e8e49-104">Questo script di esempio crea tutti gli elementi necessari per eseguire più macchine virtuali Windows Server 2016 configurate in una configurazione a disponibilità elevata e con bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="e8e49-104">This script sample creates everything needed to run several Windows Server 2016 virtual machines configured in a highly available and load balanced configuration.</span></span> <span data-ttu-id="e8e49-105">Dopo aver eseguito lo script, si disporrà di tre macchine virtuali, aggiunte a un set di disponibilità di Azure e accessibili tramite Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="e8e49-105">After running the script, you will have three virtual machines, joined to an Azure Availability Set, and accessible through an Azure Load Balancer.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="e8e49-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="e8e49-106">Sample script</span></span>

<span data-ttu-id="e8e49-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.ps1 "Creare una VM NLB")]</span><span class="sxs-lookup"><span data-stu-id="e8e49-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.ps1 "Create VM NLB")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="e8e49-108">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="e8e49-108">Clean up deployment</span></span> 

<span data-ttu-id="e8e49-109">Eseguire questo comando per rimuovere il gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="e8e49-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="e8e49-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="e8e49-110">Script explanation</span></span>

<span data-ttu-id="e8e49-111">Questo script usa i comandi seguenti per creare la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="e8e49-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="e8e49-112">Ogni elemento della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="e8e49-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="e8e49-113">Comando</span><span class="sxs-lookup"><span data-stu-id="e8e49-113">Command</span></span> | <span data-ttu-id="e8e49-114">Note</span><span class="sxs-lookup"><span data-stu-id="e8e49-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e8e49-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e8e49-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="e8e49-116">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="e8e49-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e8e49-117">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="e8e49-117">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="e8e49-118">Crea una configurazione di subnet.</span><span class="sxs-lookup"><span data-stu-id="e8e49-118">Creates a subnet configuration.</span></span> <span data-ttu-id="e8e49-119">Questa configurazione viene usata con il processo di creazione della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e8e49-119">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="e8e49-120">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="e8e49-120">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="e8e49-121">Crea una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e8e49-121">Creates a virtual network.</span></span> |
| [<span data-ttu-id="e8e49-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="e8e49-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="e8e49-123">Crea un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="e8e49-123">Creates a public IP address.</span></span> |
| [<span data-ttu-id="e8e49-124">New-AzureRmLoadBalancerFrontendIpConfig</span><span class="sxs-lookup"><span data-stu-id="e8e49-124">New-AzureRmLoadBalancerFrontendIpConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) | <span data-ttu-id="e8e49-125">Crea una configurazione IP front-end per un servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="e8e49-125">Creates a front-end IP configuration for a load balancer.</span></span> |
| [<span data-ttu-id="e8e49-126">New-AzureRmLoadBalancerBackendAddressPoolConfig</span><span class="sxs-lookup"><span data-stu-id="e8e49-126">New-AzureRmLoadBalancerBackendAddressPoolConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) | <span data-ttu-id="e8e49-127">Crea una configurazione del pool di indirizzi back-end per un servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="e8e49-127">Creates a backend address pool configuration for a load balancer.</span></span> |
| [<span data-ttu-id="e8e49-128">New-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="e8e49-128">New-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) | <span data-ttu-id="e8e49-129">Crea la configurazione di una porta probe per un servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="e8e49-129">Creates a probe configuration for a load balancer.</span></span> |
| [<span data-ttu-id="e8e49-130">New-AzureRmLoadBalancerRuleConfig</span><span class="sxs-lookup"><span data-stu-id="e8e49-130">New-AzureRmLoadBalancerRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) | <span data-ttu-id="e8e49-131">Crea la configurazione di una regola per un servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="e8e49-131">Creates a rule configuration for a load balancer.</span></span> |
| [<span data-ttu-id="e8e49-132">New-AzureRmLoadBalancerInboundNatRuleConfig</span><span class="sxs-lookup"><span data-stu-id="e8e49-132">New-AzureRmLoadBalancerInboundNatRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerinboundnatruleconfig) | <span data-ttu-id="e8e49-133">Crea la configurazione di una regola NAT in ingresso per un servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="e8e49-133">Creates an inbound NAT rule configuration for a load balancer.</span></span> |
| [<span data-ttu-id="e8e49-134">New-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="e8e49-134">New-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancer) | <span data-ttu-id="e8e49-135">Crea un servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="e8e49-135">Creates a load balancer.</span></span> |
| [<span data-ttu-id="e8e49-136">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="e8e49-136">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="e8e49-137">Crea una configurazione di regola del gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="e8e49-137">Creates a network security group rule configuration.</span></span> <span data-ttu-id="e8e49-138">Questa configurazione viene usata per creare una regola NSG quando viene creato il gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="e8e49-138">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="e8e49-139">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="e8e49-139">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="e8e49-140">Crea un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="e8e49-140">Creates a network security group.</span></span> |
| [<span data-ttu-id="e8e49-141">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="e8e49-141">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="e8e49-142">Ottiene informazioni sulla subnet.</span><span class="sxs-lookup"><span data-stu-id="e8e49-142">Gets subnet information.</span></span> <span data-ttu-id="e8e49-143">Queste informazioni vengono usate durante la creazione di un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="e8e49-143">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="e8e49-144">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="e8e49-144">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="e8e49-145">Crea un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="e8e49-145">Creates a network interface.</span></span> |
| [<span data-ttu-id="e8e49-146">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="e8e49-146">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="e8e49-147">Crea una configurazione di VM.</span><span class="sxs-lookup"><span data-stu-id="e8e49-147">Creates a VM configuration.</span></span> <span data-ttu-id="e8e49-148">Questa configurazione include informazioni quali il nome della VM, il sistema operativo e le credenziali amministrative.</span><span class="sxs-lookup"><span data-stu-id="e8e49-148">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="e8e49-149">La configurazione viene usata durante la creazione della VM.</span><span class="sxs-lookup"><span data-stu-id="e8e49-149">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="e8e49-150">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="e8e49-150">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="e8e49-151">Creare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e8e49-151">Create a virtual machine.</span></span> |
|[<span data-ttu-id="e8e49-152">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e8e49-152">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="e8e49-153">Rimuove un gruppo di risorse e tutte le risorse contenute al suo interno.</span><span class="sxs-lookup"><span data-stu-id="e8e49-153">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e8e49-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e8e49-154">Next steps</span></span>

<span data-ttu-id="e8e49-155">Per altre informazioni sul modulo Azure PowerShell, vedere la [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e8e49-155">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="e8e49-156">Altri esempi di script PowerShell della macchina virtuale sono reperibili nella [documentazione della VM Windows di Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e8e49-156">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
