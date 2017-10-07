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
# <a name="how-toorun-a-streaming-job-in-azure-stream-analytics"></a><span data-ttu-id="b965c-104">Come un flusso toorun processo Analitica di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="b965c-104">How toorun a streaming job in Azure Stream Analytics</span></span>
<span data-ttu-id="b965c-105">Quando un processo per l'input, output e query sono state specificate tutte che è possibile avviare il processo di flusso Analitica hello.</span><span class="sxs-lookup"><span data-stu-id="b965c-105">When a job input, query and output have all been specified you can start hello Stream Analytics job.</span></span>

<span data-ttu-id="b965c-106">toostart il processo:</span><span class="sxs-lookup"><span data-stu-id="b965c-106">toostart your job:</span></span>

1. <span data-ttu-id="b965c-107">Nel portale di Azure classico hello, dal dashboard processo hello, fare clic su **avviare** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="b965c-107">In hello Azure Classic portal, from hello job dashboard, click **Start** at hello bottom of hello page.</span></span>
   
   ![Pulsante Avvia processo](./media/stream-analytics-run-a-job/1-stream-analytics-run-a-job.png)  
   
   <span data-ttu-id="b965c-109">Nel portale di Azure hello, fare clic su **avviare** nella parte superiore di hello della pagina di processo.</span><span class="sxs-lookup"><span data-stu-id="b965c-109">In hello Azure portal, click **Start** at hello top of your job page.</span></span>
   
   ![Portale di Azure, Pulsante Avvia processo](./media/stream-analytics-run-a-job/4-stream-analytics-run-a-job.png)  
2. <span data-ttu-id="b965c-111">Specificare un **avviare Output** toodetermine valore quando questo processo verrà avviata la produzione di output.</span><span class="sxs-lookup"><span data-stu-id="b965c-111">Specify a **Start Output** value toodetermine when this job will start producing output.</span></span> <span data-ttu-id="b965c-112">Hello impostazione predefinita per i processi che non sono già state avviate è **Job Start Time**, il che significa che il processo di hello avviare immediatamente l'elaborazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="b965c-112">hello default setting for jobs that have not previously been started is **Job Start Time**, which means that hello job will immediately start processing data.</span></span> <span data-ttu-id="b965c-113">È inoltre possibile specificare un **personalizzato** tempo in hello passato (per l'utilizzo di dati cronologici) o hello futura (toodelay l'elaborazione fino a un momento futuro).</span><span class="sxs-lookup"><span data-stu-id="b965c-113">You can also specify a **Custom** time in hello past (for consuming historical data) or hello future (toodelay processing until a future time).</span></span> <span data-ttu-id="b965c-114">Per i casi in cui un processo è stato avviato e arrestato, in precedenza hello opzione **ora ultimo arresto** è disponibile nel processo di ordine tooresume hello dall'ultima ora di output di hello ed evitare la perdita di dati.</span><span class="sxs-lookup"><span data-stu-id="b965c-114">For cases when a job has been previously started and stopped, hello option **Last Stopped Time** is available in order tooresume hello job from hello last output time and avoid data loss.</span></span>  
   
   ![Ora di avvio del processo di streaming](./media/stream-analytics-run-a-job/2-stream-analytics-run-a-job.png)  
   
   ![Portale di Azure, ora di avvio del processo di streaming](./media/stream-analytics-run-a-job/5-stream-analytics-run-a-job.png)  
3. <span data-ttu-id="b965c-117">Confermare la selezione.</span><span class="sxs-lookup"><span data-stu-id="b965c-117">Confirm your selection.</span></span> <span data-ttu-id="b965c-118">lo stato del processo Hello cambierà troppo*iniziale* e a breve verrà spostata troppo*esecuzione* una volta avviato il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="b965c-118">hello job status will change too*Starting* and will shortly move too*Running* once hello job has started.</span></span> <span data-ttu-id="b965c-119">È possibile monitorare lo stato di avanzamento hello di hello **avviare** operazione hello **Hub di notifica**:</span><span class="sxs-lookup"><span data-stu-id="b965c-119">You can monitor hello progress of hello **Start** operation in hello **Notification Hub**:</span></span>
   
   ![avanzamento del processo di streaming](./media/stream-analytics-run-a-job/3-stream-analytics-run-a-job.png)  
   
   ![Portale di Azure, stato del processo di streaming](./media/stream-analytics-run-a-job/6-stream-analytics-run-a-job.png)  

## <a name="get-help"></a><span data-ttu-id="b965c-122">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="b965c-122">Get help</span></span>
<span data-ttu-id="b965c-123">Per assistenza, provare il [Forum di Analisi di flusso di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="b965c-123">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="b965c-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b965c-124">Next steps</span></span>
* [<span data-ttu-id="b965c-125">Introduzione tooAzure flusso Analitica</span><span class="sxs-lookup"><span data-stu-id="b965c-125">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="b965c-126">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="b965c-126">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="b965c-127">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="b965c-127">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="b965c-128">Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="b965c-128">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="b965c-129">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="b965c-129">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

