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
# <a name="understand-stream-analytics-job-monitoring-and-how-toomonitor-queries"></a><span data-ttu-id="6c2b8-104">Comprendere il monitoraggio di processo di flusso Analitica e la modalità query toomonitor</span><span class="sxs-lookup"><span data-stu-id="6c2b8-104">Understand Stream Analytics job monitoring and how toomonitor queries</span></span>

## <a name="introduction-hello-monitor-page"></a><span data-ttu-id="6c2b8-105">Introduzione: pagina di monitoraggio hello</span><span class="sxs-lookup"><span data-stu-id="6c2b8-105">Introduction: hello monitor page</span></span>
<span data-ttu-id="6c2b8-106">Hello portale di Azure sia superficie metriche chiave delle prestazioni che è possono toomonitor utilizzato e risolvere i problemi delle prestazioni di query e processi.</span><span class="sxs-lookup"><span data-stu-id="6c2b8-106">hello Azure portal both surface key performance metrics that can be used toomonitor and troubleshoot your query and job performance.</span></span> <span data-ttu-id="6c2b8-107">toosee queste metriche, individuare il processo di flusso Analitica toohello si è interessati a visualizzare le metriche per e hello vista **monitoraggio** sezione nella pagina di panoramica hello.</span><span class="sxs-lookup"><span data-stu-id="6c2b8-107">toosee these metrics, browse toohello Stream Analytics job you are interested in seeing metrics for and view hello **Monitoring** section on hello Overview page.</span></span>  

![Collegamento al monitoraggio](./media/stream-analytics-monitoring/02-stream-analytics-monitoring-block.png)

<span data-ttu-id="6c2b8-109">finestra Hello verrà visualizzato come illustrato:</span><span class="sxs-lookup"><span data-stu-id="6c2b8-109">hello window will appear as shown:</span></span>

![Monitoraggio del dashboard dei processi](./media/stream-analytics-monitoring/01-stream-analytics-monitoring.png)  

## <a name="metrics-available-for-stream-analytics"></a><span data-ttu-id="6c2b8-111">Metriche disponibili per l'analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="6c2b8-111">Metrics available for Stream Analytics</span></span>
| <span data-ttu-id="6c2b8-112">Metrica</span><span class="sxs-lookup"><span data-stu-id="6c2b8-112">Metric</span></span>                 | <span data-ttu-id="6c2b8-113">Definizione</span><span class="sxs-lookup"><span data-stu-id="6c2b8-113">Definition</span></span>                               |
| ---------------------- | ---------------------------------------- |
| <span data-ttu-id="6c2b8-114">% utilizzo unità di streaming</span><span class="sxs-lookup"><span data-stu-id="6c2b8-114">SU % Utilization</span></span>       | <span data-ttu-id="6c2b8-115">utilizzo di Hello di hello unità di Streaming assegnato tooa processo dalla scheda Scala hello del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="6c2b8-115">hello utilization of hello Streaming Unit(s) assigned tooa job from hello Scale tab of hello job.</span></span> <span data-ttu-id="6c2b8-116">Se questo indicatore raggiunge l'80% o più, esiste una forte probabilità che l'elaborazione di eventi possa essere ritardata o interrotta.</span><span class="sxs-lookup"><span data-stu-id="6c2b8-116">Should this indicator reach 80%, or above, there is high probability that event processing may be delayed or stopped making progress.</span></span> |
| <span data-ttu-id="6c2b8-117">Eventi di input</span><span class="sxs-lookup"><span data-stu-id="6c2b8-117">Input Events</span></span>           | <span data-ttu-id="6c2b8-118">Quantità di dati ricevuti dal processo di flusso Analitica hello, numero di eventi.</span><span class="sxs-lookup"><span data-stu-id="6c2b8-118">Amount of data received by hello Stream Analytics job, in number of events.</span></span> <span data-ttu-id="6c2b8-119">Può essere utilizzato toovalidate che gli eventi vengono inviati toohello origine di input.</span><span class="sxs-lookup"><span data-stu-id="6c2b8-119">This can be used toovalidate that events are being sent toohello input source.</span></span> |
| <span data-ttu-id="6c2b8-120">Eventi di output</span><span class="sxs-lookup"><span data-stu-id="6c2b8-120">Output Events</span></span>          | <span data-ttu-id="6c2b8-121">Quantità di dati inviati dal hello Analitica flusso processo toohello destinazione di output, in numero di eventi.</span><span class="sxs-lookup"><span data-stu-id="6c2b8-121">Amount of data sent by hello Stream Analytics job toohello output target, in number of events.</span></span> |
| <span data-ttu-id="6c2b8-122">Eventi non ordinati</span><span class="sxs-lookup"><span data-stu-id="6c2b8-122">Out-of-Order Events</span></span>    | <span data-ttu-id="6c2b8-123">Numero di eventi non ordinati che sono stati eliminati o ha un timestamp, in base a criteri di ordinamento eventi hello ricevuti.</span><span class="sxs-lookup"><span data-stu-id="6c2b8-123">Number of events received out of order that were either dropped or given an adjusted timestamp, based on hello Event Ordering Policy.</span></span> <span data-ttu-id="6c2b8-124">Questo può essere influenzato dalla configurazione hello di impostazione della finestra di tolleranza ordine hello.</span><span class="sxs-lookup"><span data-stu-id="6c2b8-124">This can be impacted by hello configuration of hello Out of Order Tolerance Window setting.</span></span> |
| <span data-ttu-id="6c2b8-125">Errori di conversione dati</span><span class="sxs-lookup"><span data-stu-id="6c2b8-125">Data Conversion Errors</span></span> | <span data-ttu-id="6c2b8-126">numero di errori di conversione dei dati rilevati da un processo di Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="6c2b8-126">Number of data conversion errors incurred by a Stream Analytics job.</span></span> |
| <span data-ttu-id="6c2b8-127">Errori di runtime</span><span class="sxs-lookup"><span data-stu-id="6c2b8-127">Runtime Errors</span></span>         | <span data-ttu-id="6c2b8-128">numero totale di Hello di errori che si verificano durante l'esecuzione di un processo di flusso Analitica.</span><span class="sxs-lookup"><span data-stu-id="6c2b8-128">hello total number of errors that happen during execution of a Stream Analytics job.</span></span> |
| <span data-ttu-id="6c2b8-129">Ultimi eventi di input</span><span class="sxs-lookup"><span data-stu-id="6c2b8-129">Late Input Events</span></span>      | <span data-ttu-id="6c2b8-130">Numero di eventi che arrivano in ritardo di origine di hello che modo sono stati eliminati o al relativo timestamp è stato modificato, in base alla configurazione di criteri di ordinamento eventi hello dell'impostazione tardiva finestra di tolleranza per arrivo hello.</span><span class="sxs-lookup"><span data-stu-id="6c2b8-130">Number of events arriving late from hello source which have either been dropped or their timestamp has been adjusted, based on hello Event Ordering Policy configuration of hello Late Arrival Tolerance Window setting.</span></span> |
| <span data-ttu-id="6c2b8-131">Richieste di funzioni</span><span class="sxs-lookup"><span data-stu-id="6c2b8-131">Function Requests</span></span>      | <span data-ttu-id="6c2b8-132">Numero di chiamate toohello funzione Azure Machine Learning (se presente).</span><span class="sxs-lookup"><span data-stu-id="6c2b8-132">Number of calls toohello Azure Machine Learning function (if present).</span></span> |
| <span data-ttu-id="6c2b8-133">Richieste di funzioni non riuscite</span><span class="sxs-lookup"><span data-stu-id="6c2b8-133">Failed Function Requests</span></span> | <span data-ttu-id="6c2b8-134">Numero di chiamate non riuscite alla funzione di Azure Machine Learning (se presente).</span><span class="sxs-lookup"><span data-stu-id="6c2b8-134">Number of failed Azure Machine Learning function calls (if present).</span></span> |
| <span data-ttu-id="6c2b8-135">Eventi di funzioni</span><span class="sxs-lookup"><span data-stu-id="6c2b8-135">Function Events</span></span>        | <span data-ttu-id="6c2b8-136">Numero di eventi inviati funzione Azure Machine Learning toohello (se presente).</span><span class="sxs-lookup"><span data-stu-id="6c2b8-136">Number of events sent toohello Azure Machine Learning function (if present).</span></span> |
| <span data-ttu-id="6c2b8-137">Byte evento di input</span><span class="sxs-lookup"><span data-stu-id="6c2b8-137">Input Event Bytes</span></span>      | <span data-ttu-id="6c2b8-138">Quantità di dati ricevuti dal processo di flusso Analitica hello, in byte.</span><span class="sxs-lookup"><span data-stu-id="6c2b8-138">Amount of data received by hello Stream Analytics job, in bytes.</span></span> <span data-ttu-id="6c2b8-139">Può essere utilizzato toovalidate che gli eventi vengono inviati toohello origine di input.</span><span class="sxs-lookup"><span data-stu-id="6c2b8-139">This can be used toovalidate that events are being sent toohello input source.</span></span> |


## <a name="customizing-monitoring-in-hello-azure-portal"></a><span data-ttu-id="6c2b8-140">Personalizzazione di monitoraggio nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="6c2b8-140">Customizing Monitoring in hello Azure portal</span></span>
<span data-ttu-id="6c2b8-141">È possibile modificare il tipo di hello del grafico, metriche visualizzate, intervallo di tempo nelle impostazioni di modifica grafico hello.</span><span class="sxs-lookup"><span data-stu-id="6c2b8-141">You can adjust hello type of chart, metrics shown, and time range in hello Edit Chart settings.</span></span> <span data-ttu-id="6c2b8-142">Per informazioni dettagliate, vedere [come tooCustomize monitoraggio](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="6c2b8-142">For details, see [How tooCustomize Monitoring](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span></span>

  ![Monitoraggio query, grafico cronologico](./media/stream-analytics-monitoring/08-stream-analytics-monitoring.png)  


## <a name="get-help"></a><span data-ttu-id="6c2b8-144">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="6c2b8-144">Get help</span></span>
<span data-ttu-id="6c2b8-145">Per assistenza, provare il [Forum di Analisi di flusso di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="6c2b8-145">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c2b8-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6c2b8-146">Next steps</span></span>
* [<span data-ttu-id="6c2b8-147">Introduzione tooAzure flusso Analitica</span><span class="sxs-lookup"><span data-stu-id="6c2b8-147">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="6c2b8-148">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="6c2b8-148">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="6c2b8-149">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="6c2b8-149">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="6c2b8-150">Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="6c2b8-150">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="6c2b8-151">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="6c2b8-151">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

