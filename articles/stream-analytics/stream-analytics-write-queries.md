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
# <a name="how-toowrite-queries-in-stream-analytics"></a><span data-ttu-id="83914-104">La modalità di query toowrite in flusso Analitica</span><span class="sxs-lookup"><span data-stu-id="83914-104">How toowrite queries in Stream Analytics</span></span>
<span data-ttu-id="83914-105">Scrittura di query per il flusso di elaborazione logica Analitica di flusso di Azure viene implementata come un "query in esecuzione" definito prima di avvia e raggiunge il processo di hello eseguite sui dati di un processo.</span><span class="sxs-lookup"><span data-stu-id="83914-105">Writing queries for stream processing logic in Azure Stream Analytics is implemented as a "standing query" that is defined before a job starts and executed on data as it reaches hello job.</span></span> <span data-ttu-id="83914-106">la trasformazione dei dati Hello è espresso in un linguaggio di query simile a SQL, che è sostanzialmente un subset di T-SQL con alcune aggiunte estensioni del linguaggio come [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) utilizzato tooexpress temporale semantica.</span><span class="sxs-lookup"><span data-stu-id="83914-106">hello data transformation is expressed in a SQL-like query language, which is largely a subset of T-SQL with some added language extensions like [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) used tooexpress temporal semantics.</span></span>

## <a name="writing-queries"></a><span data-ttu-id="83914-107">Scrittura di query:</span><span class="sxs-lookup"><span data-stu-id="83914-107">Writing Queries:</span></span>
1. <span data-ttu-id="83914-108">Nel processo flusso Analitica nel portale di gestione di Azure hello, fare clic su **Query**.</span><span class="sxs-lookup"><span data-stu-id="83914-108">In your Stream Analytics Job in hello Azure Management portal, click **Query**.</span></span>
   
    ![Query di selezione](./media/stream-analytics-write-queries/1-stream-analytics-write-queries.png)  
   
    <span data-ttu-id="83914-110">Nel portale di Azure hello, fare clic su **Query**.</span><span class="sxs-lookup"><span data-stu-id="83914-110">In hello Azure Portal, click **Query**.</span></span>
   
    ![Selezionare l'anteprima della query](./media/stream-analytics-write-queries/query-preview-portal.png)  
2. <span data-ttu-id="83914-112">I nuovi processi hanno un toohelp modello di query consentono di iniziare.</span><span class="sxs-lookup"><span data-stu-id="83914-112">New jobs have a query template toohelp get you started.</span></span> <span data-ttu-id="83914-113">query Hello modello esegue "pass-through" eseguire una query che viene proiettato tutti i campi da eventi di input nell'output di hello.</span><span class="sxs-lookup"><span data-stu-id="83914-113">hello query template performs a "pass-through" query that projects all fields from input events into hello output.</span></span>  
   
   * <span data-ttu-id="83914-114">Se è stato definito almeno un input e output per il processo, è possibile sostituire i segnaposto hello "[YourOutputAlias]" e "[YourInputAlias]" campi con alias hello di hello di input e output che si desidera utilizzare prima.</span><span class="sxs-lookup"><span data-stu-id="83914-114">If you have defined at least one input and output for your job, you can replace hello placeholder "[YourOutputAlias]" and "[YourInputAlias]" fields with hello aliases of hello input and output that you wish use first.</span></span> <span data-ttu-id="83914-115">È inoltre possibile creare e testare la query nel portale di Azure classico hello senza definire l'input e output per il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="83914-115">In addition, you can still author and test your query in hello Azure Classic Portal without defining inputs and outputs on hello job.</span></span>
   * <span data-ttu-id="83914-116">Se si desidera tooperform maggiore elaborazione rispetto a un semplice pass-through, è possibile modificare la definizione della query hello.</span><span class="sxs-lookup"><span data-stu-id="83914-116">If you wish tooperform more processing than a simple pass-through, you can edit hello query definition.</span></span> <span data-ttu-id="83914-117">tooget introduttiva alla creazione di query, esaminare alcune query comuni, vengono acquisiti i modelli [qui](stream-analytics-stream-analytics-query-patterns.md).</span><span class="sxs-lookup"><span data-stu-id="83914-117">tooget started with query authoring, take a look at some common query patterns are captured [here](stream-analytics-stream-analytics-query-patterns.md).</span></span>  
   
   ![Eseguire query sui dati, finestra](./media/stream-analytics-write-queries/2-stream-analytics-write-queries.png)  

## <a name="toovalidate-query-data-is-working"></a><span data-ttu-id="83914-119">dati di query toovalidate funzioni:</span><span class="sxs-lookup"><span data-stu-id="83914-119">toovalidate query data is working:</span></span>
<span data-ttu-id="83914-120">È possibile verificare che la query si comporti come previsto eseguendo nel browser hello su uno o più file JSON locali contenente i dati di test.</span><span class="sxs-lookup"><span data-stu-id="83914-120">You can test that your query behaves as expected by running it in hello browser over one or more local JSON files containing test data.</span></span> <span data-ttu-id="83914-121">Questo non verrà avviato il processo di hello né quindi alcuna implicazione di fatturazione.</span><span class="sxs-lookup"><span data-stu-id="83914-121">This will not start hello job or have any billing implications.</span></span>

> [!NOTE]
> <span data-ttu-id="83914-122">Attualmente il test delle query nel browser non è supportato nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="83914-122">Currently in-browser query testing is not supported in hello Azure Portal.</span></span>  
> 
> 

1. <span data-ttu-id="83914-123">Assicurarsi che non siano presenti errori nella query hello (in caso contrario hello Test pulsante sarà disabilitato) e quindi fare clic su pulsante Test hello.</span><span class="sxs-lookup"><span data-stu-id="83914-123">Make sure that there are no errors in hello query (otherwise hello Test button will be disabled) and then click hello Test button.</span></span>  
   
   ![Eseguire query sui dati, test](./media/stream-analytics-write-queries/3-stream-analytics-write-queries.png)  
2. <span data-ttu-id="83914-125">Sarà richiesta toospecify file per ogni input hello a cui fa riferimento nella query hello.</span><span class="sxs-lookup"><span data-stu-id="83914-125">You will be prompted toospecify files for each of hello inputs referenced in hello query.</span></span> <span data-ttu-id="83914-126">In questo esempio, query modello hello viene lasciata come-è, quindi finestra di dialogo hello è richiesta per un input denominato "yourinputalias".</span><span class="sxs-lookup"><span data-stu-id="83914-126">In this example, hello template query is left as-is, so hello dialog is prompting for an input named "yourinputalias".</span></span>  
   
   ![Verificare query sui dati](./media/stream-analytics-write-queries/4-stream-analytics-write-queries.png)  
3. <span data-ttu-id="83914-128">Individuare il file di test tooa.</span><span class="sxs-lookup"><span data-stu-id="83914-128">Browse tooa test file.</span></span> <span data-ttu-id="83914-129">Sono disponibili in diversi file di esempio [github](https://github.com/Azure/azure-stream-analytics/tree/master/Sample Data) ed è anche possibile recuperare i dati di esempio dal proprio input flusso di dati tramite una funzione di dati di esempio nella scheda input hello hello.</span><span class="sxs-lookup"><span data-stu-id="83914-129">Several sample files are available on [github](https://github.com/Azure/azure-stream-analytics/tree/master/Sample Data) and you can also retrieve sample data from your own data stream inputs via hello Sample Data function on hello inputs tab.</span></span>  
   
   ![Input della query](./media/stream-analytics-write-queries/5-stream-analytics-write-queries.png)  
4. <span data-ttu-id="83914-131">Dopo la chiusura di finestra di dialogo hello, verrà eseguita la query sui dati di test hello e verranno visualizzati risultati hello nella parte inferiore di hello della pagina di Query hello.</span><span class="sxs-lookup"><span data-stu-id="83914-131">After closing hello dialog, your query will be run over hello test data and you will see hello results at hello bottom of hello Query page.</span></span>  
   
   ![Riepilogo della query](./media/stream-analytics-write-queries/6-stream-analytics-write-queries.png)  

## <a name="get-help"></a><span data-ttu-id="83914-133">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="83914-133">Get help</span></span>
<span data-ttu-id="83914-134">Per assistenza, provare il [Forum di Analisi di flusso di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="83914-134">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="83914-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="83914-135">Next steps</span></span>
* [<span data-ttu-id="83914-136">Introduzione tooAzure flusso Analitica</span><span class="sxs-lookup"><span data-stu-id="83914-136">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="83914-137">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="83914-137">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="83914-138">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="83914-138">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="83914-139">Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="83914-139">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="83914-140">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="83914-140">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

