---
title: Convertire una macchina virtuale Windows da dischi non gestiti a dischi gestiti - Azure Managed Disks | Microsoft Docs
description: Come convertire i dischi non gestiti di una VM Windows in dischi gestiti usando PowerShell nel modello di distribuzione Resource Manager
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: cynthn
ms.openlocfilehash: 54afcf1e37f696979bfe270a473c72aedf20dc43
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="convert-a-windows-virtual-machine-from-unmanaged-disks-to-managed-disks"></a><span data-ttu-id="6f81c-103">Convertire i dischi non gestiti di una VM Windows in dischi gestiti</span><span class="sxs-lookup"><span data-stu-id="6f81c-103">Convert a Windows virtual machine from unmanaged disks to managed disks</span></span>

<span data-ttu-id="6f81c-104">Se si hanno macchine virtuali (VM) Windows che usano dischi non gestiti, è possibile convertire le VM all'uso di dischi gestiti mediante il servizio [Azure Managed Disks](managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6f81c-104">If you have existing Windows virtual machines (VMs) that use unmanaged disks, you can convert the VMs to use managed disks through the [Azure Managed Disks](managed-disks-overview.md) service.</span></span> <span data-ttu-id="6f81c-105">Questo processo consente di convertire sia il disco del sistema operativo che eventuali dischi dati collegati.</span><span class="sxs-lookup"><span data-stu-id="6f81c-105">This process converts both the OS disk and any attached data disks.</span></span>

<span data-ttu-id="6f81c-106">Questo articolo illustra come convertire le VM con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6f81c-106">This article shows you how to convert VMs by using Azure PowerShell.</span></span> <span data-ttu-id="6f81c-107">Se è necessario eseguirne l'installazione o l'aggiornamento, vedere [Installare e configurare Azure PowerShell](/powershell/azure/install-azurerm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="6f81c-107">If you need to install or upgrade it, see [Install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6f81c-108">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="6f81c-108">Before you begin</span></span>


* <span data-ttu-id="6f81c-109">Vedere [Pianificare la migrazione a Managed Disks](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks).</span><span class="sxs-lookup"><span data-stu-id="6f81c-109">Review [Plan for the migration to Managed Disks](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks).</span></span>

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]




## <a name="convert-single-instance-vms"></a><span data-ttu-id="6f81c-110">Convertire VM a istanza singola</span><span class="sxs-lookup"><span data-stu-id="6f81c-110">Convert single-instance VMs</span></span>
<span data-ttu-id="6f81c-111">Questa sezione descrive come convertire i dischi delle macchine virtuali di Azure a istanza singola da non gestiti a gestiti.</span><span class="sxs-lookup"><span data-stu-id="6f81c-111">This section covers how to convert single-instance Azure VMs from unmanaged disks to managed disks.</span></span> <span data-ttu-id="6f81c-112">Se le VM sono in un set di disponibilità, vedere la sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="6f81c-112">(If your VMs are in an availability set, see the next section.)</span></span> 

1. <span data-ttu-id="6f81c-113">Deallocare la VM mediante il cmdlet [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="6f81c-113">Deallocate the VM by using the [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet.</span></span> <span data-ttu-id="6f81c-114">L'esempio seguente dealloca la macchina virtuale denominata `myVM` nel gruppo di risorse `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="6f81c-114">The following example deallocates the VM named `myVM` in the resource group named `myResourceGroup`:</span></span> 

  ```powershell
  $rgName = "myResourceGroup"
  $vmName = "myVM"
  Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
  ```

2. <span data-ttu-id="6f81c-115">Convertire i dischi della VM in dischi gestiti mediante il cmdlet [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk).</span><span class="sxs-lookup"><span data-stu-id="6f81c-115">Convert the VM to managed disks by using the [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk) cmdlet.</span></span> <span data-ttu-id="6f81c-116">Il processo seguente converte la macchina virtuale precedente, incluso il disco del sistema operativo ed eventuali dischi dati:</span><span class="sxs-lookup"><span data-stu-id="6f81c-116">The following process converts the previous VM, including the OS disk and any data disks:</span></span>

  ```powershell
  ConvertTo-AzureRmVMManagedDisk -ResourceGroupName $rgName -VMName $vmName
  ```

3. <span data-ttu-id="6f81c-117">Avviare la VM dopo la conversione ai dischi gestiti mediante [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="6f81c-117">Start the VM after the conversion to managed disks by using [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm).</span></span> <span data-ttu-id="6f81c-118">L'esempio seguente riavvia la VM precedente:</span><span class="sxs-lookup"><span data-stu-id="6f81c-118">The following example restarts the previous VM:</span></span>

  ```powershell
  Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
  ```


## <a name="convert-vms-in-an-availability-set"></a><span data-ttu-id="6f81c-119">Convertire VM in un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="6f81c-119">Convert VMs in an availability set</span></span>

<span data-ttu-id="6f81c-120">Se le macchine virtuali che si desidera convertire in dischi gestiti si trovano in un set di disponibilità, è innanzitutto necessario convertire il set di disponibilità in un set di disponibilità gestito.</span><span class="sxs-lookup"><span data-stu-id="6f81c-120">If the VMs that you want to convert to managed disks are in an availability set, you first need to convert the availability set to a managed availability set.</span></span>

1. <span data-ttu-id="6f81c-121">Convertire il set di disponibilità mediante il cmdlet [Update-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/update-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="6f81c-121">Convert the availability set by using the [Update-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/update-azurermavailabilityset) cmdlet.</span></span> <span data-ttu-id="6f81c-122">L'esempio seguente aggiorna il set di disponibilità denominato `myAvailabilitySet` nel gruppo di risorse `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="6f81c-122">The following example updates the availability set named `myAvailabilitySet` in the resource group named `myResourceGroup`:</span></span>

  ```powershell
  $rgName = 'myResourceGroup'
  $avSetName = 'myAvailabilitySet'

  $avSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rgName -Name $avSetName
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned 
  ```

  <span data-ttu-id="6f81c-123">Se l'area in cui si trova il set di disponibilità ha solo 2 domini di errore gestiti, ma il numero di domini di errore non gestiti è 3, questo comando visualizza un errore di questo tipo: "Il conteggio del dominio di errore specificato 3 deve essere compreso nell'intervallo 1-2".</span><span class="sxs-lookup"><span data-stu-id="6f81c-123">If the region where your availability set is located has only 2 managed fault domains but the number of unmanaged fault domains is 3, this command shows an error similar to "The specified fault domain count 3 must fall in the range 1 to 2."</span></span> <span data-ttu-id="6f81c-124">Per correggere l'errore, impostare il dominio di errore su 2 e impostare `Sku` su `Aligned` come segue:</span><span class="sxs-lookup"><span data-stu-id="6f81c-124">To resolve the error, update the fault domain to 2 and update `Sku` to `Aligned` as follows:</span></span>

  ```powershell
  $avSet.PlatformFaultDomainCount = 2
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned
  ```

2. <span data-ttu-id="6f81c-125">Deallocare e convertire le VM nel set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="6f81c-125">Deallocate and convert the VMs in the availability set.</span></span> <span data-ttu-id="6f81c-126">Lo script seguente dealloca ogni VM mediante il cmdlet [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm), la converte mediante [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk) e la riavvia mediante [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="6f81c-126">The following script deallocates each VM by using the [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet, converts it by using [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk), and restarts it by using [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

  ```powershell
  $avSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rgName -Name $avSetName

  foreach($vmInfo in $avSet.VirtualMachinesReferences)
  {
     $vm = Get-AzureRmVM -ResourceGroupName $rgName | Where-Object {$_.Id -eq $vmInfo.id}
     Stop-AzureRmVM -ResourceGroupName $rgName -Name $vm.Name -Force
     ConvertTo-AzureRmVMManagedDisk -ResourceGroupName $rgName -VMName $vm.Name
     Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
  }
  ```


## <a name="troubleshooting"></a><span data-ttu-id="6f81c-127">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="6f81c-127">Troubleshooting</span></span>

<span data-ttu-id="6f81c-128">Se si verifica un errore durante la conversione o se una VM si trova in uno stato di errore a causa di problemi in una conversione precedente, eseguire di nuovo il cmdlet `ConvertTo-AzureRmVMManagedDisk`.</span><span class="sxs-lookup"><span data-stu-id="6f81c-128">If there is an error during conversion, or if a VM is in a failed state because of issues in a previous conversion, run the `ConvertTo-AzureRmVMManagedDisk` cmdlet again.</span></span> <span data-ttu-id="6f81c-129">In genere è sufficiente riprovare per sbloccare la situazione.</span><span class="sxs-lookup"><span data-stu-id="6f81c-129">A simple retry usually unblocks the situation.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6f81c-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6f81c-130">Next steps</span></span>

[<span data-ttu-id="6f81c-131">Convertire i dischi gestiti da Standard a Premium</span><span class="sxs-lookup"><span data-stu-id="6f81c-131">Convert standard managed disks to premium</span></span>](convert-disk-storage.md)

<span data-ttu-id="6f81c-132">Eseguire una copia di sola lettura di una VM usando [snapshot](snapshot-copy-managed-disk.md).</span><span class="sxs-lookup"><span data-stu-id="6f81c-132">Take a read-only copy of a VM by using [snapshots](snapshot-copy-managed-disk.md).</span></span>

