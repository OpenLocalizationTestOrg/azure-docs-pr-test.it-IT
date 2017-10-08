---
title: aaaAttach tooa un disco di dati non gestiti - macchina virtuale di Windows Azure | Documenti Microsoft
description: Tooattach nuovo o esistente dati non gestiti disco tooa macchina virtuale Windows in Azure mediante portale hello hello come modello di distribuzione di gestione risorse.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3790fc59-7264-41df-b7a3-8d1226799885
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: cynthn
ms.openlocfilehash: 923a6663974143bf359970f9b0eb0d36cabcba9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-an-unmanaged-data-disk-tooa-windows-vm-in-hello-azure-portal"></a>Funzionamento dei dischi tooa macchina virtuale di Windows nel portale di Azure hello tooattach un dati non gestiti

Questo articolo illustra come non gestito tooattach sia nuovi che esistenti dischi tooWindows le macchine virtuali tramite hello portale di Azure. È anche possibile [collegare un disco dati usando PowerShell](./attach-disk-ps.md). Prima di procedere, rivedere i suggerimenti seguenti:

* dimensioni di Hello della macchina virtuale hello controlla il numero di dischi dati è possibile collegare. Per informazioni dettagliate, vedere [Dimensioni delle macchine virtuali](sizes.md).
* toouse archiviazione Premium, è necessario una macchina virtuale serie DS o GS-series. È possibile utilizzare dischi dagli account di archiviazione sia Premium che Standard con queste macchine virtuali. L’archiviazione Premium è disponibile solo in determinate aree geografiche. Per ulteriori informazioni, vedere [Archiviazione Premium: archiviazione ad alte prestazioni per carichi di lavoro delle macchine virtuali di Azure](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Per un nuovo disco, non è necessario toocreate è primo poiché Azure crea momento del collegamento.


È anche possibile [collegare un disco dati usando Powershell](attach-disk-ps.md).


## <a name="find-hello-virtual-machine"></a>Trovare la macchina virtuale hello
1. Accedi toohello [portale di Azure](https://portal.azure.com/).
2. Dal menu hello hello sinistra, fare clic su **macchine virtuali**.
3. Selezionare macchina virtuale hello hello elenco.
4. Nel pannello macchine virtuali di hello, fare clic su **dischi**.
   
Continuare seguendo le istruzioni per il collegamento di un [nuovo disco](#option-1-attach-a-new-disk) o un [disco esistente](#option-2-attach-an-existing-disk).

## <a name="option-1-attach-and-initialize-a-new-disk"></a>Opzione 1: Connettere e inizializzare un nuovo disco
1. In hello **dischi** pannello, fare clic su **+ Aggiungi disco di dati**.
2. In hello **collega disco gestito** pannello, digitare un nome per il disco hello in **nome** e quindi selezionare **New (disco vuoto)** in **tipo di origine**.
3. In **contenitore di archiviazione**, fare clic su hello **Sfoglia** pulsante ed esplorare toohello account di archiviazione e contenitore in cui desideri hello nuovo disco rigido virtuale toobe archiviati e quindi fare clic su **selezionare**. 
  
   ![Esaminare le impostazioni del disco](./media/attach-disk-portal/attach-empty-unmanaged.png)
   
3. Una volta con impostazioni hello per disco dati hello, fare clic su **OK**.
4. In hello **dischi** pannello, fare clic su **salvare** configurazione della macchina virtuale toohello tooadd hello disco.


### <a name="initialize-a-new-data-disk"></a>Inizializzare un nuovo disco dati

1. Connessione macchina virtuale toohello. Per istruzioni, vedere [come tooconnect e tooan virtuali di Azure di accesso del computer che eseguono Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
1. Fare clic su hello **avviare** menu all'interno di hello VM e tipo **diskmgmt.msc** e fare clic su **invio**. Verrà avviato lo snap-in Gestione disco hello.
2. Gestione disco riconosce che si disponga di un disco non inizializzato e si aprirà la finestra Inizializza disco hello.
3. Assicurarsi che sia selezionato il nuovo disco di hello e fare clic su **OK** tooinitialize è.
4. Hello nuovo disco verrà visualizzato come **non allocato**. Fare clic sul disco hello e selezionare **nuovo volume semplice**. Hello **semplice creazione guidata nuovo Volume** viene avviato.
5. Seguire i passaggi guidata hello, mantenendo tutti i valori predefiniti di hello, al termine selezionare **fine**.
6. Chiudere Gestione disco.
7. È possibile utilizzare una finestra popup che è necessario nuovo disco di tooformat hello prima che sia possibile utilizzarlo. Fare clic su **Formatta disco**.
8. In hello **nuovo disco in formato** finestra di dialogo, controllare le impostazioni di hello e quindi fare clic su **avviare**.
9. Visualizzato un avviso che la formattazione di dischi hello Cancella tutti i dati di hello, fare clic su **OK**.
10. Una volta completato il formato di hello, fare clic su **OK**.


## <a name="option-2-attach-an-existing-disk"></a>Opzione 2: Collegare un disco esistente
1. In hello **dischi** pannello, fare clic su **+ Aggiungi disco di dati**.
2. In hello **collega disco non gestito** pannello, in **tipo di origine** selezionare **blob esistente**.

    ![Esaminare le impostazioni del disco](./media/attach-disk-portal/attach-existing-unmanaged.png)

    3. Fare clic su **Sfoglia** toonavigate toohello account di archiviazione e contenitore hello disco rigido virtuale esistente in cui si trova. Fare clic su hello disco rigido virtuale e quindi fare clic su **selezionare**.
4. Fare clic su **OK** in hello **collega disco non gestito** blade.
5. In hello **dischi** pannello, fare clic su **salvare** configurazione toohello del disco hello tooadd per hello macchina virtuale.
   


## <a name="use-trim-with-standard-storage"></a>Usare TRIM con l'archiviazione Standard

Se si usa l'archiviazione Standard (HDD), è consigliabile abilitare TRIM. TRIM rimuove i blocchi inutilizzati nel disco hello in modo verrà addebitato solo per l'archiviazione che stiano effettivamente usando. In questo modo è possibile risparmiare sui costi quando si creano file di grandi dimensioni per poi eliminarli. 

È possibile eseguire questo comando toocheck hello TRIM impostare. Aprire un prompt dei comandi nella macchina virtuale Windows e digitare:

```
fsutil behavior query DisableDeleteNotify
```

Se il comando hello restituisce 0, l'ottimizzazione TRIM è abilitato correttamente. Se viene restituito 1, eseguire hello tooenable comando TRIM seguenti:
```
fsutil behavior set DisableDeleteNotify 0
```

Dopo l'eliminazione di dati dal disco, è possibile garantire scaricamento correttamente eseguendo le operazioni TRIM hello deframmentazione con TRIM:

```
defrag.exe <volume:> -l
```

È inoltre possibile garantire l'intero volume hello viene ritagliato formattando volume hello.


## <a name="next-steps"></a>Passaggi successivi
Se l'applicazione necessita di dati di toostore unità d: hello toouse, è possibile [modificare hello lettera di unità del disco temporaneo di Windows hello](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

