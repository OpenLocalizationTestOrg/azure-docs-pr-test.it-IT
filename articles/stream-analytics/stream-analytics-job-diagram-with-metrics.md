---
title: aaa Analitica di flusso di Azure basate sui dati debug tramite il diagramma di processo hello | Documenti Microsoft
description: Risoluzione dei problemi con il processo di flusso Analitica metriche e Diagramma processo hello.
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 05/01/2017
ms.author: jeffstok
ms.openlocfilehash: 1af884d485bebb06b034da01a13f7f8240516571
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="data-driven-debugging-by-using-hello-job-diagram"></a>Il debug con il diagramma di processo hello guidate dai dati

diagramma di processo Hello su hello **monitoraggio** pannello nel portale di Azure hello consentono di visualizzare la pipeline di processo. Mostra gli input, gli output e i passaggi delle query. È possibile usare le metriche hello di hello processo diagramma tooexamine per ogni passaggio, toomore isolare rapidamente origine hello di un problema durante la risoluzione dei problemi.

## <a name="using-hello-job-diagram"></a>Utilizzando il diagramma di processo hello

Nel portale di Azure hello mentre in un processo di flusso Analitica, in **supporto + risoluzione dei problemi**selezionare **Diagramma processo**:

![Diagramma di processo con metriche - posizione](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-1.png)

Selezionare ogni sezione corrispondente di hello toosee query passaggio in un riquadro di modifica di query. Viene visualizzato un grafico di metrica per il passaggio di hello in un riquadro inferiore della pagina hello.

![Diagramma di processo con metriche - processo di base](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-2.png)

Selezionare le partizioni di hello toosee di input dell'hub eventi di Azure hello **...** Si apre il menu di scelta rapida. È inoltre possibile visualizzare unione input hello.

![Diagramma di processo con metriche - espandere la partizione](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-3.png)

grafico metrica hello di toosee per una singola partizione, il nodo di partizione selezionare hello. le metriche Hello vengono visualizzate nella parte inferiore di hello della pagina hello.

![Diagramma di processo con metriche - altre metriche](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-4.png)

grafico delle metriche di hello toosee per una fusione, nodo unione hello selezionare. Hello seguente grafico mostra che gli eventi non sono stati rimossi o modificati.

![Diagramma di processo con metriche - griglia](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-5.png)

dettagli di hello toosee del valore della metrica hello e l'ora, il grafico toohello punto.

![Diagramma di processo con metriche - puntare con il mouse](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-6.png)

## <a name="troubleshoot-by-using-metrics"></a>Risolvere i problemi mediante le metriche

Hello **QueryLastProcessedTime** metrica indica quando un passaggio specifico ha ricevuto dati. Osservando la topologia hello, è possibile lavorare all'indietro da hello output processore toosee il passaggio non riceve dati. Se un passaggio non ottiene i dati, passare passaggio della query toohello subito prima. Verificare se il passaggio della query precedente hello è un intervallo di tempo e se è trascorso tempo sufficiente toooutput dati. (Si noti che ora windows sono ora bloccati toohello.)
 
Se hello passaggio della query precedente è un processore di input, utilizzare hello di hello metriche input toohelp risposte seguenti domande di destinazione. Esse consentono di determinare se un processo sta ricevendo dati dalle sue origini di input. Se la query hello è partizionata, è possibile esaminare ogni partizione.
 
### <a name="how-much-data-is-being-read"></a>Quanti dati vengono letti?

*   **InputEventsSourcesTotal** hello numero di unità di dati di lettura. Salve, ad esempio, numero di BLOB.
*   **InputEventsTotal** hello numero di eventi di lettura. Questa metrica è disponibile per ogni partizione.
*   **InputEventsInBytesTotal** hello numero di byte letti.
*   **InputEventsLastArrivalTime** viene aggiornato con l'ora di accodamento di ogni evento ricevuto.
 
### <a name="is-time-moving-forward-if-actual-events-are-read-punctuation-might-not-be-issued"></a>L'ora viene spostata in avanti? Se vengono letti eventi reali, potrebbe non essere generata la punteggiatura.

*   **InputEventsLastPunctuationTime** indica un segno di punteggiatura emissione tookeep ora spostare in avanti. Se la punteggiatura non viene generata, il flusso di dati può bloccarsi.
 
### <a name="are-there-any-errors-in-hello-input"></a>Sono presenti errori di input hello?

*   **InputEventsEventDataNullTotal** è un conteggio degli eventi con dati Null.
*   **InputEventsSerializerErrorsTotal** è un conteggio degli eventi che non è stato possibile deserializzare correttamente.
*   **InputEventsDegradedTotal** è un conteggio degli eventi che sono stati interessati da un problema diverso dalla deserializzazione.
 
### <a name="are-events-being-dropped-or-adjusted"></a>Vengono eliminati o modificati eventi?

*   **InputEventsEarlyTotal** hello numero di eventi con un timestamp dell'applicazione prima di limite massimo di hello.
*   **InputEventsLateTotal** hello numero di eventi con un timestamp dell'applicazione dopo il limite massimo di hello.
*   **InputEventsDroppedBeforeApplicationStartTimeTotal** è hello numero di eventi eliminato prima dell'ora di inizio processo hello.
 
### <a name="are-we-falling-behind-in-reading-data"></a>Si sta verificando un ritardo nella lettura dei dati?

*   **InputEventsSourcesBackloggedTotal** indica quanti messaggi più necessario toobe di lettura per gli input di hub eventi e IoT Hub di Azure.


## <a name="get-help"></a>Ottenere aiuto
Per ottenere assistenza aggiuntiva, provare ad accedere al [forum di Analisi di flusso di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Passaggi successivi
* [Introduzione tooStream Analitica](stream-analytics-introduction.md)
* [Introduzione ad Analisi di flusso](stream-analytics-real-time-fraud-detection.md)
* [Scalabilità dei processi di Analisi di flusso](stream-analytics-scale-jobs.md)
* [Informazioni di riferimento sul linguaggio di query di Analisi di flusso](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Informazioni di riferimento sull'API REST di gestione di Analisi di flusso](https://msdn.microsoft.com/library/azure/dn835031.aspx)
