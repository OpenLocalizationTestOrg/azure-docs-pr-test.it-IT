---
title: aaaUpload un tooAzure VHD generalizzato di esempio di Script di PowerShell | Documenti Microsoft
description: PowerShell di esempio tooupload script un tooAzure disco rigido virtuale generalizzato e creare una nuova macchina virtuale utilizzando il modello di distribuzione Gestione risorse di hello e dischi gestiti.
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/18/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 72b4ff09eb7a6ba1604b9d5cbac51e60eded7545
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sample-script-tooupload-a-vhd-tooazure-and-create-a-new-vm"></a><span data-ttu-id="13200-103">Esempio di script tooupload tooAzure un disco rigido virtuale e creare una nuova macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="13200-103">Sample script tooupload a VHD tooAzure and create a new VM</span></span>

<span data-ttu-id="13200-104">Questo script accetta un file con estensione vhd locale da una macchina virtuale generalizzata e lo carica tooAzure, crea un'immagine del disco gestito e Usa hello toocreate una nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="13200-104">This script takes a local .vhd file from a generalized VM and uploads it tooAzure, creates a Managed Disk image and uses hello toocreate a new VM.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="13200-105">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="13200-105">Sample script</span></span>

```powershell
# Provide values for hello variables
$resourceGroup = 'myResourceGroup'
$location = 'EastUS'
$storageaccount = 'mystorageaccount'
$storageType = 'Standard_LRS'
$containername = 'mycontainer'
$localPath = 'C:\Users\Public\Documents\Hyper-V\VHDs\generalized.vhd'
$vmName = 'myVM'
$imageName = 'myImage'
$vhdName = 'myUploadedVhd.vhd'
$diskSizeGB = '128'
$subnetName = 'mySubnet'
$vnetName = 'myVnet'
$ipName = 'myPip'
$nicName = 'myNic'
$nsgName = 'myNsg'
$ruleName = 'myRdpRule'
$vmName = 'myVM'
$computerName = 'myComputerName'
$vmSize = 'Standard_DS1_v2'

# Get hello username and password toobe used for hello administrators account on hello VM. 
# This is used when connecting toohello VM using RDP.

$cred = Get-Credential

# Upload hello VHD
New-AzureRmResourceGroup -Name $resourceGroup -Location $location
New-AzureRmStorageAccount -ResourceGroupName $resourceGroup -Name $storageAccount -Location $location `
    -SkuName $storageType -Kind "Storage"
$urlOfUploadedImageVhd = ('https://' + $storageaccount + '.blob.core.windows.net/' + $containername + '/' + $vhdName)
Add-AzureRmVhd -ResourceGroupName $resourceGroup -Destination $urlOfUploadedImageVhd `
    -LocalFilePath $localPath

# Note: Uploading hello VHD may take awhile!

# Create a managed image from hello uploaded VHD 
$imageConfig = New-AzureRmImageConfig -Location $location
$imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized `
    -BlobUri $urlOfUploadedImageVhd
$image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $resourceGroup -Image $imageConfig
 
# Create hello networking resources
$singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroup -Location $location `
    -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
$pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $resourceGroup -Location $location `
    -AllocationMethod Dynamic
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $resourceGroup -Location $location `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description 'Allow RDP' -Access Allow `
    -Protocol Tcp -Direction Inbound -Priority 110 -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $resourceGroup -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $resourceGroup -Name $vnetName

# Start building hello VM configuration
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

# Set hello VM image as source image for hello new VM
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id

# Finish hello VM configuration and add hello NIC.
$vm = Set-AzureRmVMOSDisk -VM $vm  -DiskSizeInGB $diskSizeGB -CreateOption FromImage -Caching ReadWrite
$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

# Create hello VM
New-AzureRmVM -VM $vm -ResourceGroupName $resourceGroup -Location $location

# Verify that hello VM was created
$vmList = Get-AzureRmVM -ResourceGroupName $resourceGroup
$vmList.Name


```


<!-- 
[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-iis/create-windows-vm-iis.ps1 "Create VM IIS")] -->

## <a name="clean-up-deployment"></a><span data-ttu-id="13200-106">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="13200-106">Clean up deployment</span></span> 

<span data-ttu-id="13200-107">Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="13200-107">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name $resourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="13200-108">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="13200-108">Script explanation</span></span>

<span data-ttu-id="13200-109">Questo script utilizza hello dopo la distribuzione di comandi toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="13200-109">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="13200-110">Ogni elemento nella documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="13200-110">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="13200-111">Comando</span><span class="sxs-lookup"><span data-stu-id="13200-111">Command</span></span>                                                                                                             | <span data-ttu-id="13200-112">Note</span><span class="sxs-lookup"><span data-stu-id="13200-112">Notes</span></span>                                                                                                                                                                                |
|---------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="13200-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="13200-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)                           | <span data-ttu-id="13200-114">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="13200-114">Creates a resource group in which all resources are stored.</span></span>                                                                                                                          |
| [<span data-ttu-id="13200-115">New-AzureRmStorageAccount</span><span class="sxs-lookup"><span data-stu-id="13200-115">New-AzureRmStorageAccount</span></span>](/powershell/module/azurerm.resources/new-azurermstorageaccount)                         | <span data-ttu-id="13200-116">Crea un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="13200-116">Creates a storage account.</span></span>                                                                                                                                                           |
| [<span data-ttu-id="13200-117">Add-AzureRmVhd</span><span class="sxs-lookup"><span data-stu-id="13200-117">Add-AzureRmVhd</span></span>](/powershell/module/azurerm.resources/add-azurermvhd)                                               | <span data-ttu-id="13200-118">Carica un disco rigido virtuale da un blob di tooa macchina virtuale locale in un account di archiviazione cloud in Azure.</span><span class="sxs-lookup"><span data-stu-id="13200-118">Uploads a virtual hard disk from an on-premises virtual machine tooa blob in a cloud storage account in Azure.</span></span>                                                                       |
| [<span data-ttu-id="13200-119">New-AzureRmImageConfig</span><span class="sxs-lookup"><span data-stu-id="13200-119">New-AzureRmImageConfig</span></span>](/powershell/module/azurerm.resources/new-azurermimageconfig)                               | <span data-ttu-id="13200-120">Crea un oggetto dell'immagine configurabile.</span><span class="sxs-lookup"><span data-stu-id="13200-120">Creates a configurable image object.</span></span>                                                                                                                                                 |
| [<span data-ttu-id="13200-121">Set-AzureRmImageOsDisk</span><span class="sxs-lookup"><span data-stu-id="13200-121">Set-AzureRmImageOsDisk</span></span>](/powershell/module/azurerm.resources/set-azurermimageosdisk)                               | <span data-ttu-id="13200-122">Imposta proprietà del disco di hello del sistema operativo su un oggetto immagine.</span><span class="sxs-lookup"><span data-stu-id="13200-122">Sets hello operating system disk properties on an image object.</span></span>                                                                                                                        |
| [<span data-ttu-id="13200-123">New-AzureRmImage</span><span class="sxs-lookup"><span data-stu-id="13200-123">New-AzureRmImage</span></span>](/powershell/module/azurerm.resources/new-azurermimage)                                           | <span data-ttu-id="13200-124">Crea una nuova immagine.</span><span class="sxs-lookup"><span data-stu-id="13200-124">Creates a new image.</span></span>                                                                                                                                                                 |
| [<span data-ttu-id="13200-125">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="13200-125">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.resources/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="13200-126">Crea una configurazione di subnet.</span><span class="sxs-lookup"><span data-stu-id="13200-126">Creates a subnet configuration.</span></span> <span data-ttu-id="13200-127">Questa configurazione viene utilizzata con processo di creazione di hello rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="13200-127">This configuration is used with hello virtual network creation process.</span></span>                                                                                |
| [<span data-ttu-id="13200-128">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="13200-128">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.resources/new-azurermvirtualnetwork)                         | <span data-ttu-id="13200-129">Crea una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="13200-129">Creates a virtual network.</span></span>                                                                                                                                                           |
| [<span data-ttu-id="13200-130">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="13200-130">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.resources/new-azurermpublicipaddress)                       | <span data-ttu-id="13200-131">Crea un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="13200-131">Creates a public IP address.</span></span>                                                                                                                                                         |
| [<span data-ttu-id="13200-132">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="13200-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.resources/new-azurermnetworkinterface)                     | <span data-ttu-id="13200-133">Crea un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="13200-133">Creates a network interface.</span></span>                                                                                                                                                         |
| [<span data-ttu-id="13200-134">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="13200-134">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.resources/new-azurermnetworksecurityruleconfig)   | <span data-ttu-id="13200-135">Crea una configurazione di regola del gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="13200-135">Creates a network security group rule configuration.</span></span> <span data-ttu-id="13200-136">Questa configurazione è toocreate utilizzata una regola di gruppo quando hello gruppo viene creato.</span><span class="sxs-lookup"><span data-stu-id="13200-136">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span>                                                       |
| [<span data-ttu-id="13200-137">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="13200-137">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.resources/new-azurermnetworksecuritygroup)             | <span data-ttu-id="13200-138">Crea un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="13200-138">Creates a network security group.</span></span>                                                                                                                                                    |
| [<span data-ttu-id="13200-139">Get-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="13200-139">Get-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.resources/get-azurermvirtualnetwork)                         | <span data-ttu-id="13200-140">Ottiene una rete virtuale in un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="13200-140">Gets a virtual network in a resource group.</span></span>                                                                                                                                          |
| [<span data-ttu-id="13200-141">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="13200-141">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.resources/new-azurermvmconfig)                                     | <span data-ttu-id="13200-142">Crea una configurazione di VM.</span><span class="sxs-lookup"><span data-stu-id="13200-142">Creates a VM configuration.</span></span> <span data-ttu-id="13200-143">Questa configurazione include informazioni quali il nome della VM, il sistema operativo e le credenziali amministrative.</span><span class="sxs-lookup"><span data-stu-id="13200-143">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="13200-144">configurazione di Hello viene utilizzato durante la creazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="13200-144">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="13200-145">Set-AzureRmVMSourceImage</span><span class="sxs-lookup"><span data-stu-id="13200-145">Set-AzureRmVMSourceImage</span></span>](/powershell/module/azurerm.resources/set-azurermvmsourceimage)                           | <span data-ttu-id="13200-146">Specifica un'immagine per una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="13200-146">Specifies an image for a virtual machine.</span></span>                                                                                                                                            |
| [<span data-ttu-id="13200-147">Set-AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="13200-147">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.resources/set-azurermvmosdisk)                                     | <span data-ttu-id="13200-148">Imposta proprietà del disco di hello del sistema operativo in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="13200-148">Sets hello operating system disk properties on a virtual machine.</span></span>                                                                                                                      |
| [<span data-ttu-id="13200-149">Set-AzureRmVMOperatingSystem</span><span class="sxs-lookup"><span data-stu-id="13200-149">Set-AzureRmVMOperatingSystem</span></span>](/powershell/module/azurerm.resources/set-azurermvmoperatingsystem)                   | <span data-ttu-id="13200-150">Imposta proprietà del disco di hello del sistema operativo in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="13200-150">Sets hello operating system disk properties on a virtual machine.</span></span>                                                                                                                      |
| [<span data-ttu-id="13200-151">Add-AzureRmVMNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="13200-151">Add-AzureRmVMNetworkInterface</span></span>](/powershell/module/azurerm.resources/add-azurermvmnetworkinterface)                 | <span data-ttu-id="13200-152">Aggiunge una macchina di virtuale tooa interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="13200-152">Adds a network interface tooa virtual machine.</span></span>                                                                                                                                       |
| [<span data-ttu-id="13200-153">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="13200-153">New-AzureRmVM</span></span>](/powershell/module/azurerm.resources/new-azurermvm)                                                 | <span data-ttu-id="13200-154">Creare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="13200-154">Create a virtual machine.</span></span>                                                                                                                                                            |
| [<span data-ttu-id="13200-155">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="13200-155">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup)                     | <span data-ttu-id="13200-156">Rimuove un gruppo di risorse e tutte le risorse contenute al suo interno.</span><span class="sxs-lookup"><span data-stu-id="13200-156">Removes a resource group and all resources contained within.</span></span>                                                                                                                         |

## <a name="next-steps"></a><span data-ttu-id="13200-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="13200-157">Next steps</span></span>

<span data-ttu-id="13200-158">Per ulteriori informazioni sul modulo di Azure PowerShell hello, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="13200-158">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="13200-159">Esempi di script di PowerShell di macchina virtuale aggiuntiva sono reperibile in hello [documentazione macchina virtuale Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="13200-159">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
