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
# <a name="convert-a-windows-virtual-machine-from-unmanaged-disks-toomanaged-disks"></a>Convertire una macchina virtuale Windows da dischi toomanaged dischi non gestito

Se si dispone di Windows macchine virtuali (VM) che usano dischi non gestiti, è possibile convertire hello macchine virtuali gestite toouse dischi tramite hello [dischi gestiti di Azure](managed-disks-overview.md) servizio. Questo processo converte disco hello del sistema operativo sia eventuali dischi dati collegati.

In questo articolo illustra come tooconvert macchine virtuali tramite Azure PowerShell. Se è necessario tooinstall o eseguirne l'aggiornamento, vedere [installare e configurare Azure PowerShell](/powershell/azure/install-azurerm-ps.md).

## <a name="before-you-begin"></a>Prima di iniziare


* Revisione [pianificare la migrazione di hello di dischi tooManaged](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks).

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]




## <a name="convert-single-instance-vms"></a>Convertire VM a istanza singola
Questa sezione vengono trattati come tooconvert a istanza singola macchine virtuali di Azure da codice non dischi toomanaged dischi. (Se le macchine virtuali si trovano in un set di disponibilità, vedere la sezione successiva di hello). 

1. Deallocare hello VM utilizzando hello [Stop AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet. esempio Hello dealloca hello macchina virtuale denominata `myVM` nel gruppo di risorse hello denominato `myResourceGroup`: 

  ```powershell
  $rgName = "myResourceGroup"
  $vmName = "myVM"
  Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
  ```

2. Convertire i dischi di hello VM toomanaged con hello [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk) cmdlet. Hello seguente converte processo hello precedente macchina virtuale, compresi disco hello del sistema operativo e qualsiasi disco dati:

  ```powershell
  ConvertTo-AzureRmVMManagedDisk -ResourceGroupName $rgName -VMName $vmName
  ```

3. Avviare hello VM dopo i dischi di hello conversione toomanaged utilizzando [inizio AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm). Dopo il riavvio di esempio Hello hello VM precedente:

  ```powershell
  Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
  ```


## <a name="convert-vms-in-an-availability-set"></a>Convertire VM in un set di disponibilità

Se le macchine virtuali hello che si desidera tooconvert toomanaged dischi sono in un set di disponibilità, è necessario innanzitutto tooconvert hello disponibilità set tooa gestito set di disponibilità.

1. Convertire la disponibilità di hello imposta utilizzando hello [aggiornamento AzureRmAvailabilitySet](/powershell/module/azurerm.compute/update-azurermavailabilityset) cmdlet. Hello aggiornamenti hello set denominata di disponibilità di esempio seguente `myAvailabilitySet` nel gruppo di risorse hello denominato `myResourceGroup`:

  ```powershell
  $rgName = 'myResourceGroup'
  $avSetName = 'myAvailabilitySet'

  $avSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rgName -Name $avSetName
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned 
  ```

  Se area hello in cui si trova il set di disponibilità ha solo 2 domini di errore gestito ma il numero di hello di domini di errore non gestito è 3, questo comando viene visualizzato un errore simile troppo "hello è specificato il numero di domini di errore 3 deve essere compreso nel too2 compreso tra 1 hello." tooresolve hello errore, l'aggiornamento hello errore dominio too2 e update `Sku` troppo`Aligned` come indicato di seguito:

  ```powershell
  $avSet.PlatformFaultDomainCount = 2
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned
  ```

2. Rilasciare e convertire le macchine virtuali hello in set di disponibilità hello. Hello lo script seguente esegue la deallocazione ogni macchina virtuale utilizzando hello [Stop AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet converta utilizzando [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk)e lo riavvia utilizzando [inizio AzureRmVM ](/powershell/module/azurerm.compute/start-azurermvm):

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


## <a name="troubleshooting"></a>Risoluzione dei problemi

Se si verifica un errore durante la conversione, o se una macchina virtuale è in uno stato di errore a causa di problemi di conversione precedente, eseguire hello `ConvertTo-AzureRmVMManagedDisk` cmdlet nuovamente. In genere, un nuovo tentativo di semplice Sblocca situazione hello.


## <a name="next-steps"></a>Passaggi successivi

[Conversione di dischi gestiti standard toopremium](convert-disk-storage.md)

Eseguire una copia di sola lettura di una VM usando [snapshot](snapshot-copy-managed-disk.md).

