---
title: "un set di disponibilità di macchine virtuali aaaChange | Documenti Microsoft"
description: "Informazioni su come la disponibilità di hello toochange imposta per le macchine virtuali tramite Azure PowerShell e modello di distribuzione di gestione risorse di hello."
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
ms.openlocfilehash: 3b1cc010a6d4c4883f2e34da9cfca4372aec92cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-availability-set-for-a-windows-vm"></a><span data-ttu-id="b68c9-103">Modificare la disponibilità di hello impostato per una macchina virtuale Windows</span><span class="sxs-lookup"><span data-stu-id="b68c9-103">Change hello availability set for a Windows VM</span></span>
<span data-ttu-id="b68c9-104">Hello alla procedura seguente viene descritto come toochange hello set di disponibilità di una macchina virtuale con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b68c9-104">hello following steps describe how toochange hello availability set of a VM using Azure PowerShell.</span></span> <span data-ttu-id="b68c9-105">Una macchina virtuale può essere aggiunti solo disponibilità tooan impostata al momento della creazione.</span><span class="sxs-lookup"><span data-stu-id="b68c9-105">A VM can only be added tooan availability set when it is created.</span></span> <span data-ttu-id="b68c9-106">Nel set di disponibilità hello toochange ordine, è necessario toodelete e ricreare macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="b68c9-106">In order toochange hello availability set, you need toodelete and recreate hello virtual machine.</span></span> 

## <a name="change-hello-availability-set-using-powershell"></a><span data-ttu-id="b68c9-107">Modifica hello set di disponibilità usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="b68c9-107">Change hello availability set using PowerShell</span></span>
1. <span data-ttu-id="b68c9-108">Acquisire hello dopo i dettagli della chiave da hello VM toobe modificato.</span><span class="sxs-lookup"><span data-stu-id="b68c9-108">Capture hello following key details from hello VM toobe modified.</span></span>
   
    <span data-ttu-id="b68c9-109">Nome della macchina virtuale hello</span><span class="sxs-lookup"><span data-stu-id="b68c9-109">Name of hello VM</span></span>
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <Name-of-resource-group> -Name <name-of-VM>
    $vm.Name
    ```
   
    <span data-ttu-id="b68c9-110">Dimensioni macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="b68c9-110">VM Size</span></span>
   
    ```powershell
    $vm.HardwareProfile.VmSize
    ```
   
    <span data-ttu-id="b68c9-111">Interfaccia di rete primaria di rete e le interfacce di rete facoltativa se hello VM esistenti</span><span class="sxs-lookup"><span data-stu-id="b68c9-111">Network primary network interface and optional network interfaces if they exist on hello VM</span></span>
   
    ```powershell
    $vm.NetworkProfile.NetworkInterfaces[0].Id
    ```
   
    <span data-ttu-id="b68c9-112">Profilo del disco del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="b68c9-112">OS Disk Profile</span></span>
   
    ```powershell
    $vm.StorageProfile.OsDisk.OsType
    $vm.StorageProfile.OsDisk.Name
    $vm.StorageProfile.OsDisk.Vhd.Uri
    ```
   
    <span data-ttu-id="b68c9-113">Profilo di ogni disco dati</span><span class="sxs-lookup"><span data-stu-id="b68c9-113">Disk profiles for each data disk</span></span> 
   
    ```powershell
    $vm.StorageProfile.DataDisks[<index>].Lun
    $vm.StorageProfile.DataDisks[<index>].Vhd.Uri
    ```
   
    <span data-ttu-id="b68c9-114">Estensioni VM installate</span><span class="sxs-lookup"><span data-stu-id="b68c9-114">VM extensions installed</span></span> 
   
    ```powershell
    $vm.Extensions
    ```
2. <span data-ttu-id="b68c9-115">Eliminare hello macchina virtuale senza eliminare alcuna delle interfacce di rete di hello o dischi hello.</span><span class="sxs-lookup"><span data-stu-id="b68c9-115">Delete hello VM without deleting any of hello disks or hello network interfaces.</span></span>
   
    ```powershell
    Remove-AzureRmVM -ResourceGroupName <resourceGroupName> -Name <vmName> 
    ```
3. <span data-ttu-id="b68c9-116">Creare disponibilità hello impostata se non esiste già</span><span class="sxs-lookup"><span data-stu-id="b68c9-116">Create hello availability set if it does not already exist</span></span>
   
    ```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName <resourceGroupName> -Name <availabilitySetName> -Location "<location>" 
    ```
4. <span data-ttu-id="b68c9-117">Ricreare hello macchina virtuale utilizzando il nuovo gruppo di disponibilità hello</span><span class="sxs-lookup"><span data-stu-id="b68c9-117">Recreate hello VM using hello new availability set</span></span>
   
    ```powershell
    $vm2 = New-AzureRmVMConfig -VMName <VM-name> -VMSize <vm-size> -AvailabilitySetId <availability-set-id>
   
    Set-AzureRmVMOSDisk -CreateOption "Attach" -VM <vmConfig> -VhdUri <osDiskURI> -Name <osDiskName> [-Windows | -Linux]
   
    Add-AzureRmVMNetworkInterface -VM <vmConfig> -Id  <nicId> 
   
    New-AzureRmVM -ResourceGroupName <resourceGroupName> -Location <location> -VM <vmConfig>
    ``` 
5. <span data-ttu-id="b68c9-118">Aggiungere dischi dati ed estensioni.</span><span class="sxs-lookup"><span data-stu-id="b68c9-118">Add data disks and extensions.</span></span> <span data-ttu-id="b68c9-119">Per ulteriori informazioni, vedere [collega disco dati tooVM](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) e [estensioni in modelli di gestione risorse](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).</span><span class="sxs-lookup"><span data-stu-id="b68c9-119">For more information, see [Attach Data Disk tooVM](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Extensions in Resource Manager templates](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).</span></span> <span data-ttu-id="b68c9-120">I dischi dati e le estensioni possono essere aggiunti toohello VM tramite PowerShell o CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="b68c9-120">Data disks and extensions can be added toohello VM using PowerShell or Azure CLI.</span></span>

## <a name="example-script"></a><span data-ttu-id="b68c9-121">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="b68c9-121">Example Script</span></span>
<span data-ttu-id="b68c9-122">Hello script riportato di seguito viene fornito un esempio di raccogliere le informazioni di hello necessaria, l'eliminazione di hello macchina virtuale originale e quindi ricrearla in un nuovo set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="b68c9-122">hello following script provides an example of gathering hello required information, deleting hello original VM and then recreating it in a new availability set.</span></span>

```powershell
    #set variables
    $rg = "demo-resource-group"
    $vmName = "demo-vm"
    $newAvailSetName = "demo-as"
    $outFile = "C:\temp\outfile.txt"

    #Get VM Details
    $OriginalVM = get-azurermvm -ResourceGroupName $rg -Name $vmName

    #Output VM details toofile
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

    #Remove hello original VM
    Remove-AzureRmVM -ResourceGroupName $rg -Name $vmName

    #Create new availability set if it does not exist
    $availSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rg -Name $newAvailSetName -ErrorAction Ignore
    if (-Not $availSet) {
    $availset = New-AzureRmAvailabilitySet -ResourceGroupName $rg -Name $newAvailSetName -Location $OriginalVM.Location
    }

    #Create hello basic configuration for hello replacement VM
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

    #Create hello VM
    New-AzureRmVM -ResourceGroupName $rg -Location $OriginalVM.Location -VM $NewVM -DisableBginfoExtension
```

## <a name="next-steps"></a><span data-ttu-id="b68c9-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b68c9-123">Next steps</span></span>
<span data-ttu-id="b68c9-124">Aggiungere ulteriore spazio di archiviazione tooyour VM aggiungendo un ulteriore [disco dati](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b68c9-124">Add additional storage tooyour VM by adding an additional [data disk](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

