---
title: un disco gestito da un disco rigido virtuale in Azure aaaCreate | Documenti Microsoft
description: "Creare un disco gestito da un disco rigido virtuale che è attualmente in un account di archiviazione Azure tramite hello modello di distribuzione di gestione delle risorse."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/05/2017
ms.author: cynthn
ms.openlocfilehash: 77adaac5419186ff85039fe2c4752f021aa5e448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-managed-disks-from-unmanaged-disks-in-a-storage-account"></a>Creare dischi gestiti da dischi non gestiti in un account di archiviazione

Un disco gestito può essere creato da un disco dati esistente o da un disco del sistema operativo che si trova attualmente in un account di archiviazione di Azure. È anche possibile creare un disco vuoto da usare come nuovo disco dati per una VM. 

## <a name="before-you-begin"></a>Prima di iniziare
Se si usa PowerShell, assicurarsi di aver hello la versione più recente del modulo AzureRM.Compute PowerShell hello. Eseguire hello seguenti comando tooinstall.

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Per altre informazioni, vedere [Controllo delle versioni di Azure PowerShell](/powershell/azure/overview).


## <a name="create-a-managed-disk-from-a-vhd-in-an-azure-storage-account"></a>Creare un disco gestito da un disco rigido virtuale in un account di archiviazione di Azure

Nell'esempio hello è creare un disco da un file VHD come disco gestito e assegnarlo parametro toohello **$Disco1** toouse in un secondo momento. 

Hello gestito verrà creato un disco in hello **degli Stati Uniti occidentali** percorso, in un gruppo di risorse denominato **myResourceGroup**. verrà denominato disco Hello **myDisk** e verrà creato da un file di disco rigido virtuale denominato **myDisk.vhd** è caricato in precedenza denominato account di archiviazione di tooa **mystorageaccount**. disco gestito Hello verrà creata nel servizio di archiviazione con ridondanza locale premium (LRS). StandardLRS e PremiumLRS sono solo hello **- AccountType** opzioni disponibili per i dischi gestiti. 

1.  Impostare alcuni parametri

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $diskName = "myDisk"
    $vhdUri = "https://mystorageaccount.blob.core.windows.net/vhds/myDisk.vhd"
    ```

2. Creare il disco di dati hello. 
    ```powershell
    $disk1 = New-AzureRmDisk -DiskName $diskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $vhdUri) -ResourceGroupName $rgName
    ```
    
    

## <a name="create-an-empty-data-disk-as-a-managed-disk"></a>Creare un disco dati vuoto come disco gestito

Nell'esempio hello verrà creato un disco dati vuoto come disco gestito e assegnarlo parametro toohello **$dataDisk2** toouse in un secondo momento. Un disco dati vuoto sarà necessario toobe inizializzato accesso toohello macchina virtuale e utilizzare diskmgmt.msc o [in modalità remota tramite Gestione remota Windows e uno script](attach-disk-ps.md#initialize-the-disk), una volta collegato tooa in esecuzione sulla macchina virtuale.

verrà creato un disco dati vuoto Hello in hello **occidentale Stati Uniti centro** percorso, in un gruppo di risorse denominato **myResourceGroup**. verrà denominato disco Hello **myEmptyDataDisk**. verrà creato un disco vuoto Hello in archiviazione con ridondanza locale premium (LRS). StandardLRS e PremiumLRS sono solo hello **- AccountType** opzioni disponibili per i dischi gestiti.

dimensioni del disco Hello in questo esempio sono 128GB, ma è consigliabile scegliere una dimensione soddisfa le esigenze di hello di tutte le applicazioni in esecuzione nella macchina virtuale.

1.  Impostare alcuni parametri

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $dataDiskName = "myEmptyDataDisk"
    ```

2. Creare il disco di dati hello.
    ```powershell
    $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Empty -DiskSizeGB 128) -ResourceGroupName $rgName
    ```
    
## <a name="next-steps"></a>Passaggi successivi   
- Se si dispone già di una macchina virtuale, è possibile [collegare un disco dati](attach-disk-portal.md).
