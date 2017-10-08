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
# <a name="sample-script-tooupload-a-vhd-tooazure-and-create-a-new-vm"></a>Esempio di script tooupload tooAzure un disco rigido virtuale e creare una nuova macchina virtuale

Questo script accetta un file con estensione vhd locale da una macchina virtuale generalizzata e lo carica tooAzure, crea un'immagine del disco gestito e Usa hello toocreate una nuova macchina virtuale.

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script di esempio

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

## <a name="clean-up-deployment"></a>Pulire la distribuzione 

Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.

```powershell
Remove-AzureRmResourceGroup -Name $resourceGroup
```

## <a name="script-explanation"></a>Spiegazione dello script

Questo script utilizza hello dopo la distribuzione di comandi toocreate hello. Ogni elemento nella documentazione specifica toocommand hello tabella collegamenti.

| Comando                                                                                                             | Note                                                                                                                                                                                |
|---------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)                           | Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.                                                                                                                          |
| [New-AzureRmStorageAccount](/powershell/module/azurerm.resources/new-azurermstorageaccount)                         | Crea un account di archiviazione.                                                                                                                                                           |
| [Add-AzureRmVhd](/powershell/module/azurerm.resources/add-azurermvhd)                                               | Carica un disco rigido virtuale da un blob di tooa macchina virtuale locale in un account di archiviazione cloud in Azure.                                                                       |
| [New-AzureRmImageConfig](/powershell/module/azurerm.resources/new-azurermimageconfig)                               | Crea un oggetto dell'immagine configurabile.                                                                                                                                                 |
| [Set-AzureRmImageOsDisk](/powershell/module/azurerm.resources/set-azurermimageosdisk)                               | Imposta proprietà del disco di hello del sistema operativo su un oggetto immagine.                                                                                                                        |
| [New-AzureRmImage](/powershell/module/azurerm.resources/new-azurermimage)                                           | Crea una nuova immagine.                                                                                                                                                                 |
| [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.resources/new-azurermvirtualnetworksubnetconfig) | Crea una configurazione di subnet. Questa configurazione viene utilizzata con processo di creazione di hello rete virtuale.                                                                                |
| [New-AzureRmVirtualNetwork](/powershell/module/azurerm.resources/new-azurermvirtualnetwork)                         | Crea una rete virtuale.                                                                                                                                                           |
| [New-AzureRmPublicIpAddress](/powershell/module/azurerm.resources/new-azurermpublicipaddress)                       | Crea un indirizzo IP pubblico.                                                                                                                                                         |
| [New-AzureRmNetworkInterface](/powershell/module/azurerm.resources/new-azurermnetworkinterface)                     | Crea un'interfaccia di rete.                                                                                                                                                         |
| [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.resources/new-azurermnetworksecurityruleconfig)   | Crea una configurazione di regola del gruppo di sicurezza di rete. Questa configurazione è toocreate utilizzata una regola di gruppo quando hello gruppo viene creato.                                                       |
| [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.resources/new-azurermnetworksecuritygroup)             | Crea un gruppo di sicurezza di rete.                                                                                                                                                    |
| [Get-AzureRmVirtualNetwork](/powershell/module/azurerm.resources/get-azurermvirtualnetwork)                         | Ottiene una rete virtuale in un gruppo di risorse.                                                                                                                                          |
| [New-AzureRmVMConfig](/powershell/module/azurerm.resources/new-azurermvmconfig)                                     | Crea una configurazione di VM. Questa configurazione include informazioni quali il nome della VM, il sistema operativo e le credenziali amministrative. configurazione di Hello viene utilizzato durante la creazione della macchina virtuale. |
| [Set-AzureRmVMSourceImage](/powershell/module/azurerm.resources/set-azurermvmsourceimage)                           | Specifica un'immagine per una macchina virtuale.                                                                                                                                            |
| [Set-AzureRmVMOSDisk](/powershell/module/azurerm.resources/set-azurermvmosdisk)                                     | Imposta proprietà del disco di hello del sistema operativo in una macchina virtuale.                                                                                                                      |
| [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.resources/set-azurermvmoperatingsystem)                   | Imposta proprietà del disco di hello del sistema operativo in una macchina virtuale.                                                                                                                      |
| [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.resources/add-azurermvmnetworkinterface)                 | Aggiunge una macchina di virtuale tooa interfaccia di rete.                                                                                                                                       |
| [New-AzureRmVM](/powershell/module/azurerm.resources/new-azurermvm)                                                 | Creare una macchina virtuale.                                                                                                                                                            |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup)                     | Rimuove un gruppo di risorse e tutte le risorse contenute al suo interno.                                                                                                                         |

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sul modulo di Azure PowerShell hello, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).

Esempi di script di PowerShell di macchina virtuale aggiuntiva sono reperibile in hello [documentazione macchina virtuale Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
