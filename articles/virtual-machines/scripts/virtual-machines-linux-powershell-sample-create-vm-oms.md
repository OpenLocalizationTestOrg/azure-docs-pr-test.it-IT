---
title: Esempio di script di Azure PowerShell - OMS | Microsoft Docs
description: Esempio di script di Azure PowerShell - OMS
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/01/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: cd23f71221efb62d2547b2b683ca8e2218403a2d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-operations-management-suite-monitored-vm-with-powershell"></a><span data-ttu-id="06128-103">Creare una VM monitorata da Operations Management Suite con PowerShell</span><span class="sxs-lookup"><span data-stu-id="06128-103">Create an Operations Management Suite monitored VM with PowerShell</span></span>

<span data-ttu-id="06128-104">Questo script consente di creare una macchina virtuale di Azure, installare l'agente Operations Management Suite (OMS) e registrare il sistema in un'area di lavoro OMS.</span><span class="sxs-lookup"><span data-stu-id="06128-104">This script creates an Azure Virtual Machine, installs the Operations Management Suite (OMS) agent, and enrolls the system with an OMS workspace.</span></span> <span data-ttu-id="06128-105">Dopo l'esecuzione dello script, la macchina virtuale sarà visibile nella console di OMS.</span><span class="sxs-lookup"><span data-stu-id="06128-105">Once the script has run, the virtual machine will be visible in the OMS console.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="06128-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="06128-106">Sample script</span></span>

<span data-ttu-id="06128-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-monitor-oms/create-vm-monitor-oms.ps1 "Creare una VM OMS")]</span><span class="sxs-lookup"><span data-stu-id="06128-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-monitor-oms/create-vm-monitor-oms.ps1 "Create VM OMS")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="06128-108">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="06128-108">Clean up deployment</span></span> 

<span data-ttu-id="06128-109">Eseguire questo comando per rimuovere il gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="06128-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="06128-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="06128-110">Script explanation</span></span>

<span data-ttu-id="06128-111">Questo script usa i comandi seguenti per creare la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="06128-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="06128-112">Ogni elemento della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="06128-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="06128-113">Comando</span><span class="sxs-lookup"><span data-stu-id="06128-113">Command</span></span> | <span data-ttu-id="06128-114">Note</span><span class="sxs-lookup"><span data-stu-id="06128-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="06128-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="06128-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="06128-116">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="06128-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="06128-117">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="06128-117">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="06128-118">Crea una configurazione di subnet.</span><span class="sxs-lookup"><span data-stu-id="06128-118">Creates a subnet configuration.</span></span> <span data-ttu-id="06128-119">Questa configurazione viene usata con il processo di creazione della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="06128-119">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="06128-120">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="06128-120">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="06128-121">Crea una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="06128-121">Creates a virtual network.</span></span> |
| [<span data-ttu-id="06128-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="06128-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="06128-123">Crea un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="06128-123">Creates a public IP address.</span></span> |
| [<span data-ttu-id="06128-124">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="06128-124">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="06128-125">Crea una configurazione di regola del gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="06128-125">Creates a network security group rule configuration.</span></span> <span data-ttu-id="06128-126">Questa configurazione viene usata per creare una regola NSG quando viene creato il gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="06128-126">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="06128-127">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="06128-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="06128-128">Crea un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="06128-128">Creates a network security group.</span></span> |
| [<span data-ttu-id="06128-129">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="06128-129">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="06128-130">Ottiene informazioni sulla subnet.</span><span class="sxs-lookup"><span data-stu-id="06128-130">Gets subnet information.</span></span> <span data-ttu-id="06128-131">Queste informazioni vengono usate durante la creazione di un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="06128-131">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="06128-132">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="06128-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="06128-133">Crea un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="06128-133">Creates a network interface.</span></span> |
| [<span data-ttu-id="06128-134">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="06128-134">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="06128-135">Crea una configurazione di VM.</span><span class="sxs-lookup"><span data-stu-id="06128-135">Creates a VM configuration.</span></span> <span data-ttu-id="06128-136">Questa configurazione include informazioni quali il nome della VM, il sistema operativo e le credenziali amministrative.</span><span class="sxs-lookup"><span data-stu-id="06128-136">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="06128-137">La configurazione viene usata durante la creazione della VM.</span><span class="sxs-lookup"><span data-stu-id="06128-137">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="06128-138">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="06128-138">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="06128-139">Creare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="06128-139">Create a virtual machine.</span></span> |
| [<span data-ttu-id="06128-140">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="06128-140">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="06128-141">Aggiungere un'estensione di VM alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="06128-141">Add a VM extension to the virtual machine.</span></span> <span data-ttu-id="06128-142">In questo caso, l'estensione dell'agente Operations Management Suite viene usata per installare l'agente OMS e registrare la VM in un'area di lavoro OMS.</span><span class="sxs-lookup"><span data-stu-id="06128-142">In this case, the Operations Management Suite agent extension is used to install the OMS agent and enroll the VM in an OMS workspace.</span></span> |
|[<span data-ttu-id="06128-143">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="06128-143">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="06128-144">Rimuove un gruppo di risorse e tutte le risorse contenute al suo interno.</span><span class="sxs-lookup"><span data-stu-id="06128-144">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="06128-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="06128-145">Next steps</span></span>

<span data-ttu-id="06128-146">Per altre informazioni sul modulo Azure PowerShell, vedere la [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="06128-146">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="06128-147">Altri esempi di script PowerShell per la macchina virtuale sono reperibili nella [documentazione della VM Linux di Azure](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="06128-147">Additional virtual machine PowerShell script samples can be found in the [Azure Linux VM documentation](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
