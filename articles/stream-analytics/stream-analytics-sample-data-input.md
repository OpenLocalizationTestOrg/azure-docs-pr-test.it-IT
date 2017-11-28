---
title: gli input di campionamento aaa Analitica di flusso di Azure | Documenti Microsoft
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
ms.openlocfilehash: 9637a8664de099eebb8f5654036d2957f4c6b7ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-input-stream-sampling"></a><span data-ttu-id="15ece-104">Campionamento del flusso di input della funzione di analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="15ece-104">Azure Stream Analytics input-stream sampling</span></span>

<span data-ttu-id="15ece-105">Tramite Azure flusso Analitica, è possibile campionare eventi di input che provengono da un file e le query di test nel portale di hello senza toostart o arrestare un processo.</span><span class="sxs-lookup"><span data-stu-id="15ece-105">By using Azure Stream Analytics, you can sample input events that come from a file and test queries in hello portal without needing toostart or stop a job.</span></span>

## <a name="testing-your-query"></a><span data-ttu-id="15ece-106">Test di una query</span><span class="sxs-lookup"><span data-stu-id="15ece-106">Testing your query</span></span>

<span data-ttu-id="15ece-107">Nel riquadro dettagli processo flusso Analitica hello aprire hello **editor di Query** pannello facendo clic sul nome della query hello in **Query**.</span><span class="sxs-lookup"><span data-stu-id="15ece-107">In hello Stream Analytics job details pane, open hello **Query editor** blade by clicking hello query name under **Query**.</span></span> <span data-ttu-id="15ece-108">(In questo scenario di esempio, poiché non è ancora stata creata alcuna query, fare clic su hello **< >** segnaposto.)</span><span class="sxs-lookup"><span data-stu-id="15ece-108">(In our example scenario, because no query has been created yet, click hello **< >** placeholder.)</span></span>

![editor di query Hello Analitica di flusso](media/stream-analytics-sample-data-input/stream-analytics-query-editor.png)

<span data-ttu-id="15ece-110">Pannello di Hello editor avanzato per la creazione della query viene visualizzato come lo era nella versione precedente di hello.</span><span class="sxs-lookup"><span data-stu-id="15ece-110">hello rich editor blade for creating your query is displayed as it was in hello previous release.</span></span> <span data-ttu-id="15ece-111">Ora pannello hello è stato aggiornato con un nuovo riquadro a sinistra che mostra hello input e output utilizzati dalla query hello e definito per il processo.</span><span class="sxs-lookup"><span data-stu-id="15ece-111">Now hello blade has been updated with a new left pane that shows hello inputs and outputs that are used by hello query and defined for this job.</span></span>

![editor di query flusso Analitica Hello input e restituisce gli elenchi](media/stream-analytics-sample-data-input/stream-analytics-query-editor-highlight.png)

<span data-ttu-id="15ece-113">Sono inoltre visibili altri input e output, che non sono definiti.</span><span class="sxs-lookup"><span data-stu-id="15ece-113">Also shown are an additional input and output, which are not defined.</span></span> <span data-ttu-id="15ece-114">Provengono da hello nuovo modello di query iniziale.</span><span class="sxs-lookup"><span data-stu-id="15ece-114">They come from hello new query template that you start with.</span></span> <span data-ttu-id="15ece-115">Sono modificato, o addirittura eliminato completamente, come si modifica la query hello.</span><span class="sxs-lookup"><span data-stu-id="15ece-115">They change, or even disappear altogether, as you edit hello query.</span></span> <span data-ttu-id="15ece-116">È possibile ignorarli senza problemi per il momento.</span><span class="sxs-lookup"><span data-stu-id="15ece-116">You can safely ignore them for now.</span></span>

<span data-ttu-id="15ece-117">tootest con dati di input di esempio, uno degli input e quindi scegliere **caricare i dati di esempio dal file**.</span><span class="sxs-lookup"><span data-stu-id="15ece-117">tootest with sample input data, right-click any of your inputs, and then select **Upload sample data from file**.</span></span>

![Hello flusso Analitica query editor caricamento dati di esempio di file (comando)](media/stream-analytics-sample-data-input/stream-analytics-query-editor-upload.png)

<span data-ttu-id="15ece-119">Dopo il caricamento di hello è completo, fare clic su **Test** tootest questa query hello campionare i dati appena immessa.</span><span class="sxs-lookup"><span data-stu-id="15ece-119">After hello upload is complete, click **Test** tootest this query against hello sample data you have just provided.</span></span>

![pulsante di Test dell'editor di query di Hello Analitica di flusso](media/stream-analytics-sample-data-input/stream-analytics-query-editor-test.png)

<span data-ttu-id="15ece-121">Se si desidera l'output del test hello toosave per un uso successivo, nel browser hello con risultati di download toohello un collegamento viene visualizzato l'output di hello della query.</span><span class="sxs-lookup"><span data-stu-id="15ece-121">If you want toosave hello test output for later use, hello output of your query is displayed in hello browser with a link toohello download results.</span></span> <span data-ttu-id="15ece-122">È ora facilmente e in modo iterativo modificare la query e testarlo ripetutamente toosee come output di hello cambia.</span><span class="sxs-lookup"><span data-stu-id="15ece-122">You can now easily and iteratively modify your query and test it repeatedly toosee how hello output changes.</span></span>

![Output di esempio dell'editor query della funzione di analisi di flusso](media/stream-analytics-sample-data-input/stream-analytics-query-editor-samples-output.png)

<span data-ttu-id="15ece-124">In hello immagine precedente, è stato aggiunto un secondo output, chiamato **HighAvgTempOutput**.</span><span class="sxs-lookup"><span data-stu-id="15ece-124">In hello preceding image, a second output has been added, called **HighAvgTempOutput**.</span></span>

<span data-ttu-id="15ece-125">Quando si utilizza più output in una query, è possibile visualizzare i risultati di hello per ogni output separatamente e attivare o disattivare facilmente tra di essi.</span><span class="sxs-lookup"><span data-stu-id="15ece-125">When you use multiple outputs in a query, you can see hello results for each output separately and easily toggle between them.</span></span>

<span data-ttu-id="15ece-126">Dopo che si è soddisfatti dei risultati di hello, è possibile salvare la query, avviare il processo, tranquillamente e guardare magic hello di flusso Analitica.</span><span class="sxs-lookup"><span data-stu-id="15ece-126">After you are satisfied with hello results, you can save your query, start your job, sit back and watch hello magic of Stream Analytics.</span></span>

## <a name="get-help"></a><span data-ttu-id="15ece-127">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="15ece-127">Get help</span></span>

<span data-ttu-id="15ece-128">Per ulteriore assistenza, provare il [Forum di Analisi dei flussi di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="15ece-128">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="15ece-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="15ece-129">Next steps</span></span>
* [<span data-ttu-id="15ece-130">Introduzione tooAzure flusso Analitica</span><span class="sxs-lookup"><span data-stu-id="15ece-130">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="15ece-131">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="15ece-131">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="15ece-132">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="15ece-132">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="15ece-133">Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="15ece-133">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="15ece-134">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="15ece-134">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
