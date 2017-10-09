---
title: disco del sistema operativo aaaExpand in VM Linux con hello Azure CLI 1.0 | Documenti Microsoft
description: Informazioni su come tooexpand hello disco virtuale del sistema operativo (sistema operativo) in una VM Linux utilizzando hello Azure CLI 1.0 e modello di distribuzione di gestione risorse di hello
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 0db78c0b86b48b2c5358611e11bb0b7ad781a559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="expand-os-disk-on-a-linux-vm-using-hello-azure-cli-with-hello-azure-cli-10"></a>Espandere il disco del sistema operativo in una VM Linux con hello Azure CLI hello Azure CLI 1.0
dimensioni di disco rigido virtuale Hello predefinite per il sistema operativo hello (sistema operativo) sono in genere 30 GB in una macchina virtuale Linux (VM) in Azure. È possibile [aggiungere dischi dati](add-disk.md) tooprovide per ulteriore spazio di archiviazione, ma è inoltre possibile del disco del sistema operativo hello tooexpand. In questo articolo illustra in dettaglio come tooexpand hello del sistema operativo del disco per una VM Linux con dischi non gestiti hello Azure CLI 1.0.

## <a name="cli-versions-toocomplete-hello-task"></a>Attività hello toocomplete versioni CLI
È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:

- [Azure CLI 1.0](#prerequisites) : l'interfaccia CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)
- [Azure CLI 2.0](expand-disks.md) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello

## <a name="prerequisites"></a>Prerequisiti
È necessario hello [più recente di Azure CLI 1.0](../../cli-install-nodejs.md) installato e registrato nel tooan [account Azure](https://azure.microsoft.com/pricing/free-trial/) utilizzando la modalità di gestione risorse hello nel modo seguente:

```azurecli
azure config mode arm
```

In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati. I nomi dei parametri di esempio includono *myResourceGroup* e *myVM*.

## <a name="expand-os-disk"></a>Espandere il disco del sistema operativo

1. Impossibile eseguire operazioni su dischi rigidi virtuali con hello macchina virtuale in esecuzione. Arresta Hello riportato e dealloca hello macchina virtuale denominata *myVM* nel gruppo di risorse hello denominato *myResourceGroup*:

    ```azurecli
    azure vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > `azure vm stop`non rilasciare le risorse di calcolo hello. toorelease le risorse di calcolo, utilizzare `azure vm deallocate`. Hello VM deve essere deallocata il disco rigido virtuale di tooexpand hello.

2. Aggiornare hello dimensioni del disco del sistema operativo hello non gestita usando hello `azure vm set` comando. dopo gli aggiornamenti di esempio Hello hello macchina virtuale denominata *myVM* nel gruppo di risorse hello denominato *myResourceGroup* toobe *50* GB:

    ```azurecli
    azure vm set \
        --resource-group myResourceGroup \
        --name myVM \
        --new-os-disk-size 50
    ```

3. Avviare la macchina virtuale come segue:

    ```azurecli
    azure vm start --resource-group myResourceGroup --name myVM
    ```

4. SSH tooyour VM con le credenziali appropriate hello. disco del sistema operativo hello tooverify è stato ridimensionato, utilizzare `df -h`. Hello output di esempio seguente mostra la partizione primaria hello (*dev/sda1*) ora è di 50 GB:

    ```bash
    Filesystem      Size  Used Avail Use% Mounted on
    udev            1.7G     0  1.7G   0% /dev
    tmpfs           344M  5.0M  340M   2% /run
    /dev/sda1        49G  1.3G   48G   3% /
    ```

## <a name="next-steps"></a>Passaggi successivi
Se è necessario ulteriore spazio di archiviazione, è anche [aggiungere tooa dischi dati VM Linux](add-disk.md). Per ulteriori informazioni sulla crittografia del disco, vedere [Encrypt dischi in una VM Linux utilizzando hello Azure CLI](encrypt-disks.md).
