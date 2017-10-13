---
title: Usare il dashboard del dispositivo StorSimple Manager | Microsoft Docs
description: "Descrive il dashboard del dispositivo del servizio StorSimple Manager e come utilizzarlo per visualizzare le metriche di archiviazione, gli iniziatori connessi e individuare il numero di serie del dispositivo e l’IQN."
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
ms.openlocfilehash: 0d8035b9608ca3bac3d4822c7c755b81c96d481e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-device-dashboard-in-storsimple-manager-service"></a>Usare il dashboard del dispositivo nel servizio StorSimple Manager  

## <a name="overview"></a>Panoramica
Il dashboard del dispositivo StorSimple Manager offre una panoramica delle informazioni per un determinato dispositivo StorSimple, a differenza del dashboard del servizio che fornisce informazioni su tutti i dispositivi inclusi nella soluzione Microsoft Azure StorSimple.

![Pagina dashboard del dispositivo](./media/storsimple-device-dashboard/StorSimple_DeviceDashbaord1M.png)

La scheda dashboard contiene le informazioni seguenti:

* **Area del grafico** – è possibile visualizzare le metriche di archiviazione rilevanti nell'area del grafico nella parte superiore del dashboard. In questo grafico, è possibile visualizzare le metriche per l'archiviazione primaria totale (la quantità di dati scritti dall'host per il dispositivo) e l'archiviazione cloud totale utilizzata dal dispositivo in un periodo di tempo.
  
     In questo contesto *archiviazione primaria* si riferisce alla quantità totale di dati scritti dall'host e può essere suddivisa in base al tipo di volume: *archiviazione primaria a livelli* include sia i dati archiviati in locale che quelli archiviati a livelli nel cloud, mentre *archiviazione primaria aggiunta in locale* include solo i dati archiviati in locale. L’*Archiviazione cloud*d'altra parte, è una misura della quantità totale di dati archiviati nel cloud. Sono inclusi i backup e i dati a più livelli. Si noti che i dati archiviati nel cloud sono deduplicati e compressi, mentre l'archiviazione primaria indica la quantità di spazio di archiviazione utilizzato prima della loro deduplicazione e compressione. (È possibile confrontare i due numeri per avere un'idea del tasso di compressione). Per entrambe le archiviazioni primarie e cloud, gli importi mostrati si baseranno sulla frequenza di rilevamento che si configura. Ad esempio, se si sceglie una frequenza di una settimana, il grafico mostrerà dati per ogni giorno della settimana precedente.
  
     È possibile configurare il grafico come segue:
  
  * Per visualizzare la quantità di archiviazione cloud usata nel corso del tempo, selezionare l'opzione **SPAZIO DI ARCHIVIAZIONE CLOUD UTILIZZATO**. Per visualizzare l'archiviazione totale scritta dall'host, selezionare le opzioni **PRIMARY TIERED STORAGE USED** (ARCHIVIAZIONE PRIMARIA A LIVELLI USATA) e **PRIMARY LOCALLY PINNED STORAGE USED** (ARCHIVIAZIONE PRIMARIA AGGIUNTA IN LOCALE USATA). Nella figura, entrambe le opzioni sono selezionate. Pertanto, il grafico mostra la quantità di archiviazione per l’archiviazione cloud e per l’archiviazione primaria. Tenere presente che l'archiviazione primaria usata prima di installare l'aggiornamento 2 è indicata dalla riga **PRIMARY TIERED STORAGE USED** (ARCHIVIAZIONE PRIMARIA A LIVELLI USATA).
  * Utilizzare il menu a discesa nell'angolo in alto a destra del grafico per specificare una scala temporale di 1 settimana, 1 mese, 3 mesi o 1 anno. Si noti che il grafico di primo livello viene aggiornato solo una volta al giorno e pertanto rifletterà i totali del giorno precedente.
    
    Per ulteriori informazioni, vedere [Utilizzo del servizio StorSimple Manager per monitorare il dispositivo StorSimple](storsimple-monitor-device.md).
* **Panoramica sull'utilizzo**: nell'area relativa alla **panoramica sull'uso**, è possibile visualizzare la quantità di archiviazione primaria usata, la quantità di archiviazione sottoposta a provisioning e la capacità di archiviazione massima per il dispositivo. Confrontando i numeri di utilizzo alla quantità massima di archiviazione disponibile, è possibile visualizzare immediatamente se è necessario ottenere memoria aggiuntiva. Si noti che questa panoramica viene aggiornata ogni 15 minuti, e a causa della differenza nella frequenza di aggiornamento, potrebbe mostrare numeri diversi da quelli visualizzati nell'area del grafico mostrato sopra, che viene aggiornato ogni giorno. Per ulteriori informazioni, vedere [Utilizzo del servizio StorSimple Manager per monitorare il dispositivo StorSimple](storsimple-monitor-device.md).
* **Avvisi**: nell'area relativa agli **avvisi** viene fornita una panoramica degli avvisi per il dispositivo. Gli avvisi sono raggruppati in base alla gravità e viene fornito un conteggio del numero di avvisi a ogni livello di gravità. Cliccando sulla gravità dell'avviso si apre una scheda avvisi che mostra solo gli avvisi di tale livello di gravità per il dispositivo.
* **Processi**: nell'area relativa ai **processi** viene mostrato il risultato della recente attività di processo. Questo garantisce che il sistema funziona come previsto, o può far sapere all’utente se è necessario adottare misure correttive. Per ulteriori informazioni sui processi completati di recente, fare clic su **processi completati nelle ultime 24 ore**.
* L’area **riepilogo rapido** a destra del dashboard fornisce informazioni utili come ad esempio il modello di dispositivo, il numero di serie, stato, descrizione e numero di volumi.

È inoltre possibile configurare il failover e visualizzare gli iniziatori connessi dal dashboard del dispositivo.

Le attività comuni che possono essere eseguite in questa pagina sono:

* Visualizzare gli iniziatori connessi
* Trovare il numero di serie del dispositivo
* Trovare l’IQN di destinazione del dispositivo

## <a name="view-connected-initiators"></a>Visualizzare gli iniziatori connessi
È possibile visualizzare gli iniziatori iSCSI connessi al dispositivo facendo clic sul collegamento **Visualizzare gli iniziatori connessi** fornito nell'area di **riepilogo rapido** del dashboard del dispositivo. Questa pagina fornisce un elenco tabulare degli iniziatori connessi correttamente al dispositivo. Per ogni iniziatore, è possibile vedere:

* iSCSI Qualified Name (IQN) dell'iniziatore connesso.
* Il nome del record di controllo di accesso (ACR) che consente questo iniziatore connesso.
* L'indirizzo IP dell'iniziatore connesso.
* Le interfacce di rete a cui l'iniziatore è connesso nel dispositivo di archiviazione. Questi possono variare da DATA 0 a DATA 5.
* Tutti i volumi che l'iniziatore connesso è autorizzato ad accedere in base alla configurazione ACR corrente.

Se si visualizzano iniziatori imprevisti nell'elenco o non si visualizzano quelli previsti, verificare la configurazione ACR. Un massimo di 512 iniziatori può connettersi al dispositivo.

## <a name="find-the-device-serial-number"></a>Trovare il numero di serie del dispositivo
Il numero di serie del dispositivo potrebbe essere necessario quando si configura Microsoft Multipath i/o (MPIO) sul dispositivo. Eseguire i passaggi seguenti per trovare il numero di serie del dispositivo.

#### <a name="to-find-the-device-serial-number"></a>Per trovare il numero di serie del dispositivo
1. Andare su **Dispositivi** > **Dashboard**.
2. Nel riquadro a destra del dashboard, individuare l’area **riepilogo rapido** .
3. Scorrere verso il basso e individuare il numero di serie.

## <a name="find-the-device-target-iqn"></a>Trovare l’IQN di destinazione del dispositivo
L’IQN di destinazione del dispositivo potrebbe essere necessario quando si configura il Challenge Handshake Authentication Protocol (CHAP) sul dispositivo StorSimple. Eseguire i passaggi seguenti per trovare l’IQN di destinazione del dispositivo.

### <a name="to-find-the-device-target-iqn"></a>Per trovare l’IQN di destinazione del dispositivo
1. Andare su **Dispositivi** > **Dashboard**.
2. Nel riquadro a destra del dashboard, individuare l’area **riepilogo rapido** .
3. Scorrere verso il basso e individuare l’IQN di destinazione.

## <a name="next-steps"></a>Passaggi successivi
* Ulteriori informazioni sul [dashboard del servizio StorSimple Manager](storsimple-service-dashboard.md).
* Ulteriori informazioni sull’ [utilizzo del servizio StorSimple Manager per amministrare il dispositivo StorSimple](storsimple-manager-service-administration.md).

