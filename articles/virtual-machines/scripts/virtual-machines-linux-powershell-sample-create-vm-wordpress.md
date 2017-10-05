---
title: Esempio di script di Azure PowerShell - WordPress | Microsoft Docs
description: Esempio di script di Azure PowerShell - WordPress
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
ms.openlocfilehash: 778a6d5cfc63f80aa66654d682fedb178cfd67a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-wordpress-vm-with-powershell"></a><span data-ttu-id="17e36-103">Creare una VM WordPress con PowerShell</span><span class="sxs-lookup"><span data-stu-id="17e36-103">Create a WordPress VM with PowerShell</span></span>

<span data-ttu-id="17e36-104">Questo script crea una macchina virtuale e usa l'estensione di script personalizzata della macchina virtuale di Azure per installare WordPress.</span><span class="sxs-lookup"><span data-stu-id="17e36-104">This script creates a virtual machine and uses the Azure Virtual Machine custom script extension to install WordPress.</span></span> <span data-ttu-id="17e36-105">Dopo aver eseguito lo script, è possibile accedere al sito di configurazione di WordPress in `http://<public IP of VM>/wordpress`.</span><span class="sxs-lookup"><span data-stu-id="17e36-105">After running the script, you can access the WordPress configuration site at  `http://<public IP of VM>/wordpress`.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="17e36-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="17e36-106">Sample script</span></span>

<span data-ttu-id="17e36-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-wordpress-mysql/create-wordpress-mysql.ps1 "Creare una VM WordPress")]</span><span class="sxs-lookup"><span data-stu-id="17e36-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-wordpress-mysql/create-wordpress-mysql.ps1 "Create VM WordPress")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="17e36-108">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="17e36-108">Clean up deployment</span></span> 

<span data-ttu-id="17e36-109">Eseguire questo comando per rimuovere il gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="17e36-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="17e36-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="17e36-110">Script explanation</span></span>

<span data-ttu-id="17e36-111">Questo script usa i comandi seguenti per creare la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="17e36-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="17e36-112">Ogni elemento della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="17e36-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="17e36-113">Comando</span><span class="sxs-lookup"><span data-stu-id="17e36-113">Command</span></span> | <span data-ttu-id="17e36-114">Note</span><span class="sxs-lookup"><span data-stu-id="17e36-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="17e36-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="17e36-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="17e36-116">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="17e36-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="17e36-117">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="17e36-117">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="17e36-118">Crea una configurazione di subnet.</span><span class="sxs-lookup"><span data-stu-id="17e36-118">Creates a subnet configuration.</span></span> <span data-ttu-id="17e36-119">Questa configurazione viene usata con il processo di creazione della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="17e36-119">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="17e36-120">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="17e36-120">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="17e36-121">Crea una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="17e36-121">Creates a virtual network.</span></span> |
| [<span data-ttu-id="17e36-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="17e36-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="17e36-123">Crea un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="17e36-123">Creates a public IP address.</span></span> |
| [<span data-ttu-id="17e36-124">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="17e36-124">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="17e36-125">Crea una configurazione di regola del gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="17e36-125">Creates a network security group rule configuration.</span></span> <span data-ttu-id="17e36-126">Questa configurazione viene usata per creare una regola NSG quando viene creato il gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="17e36-126">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="17e36-127">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="17e36-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="17e36-128">Crea un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="17e36-128">Creates a network security group.</span></span> |
| [<span data-ttu-id="17e36-129">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="17e36-129">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="17e36-130">Ottiene informazioni sulla subnet.</span><span class="sxs-lookup"><span data-stu-id="17e36-130">Gets subnet information.</span></span> <span data-ttu-id="17e36-131">Queste informazioni vengono usate durante la creazione di un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="17e36-131">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="17e36-132">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="17e36-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="17e36-133">Crea un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="17e36-133">Creates a network interface.</span></span> |
| [<span data-ttu-id="17e36-134">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="17e36-134">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="17e36-135">Crea una configurazione di VM.</span><span class="sxs-lookup"><span data-stu-id="17e36-135">Creates a VM configuration.</span></span> <span data-ttu-id="17e36-136">Questa configurazione include informazioni quali il nome della VM, il sistema operativo e le credenziali amministrative.</span><span class="sxs-lookup"><span data-stu-id="17e36-136">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="17e36-137">La configurazione viene usata durante la creazione della VM.</span><span class="sxs-lookup"><span data-stu-id="17e36-137">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="17e36-138">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="17e36-138">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="17e36-139">Creare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="17e36-139">Create a virtual machine.</span></span> |
| [<span data-ttu-id="17e36-140">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="17e36-140">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="17e36-141">Consente di aggiungere l'estensione di script personalizzata alla macchina virtuale che richiama uno script per installare WordPress.</span><span class="sxs-lookup"><span data-stu-id="17e36-141">Add the Custom Script Extension to the virtual machine, which invokes a script to install WordPress.</span></span> |
|[<span data-ttu-id="17e36-142">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="17e36-142">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="17e36-143">Rimuove un gruppo di risorse e tutte le risorse contenute al suo interno.</span><span class="sxs-lookup"><span data-stu-id="17e36-143">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="17e36-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="17e36-144">Next steps</span></span>

<span data-ttu-id="17e36-145">Per altre informazioni sul modulo Azure PowerShell, vedere la [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="17e36-145">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="17e36-146">Altri esempi di script PowerShell per la macchina virtuale sono reperibili nella [documentazione della VM Linux di Azure](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="17e36-146">Additional virtual machine PowerShell script samples can be found in the [Azure Linux VM documentation](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
