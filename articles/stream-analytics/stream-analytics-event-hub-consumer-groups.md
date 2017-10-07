---
title: aaaDebug Analitica di flusso di Azure con i ricevitori di eventi hub | Documenti Microsoft
description: Procedure consigliate di query per considerare i gruppi di consumer dell'hub eventi nei processi di Analisi di flusso.
keywords: limite dell'hub eventi, gruppo di consumer
services: stream-analytics
documentationcenter: 
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
ms.openlocfilehash: 89821e6273151de43b5e42d907e547c939e24824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="debug-azure-stream-analytics-with-event-hub-receivers"></a>Eseguire il debug di Analisi di flusso di Azure con i ricevitori dell'hub eventi

Azure flusso Analitica tooingest o output dei dati da un processo, è possibile utilizzare gli hub di eventi di Azure. Una procedura consigliata per l'uso di hub eventi è toouse più gruppi di consumer, scalabilità processo tooensure. Uno dei motivi è che il numero di hello di lettori nel processo di flusso Analitica hello un input specifico riguarda il numero di hello di lettori in un gruppo di consumer singolo. numero preciso di Hello di ricevitori è basato sui dettagli di implementazione interna per la logica della topologia di scalabilità orizzontale hello. numero di Hello di ricevitori non è esposta esternamente. numero di Hello di lettori può cambiare in fase di inizio processo hello o durante gli aggiornamenti di processo.

> [!NOTE]
> Quando il numero di hello di lettori cambia durante l'aggiornamento di un processo, gli avvisi temporanei vengono scritti tooaudit log. I processi di Analisi di flusso vengono ripristinati automaticamente da questi problemi temporanei.

## <a name="number-of-readers-per-partition-exceeds-event-hubs-limit-of-five"></a>Il numero di lettori per partizione supera il limite di cinque hub eventi

Gli scenari in cui hello numero di lettori per ogni partizione supera il limite di hub eventi hello di cinque includono seguente hello:

* Più istruzioni SELECT: se si utilizzano più istruzioni SELECT che fanno riferimento troppo**stesso** hub eventi di input, ogni istruzione SELECT fa sì che un nuovo toobe ricevitore creato.
* UNIONE: Quando si utilizza un'unione, è possibile toohave più input che fanno riferimento toohello **stesso** gruppo di hub e consumer di eventi.
* Self-JOIN: Quando si usa un'operazione SELF JOIN, è possibile toorefer toohello **stesso** hub di eventi più volte.

## <a name="solution"></a>Soluzione

Hello procedure consigliate seguenti consente di attenuare gli scenari in cui hello numero di lettori per ogni partizione supera il limite di hub eventi hello di cinque.

### <a name="split-your-query-into-multiple-steps-by-using-a-with-clause"></a>Suddividere la query in più passaggi usando una clausola WITH

clausola WITH Hello specifica un set di risultati denominato temporaneo che è possibile fare riferimento a una clausola FROM nella query hello. Definire una clausola WITH hello in ambito di esecuzione hello di una singola istruzione SELECT.

Ad esempio, invece di questa query:

```
SELECT foo 
INTO output1
FROM inputEventHub

SELECT bar
INTO output2
FROM inputEventHub 
…
```

Usare questa query:

```
WITH input (
   SELECT * FROM inputEventHub
) as data

SELECT foo
INTO output1
FROM data

SELECT bar
INTO output2
FROM data
…
```

### <a name="ensure-that-inputs-bind-toodifferent-consumer-groups"></a>Verificare che gli input associano gruppi di consumer toodifferent

Per le query in cui tre o più input sono connesso toohello consumer di hub eventi stesso gruppo, creare gruppi di consumer distinto. Ciò richiede la creazione di hello di input flusso Analitica aggiuntivi.


## <a name="get-help"></a>Ottenere aiuto
Per ottenere assistenza aggiuntiva, provare ad accedere al [forum di Analisi di flusso di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Passaggi successivi
* [Introduzione tooStream Analitica](stream-analytics-introduction.md)
* [Introduzione ad Analisi di flusso](stream-analytics-real-time-fraud-detection.md)
* [Scalabilità dei processi di Analisi di flusso](stream-analytics-scale-jobs.md)
* [Informazioni di riferimento sul linguaggio di query di Analisi di flusso](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Informazioni di riferimento sull'API REST di gestione di Analisi di flusso](https://msdn.microsoft.com/library/azure/dn835031.aspx)
