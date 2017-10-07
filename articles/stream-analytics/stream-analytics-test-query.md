---
title: il test delle query Analitica flusso aaaAzure | Documenti Microsoft
description: Come tootest le query nei processi di flusso Analitica.
keywords: testare query, risolvere i problemi relativi alle query
documentation center: 
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
ms.openlocfilehash: 3b141d98332fdc170e696e181c8446796a86f78e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="test-azure-stream-analytics-queries-in-hello-azure-portal"></a><span data-ttu-id="08f07-104">Testare le query Analitica di flusso di Azure nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="08f07-104">Test Azure Stream Analytics queries in hello Azure portal</span></span>

<span data-ttu-id="08f07-105">Con Analitica di flusso di Azure, è possibile testare le query in hello portale di Azure senza la necessità di toostart o arrestare un processo.</span><span class="sxs-lookup"><span data-stu-id="08f07-105">With Azure Stream Analytics, you can test queries in hello Azure portal without needing toostart or stop a job.</span></span>

## <a name="test-hello-input"></a><span data-ttu-id="08f07-106">Input di test hello</span><span class="sxs-lookup"><span data-stu-id="08f07-106">Test hello input</span></span>

1. <span data-ttu-id="08f07-107">tootest con dati di input di esempio, uno degli input e quindi scegliere **caricare i dati di esempio dal file**.</span><span class="sxs-lookup"><span data-stu-id="08f07-107">tootest with sample input data, right-click any of your inputs, and then select **Upload sample data from file**.</span></span>

    ![Pulsante per il testo delle query nell'editor query della funzione di analisi di flusso](media/stream-analytics-test-query/stream-analytics-test-query-editor-upload.png)

2. <span data-ttu-id="08f07-109">Dopo il caricamento di hello è completo, fare clic su **Test** tootest aver fornito dati di esempio di questa query hello.</span><span class="sxs-lookup"><span data-stu-id="08f07-109">After hello upload is complete, click **Test** tootest this query against hello sample data you have provided.</span></span>

    ![dati di esempio per il test nell'editor query della funzione di analisi di flusso](media/stream-analytics-test-query/stream-analytics-test-query-editor-test.png)

<span data-ttu-id="08f07-111">output di Hello della query viene visualizzato nel browser hello, con risultati collegamento se si vuole output del test hello toosave per un uso successivo.</span><span class="sxs-lookup"><span data-stu-id="08f07-111">hello output of your query is displayed in hello browser, with Download results link should you want toosave hello test output for later use.</span></span> <span data-ttu-id="08f07-112">È ora facilmente e in modo iterativo modificare la query e testarlo ripetutamente toosee come output di hello cambia.</span><span class="sxs-lookup"><span data-stu-id="08f07-112">You can now easily and iteratively modify your query and test it repeatedly toosee how hello output changes.</span></span>

![Output di esempio dell'editor query della funzione di analisi di flusso](media/stream-analytics-test-query/stream-analytics-test-query-editor-samples-output.png)

<span data-ttu-id="08f07-114">Con più output in una query, è possibile visualizzare i risultati di hello per entrambi gli output separatamente e attivare o disattivare facilmente tra di essi.</span><span class="sxs-lookup"><span data-stu-id="08f07-114">With multiple outputs used in a query, you can see hello results for both outputs separately and easily toggle between them.</span></span>

<span data-ttu-id="08f07-115">Dopo che si è soddisfatti dei risultati di hello visualizzati nel browser di hello, è possibile salvare la query, avviare il processo e consentire la elabora gli eventi senza errori.</span><span class="sxs-lookup"><span data-stu-id="08f07-115">After you are satisfied with hello results shown in hello browser, you can save your query, start your job, and let it process events without error.</span></span>

## <a name="get-help"></a><span data-ttu-id="08f07-116">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="08f07-116">Get help</span></span>

<span data-ttu-id="08f07-117">Per ulteriore assistenza, provare il [Forum di Analisi dei flussi di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="08f07-117">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="08f07-118">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="08f07-118">Next steps</span></span>

* [<span data-ttu-id="08f07-119">Introduzione tooAzure flusso Analitica</span><span class="sxs-lookup"><span data-stu-id="08f07-119">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="08f07-120">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="08f07-120">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="08f07-121">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="08f07-121">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="08f07-122">Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="08f07-122">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="08f07-123">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="08f07-123">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
