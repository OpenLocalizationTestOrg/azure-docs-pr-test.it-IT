---
title: Come avviare processi di streaming in Analisi di flusso | Documentazione Microsoft
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
ms.openlocfilehash: 9a3ff37a893b0f29a2ac2eda6cd50687ee779ead
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-run-a-streaming-job-in-azure-stream-analytics"></a><span data-ttu-id="0a085-104">Come eseguire un processo di streaming in Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="0a085-104">How to run a streaming job in Azure Stream Analytics</span></span>
<span data-ttu-id="0a085-105">Dopo che sono stati specificati un processo di input, una query e un output, è possibile avviare il processo dell’analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="0a085-105">When a job input, query and output have all been specified you can start the Stream Analytics job.</span></span>

<span data-ttu-id="0a085-106">Per avviare il processo:</span><span class="sxs-lookup"><span data-stu-id="0a085-106">To start your job:</span></span>

1. <span data-ttu-id="0a085-107">Nel portale di Azure classico, dal dashboard del processo, fare clic su **Start** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="0a085-107">In the Azure Classic portal, from the job dashboard, click **Start** at the bottom of the page.</span></span>
   
   ![Pulsante Avvia processo](./media/stream-analytics-run-a-job/1-stream-analytics-run-a-job.png)  
   
   <span data-ttu-id="0a085-109">Nel portale di Azure fare clic su **Start** nella parte superiore della pagina del processo.</span><span class="sxs-lookup"><span data-stu-id="0a085-109">In the Azure portal, click **Start** at the top of your job page.</span></span>
   
   ![Portale di Azure, Pulsante Avvia processo](./media/stream-analytics-run-a-job/4-stream-analytics-run-a-job.png)  
2. <span data-ttu-id="0a085-111">Specificare un valore per **Avvia output** per determinare quando questo processo inizierà a produrre output.</span><span class="sxs-lookup"><span data-stu-id="0a085-111">Specify a **Start Output** value to determine when this job will start producing output.</span></span> <span data-ttu-id="0a085-112">L'impostazione predefinita per i processi che non sono stati precedentemente avviati è **Ora di inizio processo**, il che significa che il processo avvia immediatamente l'elaborazione dati.</span><span class="sxs-lookup"><span data-stu-id="0a085-112">The default setting for jobs that have not previously been started is **Job Start Time**, which means that the job will immediately start processing data.</span></span> <span data-ttu-id="0a085-113">È inoltre possibile specificare un tempo **personalizzato** passato (per l'utilizzo di dati cronologici) o futuro (per posticipare l'elaborazione a un secondo momento).</span><span class="sxs-lookup"><span data-stu-id="0a085-113">You can also specify a **Custom** time in the past (for consuming historical data) or the future (to delay processing until a future time).</span></span> <span data-ttu-id="0a085-114">Nei casi in cui un processo è stato precedentemente avviato e arrestato, l'opzione **Ultimo arresto** è disponibile per consentire di riprendere il processo dall'ultima data di output ed evitare la perdita di dati.</span><span class="sxs-lookup"><span data-stu-id="0a085-114">For cases when a job has been previously started and stopped, the option **Last Stopped Time** is available in order to resume the job from the last output time and avoid data loss.</span></span>  
   
   ![Ora di avvio del processo di streaming](./media/stream-analytics-run-a-job/2-stream-analytics-run-a-job.png)  
   
   ![Portale di Azure, ora di avvio del processo di streaming](./media/stream-analytics-run-a-job/5-stream-analytics-run-a-job.png)  
3. <span data-ttu-id="0a085-117">Confermare la selezione.</span><span class="sxs-lookup"><span data-stu-id="0a085-117">Confirm your selection.</span></span> <span data-ttu-id="0a085-118">Lo stato del processo cambierà in *Avvio* e passerà rapidamente a *In esecuzione* dopo aver avviato il processo.</span><span class="sxs-lookup"><span data-stu-id="0a085-118">The job status will change to *Starting* and will shortly move to *Running* once the job has started.</span></span> <span data-ttu-id="0a085-119">È possibile monitorare lo stato di avanzamento dell'operazione di **Avvio** nell'**Hub di notifica**:</span><span class="sxs-lookup"><span data-stu-id="0a085-119">You can monitor the progress of the **Start** operation in the **Notification Hub**:</span></span>
   
   ![avanzamento del processo di streaming](./media/stream-analytics-run-a-job/3-stream-analytics-run-a-job.png)  
   
   ![Portale di Azure, stato del processo di streaming](./media/stream-analytics-run-a-job/6-stream-analytics-run-a-job.png)  

## <a name="get-help"></a><span data-ttu-id="0a085-122">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="0a085-122">Get help</span></span>
<span data-ttu-id="0a085-123">Per assistenza, provare il [Forum di Analisi di flusso di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="0a085-123">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a085-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0a085-124">Next steps</span></span>
* [<span data-ttu-id="0a085-125">Introduzione ad Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="0a085-125">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="0a085-126">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="0a085-126">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="0a085-127">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="0a085-127">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="0a085-128">Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="0a085-128">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="0a085-129">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="0a085-129">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

