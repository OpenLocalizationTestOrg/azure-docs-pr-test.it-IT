---
title: aaaUse PowerShell tooresize una macchina virtuale Windows in Azure | Documenti Microsoft
description: Ridimensionare una macchina virtuale di Windows creata nel modello di distribuzione di gestione risorse hello, tramite Azure Powershell.
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
ms.openlocfilehash: a4a80f3bc99911e4f1a095f0ce63aca00fa50694
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-windows-vm"></a><span data-ttu-id="14945-103">Ridimensionare una VM Windows</span><span class="sxs-lookup"><span data-stu-id="14945-103">Resize a Windows VM</span></span>
<span data-ttu-id="14945-104">Questo articolo illustra come tooresize creare una macchina virtuale di Windows, nel modello di distribuzione di gestione risorse hello con Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="14945-104">This article shows you how tooresize a Windows VM, created in hello Resource Manager deployment model using Azure Powershell.</span></span>

<span data-ttu-id="14945-105">Dopo aver creato una macchina virtuale (VM), è possibile scalare hello VM verso l'alto o verso il basso la modifica delle dimensioni della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="14945-105">After you create a virtual machine (VM), you can scale hello VM up or down by changing hello VM size.</span></span> <span data-ttu-id="14945-106">In alcuni casi, è necessario deallocare prima hello VM.</span><span class="sxs-lookup"><span data-stu-id="14945-106">In some cases, you must deallocate hello VM first.</span></span> <span data-ttu-id="14945-107">Questa situazione può verificarsi se hello nuova dimensione non è disponibile nel cluster hardware hello che attualmente ospita hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="14945-107">This can happen if hello new size is not available on hello hardware cluster that is currently hosting hello VM.</span></span>

## <a name="resize-a-windows-vm-not-in-an-availability-set"></a><span data-ttu-id="14945-108">Ridimensionare una VM Windows non inclusa in un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="14945-108">Resize a Windows VM not in an availability set</span></span>
1. <span data-ttu-id="14945-109">Elenco delle dimensioni delle macchine Virtuali di hello che sono disponibili nel cluster hardware hello in cui è ospitato hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="14945-109">List hello VM sizes that are available on hello hardware cluster where hello VM is hosted.</span></span> 
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName> 
    ```
2. <span data-ttu-id="14945-110">Se lo si desidera hello dimensioni sono elencata, eseguire hello seguenti comandi tooresize hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="14945-110">If hello desired size is listed, run hello following commands tooresize hello VM.</span></span> <span data-ttu-id="14945-111">Se lo si desidera hello dimensioni non sono elencata, andare toostep 3.</span><span class="sxs-lookup"><span data-stu-id="14945-111">If hello desired size is not listed, go on toostep 3.</span></span>
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVMsize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. <span data-ttu-id="14945-112">Se lo si desidera hello dimensioni non sono elencata, eseguire hello seguenti comandi toodeallocate hello VM, ridimensionarlo e riavviare hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="14945-112">If hello desired size is not listed, run hello following commands toodeallocate hello VM, resize it, and restart hello VM.</span></span>
   
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
> <span data-ttu-id="14945-113">Deallocazione di hello VM rilascia tutti gli indirizzi IP dinamici assegnati toohello VM.</span><span class="sxs-lookup"><span data-stu-id="14945-113">Deallocating hello VM releases any dynamic IP addresses assigned toohello VM.</span></span> <span data-ttu-id="14945-114">Hello del sistema operativo e i dischi di dati non sono interessati.</span><span class="sxs-lookup"><span data-stu-id="14945-114">hello OS and data disks are not affected.</span></span> 
> 
> 

## <a name="resize-a-windows-vm-in-an-availability-set"></a><span data-ttu-id="14945-115">Ridimensionare una VM Windows inclusa in un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="14945-115">Resize a Windows VM in an availability set</span></span>
<span data-ttu-id="14945-116">Se hello nuove dimensioni per una macchina virtuale in un set di disponibilità non sono disponibile nel cluster hardware hello attualmente ospitando hello macchina virtuale, quindi tutte le macchine virtuali nel set di disponibilità hello saranno necessario toobe deallocato hello tooresize macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="14945-116">If hello new size for a VM in an availability set is not available on hello hardware cluster currently hosting hello VM, then all VMs in hello availability set will need toobe deallocated tooresize hello VM.</span></span> <span data-ttu-id="14945-117">Inoltre, potrebbe essere necessario dimensioni hello tooupdate delle altre macchine virtuali in hello set di disponibilità dopo una macchina virtuale è stata ridimensionata.</span><span class="sxs-lookup"><span data-stu-id="14945-117">You also might need tooupdate hello size of other VMs in hello availability set after one VM has been resized.</span></span> <span data-ttu-id="14945-118">tooresize una macchina virtuale in un set di disponibilità, eseguire hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="14945-118">tooresize a VM in an availability set, perform hello following steps.</span></span>

1. <span data-ttu-id="14945-119">Elenco delle dimensioni delle macchine Virtuali di hello che sono disponibili nel cluster hardware hello in cui è ospitato hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="14945-119">List hello VM sizes that are available on hello hardware cluster where hello VM is hosted.</span></span>
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName>
    ```
2. <span data-ttu-id="14945-120">Se lo si desidera hello dimensioni sono elencata, eseguire hello seguenti comandi tooresize hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="14945-120">If hello desired size is listed, run hello following commands tooresize hello VM.</span></span> <span data-ttu-id="14945-121">Se non è elencato, andare toostep 3.</span><span class="sxs-lookup"><span data-stu-id="14945-121">If it is not listed, go toostep 3.</span></span>
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVmSize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. <span data-ttu-id="14945-122">Se lo si desidera hello dimensioni non sono elencata, continuare con i seguenti passaggi toodeallocate hello tutte le macchine virtuali nel set di disponibilità hello ridimensiona una macchina virtuale e riavviarle.</span><span class="sxs-lookup"><span data-stu-id="14945-122">If hello desired size is not listed, continue with hello following steps toodeallocate all VMs in hello availability set, resize VMs, and restart them.</span></span>
4. <span data-ttu-id="14945-123">Arrestare tutte le macchine virtuali nel set di disponibilità hello.</span><span class="sxs-lookup"><span data-stu-id="14945-123">Stop all VMs in hello availability set.</span></span>
   
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
5. <span data-ttu-id="14945-124">Ridimensionare e riavviare le macchine virtuali hello in set di disponibilità hello.</span><span class="sxs-lookup"><span data-stu-id="14945-124">Resize and restart hello VMs in hello availability set.</span></span>
   
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

## <a name="next-steps"></a><span data-ttu-id="14945-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="14945-125">Next steps</span></span>
* <span data-ttu-id="14945-126">Per una maggiore scalabilità, eseguire più istanze di VM e la scalabilità orizzontale. Per altre informazioni, vedere [Ridimensionare automaticamente le macchine virtuali in un set di scalabilità di macchine virtuali](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="14945-126">For additional scalability, run multiple VM instances and scale out. For more information, see [Automatically scale Windows machines in a Virtual Machine Scale Set](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md).</span></span>

