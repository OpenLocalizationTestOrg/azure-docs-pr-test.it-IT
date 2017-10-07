---
title: dashboard del dispositivo StorSimple Manager hello aaaUse | Documenti Microsoft
description: "Descrive i dashboard del dispositivo del servizio StorSimple Manager hello e come toouse è tooview metriche di archiviazione e gli iniziatori connessi e trova hello numero di serie e IQN."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 6c213969-a385-461f-b698-78ef5b8a79cc
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e213fc0a081c21b9d6b408a3dd845cc93a31e250
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-device-dashboard-in-storsimple-manager-service"></a>Utilizzare i dashboard del dispositivo hello nel servizio StorSimple Manager  

## <a name="overview"></a>Panoramica
dashboard del dispositivo StorSimple Manager Hello viene fornita una panoramica delle informazioni per un dispositivo StorSimple specifico, al contrario toohello servizio dashboard che fornisce informazioni su tutti i dispositivi di hello inclusi nella soluzione StorSimple di Microsoft Azure.

![Pagina dashboard del dispositivo](./media/storsimple-device-dashboard/StorSimple_DeviceDashbaord1M.png)

dashboard Hello contiene hello le seguenti informazioni:

* **Area grafico** : È possibile visualizzare metriche di archiviazione pertinenti hello nell'area del grafico nella parte superiore di hello del dashboard hello hello. In questo grafico, è possibile visualizzare le metriche di archiviazione primaria totale hello (quantità hello dei dati scritti dal dispositivo tooyour host) e hello totale usata dal dispositivo in un periodo di tempo di archiviazione cloud.
  
     In questo contesto, *archiviazione primaria* fa riferimento toohello quantità totale di dati scritti dall'host hello e possono essere suddivisi per tipo di volume: *primario a livelli di archiviazione* include sia archiviati localmente i dati e i dati cloud toohello a più livelli. *primario aggiunto in locale archiviazione* include solo i dati archiviati in locale. *Archiviazione cloud*, in hello invece, è una misura della quantità totale di hello dei dati archiviati nel cloud hello. Sono inclusi i backup e i dati a più livelli. Si noti che i dati archiviati nel cloud hello sono deduplicati e compresso, mentre l'archiviazione primaria indica la quantità hello spazio di archiviazione utilizzato prima che i dati di hello sono deduplicato e compresso. (È possibile confrontare questi tooget due numeri un'idea del tasso di compressione hello). Per entrambi primario e del cloud di archiviazione, hello quantità visualizzate saranno basate su hello rilevamento frequenza configurata. Ad esempio, se si sceglie una frequenza di una settimana, quindi hello grafico mostrerà dati per ogni giorno hello settimana precedente.
  
     È possibile configurare il grafico hello come indicato di seguito:
  
  * quantità di hello toosee di archiviazione cloud usato nel corso del tempo, seleziona hello **archiviazione CLOUD usata** opzione. toosee hello spazio di archiviazione totale scritta dall'host di hello, seleziona hello **primario utilizzato archiviazione a livelli** e **primario locale aggiunto spazio di archiviazione usato** opzioni. Nella figura hello, sono selezionate entrambe le opzioni. Pertanto, il grafico di hello Mostra quantità di archiviazione per i cloud e l'archiviazione primaria. Si noti che qualsiasi archiviazione primario utilizzato precedente tooinstalling Update 2 sono rappresentato da hello **primario utilizzato archiviazione a livelli** riga.
  * Utilizzare il menu di scelta rapida hello nell'angolo superiore destro di hello di hello grafico toospecify in un periodo di tempo 1 settimana, 1 mese, 3 mesi o 1 anno. Si noti che hello di livello superiore del grafico viene aggiornato solo una volta al giorno e pertanto rifletterà hello totali del giorno precedente.
    
    Per ulteriori informazioni, vedere [utilizzare hello toomonitor servizio StorSimple Manager dispositivo StorSimple](storsimple-monitor-device.md).
* **Panoramica sull'utilizzo** : In hello **panoramica sull'utilizzo** area, è possibile visualizzare hello di archiviazione primario utilizzato, hello quantità di archiviazione sottoposto a provisioning e la capacità di archiviazione massima hello per il dispositivo. Confrontando queste quantità massima di toohello numeri dell'utilizzo di archiviazione disponibile, è possibile visualizzare a colpo d'occhio, se è necessario ulteriore spazio di archiviazione tooobtain. Si noti che questa panoramica viene aggiornata ogni 15 minuti, a causa di differenza hello nella frequenza di aggiornamento, potrebbe visualizzare numeri diversi rispetto a quelli mostrati in hello area grafico precedente, che viene aggiornato ogni giorno. Per ulteriori informazioni, vedere [utilizzare hello toomonitor servizio StorSimple Manager dispositivo StorSimple](storsimple-monitor-device.md).
* **Avvisi** : hello **avvisi** area contiene una panoramica degli avvisi di hello per il dispositivo. Avvisi sono raggruppati in base alla gravità e viene fornito un conteggio del numero di hello degli avvisi a ogni livello di gravità. Fare clic su avviso hello gravità, viene visualizzata con ambito di hello avvisi scheda tooshow che Hello solo gli avvisi di tale livello di gravità per questo dispositivo.
* **I processi** : hello **processi** Mostra area hello risultato dell'attività dei processi recenti. È possibile verificare che hello sistema funzioni come previsto o è possibile consentono di sapere che è necessario l'intervento tootake. Fare clic su ulteriori informazioni sui processi completati di recente, toosee **processi completati nelle hello ultime 24 ore**.
* Hello **riepilogo rapido** area hello destra del dashboard hello fornisce informazioni utili, ad esempio un modello di dispositivo, numero di serie, stato, descrizione e numero di volumi.

È anche possibile configurare il failover e visualizzare gli iniziatori connessi nel dashboard del dispositivo hello.

attività comuni di Hello che possono essere eseguite in questa pagina sono:

* Visualizzare gli iniziatori connessi
* Trovare il numero di serie hello
* Trovare hello. nome qualificato iSCSI di destinazione del dispositivo

## <a name="view-connected-initiators"></a>Visualizzare gli iniziatori connessi
È possibile visualizzare hello gli iniziatori iSCSI connessi tooyour dispositivo facendo clic su hello **Visualizza iniziatori connessi** collegamento fornito nel hello **riepilogo rapido** area del dashboard del dispositivo. Questa pagina fornisce un elenco tabulare degli iniziatori hello tooyour dispositivo connesso correttamente. Per ogni iniziatore, è possibile vedere:

* Hello iSCSI nome qualificato di hello connesso iniziatore.
* nome Hello hello controllo del record di accesso (ACR) che consente dell'iniziatore connesso.
* indirizzo IP Hello di hello connesso iniziatore.
* Hello interfacce di rete che iniziatore hello è tooon connesso il dispositivo di archiviazione. Queste possono variare da DATA 0 tooDATA 5.
* Tutti i volumi hello hello iniziatore connesso è consentita in base di configurazione del record corrente toohello tooaccess.

Se si visualizzati iniziatori imprevisti nell'elenco o non vi sono quelli previsti, hello, rivedere la configurazione di record. Dispositivo tooyour possibile connettere un massimo di 512 iniziatori.

## <a name="find-hello-device-serial-number"></a>Trovare il numero di serie hello
Numero di serie hello potrebbe essere necessario quando si configura Microsoft Multipath i/o (MPIO) sul dispositivo hello. Eseguire hello seguendo i passaggi toofind hello numero di serie.

#### <a name="toofind-hello-device-serial-number"></a>numero di serie hello toofind
1. Passare troppo**dispositivi** > **Dashboard**.
2. Nel riquadro di destra hello del dashboard hello, individuare hello **riepilogo rapido** area.
3. Scorrere verso il basso e individuare il numero di serie hello.

## <a name="find-hello-device-target-iqn"></a>Trovare hello. nome qualificato iSCSI di destinazione del dispositivo
Nome qualificato iSCSI di destinazione del dispositivo hello potrebbe essere necessario quando si configura hello Challenge Handshake Authentication Protocol (CHAP) sul dispositivo StorSimple. Eseguire i seguenti passaggi toofind hello dispositivo destinazione IQN hello.

### <a name="toofind-hello-device-target-iqn"></a>nome qualificato iSCSI di destinazione del dispositivo hello toofind
1. Passare troppo**dispositivi** > **Dashboard**.
2. Nel riquadro di destra hello del dashboard hello, individuare hello **riepilogo rapido** area.
3. Scorrere verso il basso e individuare la destinazione hello IQN.

## <a name="next-steps"></a>Passaggi successivi
* Altre informazioni su hello [dashboard del servizio StorSimple Manager](storsimple-service-dashboard.md).
* Altre informazioni, vedere [utilizzando hello tooadminister servizio StorSimple Manager dispositivo StorSimple](storsimple-manager-service-administration.md).

