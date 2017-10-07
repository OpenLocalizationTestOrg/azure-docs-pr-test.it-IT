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
# <a name="debug-stream-analytics-jobs-using-service-and-operation-logs"></a><span data-ttu-id="f0e5c-104">Eseguire il debug dei processi di analisi di flusso con i log dei servizi e delle operazioni</span><span class="sxs-lookup"><span data-stu-id="f0e5c-104">Debug Stream Analytics jobs using service and operation logs</span></span>
<span data-ttu-id="f0e5c-105">Tutti i dettagli del toorecord toousers registrazione operativo approvvigionamento di servizi di Azure i messaggi correlati toomanagement operazioni.</span><span class="sxs-lookup"><span data-stu-id="f0e5c-105">All Azure services supply operational logging messages toousers toorecord details related toomanagement operations.</span></span> <span data-ttu-id="f0e5c-106">In Azure flusso Analitica, è possono utilizzare queste informazioni per il debugging, ad esempio la visualizzazione dello stato del processo, lo stato del processo ed errore messaggi tootrack hello lo stato di avanzamento di un processo nel tempo, dall'inizio tooprocessing toooutput.</span><span class="sxs-lookup"><span data-stu-id="f0e5c-106">In Azure Stream Analytics, this information can be used for debugging purposes such as viewing job status, job progress, and failure messages tootrack hello progress of a job over time, from start tooprocessing toooutput.</span></span>

## <a name="find-operation-logs-in-hello-azure-management-portal"></a><span data-ttu-id="f0e5c-107">Trovare il log delle operazioni nel portale di gestione di Azure hello</span><span class="sxs-lookup"><span data-stu-id="f0e5c-107">Find operation logs in hello Azure Management portal</span></span>
<span data-ttu-id="f0e5c-108">E’ possibile accedere ai log delle operazioni in due modi:</span><span class="sxs-lookup"><span data-stu-id="f0e5c-108">Operation Logs can be accessed in two ways:</span></span>  

* <span data-ttu-id="f0e5c-109">Dashboard del processo di flusso Analitica hello</span><span class="sxs-lookup"><span data-stu-id="f0e5c-109">Dashboard of hello Stream Analytics job</span></span>  
* <span data-ttu-id="f0e5c-110">Servizi di gestione nel portale di Azure classico hello</span><span class="sxs-lookup"><span data-stu-id="f0e5c-110">Management Services in hello Azure Classic portal</span></span>  

## <a name="dashboard-of-hello-stream-analytics-job"></a><span data-ttu-id="f0e5c-111">Dashboard del processo di flusso Analitica hello</span><span class="sxs-lookup"><span data-stu-id="f0e5c-111">Dashboard of hello Stream Analytics job</span></span>
<span data-ttu-id="f0e5c-112">Un collegamento di toohello corrispondente i log di un processo di flusso Analitica viene visualizzato nella scheda Dashboard del processo di hello. Se si fa clic su tale collegamento, Imposta filtri hello in modo che consente di visualizzare i log più recenti di tale processo specifico.</span><span class="sxs-lookup"><span data-stu-id="f0e5c-112">A link toohello corresponding logs of a Stream Analytics job is displayed on hello job’s Dashboard tab. If you click on that link, it will set hello filters in a way that it shows latest logs for that specific job.</span></span>

  ![Selezionare i log dei servizi di gestione](./media/stream-analytics-operation-logs/01-stream-analytics-operation-logs.png)  

## <a name="management-services"></a><span data-ttu-id="f0e5c-114">Servizi di gestione</span><span class="sxs-lookup"><span data-stu-id="f0e5c-114">Management Services</span></span>
<span data-ttu-id="f0e5c-115">toomanually passare registri operazioni toohello per Analitica flusso e altri servizi nel portale di Azure classico hello:</span><span class="sxs-lookup"><span data-stu-id="f0e5c-115">toomanually navigate toohello Operation Logs for Stream Analytics and other services in hello Azure Classic portal:</span></span>

1. <span data-ttu-id="f0e5c-116">Fare clic su **servizi di gestione** in hello [portale di Azure classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="f0e5c-116">Click on **Management Services** in hello [Azure Classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="f0e5c-117">Selezionare **Analitica flusso** per **tipo** e il nome del processo di hello per hello **nome servizio**.</span><span class="sxs-lookup"><span data-stu-id="f0e5c-117">Select **Stream Analytics** for **Type** and hello name of hello job for **Service Name**.</span></span>  
   
   ![Selezionare analisi di flusso](./media/stream-analytics-operation-logs/02-stream-analytics-operation-logs.png)  

## <a name="find-audit-logs-in-hello-azure-portal"></a><span data-ttu-id="f0e5c-119">Trovare i log di controllo nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="f0e5c-119">Find audit logs in hello Azure portal</span></span>
<span data-ttu-id="f0e5c-120">Fare clic su registri toofind per il processo di flusso Analitica nel portale di Azure hello **Sfoglia** e quindi selezionare **log di controllo**.</span><span class="sxs-lookup"><span data-stu-id="f0e5c-120">toofind operational logs for your Stream Analytics job in hello Azure portal, Click **Browse** and then select **Audit logs**.</span></span>

  ![Selezione analisi di flusso del portale di Azure](./media/stream-analytics-operation-logs/06-stream-analytics-operation-logs.png)  

<span data-ttu-id="f0e5c-122">Verrà aperta una blade che mostra gli eventi da hello ultimi 7 giorni per tutte le risorse nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="f0e5c-122">This will open a blade showing events from hello last 7 days for all resources in your subscription.</span></span>  <span data-ttu-id="f0e5c-123">È possibile filtrare gli eventi toosee di un tipo specificato o un intervallo di tempo facendo hello **filtro** comando.</span><span class="sxs-lookup"><span data-stu-id="f0e5c-123">You can filter toosee events of a specify type or time frame by clicking hello **Filter** command.</span></span>

  ![Selezione analisi di flusso del portale di Azure](./media/stream-analytics-operation-logs/07-stream-analytics-operation-logs.png)  

## <a name="get-log-details"></a><span data-ttu-id="f0e5c-125">Ottenere i dettagli dei log</span><span class="sxs-lookup"><span data-stu-id="f0e5c-125">Get log details</span></span>
<span data-ttu-id="f0e5c-126">È possibile filtrare l'intervallo di tempo e registri di hello tooview di stato per il processo.</span><span class="sxs-lookup"><span data-stu-id="f0e5c-126">You can filter by Time Range and Status tooview hello logs for your job.</span></span>

<span data-ttu-id="f0e5c-127">Nel portale di gestione di Azure hello, fare clic su hello **dettagli** pulsante nella parte inferiore di hello di hello finestra tooview ulteriori dettagli sull'evento selezionato.</span><span class="sxs-lookup"><span data-stu-id="f0e5c-127">In hello Azure Management portal, click on hello **Details** button at hello bottom of hello window tooview more details about a selected event.</span></span> 

  ![Selezionare i dettagli](./media/stream-analytics-operation-logs/03-stream-analytics-operation-logs.png)  

<span data-ttu-id="f0e5c-129">In hello portale di Azure, fare clic su un toosee voce di log hello eventi dettagliati in essa contenuti.</span><span class="sxs-lookup"><span data-stu-id="f0e5c-129">In hello Azure portal, click on a log entry toosee hello detailed events inside it.</span></span>

  ![Selezione dettagli del portale di Azure](./media/stream-analytics-operation-logs/08-stream-analytics-operation-logs.png)  

<span data-ttu-id="f0e5c-131">Da qui, è possibile aprire hello **dettaglio** pannello facendo clic sull'evento hello.</span><span class="sxs-lookup"><span data-stu-id="f0e5c-131">From there, you can open hello **Detail** blade by clicking on hello event.</span></span>

  ![Selezione dettagli del portale di Azure](./media/stream-analytics-operation-logs/09-stream-analytics-operation-logs.png)  

## <a name="debug-a-failed-job"></a><span data-ttu-id="f0e5c-133">Debug di un processo non riuscito</span><span class="sxs-lookup"><span data-stu-id="f0e5c-133">Debug a failed job</span></span>
<span data-ttu-id="f0e5c-134">Nel portale di gestione di Azure hello, fare clic sull'icona di ricerca hello e digitare "non riuscito".</span><span class="sxs-lookup"><span data-stu-id="f0e5c-134">In hello Azure Management portal, click on hello Search icon and type ‘failed’.</span></span> <span data-ttu-id="f0e5c-135">In questo modo si visualizzeranno tutti i log dei processi non riusciti.</span><span class="sxs-lookup"><span data-stu-id="f0e5c-135">This gives a result of all logs with failures.</span></span> 

  ![Eseguire il debug di un processo non riuscito](./media/stream-analytics-operation-logs/04-stream-analytics-operation-logs.png)  

<span data-ttu-id="f0e5c-137">Nel portale di Azure hello, è possibile filtrare per livello di messaggio tooview **critico** eventi.</span><span class="sxs-lookup"><span data-stu-id="f0e5c-137">In hello Azure portal, you can filter by level of message tooview **Critical** events.</span></span>

  ![Debug del portale di Azure](./media/stream-analytics-operation-logs/10-stream-analytics-operation-logs.png)  

<span data-ttu-id="f0e5c-139">È possibile selezionare uno qualsiasi degli errori di hello e fare clic su hello **dettagli** per ulteriori informazioni sull'errore hello.</span><span class="sxs-lookup"><span data-stu-id="f0e5c-139">You can select any one of hello failures, and click on hello **Details** for more information on hello error.</span></span>  <span data-ttu-id="f0e5c-140">Alcuni messaggi di errore forniscono inoltre informazioni su come toomitigate hello problema.</span><span class="sxs-lookup"><span data-stu-id="f0e5c-140">Some error messages also provide information about how toomitigate hello issue.</span></span> 

  ![Dettagli operazione](./media/stream-analytics-operation-logs/05-stream-analytics-operation-logs.png)  

<span data-ttu-id="f0e5c-142">Nel caso in cui è necessario toocontact [supporto](https://azure.microsoft.com/support/options/) o fornire informazioni toohello team tramite hello [forum MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics), tenere presente i dettagli operazione hello, in particolare hello **ID di correlazione**.</span><span class="sxs-lookup"><span data-stu-id="f0e5c-142">In case you need toocontact [Support](https://azure.microsoft.com/support/options/) or provide information toohello team via hello [MSDN forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics), please note hello Operation Details, specifically hello **Correlation ID**.</span></span> 

## <a name="get-help"></a><span data-ttu-id="f0e5c-143">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="f0e5c-143">Get help</span></span>
<span data-ttu-id="f0e5c-144">Per assistenza, provare il [Forum di Analisi di flusso di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="f0e5c-144">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0e5c-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f0e5c-145">Next steps</span></span>
* [<span data-ttu-id="f0e5c-146">Introduzione tooAzure flusso Analitica</span><span class="sxs-lookup"><span data-stu-id="f0e5c-146">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="f0e5c-147">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="f0e5c-147">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="f0e5c-148">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="f0e5c-148">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="f0e5c-149">Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="f0e5c-149">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="f0e5c-150">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="f0e5c-150">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

