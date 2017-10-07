---
title: toostart aaaHow streaming i processi di flusso Analitica | Documenti Microsoft
description: Come eseguire un processo di streaming in Analisi di flusso di Azure | segmento del percorso di apprendimento.
keywords: processi di streaming
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9d46950f-2b69-49ce-a567-df558c5dd820
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 67aa14860c38cbd0535d0ec4f23729445d0185c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-streaming-job-in-azure-stream-analytics"></a>Come un flusso toorun processo Analitica di flusso di Azure
Quando un processo per l'input, output e query sono state specificate tutte che è possibile avviare il processo di flusso Analitica hello.

toostart il processo:

1. Nel portale di Azure classico hello, dal dashboard processo hello, fare clic su **avviare** nella parte inferiore di hello della pagina hello.
   
   ![Pulsante Avvia processo](./media/stream-analytics-run-a-job/1-stream-analytics-run-a-job.png)  
   
   Nel portale di Azure hello, fare clic su **avviare** nella parte superiore di hello della pagina di processo.
   
   ![Portale di Azure, Pulsante Avvia processo](./media/stream-analytics-run-a-job/4-stream-analytics-run-a-job.png)  
2. Specificare un **avviare Output** toodetermine valore quando questo processo verrà avviata la produzione di output. Hello impostazione predefinita per i processi che non sono già state avviate è **Job Start Time**, il che significa che il processo di hello avviare immediatamente l'elaborazione dei dati. È inoltre possibile specificare un **personalizzato** tempo in hello passato (per l'utilizzo di dati cronologici) o hello futura (toodelay l'elaborazione fino a un momento futuro). Per i casi in cui un processo è stato avviato e arrestato, in precedenza hello opzione **ora ultimo arresto** è disponibile nel processo di ordine tooresume hello dall'ultima ora di output di hello ed evitare la perdita di dati.  
   
   ![Ora di avvio del processo di streaming](./media/stream-analytics-run-a-job/2-stream-analytics-run-a-job.png)  
   
   ![Portale di Azure, ora di avvio del processo di streaming](./media/stream-analytics-run-a-job/5-stream-analytics-run-a-job.png)  
3. Confermare la selezione. lo stato del processo Hello cambierà troppo*iniziale* e a breve verrà spostata troppo*esecuzione* una volta avviato il processo di hello. È possibile monitorare lo stato di avanzamento hello di hello **avviare** operazione hello **Hub di notifica**:
   
   ![avanzamento del processo di streaming](./media/stream-analytics-run-a-job/3-stream-analytics-run-a-job.png)  
   
   ![Portale di Azure, stato del processo di streaming](./media/stream-analytics-run-a-job/6-stream-analytics-run-a-job.png)  

## <a name="get-help"></a>Ottenere aiuto
Per assistenza, provare il [Forum di Analisi di flusso di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Passaggi successivi
* [Introduzione tooAzure flusso Analitica](stream-analytics-introduction.md)
* [Introduzione all'uso di Analisi dei flussi di Azure](stream-analytics-real-time-fraud-detection.md)
* [Ridimensionare i processi di Analisi dei flussi di Azure](stream-analytics-scale-jobs.md)
* [Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure](https://msdn.microsoft.com/library/azure/dn835031.aspx)

