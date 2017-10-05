---
title: Usare PowerShell per ridimensionare una macchina virtuale Windows in Azure | Documentazione Microsoft
description: Ridimensionare una macchina virtuale Windows creata nel modello di distribuzione Resource Manager usando Azure PowerShell.
services: virtual-machines-windows
documentationcenter: 
author: Drewm3
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 057ff274-6dad-415e-891c-58f8eea9ed78
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: drewm
ms.openlocfilehash: 742efd1496de9ce76b1e5636297ef30f546bd108
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="resize-a-windows-vm"></a><span data-ttu-id="79373-103">Ridimensionare una VM Windows</span><span class="sxs-lookup"><span data-stu-id="79373-103">Resize a Windows VM</span></span>
<span data-ttu-id="79373-104">Questo articolo illustra come ridimensionare una VM Windows creata nel modello di distribuzione Resource Manager usando Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="79373-104">This article shows you how to resize a Windows VM, created in the Resource Manager deployment model using Azure Powershell.</span></span>

<span data-ttu-id="79373-105">Dopo aver creato una macchina virtuale (VM), è possibile scalarla in verticale o in orizzontale modificandone le dimensioni.</span><span class="sxs-lookup"><span data-stu-id="79373-105">After you create a virtual machine (VM), you can scale the VM up or down by changing the VM size.</span></span> <span data-ttu-id="79373-106">In alcuni casi, è necessario prima deallocare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="79373-106">In some cases, you must deallocate the VM first.</span></span> <span data-ttu-id="79373-107">Questa situazione può verificarsi se le nuove dimensioni non sono disponibili nel cluster hardware che attualmente ospita la VM.</span><span class="sxs-lookup"><span data-stu-id="79373-107">This can happen if the new size is not available on the hardware cluster that is currently hosting the VM.</span></span>

## <a name="resize-a-windows-vm-not-in-an-availability-set"></a><span data-ttu-id="79373-108">Ridimensionare una VM Windows non inclusa in un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="79373-108">Resize a Windows VM not in an availability set</span></span>
1. <span data-ttu-id="79373-109">Elencare le dimensioni di VM disponibili nel cluster hardware in cui la VM è ospitata.</span><span class="sxs-lookup"><span data-stu-id="79373-109">List the VM sizes that are available on the hardware cluster where the VM is hosted.</span></span> 
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName> 
    ```
2. <span data-ttu-id="79373-110">Se la dimensione desiderata è inclusa nell'elenco, per ridimensionare la VM eseguire i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="79373-110">If the desired size is listed, run the following commands to resize the VM.</span></span> <span data-ttu-id="79373-111">Se la dimensione desiderata non è inclusa nell'elenco, andare al passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="79373-111">If the desired size is not listed, go on to step 3.</span></span>
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVMsize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. <span data-ttu-id="79373-112">Se la dimensione desiderata non è nell'elenco, eseguire i comandi seguenti per deallocare la VM, ridimensionarla e quindi riavviare la VM.</span><span class="sxs-lookup"><span data-stu-id="79373-112">If the desired size is not listed, run the following commands to deallocate the VM, resize it, and restart the VM.</span></span>
   
    ```powershell
    $rgname = "<resourceGroupName>"
    $vmname = "<vmName>"
    Stop-AzureRmVM -ResourceGroupName $rgname -VMName $vmname -Force
    $vm = Get-AzureRmVM -ResourceGroupName $rgname -VMName $vmname
    $vm.HardwareProfile.VmSize = "<newVMSize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName $rgname
    Start-AzureRmVM -ResourceGroupName $rgname -Name $vmname
    ```

> [!WARNING]
> <span data-ttu-id="79373-113">La deallocazione della VM rilascia qualsiasi indirizzo IP dinamico assegnato alla VM.</span><span class="sxs-lookup"><span data-stu-id="79373-113">Deallocating the VM releases any dynamic IP addresses assigned to the VM.</span></span> <span data-ttu-id="79373-114">I dischi del sistema operativo e dei dati non sono coinvolti.</span><span class="sxs-lookup"><span data-stu-id="79373-114">The OS and data disks are not affected.</span></span> 
> 
> 

## <a name="resize-a-windows-vm-in-an-availability-set"></a><span data-ttu-id="79373-115">Ridimensionare una VM Windows inclusa in un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="79373-115">Resize a Windows VM in an availability set</span></span>
<span data-ttu-id="79373-116">Se la nuova dimensione di una VM inclusa in un set di disponibilità non è disponibile nel cluster hardware che attualmente ospita la VM in questione, per ridimensionare tale VM sarà necessario deallocare tutte le VM incluse nel set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="79373-116">If the new size for a VM in an availability set is not available on the hardware cluster currently hosting the VM, then all VMs in the availability set will need to be deallocated to resize the VM.</span></span> <span data-ttu-id="79373-117">Dopo il ridimensionamento di una VM, può inoltre essere necessario aggiornare le dimensioni delle altre VM incluse nel gruppo di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="79373-117">You also might need to update the size of other VMs in the availability set after one VM has been resized.</span></span> <span data-ttu-id="79373-118">Per ridimensionare una VM inclusa in un gruppo di disponibilità, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="79373-118">To resize a VM in an availability set, perform the following steps.</span></span>

1. <span data-ttu-id="79373-119">Elencare le dimensioni di VM disponibili nel cluster hardware in cui la VM è ospitata.</span><span class="sxs-lookup"><span data-stu-id="79373-119">List the VM sizes that are available on the hardware cluster where the VM is hosted.</span></span>
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName>
    ```
2. <span data-ttu-id="79373-120">Se la dimensione desiderata è inclusa nell'elenco, per ridimensionare la VM eseguire i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="79373-120">If the desired size is listed, run the following commands to resize the VM.</span></span> <span data-ttu-id="79373-121">Se non è inclusa nell'elenco, andare al passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="79373-121">If it is not listed, go to step 3.</span></span>
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVmSize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. <span data-ttu-id="79373-122">Se la dimensione desiderata non è elencata, seguire questa procedura per deallocare tutte le VM incluse nel set di disponibilità, ridimensionare le VM e quindi riavviarle.</span><span class="sxs-lookup"><span data-stu-id="79373-122">If the desired size is not listed, continue with the following steps to deallocate all VMs in the availability set, resize VMs, and restart them.</span></span>
4. <span data-ttu-id="79373-123">Arrestare tutte le VM nel set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="79373-123">Stop all VMs in the availability set.</span></span>
   
   ```powershell
   $rg = "<resourceGroupName>"
   $as = Get-AzureRmAvailabilitySet -ResourceGroupName $rg
   $vmIds = $as.VirtualMachinesReferences
   foreach ($vmId in $vmIDs){
     $string = $vmID.Id.Split("/")
     $vmName = $string[8]
     Stop-AzureRmVM -ResourceGroupName $rg -Name $vmName -Force
   } 
   ```
5. <span data-ttu-id="79373-124">Ridimensionare e riavviare tutte le VM nel set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="79373-124">Resize and restart the VMs in the availability set.</span></span>
   
   ```powershell
   $rg = "<resourceGroupName>"
   $newSize = "<newVmSize>"
   $as = Get-AzureRmAvailabilitySet -ResourceGroupName $rg
   $vmIds = $as.VirtualMachinesReferences
   foreach ($vmId in $vmIDs){
     $string = $vmID.Id.Split("/")
     $vmName = $string[8]
     $vm = Get-AzureRmVM -ResourceGroupName $rg -Name $vmName
     $vm.HardwareProfile.VmSize = $newSize
     Update-AzureRmVM -ResourceGroupName $rg -VM $vm
     Start-AzureRmVM -ResourceGroupName $rg -Name $vmName
   }
   ```

## <a name="next-steps"></a><span data-ttu-id="79373-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="79373-125">Next steps</span></span>
* <span data-ttu-id="79373-126">Per una maggiore scalabilità, eseguire più istanze di VM e la scalabilità orizzontale.</span><span class="sxs-lookup"><span data-stu-id="79373-126">For additional scalability, run multiple VM instances and scale out.</span></span> <span data-ttu-id="79373-127">Per altre informazioni, vedere [Ridimensionare automaticamente le macchine virtuali in un set di scalabilità di macchine virtuali](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="79373-127">For more information, see [Automatically scale Windows machines in a Virtual Machine Scale Set](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md).</span></span>

