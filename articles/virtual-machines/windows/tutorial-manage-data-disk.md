---
title: Gestire i dischi di Azure con Azure PowerShell | Microsoft Docs
description: 'Esercitazione: gestire i dischi di Azure con Azure PowerShell'
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
ms.openlocfilehash: 6f1bc9361745adc211f22416a7ba8ac1b8dc614e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-disks-with-powershell"></a>Gestire i dischi di Azure con PowerShell

Le macchine virtuali di Azure usano dischi per archiviare sistema operativo, applicazioni e dati di VM. Quando si crea una VM, è importante scegliere dimensione del disco e configurazione appropriate per il carico di lavoro previsto. Questa esercitazione illustra la distribuzione e la gestione dei dischi di VM. Vengono fornite informazioni su:

> [!div class="checklist"]
> * Dischi del sistema operativo e dischi temporanei
> * Dischi dati
> * Dischi Standard e Premium
> * Prestazioni dei dischi
> * Collegamento e preparazione dei dischi dati

Questa esercitazione richiede il modulo Azure PowerShell 3.6 o versioni successive. Eseguire ` Get-Module -ListAvailable AzureRM` per trovare la versione. Se è necessario eseguire l'aggiornamento, vedere [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps) (Installare il modulo di Azure PowerShell).

## <a name="default-azure-disks"></a>Dischi di Azure predefiniti

Quando viene creata una macchina virtuale di Azure, due dischi vengono automaticamente collegati alla macchina virtuale. 

**Disco del sistema operativo**: i dischi del sistema operativo possono essere ridimensionati fino a 1 terabyte e ospitano il sistema operativo delle macchine virtuali.  Al disco del sistema operativo viene assegnata una lettera di unità *c:* per impostazione predefinita. La configurazione della memorizzazione nella cache del disco del sistema operativo è ottimizzata per le prestazioni del sistema operativo. Il disco del sistema operativo **non deve** ospitare applicazioni o dati. Per le applicazioni e i dati, usare un disco dati, descritto in dettaglio più avanti in questo articolo.

**Disco temporaneo**: i dischi temporanei usano un'unità SSD che si trova nello stesso host della macchina virtuale di Azure. I dischi temporanei sono altamente efficienti e possono essere usati per operazioni quali l'elaborazione dei dati temporanei. Tuttavia, se la macchina virtuale viene spostata in un nuovo host, tutti i dati memorizzati su un disco temporaneo vengono rimossi. Le dimensioni del disco temporaneo sono determinate dalle dimensioni della macchina virtuale. Ai dischi temporanei viene assegnata una lettera di unità *d:* per impostazione predefinita.

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

È possibile aggiungere altri dischi dati per l'installazione di applicazioni e l'archiviazione dei dati. I dischi dati devono essere usati in qualsiasi situazione in cui si desidera un'archiviazione dei dati durevoli e reattiva. Ciascun disco dati ha una capacità massima di 1 terabyte. Le dimensione della macchina virtuale determinano il numero di dischi dati possono essere collegati a una macchina virtuale. Per ogni core della macchina virtuale, è possibile collegare due dischi dati. 

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

I dischi premium sono supportati da un disco a bassa latenza e ad alte prestazioni basato su SSD. Ideale per le macchine virtuali che eseguono il carico di lavoro della produzione. L'archiviazione premium supporta le macchine virtuali serie DS, DSv2, GS e FS. I dischi premium sono di tre tipi, P10, P20 e P30. Le dimensioni del disco determinano il tipo di disco. Quando si effettua la selezione, il valore delle dimensioni di un disco viene arrotondato per eccesso al tipo successivo. Ad esempio, se la dimensione è inferiore a 128 GB il tipo di disco sarà P10, se è tra 129 e 512 GB sarà P20 e oltre 512 GB sarà P30. 

### <a name="premium-disk-performance"></a>Prestazioni disco premium

|Tipo di disco di Archiviazione Premium | P10 | P20 | P30 |
| --- | --- | --- | --- |
| Dimensioni del disco (arrotondate) | 128 GB | 512 GB | 1.024 GB (1 TB) |
| IOPS per disco | 500 | 2.300 | 5.000 |
Velocità effettiva per disco | 100 MB/s | 150 MB/s | 200 MB/s |

Sebbene la tabella sopra riportata identifichi il numero massimo di operazioni di I/O al secondo per disco, è possibile raggiungere un livello superiore di prestazioni tramite lo striping di più dischi di dati. Ad esempio, è possibile collegare 64 dati dischi alla macchina virtuale Standard_GS5. Se ognuno di questi dischi viene ridimensionato come un P30, è possibile ottenere un massimo di 80.000 operazioni di I/O al secondo. Per informazioni dettagliate sul numero massimo di operazioni di I/O al secondo per macchina virtuale, vedere [Dimensioni delle VM Linux](./sizes.md).

## <a name="create-and-attach-disks"></a>Creare e collegare dischi

Per completare l'esempio contenuto in questa esercitazione è necessario disporre di una macchina virtuale esistente. Se necessario, questo [script di esempio](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) può crearne una appositamente. Quando si esegue l'esercitazione, sostituire i nomi del gruppo di risorse e delle macchine virtuali dove necessario.

Creare la configurazione iniziale con [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig). L'esempio seguente configura un disco delle dimensioni di 128 GB.

```powershell
$diskConfig = New-AzureRmDiskConfig -Location EastUS -CreateOption Empty -DiskSizeGB 128
```

Creare il disco dati con il comando [New-AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk).

```powershell
$dataDisk = New-AzureRmDisk -ResourceGroupName myResourceGroup -DiskName myDataDisk -Disk $diskConfig
```

Ottenere la macchina virtuale a cui si vuole aggiungere il disco dati con il comando [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm).

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

Aggiungere il disco dati alla configurazione della macchina virtuale con il comando [Add-AzureRmVMDataDisk](/powershell/module/azurerm.compute/add-azurermvmdatadisk).

```powershell
$vm = Add-AzureRmVMDataDisk -VM $vm -Name myDataDisk -CreateOption Attach -ManagedDiskId $dataDisk.Id -Lun 1
```

Aggiornare la macchina virtuale con il comando [Update-AzureRmVM](/powershell/module/azurerm.compute/add-azurermvmdatadisk).

```powershell
Update-AzureRmVM -ResourceGroupName myResourceGroup -VM $vm
```

## <a name="prepare-data-disks"></a>Preparare i dischi di dati

Dopo aver collegato un disco alla macchina virtuale, il sistema operativo deve essere configurato per l'uso del disco. Nell'esempio seguente viene illustrato come configurare manualmente il primo disco aggiunto alla macchina virtuale. Questo processo può essere automatizzato tramite l'[estensione dello script personalizzata](./tutorial-automate-vm-deployment.md).

### <a name="manual-configuration"></a>Configurazione manuale

Creare una connessione RDP alla macchina virtuale. Aprire PowerShell ed eseguire questo script.

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

Passare all'esercitazione successiva per informazioni sull'automazione della configurazione delle macchine virtuali.

> [!div class="nextstepaction"]
> [Automatizzare la configurazione delle macchine virtuali](./tutorial-automate-vm-deployment.md)
