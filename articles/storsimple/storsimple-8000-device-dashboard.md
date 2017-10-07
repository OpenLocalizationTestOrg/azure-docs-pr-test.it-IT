---
title: dispositivo serie StorSimple 8000 aaaUse riepilogo | Documenti Microsoft
description: "Descrive dispositivo del servizio di gestione di dispositivi StorSimple hello riepilogo e in che modo toouse è tooview metriche di archiviazione e gli iniziatori connessi e trova hello numero di serie e IQN."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: b45ffc6ec52ebb6549c25a00c68c62460b208b7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-device-summary-in-storsimple-device-manager-service"></a>Usare dispositivo hello riepilogo nel servizio di gestione di dispositivi StorSimple

## <a name="overview"></a>Panoramica
Pannello riepilogo dispositivo StorSimple di Hello viene fornita una panoramica delle informazioni per un dispositivo StorSimple specifico, al contrario toohello servizio Pannello di riepilogo, che fornisce informazioni su tutti i dispositivi di hello inclusi nella soluzione StorSimple di Microsoft Azure.

Pannello riepilogo di Hello dispositivo fornisce un riepilogo di un dispositivo StorSimple serie 8000 registrato con un determinato StorSimple Manager di dispositivi, evidenziando i problemi dei dispositivi che richiedono attenzione da parte dell'amministratore di sistema. In questa esercitazione presenta Pannello di riepilogo dispositivo hello, spiega (funzione) e il contenuto di hello e vengono descritte le attività di hello che è possibile eseguire questo pannello.

Pannello riepilogo di Hello dispositivo Visualizza hello le seguenti informazioni:

![Pannello di riepilogo del dispositivo](./media/storsimple-8000-device-dashboard/device-summary1.png)

## <a name="management-command-bar"></a>Barra dei comandi di gestione

Nel pannello dispositivo di StorSimple hello, vedrai opzioni hello per la gestione del dispositivo StorSimple. Verranno visualizzati i comandi di gestione hello in alto di hello del pannello hello e sul lato sinistro di hello. Usare queste opzioni tooadd condivisioni o volumi, aggiornare o eseguire il failover del dispositivo.

![Barra dei comandi di gestione](./media/storsimple-8000-device-dashboard/device-summary2.png)

## <a name="essentials"></a>Informazioni di base

area essentials Hello acquisisce alcune delle proprietà importanti di hello, ad esempio, stato hello, modello, nome qualificato iSCSI di destinazione e versione del software hello. 

![Informazioni di base sui dispositivi](./media/storsimple-8000-device-dashboard/device-summary3.png)

## <a name="monitoring"></a>Monitoraggio

* Hello **avvisi** riquadro fornisce uno snapshot di tutti gli avvisi attivi hello per il dispositivo, raggruppato in base alla gravità dell'avviso.

    ![Riquadro avvisi](./media/storsimple-8000-device-dashboard/device-summary4.png)

    Fare clic su hello di hello riquadro tooopen **avvisi** blade e quindi fare clic su un singolo avviso tooview ulteriori dettagli sull'avviso, inclusi eventuali azioni consigliate. È inoltre possibile cancellare avviso hello se hello problema è stato risolto.

    ![Fare clic sul riquadro degli avvisi](./media/storsimple-8000-device-dashboard/device-summary10.png)

* Hello **stato e l'integrità** riquadro offre informazioni approfondite integrità hello del componente hardware per un dispositivo, inclusi lo stato del dispositivo hello. stato del dispositivo Hello può essere disattivato, pronto, online o offline tooset up.

    ![Riquadro Stato e integrità](./media/storsimple-8000-device-dashboard/device-summary5.png)

* Hello **volumi** riquadro fornisce un riepilogo del numero di hello di volumi nel dispositivo raggruppati per stato.

    ![Riquadro Volumi](./media/storsimple-8000-device-dashboard/device-summary6.png)

    Fare clic su hello di hello riquadro tooopen **volumi** elenco pannello, quindi fare clic su un singolo volume di tooview o modificarne le proprietà.
    
    ![Fare clic sul riquadro Volumi](./media/storsimple-8000-device-dashboard/device-summary9.png)
    
    Per ulteriori informazioni, vedere come troppo[gestire volumi](storsimple-8000-manage-volumes-u2.md).

* In hello **utilizzo** grafico, è possibile visualizzare l'archiviazione primaria di hello usata tra il dispositivo e archiviazione cloud hello consumata in hello ultimi 7 giorni, il periodo di tempo predefinito di hello.

     ![Riquadro Utilizzo](./media/storsimple-8000-device-dashboard/device-summary7.png)
    
     toochoose una scala temporale diverso, utilizzare hello **modifica** opzione nell'angolo superiore destro di hello del grafico hello.

     ![Modificare il grafico sull'utilizzo](./media/storsimple-8000-device-dashboard/device-summary12.png)

     In questo grafico, è possibile visualizzare le metriche di archiviazione primaria totale hello (quantità hello dei dati scritti dal dispositivo tooyour host) e hello totale usata dal dispositivo in un periodo di tempo di archiviazione cloud.
  
     In questo contesto, *archiviazione primaria* fa riferimento toohello quantità totale di dati scritti dall'host hello e possono essere suddivisi per tipo di volume: *primario a livelli di archiviazione* include sia archiviati localmente i dati e i dati cloud toohello a più livelli. mentre *archiviazione primaria aggiunta in locale* include solo i dati archiviati in locale. *Archiviazione cloud*, in hello invece, è una misura della quantità totale di hello dei dati archiviati nel cloud hello. Questo tipo di archiviazione include i backup e i dati a più livelli. dati Hello archiviati nel cloud hello sono deduplicati e compresso, mentre l'archiviazione primaria indica la quantità hello spazio di archiviazione utilizzato prima che i dati di hello sono deduplicati e compressi. (È possibile confrontare questi tooget due numeri un'idea del tasso di compressione hello). Per entrambi primario e l'archiviazione, hello importi basati su rilevamento frequenza configurata hello cloud. Ad esempio, se si sceglie una frequenza di una settimana, il grafico hello Mostra i dati per ogni giorno hello settimana precedente.

     quantità di hello toosee di archiviazione cloud usato nel corso del tempo, seleziona hello **archiviazione CLOUD usata** opzione. toosee hello spazio di archiviazione totale scritta dall'host di hello, seleziona hello **primario utilizzato archiviazione a livelli** e **primario locale aggiunto spazio di archiviazione usato** opzioni. 
     Per ulteriori informazioni, vedere [utilizzare hello toomonitor servizio di gestione di dispositivi StorSimple dispositivo StorSimple](storsimple-monitor-device.md).


* Hello **capacità** riquadro Visualizza hello primario spazio di archiviazione viene eseguito il provisioning e rimanente in hello dispositivo toohello relativo spazio di archiviazione totale disponibile per hello stesso. **Il provisioning** fa riferimento toohello quantità di spazio di archiviazione preparata e allocata per l'utilizzo, **rimanente** fa riferimento toohello residua che è possibile effettuare il provisioning in questo dispositivo. 

    ![Riquadro Utilizzo](./media/storsimple-8000-device-dashboard/device-summary8.png)

    Fare clic su questo tooview riquadro come viene eseguito il provisioning della capacità di hello tra i volumi aggiunti in locale e a più livelli. Hello **a livelli rimanenti** capacità sia hello disponibile una capacità che è possibile effettuare il provisioning inclusi cloud, mentre hello **rimanenti locale** capacità hello rimanente su dischi hello collegato toothis dispositivo.

    ![Fare clic sul grafico Utilizzo](./media/storsimple-8000-device-dashboard/device-summary13.png)


## <a name="next-steps"></a>Passaggi successivi
* Altre informazioni su hello [Pannello di riepilogo del servizio StorSimple](storsimple-8000-service-dashboard.md).
* Altre informazioni, vedere [utilizzando hello tooadminister servizio di gestione di dispositivi StorSimple dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

