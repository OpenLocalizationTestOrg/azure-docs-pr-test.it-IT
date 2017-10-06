---
title: aaaHandling ordine degli eventi e lateness con Analitica di flusso di Azure | Documenti Microsoft
description: Informazioni su come funziona Analisi di flusso con gli eventi non in ordine o in ritardo nei flussi di dati.
keywords: non in ordine, in ritardo, eventi
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
ms.openlocfilehash: 87c028662fbafbf4f72f57f215d017f65bb649f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-event-order-handling"></a>Gestione dell'ordine degli eventi con Analisi di flusso di Azure

In un flusso di dati temporali degli eventi, ogni evento viene registrato con il tempo di hello viene ricevuto l'evento hello. Alcune condizioni potrebbero produrre i flussi di eventi di ricezione toooccasionally alcuni eventi in un ordine diverso rispetto a cui sono stati inviati. La ritrasmissione TCP semplice, o anche un sfasamento tra l'invio di dispositivo e la ricezione di hub eventi hello hello può causare questo toooccur. Eventi "Punteggiatura" vengono aggiunti anche i flussi di eventi tooreceived, ora hello tooadvance in assenza di hello di arrivo di eventi. Questo è necessario negli scenari come "Inviare una notifica quando non si verificano accessi per 3 minuti".

I flussi di input che non sono in ordine vengono:
* Ordinati (e perciò **ritardati**).
* Regolato dal sistema hello, in base a criteri di tooa specificato dall'utente.


## <a name="lateness-tolerance"></a>Tolleranza ai ritardi
Analisi di flusso tollera questi tipi di scenari. Analisi di flusso è in grado di gestire gli eventi "non in ordine" e "in ritardo". Gestisce questi eventi in hello seguenti modi:

* Gli eventi che arrivano senza ordine ma all'interno di hello, impostare la tolleranza sono **riordinati timestamp**.
* Gli eventi che arrivano con un ritardo maggiore della tolleranza vengono **eliminati o regolati**.
    * **Rettificato**: toohave tooappear rettificato ricevuti dal tempo accettabile più recente di hello.
    * **Eliminati**: rimossi.

![Gestione degli eventi con Analisi di flusso](media/stream-analytics-event-handling/stream-analytics-event-handling.png)

## <a name="reduce-hello-number-of-out-of-order-events"></a>Ridurre il numero di hello di eventi in ordine

Poiché Analisi di flusso applica una trasformazione temporale quando elabora gli eventi in ingresso (ad esempio per le aggregazioni finestra o i join temporali), ordina gli eventi in ingresso per timestamp.

Quando la parola chiave da hello "timestamp" è **non** , tempo di accodamento eventi di hello hub eventi di Azure viene utilizzato per impostazione predefinita. Hub eventi garantisce monotonicità di hello timestamp in ogni partizione dell'hub eventi hello. Garantisce anche che gli eventi di tutte le partizioni saranno uniti in ordine di timestamp. Queste due garanzie di Hub eventi assicurano l'assenza di eventi non in ordine.

In alcuni casi, è importante per il timestamp è toouse hello del mittente. In tal caso, un timestamp di payload dell'evento hello viene scelto utilizzando "timestamp da". Questi scenari potrebbero introdurre una o più cause che determinano eventi non ordinati:

* I producer di eventi presentano sfasamenti di orario. Questo è comune quando i producer provengono da computer diversi che inevitabilmente hanno orologi diversi.
* Si verifica un ritardo di rete dall'origine hello dell'hub di eventi di hello eventi toohello destinazione.
* Esistono sfasamenti di orario tra le partizioni dell'hub eventi. Analisi di flusso innanzitutto ordina gli eventi di tutte le partizioni dell'hub eventi in base all'ora di accodamento dell'evento. Quindi, viene esaminato il flusso di dati hello per misordered eventi.

Nella scheda Configurazione hello, vedrai hello valori predefiniti seguenti:

![Gestione degli eventi non in ordine di Analisi di flusso](media/stream-analytics-event-handling/stream-analytics-out-of-order-handling.png)

Se si usano 0 secondi come finestra di tolleranza di errore in ordine di hello, asserito che tutti gli eventi sono in ordine tutto il tempo hello. Dato origini hello tre eventi misordered, è improbabile che questo è true. 

tooallow Analitica flusso toocorrect misorder un evento, è possibile specificare una finestra di tolleranza in ordine diverso da zero. Eventi di buffer flusso Analitica backup toothat finestra e quindi riordini che loro usando hello timestamp che scelto. Si applica quindi la trasformazione temporale hello. È possibile iniziare con una finestra di 3 secondi e ottimizzare hello valore tooreduce hello il numero di eventi che sono in base al tempo. 

Un effetto collaterale della memorizzazione nel buffer hello è che l'output di hello è **ritardato hello stesso periodo di tempo**. È possibile ottimizzare hello valore tooreduce hello il numero di eventi in ordine e mantenere la bassa latenza processo hello.

## <a name="get-help"></a>Ottenere aiuto
Per ottenere assistenza aggiuntiva, provare ad accedere al [forum di Analisi di flusso di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Passaggi successivi
* [Introduzione tooStream Analitica](stream-analytics-introduction.md)
* [Introduzione ad Analisi di flusso](stream-analytics-real-time-fraud-detection.md)
* [Scalabilità dei processi di Analisi di flusso](stream-analytics-scale-jobs.md)
* [Informazioni di riferimento sul linguaggio di query di Analisi di flusso](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Informazioni di riferimento sull'API REST di gestione di Analisi di flusso](https://msdn.microsoft.com/library/azure/dn835031.aspx)