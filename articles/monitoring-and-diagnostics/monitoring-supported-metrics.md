---
title: le metriche di monitoraggio - metriche supportate per ogni tipo di risorsa aaaAzure | Documenti Microsoft
description: Elenco delle metriche disponibili per ogni tipo di risorsa con il monitoraggio di Azure.
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 63d4ac65-1688-40d1-85c8-7cd408285b0f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/05/2017
ms.author: johnkem
ms.openlocfilehash: 66834238a1a4fcd7db1464cc023c18ee2563517a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="supported-metrics-with-azure-monitor"></a>Metriche supportate con il monitoraggio di Azure
Monitoraggio di Azure fornisce diversi modi toointeract con le metriche, tra cui creazione di grafici nel portale di hello, accesso tramite l'API REST hello o query su essi tramite PowerShell o CLI. Di seguito è riportato un elenco completo di tutte le metriche attualmente disponibili con la pipeline delle metriche di monitoraggio di Azure.

> [!NOTE]
> Altre metriche potrebbero essere disponibili nel portale di hello o utilizzando le API legacy. Questo elenco include solo le metriche di anteprima pubblica disponibile tramite l'anteprima pubblica di hello della pipeline metrica di monitoraggio di Azure hello consolidato.
>
>

## <a name="microsoftanalysisservicesservers"></a>Microsoft.AnalysisServices/servers

|Metrica|Nome visualizzato per la metrica|Unità|Tipo di aggregazione|Descrizione|
|---|---|---|---|---|
|qpu_metric|QPU|Numero|Media|QPU. Intervallo 0-100 per S1, 0-200 per S2 e 0-400 per S4|
|memory_metric|Memoria|Byte|Media|Memoria. Intervallo 0-25 GB per S1, 0-50 GB per S2 e 0-100 GB per S4|
|TotalConnectionRequests|Numero totale di richieste di connessione|Numero|Media|Numero totale delle richieste di connessione in arrivo.|
|SuccessfullConnectionsPerSec|Connessioni riuscite al secondo|Conteggio al secondo|Media|Numero delle connessioni completate correttamente al secondo.|
|TotalConnectionFailures|Numero totale di errori di connessione|Numero|Media|Numero totale dei tentativi di connessione non riusciti.|
|CurrentUserSessions|Sessioni utente correnti|Numero|Media|Numero corrente di sessioni utente attive.|
|QueryPoolBusyThreads|Thread occupati pool di query|Numero|Media|Numero dei thread occupati nel pool di thread di query hello.|
|CommandPoolJobQueueLength|Lunghezza coda processi nel pool di comandi|Numero|Media|Numero di processi in coda hello hello comando del pool dei thread.|
|ProcessingPoolJobQueueLength|Lunghezza coda processi nel pool di elaborazione|Numero|Media|Numero di processi non dei / O nella coda di hello di hello pool di thread di elaborazione.|
|CurrentConnections|Connessione: connessioni correnti|Numero|Media|Numero corrente delle connessioni client stabilite.|
|CleanerCurrentPrice|Memoria: prezzo corrente pulitura memoria|Numero|Media|Prezzo corrente di memoria, $/ byte/ora, too1000 normalizzato.|
|CleanerMemoryShrinkable|Memoria: pulitura memoria compattabile|Byte|Media|Quantità di memoria, in byte, soggetto toopurging dallo sfondo hello più chiara.|
|CleanerMemoryNonshrinkable|Memoria: pulitura memoria non compattabile|Byte|Media|Quantità di memoria, in byte, non soggetto toopurging dallo sfondo hello più chiara.|
|MemoryUsage|Memoria: utilizzo memoria|Byte|Media|Utilizzo della memoria di hello processo server utilizzato per il calcolo del prezzo di memoria più pulita. Uguale a toocounter Process\PrivateBytes più hello di dati con mapping in memoria, ignorando la memoria è stato eseguito il mapping o allocazione dal motore in memoria analitica hello xVelocity (VertiPaq) che superano il motore xVelocity hello limite di memoria.|
|MemoryLimitHard|Memoria: limite memoria assoluto|Byte|Media|Limite assoluto della memoria, dal file di configurazione.|
|MemoryLimitHigh|Memoria: limite memoria massimo|Byte|Media|Limite superiore della memoria, dal file di configurazione.|
|MemoryLimitLow|Memoria: limite memoria minimo|Byte|Media|Limite inferiore della memoria, dal file di configurazione.|
|MemoryLimitVertiPaq|Memoria: limite memoria VertiPaq|Byte|Media|Limite in memoria dal file di configurazione.|
|Quota|Memoria: quota|Byte|Media|Quota di memoria corrente, in byte. Le quote di memoria sono note anche come concessioni di memoria o prenotazioni di memoria.|
|QuotaBlocked|Memoria: Richieste di quota bloccate|Numero|Media|Numero corrente di richieste di quota bloccate fino a quando non vengono liberate altre quote di memoria.|
|VertiPaqNonpaged|Memoria: VertiPaq non di paging|Byte|Media|Byte di memoria bloccata nel hello working set per l'utilizzo dal motore in memoria hello.|
|VertiPaqPaged|Memoria: VertiPaq di paging|Byte|Media|Byte di memoria di paging in uso per i dati in memoria.|
|RowsReadPerSec|Elaborazione: righe lette al secondo|Conteggio al secondo|Media|Velocità di lettura delle righe da tutti i database relazionali.|
|RowsConvertedPerSec|Elaborazione: righe convertite al secondo|Conteggio al secondo|Media|Velocità di conversione delle righe durante l'elaborazione.|
|RowsWrittenPerSec|Elaborazione: righe scritte al secondo|Conteggio al secondo|Media|Velocità di scrittura delle righe durante l'elaborazione.|
|CommandPoolBusyThreads|Thread: thread occupati nel pool di comandi|Numero|Media|Numero dei thread occupati nel pool di thread comando hello.|
|CommandPoolIdleThreads|Thread: Thread inattivi pool di comandi|Numero|Media|Numero di thread inattivi nel pool di thread comando hello.|
|LongParsingBusyThreads|Thread: thread occupati per analisi dei thread lunghi|Numero|Media|Numero dei thread occupati nel pool di thread analisi dei thread lunghi hello.|
|LongParsingIdleThreads|Thread: Thread inattivi per analisi dei thread lunghi|Numero|Media|Numero di thread inattivi nel pool di thread analisi dei thread lunghi hello.|
|LongParsingJobQueueLength|Thread: lunghezza coda processi di analisi dei thread lunghi|Numero|Media|Numero di processi in coda hello di hello analisi dei thread lunghi pool di thread.|
|ProcessingPoolBusyIOJobThreads|Thread: thread di processi di I/O occupati nel pool di elaborazione|Numero|Media|Numero di thread che eseguono processi dei / o nel pool di thread di elaborazione hello.|
|ProcessingPoolBusyNonIOThreads|Thread: Thread non di I/O occupati nel pool di elaborazione|Numero|Media|Numero di thread che eseguono processi non dei / O nel pool di thread di elaborazione hello.|
|ProcessingPoolIOJobQueueLength|Thread: lunghezza coda processi di I/O nel pool di elaborazione|Numero|Media|Numero di processi dei / o in coda hello di hello pool di thread di elaborazione.|
|ProcessingPoolIdleIOJobThreads|Thread: thread di processi di I/O inattivi nel pool di elaborazione|Numero|Media|Numero di thread inattivi per i processi nel pool di thread di elaborazione hello.|
|ProcessingPoolIdleNonIOThreads|Thread: thread non di I/O inattivi nel pool di elaborazione|Numero|Media|Numero di thread inattivi nel pool di thread di elaborazione hello dedicato toonon processi dei / O.|
|QueryPoolIdleThreads|Thread: thread inattivi nel pool di query|Numero|Media|Numero di thread inattivi per i processi nel pool di thread di elaborazione hello.|
|QueryPoolJobQueueLength|Thread: lunghezza coda processi nel pool di query|Numero|Media|Numero di processi in coda hello del pool di thread di query hello.|
|ShortParsingBusyThreads|Thread: thread occupati per analisi dei thread brevi|Numero|Media|Numero dei thread occupati nel hello breve l'analisi di pool di thread.|
|ShortParsingIdleThreads|Thread: thread inattivi per analisi dei thread brevi|Numero|Media|Numero di thread inattivi nel hello breve l'analisi di pool di thread.|
|ShortParsingJobQueueLength|Thread: lunghezza coda processi di analisi dei thread brevi|Numero|Media|Numero di processi in coda hello di hello breve l'analisi di pool di thread.|
|memory_thrashing_metric|Thrashing di memoria|Percentuale|Media|Thrashing di memoria medio.|

## <a name="microsoftapimanagementservice"></a>Microsoft.ApiManagement/service

|Metrica|Nome visualizzato per la metrica|Unità|Tipo di aggregazione|Descrizione|
|---|---|---|---|---|
|TotalRequests|Totale richieste gateway|Numero|Totale|Numero di richieste del gateway|
|SuccessfulRequests|Richieste gateway riuscite|Numero|Totale|Numero di richieste del gateway riuscite|
|UnauthorizedRequests|Richieste del gateway non autorizzate|Numero|Totale|Numero di richieste del gateway non autorizzate|
|FailedRequests|Richieste gateway non riuscite|Numero|Totale|Numero di errori nelle richieste gateway|
|OtherRequests|Altre richieste del gateway|Numero|Totale|Numero di altre richieste del gateway|

## <a name="microsoftbatchbatchaccounts"></a>Microsoft.Batch/batchAccounts

|Metrica|Nome visualizzato per la metrica|Unità|Tipo di aggregazione|Descrizione|
|---|---|---|---|---|
|CoreCount|Numero di core dedicati|Numero|Totale|Numero totale di core dedicati in account batch hello|
|TotalNodeCount|Numero di nodi dedicati|Numero|Totale|Numero totale di nodi dedicati nell'account di batch hello|
|LowPriorityCoreCount|Numero di core a bassa priorità|Numero|Totale|Numero totale di core con priorità bassa nell'account di batch hello|
|TotalLowPriorityNodeCount|Numero di nodi a bassa priorità|Numero|Totale|Numero totale di nodi con priorità bassa nell'account di batch hello|
|CreatingNodeCount|Numero nodi creati|Conteggio|Totale|Il numero di nodi in fase di creazione|
|StartingNodeCount|Numero nodi avviati|Conteggio|Totale|Il numero di nodi in fase di avvio|
|WaitingForStartTaskNodeCount|Numero nodi in attesa dell'attività di avvio|Conteggio|Totale|Numero di nodi in attesa di hello Avvia attività toocomplete|
|StartTaskFailedNodeCount|Numero nodi con attività di avvio non riuscita|Conteggio|Totale|Numero di nodi in cui non è riuscita hello Avvia attività|
|IdleNodeCount|Numero nodi inattivi|Conteggio|Totale|Il numero di nodi inattivi|
|OfflineNodeCount|Numero nodi offline|Conteggio|Totale|Il numero di nodi offline|
|RebootingNodeCount|Numero nodi riavviati|Conteggio|Totale|Il numero di nodi in fase di riavvio|
|ReimagingNodeCount|Numero nodi con immagine ricreata|Conteggio|Totale|Il numero di nodi in fase di ricreazione dell'immagine|
|RunningNodeCount|Numero nodi eseguiti|Conteggio|Totale|Il numero di nodi in esecuzione|
|LeavingPoolNodeCount|Numero nodi usciti dal pool|Conteggio|Totale|Numero di nodi lasciando hello Pool|
|UnusableNodeCount|Numero nodi non usabili|Conteggio|Totale|Il numero di nodi che non possono essere usati|
|PreemptedNodeCount|Numero di nodi annullati|Numero|Totale|Numero di nodi annullati|
|TaskStartEvent|Eventi attività avviate|Numero|Totale|Il numero totale di attività avviate|
|TaskCompleteEvent|Eventi attività completate|Numero|Totale|Il numero totale di attività completate|
|TaskFailEvent|Eventi attività non riuscite|Numero|Totale|Il numero totale di attività completate con lo stato Non riuscito|
|PoolCreateEvent|Eventi pool creati|Numero|Totale|Il numero totale di pool che sono stati creati|
|PoolResizeStartEvent|Eventi ridimensionamento pool avviati|Numero|Totale|Il numero totale di ridimensionamenti dei pool avviati|
|PoolResizeCompleteEvent|Eventi ridimensionamento pool completati|Numero|Totale|Il numero totale di ridimensionamenti dei pool completati|
|PoolDeleteStartEvent|Eventi eliminazione pool avviati|Numero|Totale|Il numero totale di eliminazioni di pool avviate|
|PoolDeleteCompleteEvent|Eventi eliminazione pool completati|Numero|Totale|Il numero totale di eliminazioni di pool completate|

## <a name="microsoftcacheredis"></a>Microsoft.Cache/redis

|Metrica|Nome visualizzato per la metrica|Unità|Tipo di aggregazione|Descrizione|
|---|---|---|---|---|
|connectedclients|Client connessi|Numero|Massima||
|totalcommandsprocessed|Totale operazioni|Numero|Totale||
|cachehits|Riscontri cache|Numero|Totale||
|cachemisses|Mancati riscontri nella cache|Numero|Totale||
|getcommands|Operazioni Get|Numero|Totale||
|setcommands|Operazioni Set|Numero|Totale||
|evictedkeys|Chiavi rimosse|Numero|Totale||
|totalkeys|Totale chiavi|Numero|Massima||
|expiredkeys|Chiavi scadute|Numero|Totale||
|usedmemory|Memoria utilizzata|Byte|Massima||
|usedmemoryRss|Memoria utilizzata RSS|Byte|Massima||
|serverLoad|Carico server|Percentuale|Massima||
|cacheWrite|Scrittura nella cache|Byte al secondo|Massima||
|cacheRead|Lettura da cache|Byte al secondo|Massima||
|percentProcessorTime|CPU|Percentuale|Massima||
|connectedclients0|Client connessi (partizione 0)|Numero|Massima||
|totalcommandsprocessed0|Totale operazioni (partizione 0)|Numero|Totale||
|cachehits0|Riscontri cache (partizione 0)|Numero|Totale||
|cachemisses0|Mancati riscontri nella cache (partizione 0)|Numero|Totale||
|getcommands0|Operazioni Get (partizione 0)|Numero|Totale||
|setcommands0|Operazioni Set (partizione 0)|Numero|Totale||
|evictedkeys0|Chiavi rimosse (partizione 0)|Numero|Totale||
|totalkeys0|Totale chiavi (partizione 0)|Numero|Massima||
|expiredkeys0|Chiavi scadute (partizione 0)|Numero|Totale||
|usedmemory0|Memoria usata (partizione 0)|Byte|Massima||
|usedmemoryRss0|Memoria usata RSS (partizione 0)|Byte|Massima||
|serverLoad0|Carico server (partizione 0)|Percentuale|Massima||
|cacheWrite0|Scrittura nella cache (partizione 0)|Byte al secondo|Massima||
|cacheRead0|Lettura da cache (partizione 0)|Byte al secondo|Massima||
|percentProcessorTime0|CPU (partizione 0)|Percentuale|Massima||
|connectedclients1|Client connessi (partizione 1)|Numero|Massima||
|totalcommandsprocessed1|Totale operazioni (partizione 1)|Numero|Totale||
|cachehits1|Riscontri cache (partizione 1)|Numero|Totale||
|cachemisses1|Mancati riscontri nella cache (partizione 1)|Numero|Totale||
|getcommands1|Operazioni Get (partizione 1)|Numero|Totale||
|setcommands1|Operazioni Set (partizione 1)|Numero|Totale||
|evictedkeys1|Chiavi rimosse (partizione 1)|Numero|Totale||
|totalkeys1|Totale chiavi (partizione 1)|Numero|Massima||
|expiredkeys1|Chiavi scadute (partizione 1)|Numero|Totale||
|usedmemory1|Memoria usata (partizione 1)|Byte|Massima||
|usedmemoryRss1|Memoria usata RSS (partizione 1)|Byte|Massima||
|serverLoad1|Carico server (partizione 1)|Percentuale|Massima||
|cacheWrite1|Scrittura nella cache (partizione 1)|Byte al secondo|Massima||
|cacheRead1|Lettura da cache (partizione 1)|Byte al secondo|Massima||
|percentProcessorTime1|CPU (partizione 1)|Percentuale|Massima||
|connectedclients2|Client connessi (partizione 2)|Numero|Massima||
|totalcommandsprocessed2|Totale operazioni (partizione 2)|Numero|Totale||
|cachehits2|Riscontri cache (partizione 2)|Numero|Totale||
|cachemisses2|Mancati riscontri nella cache (partizione 2)|Numero|Totale||
|getcommands2|Operazioni Get (partizione 2)|Numero|Totale||
|setcommands2|Operazioni Set (partizione 2)|Numero|Totale||
|evictedkeys2|Chiavi rimosse (partizione 2)|Numero|Totale||
|totalkeys2|Totale chiavi (partizione 2)|Numero|Massima||
|expiredkeys2|Chiavi scadute (partizione 2)|Numero|Totale||
|usedmemory2|Memoria usata (partizione 2)|Byte|Massima||
|usedmemoryRss2|Memoria usata RSS (partizione 2)|Byte|Massima||
|serverLoad2|Carico server (partizione 2)|Percentuale|Massima||
|cacheWrite2|Scrittura nella cache (partizione 2)|Byte al secondo|Massima||
|cacheRead2|Lettura da cache (partizione 2)|Byte al secondo|Massima||
|percentProcessorTime2|CPU (partizione 2)|Percentuale|Massima||
|connectedclients3|Client connessi (partizione 3)|Numero|Massima||
|totalcommandsprocessed3|Totale operazioni (partizione 3)|Numero|Totale||
|cachehits3|Riscontri cache (partizione 3)|Numero|Totale||
|cachemisses3|Mancati riscontri nella cache (partizione 3)|Numero|Totale||
|getcommands3|Operazioni Get (partizione 3)|Numero|Totale||
|setcommands3|Operazioni Set (partizione 3)|Numero|Totale||
|evictedkeys3|Chiavi rimosse (partizione 3)|Numero|Totale||
|totalkeys3|Totale chiavi (partizione 3)|Numero|Massima||
|expiredkeys3|Chiavi scadute (partizione 3)|Numero|Totale||
|usedmemory3|Memoria usata (partizione 3)|Byte|Massima||
|usedmemoryRss3|Memoria usata RSS (partizione 3)|Byte|Massima||
|serverLoad3|Carico server (partizione 3)|Percentuale|Massima||
|cacheWrite3|Scrittura nella cache (partizione 3)|Byte al secondo|Massima||
|cacheRead3|Lettura da cache (partizione 3)|Byte al secondo|Massima||
|percentProcessorTime3|CPU (partizione 3)|Percentuale|Massima||
|connectedclients4|Client connessi (partizione 4)|Numero|Massima||
|totalcommandsprocessed4|Totale operazioni (partizione 4)|Numero|Totale||
|cachehits4|Riscontri cache (partizione 4)|Numero|Totale||
|cachemisses4|Mancati riscontri nella cache (partizione 4)|Numero|Totale||
|getcommands4|Operazioni Get (partizione 4)|Numero|Totale||
|setcommands4|Operazioni Set (partizione 4)|Numero|Totale||
|evictedkeys4|Chiavi rimosse (partizione 4)|Numero|Totale||
|totalkeys4|Totale chiavi (partizione 4)|Numero|Massima||
|expiredkeys4|Chiavi scadute (partizione 4)|Numero|Totale||
|usedmemory4|Memoria usata (partizione 4)|Byte|Massima||
|usedmemoryRss4|Memoria usata RSS (partizione 4)|Byte|Massima||
|serverLoad4|Carico server (partizione 4)|Percentuale|Massima||
|cacheWrite4|Scrittura nella cache (partizione 4)|Byte al secondo|Massima||
|cacheRead4|Lettura da cache (partizione 4)|Byte al secondo|Massima||
|percentProcessorTime4|CPU (partizione 4)|Percentuale|Massima||
|connectedclients5|Client connessi (partizione 5)|Numero|Massima||
|totalcommandsprocessed5|Totale operazioni (partizione 5)|Numero|Totale||
|cachehits5|Riscontri cache (partizione 5)|Numero|Totale||
|cachemisses5|Mancati riscontri nella cache (partizione 5)|Numero|Totale||
|getcommands5|Operazioni Get (partizione 5)|Numero|Totale||
|setcommands5|Operazioni Set (partizione 5)|Numero|Totale||
|evictedkeys5|Chiavi rimosse (partizione 5)|Numero|Totale||
|totalkeys5|Totale chiavi (partizione 5)|Numero|Massima||
|expiredkeys5|Chiavi scadute (partizione 5)|Numero|Totale||
|usedmemory5|Memoria usata (partizione 5)|Byte|Massima||
|usedmemoryRss5|Memoria usata RSS (partizione 5)|Byte|Massima||
|serverLoad5|Carico server (partizione 5)|Percentuale|Massima||
|cacheWrite5|Scrittura nella cache (partizione 5)|Byte al secondo|Massima||
|cacheRead5|Lettura da cache (partizione 5)|Byte al secondo|Massima||
|percentProcessorTime5|CPU (partizione 5)|Percentuale|Massima||
|connectedclients6|Client connessi (partizione 6)|Numero|Massima||
|totalcommandsprocessed6|Totale operazioni (partizione 6)|Numero|Totale||
|cachehits6|Riscontri cache (partizione 6)|Numero|Totale||
|cachemisses6|Mancati riscontri nella cache (partizione 6)|Numero|Totale||
|getcommands6|Operazioni Get (partizione 6)|Numero|Totale||
|setcommands6|Operazioni Set (partizione 6)|Numero|Totale||
|evictedkeys6|Chiavi rimosse (partizione 6)|Numero|Totale||
|totalkeys6|Totale chiavi (partizione 6)|Numero|Massima||
|expiredkeys6|Chiavi scadute (partizione 6)|Numero|Totale||
|usedmemory6|Memoria usata (partizione 6)|Byte|Massima||
|usedmemoryRss6|Memoria usata RSS (partizione 6)|Byte|Massima||
|serverLoad6|Carico server (partizione 6)|Percentuale|Massima||
|cacheWrite6|Scrittura nella cache (partizione 6)|Byte al secondo|Massima||
|cacheRead6|Lettura da cache (partizione 6)|Byte al secondo|Massima||
|percentProcessorTime6|CPU (partizione 6)|Percentuale|Massima||
|connectedclients7|Client connessi (partizione 7)|Numero|Massima||
|totalcommandsprocessed7|Totale operazioni (partizione 7)|Numero|Totale||
|cachehits7|Riscontri cache (partizione 7)|Numero|Totale||
|cachemisses7|Mancati riscontri nella cache (partizione 7)|Numero|Totale||
|getcommands7|Operazioni Get (partizione 7)|Numero|Totale||
|setcommands7|Operazioni Set (partizione 7)|Numero|Totale||
|evictedkeys7|Chiavi rimosse (partizione 7)|Numero|Totale||
|totalkeys7|Totale chiavi (partizione 7)|Numero|Massima||
|expiredkeys7|Chiavi scadute (partizione 7)|Numero|Totale||
|usedmemory7|Memoria usata (partizione 7)|Byte|Massima||
|usedmemoryRss7|Memoria usata RSS (partizione 7)|Byte|Massima||
|serverLoad7|Carico server (partizione 7)|Percentuale|Massima||
|cacheWrite7|Scrittura nella cache (partizione 7)|Byte al secondo|Massima||
|cacheRead7|Lettura da cache (partizione 7)|Byte al secondo|Massima||
|percentProcessorTime7|CPU (partizione 7)|Percentuale|Massima||
|connectedclients8|Client connessi (partizione 8)|Numero|Massima||
|totalcommandsprocessed8|Totale operazioni (partizione 8)|Numero|Totale||
|cachehits8|Riscontri cache (partizione 8)|Numero|Totale||
|cachemisses8|Mancati riscontri nella cache (partizione 8)|Numero|Totale||
|getcommands8|Operazioni Get (partizione 8)|Numero|Totale||
|setcommands8|Operazioni Set (partizione 8)|Numero|Totale||
|evictedkeys8|Chiavi rimosse (partizione 8)|Numero|Totale||
|totalkeys8|Totale chiavi (partizione 8)|Numero|Massima||
|expiredkeys8|Chiavi scadute (partizione 8)|Numero|Totale||
|usedmemory8|Memoria usata (partizione 8)|Byte|Massima||
|usedmemoryRss8|Memoria usata RSS (partizione 8)|Byte|Massima||
|serverLoad8|Carico server (partizione 8)|Percentuale|Massima||
|cacheWrite8|Scrittura nella cache (partizione 8)|Byte al secondo|Massima||
|cacheRead8|Lettura da cache (partizione 8)|Byte al secondo|Massima||
|percentProcessorTime8|CPU (partizione 8)|Percentuale|Massima||
|connectedclients9|Client connessi (partizione 9)|Numero|Massima||
|totalcommandsprocessed9|Totale operazioni (partizione 9)|Numero|Totale||
|cachehits9|Riscontri cache (partizione 9)|Numero|Totale||
|cachemisses9|Mancati riscontri nella cache (partizione 9)|Numero|Totale||
|getcommands9|Operazioni Get (partizione 9)|Numero|Totale||
|setcommands9|Operazioni Set (partizione 9)|Numero|Totale||
|evictedkeys9|Chiavi rimosse (partizione 9)|Numero|Totale||
|totalkeys9|Totale chiavi (partizione 9)|Numero|Massima||
|expiredkeys9|Chiavi scadute (partizione 9)|Numero|Totale||
|usedmemory9|Memoria usata (partizione 9)|Byte|Massima||
|usedmemoryRss9|Memoria usata RSS (partizione 9)|Byte|Massima||
|serverLoad9|Carico server (partizione 9)|Percentuale|Massima||
|cacheWrite9|Scrittura nella cache (partizione 9)|Byte al secondo|Massima||
|cacheRead9|Lettura da cache (partizione 9)|Byte al secondo|Massima||
|percentProcessorTime9|CPU (partizione 9)|Percentuale|Massima||

## <a name="microsoftcognitiveservicesaccounts"></a>Microsoft.CognitiveServices/accounts

|Metrica|Nome visualizzato per la metrica|Unità|Tipo di aggregazione|Descrizione|
|---|---|---|---|---|
|TotalCalls|Totale chiamate|Numero|Totale|Numero totale di chiamate.|
|SuccessfulCalls|Chiamate riuscite|Numero|Totale|Numero di chiamate riuscite.|
|TotalErrors|Totale errori|Numero|Totale|Numero totale di chiamate con risposta di errore (codice di risposta HTTP 4xx o 5xx).|
|BlockedCalls|Chiamate bloccate|Numero|Totale|Numero di chiamate che hanno superato il limite di frequenza o di quota.|
|ServerErrors|Errori server|Numero|Totale|Numero di chiamate con errore interno del servizio (codice di risposta HTTP 5xx).|
|ClientErrors|Errori client|Numero|Totale|Numero di chiamate con errore sul lato client (codice di risposta HTTP 4xx).|
|DataIn|Dati in entrata|Byte|Totale|Dimensione in byte dei dati in entrata.|
|DataOut|Dati in uscita|Byte|Totale|Dimensione in byte dei dati in uscita.|
|Latency|Latenza|Millisecondi|Media|Latenza in millisecondi.|

## <a name="microsoftcomputevirtualmachines"></a>Microsoft.Compute/virtualMachines

|Metrica|Nome visualizzato per la metrica|Unità|Tipo di aggregazione|Descrizione|
|---|---|---|---|---|
|Percentage CPU|CPU percentuale|Percentuale|Media|percentuale di Hello di unità di calcolo allocato che sono attualmente in uso da hello le macchine virtuali|
|Rete in ingresso|Rete in ingresso|Byte|Totale|numero di Hello di byte ricevuti su tutte le interfacce di rete da macchine virtuali (traffico in ingresso) hello|
|Rete in uscita|Rete in uscita|Byte|Totale|numero di Hello di byte da tutte le interfacce di rete da hello le macchine virtuali (traffico in uscita)|
|Byte letti da disco|Byte letti da disco|Byte|Totale|Il numero totale di byte letti dal disco durante il periodo di monitoraggio|
|Disk Write Bytes|Byte scritti su disco|Byte|Totale|Numero totale di byte scritti toodisk durante il periodo di monitoraggio|
|Operazioni lettura disco/sec|Operazioni lettura disco/sec|Conteggio al secondo|Media|Il numero di IOPS letti dal disco|
|Disk Write Operations/Sec|Operazioni scrittura disco/sec|Conteggio al secondo|Media|Il numero di IOPS scritti sul disco|

## <a name="microsoftcomputevirtualmachinescalesets"></a>Microsoft.Compute/virtualMachineScaleSets

|Metrica|Nome visualizzato per la metrica|Unità|Tipo di aggregazione|Descrizione|
|---|---|---|---|---|
|Percentage CPU|CPU percentuale|Percentuale|Media|percentuale di Hello di unità di calcolo allocato che sono attualmente in uso da hello le macchine virtuali|
|Rete in ingresso|Rete in ingresso|Byte|Totale|numero di Hello di byte ricevuti su tutte le interfacce di rete da macchine virtuali (traffico in ingresso) hello|
|Rete in uscita|Rete in uscita|Byte|Totale|numero di Hello di byte da tutte le interfacce di rete da hello le macchine virtuali (traffico in uscita)|
|Byte letti da disco|Byte letti da disco|Byte|Totale|Il numero totale di byte letti dal disco durante il periodo di monitoraggio|
|Disk Write Bytes|Byte scritti su disco|Byte|Totale|Numero totale di byte scritti toodisk durante il periodo di monitoraggio|
|Operazioni lettura disco/sec|Operazioni lettura disco/sec|Conteggio al secondo|Media|Il numero di IOPS letti dal disco|
|Disk Write Operations/Sec|Operazioni scrittura disco/sec|Conteggio al secondo|Media|Il numero di IOPS scritti sul disco|

## <a name="microsoftcomputevirtualmachinescalesetsvirtualmachines"></a>Microsoft.Compute/virtualMachineScaleSets/virtualMachines

|Metrica|Nome visualizzato per la metrica|Unità|Tipo di aggregazione|Descrizione|
|---|---|---|---|---|
|Percentage CPU|CPU percentuale|Percentuale|Media|percentuale di Hello di unità di calcolo allocato che sono attualmente in uso da hello le macchine virtuali|
|Rete in ingresso|Rete in ingresso|Byte|Totale|numero di Hello di byte ricevuti su tutte le interfacce di rete da macchine virtuali (traffico in ingresso) hello|
|Rete in uscita|Rete in uscita|Byte|Totale|numero di Hello di byte da tutte le interfacce di rete da hello le macchine virtuali (traffico in uscita)|
|Byte letti da disco|Byte letti da disco|Byte|Totale|Il numero totale di byte letti dal disco durante il periodo di monitoraggio|
|Disk Write Bytes|Byte scritti su disco|Byte|Totale|Numero totale di byte scritti toodisk durante il periodo di monitoraggio|
|Operazioni lettura disco/sec|Operazioni lettura disco/sec|Conteggio al secondo|Media|Il numero di IOPS letti dal disco|
|Disk Write Operations/Sec|Operazioni scrittura disco/sec|Conteggio al secondo|Media|Il numero di IOPS scritti sul disco|

## <a name="microsoftcustomerinsightshubs"></a>Microsoft.CustomerInsights/hubs

|Metrica|Nome visualizzato per la metrica|Unità|Tipo di aggregazione|Descrizione|
|---|---|---|---|---|
|DCIApiCalls|Chiamate all'API di Customer Insights|Numero|Totale||
|DCIMappingImportOperationSuccessfulLines|Righe riuscite con l'operazione di importazione mapping|Numero|Totale||
|DCIMappingImportOperationFailedLines|Righe non riuscite con l'operazione di importazione mapping|Numero|Totale||
|DCIMappingImportOperationTotalLines|Righe totali dell'operazione di importazione mapping|Numero|Totale||
|DCIMappingImportOperationRuntimeInSeconds|Runtime dell'operazione di importazione mapping in secondi|Secondi|Totale||
|DCIOutboundProfileExportSucceeded|Esportazione profili in uscita riuscita|Numero|Totale||
|DCIOutboundProfileExportFailed|Esportazione profili in uscita non riuscita|Numero|Totale||
|DCIOutboundProfileExportDuration|Durata esportazione profili in uscita|Secondi|Totale||
|DCIOutboundKpiExportSucceeded|Esportazione di KPI in uscita riuscita|Numero|Totale||
|DCIOutboundKpiExportFailed|Esportazione di KPI in uscita non riuscita|Numero|Totale||
|DCIOutboundKpiExportDuration|Durata esportazione KPI in uscita|Secondi|Totale||
|DCIOutboundKpiExportStarted|Esportazione KPI in uscita avviata|Secondi|Totale||
|DCIOutboundKpiRecordCount|Numero di record KPI in uscita|Secondi|Totale||
|DCIOutboundProfileExportCount|Numero di esportazioni profili in uscita|Secondi|Totale||
|DCIOutboundInitialProfileExportFailed|Esportazione profili iniziali in uscita non riuscita|Secondi|Totale||
|DCIOutboundInitialProfileExportSucceeded|Esportazione profili iniziali in uscita riuscita|Secondi|Totale||
|DCIOutboundInitialKpiExportFailed|Esportazione KPI iniziali in uscita non riuscita|Secondi|Totale||
|DCIOutboundInitialKpiExportSucceeded|Esportazione KPI iniziali in uscita riuscita|Secondi|Totale||
|DCIOutboundInitialProfileExportDurationInSeconds|Durata esportazione profili iniziali in uscita in secondi|Secondi|Totale||
|AdlaJobForStandardKpiFailed|Processo Adla per Kpi standard non riuscito in secondi|Secondi|Totale||
|AdlaJobForStandardKpiTimeOut|Timeout processo Adla per Kpi standard in secondi|Secondi|Totale||
|AdlaJobForStandardKpiCompleted|Processo Adla per Kpi standard completato in secondi|Secondi|Totale||
|ImportASAValuesFailed|Numero importazioni valori ASA non riuscite|Numero|Totale||
|ImportASAValuesSucceeded|Numero importazioni valori ASA riuscite|Numero|Totale||

## <a name="microsoftdatalakeanalyticsaccounts"></a>Microsoft.DataLakeAnalytics/accounts

|Metrica|Nome visualizzato per la metrica|Unità|Tipo di aggregazione|Descrizione|
|---|---|---|---|---|
|JobEndedSuccess|Processi completati|Numero|Totale|Numero di processi completati|
|JobEndedFailure|Processi non riusciti|Numero|Totale|Numero di processi non riusciti|
|JobEndedCancelled|Processi annullati|Numero|Totale|Numero di processi annullati|
|JobAUEndedSuccess|Tempo di aggiornamenti automatici con esito positivo|Secondi|Totale|Tempo totale di aggiornamenti automatici per i processi completati|
|JobAUEndedFailure|Tempo di aggiornamenti automatici non riusciti|Secondi|Totale|Tempo totale di aggiornamenti automatici per processi non riusciti|
|JobAUEndedCancelled|Tempo di aggiornamenti automatici annullati|Secondi|Totale|Tempo totale di aggiornamenti automatici per processi annullati.|

## <a name="microsoftdbformysqlservers"></a>Microsoft.DBforMySQL/servers

|Metrica|Nome visualizzato per la metrica|Unità|Tipo di aggregazione|Descrizione|
|---|---|---|---|---|
|cpu_percent|Percentuale CPU|Percentuale|Media|Percentuale CPU|
|compute_limit|Limite unità di calcolo|Numero|Media|Limite unità di calcolo|
|compute_consumption_percent|Compute Unit percentage (Percentuale unità di calcolo)|Percentuale|Media|Percentuale unità di calcolo|
|memory_percent|Percentuale memoria|Percentuale|Media|Percentuale memoria|
|io_consumption_percent|IO percent (Percentuale IO)|Percentuale|Media|Percentuale IO|
|storage_percent|Percentuale archiviazione|Percentuale|Media|Percentuale archiviazione|
|storage_used|Uso archiviazione|Byte|Media|Uso archiviazione|
|storage_limit|Limite archiviazione|Byte|Media|Limite archiviazione|
|active_connections|Total active connections (Numero totale di connessioni attive)|Numero|Media|Numero totale di connessioni attive|
|connections_failed|Total failed connections (Numero totale di connessioni non riuscite)|Numero|Media|Numero totale di connessioni non riuscite|

## <a name="microsoftdbforpostgresqlservers"></a>Microsoft.DBforPostgreSQL/servers

|Metrica|Nome visualizzato per la metrica|Unità|Tipo di aggregazione|Descrizione|
|---|---|---|---|---|
|cpu_percent|Percentuale CPU|Percentuale|Media|Percentuale CPU|
|compute_limit|Limite unità di calcolo|Numero|Media|Limite unità di calcolo|
|compute_consumption_percent|Compute Unit percentage (Percentuale unità di calcolo)|Percentuale|Media|Percentuale unità di calcolo|
|memory_percent|Percentuale memoria|Percentuale|Media|Percentuale memoria|
|io_consumption_percent|IO percent (Percentuale IO)|Percentuale|Media|Percentuale IO|
|storage_percent|Percentuale archiviazione|Percentuale|Media|Percentuale archiviazione|
|storage_used|Uso archiviazione|Byte|Media|Uso archiviazione|
|storage_limit|Limite archiviazione|Byte|Media|Limite archiviazione|
|active_connections|Total active connections (Numero totale di connessioni attive)|Numero|Media|Numero totale di connessioni attive|
|connections_failed|Total failed connections (Numero totale di connessioni non riuscite)|Numero|Media|Numero totale di connessioni non riuscite|

## <a name="microsoftdevicesiothubs"></a>Microsoft.Devices/IotHubs

|Metrica|Nome visualizzato per la metrica|Unità|Tipo di aggregazione|Descrizione|
|---|---|---|---|---|
|d2c.telemetry.ingress.allProtocol|Tentativi di invio di messaggi di telemetria|Numero|Totale|Numero di tentativi toobe di telemetria da dispositivo a cloud messaggi inviati tooyour IoT hub|
|d2c.telemetry.ingress.success|Messaggi di telemetria inviati|Numero|Totale|Numero di messaggi da dispositivo a cloud telemetria inviato tooyour IoT hub|
|c2d.commands.egress.complete.success|Comandi completati|Numero|Totale|Numero di comandi cloud a dispositivo completata dal dispositivo hello|
|c2d.commands.egress.abandon.success|Comandi abbandonati|Numero|Totale|Numero di comandi cloud a dispositivo abbandonato da dispositivo hello|
|c2d.commands.egress.reject.success|Comandi rifiutati|Numero|Totale|Numero di comandi cloud a dispositivo rifiutato dal dispositivo hello|
|devices.totalDevices|Totale dispositivi|Numero|Totale|Numero di dispositivi registrati tooyour IoT hub|
|devices.connectedDevices.allProtocol|Dispositivi connessi|Numero|Totale|Numero di dispositivi connessi tooyour IoT hub|
|d2c.telemetry.egress.success|Messaggi telemetria recapitati|Numero|Totale|Numero di volte in cui i messaggi sono stati scritti correttamente tooendpoints (totale)|
|d2c.telemetry.egress.dropped|Messaggi rimossi|Numero|Totale|Numero di messaggi ignorati perché l'endpoint di recapito hello è obsoleto|
|d2c.telemetry.egress.orphaned|Messaggi orfani|Numero|Totale|numero di Hello dei messaggi non corrisponde alcuna route inclusi route fallback hello|
|d2c.telemetry.egress.invalid|Messaggi non validi|Numero|Totale|Hello conteggio dei messaggi non recapitati a causa di tooincompatibility con endpoint hello|
|d2c.telemetry.egress.fallback|Messaggi corrispondenti alla condizione di fallback|Numero|Totale|Numero di messaggi scritti toohello fallback endpoint|
|d2c.endpoints.egress.eventHubs|I messaggi recapitati tooEvent gli endpoint Hub|Numero|Totale|Numero di volte in cui i messaggi sono stati tooEvent scritto correttamente gli endpoint di Hub|
|d2c.endpoints.latency.eventHubs|Latenza messaggi per gli endpoint di Hub eventi|Millisecondi|Media|Latenza media tra l'hub IoT toohello di messaggio in ingresso e in ingresso messaggio Hello in un endpoint di Hub eventi, in millisecondi|
|d2c.endpoints.egress.serviceBusQueues|I messaggi recapitati tooService endpoint coda del Bus|Numero|Totale|Numero di volte in cui i messaggi sono stati tooService scritto correttamente gli endpoint di coda del Bus|
|d2c.endpoints.latency.serviceBusQueues|Latenza messaggi per gli endpoint della coda del bus di servizio|Millisecondi|Media|Latenza media tra l'hub IoT toohello di messaggio in ingresso e in ingresso messaggio Hello in un endpoint di coda di Service Bus, in millisecondi|
|d2c.endpoints.egress.serviceBusTopics|I messaggi recapitati tooService gli endpoint di argomento del Bus|Numero|Totale|Numero di volte in cui i messaggi sono stati tooService scritto correttamente gli endpoint di argomento del Bus|
|d2c.endpoints.latency.serviceBusTopics|Latenza messaggi per gli endpoint dell'argomento del bus di servizio|Millisecondi|Media|Latenza media tra l'hub IoT toohello di messaggio in ingresso e in ingresso messaggio Hello in un endpoint di argomento del Bus di servizio, in millisecondi|
|d2c.endpoints.egress.builtIn.events|I messaggi recapitati toohello endpoint predefinito (messaggi e gli eventi)|Numero|Totale|Numero di volte in cui i messaggi sono stati scritti correttamente toohello endpoint predefinito (messaggi e gli eventi)|
|d2c.endpoints.latency.builtIn.events|Latenza dei messaggi per l'endpoint predefinito hello (messaggi e gli eventi)|Millisecondi|Media|Latenza media tra l'hub IoT toohello di messaggio in ingresso e in ingresso messaggio Hello in endpoint predefinito hello (messaggi e gli eventi), in millisecondi |
|d2c.twin.read.success|Letture dei dispositivi gemelli completate dai dispositivi|Numero|Totale|conteggio di Hello di letture doppi avviato dal dispositivo tutte esito positivo.|
|d2c.twin.read.failure|Letture dei dispositivi gemelli non riuscite per i dispositivi|Numero|Totale|conteggio Hello di tutti i Impossibile letture doppi avviato dal dispositivo.|
|d2c.twin.read.size|Dimensioni delle risposte di letture dei dispositivi gemelli dai dispositivi|Byte|Media|Media di Hello, min e max di eseguite correttamente avviato dal dispositivo doppio letture.|
|d2c.twin.update.success|Aggiornamenti dei dispositivi gemelli completati dai dispositivi|Numero|Totale|conteggio di Hello degli aggiornamenti di un doppio avviato dal dispositivo tutte esito positivo.|
|d2c.twin.update.failure|Aggiornamenti dei dispositivi gemelli non riusciti per i dispositivi|Numero|Totale|numero di Hello di tutti di doppi avviato dal dispositivo aggiornamenti non riusciti.|
|d2c.twin.update.size|Dimensioni degli aggiornamenti dei dispositivi gemelli dai dispositivi|Byte|Media|Hello Media, min e dimensioni massime di eseguite correttamente avviato dal dispositivo doppio gli aggiornamenti.|
|c2d.methods.success|Chiamate a metodi diretti riuscite|Numero|Totale|conteggio di Hello di chiamate dirette del metodo eseguite correttamente.|
|c2d.methods.failure|Chiamate a metodi diretti non riuscite|Numero|Totale|conteggio Hello di tutti i Impossibile chiamate dirette del metodo.|
|c2d.methods.requestSize|Dimensioni delle richieste di chiamate a metodi diretti|Byte|Media|Hello Media, min e max di richieste dirette del metodo eseguite correttamente.|
|c2d.methods.responseSize|Dimensioni delle risposte a chiamate a metodi diretti|Byte|Media|Hello Media, min e max di tutte le risposte dirette del metodo ha esito positivo.|
|c2d.twin.read.success|Letture dei dispositivi gemelli completate dal back-end|Numero|Totale|conteggio di Hello di letture di back-end avviato doppi eseguite correttamente.|
|c2d.twin.read.failure|Letture dei dispositivi gemelli non riuscite per il back-end|Numero|Totale|conteggio Hello di tutti i Impossibile letture doppi avviato dal back-end.|
|c2d.twin.read.size|Dimensioni delle risposte di letture dei dispositivi gemelli dal back-end|Byte|Media|Media di Hello, min e max di eseguite correttamente back-end avviato doppio letture.|
|c2d.twin.update.success|Aggiornamenti dei dispositivi gemelli completati dal back-end|Numero|Totale|conteggio di Hello degli aggiornamenti di back-end avviato doppi eseguite correttamente.|
|c2d.twin.update.failure|Aggiornamenti dei dispositivi gemelli non riusciti per il back-end|Numero|Totale|numero Hello di tutti di back-end avviato doppi aggiornamenti non riusciti.|
|c2d.twin.update.size|Dimensioni degli aggiornamenti dei dispositivi gemelli dal back-end|Byte|Media|Hello Media, min e le dimensioni massime di tutte le back-end avviato doppio gli aggiornamenti.|
|twinQueries.success|Query dei dispositivi gemelli completate|Numero|Totale|conteggio di Hello di tutte le query doppi ha esito positivo.|
|twinQueries.failure|Query dei dispositivi gemelli non riuscite|Numero|Totale|conteggio di Hello di tutte le query doppi non riuscita.|
|twinQueries.resultSize|Dimensioni dei risultati delle query dei dispositivi gemelli|Byte|Media|Hello Media, min e max di dimensioni del risultato hello di tutte le query doppi ha esito positivo.|
|jobs.createTwinUpdateJob.success|Creazioni di processi di aggiornamento dei dispositivi gemelli completate|Numero|Totale|conteggio di Hello di tutti alla creazione di processi di aggiornamento di un doppio.|
|jobs.createTwinUpdateJob.failure|Creazioni di processi di aggiornamento dei dispositivi gemelli non riuscite|Numero|Totale|conteggio di Hello di tutti i creazione non riuscita dei processi di aggiornamento di un doppio.|
|jobs.createDirectMethodJob.success|Creazioni di processi di chiamata al metodo completate|Numero|Totale|conteggio di Hello di tutti alla creazione di processi di chiamate dirette del metodo.|
|jobs.createDirectMethodJob.failure|Creazioni di processi di chiamata al metodo non riuscite|Numero|Totale|conteggio di Hello di tutti i creazione non riuscita dei processi di chiamate dirette del metodo.|
|jobs.listJobs.success|Processi toolist chiamate con esito positivo|Numero|Totale|conteggio di Hello di tutti i processi di toolist chiamate con esito positivo.|
|jobs.listJobs.failure|Processi toolist chiamate non riuscite|Numero|Totale|conteggio di Hello di tutti i processi toolist di chiamate non riuscite.|
|jobs.cancelJob.success|Annullamenti di processi riusciti|Numero|Totale|conteggio Hello di tutte le chiamate toocancel un processo.|
|jobs.cancelJob.failure|Annullamenti di processi non riusciti|Numero|Totale|conteggio di Hello di tutte le chiamate non riuscite toocancel un processo.|
|jobs.queryJobs.success|Query sui processi riuscite|Numero|Totale|conteggio di Hello di tutti i processi di tooquery chiamate con esito positivo.|
|jobs.queryJobs.failure|Query sui processi non riuscite|Numero|Totale|conteggio di Hello di tutti i processi tooquery di chiamate non riuscite.|
|jobs.completed|Processi completati|Numero|Totale|conteggio di Hello di tutti i processi completati.|
|jobs.failed|Processi non riusciti|Numero|Totale|conteggio di Hello di tutti i processi non riusciti.|
|d2c.telemetry.ingress.sendThrottle|Number of throttling errors (Numero di errori di limitazione)|Numero|Totale|Numero di errori di limitazione a causa di limitazioni di velocità effettiva toodevice|
|dailyMessageQuotaUsed|Total number of messages used (Numero totale di messaggi usati)|Numero|Media|Numero totale di messaggi usati nella data odierna|

## <a name="microsofteventhubnamespaces"></a>Microsoft.EventHub/namespaces

|Metrica|Nome visualizzato per la metrica|Unità|Tipo di aggregazione|Descrizione|
|---|---|---|---|---|
|INREQS|Richieste di invio in ingresso|Numero|Totale|Totale richieste di invio in ingresso per un hub di notifica|
|SUCCREQ|Richieste riuscite|Numero|Totale|Richieste riuscite totali per uno spazio dei nomi|
|FAILREQ|Richieste non riuscite|Numero|Totale|Richieste non riuscite totali per uno spazio dei nomi|
|SVRBSY|Errori server occupato|Numero|Totale|Errori di server occupato totali per uno spazio dei nomi|
|INTERR|Errori interni server|Numero|Totale|Errori di server interni totali per uno spazio dei nomi|
|MISCERR|Altri errori|Numero|Totale|Richieste non riuscite totali per uno spazio dei nomi|
|INMSGS|Messaggi in ingresso|Numero|Totale|Messaggi in ingresso totali per uno spazio dei nomi|
|OUTMSGS|Messaggi in uscita|Numero|Totale|Messaggi in uscita totali per uno spazio dei nomi|
|EHINMBS|Byte in ingresso|Byte|Totale|Velocità effettiva dei messaggi in ingresso di Hub eventi per uno spazio dei nomi|
|EHOUTMBS|Byte in uscita|Byte|Totale|Messaggi in uscita totali per uno spazio dei nomi|
|EHABL|Messaggi backlog archiviati|Numero|Totale|Messaggi archiviati di Hub eventi nel backlog per uno spazio dei nomi|
|EHAMSGS|Messaggi archiviati|Numero|Totale|Messaggi archiviati di Hub eventi in uno spazio dei nomi|
|EHAMBS|Velocità effettiva messaggi archiviati|Byte|Totale|Velocità effettiva dei messaggi archiviati di Hub eventi in uno spazio dei nomi|

## <a name="microsoftlogicworkflows"></a>Microsoft.Logic/workflows

|Metrica|Nome visualizzato per la metrica|Unità|Tipo di aggregazione|Descrizione|
|---|---|---|---|---|
|RunsStarted|Esecuzioni avviate|Numero|Totale|Il numero di esecuzioni del flusso di lavoro avviate.|
|RunsCompleted|Esecuzioni completate|Numero|Totale|Il numero di esecuzioni del flusso di lavoro completate.|
|RunsSucceeded|Esecuzioni riuscite|Numero|Totale|Il numero di esecuzioni del flusso di lavoro riuscite.|
|RunsFailed|Esecuzioni non riuscite|Numero|Totale|Il numero di esecuzioni del flusso di lavoro non riuscite.|
|RunsCancelled|Esecuzioni annullate|Numero|Totale|Il numero di esecuzioni del flusso di lavoro annullate.|
|RunLatency|Latenza esecuzioni|Secondi|Media|La latenza delle esecuzioni del flusso di lavoro completate.|
|RunSuccessLatency|Latenza esecuzioni riuscite|Secondi|Media|La latenza delle esecuzioni del flusso di lavoro riuscite.|
|RunThrottledEvents|Eventi limitati esecuzione|Numero|Totale|Il numero di eventi limitati di trigger o azione del flusso di lavoro.|
|RunFailurePercentage|Percentuale di errori di esecuzione|Percentuale|Totale|Percentuale di esecuzioni del flusso di lavoro non riuscite.|
|ActionsStarted|Azioni avviate |Numero|Totale|Il numero di azioni del flusso di lavoro avviate.|
|ActionsCompleted|Azioni completate |Numero|Totale|Il numero di azioni del flusso di lavoro completate.|
|ActionsSucceeded|Azioni riuscite |Numero|Totale|Il numero di azioni del flusso di lavoro riuscite.|
|ActionsFailed|Azioni non riuscite|Numero|Totale|Il numero di azioni del flusso di lavoro non riuscite.|
|ActionsSkipped|Azioni ignorate |Numero|Totale|Il numero di azioni del flusso di lavoro ignorate.|
|ActionLatency|Latenza azioni |Secondi|Media|La latenza delle azioni del flusso di lavoro completate.|
|ActionSuccessLatency|Latenza azioni riuscite |Secondi|Media|La latenza delle azioni del flusso di lavoro riuscite.|
|ActionThrottledEvents|Eventi limitati azione|Numero|Totale|Il numero di eventi limitati di azione del flusso di lavoro.|
|TriggersStarted|Trigger avviati |Numero|Totale|Il numero di trigger del flusso di lavoro avviati.|
|TriggersCompleted|Trigger completati |Numero|Totale|Il numero di trigger del flusso di lavoro completati.|
|TriggersSucceeded|Trigger riusciti |Numero|Totale|Il numero di trigger del flusso di lavoro riusciti.|
|TriggersFailed|Trigger non riusciti |Numero|Totale|Il numero di trigger del flusso di lavoro non riusciti.|
|TriggersSkipped|Trigger ignorati|Numero|Totale|Il numero di trigger del flusso di lavoro ignorati.|
|TriggersFired|Trigger rimossi |Numero|Totale|Il numero di trigger del flusso di lavoro rimossi.|
|TriggerLatency|Latenza trigger |Secondi|Media|La latenza dei trigger del flusso di lavoro completati.|
|TriggerFireLatency|Latenza trigger rimossi |Secondi|Media|La latenza dei trigger del flusso di lavoro rimossi.|
|TriggerSuccessLatency|Latenza trigger riusciti |Secondi|Media|La latenza dei trigger del flusso di lavoro riusciti.|
|TriggerThrottledEvents|Eventi limitati trigger|Numero|Totale|Il numero di eventi limitati di trigger del flusso di lavoro.|
|BillableActionExecutions|Esecuzioni di azioni fatturabili|Conteggio|Totale|Numero di esecuzioni di azioni del flusso di lavoro fatturate.|
|BillableTriggerExecutions|Esecuzioni di trigger fatturabili|Conteggio|Totale|Numero di esecuzioni di trigger del flusso di lavoro fatturate.|
|TotalBillableExecutions|Esecuzioni fatturabili totali|Conteggio|Totale|Numero di esecuzioni di flussi di lavoro fatturate.|

## <a name="microsoftnetworkapplicationgateways"></a>Microsoft.Network/applicationGateways

|Metrica|Nome visualizzato per la metrica|Unità|Tipo di aggregazione|Descrizione|
|---|---|---|---|---|
|Throughput|Velocità effettiva|Byte al secondo|Media||

## <a name="microsoftnetworkexpressroutecircuits"></a>Microsoft.Network/expressRouteCircuits

|Metrica|Nome visualizzato per la metrica|Unità|Tipo di aggregazione|Descrizione|
|---|---|---|---|---|
|BytesIn|BytesIn|Numero|Totale||
|BytesOut|BytesOut|Numero|Totale||

## <a name="microsoftnotificationhubsnamespacesnotificationhubs"></a>Microsoft.NotificationHubs/Namespaces/NotificationHubs

|Metrica|Nome visualizzato per la metrica|Unità|Tipo di aggregazione|Descrizione|
|---|---|---|---|---|
|registration.all|Operazione di registrazione|Numero|Totale|conteggio di Hello di tutte le operazioni di registrazione corretta (query di creazione degli aggiornamenti ed eliminazioni). |
|registration.create|Operazioni di creazione registrazione|Numero|Totale|conteggio di Hello di tutte le operazioni di creazione di registrazione ha esito positivo.|
|registration.update|Operazioni di aggiornamento registrazione|Numero|Totale|conteggio di Hello di tutti gli aggiornamenti di registrazione ha esito positivo.|
|registration.get|Operazioni di lettura registrazione|Numero|Totale|conteggio di Hello di tutte le query di registrazione ha esito positivo.|
|registration.delete|Operazioni di eliminazione registrazione|Numero|Totale|conteggio di Hello di tutte le eliminazioni di dopo la corretta registrazione.|
|incoming|Messaggi in ingresso|Numero|Totale|conteggio Hello di tutte le chiamate API di trasmissione. |
|incoming.scheduled|Notifiche push pianificate inviate|Numero|Totale|Notifiche push pianificate annullate|
|incoming.scheduled.cancel|Notifiche push pianificate annullate|Numero|Totale|Notifiche push pianificate annullate|
|scheduled.pending|Notifiche pianificate in sospeso|Numero|Totale|Notifiche pianificate in sospeso|
|installation.all|Operazioni di gestione installazione|Numero|Totale|Operazioni di gestione installazione|
|installation.get|Ottieni operazioni di installazione|Numero|Totale|Ottieni operazioni di installazione|
|installation.upsert|Crea o aggiorna operazioni di installazione|Numero|Totale|Crea o aggiorna operazioni di installazione|
|installation.patch|Operazioni di installazione patch|Numero|Totale|Operazioni di installazione patch|
|installation.delete|Elimina operazioni di installazione|Numero|Totale|Elimina operazioni di installazione|
|outgoing.allpns.success|Notifiche riuscite|Numero|Totale|conteggio di Hello di tutte le notifiche di esito positivo.|
|outgoing.allpns.invalidpayload|Errori payload|Numero|Totale|conteggio di Hello di push non riuscita perché hello PNS ha restituito un errore di payload non valido.|
|outgoing.allpns.pnserror|Errori sistema di notifica esterno|Numero|Totale|conteggio di Hello di push che non è riuscita perché si è verificato un problema di comunicazione con hello PNS (esclusi i problemi di autenticazione).|
|outgoing.allpns.channelerror|Errori canale|Numero|Totale|conteggio Hello di inserimenti che non è riuscita perché il canale di hello non valido non associato hello corretto app limitate o scaduto.|
|outgoing.allpns.badorexpiredchannel|Errori canale non valido o scaduto|Numero|Totale|conteggio Hello di push non riuscita perché hello canale/token/registrationId nella registrazione hello è scaduto o non valido.|
|outgoing.wns.success|Notifiche WNS completate|Numero|Totale|conteggio di Hello di tutte le notifiche di esito positivo.|
|outgoing.wns.invalidcredentials|Errori di autorizzazione WNS (credenziali non valide)|Numero|Totale|conteggio Hello di inserimenti che non è riuscita perché non ha accettato hello PNS hello fornito le credenziali o credenziali hello sono bloccate. (Windows Live non riconosce le credenziali di hello).|
|outgoing.wns.badchannel|Errore canale WNS non valido|Numero|Totale|numero di inserimenti che non è riuscita perché non è stato riconosciuto hello ChannelURI nella registrazione hello Hello (stato WNS: 404 non trovato).|
|outgoing.wns.expiredchannel|Errore canale WNS scaduto|Numero|Totale|numero di inserimenti che non è riuscita perché hello URI di canale scaduto Hello (stato WNS: 410 Gone).|
|outgoing.wns.throttled|Notifiche WNS limitate|Numero|Totale|numero di inserimenti che non è riuscita perché WNS è la limitazione di questa applicazione Hello (stato WNS: 406-pagina non valida).|
|outgoing.wns.tokenproviderunreachable|Errori di autorizzazione WNS (non disponibile)|Numero|Totale|Windows Live non è raggiungibile.|
|outgoing.wns.invalidtoken|Errori di autorizzazione WNS (token non valido)|Numero|Totale|Hello token fornito tooWNS non è valido (stato WNS: 401 non autorizzato).|
|outgoing.wns.wrongtoken|Errori di autorizzazione WNS (token errato)|Numero|Totale|Hello token fornito tooWNS è valido, ma per un'altra applicazione (stato WNS: 403-accesso negato). Questa situazione può verificarsi se hello ChannelURI nella registrazione hello è associata a un'altra app. Verificare che app client hello è associata a hello stessa app le cui credenziali vengono nell'hub di notifica hello.|
|outgoing.wns.invalidnotificationformat|Formato notifica WNS non valido|Numero|Totale|formato Hello della notifica hello non è valido (stato WNS: 400). Si noti che WNS non rifiuta tutti i payload non validi.|
|outgoing.wns.invalidnotificationsize|Errore dimensioni notifica WNS non valide|Numero|Totale|il payload di notifica Hello è troppo grande (stato WNS: 413).|
|outgoing.wns.channelthrottled|Canale WNS limitato|Numero|Totale|notifica Hello è stata eliminata poiché hello ChannelURI nella registrazione hello è limitata (intestazione della risposta WNS: X-WNS-NotificationStatus:channelThrottled).|
|outgoing.wns.channeldisconnected|Canale WNS disconnesso|Numero|Totale|notifica Hello è stata eliminata poiché hello ChannelURI nella registrazione hello è limitata (intestazione della risposta WNS: X-WNS-DeviceConnectionStatus: disconnesso).|
|outgoing.wns.dropped|Notifiche WNS eliminate|Numero|Totale|notifica Hello è stata eliminata poiché hello ChannelURI nella registrazione hello è limitata (X-WNS-NotificationStatus: eliminato ma non X-WNS-DeviceConnectionStatus: disconnesso).|
|outgoing.wns.pnserror|Errori WNS|Numero|Totale|La notifica non è stata recapitata a causa di errori di comunicazione con WNS.|
|outgoing.wns.authenticationerror|Errori di autenticazione WNS|Numero|Totale|La notifica non è stata recapitata a causa di errori di comunicazione con Windows Live, di credenziali non valide o di token non corretto.|
|outgoing.apns.success|Notifiche APNS completate|Numero|Totale|conteggio di Hello di tutte le notifiche di esito positivo.|
|outgoing.apns.invalidcredentials|Errori di autorizzazione del servizio APN|Numero|Totale|conteggio Hello di inserimenti che non è riuscita perché non ha accettato hello PNS hello fornito le credenziali o credenziali hello sono bloccate.|
|outgoing.apns.badchannel|Errore canale APNS non valido|Numero|Totale|numero di inserimenti che non è riuscita perché non è valido il token hello Hello (codice di stato servizio APN: 8).|
|outgoing.apns.expiredchannel|Errore canale APNS scaduto|Numero|Totale|conteggio di Hello del token che sono stati invalidati dal canale di feedback APNS hello.|
|outgoing.apns.invalidnotificationsize|Errore dimensioni notifica APNS non valide|Numero|Totale|numero di inserimenti che non è riuscita perché è troppo grande payload hello Hello (codice di stato servizio APN: 7).|
|outgoing.apns.pnserror|Errori APNS|Numero|Totale|conteggio Hello di push non riuscita a causa di errori di comunicazione con il servizio APN.|
|outgoing.gcm.success|Notifiche GCM completate|Numero|Totale|conteggio di Hello di tutte le notifiche di esito positivo.|
|outgoing.gcm.invalidcredentials|Errori di autorizzazione GCM (credenziali non valide)|Numero|Totale|conteggio Hello di inserimenti che non è riuscita perché non ha accettato hello PNS hello fornito le credenziali o credenziali hello sono bloccate.|
|outgoing.gcm.badchannel|Errore canale GCM non valido|Numero|Totale|numero di inserimenti che non è riuscita perché non è stato riconosciuto registrationId hello nella registrazione hello Hello (risultato GCM: registrazione non valida).|
|outgoing.gcm.expiredchannel|Errore canale GCM scaduto|Numero|Totale|numero di inserimenti che non è riuscita perché è scaduto registrationId hello nella registrazione hello Hello (risultato GCM: non registrato).|
|outgoing.gcm.throttled|Notifiche GCM limitate|Numero|Totale|numero di inserimenti che non è riuscita perché l'app limitate GCM Hello (codice di stato GCM: 501-599 o risultato: non disponibile).|
|outgoing.gcm.invalidnotificationformat|Formato notifiche GCM non valido|Numero|Totale|numero di inserimenti che non è riuscita perché non è stato correttamente formattato payload hello Hello (risultato GCM: InvalidDataKey o InvalidTtl).|
|outgoing.gcm.invalidnotificationsize|Errore dimensioni notifica GCM non valide|Numero|Totale|numero di inserimenti che non è riuscita perché è troppo grande payload hello Hello (risultato GCM: MessageTooBig).|
|outgoing.gcm.wrongchannel|Errore canale GCM errato|Numero|Totale|conteggio Hello di push non riuscita perché non è registrationId hello nella registrazione hello associata app corrente toohello (risultato GCM: InvalidPackageName).|
|outgoing.gcm.pnserror|Errori GCM|Numero|Totale|conteggio Hello di push non riuscita a causa di errori di comunicazione con GCM.|
|outgoing.gcm.authenticationerror|Errori di autenticazione GCM|Numero|Totale|numero di inserimenti che non è riuscita perché hello PNS non ha accettato hello fornito le credenziali di hello le credenziali sono bloccate o hello SenderId non è configurata correttamente in app hello Hello (risultato GCM: MismatchedSenderId).|
|outgoing.mpns.success|Notifiche MPNS completate|Numero|Totale|conteggio di Hello di tutte le notifiche di esito positivo.|
|outgoing.mpns.invalidcredentials|Credenziali MPNS non valide|Numero|Totale|conteggio Hello di inserimenti che non è riuscita perché non ha accettato hello PNS hello fornito le credenziali o credenziali hello sono bloccate.|
|outgoing.mpns.badchannel|Errori canale MPNS errato|Numero|Totale|numero di inserimenti che non è riuscita perché non è stato riconosciuto hello ChannelURI nella registrazione hello Hello (stato MPNS: 404 non trovato).|
|outgoing.mpns.throttled|Notifiche MPNS limitate|Numero|Totale|numero di inserimenti che non è riuscita perché MPNS è la limitazione di questa applicazione Hello (WNS MPNS: 406-pagina non valida).|
|outgoing.mpns.invalidnotificationformat|Formato notifiche MPNS non valido|Numero|Totale|conteggio Hello di push non riuscita perché il payload di hello della notifica hello è troppo grande.|
|outgoing.mpns.channeldisconnected|Canale MPNS disconnesso|Numero|Totale|numero di inserimenti che non è riuscita perché è stata disconnessa hello ChannelURI nella registrazione hello Hello (stato MPNS: 412 non trovato).|
|outgoing.mpns.dropped|Notifiche MPNS eliminate|Numero|Totale|numero di inserimenti che sono state eliminate da MPNS Hello (intestazione della risposta MPNS: X NotificationStatus: QueueFull o soppressi).|
|outgoing.mpns.pnserror|Errori MPNS|Numero|Totale|conteggio Hello di push non riuscita a causa di errori di comunicazione con MPNS.|
|outgoing.mpns.authenticationerror|Errori di autenticazione MPNS|Numero|Totale|conteggio Hello di inserimenti che non è riuscita perché non ha accettato hello PNS hello fornito le credenziali o credenziali hello sono bloccate.|
|notificationhub.pushes|Tutte le notifiche in uscita|Numero|Totale|Tutte le comunicazioni in uscita dell'hub di notifica hello|
|incoming.all.requests|Tutte le richieste in ingresso|Numero|Totale|Totale richieste in ingresso per un hub di notifica|
|incoming.all.failedrequests|Tutte le richieste in ingresso non riuscite|Numero|Totale|Totale richieste in ingresso non riuscite per un hub di notifica|

## <a name="microsoftpowerbidedicatedcapacities"></a>Microsoft.PowerBIDedicated/capacities

|Metrica|Nome visualizzato per la metrica|Unità|Tipo di aggregazione|Descrizione|
|---|---|---|---|---|
|qpu_metric|QPU|Numero|Media|QPU. Intervallo 0-100 per S1, 0-200 per S2 e 0-400 per S4|
|memory_metric|Memoria|Byte|Media|Memoria. Intervallo 0-25 GB per S1, 0-50 GB per S2 e 0-100 GB per S4|
|TotalConnectionRequests|Numero totale di richieste di connessione|Numero|Media|Numero totale delle richieste di connessione in arrivo.|
|SuccessfullConnectionsPerSec|Connessioni riuscite al secondo|Conteggio al secondo|Media|Numero delle connessioni completate correttamente al secondo.|
|TotalConnectionFailures|Numero totale di errori di connessione|Numero|Media|Numero totale dei tentativi di connessione non riusciti.|
|CurrentUserSessions|Sessioni utente correnti|Numero|Media|Numero corrente di sessioni utente attive.|
|QueryPoolBusyThreads|Thread occupati pool di query|Numero|Media|Numero dei thread occupati nel pool di thread di query hello.|
|CommandPoolJobQueueLength|Lunghezza coda processi nel pool di comandi|Numero|Media|Numero di processi in coda hello hello comando del pool dei thread.|
|ProcessingPoolJobQueueLength|Lunghezza coda processi nel pool di elaborazione|Numero|Media|Numero di processi non dei / O nella coda di hello di hello pool di thread di elaborazione.|
|CurrentConnections|Connessione: connessioni correnti|Numero|Media|Numero corrente delle connessioni client stabilite.|
|CleanerCurrentPrice|Memoria: prezzo corrente pulitura memoria|Numero|Media|Prezzo corrente di memoria, $/ byte/ora, too1000 normalizzato.|
|CleanerMemoryShrinkable|Memoria: pulitura memoria compattabile|Byte|Media|Quantità di memoria, in byte, soggetto toopurging dallo sfondo hello più chiara.|
|CleanerMemoryNonshrinkable|Memoria: pulitura memoria non compattabile|Byte|Media|Quantità di memoria, in byte, non soggetto toopurging dallo sfondo hello più chiara.|
|MemoryUsage|Memoria: utilizzo memoria|Byte|Media|Utilizzo della memoria di hello processo server utilizzato per il calcolo del prezzo di memoria più pulita. Uguale a toocounter Process\PrivateBytes più hello di dati con mapping in memoria, ignorando la memoria è stato eseguito il mapping o allocazione dal motore in memoria analitica hello xVelocity (VertiPaq) che superano il motore xVelocity hello limite di memoria.|
|MemoryLimitHard|Memoria: limite memoria assoluto|Byte|Media|Limite assoluto della memoria, dal file di configurazione.|
|MemoryLimitHigh|Memoria: limite memoria massimo|Byte|Media|Limite superiore della memoria, dal file di configurazione.|
|MemoryLimitLow|Memoria: limite memoria minimo|Byte|Media|Limite inferiore della memoria, dal file di configurazione.|
|MemoryLimitVertiPaq|Memoria: limite memoria VertiPaq|Byte|Media|Limite in memoria dal file di configurazione.|
|Quota|Memoria: quota|Byte|Media|Quota di memoria corrente, in byte. Le quote di memoria sono note anche come concessioni di memoria o prenotazioni di memoria.|
|QuotaBlocked|Memoria: Richieste di quota bloccate|Numero|Media|Numero corrente di richieste di quota bloccate fino a quando non vengono liberate altre quote di memoria.|
|VertiPaqNonpaged|Memoria: VertiPaq non di paging|Byte|Media|Byte di memoria bloccata nel hello working set per l'utilizzo dal motore in memoria hello.|
|VertiPaqPaged|Memoria: VertiPaq di paging|Byte|Media|Byte di memoria di paging in uso per i dati in memoria.|
|RowsReadPerSec|Elaborazione: righe lette al secondo|Conteggio al secondo|Media|Velocità di lettura delle righe da tutti i database relazionali.|
|RowsConvertedPerSec|Elaborazione: righe convertite al secondo|Conteggio al secondo|Media|Velocità di conversione delle righe durante l'elaborazione.|
|RowsWrittenPerSec|Elaborazione: righe scritte al secondo|Conteggio al secondo|Media|Velocità di scrittura delle righe durante l'elaborazione.|
|CommandPoolBusyThreads|Thread: thread occupati nel pool di comandi|Numero|Media|Numero dei thread occupati nel pool di thread comando hello.|
|CommandPoolIdleThreads|Thread: Thread inattivi pool di comandi|Numero|Media|Numero di thread inattivi nel pool di thread comando hello.|
|LongParsingBusyThreads|Thread: thread occupati per analisi dei thread lunghi|Numero|Media|Numero dei thread occupati nel pool di thread analisi dei thread lunghi hello.|
|LongParsingIdleThreads|Thread: Thread inattivi per analisi dei thread lunghi|Numero|Media|Numero di thread inattivi nel pool di thread analisi dei thread lunghi hello.|
|LongParsingJobQueueLength|Thread: lunghezza coda processi di analisi dei thread lunghi|Numero|Media|Numero di processi in coda hello di hello analisi dei thread lunghi pool di thread.|
|ProcessingPoolBusyIOJobThreads|Thread: thread di processi di I/O occupati nel pool di elaborazione|Numero|Media|Numero di thread che eseguono processi dei / o nel pool di thread di elaborazione hello.|
|ProcessingPoolBusyNonIOThreads|Thread: Thread non di I/O occupati nel pool di elaborazione|Numero|Media|Numero di thread che eseguono processi non dei / O nel pool di thread di elaborazione hello.|
|ProcessingPoolIOJobQueueLength|Thread: lunghezza coda processi di I/O nel pool di elaborazione|Numero|Media|Numero di processi dei / o in coda hello di hello pool di thread di elaborazione.|
|ProcessingPoolIdleIOJobThreads|Thread: thread di processi di I/O inattivi nel pool di elaborazione|Numero|Media|Numero di thread inattivi per i processi nel pool di thread di elaborazione hello.|
|ProcessingPoolIdleNonIOThreads|Thread: thread non di I/O inattivi nel pool di elaborazione|Numero|Media|Numero di thread inattivi nel pool di thread di elaborazione hello dedicato toonon processi dei / O.|
|QueryPoolIdleThreads|Thread: thread inattivi nel pool di query|Numero|Media|Numero di thread inattivi per i processi nel pool di thread di elaborazione hello.|
|QueryPoolJobQueueLength|Thread: lunghezza coda processi nel pool di query|Numero|Media|Numero di processi in coda hello del pool di thread di query hello.|
|ShortParsingBusyThreads|Thread: thread occupati per analisi dei thread brevi|Numero|Media|Numero dei thread occupati nel hello breve l'analisi di pool di thread.|
|ShortParsingIdleThreads|Thread: thread inattivi per analisi dei thread brevi|Numero|Media|Numero di thread inattivi nel hello breve l'analisi di pool di thread.|
|ShortParsingJobQueueLength|Thread: lunghezza coda processi di analisi dei thread brevi|Numero|Media|Numero di processi in coda hello di hello breve l'analisi di pool di thread.|
|memory_thrashing_metric|Thrashing di memoria|Percentuale|Media|Thrashing di memoria medio.|

## <a name="microsoftsearchsearchservices"></a>Microsoft.Search/searchServices

|Metrica|Nome visualizzato per la metrica|Unità|Tipo di aggregazione|Descrizione|
|---|---|---|---|---|
|SearchLatency|Latenza ricerca|Secondi|Media|Latenza media di ricerca per il servizio di ricerca hello|
|SearchQueriesPerSecond|Query di ricerca al secondo|Conteggio al secondo|Media|Query di ricerca al secondo per il servizio di ricerca hello|
|ThrottledSearchQueriesPercentage|Percentuale query di ricerca limitate|Percentuale|Media|Percentuale di query di ricerca che sono state limitate per il servizio di ricerca hello|

## <a name="microsoftservicebusnamespaces"></a>Microsoft.ServiceBus/namespaces

|Metrica|Nome visualizzato per la metrica|Unità|Tipo di aggregazione|Descrizione|
|---|---|---|---|---|
|CPUXNS|Uso della CPU per spazio dei nomi|Percentuale|Massima|Metrica di utilizzo CPU per spazio dei nomi Premium del bus di servizio|
|WSXNS|Uso delle dimensioni della memoria per spazio dei nomi|Percentuale|Massima|Metrica di utilizzo memoria per spazio dei nomi Premium del bus di servizio|

## <a name="microsoftsqlserversdatabases"></a>Microsoft.Sql/servers/databases

|Metrica|Nome visualizzato per la metrica|Unità|Tipo di aggregazione|Descrizione|
|---|---|---|---|---|
|cpu_percent|Percentuale CPU|Percentuale|Media|Percentuale CPU|
|physical_data_read_percent|Percentuale di I/O di dati|Percentuale|Media|Percentuale di I/O di dati|
|log_write_percent|Percentuale I/O registro|Percentuale|Media|Percentuale I/O registro|
|dtu_consumption_percent|Percentuale di DTU|Percentuale|Media|Percentuale di DTU|
|storage|Dimensioni totali database|Byte|Massima|Dimensioni totali database|
|connection_successful|Connessioni riuscite|Numero|Totale|Connessioni riuscite|
|connection_failed|Connessioni non riuscite|Numero|Totale|Connessioni non riuscite|
|blocked_by_firewall|Blocco da parte del firewall|Numero|Totale|Blocco da parte del firewall|
|deadlock|Deadlock|Numero|Totale|Deadlock|
|storage_percent|Percentuale di dimensioni del database|Percentuale|Massima|Percentuale di dimensioni del database|
|xtp_storage_percent|Percentuale di archiviazione OLTP in memoria|Percentuale|Media|Percentuale di archiviazione OLTP in memoria|
|workers_percent|Percentuale ruoli di lavoro|Percentuale|Media|Percentuale ruoli di lavoro|
|sessions_percent|Percentuale sessioni|Percentuale|Media|Percentuale sessioni|
|dtu_limit|Limite DTU|Numero|Media|Limite DTU|
|dtu_used|Uso DTU|Conteggio|Media|Uso DTU|
|dwu_limit|Limite DWU|Numero|Massima|Limite DWU|
|dwu_consumption_percent|Percentuale DWU|Percentuale|Massima|Percentuale DWU|
|dwu_used|Uso DWU|Numero|Massima|Uso DWU|

## <a name="microsoftsqlserverselasticpools"></a>Microsoft.Sql/servers/elasticPools

|Metrica|Nome visualizzato per la metrica|Unità|Tipo di aggregazione|Descrizione|
|---|---|---|---|---|
|cpu_percent|Percentuale CPU|Percentuale|Media|Percentuale CPU|
|database_cpu_percent|Percentuale CPU|Percentuale|Media|Percentuale CPU|
|physical_data_read_percent|Percentuale di I/O di dati|Percentuale|Media|Percentuale di I/O di dati|
|database_physical_data_read_percent|Percentuale di I/O di dati|Percentuale|Media|Percentuale di I/O di dati|
|log_write_percent|Percentuale I/O registro|Percentuale|Media|Percentuale I/O registro|
|database_log_write_percent|Percentuale I/O registro|Percentuale|Media|Percentuale I/O registro|
|dtu_consumption_percent|Percentuale di DTU|Percentuale|Media|Percentuale di DTU|
|database_dtu_consumption_percent|Percentuale di DTU|Percentuale|Media|Percentuale di DTU|
|storage_percent|Percentuale archiviazione|Percentuale|Media|Percentuale archiviazione|
|workers_percent|Percentuale ruoli di lavoro|Percentuale|Media|Percentuale ruoli di lavoro|
|database_workers_percent|Percentuale ruoli di lavoro|Percentuale|Media|Percentuale ruoli di lavoro|
|sessions_percent|Percentuale sessioni|Percentuale|Media|Percentuale sessioni|
|database_sessions_percent|Percentuale sessioni|Percentuale|Media|Percentuale sessioni|
|eDTU_limit|Limite eDTU|Conteggio|Media|Limite eDTU|
|storage_limit|Limite archiviazione|Byte|Media|Limite archiviazione|
|eDTU_used|Uso eDTU|Conteggio|Media|Uso eDTU|
|storage_used|Uso archiviazione|Byte|Media|Uso archiviazione|
|database_storage_used|Uso archiviazione|Byte|Media|Uso archiviazione|
|xtp_storage_percent|Percentuale di archiviazione OLTP in memoria|Percentuale|Media|Percentuale di archiviazione OLTP in memoria|

## <a name="microsoftsqlservers"></a>Microsoft.Sql/servers

|Metrica|Nome visualizzato per la metrica|Unità|Tipo di aggregazione|Descrizione|
|---|---|---|---|---|
|dtu_consumption_percent|Percentuale di DTU|Percentuale|Media|Percentuale di DTU|
|database_dtu_consumption_percent|Percentuale di DTU|Percentuale|Media|Percentuale di DTU|
|storage_used|Uso archiviazione|Byte|Media|Uso archiviazione|
|database_storage_used|Uso archiviazione|Byte|Media|Uso archiviazione|

## <a name="microsoftstreamanalyticsstreamingjobs"></a>Microsoft.StreamAnalytics/streamingjobs

|Metrica|Nome visualizzato per la metrica|Unità|Tipo di aggregazione|Descrizione|
|---|---|---|---|---|
|ResourceUtilization|% utilizzo unità di streaming|Percentuale|Massima|% utilizzo unità di streaming|
|InputEvents|Eventi di input|Conteggio|Totale|Eventi di input|
|InputEventBytes|Byte evento di input|Byte|Totale|Byte evento di input|
|LateInputEvents|Ultimi eventi di input|Conteggio|Totale|Ultimi eventi di input|
|OutputEvents|Eventi di output|Conteggio|Totale|Eventi di output|
|ConversionErrors|Errori di conversione dati|Conteggio|Totale|Errori di conversione dati|
|Errors|Errori di runtime|Conteggio|Totale|Errori di runtime|
|DroppedOrAdjustedEvents|Eventi non in ordine|Conteggio|Totale|Eventi non in ordine|
|AMLCalloutRequests|Richieste di funzioni|Conteggio|Totale|Richieste di funzioni|
|AMLCalloutFailedRequests|Richieste di funzioni non riuscite|Conteggio|Totale|Richieste di funzioni non riuscite|
|AMLCalloutInputEvents|Eventi di funzioni|Conteggio|Totale|Eventi di funzioni|

## <a name="microsoftwebserverfarms"></a>Microsoft.Web/serverfarms

|Metrica|Nome visualizzato per la metrica|Unità|Tipo di aggregazione|Descrizione|
|---|---|---|---|---|
|CpuPercentage|Percentuale CPU|Percentuale|Media|Percentuale CPU|
|MemoryPercentage|Percentuale memoria|Percentuale|Media|Percentuale memoria|
|DiskQueueLength|Lunghezza coda disco|Numero|Totale|Lunghezza coda disco|
|HttpQueueLength|Lunghezza coda HTTP|Numero|Totale|Lunghezza coda HTTP|
|BytesReceived|Dati in entrata|Byte|Totale|Dati in entrata|
|BytesSent|Dati in uscita|Byte|Totale|Dati in uscita|

## <a name="microsoftwebsites-excluding-functions"></a>Microsoft.Web/sites (escluse le funzioni)

|Metrica|Nome visualizzato per la metrica|Unità|Tipo di aggregazione|Descrizione|
|---|---|---|---|---|
|CpuTime|Tempo CPU|Secondi|Totale|Tempo CPU|
|Requests|Richieste|Numero|Totale|Richieste|
|BytesReceived|Dati in entrata|Byte|Totale|Dati in entrata|
|BytesSent|Dati in uscita|Byte|Totale|Dati in uscita|
|Http101|Http 101|Numero|Totale|Http 101|
|Http2xx|Http 2xx|Numero|Totale|Http 2xx|
|Http3xx|Http 3xx|Numero|Totale|Http 3xx|
|Http401|Http 401|Numero|Totale|Http 401|
|Http403|Http 403|Numero|Totale|Http 403|
|Http404|Http 404|Numero|Totale|Http 404|
|Http406|Http 406|Numero|Totale|Http 406|
|Http4xx|Http 4xx|Numero|Totale|Http 4xx|
|Http5xx|Errori server HTTP|Numero|Totale|Errori server HTTP|
|MemoryWorkingSet|Working set della memoria|Byte|Media|Working set della memoria|
|AverageMemoryWorkingSet|Working set della memoria medio|Byte|Media|Working set della memoria medio|
|AverageResponseTime|Tempo medio di risposta|Secondi|Media|Tempo medio di risposta|

## <a name="microsoftwebsites-functions"></a>Microsoft.Web/sites (funzioni)

|Metrica|Nome visualizzato per la metrica|Unità|Tipo di aggregazione|Descrizione|
|---|---|---|---|---|
|BytesReceived|Dati in entrata|Byte|Totale|Dati in entrata|
|BytesSent|Dati in uscita|Byte|Totale|Dati in uscita|
|Http5xx|Errori server HTTP|Numero|Totale|Errori server HTTP|
|MemoryWorkingSet|Working set della memoria|Byte|Media|Working set della memoria|
|AverageMemoryWorkingSet|Working set della memoria medio|Byte|Media|Working set della memoria medio|
|FunctionExecutionUnits|Unità di esecuzione della funzione|Numero|Media|Unità di esecuzione della funzione|
|FunctionExecutionCount|Conteggio delle esecuzioni della funzione|Numero|Media|Conteggio delle esecuzioni della funzione|

## <a name="microsoftwebsitesslots"></a>Microsoft.Web/sites/slots

|Metrica|Nome visualizzato per la metrica|Unità|Tipo di aggregazione|Descrizione|
|---|---|---|---|---|
|CpuTime|Tempo CPU|Secondi|Totale|Tempo CPU|
|Requests|Richieste|Numero|Totale|Richieste|
|BytesReceived|Dati in entrata|Byte|Totale|Dati in entrata|
|BytesSent|Dati in uscita|Byte|Totale|Dati in uscita|
|Http101|Http 101|Numero|Totale|Http 101|
|Http2xx|Http 2xx|Numero|Totale|Http 2xx|
|Http3xx|Http 3xx|Numero|Totale|Http 3xx|
|Http401|Http 401|Numero|Totale|Http 401|
|Http403|Http 403|Numero|Totale|Http 403|
|Http404|Http 404|Numero|Totale|Http 404|
|Http406|Http 406|Numero|Totale|Http 406|
|Http4xx|Http 4xx|Numero|Totale|Http 4xx|
|Http5xx|Errori server HTTP|Numero|Totale|Errori server HTTP|
|MemoryWorkingSet|Working set della memoria|Byte|Media|Working set della memoria|
|AverageMemoryWorkingSet|Working set della memoria medio|Byte|Media|Working set della memoria medio|
|AverageResponseTime|Tempo medio di risposta|Secondi|Media|Tempo medio di risposta|
|FunctionExecutionUnits|Unità di esecuzione della funzione|Numero|Media|Unità di esecuzione della funzione|
|FunctionExecutionCount|Conteggio delle esecuzioni della funzione|Numero|Media|Conteggio delle esecuzioni della funzione|

## <a name="next-steps"></a>Passaggi successivi
* [Metriche in Monitoraggio di Azure](monitoring-overview-metrics.md)
* [Create alerts on metrics](insights-receive-alert-notifications.md)
* [Esportare le metriche toostorage, Hub eventi o Log Analitica](monitoring-overview-of-diagnostic-logs.md)
