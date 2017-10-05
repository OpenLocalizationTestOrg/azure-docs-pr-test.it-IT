---
title: Esempio di script di Azure PowerShell - IIS con DSC | Microsoft Docs
description: Esempio di script di Azure PowerShell - IIS con DSC
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
ms.date: 03/01/2017
ms.author: nepeters
ms.openlocfilehash: 38476119c88aa7d4f6578fc1e3756e11951e804a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-iis-vm-with-powershell"></a><span data-ttu-id="c52d7-103">Creare una VM IIS con PowerShell</span><span class="sxs-lookup"><span data-stu-id="c52d7-103">Create an IIS VM with PowerShell</span></span>

<span data-ttu-id="c52d7-104">Questo script crea una macchina virtuale di Azure con Windows Server 2016 e usa l'estensione DSC di Macchina virtuale di Azure per installare IIS.</span><span class="sxs-lookup"><span data-stu-id="c52d7-104">This script creates an Azure Virtual Machine running Windows Server 2016, and then uses the Azure Virtual Machine DSC Extension to install IIS.</span></span> <span data-ttu-id="c52d7-105">Dopo l'esecuzione dello script, è possibile accedere al sito Web IIS predefinito tramite l'indirizzo IP pubblico della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c52d7-105">After running the script, you can access the default IIS website on the public IP address of the virtual machine.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="c52d7-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="c52d7-106">Sample script</span></span>

<span data-ttu-id="c52d7-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-dsc/create-windows-vm-iis-dsc.ps1 "Creare una VM IIS DSC")]</span><span class="sxs-lookup"><span data-stu-id="c52d7-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-dsc/create-windows-vm-iis-dsc.ps1 "Create VM IIS DSC")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="c52d7-108">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="c52d7-108">Clean up deployment</span></span> 

<span data-ttu-id="c52d7-109">Eseguire questo comando per rimuovere il gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="c52d7-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="c52d7-110">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="c52d7-110">Script explanation</span></span>

<span data-ttu-id="c52d7-111">Questo script usa i comandi seguenti per creare la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="c52d7-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="c52d7-112">Ogni elemento della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="c52d7-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="c52d7-113">Comando</span><span class="sxs-lookup"><span data-stu-id="c52d7-113">Command</span></span> | <span data-ttu-id="c52d7-114">Note</span><span class="sxs-lookup"><span data-stu-id="c52d7-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c52d7-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c52d7-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="c52d7-116">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="c52d7-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c52d7-117">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="c52d7-117">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="c52d7-118">Crea una configurazione di subnet.</span><span class="sxs-lookup"><span data-stu-id="c52d7-118">Creates a subnet configuration.</span></span> <span data-ttu-id="c52d7-119">Questa configurazione viene usata con il processo di creazione della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="c52d7-119">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="c52d7-120">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="c52d7-120">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="c52d7-121">Crea una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="c52d7-121">Creates a virtual network.</span></span> |
| [<span data-ttu-id="c52d7-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="c52d7-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="c52d7-123">Crea un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="c52d7-123">Creates a public IP address.</span></span> |
| [<span data-ttu-id="c52d7-124">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="c52d7-124">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="c52d7-125">Crea una configurazione di regola del gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="c52d7-125">Creates a network security group rule configuration.</span></span> <span data-ttu-id="c52d7-126">Questa configurazione viene usata per creare una regola NSG quando viene creato il gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="c52d7-126">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="c52d7-127">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="c52d7-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="c52d7-128">Crea un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="c52d7-128">Creates a network security group.</span></span> |
| [<span data-ttu-id="c52d7-129">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="c52d7-129">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="c52d7-130">Ottiene informazioni sulla subnet.</span><span class="sxs-lookup"><span data-stu-id="c52d7-130">Gets subnet information.</span></span> <span data-ttu-id="c52d7-131">Queste informazioni vengono usate durante la creazione di un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="c52d7-131">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="c52d7-132">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="c52d7-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="c52d7-133">Crea un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="c52d7-133">Creates a network interface.</span></span> |
| [<span data-ttu-id="c52d7-134">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="c52d7-134">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="c52d7-135">Crea una configurazione di VM.</span><span class="sxs-lookup"><span data-stu-id="c52d7-135">Creates a VM configuration.</span></span> <span data-ttu-id="c52d7-136">Questa configurazione include informazioni quali il nome della VM, il sistema operativo e le credenziali amministrative.</span><span class="sxs-lookup"><span data-stu-id="c52d7-136">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="c52d7-137">La configurazione viene usata durante la creazione della VM.</span><span class="sxs-lookup"><span data-stu-id="c52d7-137">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="c52d7-138">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="c52d7-138">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="c52d7-139">Creare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c52d7-139">Create a virtual machine.</span></span> |
| [<span data-ttu-id="c52d7-140">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="c52d7-140">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="c52d7-141">Aggiungere un'estensione di VM alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c52d7-141">Add a VM extension to the virtual machine.</span></span> <span data-ttu-id="c52d7-142">In questo esempio, l'estensione dello script personalizzato è usata per installare IIS.</span><span class="sxs-lookup"><span data-stu-id="c52d7-142">In this sample, the custom script extension is used to install IIS.</span></span> |
|[<span data-ttu-id="c52d7-143">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c52d7-143">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="c52d7-144">Rimuove un gruppo di risorse e tutte le risorse contenute al suo interno.</span><span class="sxs-lookup"><span data-stu-id="c52d7-144">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c52d7-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c52d7-145">Next steps</span></span>

<span data-ttu-id="c52d7-146">Per altre informazioni sul modulo Azure PowerShell, vedere la [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c52d7-146">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="c52d7-147">Altri esempi di script PowerShell della macchina virtuale sono reperibili nella [documentazione della VM Windows di Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c52d7-147">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
