---
title: aaaAzure Script di PowerShell di esempio - OMS | Documenti Microsoft
description: Esempio di script di Azure PowerShell - OMS
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
ms.date: 03/14/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 1eeafbe743013e97bf3fcefb5ce87f72cb503a4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-operations-management-suite-monitored-vm-with-powershell"></a><span data-ttu-id="06370-103">Creare una VM monitorata da Operations Management Suite con PowerShell</span><span class="sxs-lookup"><span data-stu-id="06370-103">Create an Operations Management Suite monitored VM with PowerShell</span></span>

<span data-ttu-id="06370-104">Questo script crea una macchina virtuale di Azure, installa l'agente di Operations Management Suite (OMS) hello e registra sistema hello con un'area di lavoro OMS.</span><span class="sxs-lookup"><span data-stu-id="06370-104">This script creates an Azure Virtual Machine, installs hello Operations Management Suite (OMS) agent, and enrolls hello system with an OMS workspace.</span></span> <span data-ttu-id="06370-105">Dopo l'esecuzione dello script di hello, macchina virtuale hello saranno visibile nella console OMS hello.</span><span class="sxs-lookup"><span data-stu-id="06370-105">Once hello script has run, hello virtual machine will be visible in hello OMS console.</span></span> <span data-ttu-id="06370-106">Inoltre, è necessario tooupdate hello OMS workspace ID chiave e quella dell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="06370-106">Also, you need tooupdate hello OMS workspace ID and workspace key.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="06370-107">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="06370-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-detailed-oms.ps1 "Create VM OMS")]

## <a name="clean-up-deployment"></a><span data-ttu-id="06370-108">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="06370-108">Clean up deployment</span></span> 

<span data-ttu-id="06370-109">Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="06370-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="06370-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="06370-110">Script explanation</span></span>

<span data-ttu-id="06370-111">Questo script utilizza hello dopo la distribuzione di comandi toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="06370-111">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="06370-112">Ogni elemento nella documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="06370-112">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="06370-113">Comando</span><span class="sxs-lookup"><span data-stu-id="06370-113">Command</span></span> | <span data-ttu-id="06370-114">Note</span><span class="sxs-lookup"><span data-stu-id="06370-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="06370-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="06370-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="06370-116">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="06370-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="06370-117">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="06370-117">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="06370-118">Crea una configurazione di subnet.</span><span class="sxs-lookup"><span data-stu-id="06370-118">Creates a subnet configuration.</span></span> <span data-ttu-id="06370-119">Questa configurazione viene utilizzata con processo di creazione di hello rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="06370-119">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="06370-120">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="06370-120">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="06370-121">Crea una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="06370-121">Creates a virtual network.</span></span> |
| [<span data-ttu-id="06370-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="06370-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="06370-123">Crea un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="06370-123">Creates a public IP address.</span></span> |
| [<span data-ttu-id="06370-124">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="06370-124">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="06370-125">Crea una configurazione di regola del gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="06370-125">Creates a network security group rule configuration.</span></span> <span data-ttu-id="06370-126">Questa configurazione è toocreate utilizzata una regola di gruppo quando hello gruppo viene creato.</span><span class="sxs-lookup"><span data-stu-id="06370-126">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="06370-127">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="06370-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="06370-128">Crea un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="06370-128">Creates a network security group.</span></span> |
| [<span data-ttu-id="06370-129">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="06370-129">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="06370-130">Ottiene informazioni sulla subnet.</span><span class="sxs-lookup"><span data-stu-id="06370-130">Gets subnet information.</span></span> <span data-ttu-id="06370-131">Queste informazioni vengono usate durante la creazione di un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="06370-131">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="06370-132">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="06370-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="06370-133">Crea un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="06370-133">Creates a network interface.</span></span> |
| [<span data-ttu-id="06370-134">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="06370-134">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="06370-135">Crea una configurazione di VM.</span><span class="sxs-lookup"><span data-stu-id="06370-135">Creates a VM configuration.</span></span> <span data-ttu-id="06370-136">Questa configurazione include informazioni quali il nome della VM, il sistema operativo e le credenziali amministrative.</span><span class="sxs-lookup"><span data-stu-id="06370-136">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="06370-137">configurazione di Hello viene utilizzato durante la creazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="06370-137">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="06370-138">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="06370-138">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="06370-139">Creare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="06370-139">Create a virtual machine.</span></span> |
| [<span data-ttu-id="06370-140">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="06370-140">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="06370-141">Aggiungere una macchina virtuale VM estensione toohello.</span><span class="sxs-lookup"><span data-stu-id="06370-141">Add a VM extension toohello virtual machine.</span></span> <span data-ttu-id="06370-142">In questo caso, hello estensione agente Operations Management Suite tooinstall utilizzati hello OMS agente e registrare hello macchina virtuale in un'area di lavoro OMS.</span><span class="sxs-lookup"><span data-stu-id="06370-142">In this case, hello Operations Management Suite agent extension is used tooinstall hello OMS agent and enroll hello VM in an OMS workspace.</span></span> |
|[<span data-ttu-id="06370-143">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="06370-143">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="06370-144">Rimuove un gruppo di risorse e tutte le risorse contenute al suo interno.</span><span class="sxs-lookup"><span data-stu-id="06370-144">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="06370-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="06370-145">Next steps</span></span>

<span data-ttu-id="06370-146">Per ulteriori informazioni sul modulo di Azure PowerShell hello, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="06370-146">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="06370-147">Esempi di script di PowerShell di macchina virtuale aggiuntiva sono reperibile in hello [documentazione macchina virtuale Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="06370-147">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
