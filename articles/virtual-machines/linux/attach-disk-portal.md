---
title: aaaAttach un tooa disco dati VM Linux | Documenti Microsoft
description: Tooattach dati nuovi o esistenti disco tooa VM Linux in Azure mediante portale hello hello come modello di distribuzione di gestione risorse.
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 5e1c6212-976c-4962-a297-177942f90907
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: cynthn
ms.openlocfilehash: 069c3c6f5e71a8c495342e6d0c6f3d92c4ed5053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-data-disk-tooa-linux-vm-in-hello-azure-portal"></a>Funzionamento dei dischi tooa VM Linux nel portale di Azure hello tooattach un tipo di dati
Questo articolo illustra come tooattach sia nuovi che esistenti dischi di macchina virtuale di Linux tooa tramite hello portale di Azure. È anche possibile [collegare un tooa di disco dati macchina virtuale di Windows nel portale di Azure hello](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). È possibile scegliere toouse entrambi i dischi di Azure gestiti o non gestito di dischi. Dischi gestiti vengono gestiti dal hello piattaforma Azure e non richiedono alcun toostore preparazione o percorso li. I dischi non gestiti richiedono un account di archiviazione e presentano alcune [quote e limiti applicati](../../azure-subscription-service-limits.md#storage-limits). Per altre informazioni su Azure Managed Disks, vedere [Azure Managed Disks overview](../windows/managed-disks-overview.md) (Panoramica di Azure Managed Disks).

Prima di collegare i dischi tooyour VM, esaminare i seguenti suggerimenti:

* dimensioni di Hello della macchina virtuale hello controlla il numero di dischi dati è possibile collegare. Per informazioni dettagliate, vedere [Dimensioni delle macchine virtuali](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* toouse archiviazione Premium, è necessario una macchina virtuale serie DS o GS-series. Con queste macchine virtuali, è possibile usare dischi Premium e Standard. L’archiviazione Premium è disponibile solo in determinate aree geografiche. Per ulteriori informazioni, vedere [Archiviazione Premium: archiviazione ad alte prestazioni per carichi di lavoro delle macchine virtuali di Azure](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* I dischi collegati toovirtual macchine sono effettivamente i file con estensione vhd archiviati in Azure. Per informazioni dettagliate, vedere [Informazioni sui dischi e sui dischi rigidi virtuali per le macchine virtuali](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


## <a name="find-hello-virtual-machine"></a>Trovare la macchina virtuale hello
1. Accedi toohello [portale di Azure](https://portal.azure.com/).
2. Nel menu Hub hello, fare clic su **macchine virtuali**.
3. Selezionare macchina virtuale hello hello elenco.
4. toohello virtuale macchine pannello **Essentials**, fare clic su **dischi**.
   
    ![Aprire le impostazioni del disco](./media/attach-disk-portal/find-disk-settings.png)

Continuare seguendo le istruzioni per il collegamento di un [disco gestito](#use-azure-managed-disks) o di un [disco non gestito](#use-unmanaged-disks).

## <a name="use-azure-managed-disks"></a>Usare Azure Managed Disks

### <a name="attach-a-new-disk"></a>Collegare un nuovo disco

1. In hello **dischi** pannello, fare clic su **+ Aggiungi disco di dati**.
2. Fare clic sul menu a discesa hello **nome** e selezionare **Crea disco**:

    ![Creare un disco gestito Azure](./media/attach-disk-portal/create-new-md.png)

3. Immettere un nome per il disco gestito. Esaminare le impostazioni predefinite di hello, aggiornare, se necessario e quindi fare clic su **crea**.
   
   ![Esaminare le impostazioni del disco](./media/attach-disk-portal/create-new-md-settings.png)

4. Fare clic su **salvare** toocreate hello gestiti disco e aggiornamento configurazione della macchina virtuale hello:

   ![Salvare il nuovo disco gestito Azure](./media/attach-disk-portal/confirm-create-new-md.png)

5. Dopo che Azure crea un disco hello e lo collega macchina virtuale toohello, nuovo disco hello è elencato nelle impostazioni del disco della macchina virtuale hello in **dischi dati**. I dischi gestiti sono una risorsa di primo livello e disco hello viene visualizzato nella radice di hello hello del gruppo di risorse:

   ![Disco gestito Azure nel gruppo di risorse](./media/attach-disk-portal/view-md-resource-group.png)

### <a name="attach-an-existing-disk"></a>Collegare un disco esistente
1. In hello **dischi** pannello, fare clic su **+ Aggiungi disco di dati**.
2. Fare clic sul menu a discesa hello **nome** tooview un elenco esistente gestito dischi accessibili tooyour sottoscrizione di Azure. Seleziona hello gestito tooattach disco:

   ![Collegare il disco gestito di Azure](./media/attach-disk-portal/select-existing-md.png)

3. Fare clic su **salvare** tooattach hello esistenti gestiti disco e aggiornamento configurazione della macchina virtuale hello:
   
   ![Salvare gli aggiornamenti del disco gestito Azure](./media/attach-disk-portal/confirm-attach-existing-md.png)

4. Dopo il collega Azure hello macchina virtuale di toohello disco, viene elencata per le impostazioni del disco della macchina virtuale hello in **dischi dati**.

## <a name="use-unmanaged-disks"></a>Usare i dischi non gestiti

### <a name="attach-a-new-disk"></a>Collegare un nuovo disco

1. In hello **dischi** pannello, fare clic su **+ Aggiungi disco di dati**.
2. Esaminare le impostazioni predefinite di hello, aggiornare, se necessario e quindi fare clic su **OK**.
   
   ![Esaminare le impostazioni del disco](./media/attach-disk-portal/attach-new.png)
3. Dopo che Azure crea un disco hello e lo collega macchina virtuale toohello, nuovo disco hello è elencato nelle impostazioni del disco della macchina virtuale hello in **dischi dati**.

### <a name="attach-an-existing-disk"></a>Collegare un disco esistente
1. In hello **dischi** pannello, fare clic su **+ Aggiungi disco di dati**.
2. In **Collega un disco esistente** fare clic su **File VHD**.
   
   ![Collegare un disco esistente](./media/attach-disk-portal/attach-existing.png)
3. In **gli account di archiviazione**, selezionare account hello e contenitore che include i file con estensione vhd hello.
   
   ![Individuare il percorso di un VHD](./media/attach-disk-portal/find-storage-container.png)
4. Selezionare i file con estensione vhd hello.
5. In **collegare un disco esistente**, file hello appena selezionata è elencato in **File VHD**. Fare clic su **OK**.
6. Dopo il collega Azure hello macchina virtuale di toohello disco, viene elencata per le impostazioni del disco della macchina virtuale hello in **dischi dati**.


## <a name="next-steps"></a>Passaggi successivi
Dopo aver aggiunto il disco di hello, è necessario tooprepare l'utilizzo. Per ulteriori informazioni, vedere [Procedura: inizializzare un nuovo disco dati in Linux](add-disk.md).
