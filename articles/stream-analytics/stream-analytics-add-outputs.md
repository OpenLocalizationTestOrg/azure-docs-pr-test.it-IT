---
title: Come configurare gli output dei dati per i processi di Analisi di flusso | Microsoft Docs
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
ms.openlocfilehash: 1ffa517469da1a8d79917b9747abc97ca3bef463
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-data-outputs-for-stream-analytics-jobs"></a><span data-ttu-id="107e1-104">Come configurare gli output dei dati per i processi di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="107e1-104">How to configure data outputs for Stream Analytics jobs</span></span>

<span data-ttu-id="107e1-105">I processi di Analisi di flusso di Azure possono essere connessi a uno o più output dei dati, che definisce una connessione a un sink di dati esistente.</span><span class="sxs-lookup"><span data-stu-id="107e1-105">Azure Stream Analytics jobs can be connected to one or more data outputs, which define a connection to an existing data sink.</span></span> <span data-ttu-id="107e1-106">Dato che il processo di Analisi di flusso elabora e trasforma i dati in entrata, un flusso di eventi di output dei dati viene scritto nell'output del processo.</span><span class="sxs-lookup"><span data-stu-id="107e1-106">As your Stream Analytics job processes and transforms incoming data, a stream of data output events is written to your job's output.</span></span>

<span data-ttu-id="107e1-107">È possibile usare gli output dei dati di Analisi di flusso per creare dashboard o avvisi in tempo reale, attivare i flussi di lavoro degli spostamenti dei dati o semplicemente archiviare i dati per una successiva elaborazione batch.</span><span class="sxs-lookup"><span data-stu-id="107e1-107">Stream Analytics data outputs can be used to source real-time dashboards or alerts, trigger data movement workflows, or simply archive data for batch processing later on.</span></span> <span data-ttu-id="107e1-108">L'analisi di flusso dispone dell'integrazione di prima classe con diversi servizi di Azure, che sono documentati in dettaglio di seguito.</span><span class="sxs-lookup"><span data-stu-id="107e1-108">Stream Analytics has first class integration with several Azure services, which are documented in detail here.</span></span>

<span data-ttu-id="107e1-109">Per aggiungere un output al processo di analisi di flusso:</span><span class="sxs-lookup"><span data-stu-id="107e1-109">To add an output to your Stream Analytics job:</span></span>

1. <span data-ttu-id="107e1-110">Nel [portale di Azure](https://portal.azure.com), aprire il processo e fare clic su **Output** e quindi fare clic su **Aggiungi** nel pannello Output che viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="107e1-110">In the [Azure portal](https://portal.azure.com), open your job and click **Outputs** and then click **Add** in the Outputs blade that appears.</span></span>
   
    ![Aggiungere output](./media/stream-analytics-add-outputs/1-stream-analytics-add-outputs.png)  
   
2. <span data-ttu-id="107e1-112">Fornire un nome descrittivo per l'output nella finestra di **Alias di output** .</span><span class="sxs-lookup"><span data-stu-id="107e1-112">Provide a friendly name for this output in the **Output Alias** box.</span></span> <span data-ttu-id="107e1-113">Questo nome verrà utilizzato nella query del processo in un secondo momento per fare riferimento all'output.</span><span class="sxs-lookup"><span data-stu-id="107e1-113">This name can be used in your job's query later on to refer to the output.</span></span>  
   
    <span data-ttu-id="107e1-114">Compilare il resto delle proprietà di connessione necessarie per connettersi all'output.</span><span class="sxs-lookup"><span data-stu-id="107e1-114">Fill in the rest of the required connection properties to connect to your output.</span></span>  <span data-ttu-id="107e1-115">Questi campi variano in base al tipo di output e vengono definiti in modo dettagliato di seguito.</span><span class="sxs-lookup"><span data-stu-id="107e1-115">These fields vary by output type and are defined in detail here.</span></span>  
   
    ![Scegliere il tipo di spostamento dei dati](./media/stream-analytics-add-outputs/2-stream-analytics-add-outputs.png)  
   
3. <span data-ttu-id="107e1-117">A seconda del tipo di output, può essere necessario specificare la modalità di serializzazione o formattazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="107e1-117">Depending on the output type, you may need to specify how the data is serialized or formatted.</span></span> <span data-ttu-id="107e1-118">Di seguito sono descritte le impostazioni di serializzazione specifiche per ogni tipo di output.</span><span class="sxs-lookup"><span data-stu-id="107e1-118">The specific serialization settings for each output type are documented here.</span></span>
   
    <span data-ttu-id="107e1-119">Compilare il resto delle proprietà di connessione necessarie per connettersi all'origine dati.</span><span class="sxs-lookup"><span data-stu-id="107e1-119">Fill in the rest of the required connection properties to connect to your data source.</span></span> <span data-ttu-id="107e1-120">Questi campi variano in base al tipo di origine e di input e vengono descritti in modo dettagliato nell'articolo relativo alla [creazione di un processo](stream-analytics-create-a-job.md).</span><span class="sxs-lookup"><span data-stu-id="107e1-120">These fields vary by type of input and source type and are defined in detail in the [Create Job article](stream-analytics-create-a-job.md).</span></span>  

> [!Note]
>
> <span data-ttu-id="107e1-121">Qualsiasi elemento output aggiunto al processo, deve esistere prima che il processo venga avviato e gli eventi avviino il flusso.</span><span class="sxs-lookup"><span data-stu-id="107e1-121">Any output element added to the job, must exist before the job is started and events start flowing.</span></span> <span data-ttu-id="107e1-122">Ad esempio, se si utilizza l'archiviazione Blob come output, il processo non creerà un account di archiviazione automaticamente.</span><span class="sxs-lookup"><span data-stu-id="107e1-122">For example, if you use Blob storage as an output, the job will not create a storage account automatically.</span></span> <span data-ttu-id="107e1-123">Deve essere creato dall'utente prima che venga avviato il processo ASA.</span><span class="sxs-lookup"><span data-stu-id="107e1-123">It needs to be created by the user before the ASA job is started.</span></span>
> 
 

## <a name="get-help"></a><span data-ttu-id="107e1-124">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="107e1-124">Get help</span></span>
<span data-ttu-id="107e1-125">Per assistenza, provare il [Forum di Analisi di flusso di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="107e1-125">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="107e1-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="107e1-126">Next steps</span></span>
* [<span data-ttu-id="107e1-127">Introduzione ad Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="107e1-127">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="107e1-128">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="107e1-128">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="107e1-129">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="107e1-129">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="107e1-130">Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="107e1-130">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="107e1-131">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="107e1-131">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

