---
title: Monitoraggio processo di flusso Analitica aaaUnderstanding | Documenti Microsoft
description: Informazioni sul monitoraggio dei processi di Analisi di flusso
keywords: monitoraggio di query
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 5f5cc00f-4a7b-491e-89e1-dbafea46d399
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 36819025c7b2ddbf4b9694522f1b4820407ca5f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="understand-stream-analytics-job-monitoring-and-how-toomonitor-queries"></a>Comprendere il monitoraggio di processo di flusso Analitica e la modalità query toomonitor

## <a name="introduction-hello-monitor-page"></a>Introduzione: pagina di monitoraggio hello
Hello portale di Azure sia superficie metriche chiave delle prestazioni che è possono toomonitor utilizzato e risolvere i problemi delle prestazioni di query e processi. toosee queste metriche, individuare il processo di flusso Analitica toohello si è interessati a visualizzare le metriche per e hello vista **monitoraggio** sezione nella pagina di panoramica hello.  

![Collegamento al monitoraggio](./media/stream-analytics-monitoring/02-stream-analytics-monitoring-block.png)

finestra Hello verrà visualizzato come illustrato:

![Monitoraggio del dashboard dei processi](./media/stream-analytics-monitoring/01-stream-analytics-monitoring.png)  

## <a name="metrics-available-for-stream-analytics"></a>Metriche disponibili per l'analisi di flusso
| Metrica                 | Definizione                               |
| ---------------------- | ---------------------------------------- |
| % utilizzo unità di streaming       | utilizzo di Hello di hello unità di Streaming assegnato tooa processo dalla scheda Scala hello del processo di hello. Se questo indicatore raggiunge l'80% o più, esiste una forte probabilità che l'elaborazione di eventi possa essere ritardata o interrotta. |
| Eventi di input           | Quantità di dati ricevuti dal processo di flusso Analitica hello, numero di eventi. Può essere utilizzato toovalidate che gli eventi vengono inviati toohello origine di input. |
| Eventi di output          | Quantità di dati inviati dal hello Analitica flusso processo toohello destinazione di output, in numero di eventi. |
| Eventi non ordinati    | Numero di eventi non ordinati che sono stati eliminati o ha un timestamp, in base a criteri di ordinamento eventi hello ricevuti. Questo può essere influenzato dalla configurazione hello di impostazione della finestra di tolleranza ordine hello. |
| Errori di conversione dati | numero di errori di conversione dei dati rilevati da un processo di Analisi di flusso. |
| Errori di runtime         | numero totale di Hello di errori che si verificano durante l'esecuzione di un processo di flusso Analitica. |
| Ultimi eventi di input      | Numero di eventi che arrivano in ritardo di origine di hello che modo sono stati eliminati o al relativo timestamp è stato modificato, in base alla configurazione di criteri di ordinamento eventi hello dell'impostazione tardiva finestra di tolleranza per arrivo hello. |
| Richieste di funzioni      | Numero di chiamate toohello funzione Azure Machine Learning (se presente). |
| Richieste di funzioni non riuscite | Numero di chiamate non riuscite alla funzione di Azure Machine Learning (se presente). |
| Eventi di funzioni        | Numero di eventi inviati funzione Azure Machine Learning toohello (se presente). |
| Byte evento di input      | Quantità di dati ricevuti dal processo di flusso Analitica hello, in byte. Può essere utilizzato toovalidate che gli eventi vengono inviati toohello origine di input. |


## <a name="customizing-monitoring-in-hello-azure-portal"></a>Personalizzazione di monitoraggio nel portale di Azure hello
È possibile modificare il tipo di hello del grafico, metriche visualizzate, intervallo di tempo nelle impostazioni di modifica grafico hello. Per informazioni dettagliate, vedere [come tooCustomize monitoraggio](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).

  ![Monitoraggio query, grafico cronologico](./media/stream-analytics-monitoring/08-stream-analytics-monitoring.png)  


## <a name="get-help"></a>Ottenere aiuto
Per assistenza, provare il [Forum di Analisi di flusso di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Passaggi successivi
* [Introduzione tooAzure flusso Analitica](stream-analytics-introduction.md)
* [Introduzione all'uso di Analisi dei flussi di Azure](stream-analytics-real-time-fraud-detection.md)
* [Ridimensionare i processi di Analisi dei flussi di Azure](stream-analytics-scale-jobs.md)
* [Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure](https://msdn.microsoft.com/library/azure/dn835031.aspx)

