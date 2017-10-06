---
title: aaaDeactivate ed eliminare un dispositivo StorSimple serie 8000 | Documenti Microsoft
description: Viene descritto come dispositivo di StorSimple tooremove dal servizio innanzitutto disattivarlo e quindi eliminarlo.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: alkohli
ms.openlocfilehash: 841ecd7f0fb5e425bf23e1fe0044faeab2af4b53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-device"></a>Disattivare ed eliminare un dispositivo StorSimple

## <a name="overview"></a>Panoramica

Questo articolo viene descritto come toodeactivate ed eliminare un dispositivo StorSimple tooa connesso il servizio di gestione di dispositivi StorSimple. linee guida di Hello in questo articolo si applicano solo i dispositivi serie 8000 tooStorSimple includono hello StorSimple Cloud su. Se si utilizza un Array virtuale StorSimple, quindi andare troppo[disattivare ed eliminare un Array virtuale StorSimple](storsimple-virtual-array-deactivate-and-delete-device.md).

I server di disattivazione, connessione hello tra hello dispositivo e il servizio StorSimple Manager periferica corrispondente hello. È possibile utilizzare un dispositivo StorSimple fuori servizio tootake (ad esempio, se si sta sostituendo o l'aggiornamento di un dispositivo o se si utilizza più StorSimple). In questo caso, è necessario che il dispositivo di hello toodeactivate prima di poter eliminare.

Quando si disattiva un dispositivo, tutti i dati archiviati localmente nel dispositivo hello sono più accessibili. È possibile ripristinare solo i dati di hello associati dispositivo hello che è stato archiviato nel cloud hello.

> [!WARNING]
> La disattivazione è un'operazione permanente e non può essere annullata. Un dispositivo disattivato non può essere registrato con hello del servizio di gestione di dispositivi StorSimple a meno che non è toofactory predefinite.
>
> Hello ripristino delle impostazioni predefinite processo Elimina tutti i dati di hello che è stati archiviati localmente nel dispositivo. Pertanto, è necessario eseguire uno snapshot nel cloud di tutti i dati prima di disattivare un dispositivo. Snapshot cloud consente toorecover tutti hello dati in una fase successiva.

Dopo aver letto questa esercitazione, si sarà in grado di:

* Disattivare un dispositivo ed eliminare dati hello.
* Disattivare un dispositivo e mantenere i dati di hello.

> [!NOTE]
> Prima di disattivare un dispositivo fisico o un'appliance cloud StorSimple, arrestare o eliminare i client e gli host che dipendono da tale dispositivo.


## <a name="deactivate-and-delete-data"></a>Disattivare ed eliminare i dati

Se si è interessati a eliminare completamente il dispositivo hello e non si desidera tooretain hello dati sul dispositivo hello, quindi completare hello alla procedura seguente.

#### <a name="toodeactivate-hello-device-and-delete-hello-data"></a>dati hello dispositivo e delete toodeactivate hello

1. Prima di disattivare un dispositivo, è necessario eliminare tutti hello volume contenitori (e i volumi di hello) associato al dispositivo hello. È possibile eliminare i contenitori dei volumi solo dopo aver eliminato i backup hello associata.

    > [!NOTE]
    > Prima di disattivare un dispositivo fisico StorSimple appliance di cloud, assicurarsi che i dati di hello dal contenitore del volume hello eliminato sono effettivamente eliminati dal dispositivo hello. È possibile monitorare i grafici relativi all'utilizzo di cloud hello e quando viene visualizzato l'utilizzo di cloud hello eliminare a causa di backup hello che è stato eliminato, è possibile procedere dispositivo hello toodeactivate. Se si disattiva dispositivo hello prima questo rilascio si verifica, hello dati sono bloccati nell'account di archiviazione hello e vengono attribuiti addebiti.

2. Disattivare il dispositivo hello come indicato di seguito:
   
   1. Il servizio di gestione di dispositivi StorSimple tooyour, fare clic su **dispositivi**. In hello **dispositivi** pannello, al dispositivo selezionare hello che si desidera toodeactivate, pulsante destro del mouse e quindi fare clic su **disattiva**.

        ![Disattivare il dispositivo StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate1.png)
   2. In hello **disattiva** pannello digitare tooconfirm nome di dispositivo hello e quindi fare clic su **disattiva**. Hello disattivare processo inizia e accetta toocomplete di pochi minuti.

        ![Disattivare il dispositivo StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate2.png)

3. Dopo la disattivazione, è possibile eliminare completamente il dispositivo hello. L'eliminazione di un dispositivo per rimuoverlo dall'elenco di hello del servizio di dispositivi connessi toohello. servizio Hello quindi non può più gestire il dispositivo hello eliminato. Utilizzare hello dispositivo hello toodelete di passaggi seguente:
   
   1. Il servizio di gestione di dispositivi StorSimple tooyour, fare clic su **dispositivi**. In hello **dispositivi** blade, il dispositivo di hello selezionare disattivato che si desidera toodelete pulsante destro del mouse e quindi fare clic su **eliminare**.

        ![Disattivare il dispositivo StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate5.png)
   2. In hello **eliminare** pannello digitare tooconfirm nome di dispositivo hello e quindi fare clic su **eliminare**. l'eliminazione di Hello accetta toocomplete di pochi minuti.

        ![Disattivare il dispositivo StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate6.png)
   3. Dopo l'eliminazione di hello è completata, ricevono la notifica. elenco dei dispositivi Hello aggiorna anche l'eliminazione di hello tooreflect.

## <a name="deactivate-and-retain-data"></a>Disattivare e conservare i dati

Se si desidera che i dati di hello tooretain sono interessati a eliminare il dispositivo di hello, quindi completare hello alla procedura seguente:

#### <a name="toodeactivate-a-device-and-retain-hello-data"></a>un dispositivo toodeactivate e mantenere i dati di hello
1. Disattivare il dispositivo di hello. Tutti i contenitori dei volumi di hello e rimangono snapshot hello del dispositivo hello.
   
   1. Il servizio di gestione di dispositivi StorSimple tooyour, fare clic su **dispositivi**. In hello **dispositivi** pannello, al dispositivo selezionare hello che si desidera toodeactivate, pulsante destro del mouse e quindi fare clic su **disattiva**.

         ![Disattivare il dispositivo StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate1.png)
   2. In hello **disattiva** pannello digitare tooconfirm nome di dispositivo hello e quindi fare clic su **disattiva**. Hello disattivare processo inizia e accetta toocomplete di pochi minuti.

         ![Disattivare il dispositivo StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate2.png)
2. È ora possibile eseguire il failover hello contenitori dei volumi e gli snapshot hello associata. Per le procedure, andare troppo[Failover e ripristino di emergenza per il dispositivo StorSimple](storsimple-8000-device-failover-disaster-recovery.md).
3. Dopo la disattivazione e il failover, è possibile eliminare completamente il dispositivo di hello. L'eliminazione di un dispositivo per rimuoverlo dall'elenco di hello del servizio di dispositivi connessi toohello. servizio Hello quindi non può più gestire il dispositivo hello eliminato. dispositivo di hello toodelete, hello completo alla procedura seguente:
   
   1. Il servizio di gestione di dispositivi StorSimple tooyour, fare clic su **dispositivi**. In hello **dispositivi** blade, il dispositivo di hello selezionare disattivato che si desidera toodelete pulsante destro del mouse e quindi fare clic su **eliminare**.

       ![Disattivare il dispositivo StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate5.png)
   2. In hello **eliminare** pannello digitare tooconfirm nome di dispositivo hello e quindi fare clic su **eliminare**. l'eliminazione di Hello accetta toocomplete di pochi minuti.

       ![Disattivare il dispositivo StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate6.png)
   3. Dopo l'eliminazione di hello è completata, ricevono la notifica. elenco dei dispositivi Hello aggiorna anche l'eliminazione di hello tooreflect.

     
## <a name="deactivate-and-delete-a-cloud-appliance"></a>Disattivare ed eliminare un'appliance cloud

Per un'applicazione Cloud StorSimple, disattivazione dal portale hello dealloca ed elimina la macchina virtuale di hello e le risorse di hello create quando è stato eseguito il provisioning. Dopo la disattivazione di appliance di cloud hello, non può essere ripristinato lo stato precedente tooits.

![Disattivare un'appliance cloud StorSimple](./media/storsimple-8000-deactivate-and-delete-device/deactivate7.png)

La disattivazione comporta hello seguenti azioni:

* Hello StorSimple Appliance di Cloud viene rimosso dal servizio di hello.
* macchina virtuale Hello per hello StorSimple Appliance di Cloud viene eliminato.
* disco del sistema operativo Hello e i dischi dati creati per hello StorSimple Appliance di Cloud vengono rimossi.
* il servizio ospitato Hello e rete virtuale creati durante il provisioning vengono mantenuti. Se non si utilizzano, è necessario eliminarli manualmente.
* Gli snapshot cloud creati hello StorSimple Appliance di Cloud vengono mantenuti.

Dopo la disattivazione di appliance di hello cloud, è possibile eliminarlo dall'elenco di hello dei dispositivi. Seleziona hello disattivato dispositivo, il pulsante destro del mouse, quindi scegliere **eliminare**. StorSimple invia notifiche dopo dispositivo hello viene eliminato e hello elenco degli aggiornamenti di dispositivi.

## <a name="next-steps"></a>Passaggi successivi

* toorestore hello dispositivo disattivato toofactory predefiniti, andare troppo[ripristinare le impostazioni predefinite di hello dispositivo toofactory](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).
* Per assistenza tecnica, [contattare il supporto Microsoft](storsimple-8000-contact-microsoft-support.md).
* altre informazioni sulle toolearn come toouse hello servizio di gestione di dispositivi StorSimple, andare troppo[utilizzare hello tooadminister servizio di gestione di dispositivi StorSimple dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

