---
title: "Modificare un set di disponibilità per VM | Microsoft Docs"
description: "Informazioni su come modificare il set di disponibilità per le macchine virtuali tramite Azure PowerShell e il modello di distribuzione Resource Manager."
keywords: 
services: virtual-machines-windows
documentationcenter: 
author: Drewm3
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 44c90f90-bc9a-4260-a36f-5465e2a1ef94
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/15/2016
ms.author: drewm
ms.openlocfilehash: d1daa01191480eaeb81727416b2134b00c698dc3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="change-the-availability-set-for-a-windows-vm"></a><span data-ttu-id="737cc-103">Modificare il set di disponibilità per una VM Windows</span><span class="sxs-lookup"><span data-stu-id="737cc-103">Change the availability set for a Windows VM</span></span>
<span data-ttu-id="737cc-104">I passaggi seguenti descrivono come modificare il set di disponibilità di una VM tramite Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="737cc-104">The following steps describe how to change the availability set of a VM using Azure PowerShell.</span></span> <span data-ttu-id="737cc-105">Una VM può essere aggiunta a un set di disponibilità solo in fase di creazione.</span><span class="sxs-lookup"><span data-stu-id="737cc-105">A VM can only be added to an availability set when it is created.</span></span> <span data-ttu-id="737cc-106">Per modificare il set di disponibilità, è necessario eliminare e ricreare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="737cc-106">In order to change the availability set, you need to delete and recreate the virtual machine.</span></span> 

## <a name="change-the-availability-set-using-powershell"></a><span data-ttu-id="737cc-107">Modificare il set di disponibilità tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="737cc-107">Change the availability set using PowerShell</span></span>
1. <span data-ttu-id="737cc-108">Acquisire i dettagli principali seguenti dalla VM da modificare.</span><span class="sxs-lookup"><span data-stu-id="737cc-108">Capture the following key details from the VM to be modified.</span></span>
   
    <span data-ttu-id="737cc-109">Nome della VM</span><span class="sxs-lookup"><span data-stu-id="737cc-109">Name of the VM</span></span>
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <Name-of-resource-group> -Name <name-of-VM>
    $vm.Name
    ```
   
    <span data-ttu-id="737cc-110">Dimensioni macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="737cc-110">VM Size</span></span>
   
    ```powershell
    $vm.HardwareProfile.VmSize
    ```
   
    <span data-ttu-id="737cc-111">Interfaccia di rete primaria e interfacce di rete facoltative, se presenti, nella VM</span><span class="sxs-lookup"><span data-stu-id="737cc-111">Network primary network interface and optional network interfaces if they exist on the VM</span></span>
   
    ```powershell
    $vm.NetworkProfile.NetworkInterfaces[0].Id
    ```
   
    <span data-ttu-id="737cc-112">Profilo del disco del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="737cc-112">OS Disk Profile</span></span>
   
    ```powershell
    $vm.StorageProfile.OsDisk.OsType
    $vm.StorageProfile.OsDisk.Name
    $vm.StorageProfile.OsDisk.Vhd.Uri
    ```
   
    <span data-ttu-id="737cc-113">Profilo di ogni disco dati</span><span class="sxs-lookup"><span data-stu-id="737cc-113">Disk profiles for each data disk</span></span> 
   
    ```powershell
    $vm.StorageProfile.DataDisks[<index>].Lun
    $vm.StorageProfile.DataDisks[<index>].Vhd.Uri
    ```
   
    <span data-ttu-id="737cc-114">Estensioni VM installate</span><span class="sxs-lookup"><span data-stu-id="737cc-114">VM extensions installed</span></span> 
   
    ```powershell
    $vm.Extensions
    ```
2. <span data-ttu-id="737cc-115">Eliminare la VM senza eliminare i dischi o le interfacce di rete.</span><span class="sxs-lookup"><span data-stu-id="737cc-115">Delete the VM without deleting any of the disks or the network interfaces.</span></span>
   
    ```powershell
    Remove-AzureRmVM -ResourceGroupName <resourceGroupName> -Name <vmName> 
    ```
3. <span data-ttu-id="737cc-116">Creare il set di disponibilità, se non esiste già</span><span class="sxs-lookup"><span data-stu-id="737cc-116">Create the availability set if it does not already exist</span></span>
   
    ```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName <resourceGroupName> -Name <availabilitySetName> -Location "<location>" 
    ```
4. <span data-ttu-id="737cc-117">Ricreare la VM usando il nuovo set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="737cc-117">Recreate the VM using the new availability set</span></span>
   
    ```powershell
    $vm2 = New-AzureRmVMConfig -VMName <VM-name> -VMSize <vm-size> -AvailabilitySetId <availability-set-id>
   
    Set-AzureRmVMOSDisk -CreateOption "Attach" -VM <vmConfig> -VhdUri <osDiskURI> -Name <osDiskName> [-Windows | -Linux]
   
    Add-AzureRmVMNetworkInterface -VM <vmConfig> -Id  <nicId> 
   
    New-AzureRmVM -ResourceGroupName <resourceGroupName> -Location <location> -VM <vmConfig>
    ``` 
5. <span data-ttu-id="737cc-118">Aggiungere dischi dati ed estensioni.</span><span class="sxs-lookup"><span data-stu-id="737cc-118">Add data disks and extensions.</span></span> <span data-ttu-id="737cc-119">Per altre informazioni, vedere l'articolo su come [collegare un disco dati a una VM](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) e la sezione relativa alle [estensioni nei modelli di Resource Manager](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).</span><span class="sxs-lookup"><span data-stu-id="737cc-119">For more information, see [Attach Data Disk to VM](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Extensions in Resource Manager templates](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).</span></span> <span data-ttu-id="737cc-120">È possibile aggiungere estensioni e dischi dati alla VM tramite PowerShell o l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="737cc-120">Data disks and extensions can be added to the VM using PowerShell or Azure CLI.</span></span>

## <a name="example-script"></a><span data-ttu-id="737cc-121">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="737cc-121">Example Script</span></span>
<span data-ttu-id="737cc-122">Lo script seguente offre un esempio di raccolta delle informazioni necessarie ed eliminazione e ricreazione della VM originale in un nuovo set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="737cc-122">The following script provides an example of gathering the required information, deleting the original VM and then recreating it in a new availability set.</span></span>

```powershell
    #set variables
    $rg = "demo-resource-group"
    $vmName = "demo-vm"
    $newAvailSetName = "demo-as"
    $outFile = "C:\temp\outfile.txt"

    #Get VM Details
    $OriginalVM = get-azurermvm -ResourceGroupName $rg -Name $vmName

    #Output VM details to file
    "VM Name: " | Out-File -FilePath $outFile 
    $OriginalVM.Name | Out-File -FilePath $outFile -Append

    "Extensions: " | Out-File -FilePath $outFile -Append
    $OriginalVM.Extensions | Out-File -FilePath $outFile -Append

    "VMSize: " | Out-File -FilePath $outFile -Append
    $OriginalVM.HardwareProfile.VmSize | Out-File -FilePath $outFile -Append

    "NIC: " | Out-File -FilePath $outFile -Append
    $OriginalVM.NetworkProfile.NetworkInterfaces[0].Id | Out-File -FilePath $outFile -Append

    "OSType: " | Out-File -FilePath $outFile -Append
    $OriginalVM.StorageProfile.OsDisk.OsType | Out-File -FilePath $outFile -Append

    "OS Disk: " | Out-File -FilePath $outFile -Append
    $OriginalVM.StorageProfile.OsDisk.Vhd.Uri | Out-File -FilePath $outFile -Append

    if ($OriginalVM.StorageProfile.DataDisks) {
    "Data Disk(s): " | Out-File -FilePath $outFile -Append
    $OriginalVM.StorageProfile.DataDisks | Out-File -FilePath $outFile -Append
    }

    #Remove the original VM
    Remove-AzureRmVM -ResourceGroupName $rg -Name $vmName

    #Create new availability set if it does not exist
    $availSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rg -Name $newAvailSetName -ErrorAction Ignore
    if (-Not $availSet) {
    $availset = New-AzureRmAvailabilitySet -ResourceGroupName $rg -Name $newAvailSetName -Location $OriginalVM.Location
    }

    #Create the basic configuration for the replacement VM
    $newVM = New-AzureRmVMConfig -VMName $OriginalVM.Name -VMSize $OriginalVM.HardwareProfile.VmSize -AvailabilitySetId $availSet.Id
    Set-AzureRmVMOSDisk -VM $NewVM -VhdUri $OriginalVM.StorageProfile.OsDisk.Vhd.Uri  -Name $OriginalVM.Name -CreateOption Attach -Windows

    #Add Data Disks
    foreach ($disk in $OriginalVM.StorageProfile.DataDisks ) { 
    Add-AzureRmVMDataDisk -VM $newVM -Name $disk.Name -VhdUri $disk.Vhd.Uri -Caching $disk.Caching -Lun $disk.Lun -CreateOption Attach -DiskSizeInGB $disk.DiskSizeGB
    }

    #Add NIC(s)
    foreach ($nic in $OriginalVM.NetworkInterfaceIDs) {
        Add-AzureRmVMNetworkInterface -VM $NewVM -Id $nic
    }

    #Create the VM
    New-AzureRmVM -ResourceGroupName $rg -Location $OriginalVM.Location -VM $NewVM -DisableBginfoExtension
```

## <a name="next-steps"></a><span data-ttu-id="737cc-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="737cc-123">Next steps</span></span>
<span data-ttu-id="737cc-124">Aumentare lo spazio di archiviazione della VM aggiungendo un ulteriore [disco dati](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="737cc-124">Add additional storage to your VM by adding an additional [data disk](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

