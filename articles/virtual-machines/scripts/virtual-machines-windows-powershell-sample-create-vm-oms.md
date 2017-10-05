---
title: Esempio di script di Azure PowerShell - OMS | Microsoft Docs
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
ms.openlocfilehash: 9f876be46f5214b12d6a46e54509ba3541f819c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-operations-management-suite-monitored-vm-with-powershell"></a><span data-ttu-id="fbe4a-103">Creare una VM monitorata da Operations Management Suite con PowerShell</span><span class="sxs-lookup"><span data-stu-id="fbe4a-103">Create an Operations Management Suite monitored VM with PowerShell</span></span>

<span data-ttu-id="fbe4a-104">Questo script consente di creare una macchina virtuale di Azure, installare l'agente Operations Management Suite (OMS) e registrare il sistema in un'area di lavoro OMS.</span><span class="sxs-lookup"><span data-stu-id="fbe4a-104">This script creates an Azure Virtual Machine, installs the Operations Management Suite (OMS) agent, and enrolls the system with an OMS workspace.</span></span> <span data-ttu-id="fbe4a-105">Dopo l'esecuzione dello script, la macchina virtuale sarà visibile nella console di OMS.</span><span class="sxs-lookup"><span data-stu-id="fbe4a-105">Once the script has run, the virtual machine will be visible in the OMS console.</span></span> <span data-ttu-id="fbe4a-106">È anche necessario aggiornare la chiave dell'area di lavoro e l'ID area di lavoro OMS.</span><span class="sxs-lookup"><span data-stu-id="fbe4a-106">Also, you need to update the OMS workspace ID and workspace key.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="fbe4a-107">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="fbe4a-107">Sample script</span></span>

<span data-ttu-id="fbe4a-108">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-detailed-oms.ps1 "Creare una VM OMS")]</span><span class="sxs-lookup"><span data-stu-id="fbe4a-108">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-detailed-oms.ps1 "Create VM OMS")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="fbe4a-109">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="fbe4a-109">Clean up deployment</span></span> 

<span data-ttu-id="fbe4a-110">Eseguire questo comando per rimuovere il gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="fbe4a-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="fbe4a-111">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="fbe4a-111">Script explanation</span></span>

<span data-ttu-id="fbe4a-112">Questo script usa i comandi seguenti per creare la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="fbe4a-112">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="fbe4a-113">Ogni elemento della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="fbe4a-113">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="fbe4a-114">Comando</span><span class="sxs-lookup"><span data-stu-id="fbe4a-114">Command</span></span> | <span data-ttu-id="fbe4a-115">Note</span><span class="sxs-lookup"><span data-stu-id="fbe4a-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fbe4a-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="fbe4a-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="fbe4a-117">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="fbe4a-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="fbe4a-118">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="fbe4a-118">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="fbe4a-119">Crea una configurazione di subnet.</span><span class="sxs-lookup"><span data-stu-id="fbe4a-119">Creates a subnet configuration.</span></span> <span data-ttu-id="fbe4a-120">Questa configurazione viene usata con il processo di creazione della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="fbe4a-120">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="fbe4a-121">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="fbe4a-121">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="fbe4a-122">Crea una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="fbe4a-122">Creates a virtual network.</span></span> |
| [<span data-ttu-id="fbe4a-123">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="fbe4a-123">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="fbe4a-124">Crea un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="fbe4a-124">Creates a public IP address.</span></span> |
| [<span data-ttu-id="fbe4a-125">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="fbe4a-125">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="fbe4a-126">Crea una configurazione di regola del gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="fbe4a-126">Creates a network security group rule configuration.</span></span> <span data-ttu-id="fbe4a-127">Questa configurazione viene usata per creare una regola NSG quando viene creato il gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="fbe4a-127">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="fbe4a-128">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="fbe4a-128">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="fbe4a-129">Crea un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="fbe4a-129">Creates a network security group.</span></span> |
| [<span data-ttu-id="fbe4a-130">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="fbe4a-130">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="fbe4a-131">Ottiene informazioni sulla subnet.</span><span class="sxs-lookup"><span data-stu-id="fbe4a-131">Gets subnet information.</span></span> <span data-ttu-id="fbe4a-132">Queste informazioni vengono usate durante la creazione di un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="fbe4a-132">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="fbe4a-133">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="fbe4a-133">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="fbe4a-134">Crea un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="fbe4a-134">Creates a network interface.</span></span> |
| [<span data-ttu-id="fbe4a-135">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="fbe4a-135">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="fbe4a-136">Crea una configurazione di VM.</span><span class="sxs-lookup"><span data-stu-id="fbe4a-136">Creates a VM configuration.</span></span> <span data-ttu-id="fbe4a-137">Questa configurazione include informazioni quali il nome della VM, il sistema operativo e le credenziali amministrative.</span><span class="sxs-lookup"><span data-stu-id="fbe4a-137">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="fbe4a-138">La configurazione viene usata durante la creazione della VM.</span><span class="sxs-lookup"><span data-stu-id="fbe4a-138">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="fbe4a-139">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="fbe4a-139">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="fbe4a-140">Creare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fbe4a-140">Create a virtual machine.</span></span> |
| [<span data-ttu-id="fbe4a-141">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="fbe4a-141">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="fbe4a-142">Aggiungere un'estensione di VM alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fbe4a-142">Add a VM extension to the virtual machine.</span></span> <span data-ttu-id="fbe4a-143">In questo caso, l'estensione dell'agente Operations Management Suite viene usata per installare l'agente OMS e registrare la VM in un'area di lavoro OMS.</span><span class="sxs-lookup"><span data-stu-id="fbe4a-143">In this case, the Operations Management Suite agent extension is used to install the OMS agent and enroll the VM in an OMS workspace.</span></span> |
|[<span data-ttu-id="fbe4a-144">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="fbe4a-144">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="fbe4a-145">Rimuove un gruppo di risorse e tutte le risorse contenute al suo interno.</span><span class="sxs-lookup"><span data-stu-id="fbe4a-145">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fbe4a-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fbe4a-146">Next steps</span></span>

<span data-ttu-id="fbe4a-147">Per altre informazioni sul modulo Azure PowerShell, vedere la [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fbe4a-147">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="fbe4a-148">Altri esempi di script PowerShell della macchina virtuale sono reperibili nella [documentazione della VM Windows di Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fbe4a-148">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
