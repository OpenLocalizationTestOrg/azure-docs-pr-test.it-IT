---
title: Eseguire il debug con i log dell'operazione e del servizio in analisi di flusso | Documentazione Microsoft
description: Come usare i log delle operazioni di Analisi di flusso
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
ms.openlocfilehash: c95d240ebef6a84228eb98db70002792fcfbdea6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="debug-stream-analytics-jobs-using-service-and-operation-logs"></a><span data-ttu-id="12935-104">Eseguire il debug dei processi di analisi di flusso con i log dei servizi e delle operazioni</span><span class="sxs-lookup"><span data-stu-id="12935-104">Debug Stream Analytics jobs using service and operation logs</span></span>
<span data-ttu-id="12935-105">Tutti i servizi di Azure forniscono messaggi di registrazione operativi agli utenti per registrare i dettagli relativi alle operazioni di gestione.</span><span class="sxs-lookup"><span data-stu-id="12935-105">All Azure services supply operational logging messages to users to record details related to management operations.</span></span> <span data-ttu-id="12935-106">Nell’analisi di flusso di Azure, queste informazioni possono essere utilizzate per operazioni relative al debug, quali la visualizzazione dello stato del processo, dell’avanzamento del processo, e dei messaggi di errore per rilevare l’avanzamento di un processo nel tempo, dall’avvio, all’elaborazione, fino all’output.</span><span class="sxs-lookup"><span data-stu-id="12935-106">In Azure Stream Analytics, this information can be used for debugging purposes such as viewing job status, job progress, and failure messages to track the progress of a job over time, from start to processing to output.</span></span>

## <a name="find-operation-logs-in-the-azure-management-portal"></a><span data-ttu-id="12935-107">Trovare i log delle operazioni nel portale di gestione di Azure</span><span class="sxs-lookup"><span data-stu-id="12935-107">Find operation logs in the Azure Management portal</span></span>
<span data-ttu-id="12935-108">E’ possibile accedere ai log delle operazioni in due modi:</span><span class="sxs-lookup"><span data-stu-id="12935-108">Operation Logs can be accessed in two ways:</span></span>  

* <span data-ttu-id="12935-109">Dashboard del processo di analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="12935-109">Dashboard of the Stream Analytics job</span></span>  
* <span data-ttu-id="12935-110">Servizi di gestione nel portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="12935-110">Management Services in the Azure Classic portal</span></span>  

## <a name="dashboard-of-the-stream-analytics-job"></a><span data-ttu-id="12935-111">Dashboard del processo di analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="12935-111">Dashboard of the Stream Analytics job</span></span>
<span data-ttu-id="12935-112">Un collegamento per i log di un processo di analisi di flusso corrispondenti viene visualizzato nella scheda Dashboard del processo. Se si fa clic su tale collegamento, si impostano i filtri in modo da visualizzare i log più recenti di tale processo specifico.</span><span class="sxs-lookup"><span data-stu-id="12935-112">A link to the corresponding logs of a Stream Analytics job is displayed on the job’s Dashboard tab. If you click on that link, it will set the filters in a way that it shows latest logs for that specific job.</span></span>

  ![Selezionare i log dei servizi di gestione](./media/stream-analytics-operation-logs/01-stream-analytics-operation-logs.png)  

## <a name="management-services"></a><span data-ttu-id="12935-114">Servizi di gestione</span><span class="sxs-lookup"><span data-stu-id="12935-114">Management Services</span></span>
<span data-ttu-id="12935-115">Per passare manualmente ai log delle operazioni per l'analisi di flusso e altri servizi nel portale di Azure classico:</span><span class="sxs-lookup"><span data-stu-id="12935-115">To manually navigate to the Operation Logs for Stream Analytics and other services in the Azure Classic portal:</span></span>

1. <span data-ttu-id="12935-116">Fare clic su **Servizi di gestione** nel [portale di Azure classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="12935-116">Click on **Management Services** in the [Azure Classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="12935-117">Selezionare **Analisi di flusso** per **Tipo** e il nome del processo per **Nome servizio**.</span><span class="sxs-lookup"><span data-stu-id="12935-117">Select **Stream Analytics** for **Type** and the name of the job for **Service Name**.</span></span>  
   
   ![Selezionare analisi di flusso](./media/stream-analytics-operation-logs/02-stream-analytics-operation-logs.png)  

## <a name="find-audit-logs-in-the-azure-portal"></a><span data-ttu-id="12935-119">Trovare i log di controllo nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="12935-119">Find audit logs in the Azure portal</span></span>
<span data-ttu-id="12935-120">Per trovare i log operativi del processo di analisi di flusso nel portale di Azure, fare clic su **Sfoglia** e selezionare **Log di controllo**.</span><span class="sxs-lookup"><span data-stu-id="12935-120">To find operational logs for your Stream Analytics job in the Azure portal, Click **Browse** and then select **Audit logs**.</span></span>

  ![Selezione analisi di flusso del portale di Azure](./media/stream-analytics-operation-logs/06-stream-analytics-operation-logs.png)  

<span data-ttu-id="12935-122">Verrà aperto un pannello che mostra gli eventi degli ultimi 7 giorni per tutte le risorse nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="12935-122">This will open a blade showing events from the last 7 days for all resources in your subscription.</span></span>  <span data-ttu-id="12935-123">È possibile filtrare per visualizzare gli eventi di un tipo o di un intervallo di tempo specificato selezionando il comando **Filtra** .</span><span class="sxs-lookup"><span data-stu-id="12935-123">You can filter to see events of a specify type or time frame by clicking the **Filter** command.</span></span>

  ![Selezione analisi di flusso del portale di Azure](./media/stream-analytics-operation-logs/07-stream-analytics-operation-logs.png)  

## <a name="get-log-details"></a><span data-ttu-id="12935-125">Ottenere i dettagli dei log</span><span class="sxs-lookup"><span data-stu-id="12935-125">Get log details</span></span>
<span data-ttu-id="12935-126">È possibile filtrare per stato e intervallo di tempo per visualizzare i log per il processo.</span><span class="sxs-lookup"><span data-stu-id="12935-126">You can filter by Time Range and Status to view the logs for your job.</span></span>

<span data-ttu-id="12935-127">Nel portale di gestione di Azure fare clic sul pulsante **Dettagli** nella parte inferiore della finestra per visualizzare altri dettagli sull'evento selezionato.</span><span class="sxs-lookup"><span data-stu-id="12935-127">In the Azure Management portal, click on the **Details** button at the bottom of the window to view more details about a selected event.</span></span> 

  ![Selezionare i dettagli](./media/stream-analytics-operation-logs/03-stream-analytics-operation-logs.png)  

<span data-ttu-id="12935-129">Nel portale di Azure fare clic su una voce di log per visualizzare gli eventi dettagliati al suo interno.</span><span class="sxs-lookup"><span data-stu-id="12935-129">In the Azure portal, click on a log entry to see the detailed events inside it.</span></span>

  ![Selezione dettagli del portale di Azure](./media/stream-analytics-operation-logs/08-stream-analytics-operation-logs.png)  

<span data-ttu-id="12935-131">A questo punto è possibile aprire il pannello **Dettagli** facendo clic sull'evento.</span><span class="sxs-lookup"><span data-stu-id="12935-131">From there, you can open the **Detail** blade by clicking on the event.</span></span>

  ![Selezione dettagli del portale di Azure](./media/stream-analytics-operation-logs/09-stream-analytics-operation-logs.png)  

## <a name="debug-a-failed-job"></a><span data-ttu-id="12935-133">Debug di un processo non riuscito</span><span class="sxs-lookup"><span data-stu-id="12935-133">Debug a failed job</span></span>
<span data-ttu-id="12935-134">Nel portale di gestione di Azure, fare clic sull’icona Cerca e digitare "non riuscito".</span><span class="sxs-lookup"><span data-stu-id="12935-134">In the Azure Management portal, click on the Search icon and type ‘failed’.</span></span> <span data-ttu-id="12935-135">In questo modo si visualizzeranno tutti i log dei processi non riusciti.</span><span class="sxs-lookup"><span data-stu-id="12935-135">This gives a result of all logs with failures.</span></span> 

  ![Eseguire il debug di un processo non riuscito](./media/stream-analytics-operation-logs/04-stream-analytics-operation-logs.png)  

<span data-ttu-id="12935-137">Nel portale di Azure è possibile filtrare per livello di messaggio per visualizzare gli eventi **Critici** .</span><span class="sxs-lookup"><span data-stu-id="12935-137">In the Azure portal, you can filter by level of message to view **Critical** events.</span></span>

  ![Debug del portale di Azure](./media/stream-analytics-operation-logs/10-stream-analytics-operation-logs.png)  

<span data-ttu-id="12935-139">È possibile selezionare uno qualsiasi dei processi non riusciti e fare clic su **Dettagli** per ulteriori informazioni sull'errore.</span><span class="sxs-lookup"><span data-stu-id="12935-139">You can select any one of the failures, and click on the **Details** for more information on the error.</span></span>  <span data-ttu-id="12935-140">Alcuni messaggi di errore forniscono inoltre informazioni su come attenuare il problema.</span><span class="sxs-lookup"><span data-stu-id="12935-140">Some error messages also provide information about how to mitigate the issue.</span></span> 

  ![Dettagli operazione](./media/stream-analytics-operation-logs/05-stream-analytics-operation-logs.png)  

<span data-ttu-id="12935-142">Nel caso in cui sia necessario contattare il [Supporto](https://azure.microsoft.com/support/options/) o fornire informazioni al team tramite il [forum MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics), tenere presenti i dettagli dell'operazione, in particolare l’**ID di correlazione**.</span><span class="sxs-lookup"><span data-stu-id="12935-142">In case you need to contact [Support](https://azure.microsoft.com/support/options/) or provide information to the team via the [MSDN forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics), please note the Operation Details, specifically the **Correlation ID**.</span></span> 

## <a name="get-help"></a><span data-ttu-id="12935-143">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="12935-143">Get help</span></span>
<span data-ttu-id="12935-144">Per assistenza, provare il [Forum di Analisi di flusso di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="12935-144">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="12935-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="12935-145">Next steps</span></span>
* [<span data-ttu-id="12935-146">Introduzione ad Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="12935-146">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="12935-147">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="12935-147">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="12935-148">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="12935-148">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="12935-149">Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="12935-149">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="12935-150">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="12935-150">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

