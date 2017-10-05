---
title: Informazioni sul monitoraggio dei processi di Analisi di flusso | Documentazione Microsoft
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
ms.openlocfilehash: 13d96807a5591ec88deda19ea73cfedc07078433
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="understand-stream-analytics-job-monitoring-and-how-to-monitor-queries"></a><span data-ttu-id="8df2d-104">Informazioni sul monitoraggio dei processi di Analisi di flusso e su come monitorare le query</span><span class="sxs-lookup"><span data-stu-id="8df2d-104">Understand Stream Analytics job monitoring and how to monitor queries</span></span>

## <a name="introduction-the-monitor-page"></a><span data-ttu-id="8df2d-105">Introduzione: Pagina di monitoraggio</span><span class="sxs-lookup"><span data-stu-id="8df2d-105">Introduction: The monitor page</span></span>
<span data-ttu-id="8df2d-106">Il portale di Azure evidenzia le metriche delle prestazioni chiave che possono essere usate per monitorare e consente di risolvere i problemi di prestazioni delle query e dei processi.</span><span class="sxs-lookup"><span data-stu-id="8df2d-106">The Azure portal both surface key performance metrics that can be used to monitor and troubleshoot your query and job performance.</span></span> <span data-ttu-id="8df2d-107">Per visualizzare queste metriche, esplorare il processo di analisi di flusso di cui si desidera vedere le metriche e visualizzare la sezione **Monitoraggio** nella pagina della panoramica.</span><span class="sxs-lookup"><span data-stu-id="8df2d-107">To see these metrics, browse to the Stream Analytics job you are interested in seeing metrics for and view the **Monitoring** section on the Overview page.</span></span>  

![Collegamento al monitoraggio](./media/stream-analytics-monitoring/02-stream-analytics-monitoring-block.png)

<span data-ttu-id="8df2d-109">Verrà visualizzata la finestra mostrata di seguito:</span><span class="sxs-lookup"><span data-stu-id="8df2d-109">The window will appear as shown:</span></span>

![Monitoraggio del dashboard dei processi](./media/stream-analytics-monitoring/01-stream-analytics-monitoring.png)  

## <a name="metrics-available-for-stream-analytics"></a><span data-ttu-id="8df2d-111">Metriche disponibili per l'analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="8df2d-111">Metrics available for Stream Analytics</span></span>
| <span data-ttu-id="8df2d-112">Metrica</span><span class="sxs-lookup"><span data-stu-id="8df2d-112">Metric</span></span>                 | <span data-ttu-id="8df2d-113">Definizione</span><span class="sxs-lookup"><span data-stu-id="8df2d-113">Definition</span></span>                               |
| ---------------------- | ---------------------------------------- |
| <span data-ttu-id="8df2d-114">% utilizzo unità di streaming</span><span class="sxs-lookup"><span data-stu-id="8df2d-114">SU % Utilization</span></span>       | <span data-ttu-id="8df2d-115">L'utilizzo delle unità di streaming assegnate a un processo dalla scheda Scalabilità del processo.</span><span class="sxs-lookup"><span data-stu-id="8df2d-115">The utilization of the Streaming Unit(s) assigned to a job from the Scale tab of the job.</span></span> <span data-ttu-id="8df2d-116">Se questo indicatore raggiunge l'80% o più, esiste una forte probabilità che l'elaborazione di eventi possa essere ritardata o interrotta.</span><span class="sxs-lookup"><span data-stu-id="8df2d-116">Should this indicator reach 80%, or above, there is high probability that event processing may be delayed or stopped making progress.</span></span> |
| <span data-ttu-id="8df2d-117">Eventi di input</span><span class="sxs-lookup"><span data-stu-id="8df2d-117">Input Events</span></span>           | <span data-ttu-id="8df2d-118">Quantità di dati ricevuta dal processo di Analisi di flusso, in termini di numero di eventi.</span><span class="sxs-lookup"><span data-stu-id="8df2d-118">Amount of data received by the Stream Analytics job, in number of events.</span></span> <span data-ttu-id="8df2d-119">Può essere usata per convalidare l'invio degli eventi all'origine di input.</span><span class="sxs-lookup"><span data-stu-id="8df2d-119">This can be used to validate that events are being sent to the input source.</span></span> |
| <span data-ttu-id="8df2d-120">Eventi di output</span><span class="sxs-lookup"><span data-stu-id="8df2d-120">Output Events</span></span>          | <span data-ttu-id="8df2d-121">Quantità di dati inviata dal processo di Analisi di flusso alla destinazione di output, in termini di numero di eventi.</span><span class="sxs-lookup"><span data-stu-id="8df2d-121">Amount of data sent by the Stream Analytics job to the output target, in number of events.</span></span> |
| <span data-ttu-id="8df2d-122">Eventi non ordinati</span><span class="sxs-lookup"><span data-stu-id="8df2d-122">Out-of-Order Events</span></span>    | <span data-ttu-id="8df2d-123">Numero di eventi non ordinati ricevuti che sono stati eliminati o a cui è stato assegnato un timestamp modificato, in base ai Criteri di ordinamento eventi.</span><span class="sxs-lookup"><span data-stu-id="8df2d-123">Number of events received out of order that were either dropped or given an adjusted timestamp, based on the Event Ordering Policy.</span></span> <span data-ttu-id="8df2d-124">Può essere influenzato dalla configurazione dell'impostazione della Finestra di tolleranza elementi non in ordine.</span><span class="sxs-lookup"><span data-stu-id="8df2d-124">This can be impacted by the configuration of the Out of Order Tolerance Window setting.</span></span> |
| <span data-ttu-id="8df2d-125">Errori di conversione dati</span><span class="sxs-lookup"><span data-stu-id="8df2d-125">Data Conversion Errors</span></span> | <span data-ttu-id="8df2d-126">numero di errori di conversione dei dati rilevati da un processo di Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="8df2d-126">Number of data conversion errors incurred by a Stream Analytics job.</span></span> |
| <span data-ttu-id="8df2d-127">Errori di runtime</span><span class="sxs-lookup"><span data-stu-id="8df2d-127">Runtime Errors</span></span>         | <span data-ttu-id="8df2d-128">Numero totale di errori che si sono verificati durante l'esecuzione di un processo di Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="8df2d-128">The total number of errors that happen during execution of a Stream Analytics job.</span></span> |
| <span data-ttu-id="8df2d-129">Ultimi eventi di input</span><span class="sxs-lookup"><span data-stu-id="8df2d-129">Late Input Events</span></span>      | <span data-ttu-id="8df2d-130">Numero di eventi che arrivano in ritardo dall'origine che sono stati eliminati oppure il cui timestamp è stato modificato, in base alla configurazione dei Criteri di ordinamento eventi dell'impostazione della Finestra di tolleranza elementi non in ordine.</span><span class="sxs-lookup"><span data-stu-id="8df2d-130">Number of events arriving late from the source which have either been dropped or their timestamp has been adjusted, based on the Event Ordering Policy configuration of the Late Arrival Tolerance Window setting.</span></span> |
| <span data-ttu-id="8df2d-131">Richieste di funzioni</span><span class="sxs-lookup"><span data-stu-id="8df2d-131">Function Requests</span></span>      | <span data-ttu-id="8df2d-132">Numero di chiamate alla funzione di Azure Machine Learning (se presente).</span><span class="sxs-lookup"><span data-stu-id="8df2d-132">Number of calls to the Azure Machine Learning function (if present).</span></span> |
| <span data-ttu-id="8df2d-133">Richieste di funzioni non riuscite</span><span class="sxs-lookup"><span data-stu-id="8df2d-133">Failed Function Requests</span></span> | <span data-ttu-id="8df2d-134">Numero di chiamate non riuscite alla funzione di Azure Machine Learning (se presente).</span><span class="sxs-lookup"><span data-stu-id="8df2d-134">Number of failed Azure Machine Learning function calls (if present).</span></span> |
| <span data-ttu-id="8df2d-135">Eventi di funzioni</span><span class="sxs-lookup"><span data-stu-id="8df2d-135">Function Events</span></span>        | <span data-ttu-id="8df2d-136">Numero di chiamate inviate alla funzione di Azure Machine Learning (se presente).</span><span class="sxs-lookup"><span data-stu-id="8df2d-136">Number of events sent to the Azure Machine Learning function (if present).</span></span> |
| <span data-ttu-id="8df2d-137">Byte evento di input</span><span class="sxs-lookup"><span data-stu-id="8df2d-137">Input Event Bytes</span></span>      | <span data-ttu-id="8df2d-138">Quantità di dati ricevuta dal processo di Analisi di flusso, in termini di byte.</span><span class="sxs-lookup"><span data-stu-id="8df2d-138">Amount of data received by the Stream Analytics job, in bytes.</span></span> <span data-ttu-id="8df2d-139">Può essere usata per convalidare l'invio degli eventi all'origine di input.</span><span class="sxs-lookup"><span data-stu-id="8df2d-139">This can be used to validate that events are being sent to the input source.</span></span> |


## <a name="customizing-monitoring-in-the-azure-portal"></a><span data-ttu-id="8df2d-140">Personalizzazione del monitoraggio nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="8df2d-140">Customizing Monitoring in the Azure portal</span></span>
<span data-ttu-id="8df2d-141">È possibile modificare il tipo di grafico, le metriche visualizzate e l’intervallo di tempo nelle impostazioni di Modifica grafico.</span><span class="sxs-lookup"><span data-stu-id="8df2d-141">You can adjust the type of chart, metrics shown, and time range in the Edit Chart settings.</span></span> <span data-ttu-id="8df2d-142">Per altre informazioni, vedere [How to Customize Monitoring](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) (Come personalizzare il monitoraggio).</span><span class="sxs-lookup"><span data-stu-id="8df2d-142">For details, see [How to Customize Monitoring](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span></span>

  ![Monitoraggio query, grafico cronologico](./media/stream-analytics-monitoring/08-stream-analytics-monitoring.png)  


## <a name="get-help"></a><span data-ttu-id="8df2d-144">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="8df2d-144">Get help</span></span>
<span data-ttu-id="8df2d-145">Per assistenza, provare il [Forum di Analisi di flusso di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="8df2d-145">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="8df2d-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8df2d-146">Next steps</span></span>
* [<span data-ttu-id="8df2d-147">Introduzione ad Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="8df2d-147">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="8df2d-148">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="8df2d-148">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="8df2d-149">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="8df2d-149">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="8df2d-150">Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="8df2d-150">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="8df2d-151">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="8df2d-151">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

