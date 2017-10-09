---
title: aaaAzure Script di PowerShell di esempio - Docker | Documenti Microsoft
description: Esempio di script di Azure PowerShell - Docker
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
ms.date: 03/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 556093d3cfaecda352ff52cce96728fc0e723a39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-docker-host-with-powershell"></a><span data-ttu-id="c0f8a-103">Creare un host Docker con PowerShell</span><span class="sxs-lookup"><span data-stu-id="c0f8a-103">Create a Docker host with PowerShell</span></span>

<span data-ttu-id="c0f8a-104">Questo script crea una macchina virtuale con Docker abilitato e avvia un contenitore che esegue NGINX.</span><span class="sxs-lookup"><span data-stu-id="c0f8a-104">This script creates a virtual machine with Docker enabled and starts a container running NGINX.</span></span> <span data-ttu-id="c0f8a-105">Dopo l'esecuzione di script hello, è possibile accedere tramite hello FQDN di hello macchina virtuale di Azure con i server web NGINX di hello.</span><span class="sxs-lookup"><span data-stu-id="c0f8a-105">After running hello script, you can access hello NGINX web server through hello FQDN of hello Azure virtual machine.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="c0f8a-106">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="c0f8a-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-docker-host/create-docker-host.ps1 "Create Docker host")]

## <a name="clean-up-deployment"></a><span data-ttu-id="c0f8a-107">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="c0f8a-107">Clean up deployment</span></span> 

<span data-ttu-id="c0f8a-108">Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="c0f8a-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="c0f8a-109">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="c0f8a-109">Script explanation</span></span>

<span data-ttu-id="c0f8a-110">Questo script utilizza hello dopo la distribuzione di comandi toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="c0f8a-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="c0f8a-111">Ogni elemento nella documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="c0f8a-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c0f8a-112">Comando</span><span class="sxs-lookup"><span data-stu-id="c0f8a-112">Command</span></span> | <span data-ttu-id="c0f8a-113">Note</span><span class="sxs-lookup"><span data-stu-id="c0f8a-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c0f8a-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c0f8a-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="c0f8a-115">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="c0f8a-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c0f8a-116">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="c0f8a-116">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="c0f8a-117">Crea una configurazione di subnet.</span><span class="sxs-lookup"><span data-stu-id="c0f8a-117">Creates a subnet configuration.</span></span> <span data-ttu-id="c0f8a-118">Questa configurazione viene utilizzata con processo di creazione di hello rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="c0f8a-118">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="c0f8a-119">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="c0f8a-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="c0f8a-120">Crea una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="c0f8a-120">Creates a virtual network.</span></span> |
| [<span data-ttu-id="c0f8a-121">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="c0f8a-121">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="c0f8a-122">Crea un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="c0f8a-122">Creates a public IP address.</span></span> |
| [<span data-ttu-id="c0f8a-123">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="c0f8a-123">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="c0f8a-124">Crea una configurazione di regola del gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="c0f8a-124">Creates a network security group rule configuration.</span></span> <span data-ttu-id="c0f8a-125">Questa configurazione è toocreate utilizzata una regola di gruppo quando hello gruppo viene creato.</span><span class="sxs-lookup"><span data-stu-id="c0f8a-125">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="c0f8a-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="c0f8a-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="c0f8a-127">Crea un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="c0f8a-127">Creates a network security group.</span></span> |
| [<span data-ttu-id="c0f8a-128">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="c0f8a-128">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="c0f8a-129">Ottiene informazioni sulla subnet.</span><span class="sxs-lookup"><span data-stu-id="c0f8a-129">Gets subnet information.</span></span> <span data-ttu-id="c0f8a-130">Queste informazioni vengono usate durante la creazione di un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="c0f8a-130">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="c0f8a-131">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="c0f8a-131">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="c0f8a-132">Crea un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="c0f8a-132">Creates a network interface.</span></span> |
| [<span data-ttu-id="c0f8a-133">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="c0f8a-133">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="c0f8a-134">Crea una configurazione di VM.</span><span class="sxs-lookup"><span data-stu-id="c0f8a-134">Creates a VM configuration.</span></span> <span data-ttu-id="c0f8a-135">Questa configurazione include informazioni quali il nome della VM, il sistema operativo e le credenziali amministrative.</span><span class="sxs-lookup"><span data-stu-id="c0f8a-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="c0f8a-136">configurazione di Hello viene utilizzato durante la creazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c0f8a-136">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="c0f8a-137">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="c0f8a-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="c0f8a-138">Creare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c0f8a-138">Create a virtual machine.</span></span> |
| [<span data-ttu-id="c0f8a-139">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="c0f8a-139">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="c0f8a-140">Aggiungere una macchina virtuale VM estensione toohello.</span><span class="sxs-lookup"><span data-stu-id="c0f8a-140">Add a VM extension toohello virtual machine.</span></span> <span data-ttu-id="c0f8a-141">In questo esempio, hello estensione Docker è usato tooconfigure Docker ed esegue un contenitore Docker NGINX.</span><span class="sxs-lookup"><span data-stu-id="c0f8a-141">In this sample, hello Docker extension is used tooconfigure Docker and run an NGINX Docker container.</span></span> |
|[<span data-ttu-id="c0f8a-142">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c0f8a-142">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="c0f8a-143">Rimuove un gruppo di risorse e tutte le risorse contenute al suo interno.</span><span class="sxs-lookup"><span data-stu-id="c0f8a-143">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c0f8a-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c0f8a-144">Next steps</span></span>

<span data-ttu-id="c0f8a-145">Per ulteriori informazioni sul modulo di Azure PowerShell hello, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c0f8a-145">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="c0f8a-146">Esempi di script di PowerShell di macchina virtuale aggiuntiva sono reperibile in hello [documentazione VM Linux di Azure](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c0f8a-146">Additional virtual machine PowerShell script samples can be found in hello [Azure Linux VM documentation](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
