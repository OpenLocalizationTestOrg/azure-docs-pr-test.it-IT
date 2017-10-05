---
title: Caricare un disco rigido virtuale generalizzato in uno script PowerShell di esempio di Azure | Microsoft Docs
description: Script PowerShell di esempio per caricare un disco rigido virtuale generalizzato in Azure e creare una nuova macchina virtuale usando il modello di distribuzione di Resource Manager e i dischi gestiti.
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
ms.openlocfilehash: cd3d87bb4384971e28d3330cd5c1a3d351129036
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="sample-script-to-upload-a-vhd-to-azure-and-create-a-new-vm"></a><span data-ttu-id="d3b5b-103">Script di esempio per caricare un disco rigido virtuale in Azure e creare una nuova macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="d3b5b-103">Sample script to upload a VHD to Azure and create a new VM</span></span>

<span data-ttu-id="d3b5b-104">Questo script carica un file con estensione VHD locale da una macchina virtuale generalizzata in Azure, crea un'immagine del disco gestito e la usa per creare una nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d3b5b-104">This script takes a local .vhd file from a generalized VM and uploads it to Azure, creates a Managed Disk image and uses the to create a new VM.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="d3b5b-105">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="d3b5b-105">Sample script</span></span>

```powershell
# Provide values for the variables
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

# Get the username and password to be used for the administrators account on the VM. 
# This is used when connecting to the VM using RDP.

$cred = Get-Credential

# Upload the VHD
New-AzureRmResourceGroup -Name $resourceGroup -Location $location
New-AzureRmStorageAccount -ResourceGroupName $resourceGroup -Name $storageAccount -Location $location `
    -SkuName $storageType -Kind "Storage"
$urlOfUploadedImageVhd = ('https://' + $storageaccount + '.blob.core.windows.net/' + $containername + '/' + $vhdName)
Add-AzureRmVhd -ResourceGroupName $resourceGroup -Destination $urlOfUploadedImageVhd `
    -LocalFilePath $localPath

# Note: Uploading the VHD may take awhile!

# Create a managed image from the uploaded VHD 
$imageConfig = New-AzureRmImageConfig -Location $location
$imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized `
    -BlobUri $urlOfUploadedImageVhd
$image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $resourceGroup -Image $imageConfig
 
# Create the networking resources
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

# Start building the VM configuration
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

# Set the VM image as source image for the new VM
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id

# Finish the VM configuration and add the NIC.
$vm = Set-AzureRmVMOSDisk -VM $vm  -DiskSizeInGB $diskSizeGB -CreateOption FromImage -Caching ReadWrite
$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

# Create the VM
New-AzureRmVM -VM $vm -ResourceGroupName $resourceGroup -Location $location

# Verify that the VM was created
$vmList = Get-AzureRmVM -ResourceGroupName $resourceGroup
$vmList.Name


```


<!-- 
[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-iis/create-windows-vm-iis.ps1 "Create VM IIS")] -->

## <a name="clean-up-deployment"></a><span data-ttu-id="d3b5b-106">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="d3b5b-106">Clean up deployment</span></span> 

<span data-ttu-id="d3b5b-107">Eseguire questo comando per rimuovere il gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="d3b5b-107">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name $resourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="d3b5b-108">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="d3b5b-108">Script explanation</span></span>

<span data-ttu-id="d3b5b-109">Questo script usa i comandi seguenti per creare la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="d3b5b-109">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="d3b5b-110">Ogni elemento della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="d3b5b-110">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="d3b5b-111">Comando</span><span class="sxs-lookup"><span data-stu-id="d3b5b-111">Command</span></span>                                                                                                             | <span data-ttu-id="d3b5b-112">Note</span><span class="sxs-lookup"><span data-stu-id="d3b5b-112">Notes</span></span>                                                                                                                                                                                |
|---------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="d3b5b-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d3b5b-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)                           | <span data-ttu-id="d3b5b-114">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="d3b5b-114">Creates a resource group in which all resources are stored.</span></span>                                                                                                                          |
| [<span data-ttu-id="d3b5b-115">New-AzureRmStorageAccount</span><span class="sxs-lookup"><span data-stu-id="d3b5b-115">New-AzureRmStorageAccount</span></span>](/powershell/module/azurerm.resources/new-azurermstorageaccount)                         | <span data-ttu-id="d3b5b-116">Crea un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="d3b5b-116">Creates a storage account.</span></span>                                                                                                                                                           |
| [<span data-ttu-id="d3b5b-117">Add-AzureRmVhd</span><span class="sxs-lookup"><span data-stu-id="d3b5b-117">Add-AzureRmVhd</span></span>](/powershell/module/azurerm.resources/add-azurermvhd)                                               | <span data-ttu-id="d3b5b-118">Carica un disco rigido virtuale da una macchina virtuale locale in un BLOB in un account di archiviazione cloud in Azure.</span><span class="sxs-lookup"><span data-stu-id="d3b5b-118">Uploads a virtual hard disk from an on-premises virtual machine to a blob in a cloud storage account in Azure.</span></span>                                                                       |
| [<span data-ttu-id="d3b5b-119">New-AzureRmImageConfig</span><span class="sxs-lookup"><span data-stu-id="d3b5b-119">New-AzureRmImageConfig</span></span>](/powershell/module/azurerm.resources/new-azurermimageconfig)                               | <span data-ttu-id="d3b5b-120">Crea un oggetto dell'immagine configurabile.</span><span class="sxs-lookup"><span data-stu-id="d3b5b-120">Creates a configurable image object.</span></span>                                                                                                                                                 |
| [<span data-ttu-id="d3b5b-121">Set-AzureRmImageOsDisk</span><span class="sxs-lookup"><span data-stu-id="d3b5b-121">Set-AzureRmImageOsDisk</span></span>](/powershell/module/azurerm.resources/set-azurermimageosdisk)                               | <span data-ttu-id="d3b5b-122">Imposta le proprietà del disco del sistema operativo in un oggetto dell'immagine.</span><span class="sxs-lookup"><span data-stu-id="d3b5b-122">Sets the operating system disk properties on an image object.</span></span>                                                                                                                        |
| [<span data-ttu-id="d3b5b-123">New-AzureRmImage</span><span class="sxs-lookup"><span data-stu-id="d3b5b-123">New-AzureRmImage</span></span>](/powershell/module/azurerm.resources/new-azurermimage)                                           | <span data-ttu-id="d3b5b-124">Crea una nuova immagine.</span><span class="sxs-lookup"><span data-stu-id="d3b5b-124">Creates a new image.</span></span>                                                                                                                                                                 |
| [<span data-ttu-id="d3b5b-125">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="d3b5b-125">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.resources/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="d3b5b-126">Crea una configurazione di subnet.</span><span class="sxs-lookup"><span data-stu-id="d3b5b-126">Creates a subnet configuration.</span></span> <span data-ttu-id="d3b5b-127">Questa configurazione viene usata con il processo di creazione della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="d3b5b-127">This configuration is used with the virtual network creation process.</span></span>                                                                                |
| [<span data-ttu-id="d3b5b-128">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="d3b5b-128">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.resources/new-azurermvirtualnetwork)                         | <span data-ttu-id="d3b5b-129">Crea una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="d3b5b-129">Creates a virtual network.</span></span>                                                                                                                                                           |
| [<span data-ttu-id="d3b5b-130">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="d3b5b-130">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.resources/new-azurermpublicipaddress)                       | <span data-ttu-id="d3b5b-131">Crea un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="d3b5b-131">Creates a public IP address.</span></span>                                                                                                                                                         |
| [<span data-ttu-id="d3b5b-132">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="d3b5b-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.resources/new-azurermnetworkinterface)                     | <span data-ttu-id="d3b5b-133">Crea un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="d3b5b-133">Creates a network interface.</span></span>                                                                                                                                                         |
| [<span data-ttu-id="d3b5b-134">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="d3b5b-134">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.resources/new-azurermnetworksecurityruleconfig)   | <span data-ttu-id="d3b5b-135">Crea una configurazione di regola del gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="d3b5b-135">Creates a network security group rule configuration.</span></span> <span data-ttu-id="d3b5b-136">Questa configurazione viene usata per creare una regola NSG quando viene creato il gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="d3b5b-136">This configuration is used to create an NSG rule when the NSG is created.</span></span>                                                       |
| [<span data-ttu-id="d3b5b-137">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="d3b5b-137">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.resources/new-azurermnetworksecuritygroup)             | <span data-ttu-id="d3b5b-138">Crea un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="d3b5b-138">Creates a network security group.</span></span>                                                                                                                                                    |
| [<span data-ttu-id="d3b5b-139">Get-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="d3b5b-139">Get-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.resources/get-azurermvirtualnetwork)                         | <span data-ttu-id="d3b5b-140">Ottiene una rete virtuale in un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="d3b5b-140">Gets a virtual network in a resource group.</span></span>                                                                                                                                          |
| [<span data-ttu-id="d3b5b-141">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="d3b5b-141">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.resources/new-azurermvmconfig)                                     | <span data-ttu-id="d3b5b-142">Crea una configurazione di VM.</span><span class="sxs-lookup"><span data-stu-id="d3b5b-142">Creates a VM configuration.</span></span> <span data-ttu-id="d3b5b-143">Questa configurazione include informazioni quali il nome della VM, il sistema operativo e le credenziali amministrative.</span><span class="sxs-lookup"><span data-stu-id="d3b5b-143">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="d3b5b-144">La configurazione viene usata durante la creazione della VM.</span><span class="sxs-lookup"><span data-stu-id="d3b5b-144">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="d3b5b-145">Set-AzureRmVMSourceImage</span><span class="sxs-lookup"><span data-stu-id="d3b5b-145">Set-AzureRmVMSourceImage</span></span>](/powershell/module/azurerm.resources/set-azurermvmsourceimage)                           | <span data-ttu-id="d3b5b-146">Specifica un'immagine per una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d3b5b-146">Specifies an image for a virtual machine.</span></span>                                                                                                                                            |
| [<span data-ttu-id="d3b5b-147">Set-AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="d3b5b-147">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.resources/set-azurermvmosdisk)                                     | <span data-ttu-id="d3b5b-148">Imposta le proprietà del disco del sistema operativo sulla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d3b5b-148">Sets the operating system disk properties on a virtual machine.</span></span>                                                                                                                      |
| [<span data-ttu-id="d3b5b-149">Set-AzureRmVMOperatingSystem</span><span class="sxs-lookup"><span data-stu-id="d3b5b-149">Set-AzureRmVMOperatingSystem</span></span>](/powershell/module/azurerm.resources/set-azurermvmoperatingsystem)                   | <span data-ttu-id="d3b5b-150">Imposta le proprietà del disco del sistema operativo sulla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d3b5b-150">Sets the operating system disk properties on a virtual machine.</span></span>                                                                                                                      |
| [<span data-ttu-id="d3b5b-151">Add-AzureRmVMNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="d3b5b-151">Add-AzureRmVMNetworkInterface</span></span>](/powershell/module/azurerm.resources/add-azurermvmnetworkinterface)                 | <span data-ttu-id="d3b5b-152">Aggiungere un'interfaccia di rete a una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d3b5b-152">Adds a network interface to a virtual machine.</span></span>                                                                                                                                       |
| [<span data-ttu-id="d3b5b-153">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="d3b5b-153">New-AzureRmVM</span></span>](/powershell/module/azurerm.resources/new-azurermvm)                                                 | <span data-ttu-id="d3b5b-154">Creare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d3b5b-154">Create a virtual machine.</span></span>                                                                                                                                                            |
| [<span data-ttu-id="d3b5b-155">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d3b5b-155">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup)                     | <span data-ttu-id="d3b5b-156">Rimuove un gruppo di risorse e tutte le risorse contenute al suo interno.</span><span class="sxs-lookup"><span data-stu-id="d3b5b-156">Removes a resource group and all resources contained within.</span></span>                                                                                                                         |

## <a name="next-steps"></a><span data-ttu-id="d3b5b-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d3b5b-157">Next steps</span></span>

<span data-ttu-id="d3b5b-158">Per altre informazioni sul modulo Azure PowerShell, vedere la [documentazione di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d3b5b-158">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="d3b5b-159">Altri esempi di script PowerShell della macchina virtuale sono reperibili nella [documentazione della VM Windows di Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d3b5b-159">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
