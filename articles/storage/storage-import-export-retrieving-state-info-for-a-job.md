---
title: informazioni sullo stato aaaRetrieving per un processo di importazione/esportazione di Azure | Documenti Microsoft
description: Informazioni su come tooobtain informazioni sullo stato per i processi del servizio di importazione/esportazione di Microsoft Azure.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 22d7e5f0-94da-49b4-a1ac-dd4c14a423c2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: muralikk
ms.openlocfilehash: cbc35660519573d92f641924ac0025c9e577d69b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="retrieving-state-information-for-an-importexport-job"></a>Recupero delle informazioni sullo stato per un processo di Importazione/Esportazione di Azure
È possibile chiamare hello [recupero del processo](/rest/api/storageimportexport/jobs#Jobs_Get) operazione tooretrieve informazioni entrambi importare ed esportare i processi. Hello informazioni restituite includono:

-   stato corrente di Hello del processo di hello.

-   percentuale approssimativa Hello che ogni processo è stata completata.

-   stato corrente di Hello di ogni unità.

-   Gli URI per i BLOB contenenti i log degli errori e informazioni dettagliate sulla registrazione (se abilitati).

Nelle sezioni seguenti Hello viene informazioni hello restituite da hello `Get Job` operazione.

## <a name="job-states"></a>Stati del processo
tabella Hello e diagramma di stato hello riportato di seguito vengono descritti gli stati di hello che un processo passa attraverso il ciclo di vita. stato corrente di Hello del processo di hello può essere determinato dal chiamante hello `Get Job` operazione.

![JobStates](./media/storage-import-export-retrieving-state-info-for-a-job/JobStates.png "JobStates")

Hello nella tabella seguente viene descritto ogni stato di un processo può attraversare.

|Stato del processo|Descrizione|
|---------------|-----------------|
|`Creating`|Dopo che si chiama l'operazione Put Job hello, viene creato un processo e lo stato viene impostato troppo`Creating`. Durante l'esecuzione hello processo hello `Creating` stato, servizio di importazione/esportazione hello presuppone hello unità non sono stati spediti toohello datacenter. Un processo può rimanere in hello `Creating` stato backup tootwo settimane, dopo il quale viene eliminato automaticamente dal servizio hello.<br /><br /> Se si chiama operazione Update Job Properties hello durante il processo di hello hello `Creating` stato, hello processo rimane in hello `Creating` stato e hello timeout intervallo è reset tootwo settimane.|
|`Shipping`|Dopo aver spedito il pacchetto, è necessario chiamare hello Update Job Properties aggiornamento hello lo stato di operazione del processo di hello troppo`Shipping`. Hello stato shipping può essere impostata solo se hello `DeliveryPackage` (spedizioniere e numero di tracciabilità) e hello `ReturnAddress` sono state impostate proprietà per il processo di hello.<br /><br /> processo Hello rimarrà in stato di spedizione hello per le settimane tootwo. Se due settimane sono stati superati e non sono state ricevute unità hello, riceverà una notifica operatori del servizio di importazione/esportazione hello.|
|`Received`|Dopo la ricezione di tutte le unità al data center di hello, verrà impostato lo stato del processo hello toohello stato Received.|
|`Transferring`|Dopo che sono state ricevute hello unità al data center di hello e almeno un'unità è iniziata l'elaborazione, verrà impostato lo stato del processo hello toohello `Transferring` stato. Vedere hello `Drive States` sezione riportata di seguito per informazioni dettagliate.|
|`Packaging`|Una volta completata l'elaborazione di tutte le unità, il processo di hello verrà inserito in hello `Packaging` stato fino a quando non hello unità spedita toohello indietro cliente.|
|`Completed`|Dopo che tutte le unità sono stati spediti toohello indietro cliente, se il processo di hello è stata completata senza errori, quindi hello processo verrà impostato toohello `Completed` stato. Hello processo verrà automaticamente eliminato dopo 90 giorni in hello `Completed` stato.|
|`Closed`|Dopo che tutte le unità sono stati spediti toohello indietro cliente, se sono state apportate eventuali errori durante l'elaborazione di hello del processo di hello, quindi hello processo verrà impostato toohello `Closed` stato. Hello processo verrà automaticamente eliminato dopo 90 giorni in hello `Closed` stato.|

È possibile annullare un processo solo in determinati stati. Un processo annullato passerà hello passaggio copia dei dati, ma in caso contrario segue hello stesso transizioni di stato di un processo non è stato annullato.

Hello nella tabella seguente vengono descritti gli errori che possono verificarsi per ogni stato del processo, nonché l'effetto hello sul processo di hello quando si verifica un errore.

|Stato del processo|Evento|Risoluzione/passaggi successivi|
|---------------|-----------|------------------------------|
|`Creating or Undefined`|È arrivato uno o più dischi per un processo, ma non è il processo di hello hello `Shipping` stato o non sono presenti record di processo hello in servizio hello.|team addetto alle operazioni del servizio importazione/esportazione Hello verrà tenta toocontact hello cliente toocreate o aggiornare il processo di hello con processo hello toomove di informazioni necessarie in avanti.<br /><br /> Se il team di operazioni hello è cliente hello toocontact Impossibile entro due settimane, hello tenterà tooreturn hello unità.<br /><br /> In caso di hello che non può essere restituita unità hello e hello cliente non sia raggiungibile, hello unità verranno distrutte in modo sicuro 90 giorni.<br /><br /> Si noti che un processo non può essere elaborato finché non il relativo stato viene aggiornato troppo`Shipping`.|
|`Shipping`|pacchetto di Hello per un processo non è arrivato più di due settimane.|team addetto alle operazioni Hello notificherà cliente hello di pacchetto mancante hello. In base alla risposta del cliente hello, team addetto alle operazioni hello verrà estendere hello intervallo toowait per tooarrive pacchetto hello o annullare il processo di hello.<br /><br /> In caso di hello cliente hello non può essere contattato o non risponde entro 30 giorni, team addetto alle operazioni hello verrà avviata l'azione toomove hello processo hello `Shipping` stato direttamente toohello `Closed` stato.|
|`Completed/Closed`|unità di Hello mai raggiunto indirizzo hello o sono danneggiate durante la spedizione (si applica il processo di esportazione solo tooan).|Se l'unità hello non raggiungono l'indirizzo del mittente hello, cliente hello deve prima operazione di recupero del processo di chiamata hello o controllare lo stato di processo hello in hello tooensure portale che hello unità sono state spedite. Se sono state spedite le unità hello, cliente hello deve contattare tootry provider shipping hello e individuare le unità hello.<br /><br /> Se hello unità sono danneggiate durante la spedizione, il cliente hello opportuno toorequest un altro processo di esportazione o BLOB mancanti hello di download.|
|`Transferring/Packaging`|L'indirizzo del mittente per il processo manca o è errato.|team addetto alle operazioni Hello raggiungerà toohello contatto per l'indirizzo corretto hello tooobtain processo hello.<br /><br /> In caso di hello cliente hello non è raggiungibile, hello unità verranno distrutte in modo sicuro in 90 giorni.|
|`Creating / Shipping/ Transferring`|Un'unità che non compare nell'elenco di hello di unità toobe importato è incluso in hello spedizione del pacchetto.|Hello unità aggiuntive non verranno elaborate e verranno restituite toohello cliente quando viene completato il processo di hello.|

## <a name="drive-states"></a>Stati dell'unità
tabella Hello e diagramma hello riportato di seguito descrivono hello del ciclo di vita di una singola unità passa attraverso un processo di importazione o esportazione. È possibile recuperare stato corrente dell'unità hello hello chiamante `Get Job` hello e controllando `State` elemento di hello `DriveList` proprietà.

![DriveStates](./media/storage-import-export-retrieving-state-info-for-a-job/DriveStates.png "DriveStates")

Hello nella tabella seguente viene descritto ogni stato di un'unità può attraversare.

|Stato dell'unità|Descrizione|
|-----------------|-----------------|
|`Specified`|Per un processo di importazione, quando viene creato il processo di hello con hello operazione Put Job, lo stato iniziale di hello per un'unità è hello `Specified` stato. Per un processo di esportazione, poiché viene specificata alcuna unità quando viene creato il processo di hello, lo stato iniziale dell'unità di hello è hello `Received` stato.|
|`Received`|unità di Hello passerà toohello `Received` stato quando hello operatore del servizio di importazione/esportazione ha elaborato le unità ricevute dalla società per un processo di importazione di spedizione hello hello. Per un processo di esportazione, lo stato iniziale dell'unità di hello è hello `Received` stato.|
|`NeverReceived`|unità di Hello passerà toohello `NeverReceived` stato quando hello pacchetto per un processo raggiunge, ma il pacchetto di hello non contiene unità hello. Un'unità può inoltre passare a questo stato se sono trascorsi due settimane dal servizio hello ha ricevuto le informazioni di spedizione hello, ma il pacchetto di hello non è ancora arrivato al data center di hello.|
|`Transferring`|Un'unità passerà toohello `Transferring` stato quando hello servizio inizia tootransfer dati hello tooWindows di unità di archiviazione di Azure.|
|`Completed`|Un'unità passerà toohello `Completed` stato quando il servizio hello ha trasferito tutti i dati di hello senza errori.|
|`CompletedMoreInfo`|Un'unità passerà toohello `CompletedMoreInfo` stato quando hello servizio ha rilevato alcuni problemi durante la copia dei dati da o toohello unità. Hello informazioni possono includere errori, avvisi o messaggi informativi su sovrascrittura dei BLOB.|
|`ShippedBack`|unità di Hello passerà toohello `ShippedBack` lo stato quando è stato spedito dall'indirizzo mittente toohello hello data center back.|

Hello nella tabella seguente vengono descritti gli stati di errore dell'unità di hello e hello azioni eseguite per ogni stato.

|Stato dell'unità|Evento|Risoluzione/Passaggio successivo|
|-----------------|-----------|-----------------------------|
|`NeverReceived`|Un'unità che è contrassegnata come `NeverReceived` (perché non è stato ricevuto come parte della spedizione del processo di hello) arriva in un'altra spedizione.|team addetto alle operazioni Hello sposterà hello unità toohello `Received` stato.|
|`N/A`|Un'unità che non fa parte di qualsiasi processo arriva al centro dati hello come parte di un altro processo.|unità di Hello verrà contrassegnata come aggiuntiva e verrà restituito toohello cliente quando viene completato il processo di hello associato al pacchetto originale hello.|

## <a name="faulted-states"></a>Stati con errori
Quando un processo o un'unità non tooprogress normalmente tramite il ciclo di vita previsto, hello processo o un'unità verranno spostati in un `Faulted` stato. A questo punto, il team di operazioni hello contatterà il cliente di hello tramite e-mail o telefono. Una volta risolto il problema di hello, hello verificati errori processo o l'unità verrà intrapresa fuori hello `Faulted` dello stato e spostata in hello appropriati dello stato.

## <a name="next-steps"></a>Passaggi successivi

* [Tramite l'API REST del servizio importazione/esportazione hello](storage-import-export-using-the-rest-api.md)
