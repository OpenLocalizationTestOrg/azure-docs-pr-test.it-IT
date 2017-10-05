---
title: Campionamento degli input in Analisi di flusso di Azure | Microsoft Docs
description: Individuare i problemi durante la risoluzione dei processi di analisi di flusso.
keywords: risoluzione dei problemi relativi all'input, campionamento dell'input
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 0bb66090b5025d57f5ca8f30713aef4e444fa8e7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-stream-analytics-input-stream-sampling"></a><span data-ttu-id="2cf3c-104">Campionamento del flusso di input della funzione di analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="2cf3c-104">Azure Stream Analytics input-stream sampling</span></span>

<span data-ttu-id="2cf3c-105">La funzione di analisi di flusso di Azure consente di campionare eventi di input che provengono da un file e di testare le query nel portale senza la necessità di avviare o arrestare un processo.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-105">By using Azure Stream Analytics, you can sample input events that come from a file and test queries in the portal without needing to start or stop a job.</span></span>

## <a name="testing-your-query"></a><span data-ttu-id="2cf3c-106">Test di una query</span><span class="sxs-lookup"><span data-stu-id="2cf3c-106">Testing your query</span></span>

<span data-ttu-id="2cf3c-107">Nel riquadro dei dettagli del processo di analisi di flusso aprire il pannello **Editor query** facendo clic sul nome della query in **Query**.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-107">In the Stream Analytics job details pane, open the **Query editor** blade by clicking the query name under **Query**.</span></span> <span data-ttu-id="2cf3c-108">Nello scenario di esempio, poiché non è ancora stata creata alcuna query, fare clic sul segnaposto **< >**.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-108">(In our example scenario, because no query has been created yet, click the **< >** placeholder.)</span></span>

![Editor query della funzione di analisi di flusso](media/stream-analytics-sample-data-input/stream-analytics-query-editor.png)

<span data-ttu-id="2cf3c-110">Il pannello dell'editor completo per la creazione di query presenta lo stesso aspetto della versione precedente.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-110">The rich editor blade for creating your query is displayed as it was in the previous release.</span></span> <span data-ttu-id="2cf3c-111">Il pannello è stato ora aggiornato di un nuovo riquadro a sinistra, che mostra gli input e gli output usati dalla query e definiti per il processo.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-111">Now the blade has been updated with a new left pane that shows the inputs and outputs that are used by the query and defined for this job.</span></span>

![Elenchi di input e di output nell'editor query di analisi di flusso](media/stream-analytics-sample-data-input/stream-analytics-query-editor-highlight.png)

<span data-ttu-id="2cf3c-113">Sono inoltre visibili altri input e output, che non sono definiti.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-113">Also shown are an additional input and output, which are not defined.</span></span> <span data-ttu-id="2cf3c-114">Questi provengono dal nuovo modello di query iniziale</span><span class="sxs-lookup"><span data-stu-id="2cf3c-114">They come from the new query template that you start with.</span></span> <span data-ttu-id="2cf3c-115">e cambiano o addirittura scompaiono completamente man mano che si modifica la query.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-115">They change, or even disappear altogether, as you edit the query.</span></span> <span data-ttu-id="2cf3c-116">È possibile ignorarli senza problemi per il momento.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-116">You can safely ignore them for now.</span></span>

<span data-ttu-id="2cf3c-117">Per eseguire il test con dati di input di esempio, fare clic con il pulsante destro del mouse su uno degli input e quindi selezionare **Carica dati di esempio da file**.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-117">To test with sample input data, right-click any of your inputs, and then select **Upload sample data from file**.</span></span>

![Comando Carica dati di esempio da file dell'editor query della funzione di analisi di flusso](media/stream-analytics-sample-data-input/stream-analytics-query-editor-upload.png)

<span data-ttu-id="2cf3c-119">Dopo avere completato il caricamento, fare clic su **Test** per testare la query usando i dati di esempio appena specificati.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-119">After the upload is complete, click **Test** to test this query against the sample data you have just provided.</span></span>

![Pulsante Test dell'editor query della funzione di analisi di flusso](media/stream-analytics-sample-data-input/stream-analytics-query-editor-test.png)

<span data-ttu-id="2cf3c-121">Per consentire il salvataggio dei risultati del test per un utilizzo successivo, l'output della query viene visualizzato nel browser con un collegamento ai risultati del download.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-121">If you want to save the test output for later use, the output of your query is displayed in the browser with a link to the download results.</span></span> <span data-ttu-id="2cf3c-122">È possibile a questo punto modificare in modo facile e iterativo la query e testarla più volte per vedere come cambia l'output.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-122">You can now easily and iteratively modify your query and test it repeatedly to see how the output changes.</span></span>

![Output di esempio dell'editor query della funzione di analisi di flusso](media/stream-analytics-sample-data-input/stream-analytics-query-editor-samples-output.png)

<span data-ttu-id="2cf3c-124">Nell'immagine precedente è stato aggiunto un secondo output, denominato **HighAvgTempOutput**.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-124">In the preceding image, a second output has been added, called **HighAvgTempOutput**.</span></span>

<span data-ttu-id="2cf3c-125">Quando si usano più output in una query, è possibile visualizzare i risultati di ogni output separatamente e passare facilmente da un output all'altro.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-125">When you use multiple outputs in a query, you can see the results for each output separately and easily toggle between them.</span></span>

<span data-ttu-id="2cf3c-126">Quando si è soddisfatti dei risultati, è possibile salvare la query, avviare il processo e attendere l'elaborazione da parte della funzione di analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="2cf3c-126">After you are satisfied with the results, you can save your query, start your job, sit back and watch the magic of Stream Analytics.</span></span>

## <a name="get-help"></a><span data-ttu-id="2cf3c-127">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="2cf3c-127">Get help</span></span>

<span data-ttu-id="2cf3c-128">Per ulteriore assistenza, provare il [Forum di Analisi dei flussi di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="2cf3c-128">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2cf3c-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2cf3c-129">Next steps</span></span>
* [<span data-ttu-id="2cf3c-130">Introduzione ad Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="2cf3c-130">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="2cf3c-131">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="2cf3c-131">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="2cf3c-132">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="2cf3c-132">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="2cf3c-133">Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="2cf3c-133">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="2cf3c-134">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="2cf3c-134">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
