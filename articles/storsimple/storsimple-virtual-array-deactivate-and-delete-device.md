---
title: aaaDeactivate ed eliminare un Array virtuale di Microsoft Azure StorSimple | Documenti Microsoft
description: Viene descritto come dispositivo di StorSimple tooremove dal servizio innanzitutto disattivarlo e quindi eliminarlo.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: a929f5bc-03e2-4b01-b925-973db236f19f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: alkohli
ms.openlocfilehash: b1f3ddb5822d19965739777e238af19b507df984
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-virtual-array"></a>Disattivare ed eliminare un array virtuale StorSimple

## <a name="overview"></a>Panoramica

Quando si disattiva un Array virtuale StorSimple, si interrompe la connessione hello tra hello dispositivo e il servizio StorSimple Manager periferica corrispondente hello. In questa esercitazione viene illustrato come:

* Disattivare un dispositivo 
* Eliminare un dispositivo disattivato

informazioni di Hello in questo articolo si applicano tooStorSimple array virtuale. Per informazioni sulla 8000 serie, passare toohow troppo[disattivare o eliminare un dispositivo](storsimple-deactivate-and-delete-device.md).

## <a name="when-toodeactivate"></a>Quando toodeactivate?

La disattivazione è un'operazione permanente e non può essere annullata. È possibile registrare un dispositivo disattivato con il servizio di gestione di dispositivi StorSimple hello nuovamente. Si potrebbe necessario toodeactivate ed eliminare un Array virtuale StorSimple in hello seguenti scenari:

* **Failover pianificato** : il dispositivo è online e si prevede di toofail failover del dispositivo. Se si intende tooupgrade tooa maggiore dispositivo, potrebbe essere toofail failover del dispositivo. Dopo che la proprietà dati hello viene trasferita e hello failover è stato completato, il dispositivo di origine hello viene eliminato automaticamente.
* **Failover non pianificato** : il dispositivo è offline ed è necessario toofail su dispositivo hello. Questo scenario può verificarsi durante un'emergenza quando si verifica un'interruzione nel Data Center hello e il dispositivo primario è inattivo. Si prevede di toofail su hello tooa secondario dispositivo. Dopo che la proprietà dati hello viene trasferita e hello failover è stato completato, il dispositivo di origine hello viene eliminato automaticamente.
* **Rimuovere le autorizzazioni** : si desidera toodecommission hello dispositivo. Questa operazione richiede il toofirst disattivare hello dispositivo e quindi eliminarlo. Quando si disattiva un dispositivo, tutti i dati archiviati localmente non saranno più accessibili. È possibile solo i dati di hello accesso e di ripristino archiviati nel cloud hello. Se si prevede di dati del dispositivo hello tookeep dopo la disattivazione, è necessario creare uno snapshot di cloud di tutti i dati prima di disattivare un dispositivo. Snapshot cloud consente toorecover tutti hello dati in una fase successiva.

## <a name="deactivate-a-device"></a>Disattivare un dispositivo

toodeactivate il dispositivo, eseguire hello alla procedura seguente.

#### <a name="toodeactivate-hello-device"></a>dispositivo hello toodeactivate

1. Nel servizio, andare troppo**gestione > dispositivi**. In hello **dispositivi** pannello, fare clic su e dispositivo di hello select che si desidera toodeactivate.
   
    ![Selezionare toodeactivate dispositivo](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete7.png)
2. Nel **dashboard del dispositivo** pannello, fare clic su **... Ulteriori** e selezionare nell'elenco hello **disattiva**.
   
    ![Clic su Disattiva](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete8.png)
3. In hello **disattiva** pannello, nome del tipo hello dispositivo e quindi fare clic su **disattiva**. 
   
    ![Conferma della disattivazione](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete1.png)
   
    Hello disattivare processo inizia e accetta toocomplete di pochi minuti.
   
    ![Disattivazione in corso](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete2.png)
4. Dopo la disattivazione, aggiorna l'elenco di hello dei dispositivi.
   
    ![Disattivazione completata](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete3.png)
   
    È ora possibile eliminare il dispositivo.

## <a name="delete-hello-device"></a>Eliminare dispositivo hello

Un dispositivo ha toodelete disattivate prima toobe è. L'eliminazione di un dispositivo per rimuoverlo dall'elenco di hello del servizio di dispositivi connessi toohello. servizio Hello quindi non può più gestire il dispositivo hello eliminato. dati Hello associati hello dispositivo rimangono tuttavia nel cloud hello. Su questi dati sono applicati degli addebiti.

dispositivo hello toodelete, eseguire hello alla procedura seguente.

#### <a name="toodelete-hello-device"></a>dispositivo hello toodelete

1. Il servizio StorSimple Device Manager andare troppo**gestione > dispositivi**. In hello **dispositivi** pannello selezionare un dispositivo disattivato che si desidera toodelete.
2. In hello **dashboard del dispositivo** pannello, fare clic su **... Ulteriori** e quindi fare clic su **eliminare**.
   
   ![Selezionare toodelete dispositivo](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete4.png)
3. In hello **eliminare** pannello, il nome del tipo hello di eliminazione di hello tooconfirm dispositivo e quindi fare clic su **eliminare**. L'eliminazione dispositivo hello non elimina i dati di cloud hello associati hello dispositivo. 
   
   ![Conferma dell'eliminazione](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete5.png) 
4. l'eliminazione di Hello viene avviato e richiede pochi minuti toocomplete.
   
   ![Eliminazione in corso](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete6.png)
   
    Dopo l'eliminazione hello dispositivo, è possibile visualizzare l'elenco di hello aggiornato di dispositivi.

## <a name="next-steps"></a>Passaggi successivi

* Per informazioni su come toofail, andare troppo[Failover e ripristino di emergenza di matrice virtuale StorSimple](storsimple-virtual-array-failover-dr.md).

* altre informazioni sulle toolearn come toouse hello servizio di gestione di dispositivi StorSimple, andare troppo[utilizzare hello tooadminister servizio di gestione di dispositivi StorSimple l'Array virtuale StorSimple](storsimple-virtual-array-manager-service-administration.md). 

