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
# <a name="resize-a-windows-vm"></a>Ridimensionare una VM Windows
Questo articolo illustra come tooresize creare una macchina virtuale di Windows, nel modello di distribuzione di gestione risorse hello con Azure Powershell.

Dopo aver creato una macchina virtuale (VM), è possibile scalare hello VM verso l'alto o verso il basso la modifica delle dimensioni della macchina virtuale hello. In alcuni casi, è necessario deallocare prima hello VM. Questa situazione può verificarsi se hello nuova dimensione non è disponibile nel cluster hardware hello che attualmente ospita hello macchina virtuale.

## <a name="resize-a-windows-vm-not-in-an-availability-set"></a>Ridimensionare una VM Windows non inclusa in un set di disponibilità
1. Elenco delle dimensioni delle macchine Virtuali di hello che sono disponibili nel cluster hardware hello in cui è ospitato hello macchina virtuale. 
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName> 
    ```
2. Se lo si desidera hello dimensioni sono elencata, eseguire hello seguenti comandi tooresize hello macchina virtuale. Se lo si desidera hello dimensioni non sono elencata, andare toostep 3.
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVMsize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. Se lo si desidera hello dimensioni non sono elencata, eseguire hello seguenti comandi toodeallocate hello VM, ridimensionarlo e riavviare hello macchina virtuale.
   
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
> Deallocazione di hello VM rilascia tutti gli indirizzi IP dinamici assegnati toohello VM. Hello del sistema operativo e i dischi di dati non sono interessati. 
> 
> 

## <a name="resize-a-windows-vm-in-an-availability-set"></a>Ridimensionare una VM Windows inclusa in un set di disponibilità
Se hello nuove dimensioni per una macchina virtuale in un set di disponibilità non sono disponibile nel cluster hardware hello attualmente ospitando hello macchina virtuale, quindi tutte le macchine virtuali nel set di disponibilità hello saranno necessario toobe deallocato hello tooresize macchina virtuale. Inoltre, potrebbe essere necessario dimensioni hello tooupdate delle altre macchine virtuali in hello set di disponibilità dopo una macchina virtuale è stata ridimensionata. tooresize una macchina virtuale in un set di disponibilità, eseguire hello alla procedura seguente.

1. Elenco delle dimensioni delle macchine Virtuali di hello che sono disponibili nel cluster hardware hello in cui è ospitato hello macchina virtuale.
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName>
    ```
2. Se lo si desidera hello dimensioni sono elencata, eseguire hello seguenti comandi tooresize hello macchina virtuale. Se non è elencato, andare toostep 3.
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVmSize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. Se lo si desidera hello dimensioni non sono elencata, continuare con i seguenti passaggi toodeallocate hello tutte le macchine virtuali nel set di disponibilità hello ridimensiona una macchina virtuale e riavviarle.
4. Arrestare tutte le macchine virtuali nel set di disponibilità hello.
   
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
5. Ridimensionare e riavviare le macchine virtuali hello in set di disponibilità hello.
   
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

## <a name="next-steps"></a>Passaggi successivi
* Per una maggiore scalabilità, eseguire più istanze di VM e la scalabilità orizzontale. Per altre informazioni, vedere [Ridimensionare automaticamente le macchine virtuali in un set di scalabilità di macchine virtuali](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md).

