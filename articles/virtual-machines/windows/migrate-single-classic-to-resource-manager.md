---
title: aaaMigrate tooan una VM classico ARM gestiti disco VM | Documenti Microsoft
description: Eseguire la migrazione di una singola macchina virtuale di Azure dalla distribuzione classica hello tooManaged dischi nel modello di distribuzione di gestione risorse di hello del modello.
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
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: d8c4b9431f5dd8a071fcbc2ee36581a33f76ba62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manually-migrate-a-classic-vm-tooa-new-arm-managed-disk-vm-from-hello-vhd"></a>Eseguire la migrazione manuale di un tooa VM classico nuova ARM gestiti disco macchina virtuale dal disco rigido virtuale hello 


Questa sezione viene spiegato si toomigrate le macchine virtuali di Azure esistente dal modello di distribuzione classica hello troppo[dischi gestiti](managed-disks-overview.md) nel modello di distribuzione di gestione risorse di hello.


## <a name="plan-for-hello-migration-toomanaged-disks"></a>Pianificare la migrazione di hello di dischi tooManaged

In questa sezione contribuisce di decisione migliore di hello toomake sui tipi di macchina virtuale e disco.


### <a name="location"></a>Percorso

Selezionare una posizione in cui Azure Managed Disks è disponibile. Se si esegue la migrazione di dischi gestiti tooPremium, assicurarsi anche che l'archiviazione Premium è disponibile nell'area di hello in cui si intende toomigrate per. Per informazioni aggiornate sulle località disponibili, vedere [Prodotti disponibili in base all'area](https://azure.microsoft.com/regions/#services).

### <a name="vm-sizes"></a>Dimensioni delle macchine virtuali

Se si esegue la migrazione di dischi gestiti tooPremium, è pari a hello tooupdate hello VM tooPremium dimensioni in grado di archiviazione disponibile nell'area di hello macchina virtuale in cui si trova. Esaminare le dimensioni VM hello che sono in grado di archiviazione Premium. sono elencate le specifiche sulle dimensioni di macchina virtuale di Azure Hello in [dimensioni per le macchine virtuali](sizes.md).
Verificare le caratteristiche di prestazioni hello delle macchine virtuali che funzionano con archiviazione Premium e scegliere le dimensioni di macchina virtuale più appropriata hello più adatta al carico di lavoro. Assicurarsi che vi sia sufficiente larghezza di banda disponibile nel traffico VM toodrive hello disco.

### <a name="disk-sizes"></a>Dimensione disco

**Managed Disks Premium**

È possibile usare sette tipi di dischi gestiti della versione Premium con la macchina virtuale, ognuno con limiti IOP e di velocità effettiva specifici. Considerare questi limiti quando si sceglie il tipo di disco Premium per la macchina virtuale hello in base alle esigenze di hello dell'applicazione in termini di capacità, prestazioni, scalabilità e carichi di picco.

| Tipo di disco Premium  | P4    | P6    | P10   | P20   | P30   | P40   | P50   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| Dimensioni disco           | 128 GB| 512 GB| 128 GB| 512 GB            | 1024 GB (1 TB)    | 2048 GB (2 TB)    | 4095 GB (4 TB)    | 
| IOPS per disco       | 120   | 240   | 500   | 2300              | 5000              | 7500              | 7500              | 
| Velocità effettiva per disco | 25 MB al secondo  | 50 MB al secondo  | 100 MB al secondo | 150 MB al secondo | 200 MB al secondo | 250 MB al secondo | 250 MB al secondo | 

**Managed Disks Standard**

Esistono sette tipi di dischi gestiti della versione Standard che possono essere usati con la macchina virtuale. Si differenziano per capacità ma presentano gli stessi limiti IOP e di velocità effettiva. Scegliere il tipo di hello di dischi gestiti Standard in base alle esigenze di capacità hello dell'applicazione.

| Tipo di disco Standard  | S4               | S6               | S10              | S20              | S30              | S40              | S50              | 
|---------------------|---------------------|---------------------|------------------|------------------|------------------|------------------|------------------| 
| Dimensioni disco           | 30 GB            | 64 GB            | 128 GB           | 512 GB           | 1024 GB (1 TB)   | 2048 GB (2 TB)    | 4095 GB (4 TB)   | 
| IOPS per disco       | 500              | 500              | 500              | 500              | 500              | 500             | 500              | 
| Velocità effettiva per disco | 60 MB al secondo | 60 MB al secondo | 60 MB al secondo | 60 MB al secondo | 60 MB al secondo | 60 MB al secondo | 60 MB al secondo | 


### <a name="disk-caching-policy"></a>Criteri di memorizzazione nella cache su disco 

**Managed Disks Premium**

Per impostazione predefinita, la memorizzazione nella cache dei criteri di disco è *Read-Only* per tutti i dischi dati Premium, di hello e *lettura-scrittura* al disco del sistema operativo Premium hello associato toohello macchina virtuale. Questa impostazione di configurazione è consigliata tooachieve hello ottenere prestazioni ottimali per IOs dell'applicazione. Per i dischi di dati con un utilizzo elevato della scrittura o di sola scrittura (ad esempio i file di log di SQL Server), disabilitare la memorizzazione nella cache su disco in modo da migliorare le prestazioni delle applicazioni.

### <a name="pricing"></a>Prezzi

Hello revisione [prezzi per i dischi gestiti](https://azure.microsoft.com/en-us/pricing/details/managed-disks/). Prezzi di dischi gestiti Premium è identico a hello i dischi Premium non gestito. Tuttavia, il prezzo della versione Standard dei dischi gestiti è diverso da quello della versione Standard dei dischi non gestiti.


## <a name="checklist"></a>Elenco di controllo

1.  Se si esegue la migrazione di dischi gestiti tooPremium, verificare che sia disponibile nell'area di hello a che esegue la migrazione.

2.  Decidere hello nuova serie di macchine Virtuali che verrà utilizzato. Se si esegue la migrazione di dischi gestiti tooPremium deve essere uno spazio di archiviazione Premium in grado di supportare.

3.  Decidere hello VM dimensioni esatte si utilizzerà che sono disponibili nell'area di hello a che esegue la migrazione. Dimensioni della macchina virtuale devono numero di hello toobe toosupport sufficiente di dischi dati che si dispone. Ad esempio, se si dispone di quattro dischi di dati, hello VM deve disporre di due o più core. Considerare anche la potenza di elaborazione, la memoria e la larghezza di banda di rete necessarie.

4.  Dispone di hello corrente VM informazioni utili, tra cui hello elenco di dischi e i BLOB VHD corrispondenti.

Preparare l'applicazione per il tempo di inattività. toodo una migrazione parziale, è necessario toostop tutta l'elaborazione di hello nel sistema corrente hello. Solo a questo punto è possibile ottenere lo stato di tooconsistent che è possibile eseguire la migrazione toohello nuova piattaforma. Durata di tempo di inattività dipende dalla quantità di hello dei dati in toomigrate dischi hello.


## <a name="migrate-hello-vm"></a>Eseguire la migrazione di hello VM

Preparare l'applicazione per il tempo di inattività. toodo una migrazione parziale, è necessario toostop tutta l'elaborazione di hello nel sistema corrente hello. Solo a questo punto è possibile ottenere lo stato di tooconsistent che è possibile eseguire la migrazione toohello nuova piattaforma. Durata di tempo di inattività dipende dalla quantità hello di dati in toomigrate dischi hello.


1.  Innanzitutto, impostare i parametri comuni di hello:

    ```powershell
    $resourceGroupName = 'yourResourceGroupName'
    
    $location = 'your location' 
    
    $virtualNetworkName = 'yourExistingVirtualNetworkName'
    
    $virtualMachineName = 'yourVMName'
    
    $virtualMachineSize = 'Standard_DS3'
    
    $adminUserName = "youradminusername"
    
    $adminPassword = "yourpassword" | ConvertTo-SecureString -AsPlainText -Force
    
    $imageName = 'yourImageName'
    
    $osVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd'
    
    $dataVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk1.vhd'
    
    $dataDiskName = 'dataDisk1'
    ```

2.  Creare un disco del sistema operativo gestito utilizzando hello disco rigido virtuale da hello classic macchina virtuale.

    Assicurarsi di aver fornito hello completare l'URI di hello parametro toohello $osVhdUri disco rigido virtuale del sistema operativo. Per **-AccountType**, immettere **PremiumLRS** o **StandardLRS** in base al tipo di dischi (Premium o Standard) verso cui si sta eseguendo la migrazione.

    ```powershell
    $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $osVhdUri) '
    -ResourceGroupName $resourceGroupName
    ```

3.  Collegare toohello disco del sistema operativo hello nuova macchina virtuale.

    ```powershell
    $VirtualMachine = New-AzureRmVMConfig -VMName $virtualMachineName -VMSize $virtualMachineSize
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -ManagedDiskId $osDisk.Id '
    -StorageAccountType PremiumLRS -DiskSizeInGB 128 -CreateOption Attach -Windows
    ```

4.  Creare un disco dati gestiti da file di disco rigido virtuale dati hello e aggiungerlo toohello nuova macchina virtuale.

    ```powershell
    $dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreationDataCreateOption Import '
    -SourceUri $dataVhdUri ) -ResourceGroupName $resourceGroupName
    
    $VirtualMachine = Add-AzureRmVMDataDisk -VM $VirtualMachine -Name $dataDiskName '
    -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1
    ```

5.  Creare hello nuova macchina virtuale impostando public IP, la rete virtuale e scheda di rete.

    ```powershell
    $publicIp = New-AzureRmPublicIpAddress -Name ($VirtualMachineName.ToLower()+'_ip') '
    -ResourceGroupName $resourceGroupName -Location $location -AllocationMethod Dynamic
    
    $vnet = Get-AzureRmVirtualNetwork -Name $virtualNetworkName -ResourceGroupName $resourceGroupName
    
    $nic = New-AzureRmNetworkInterface -Name ($VirtualMachineName.ToLower()+'_nic') '
    -ResourceGroupName $resourceGroupName -Location $location -SubnetId $vnet.Subnets[0].Id '
    -PublicIpAddressId $publicIp.Id
    
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $nic.Id
    
    New-AzureRmVM -VM $VirtualMachine -ResourceGroupName $resourceGroupName -Location $location
    ```

> [!NOTE]
>Potrebbero essere presenti ulteriori passaggi necessari toosupport l'applicazione che non rientrano in questa Guida.
>
>

## <a name="next-steps"></a>Passaggi successivi

- Connessione macchina virtuale toohello. Per istruzioni, vedere [come tooconnect e tooan virtuali di Azure di accesso del computer che eseguono Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

