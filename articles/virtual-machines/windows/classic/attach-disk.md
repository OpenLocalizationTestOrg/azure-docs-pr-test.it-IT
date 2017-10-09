---
title: aaaAttach tooa un disco macchina virtuale di Azure classico | Documenti Microsoft
description: Collegare una macchina virtuale di Windows di dati su disco tooa creata con il modello di distribuzione classica hello e inizializzarlo.
services: virtual-machines-windows, storage
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: be4e3e74-05bc-4527-969f-84f10a1d66a7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/21/2017
ms.author: cynthn
ms.openlocfilehash: bfe1b0fa066277d28d3862a18da4b1023cb4452d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="attach-a-data-disk-tooa-windows-virtual-machine-created-with-hello-classic-deployment-model"></a>Collegare una macchina virtuale di Windows di dati su disco tooa creata con il modello di distribuzione classica hello
<!--
Refernce article:
    If you want toouse hello new portal, see [How tooattach a data disk tooa Windows VM in hello Azure portal](../../virtual-machines-windows-attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

In questo articolo viene illustrato come creare i dischi nuovi ed esistenti tooattach con hello Classic distribuzione modello tooa macchina virtuale Windows usando hello portale di Azure.

È anche possibile [collegare un tooa di disco dati VM Linux nel portale di Azure hello](../../linux/attach-disk-portal.md).

Prima di collegare un disco, esaminare i seguenti suggerimenti:

* dimensioni di Hello della macchina virtuale hello controlla il numero di dischi dati è possibile collegare. Per informazioni dettagliate, vedere [Dimensioni delle macchine virtuali](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

* toouse archiviazione Premium, è necessario una macchina virtuale serie DS o GS-series. È possibile utilizzare dischi dagli account di archiviazione sia Premium che Standard con queste macchine virtuali. L’archiviazione Premium è disponibile solo in determinate aree geografiche. Per ulteriori informazioni, vedere [Archiviazione Premium: archiviazione ad alte prestazioni per carichi di lavoro delle macchine virtuali di Azure](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

* Per un nuovo disco, non è necessario toocreate è primo poiché Azure crea momento del collegamento.

È anche possibile [collegare un disco dati usando Powershell](../../virtual-machines-windows-attach-disk-ps.md).

> [!IMPORTANT]
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).

## <a name="find-hello-virtual-machine"></a>Trovare la macchina virtuale hello
1. Accedi toohello [portale di Azure](https://portal.azure.com/).
2. Macchina virtuale selezionare hello dalla risorsa hello elencato nel dashboard di hello.
3. Nel riquadro sinistro di hello in **impostazioni**, fare clic su **dischi**.

    ![Aprire le impostazioni del disco](./media/attach-disk/virtualmachinedisks.png)

Continuare seguendo le istruzioni per il collegamento di un [nuovo disco](#option-1-attach-a-new-disk) o un [disco esistente](#option-2-attach-an-existing-disk).

## <a name="option-1-attach-and-initialize-a-new-disk"></a>Opzione 1: Connettere e inizializzare un nuovo disco

1. In hello **dischi** pannello, fare clic su **nuovo collegamento**.
2. Esaminare le impostazioni predefinite di hello, aggiornare, se necessario e quindi fare clic su **OK**.

   ![Esaminare le impostazioni del disco](./media/attach-disk/attach-new.png)

3. Dopo che Azure crea un disco hello e lo collega macchina virtuale toohello, nuovo disco hello è elencato nelle impostazioni del disco della macchina virtuale hello in **dischi dati**.

### <a name="initialize-a-new-data-disk"></a>Inizializzare un nuovo disco dati

1. Connessione macchina virtuale toohello. Per istruzioni, vedere [come tooconnect e tooan virtuali di Azure di accesso del computer che eseguono Windows](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
2. Dopo aver effettuato sulla macchina virtuale toohello, aprire **Server Manager**. Nel riquadro sinistro hello selezionare **servizi File e archiviazione**.

    ![Avviare Server Manager](../media/attach-disk-portal/fileandstorageservices.png)

3. Selezionare **Dischi**.
4. Hello **dischi** sezione sono elencati i dischi di hello. Nella maggior parte dei casi, avrà disco 0, disco 1 e disco 2. Disco 0 è il disco di sistema operativo hello, disco 1 è disco temporaneo hello e disco 2 è disco dati hello appena collegati macchina virtuale toohello. elenchi di disco dati Hello hello partizione come **sconosciuto**.

 Fare doppio clic su disco hello e selezionare **inizializzare**.

5. Si è inviata una notifica che tutti i dati verranno cancellati quando viene inizializzato il disco di hello. Fare clic su **Sì** tooacknowledge hello avviso e inizializzare hello su disco. Al termine dell'operazione, verrà indicata come partizione hello **GPT**. Fare nuovamente doppio clic su disco hello e selezionare **nuovo Volume**.

6. Completare Creazione guidata hello utilizzando i valori predefiniti di hello. Quando viene eseguito la procedura guidata hello, hello **volumi** sezione sono elencati nuovo volume hello. disco Hello è online e pronto toostore dati.

    ![Inizializzazione del volume completata](./media/attach-disk/newdiskafterinitialization.png)

## <a name="option-2-attach-an-existing-disk"></a>Opzione 2: Collegare un disco esistente
1. In hello **dischi** pannello, fare clic su **collegamento esistente**.
2. In **Collega un disco esistente** fare clic su **Posizione**.

   ![Collegare un disco esistente](./media/attach-disk/attachexistingdisksettings.png)
3. In **gli account di archiviazione**, selezionare account hello e contenitore che include i file con estensione vhd hello.

   ![Individuare il percorso di un VHD](./media/attach-disk/existdiskstorageaccountandcontainer.png)

4. Selezionare i file con estensione vhd hello.
5. In **collegare un disco esistente**, file hello appena selezionata è elencato in **File VHD**. Fare clic su **OK**.
6. Dopo il collega Azure hello macchina virtuale di toohello disco, viene elencata per le impostazioni del disco della macchina virtuale hello in **dischi dati**.

## <a name="use-trim-with-standard-storage"></a>Usare TRIM con l'archiviazione Standard

Se si usa l'archiviazione Standard (HDD), è consigliabile abilitare TRIM. TRIM rimuove i blocchi inutilizzati nel disco hello in modo verrà addebitato solo per l'archiviazione che stiano effettivamente usando. L'uso di TRIM consente di risparmiare sui costi, inclusi i blocchi inutilizzati risultanti dall'eliminazione di file di grandi dimensioni.

È possibile eseguire questo comando toocheck hello TRIM impostare. Aprire un prompt dei comandi nella macchina virtuale Windows e digitare:

```
fsutil behavior query DisableDeleteNotify
```

Se il comando hello restituisce 0, l'ottimizzazione TRIM è abilitato correttamente. Se viene restituito 1, eseguire hello tooenable comando TRIM seguenti:
```
fsutil behavior set DisableDeleteNotify 0
```

## <a name="next-steps"></a>Passaggi successivi
Se l'applicazione necessita di dati di toostore unità d: hello toouse, è possibile [modificare hello lettera di unità del disco temporaneo di Windows hello](../../virtual-machines-windows-change-drive-letter.md).

## <a name="additional-resources"></a>Risorse aggiuntive
[Informazioni sui dischi e sui dischi rigidi virtuali per le macchine virtuali](../../virtual-machines-linux-about-disks-vhds.md)
