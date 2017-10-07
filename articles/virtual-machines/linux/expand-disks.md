---
title: aaaExpand i dischi rigidi virtuali in una VM Linux di Azure | Documenti Microsoft
description: Informazioni su come tooexpand i dischi rigidi virtuali in una VM Linux con hello Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: 7c09a682cb4322c027e57667640e8f1f8e6612f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooexpand-virtual-hard-disks-on-a-linux-vm-with-hello-azure-cli"></a>Come tooexpand i dischi rigidi virtuali in una VM Linux con hello CLI di Azure
dimensioni di disco rigido virtuale Hello predefinite per il sistema operativo hello (sistema operativo) sono in genere 30 GB in una macchina virtuale Linux (VM) in Azure. È possibile [aggiungere dischi dati](add-disk.md) tooprovide per ulteriore spazio di archiviazione, ma è inoltre possibile tooexpand un disco dati esistente. In questo articolo illustra in dettaglio come dischi tooexpand gestiti per una VM Linux con hello CLI di Azure 2.0. È anche possibile espandere il disco del sistema operativo hello non gestita con hello [CLI di Azure 1.0](expand-disks-nodejs.md).

> [!WARNING]
> Assicurarsi sempre di eseguire il backup dei dati prima di eseguire operazioni di ridimensionamento dei dischi. Per altre informazioni, vedere [Eseguire il backup di macchine virtuali Linux in Azure](tutorial-backup-vms.md).

## <a name="expand-disk"></a>Espandere il disco
Assicurarsi di aver hello più recente [CLI di Azure 2.0](/cli/azure/install-az-cli2) installato e registrato con un account Azure tooan [accesso az](/cli/azure/#login).

Questo articolo richiede una VM esistente in Azure con almeno un disco dati collegato e preparato. Se non si ha già una VM da usare, vedere [Creare e preparare una VM con dischi dati](tutorial-manage-disks.md#create-and-attach-disks).

In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati. I nomi dei parametri di esempio includono *myResourceGroup* e *myVM*.

1. Impossibile eseguire operazioni su dischi rigidi virtuali con hello macchina virtuale in esecuzione. Deallocare la macchina virtuale con [az vm deallocate](/cli/azure/vm#deallocate). esempio Hello dealloca hello macchina virtuale denominata *myVM* nel gruppo di risorse hello denominato *myResourceGroup*:

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > `az vm stop`non rilasciare le risorse di calcolo hello. toorelease le risorse di calcolo, utilizzare `az vm deallocate`. Hello VM deve essere deallocata il disco rigido virtuale di tooexpand hello.

2. Vedere un elenco di dischi gestiti presenti nel gruppo di risorse con [az disk list](/cli/azure/disk#list). Hello esempio seguente visualizza un elenco di dischi gestiti nel gruppo di risorse hello denominato *myResourceGroup*:

    ```azurecli
    az disk list \
        --resource-group myResourceGroup \
        --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' \
        --output table
    ```

    Espandere hello disco necessarie con [aggiornamento disco az](/cli/azure/disk#update). esempio Hello espande disco di hello gestito denominato *myDataDisk* toobe *200*dimensioni Gb:

    ```azurecli
    az disk update \
        --resource-group myResourceGroup \
        --name myDataDisk \
        --size-gb 200
    ```

    > [!NOTE]
    > Quando si espande un disco gestito, dimensioni hello aggiornato sono mappato toohello più vicino delle dimensioni del disco gestito. Per una tabella di dimensioni disco gestito disponibili hello e livelli, vedere [gestiti dischi Panoramica di Azure - prezzi e fatturazione](../windows/managed-disks-overview.md#pricing-and-billing).

3. Avviare la macchina virtuale con [az vm start](/cli/azure/vm#start). Dopo l'avvio di esempio Hello hello macchina virtuale denominata *myVM* nel gruppo di risorse hello denominato *myResourceGroup*:

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

4. SSH tooyour VM con le credenziali appropriate hello. È possibile ottenere l'indirizzo IP pubblico hello della macchina virtuale con [Mostra vm az](/cli/azure/vm#show):

    ```azurecli
    az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
    ```

5. hello toouse espansa del disco, è necessario filesystem e partizione di tooexpand hello sottostante.

    a. Se è già montato, smontare il disco hello:

    ```bash
    sudo umount /dev/sdc1
    ```

    b. Utilizzare `parted` tooview informazioni sul disco e ridimensionare partizione hello:

    ```bash
    sudo parted /dev/sdc
    ```

    Consente di visualizzare informazioni sul layout di partizione esistente di hello con `print`. l'output è simile toohello seguente esempio, disco sottostante hello è Gb 215 dimensioni Hello:

    ```bash
    GNU Parted 3.2
    Using /dev/sdc1
    Welcome tooGNU Parted! Type 'help' tooview a list of commands.
    (parted) print
    Model: Unknown Msft Virtual Disk (scsi)
    Disk /dev/sdc1: 215GB
    Sector size (logical/physical): 512B/4096B
    Partition Table: loop
    Disk Flags:
    
    Number  Start  End    Size   File system  Flags
        1      0.00B  107GB  107GB  ext4
    ```

    c. Espandere la partizione hello con `resizepart`. Immettere il numero di partizione hello, *1*e una dimensione per la nuova partizione hello:

    ```bash
    (parted) resizepart
    Partition number? 1
    End?  [107GB]? 215GB
    ```

    d. tooexit, immettere`quit`

5. Con partizione hello ridimensionato, verificare la coerenza di partizione hello con `e2fsck`:

    ```bash
    sudo e2fsck -f /dev/sdc1
    ```

6. Ora ridimensionare filesystem hello con `resize2fs`:

    ```bash
    sudo resize2fs /dev/sdc1
    ```

7. Montaggio hello partizione toohello desiderati percorso, ad esempio `/datadrive`:

    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```

8. disco del sistema operativo hello tooverify è stato ridimensionato, utilizzare `df -h`. Hello output di esempio seguente viene illustrato l'unità dati hello, *dev/sdc1*, ora pari a 200 GB:

    ```bash
    Filesystem      Size   Used  Avail Use% Mounted on
    /dev/sdc1        197G   60M   187G   1% /datadrive
    ```

## <a name="next-steps"></a>Passaggi successivi
Se è necessario ulteriore spazio di archiviazione, è anche [aggiungere tooa dischi dati VM Linux](add-disk.md). Per ulteriori informazioni sulla crittografia del disco, vedere [Encrypt dischi in una VM Linux utilizzando hello Azure CLI](encrypt-disks.md).
