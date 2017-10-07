---
title: aaaCopy del disco per il backup di un gestito di Azure | Documenti Microsoft
description: Informazioni su come toocreate una copia di un toouse disco gestito di Azure per eseguire il backup o sulla risoluzione dei problemi di disco problemi.
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 2/6/2017
ms.author: rasquill
ms.openlocfilehash: 41b91c2d68eb5be9c493a66be5f7d085a70450d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a>Creare una copia di un disco rigido virtuale archiviato come disco gestito di Azure usando snapshot gestiti
Creare uno snapshot di un disco gestito per il backup o creare un disco gestito da snapshot hello e collegarlo tootroubleshoot macchina virtuale di test tooa. Uno snapshot gestito è una copia temporizzata completa di un disco gestito di macchina virtuale. Uno snapshot crea una copia di sola lettura del disco rigido virtuale che, per impostazione predefinita, viene memorizzato come disco gestito Standard. 

Per informazioni sui prezzi, vedere [Prezzi di Archiviazione di Azure](https://azure.microsoft.com/pricing/details/managed-disks/). <!--Add link tootopic or blog post that explains managed disks. -->

Utilizzare entrambi hello Azure tootake di CLI di Azure 2.0 portale o hello uno snapshot di hello disco gestito.

## <a name="use-azure-cli-20-tootake-a-snapshot"></a>Utilizzare Azure CLI 2.0 tootake uno snapshot

> [!NOTE] 
> Hello esempio seguente richiede hello Azure CLI 2.0 installati e registrati nell'account Azure.

Hello passaggi seguenti viene illustrato come tooobtain e creare uno snapshot di un sistema operativo gestito disco utilizzando hello `az snapshot create` con hello `--source-disk` parametro. Hello seguente si presuppone che sia presente una macchina virtuale denominata `myVM` creato con un disco del sistema operativo gestito in hello `myResourceGroup` gruppo di risorse.

```azure-cli
# take hello disk id with which toocreate a snapshot
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create -g myResourceGroup --source "$osDiskId" --name osDisk-backup
```

output di Hello dovrebbe essere simile al seguente:

```json
{
  "accountType": "Standard_LRS",
  "creationData": {
    "createOption": "Copy",
    "imageReference": null,
    "sourceResourceId": null,
    "sourceUri": "/subscriptions/<guid>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/disks/osdisk_6NexYgkFQU",
    "storageAccountId": null
  },
  "diskSizeGb": 30,
  "encryptionSettings": null,
  "id": "/subscriptions/<guid>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/snapshots/osDisk-backup",
  "location": "westus",
  "name": "osDisk-backup",
  "osType": "Linux",
  "ownerId": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "tags": null,
  "timeCreated": "2017-02-06T21:27:10.172980+00:00",
  "type": "Microsoft.Compute/snapshots"
}
```

## <a name="use-azure-portal-tootake-a-snapshot"></a>Utilizzare tootake portale Azure uno snapshot 

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. A partire da hello angolo superiore sinistro, fare clic su **New** e cercare **snapshot**.
3. Nel Pannello di Snapshot hello, fare clic su **crea**.
4. Immettere un **nome** per snapshot hello.
5. Selezionare un oggetto esistente [gruppo di risorse](../../azure-resource-manager/resource-group-overview.md#resource-groups) o nome di tipo hello uno nuovo. 
6. Selezionare una località per il data center di Azure.  
7. Per **disco di origine**, selezionare hello toosnapshot disco gestito.
8. Seleziona hello **tipo di Account** snapshot di hello toostore toouse. È consigliabile usare il tipo **Standard_LRS** a meno che non sia necessario archiviare lo snapshot su un disco a prestazioni elevate.
9. Fare clic su **Crea**.

Se si prevede toouse hello snapshot toocreate un disco gestito e collegarlo a una macchina virtuale che deve toobe a prestazioni elevate, utilizzare il parametro hello `--sku Premium_LRS` con hello `az snapshot create` comando. Questo crea snapshot hello in modo che viene archiviato come un disco gestito Premium. Managed Disks Premium offre prestazioni migliori perché consiste in unità SSD, ma con un costo superiore rispetto ai dischi Standard (HDD).


