---
title: Guida di aaaTroubleshooting per Analitica di flusso di Azure | Documenti Microsoft
description: Come tootroubleshoot il processo di flusso Analitica
keywords: guida per la risoluzione dei problemi
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
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 4add48054e06a7d8eb617a08595c1be4555c59d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-azure-stream-analytics"></a>Guida per la risoluzione dei problemi di Analisi di flusso di Azure

Risoluzione dei problemi di Azure Analitica flusso toobe complessa può apparire a prima vista. Dopo aver lavorato con molti utenti, è stato creato il processo di hello Guida toohelp semplificata e rimuovere incognite hello sulle input e output, le query e funzioni.

## <a name="troubleshoot-your-stream-analytics-job"></a>Risoluzione dei problemi del processo di Analisi di flusso

Per ottenere risultati ottimali nella risoluzione dei problemi relativi al processo di flusso Analitica, utilizzare hello alle linee guida:

1.  Testare la connettività:
    - Verificare la connettività tooinputs e output utilizzando hello **Test connessione** per ognuno di input e output.

2.  Esaminare i dati di input:
    - passa tooverify che i dati di input nell'Hub eventi, utilizzare [Service Bus Explorer](https://code.msdn.microsoft.com/windowsapps/Service-Bus-Explorer-f2abca5a) tooconnect tooAzure Hub di eventi (se viene utilizzato l'input dell'Hub eventi).  
    - Hello utilizzare [ **dati di esempio** ](stream-analytics-sample-data-input.md) pulsante per ogni input e il download dei dati di input di esempio hello.
    - Controllare hello esempio toounderstand hello forma dei dati hello: hello hello e lo schema [tipi di dati](https://msdn.microsoft.com/library/azure/dn835065.aspx).

3.  Testare la query:
    - In hello **Query** scheda, utilizzare hello **Test** pulsante query hello tootest e utilizzare dati di esempio hello scaricato troppo[test hello query](stream-analytics-test-query.md). Esaminare gli eventuali errori e tentare toocorrect li.
    - Se si utilizza [ **Timestamp By**](https://msdn.microsoft.com/library/azure/mt573293.aspx), verificare che gli eventi di hello con timestamp maggiore di hello [ora di inizio del processo](stream-analytics-out-of-order-and-late-events.md).

4.  Eseguire il debug della query:
    - Ricompilare la query hello progressivamente da aggregazioni complesse di istruzione select semplice toomore attenendosi alla procedura. Utilizzare toobuild di passaggio per passaggio e logica della query hello [WITH](https://msdn.microsoft.com/library/azure/dn835049.aspx) clausole.
    - Utilizzare [SELECT INTO](stream-analytics-select-into.md) toodebug passaggi di query.

5.  Eliminare i problemi comuni, ad esempio:
    - Oggetto [ **in** ](https://msdn.microsoft.com/library/azure/dn835048.aspx) clausola di query hello filtrati da tutti gli eventi, impedendo che viene generato alcun output.
    - Quando si utilizzano funzioni finestra, attendere hello intera finestra durata toosee un output dalla query hello.
    - Hello timestamp per gli eventi precede l'ora di inizio processo hello e, pertanto, vengono eliminati gli eventi.

6.  Usare l'ordine degli eventi:
    - Se tutti hello passaggi precedenti funzionati correttamente, andare toohello **impostazioni** pannello e selezionare [ **ordine degli eventi**](stream-analytics-out-of-order-and-late-events.md). Verificare che questo criterio sia configurato in modo sensato per lo scenario. criteri di Hello sono *non* applicate quando si utilizza hello **Test** query di hello tootest pulsante. Il risultato è una differenza tra il test nel browser e in esecuzione il processo di hello nell'ambiente di produzione.

7.  Eseguire il debug usando le metriche:
    - Se non si ottiene alcun output dopo hello previsto di durata (basata su query hello), provare a seguito di hello:
        - Esaminare [ **metriche di monitoraggio** ](stream-analytics-monitoring.md) su hello **monitoraggio** scheda. Poiché vengono aggregati i valori hello, metriche hello ritardo di pochi minuti.
            - Se gli eventi di Input > 0, il processo di hello è in grado di tooread dati di input. Se Eventi di input non è maggiore di zero:
                - toosee se l'origine dati hello i dati siano validi, archiviarlo tramite [Service Bus Explorer](https://code.msdn.microsoft.com/windowsapps/Service-Bus-Explorer-f2abca5a). La verifica viene eseguita se il processo di hello utilizza Hub eventi come input.
                - Controllare toosee se il formato di serializzazione di dati hello e codifica dei dati sono quelli previsti.
                - Se il processo di hello utilizza un Hub eventi, controllare toosee se hello corpo del messaggio hello è *Null*.
            - Se gli errori di conversione dati > 0 e progressivamente, seguente hello potrebbero essere true:
                - processo Hello potrebbe non essere in grado di toode-serializzare eventi hello.
                - Hello allo schema di eventi potrebbe non corrispondere hello definito o lo schema previsto di eventi di hello in query hello.
                - Hello tipi di dati di alcuni dei campi evento hello hello potrebbero non corrispondere alle aspettative.
            - Se gli errori di Runtime > 0, significa che il processo di hello può ricevere dati hello ma genera errori durante l'elaborazione di query hello.
                - errori hello toofind, andare toohello [i log di controllo](../azure-resource-manager/resource-group-audit.md) e filtrare in base a *non riuscito* stato.
            - Se InputEvents > 0 e OutputEvents = 0, significa che uno dei seguenti hello è vera:
                - L'elaborazione della query non ha prodotto eventi di output.
                - Il formato degli eventi o dei relativi campi potrebbe non essere valido, di conseguenza l'elaborazione della query non ha prodotto output.
                - il processo di Hello è stato Impossibile toopush dati toohello [sink di output](stream-analytics-select-into.md) per motivi di connettività o di autenticazione.
        - Hello tutte indicate in precedenza i casi di errori, le operazioni di messaggi di log forniti ulteriori dettagli, inclusi qual è il problema, ad eccezione dei casi in cui la logica della query hello filtrato tutti gli eventi. Se l'errore di elaborazione hello di più eventi, flusso Analitica registri hello primi tre messaggi di errore di hello dello stesso tipo all'interno di 10 minuti tooOperations Registra. Elimina quindi gli altri errori identici con il messaggio "Gli errori si verificano troppo rapidamente e verranno eliminati".

8. Eseguire il debug usando i log di controllo e diagnostica:
    - Utilizzare [i log di controllo](../azure-resource-manager/resource-group-audit.md)e gli errori di filtro tooidentify ed eseguire il debug.
    - Utilizzare [processo log di diagnostica](stream-analytics-job-diagnostic-logs.md) tooidentify ed eseguire il debug degli errori.

9. Esaminare l'output di hello:
    - Quando lo stato del processo hello è *esecuzione*, a seconda della durata di hello quanto stabilito nella query hello, è possibile visualizzare l'output di hello nell'origine dati di hello sink.
    - Se è possibile visualizzare l'output che verranno tooa nell'output specifico tipo, reindirizza tooan tipo di output che è meno complesso, ad esempio un Blob di Azure. Tramite Esplora archivi, controllare toosee se può essere visualizzato l'output di hello. Inoltre, verificare se i limiti di limitazione delle richieste dall'output di hello impediscono dati ricevuti.

10. Usare l'analisi del flusso di dati con le metriche del diagramma di processo:
    - flusso di dati tooanalyze e identificare i problemi, utilizzare hello [diagramma di processo con le metriche](stream-analytics-job-diagram-with-metrics.md).

11. Aprire un caso di supporto:
    - Infine, se necessario, aprire un caso di supporto tecnico Microsoft tramite hello SubscriptionID contenente il processo.

## <a name="get-help"></a>Ottenere aiuto

Per ulteriore assistenza, provare il [Forum di Analisi dei flussi di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Passaggi successivi

* [Introduzione tooAzure flusso Analitica](stream-analytics-introduction.md)
* [Introduzione all'uso di Analisi dei flussi di Azure](stream-analytics-real-time-fraud-detection.md)
* [Ridimensionare i processi di Analisi dei flussi di Azure](stream-analytics-scale-jobs.md)
* [Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure](https://msdn.microsoft.com/library/azure/dn835031.aspx)
