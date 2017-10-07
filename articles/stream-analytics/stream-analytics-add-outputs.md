---
title: Genera dati tooconfigure aaaHow per i processi di flusso Analitica | Documenti Microsoft
description: Configurare gli output per i processi di Analisi di flusso | segmento del percorso di apprendimento.
keywords: output dei dati, spostamento dei dati
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 3bbea3da-bfce-4af1-a15e-d4b23874034f
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/26/2017
ms.author: samacha
ms.openlocfilehash: c5d89e9e9f9211d3e778580c071dd53d56aed9fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-data-outputs-for-stream-analytics-jobs"></a><span data-ttu-id="d5d05-104">La modalità di output tooconfigure dati per i processi di flusso Analitica</span><span class="sxs-lookup"><span data-stu-id="d5d05-104">How tooconfigure data outputs for Stream Analytics jobs</span></span>

<span data-ttu-id="d5d05-105">I processi di flusso Analitica Azure possono essere connesso tooone o più output di dati, che definiscono un sink di dati esistente tooan connessione.</span><span class="sxs-lookup"><span data-stu-id="d5d05-105">Azure Stream Analytics jobs can be connected tooone or more data outputs, which define a connection tooan existing data sink.</span></span> <span data-ttu-id="d5d05-106">Durante il processo di flusso Analitica elabora e trasforma i dati in ingresso, un flusso di dati di eventi di output viene scritto l'output del processo tooyour.</span><span class="sxs-lookup"><span data-stu-id="d5d05-106">As your Stream Analytics job processes and transforms incoming data, a stream of data output events is written tooyour job's output.</span></span>

<span data-ttu-id="d5d05-107">Output di dati di flusso Analitica può essere utilizzato toosource di dashboard in tempo reale o avvisi, trigger flussi di lavoro lo spostamento dei dati o semplicemente i dati di archiviazione per l'elaborazione batch in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="d5d05-107">Stream Analytics data outputs can be used toosource real-time dashboards or alerts, trigger data movement workflows, or simply archive data for batch processing later on.</span></span> <span data-ttu-id="d5d05-108">L'analisi di flusso dispone dell'integrazione di prima classe con diversi servizi di Azure, che sono documentati in dettaglio di seguito.</span><span class="sxs-lookup"><span data-stu-id="d5d05-108">Stream Analytics has first class integration with several Azure services, which are documented in detail here.</span></span>

<span data-ttu-id="d5d05-109">tooadd un processo di flusso Analitica tooyour output:</span><span class="sxs-lookup"><span data-stu-id="d5d05-109">tooadd an output tooyour Stream Analytics job:</span></span>

1. <span data-ttu-id="d5d05-110">In hello [portale di Azure](https://portal.azure.com), aprire il processo e fare clic su **output** e quindi fare clic su **Aggiungi** nel Pannello di output di hello che viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="d5d05-110">In hello [Azure portal](https://portal.azure.com), open your job and click **Outputs** and then click **Add** in hello Outputs blade that appears.</span></span>
   
    ![Aggiungere output](./media/stream-analytics-add-outputs/1-stream-analytics-add-outputs.png)  
   
2. <span data-ttu-id="d5d05-112">Specificare un nome descrittivo per l'output di hello **Alias di Output** casella.</span><span class="sxs-lookup"><span data-stu-id="d5d05-112">Provide a friendly name for this output in hello **Output Alias** box.</span></span> <span data-ttu-id="d5d05-113">Questo nome può essere utilizzato nella query del processo in un secondo momento nell'output di toohello toorefer.</span><span class="sxs-lookup"><span data-stu-id="d5d05-113">This name can be used in your job's query later on toorefer toohello output.</span></span>  
   
    <span data-ttu-id="d5d05-114">Compilare il resto di hello dell'output di hello necessario connessione proprietà tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="d5d05-114">Fill in hello rest of hello required connection properties tooconnect tooyour output.</span></span>  <span data-ttu-id="d5d05-115">Questi campi variano in base al tipo di output e vengono definiti in modo dettagliato di seguito.</span><span class="sxs-lookup"><span data-stu-id="d5d05-115">These fields vary by output type and are defined in detail here.</span></span>  
   
    ![Scegliere il tipo di spostamento dei dati](./media/stream-analytics-add-outputs/2-stream-analytics-add-outputs.png)  
   
3. <span data-ttu-id="d5d05-117">In base al tipo di output di hello, potrebbe essere necessario toospecify come dati hello viene serializzati o formattati.</span><span class="sxs-lookup"><span data-stu-id="d5d05-117">Depending on hello output type, you may need toospecify how hello data is serialized or formatted.</span></span> <span data-ttu-id="d5d05-118">le impostazioni di serializzazione specifici Hello per ogni tipo di output sono documentate di seguito.</span><span class="sxs-lookup"><span data-stu-id="d5d05-118">hello specific serialization settings for each output type are documented here.</span></span>
   
    <span data-ttu-id="d5d05-119">Compilare il resto di hello di origine dei dati tooyour proprietà tooconnect hello necessarie per la connessione.</span><span class="sxs-lookup"><span data-stu-id="d5d05-119">Fill in hello rest of hello required connection properties tooconnect tooyour data source.</span></span> <span data-ttu-id="d5d05-120">Questi campi variano in base al tipo del tipo di input e di origine e sono definiti in modo dettagliato in hello [articolo Crea processo](stream-analytics-create-a-job.md).</span><span class="sxs-lookup"><span data-stu-id="d5d05-120">These fields vary by type of input and source type and are defined in detail in hello [Create Job article](stream-analytics-create-a-job.md).</span></span>  

> [!Note]
>
> <span data-ttu-id="d5d05-121">Qualsiasi processo di aggiunta toohello elemento di output, deve esistere prima hello processo viene avviato e gli eventi di inizio propagazione.</span><span class="sxs-lookup"><span data-stu-id="d5d05-121">Any output element added toohello job, must exist before hello job is started and events start flowing.</span></span> <span data-ttu-id="d5d05-122">Ad esempio, se si utilizza l'archiviazione Blob come output, il processo di hello non creerà un account di archiviazione automaticamente.</span><span class="sxs-lookup"><span data-stu-id="d5d05-122">For example, if you use Blob storage as an output, hello job will not create a storage account automatically.</span></span> <span data-ttu-id="d5d05-123">È necessario che toobe creato dall'utente hello prima dell'avvio del processo ASA hello.</span><span class="sxs-lookup"><span data-stu-id="d5d05-123">It needs toobe created by hello user before hello ASA job is started.</span></span>
> 
 

## <a name="get-help"></a><span data-ttu-id="d5d05-124">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="d5d05-124">Get help</span></span>
<span data-ttu-id="d5d05-125">Per assistenza, provare il [Forum di Analisi di flusso di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="d5d05-125">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5d05-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d5d05-126">Next steps</span></span>
* [<span data-ttu-id="d5d05-127">Introduzione tooAzure flusso Analitica</span><span class="sxs-lookup"><span data-stu-id="d5d05-127">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="d5d05-128">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="d5d05-128">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="d5d05-129">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="d5d05-129">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="d5d05-130">Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="d5d05-130">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="d5d05-131">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="d5d05-131">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

