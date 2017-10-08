---
title: le query toowrite aaaHow nel flusso Analitica | Documenti Microsoft
description: Scrivere query in Analisi di flusso ed eseguire query sui dati | segmento del percorso di apprendimento.
keywords: "la modalità query toowrite, eseguire query sui dati, scrivere una query, la scrittura di query"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 0e9cdadd-0ee0-4bee-b65b-4a06fb863c95
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: b943c34f10afd2b21789afbd341c471a5f168729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toowrite-queries-in-stream-analytics"></a>La modalità di query toowrite in flusso Analitica
Scrittura di query per il flusso di elaborazione logica Analitica di flusso di Azure viene implementata come un "query in esecuzione" definito prima di avvia e raggiunge il processo di hello eseguite sui dati di un processo. la trasformazione dei dati Hello è espresso in un linguaggio di query simile a SQL, che è sostanzialmente un subset di T-SQL con alcune aggiunte estensioni del linguaggio come [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) utilizzato tooexpress temporale semantica.

## <a name="writing-queries"></a>Scrittura di query:
1. Nel processo flusso Analitica nel portale di gestione di Azure hello, fare clic su **Query**.
   
    ![Query di selezione](./media/stream-analytics-write-queries/1-stream-analytics-write-queries.png)  
   
    Nel portale di Azure hello, fare clic su **Query**.
   
    ![Selezionare l'anteprima della query](./media/stream-analytics-write-queries/query-preview-portal.png)  
2. I nuovi processi hanno un toohelp modello di query consentono di iniziare. query Hello modello esegue "pass-through" eseguire una query che viene proiettato tutti i campi da eventi di input nell'output di hello.  
   
   * Se è stato definito almeno un input e output per il processo, è possibile sostituire i segnaposto hello "[YourOutputAlias]" e "[YourInputAlias]" campi con alias hello di hello di input e output che si desidera utilizzare prima. È inoltre possibile creare e testare la query nel portale di Azure classico hello senza definire l'input e output per il processo di hello.
   * Se si desidera tooperform maggiore elaborazione rispetto a un semplice pass-through, è possibile modificare la definizione della query hello. tooget introduttiva alla creazione di query, esaminare alcune query comuni, vengono acquisiti i modelli [qui](stream-analytics-stream-analytics-query-patterns.md).  
   
   ![Eseguire query sui dati, finestra](./media/stream-analytics-write-queries/2-stream-analytics-write-queries.png)  

## <a name="toovalidate-query-data-is-working"></a>dati di query toovalidate funzioni:
È possibile verificare che la query si comporti come previsto eseguendo nel browser hello su uno o più file JSON locali contenente i dati di test. Questo non verrà avviato il processo di hello né quindi alcuna implicazione di fatturazione.

> [!NOTE]
> Attualmente il test delle query nel browser non è supportato nel portale di Azure hello.  
> 
> 

1. Assicurarsi che non siano presenti errori nella query hello (in caso contrario hello Test pulsante sarà disabilitato) e quindi fare clic su pulsante Test hello.  
   
   ![Eseguire query sui dati, test](./media/stream-analytics-write-queries/3-stream-analytics-write-queries.png)  
2. Sarà richiesta toospecify file per ogni input hello a cui fa riferimento nella query hello. In questo esempio, query modello hello viene lasciata come-è, quindi finestra di dialogo hello è richiesta per un input denominato "yourinputalias".  
   
   ![Verificare query sui dati](./media/stream-analytics-write-queries/4-stream-analytics-write-queries.png)  
3. Individuare il file di test tooa. Sono disponibili in diversi file di esempio [github](https://github.com/Azure/azure-stream-analytics/tree/master/Sample Data) ed è anche possibile recuperare i dati di esempio dal proprio input flusso di dati tramite una funzione di dati di esempio nella scheda input hello hello.  
   
   ![Input della query](./media/stream-analytics-write-queries/5-stream-analytics-write-queries.png)  
4. Dopo la chiusura di finestra di dialogo hello, verrà eseguita la query sui dati di test hello e verranno visualizzati risultati hello nella parte inferiore di hello della pagina di Query hello.  
   
   ![Riepilogo della query](./media/stream-analytics-write-queries/6-stream-analytics-write-queries.png)  

## <a name="get-help"></a>Ottenere aiuto
Per assistenza, provare il [Forum di Analisi di flusso di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Passaggi successivi
* [Introduzione tooAzure flusso Analitica](stream-analytics-introduction.md)
* [Introduzione all'uso di Analisi dei flussi di Azure](stream-analytics-real-time-fraud-detection.md)
* [Ridimensionare i processi di Analisi dei flussi di Azure](stream-analytics-scale-jobs.md)
* [Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure](https://msdn.microsoft.com/library/azure/dn835031.aspx)

