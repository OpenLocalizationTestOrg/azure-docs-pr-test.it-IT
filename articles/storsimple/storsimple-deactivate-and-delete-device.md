---
title: aaaDeactivate ed eliminare un dispositivo StorSimple | Documenti Microsoft
description: Viene descritto come dispositivo di StorSimple tooremove dal servizio innanzitutto disattivarlo e quindi eliminarlo.
services: storsimple
documentationcenter: 
author: SharS
manager: timlt
editor: 
ms.assetid: 155cda38-c5ae-45dc-b7e8-6444494afc9e
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: anbacker
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ed86bcd089aa957128e14b1709c836d938c131a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-8000-series-device-via-storsimple-manager-service"></a>Disattivare ed eliminare un dispositivo StorSimple serie 8000 tramite il servizio StorSimple Manager
## <a name="overview"></a>Panoramica
È possibile utilizzare un dispositivo StorSimple fuori servizio tootake (ad esempio, se si sta sostituendo o l'aggiornamento di un dispositivo o se si utilizza più StorSimple). In caso di hello, occorrerà dispositivo hello toodeactivate prima di poter eliminare. I server di disattivazione, connessione hello tra hello dispositivo e il servizio StorSimple Manager corrispondente hello. In questa esercitazione viene illustrato come tooremove un dispositivo StorSimple dal servizio innanzitutto disattivarlo e quindi eliminarlo. 

Quando si disattiva un dispositivo, tutti i dati archiviati localmente nel dispositivo hello non saranno accessibili. È possibile ripristinare solo i dati di hello associati dispositivo hello che è stato archiviato nel cloud hello.  

> [!WARNING]
> La disattivazione è un'operazione permanente e non può essere annullata. Un dispositivo disattivato non può essere registrato con il servizio StorSimple Manager hello a meno che non è reimpostare innanzitutto toohello impostazioni predefinite. 
> 
> Hello ripristino delle impostazioni predefinite processo Elimina tutti i dati di hello che è stati archiviati localmente nel dispositivo. Pertanto, è essenziale eseguire uno snapshot nel cloud di tutti i dati prima di disattivare un dispositivo. In questo modo si toorecover tutti hello dati in una fase successiva.
> 
> 

In questa esercitazione viene illustrato come:

* Disattivare un dispositivo ed eliminare dati hello
* Disattivare un dispositivo e mantenere i dati di hello

Spiega anche come funzionano la disattivazione e l'eliminazione su un dispositivo virtuale StorSimple.

> [!NOTE]
> Prima di disattivare un dispositivo di StorSimple fisico o virtuale, assicurarsi che toostop o eliminare i client e gli host che dipendono da tale dispositivo.
> 
> 

## <a name="deactivate-and-delete-data"></a>Disattivare ed eliminare i dati
Se si è interessati a eliminare completamente il dispositivo hello e non si desidera tooretain hello dati sul dispositivo hello, quindi completare hello alla procedura seguente.

#### <a name="toodeactivate-hello-device-and-delete-hello-data"></a>dati hello dispositivo e delete toodeactivate hello
1. Toodeactivating precedente, un dispositivo, è necessario eliminare tutti hello volume contenitori (e volumi hello) associato al dispositivo hello. È possibile eliminare i contenitori dei volumi solo dopo aver eliminato i backup hello associata.
2. Disattivare il dispositivo hello come indicato di seguito:
   
   1. Nel servizio StorSimple Manager hello **dispositivi** pagina, al dispositivo selezionare hello che si desidera toodeactivate e, nella parte inferiore di hello della pagina hello, fare clic su **disattiva**.
   2. Verrà visualizzato un messaggio di conferma. Fare clic su **Sì** toocontinue. Hello disattivare processo verrà avviato e toocomplete di pochi minuti.
3. Dopo la disattivazione, è possibile eliminare completamente il dispositivo hello. L'eliminazione di un dispositivo per rimuoverlo dall'elenco di hello del servizio di dispositivi connessi toohello. servizio Hello quindi non può più gestire il dispositivo hello eliminato. Utilizzare hello dispositivo hello toodelete di passaggi seguente:
   
   1. Nel servizio StorSimple Manager hello **dispositivi** pagina, selezionare un dispositivo disattivato che si desidera toodelete.
   2. Nella parte inferiore di hello nella pagina di hello, fare clic su **eliminare**.
   3. Verrà richiesto di confermare. Fare clic su **Sì** toocontinue.
      
      Potrebbe richiedere alcuni minuti per toobe dispositivo hello eliminato.

## <a name="deactivate-and-retain-data"></a>Disattivare e conservare i dati
Se si desidera che i dati di hello tooretain sono interessati a eliminare il dispositivo di hello, quindi completare hello alla procedura seguente.

#### <a name="toodeactivate-a-device-and-retain-hello-data"></a>un dispositivo toodeactivate e mantenere i dati di hello
1. Disattivare il dispositivo di hello. Tutti i contenitori dei volumi di hello e rimarrà snapshot hello del dispositivo hello.
   
   1. Nel servizio StorSimple Manager hello **dispositivi** pagina, al dispositivo selezionare hello che si desidera toodeactivate e, nella parte inferiore di hello della pagina hello, fare clic su **disattiva**.
   2. Verrà visualizzato un messaggio di conferma. Fare clic su **Sì** toocontinue. Hello disattivare processo verrà avviato e toocomplete di pochi minuti.
2. È ora possibile eseguire il failover hello contenitori dei volumi e gli snapshot hello associata. Per le procedure, andare troppo[Failover e ripristino di emergenza per il dispositivo StorSimple](storsimple-device-failover-disaster-recovery.md).
3. Dopo la disattivazione e il failover, è possibile eliminare completamente il dispositivo di hello. L'eliminazione di un dispositivo per rimuoverlo dall'elenco di hello del servizio di dispositivi connessi toohello. servizio Hello quindi non può più gestire il dispositivo hello eliminato. Completare hello dispositivo hello toodelete di passaggi seguente:
   
   1. Nel servizio StorSimple Manager hello **dispositivi** pagina, selezionare un dispositivo disattivato che si desidera toodelete.
   2. Nella parte inferiore di hello nella pagina di hello, fare clic su **eliminare**.
   3. Verrà richiesto di confermare. Fare clic su **Sì** toocontinue.
      
      Potrebbe richiedere alcuni minuti per toobe dispositivo hello eliminato.

## <a name="deactivate-and-delete-a-virtual-device"></a>Disattivare ed eliminare un dispositivo virtuale
Per un dispositivo virtuale StorSimple, disattivazione dealloca la macchina virtuale hello. È quindi possibile eliminare macchine virtuali hello e le risorse di hello create quando è stato eseguito il provisioning. Dispositivo virtuale hello è disattivata, non può essere ripristinato lo stato precedente tooits. 

La disattivazione comporta hello seguenti azioni:

* dispositivo virtuale StorSimple Hello viene rimosso.
* Hello OSDisk e i dischi dati creati per il dispositivo virtuale StorSimple di hello vengono rimossi.
* Hello servizio ospitato e la rete virtuale creati durante il provisioning vengono mantenuti. Se non si utilizzano, è necessario eliminarli manualmente.
* Gli snapshot cloud creati dal dispositivo virtuale StorSimple hello vengono mantenuti.

## <a name="next-steps"></a>Passaggi successivi
* toorestore hello dispositivo disattivato toofactory predefiniti, andare troppo[ripristinare le impostazioni predefinite di hello dispositivo toofactory](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).
* Per assistenza tecnica, [contattare il supporto Microsoft](storsimple-contact-microsoft-support.md).
* altre informazioni sulle toolearn come toouse hello servizio StorSimple Manager, andare troppo[utilizzare hello tooadminister servizio StorSimple Manager dispositivo StorSimple](storsimple-manager-service-administration.md). 

