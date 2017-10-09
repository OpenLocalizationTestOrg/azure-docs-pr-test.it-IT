---
title: dischi aaaManage Azure con Azure PowerShell hello | Documenti Microsoft
description: 'Esercitazione: gestire i dischi di Azure con hello Azure PowerShell'
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 2f61ad18bc94bab527d7ae593da603c6073adc89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-disks-with-powershell"></a>Gestire i dischi di Azure con PowerShell

Macchine virtuali di Azure utilizzano il sistema operativo macchine virtuali di dischi toostore hello, applicazioni e dati. Quando si crea una macchina virtuale è importante toochoose una dimensione del disco e il carico di lavoro di configurazione appropriato toohello previsto. Questa esercitazione illustra la distribuzione e la gestione dei dischi di VM. Vengono fornite informazioni su:

> [!div class="checklist"]
> * Dischi del sistema operativo e dischi temporanei
> * Dischi dati
> * Dischi Standard e Premium
> * Prestazioni dei dischi
> * Collegamento e preparazione dei dischi dati

Questa esercitazione richiede hello Azure PowerShell versione 3.6 o versioni successive del modulo. Eseguire ` Get-Module -ListAvailable AzureRM` versione hello toofind. Se è necessario tooupgrade, vedere [modulo installare Azure PowerShell](/powershell/azure/install-azurerm-ps).

## <a name="default-azure-disks"></a>Dischi di Azure predefiniti

Quando viene creata una macchina virtuale di Azure, due dischi sono macchina virtuale toohello automaticamente collegato. 

**Disco del sistema operativo** : i dischi del sistema operativo possono essere dimensionati backup too1 terabyte e host hello del sistema operativo di macchine virtuali.  disco del sistema operativo Hello è assegnata una lettera di unità di *c:* per impostazione predefinita. disco Hello la memorizzazione nella cache di configurazione del disco del sistema operativo hello è ottimizzato per le prestazioni del sistema operativo. disco del sistema operativo Hello **non** ospitare applicazioni o i dati. Per le applicazioni e i dati, usare un disco dati, descritto in dettaglio più avanti in questo articolo.

**Disco temporaneo** -i dischi temporanei utilizzano un'unità SSD che si trova in hello stesso host hello VM Azure. I dischi temporanei sono altamente efficienti e possono essere usati per operazioni quali l'elaborazione dei dati temporanei. Tuttavia, se hello macchina virtuale viene spostata tooa nuovo host, i dati archiviati in un disco temporaneo viene rimosso. dimensione di Hello del disco temporaneo hello è determinata dalla hello dimensioni della macchina virtuale. Ai dischi temporanei viene assegnata una lettera di unità *d:* per impostazione predefinita.

### <a name="temporary-disk-sizes"></a>Dimensioni del disco temporaneo

| Tipo | Dimensioni macchina virtuale | Dimensioni massime del disco temporaneo (GB) |
|----|----|----|
| [Utilizzo generico](sizes-general.md) | Serie A e D | 800 |
| [Ottimizzate per il calcolo](sizes-compute.md) | Serie F | 800 |
| [Ottimizzate per la memoria](../virtual-machines-windows-sizes-memory.md) | Serie D e G | 6144 |
| [Ottimizzate per l'archiviazione](../virtual-machines-windows-sizes-storage.md) | Serie L | 5630 |
| [GPU](sizes-gpu.md) | Serie N | 1.440 |
| [Prestazioni elevate](sizes-hpc.md) | Serie A e H | 2000 |

## <a name="azure-data-disks"></a>Dischi dati di Azure

È possibile aggiungere altri dischi dati per l'installazione di applicazioni e l'archiviazione dei dati. I dischi dati devono essere usati in qualsiasi situazione in cui si desidera un'archiviazione dei dati durevoli e reattiva. Ciascun disco dati ha una capacità massima di 1 terabyte. dimensioni Hello della macchina virtuale hello determinano il numero di dischi dati può essere collegato tooa macchina virtuale. Per ogni core della macchina virtuale, è possibile collegare due dischi dati. 

### <a name="max-data-disks-per-vm"></a>Numero massimo di dischi di dati per macchina virtuale

| Tipo | Dimensioni macchina virtuale | Numero massimo di dischi di dati per macchina virtuale |
|----|----|----|
| [Utilizzo generico](sizes-general.md) | Serie A e D | 32 |
| [Ottimizzate per il calcolo](sizes-compute.md) | Serie F | 32 |
| [Ottimizzate per la memoria](../virtual-machines-windows-sizes-memory.md) | Serie D e G | 64 |
| [Ottimizzate per l'archiviazione](../virtual-machines-windows-sizes-storage.md) | Serie L | 64 |
| [GPU](sizes-gpu.md) | Serie N | 48 |
| [Prestazioni elevate](sizes-hpc.md) | Serie A e H | 32 |

## <a name="vm-disk-types"></a>Tipi di dischi per la VM

Azure offre due tipi di dischi.

### <a name="standard-disk"></a>Disco standard

Archiviazione Standard è supportata da unità disco rigido e offre un'archiviazione conveniente con buone prestazioni. I dischi standard sono ideali per un carico di lavoro di test e sviluppo conveniente.

### <a name="premium-disk"></a>Disco premium

I dischi premium sono supportati da un disco a bassa latenza e ad alte prestazioni basato su SSD. Ideale per le macchine virtuali che eseguono il carico di lavoro della produzione. L'archiviazione premium supporta le macchine virtuali serie DS, DSv2, GS e FS. I dischi Premium sono disponibili in tre tipi (P10, P20, P30), dimensione hello del disco di hello determina il tipo di disco hello. Quando si seleziona, un valore di hello dimensioni disco viene arrotondato per eccesso tipo successivo toohello. Ad esempio, se dimensioni hello sono inferiore al tipo di disco hello 128 GB sarà P10, tra più di 512 P30 129 e 512 P20. 

### <a name="premium-disk-performance"></a>Prestazioni disco premium

|Tipo di disco di Archiviazione Premium | P10 | P20 | P30 |
| --- | --- | --- | --- |
| Dimensioni del disco (arrotondate) | 128 GB | 512 GB | 1.024 GB (1 TB) |
| IOPS per disco | 500 | 2.300 | 5.000 |
Velocità effettiva per disco | 100 MB/s | 150 MB/s | 200 MB/s |

Mentre hello sopra tabella identifica massimo di IOPS per disco, un livello di prestazioni superiore può essere ottenuto lo striping di più dischi dati. Ad esempio, i dati di 64 dischi possono essere collegati tooStandard_GS5 VM. Se ognuno di questi dischi viene ridimensionato come un P30, è possibile ottenere un massimo di 80.000 operazioni di I/O al secondo. Per informazioni dettagliate sul numero massimo di operazioni di I/O al secondo per macchina virtuale, vedere [Dimensioni delle VM Linux](./sizes.md).

## <a name="create-and-attach-disks"></a>Creare e collegare dischi

esempio di hello toocomplete in questa esercitazione, è necessario disporre di una macchina virtuale esistente. Se necessario, questo [script di esempio](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) può crearne una appositamente. Quando il lavoro esercitazione hello, sostituire il gruppo di risorse di hello e VM nomi dove necessario.

Creare la configurazione iniziale di hello con [New AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig). Hello di esempio seguente consente di configurare un disco, ovvero 128 gigabyte di spazio.

```powershell
$diskConfig = New-AzureRmDiskConfig -Location EastUS -CreateOption Empty -DiskSizeGB 128
```

Creare il disco di dati hello con hello [New AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk) comando.

```powershell
$dataDisk = New-AzureRmDisk -ResourceGroupName myResourceGroup -DiskName myDataDisk -Disk $diskConfig
```

Macchina virtuale di hello Get che si desidera hello toowith di tooadd hello dati disco [Get AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) comando.

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

Aggiungi hello dati disco toohello configurazione della macchina virtuale con hello [Aggiungi AzureRmVMDataDisk](/powershell/module/azurerm.compute/add-azurermvmdatadisk) comando.

```powershell
$vm = Add-AzureRmVMDataDisk -VM $vm -Name myDataDisk -CreateOption Attach -ManagedDiskId $dataDisk.Id -Lun 1
```

Aggiornare la macchina virtuale hello con hello [aggiornamento AzureRmVM](/powershell/module/azurerm.compute/add-azurermvmdatadisk) comando.

```powershell
Update-AzureRmVM -ResourceGroupName myResourceGroup -VM $vm
```

## <a name="prepare-data-disks"></a>Preparare i dischi di dati

Dopo aver macchina virtuale toohello collegato, un disco del sistema operativo hello deve toobe configurato toouse hello disco. Hello esempio seguente viene illustrato come toomanually Configura primo disco hello aggiunto toohello macchina virtuale. È inoltre possibile automatizzare questo processo utilizzando hello [estensione script personalizzata](./tutorial-automate-vm-deployment.md).

### <a name="manual-configuration"></a>Configurazione manuale

Creare una connessione RDP con la macchina virtuale hello. Aprire PowerShell ed eseguire questo script.

```powershell
Get-Disk | Where partitionstyle -eq 'raw' | `
Initialize-Disk -PartitionStyle MBR -PassThru | `
New-Partition -AssignDriveLetter -UseMaximumSize | `
Format-Volume -FileSystem NTFS -NewFileSystemLabel "myDataDisk" -Confirm:$false
```

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione sono stati descritti argomenti relativi ai dischi delle VM, ad esempio:

> [!div class="checklist"]
> * Dischi del sistema operativo e dischi temporanei
> * Dischi dati
> * Dischi Standard e Premium
> * Prestazioni dei dischi
> * Collegamento e preparazione dei dischi dati

Spostare toohello Avanti toolearn esercitazione sull'automazione di configurazione della macchina virtuale.

> [!div class="nextstepaction"]
> [Automatizzare la configurazione delle macchine virtuali](./tutorial-automate-vm-deployment.md)
