---
title: aaaCreate una copia di un disco gestito di Azure per eseguire il backup | Documenti Microsoft
description: Informazioni su come toocreate una copia di un toouse disco gestito di Azure per eseguire il backup o sulla risoluzione dei problemi di disco problemi.
documentationcenter: 
author: cwatson-cat
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 15eb778e-fc07-45ef-bdc8-9090193a6d20
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 2/9/2017
ms.author: cwatson
ms.openlocfilehash: 2f33dbbee624bcd813f3c7c3e3401072d0933714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a>Creare una copia di un disco rigido virtuale archiviato come disco gestito di Azure usando snapshot gestiti
Creare uno snapshot di un disco gestito per il backup o creare un disco gestito da snapshot hello e collegarlo tootroubleshoot macchina virtuale di test tooa. Uno snapshot gestito è una copia temporizzata completa di un disco gestito di macchina virtuale. Uno snapshot crea una copia di sola lettura del disco rigido virtuale che, per impostazione predefinita, viene memorizzato come disco gestito Standard. Per altre informazioni sui dischi gestiti, vedere [Azure Managed Disks overview](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Panoramica di Azure Managed Disks).

Per informazioni sui prezzi, vedere [Prezzi di Archiviazione di Azure](https://azure.microsoft.com/pricing/details/managed-disks/). 

## <a name="before-you-begin"></a>Prima di iniziare
Se si usa PowerShell, assicurarsi di aver hello la versione più recente del modulo AzureRM.Compute PowerShell hello. Eseguire hello seguenti comando tooinstall.

```
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Per altre informazioni, vedere [Controllo delle versioni di Azure PowerShell](/powershell/azure/overview).

## <a name="copy-hello-vhd-with-a-snapshot"></a>Copiare hello disco rigido virtuale con uno snapshot
Utilizzare hello portale di Azure o PowerShell tootake uno snapshot di hello disco gestito.

### <a name="use-azure-portal-tootake-a-snapshot"></a>Utilizzare tootake portale Azure uno snapshot 

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. A partire da in alto a sinistra di hello, fare clic su **New** e cercare **snapshot**.
3. Nel Pannello di Snapshot hello, fare clic su **crea**.
4. Immettere un **nome** per snapshot hello.
5. Selezionare un oggetto esistente [gruppo di risorse](../../azure-resource-manager/resource-group-overview.md#resource-groups) o nome di tipo hello uno nuovo. 
6. Selezionare una località per il data center di Azure.  
7. Per **disco di origine**, selezionare hello toosnapshot disco gestito.
8. Seleziona hello **tipo di Account** snapshot di hello toostore toouse. È consigliabile usare il tipo **Standard_LRS** a meno che non sia necessario archiviare lo snapshot su un disco a prestazioni elevate.
9. Fare clic su **Crea**.

### <a name="use-powershell-tootake-a-snapshot"></a>Utilizzare PowerShell tootake uno snapshot
Hello passaggi seguenti mostrano come tooget hello VHD disco toobe copiati, creare configurazioni di snapshot di hello e uno snapshot del disco hello utilizzando il cmdlet New-AzureRmSnapshot hello<!--Add link toocmdlet when available-->. 

1. Impostare alcuni parametri. 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$location = 'southeastasia' 
$dataDiskName = 'ContosoMD_datadisk1' 
$snapshotName = 'ContosoMD_datadisk1_snapshot1'  
```
  Sostituire i valori di parametro hello:
  -  "myResourceGroup" con il gruppo di risorse della macchina virtuale di hello.
  -  "southeastasia" con l'area geografica hello in cui si desidera lo Snapshot gestito archiviato. <!---How do you look these up? -->
  -  "ContosoMD_datadisk1" con il nome di hello del disco VHD hello che si desidera toocopy.
  -  "ContosoMD_datadisk1_snapshot1" con hello nome che si desidera toouse del nuovo snapshot hello.

2. Ottenere hello VHD disco toobe copiati.

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $dataDiskName 
```
3. Creare configurazioni di snapshot di hello. 

 ```powershell
$snapshot =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -CreateOption Copy -Location $location 
```
4. Creare snapshot hello.

 ```powershell
New-AzureRmSnapshot -Snapshot $snapshot -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName 
```
Se si prevede toouse hello snapshot toocreate un disco gestito e collegarlo a una macchina virtuale che deve toobe a prestazioni elevate, utilizzare il parametro hello `-AccountType Premium_LRS` con il comando New-AzureRmSnapshot hello. il parametro Hello Crea snapshot hello in modo che viene archiviato come un disco gestito Premium. I dischi gestiti Premium sono più costosi di quelli Standard. Pertanto, assicurarsi che l'opzione Premium sia realmente necessaria prima di usare tale parametro.


