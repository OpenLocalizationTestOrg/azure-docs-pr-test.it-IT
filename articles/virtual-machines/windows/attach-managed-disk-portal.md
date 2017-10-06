---
title: aaaAttach tooa un disco di dati gestiti - macchina virtuale di Windows Azure | Documenti Microsoft
description: Il modo tooattach nuovo gestiti tooa disco dati macchina virtuale Windows in Azure mediante portale hello hello il modello di distribuzione di gestione risorse.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: cynthn
ms.openlocfilehash: bacc0589ad2d93e4d3d055c8f837f8db27291ead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-managed-data-disk-tooa-windows-vm-in-hello-azure-portal"></a>Funzionamento dei dischi tooa macchina virtuale di Windows nel portale di Azure hello tooattach dati gestiti

Questo articolo illustra come i dati gestiti tooattach disco tooWindows le macchine virtuali tramite hello portale di Azure. Prima di procedere, rivedere i suggerimenti seguenti:

* dimensioni di Hello della macchina virtuale hello controlla il numero di dischi dati è possibile collegare. Per informazioni dettagliate, vedere [Dimensioni delle macchine virtuali](sizes.md).
* Per un nuovo disco, non è necessario toocreate è primo poiché Azure crea momento del collegamento.

È anche possibile [collegare un disco dati usando Powershell](attach-disk-ps.md).



## <a name="add-a-data-disk"></a>Aggiungere un disco dati
1. Dal menu hello hello sinistra, fare clic su **macchine virtuali**.
2. Selezionare macchina virtuale hello hello elenco.
3. Nel Pannello di hello macchina virtuale, fare clic su **dischi**.
   4. In hello **dischi** pannello, fare clic su **+ Aggiungi disco di dati**.
5. Nell'elenco a discesa nuovo disco hello hello, selezionare **creare vuoto**.
6. In hello **disco gestito crea** pannello, digitare un nome per il disco hello e regolare hello altre impostazioni in base alle esigenze. Al termine dell'operazione fare clic su **Crea**.
7. In hello **dischi** pannello, fare clic su Salva toosave hello nuova configurazione del disco per hello macchina virtuale.
6. Dopo che Azure crea un disco hello e lo collega macchina virtuale toohello, nuovo disco hello è elencato nelle impostazioni del disco della macchina virtuale hello in **dischi dati**.


## <a name="initialize-a-new-data-disk"></a>Inizializzare un nuovo disco dati

1. Connettersi toohello macchina virtuale.
1. Fare clic su menu start hello all'interno di hello VM e tipo **diskmgmt.msc** e fare clic su **invio**. Verrà avviata hello snap-in Gestione disco.
2. Gestione disco riconoscerà che si disponga di un disco non inizializzato e si aprirà la finestra Inizializza disco hello.
3. Assicurarsi che sia selezionato il nuovo disco di hello e fare clic su **OK** tooinitialize è.
4. verrà visualizzato come nuovo disco Hello **non allocato**. Fare clic sul disco hello e selezionare **nuovo volume semplice**. Hello **semplice creazione guidata nuovo Volume** verrà avviato.
5. Seguire i passaggi guidata hello, mantenendo tutti i valori predefiniti di hello, al termine selezionare **fine**.
6. Chiudere Gestione disco.
7. Verrà visualizzato un messaggio popup che è necessario nuovo disco di tooformat hello prima che sia possibile utilizzarlo. Fare clic su **Formatta disco**.
8. In hello **nuovo disco in formato** finestra di dialogo, controllare le impostazioni di hello e quindi fare clic su **avviare**.
9. Verrà visualizzato un avviso che la formattazione dischi hello cancellerà tutti i dati di hello, fare clic su **OK**.
10. Una volta completato il formato di hello, fare clic su **OK**.

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
