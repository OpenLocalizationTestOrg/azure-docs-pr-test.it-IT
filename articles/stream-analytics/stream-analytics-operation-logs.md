---
title: utilizzo dei registri di operazione e il servizio nel flusso Analitica aaaDebug | Documenti Microsoft
description: Flusso come toouse registri operazioni Analitica
keywords: log dei servizi
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: a2ed9676-f0bd-4398-87c8-a592779ac728
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: d3dd27706ccc879a724e1894b33d47021d972f31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="debug-stream-analytics-jobs-using-service-and-operation-logs"></a>Eseguire il debug dei processi di analisi di flusso con i log dei servizi e delle operazioni
Tutti i dettagli del toorecord toousers registrazione operativo approvvigionamento di servizi di Azure i messaggi correlati toomanagement operazioni. In Azure flusso Analitica, è possono utilizzare queste informazioni per il debugging, ad esempio la visualizzazione dello stato del processo, lo stato del processo ed errore messaggi tootrack hello lo stato di avanzamento di un processo nel tempo, dall'inizio tooprocessing toooutput.

## <a name="find-operation-logs-in-hello-azure-management-portal"></a>Trovare il log delle operazioni nel portale di gestione di Azure hello
E’ possibile accedere ai log delle operazioni in due modi:  

* Dashboard del processo di flusso Analitica hello  
* Servizi di gestione nel portale di Azure classico hello  

## <a name="dashboard-of-hello-stream-analytics-job"></a>Dashboard del processo di flusso Analitica hello
Un collegamento di toohello corrispondente i log di un processo di flusso Analitica viene visualizzato nella scheda Dashboard del processo di hello. Se si fa clic su tale collegamento, Imposta filtri hello in modo che consente di visualizzare i log più recenti di tale processo specifico.

  ![Selezionare i log dei servizi di gestione](./media/stream-analytics-operation-logs/01-stream-analytics-operation-logs.png)  

## <a name="management-services"></a>Servizi di gestione
toomanually passare registri operazioni toohello per Analitica flusso e altri servizi nel portale di Azure classico hello:

1. Fare clic su **servizi di gestione** in hello [portale di Azure classico](https://manage.windowsazure.com).
2. Selezionare **Analitica flusso** per **tipo** e il nome del processo di hello per hello **nome servizio**.  
   
   ![Selezionare analisi di flusso](./media/stream-analytics-operation-logs/02-stream-analytics-operation-logs.png)  

## <a name="find-audit-logs-in-hello-azure-portal"></a>Trovare i log di controllo nel portale di Azure hello
Fare clic su registri toofind per il processo di flusso Analitica nel portale di Azure hello **Sfoglia** e quindi selezionare **log di controllo**.

  ![Selezione analisi di flusso del portale di Azure](./media/stream-analytics-operation-logs/06-stream-analytics-operation-logs.png)  

Verrà aperta una blade che mostra gli eventi da hello ultimi 7 giorni per tutte le risorse nella sottoscrizione.  È possibile filtrare gli eventi toosee di un tipo specificato o un intervallo di tempo facendo hello **filtro** comando.

  ![Selezione analisi di flusso del portale di Azure](./media/stream-analytics-operation-logs/07-stream-analytics-operation-logs.png)  

## <a name="get-log-details"></a>Ottenere i dettagli dei log
È possibile filtrare l'intervallo di tempo e registri di hello tooview di stato per il processo.

Nel portale di gestione di Azure hello, fare clic su hello **dettagli** pulsante nella parte inferiore di hello di hello finestra tooview ulteriori dettagli sull'evento selezionato. 

  ![Selezionare i dettagli](./media/stream-analytics-operation-logs/03-stream-analytics-operation-logs.png)  

In hello portale di Azure, fare clic su un toosee voce di log hello eventi dettagliati in essa contenuti.

  ![Selezione dettagli del portale di Azure](./media/stream-analytics-operation-logs/08-stream-analytics-operation-logs.png)  

Da qui, è possibile aprire hello **dettaglio** pannello facendo clic sull'evento hello.

  ![Selezione dettagli del portale di Azure](./media/stream-analytics-operation-logs/09-stream-analytics-operation-logs.png)  

## <a name="debug-a-failed-job"></a>Debug di un processo non riuscito
Nel portale di gestione di Azure hello, fare clic sull'icona di ricerca hello e digitare "non riuscito". In questo modo si visualizzeranno tutti i log dei processi non riusciti. 

  ![Eseguire il debug di un processo non riuscito](./media/stream-analytics-operation-logs/04-stream-analytics-operation-logs.png)  

Nel portale di Azure hello, è possibile filtrare per livello di messaggio tooview **critico** eventi.

  ![Debug del portale di Azure](./media/stream-analytics-operation-logs/10-stream-analytics-operation-logs.png)  

È possibile selezionare uno qualsiasi degli errori di hello e fare clic su hello **dettagli** per ulteriori informazioni sull'errore hello.  Alcuni messaggi di errore forniscono inoltre informazioni su come toomitigate hello problema. 

  ![Dettagli operazione](./media/stream-analytics-operation-logs/05-stream-analytics-operation-logs.png)  

Nel caso in cui è necessario toocontact [supporto](https://azure.microsoft.com/support/options/) o fornire informazioni toohello team tramite hello [forum MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics), tenere presente i dettagli operazione hello, in particolare hello **ID di correlazione**. 

## <a name="get-help"></a>Ottenere aiuto
Per assistenza, provare il [Forum di Analisi di flusso di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Passaggi successivi
* [Introduzione tooAzure flusso Analitica](stream-analytics-introduction.md)
* [Introduzione all'uso di Analisi dei flussi di Azure](stream-analytics-real-time-fraud-detection.md)
* [Ridimensionare i processi di Analisi dei flussi di Azure](stream-analytics-scale-jobs.md)
* [Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure](https://msdn.microsoft.com/library/azure/dn835031.aspx)

