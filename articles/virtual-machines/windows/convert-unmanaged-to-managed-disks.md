---
title: una macchina virtuale Windows da non aaaConvert dischi toomanaged dischi - Azure gestito | Documenti Microsoft
description: Come una macchina virtuale Windows da non gestito dischi toomanaged tooconvert dischi tramite PowerShell nel modello di distribuzione di gestione risorse di hello
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
ms.openlocfilehash: e8ed8694b0e776d22df26261e2fc8340bfe5cafa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="convert-a-windows-virtual-machine-from-unmanaged-disks-toomanaged-disks"></a><span data-ttu-id="9b5fe-103">Convertire una macchina virtuale Windows da dischi toomanaged dischi non gestito</span><span class="sxs-lookup"><span data-stu-id="9b5fe-103">Convert a Windows virtual machine from unmanaged disks toomanaged disks</span></span>

<span data-ttu-id="9b5fe-104">Se si dispone di Windows macchine virtuali (VM) che usano dischi non gestiti, è possibile convertire hello macchine virtuali gestite toouse dischi tramite hello [dischi gestiti di Azure](managed-disks-overview.md) servizio.</span><span class="sxs-lookup"><span data-stu-id="9b5fe-104">If you have existing Windows virtual machines (VMs) that use unmanaged disks, you can convert hello VMs toouse managed disks through hello [Azure Managed Disks](managed-disks-overview.md) service.</span></span> <span data-ttu-id="9b5fe-105">Questo processo converte disco hello del sistema operativo sia eventuali dischi dati collegati.</span><span class="sxs-lookup"><span data-stu-id="9b5fe-105">This process converts both hello OS disk and any attached data disks.</span></span>

<span data-ttu-id="9b5fe-106">In questo articolo illustra come tooconvert macchine virtuali tramite Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9b5fe-106">This article shows you how tooconvert VMs by using Azure PowerShell.</span></span> <span data-ttu-id="9b5fe-107">Se è necessario tooinstall o eseguirne l'aggiornamento, vedere [installare e configurare Azure PowerShell](/powershell/azure/install-azurerm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="9b5fe-107">If you need tooinstall or upgrade it, see [Install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9b5fe-108">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="9b5fe-108">Before you begin</span></span>


* <span data-ttu-id="9b5fe-109">Revisione [pianificare la migrazione di hello di dischi tooManaged](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks).</span><span class="sxs-lookup"><span data-stu-id="9b5fe-109">Review [Plan for hello migration tooManaged Disks](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks).</span></span>

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]




## <a name="convert-single-instance-vms"></a><span data-ttu-id="9b5fe-110">Convertire VM a istanza singola</span><span class="sxs-lookup"><span data-stu-id="9b5fe-110">Convert single-instance VMs</span></span>
<span data-ttu-id="9b5fe-111">Questa sezione vengono trattati come tooconvert a istanza singola macchine virtuali di Azure da codice non dischi toomanaged dischi.</span><span class="sxs-lookup"><span data-stu-id="9b5fe-111">This section covers how tooconvert single-instance Azure VMs from unmanaged disks toomanaged disks.</span></span> <span data-ttu-id="9b5fe-112">(Se le macchine virtuali si trovano in un set di disponibilità, vedere la sezione successiva di hello).</span><span class="sxs-lookup"><span data-stu-id="9b5fe-112">(If your VMs are in an availability set, see hello next section.)</span></span> 

1. <span data-ttu-id="9b5fe-113">Deallocare hello VM utilizzando hello [Stop AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9b5fe-113">Deallocate hello VM by using hello [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet.</span></span> <span data-ttu-id="9b5fe-114">esempio Hello dealloca hello macchina virtuale denominata `myVM` nel gruppo di risorse hello denominato `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="9b5fe-114">hello following example deallocates hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span> 

  ```powershell
  $rgName = "myResourceGroup"
  $vmName = "myVM"
  Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
  ```

2. <span data-ttu-id="9b5fe-115">Convertire i dischi di hello VM toomanaged con hello [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9b5fe-115">Convert hello VM toomanaged disks by using hello [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk) cmdlet.</span></span> <span data-ttu-id="9b5fe-116">Hello seguente converte processo hello precedente macchina virtuale, compresi disco hello del sistema operativo e qualsiasi disco dati:</span><span class="sxs-lookup"><span data-stu-id="9b5fe-116">hello following process converts hello previous VM, including hello OS disk and any data disks:</span></span>

  ```powershell
  ConvertTo-AzureRmVMManagedDisk -ResourceGroupName $rgName -VMName $vmName
  ```

3. <span data-ttu-id="9b5fe-117">Avviare hello VM dopo i dischi di hello conversione toomanaged utilizzando [inizio AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="9b5fe-117">Start hello VM after hello conversion toomanaged disks by using [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm).</span></span> <span data-ttu-id="9b5fe-118">Dopo il riavvio di esempio Hello hello VM precedente:</span><span class="sxs-lookup"><span data-stu-id="9b5fe-118">hello following example restarts hello previous VM:</span></span>

  ```powershell
  Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
  ```


## <a name="convert-vms-in-an-availability-set"></a><span data-ttu-id="9b5fe-119">Convertire VM in un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="9b5fe-119">Convert VMs in an availability set</span></span>

<span data-ttu-id="9b5fe-120">Se le macchine virtuali hello che si desidera tooconvert toomanaged dischi sono in un set di disponibilità, è necessario innanzitutto tooconvert hello disponibilità set tooa gestito set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="9b5fe-120">If hello VMs that you want tooconvert toomanaged disks are in an availability set, you first need tooconvert hello availability set tooa managed availability set.</span></span>

1. <span data-ttu-id="9b5fe-121">Convertire la disponibilità di hello imposta utilizzando hello [aggiornamento AzureRmAvailabilitySet](/powershell/module/azurerm.compute/update-azurermavailabilityset) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9b5fe-121">Convert hello availability set by using hello [Update-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/update-azurermavailabilityset) cmdlet.</span></span> <span data-ttu-id="9b5fe-122">Hello aggiornamenti hello set denominata di disponibilità di esempio seguente `myAvailabilitySet` nel gruppo di risorse hello denominato `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="9b5fe-122">hello following example updates hello availability set named `myAvailabilitySet` in hello resource group named `myResourceGroup`:</span></span>

  ```powershell
  $rgName = 'myResourceGroup'
  $avSetName = 'myAvailabilitySet'

  $avSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rgName -Name $avSetName
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned 
  ```

  <span data-ttu-id="9b5fe-123">Se area hello in cui si trova il set di disponibilità ha solo 2 domini di errore gestito ma il numero di hello di domini di errore non gestito è 3, questo comando viene visualizzato un errore simile troppo "hello è specificato il numero di domini di errore 3 deve essere compreso nel too2 compreso tra 1 hello."</span><span class="sxs-lookup"><span data-stu-id="9b5fe-123">If hello region where your availability set is located has only 2 managed fault domains but hello number of unmanaged fault domains is 3, this command shows an error similar too"hello specified fault domain count 3 must fall in hello range 1 too2."</span></span> <span data-ttu-id="9b5fe-124">tooresolve hello errore, l'aggiornamento hello errore dominio too2 e update `Sku` troppo`Aligned` come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="9b5fe-124">tooresolve hello error, update hello fault domain too2 and update `Sku` too`Aligned` as follows:</span></span>

  ```powershell
  $avSet.PlatformFaultDomainCount = 2
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned
  ```

2. <span data-ttu-id="9b5fe-125">Rilasciare e convertire le macchine virtuali hello in set di disponibilità hello.</span><span class="sxs-lookup"><span data-stu-id="9b5fe-125">Deallocate and convert hello VMs in hello availability set.</span></span> <span data-ttu-id="9b5fe-126">Hello lo script seguente esegue la deallocazione ogni macchina virtuale utilizzando hello [Stop AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet converta utilizzando [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk)e lo riavvia utilizzando [inizio AzureRmVM ](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="9b5fe-126">hello following script deallocates each VM by using hello [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet, converts it by using [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk), and restarts it by using [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

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


## <a name="troubleshooting"></a><span data-ttu-id="9b5fe-127">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="9b5fe-127">Troubleshooting</span></span>

<span data-ttu-id="9b5fe-128">Se si verifica un errore durante la conversione, o se una macchina virtuale è in uno stato di errore a causa di problemi di conversione precedente, eseguire hello `ConvertTo-AzureRmVMManagedDisk` cmdlet nuovamente.</span><span class="sxs-lookup"><span data-stu-id="9b5fe-128">If there is an error during conversion, or if a VM is in a failed state because of issues in a previous conversion, run hello `ConvertTo-AzureRmVMManagedDisk` cmdlet again.</span></span> <span data-ttu-id="9b5fe-129">In genere, un nuovo tentativo di semplice Sblocca situazione hello.</span><span class="sxs-lookup"><span data-stu-id="9b5fe-129">A simple retry usually unblocks hello situation.</span></span>


## <a name="next-steps"></a><span data-ttu-id="9b5fe-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9b5fe-130">Next steps</span></span>

[<span data-ttu-id="9b5fe-131">Conversione di dischi gestiti standard toopremium</span><span class="sxs-lookup"><span data-stu-id="9b5fe-131">Convert standard managed disks toopremium</span></span>](convert-disk-storage.md)

<span data-ttu-id="9b5fe-132">Eseguire una copia di sola lettura di una VM usando [snapshot](snapshot-copy-managed-disk.md).</span><span class="sxs-lookup"><span data-stu-id="9b5fe-132">Take a read-only copy of a VM by using [snapshots](snapshot-copy-managed-disk.md).</span></span>

