---
title: Aggiungere un input di dati ai processi di analisi di flusso | Microsoft Docs
description: Informazioni su come associare un'origine dati al processo di analisi di flusso come input di dati di streaming proveniente dall'hub eventi o dati di riferimento provenienti dall'archiviazione BLOB.
keywords: input di dati, flusso di dati
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: 
ms.assetid: 9e59bd24-2a80-4ecb-b6b2-309a07c70bcd
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 8bdbcf78f2892cbd1e1cc09cef220dff08dd9490
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="add-a-streaming-data-input-or-reference-data-to-a-stream-analytics-job"></a><span data-ttu-id="7ecb8-104">Aggiungere un input di dati di streaming o dati di riferimento a un processo di analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="7ecb8-104">Add a streaming data input or reference data to a Stream Analytics job</span></span>
<span data-ttu-id="7ecb8-105">Informazioni su come associare un'origine dati al processo di Analisi di flusso come input di dati di streaming provenienti da Hub eventi o dati di riferimento provenienti dall'archivio BLOB.</span><span class="sxs-lookup"><span data-stu-id="7ecb8-105">Learn how to hook up a data source to your Stream Analytics job as streaming data input from Event Hubs or reference data from Blob storage.</span></span>

<span data-ttu-id="7ecb8-106">I processi di analisi di flusso di Azure possono essere connessi a uno o più input di dati, che definiscono una connessione a un'origine dati esistente.</span><span class="sxs-lookup"><span data-stu-id="7ecb8-106">Azure Stream Analytics jobs can be connected to one data input or more, each of which define a connection to an existing data source.</span></span> <span data-ttu-id="7ecb8-107">Quando i dati vengono inviati a tale origine dati, vengono usati dal processo di Analisi di flusso ed elaborati in tempo reale come flussi di dati.</span><span class="sxs-lookup"><span data-stu-id="7ecb8-107">As data is sent to that data source, it is consumed by the Stream Analytics job and processed in real time as streaming data.</span></span> <span data-ttu-id="7ecb8-108">L'analisi di flusso si integra perfettamente con gli [Hub eventi di Azure](https://azure.microsoft.com/services/event-hubs/) e con l'[archivio BLOB di Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) all'interno e all'esterno della sottoscrizione del processo.</span><span class="sxs-lookup"><span data-stu-id="7ecb8-108">Stream Analytics has first class integration with [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) and [Azure Blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md) both within and outside of the job's subscription.</span></span>

<span data-ttu-id="7ecb8-109">Questo articolo è un passaggio nel [percorso di apprendimento di analisi di flusso](/documentation/learning-paths/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="7ecb8-109">This article is a step in the [Stream Analytics learning path](/documentation/learning-paths/stream-analytics/).</span></span>

## <a name="data-input-streaming-data-and-reference-data"></a><span data-ttu-id="7ecb8-110">Input di dati: dati di streaming e dati di riferimento</span><span class="sxs-lookup"><span data-stu-id="7ecb8-110">Data input: Streaming data and reference data</span></span>
<span data-ttu-id="7ecb8-111">Esistono due tipi di input distinti in Analisi di flusso: dati di riferimento e flussi di dati.</span><span class="sxs-lookup"><span data-stu-id="7ecb8-111">There are two distinct types of inputs in Stream Analytics: data streams and reference data.</span></span>

* <span data-ttu-id="7ecb8-112">**Flussi di dati**: I processi di analisi di flusso devono includere almeno un input del flusso dei dati che deve essere utilizzato e trasformato dal processo stesso.</span><span class="sxs-lookup"><span data-stu-id="7ecb8-112">**Data Streams**: Stream Analytics jobs must include at least one data stream input to be consumed and transformed by the job.</span></span> <span data-ttu-id="7ecb8-113">L'archivio BLOB di Azure e Hub eventi di Azure sono supportati come origini di input del flusso dei dati.</span><span class="sxs-lookup"><span data-stu-id="7ecb8-113">Azure Blob storage and Azure Event Hubs are supported as data stream input sources.</span></span> <span data-ttu-id="7ecb8-114">Gli Hub eventi di Azure vengono usati per raccogliere flussi di eventi da più dispositivi, servizi e applicazioni connessi.</span><span class="sxs-lookup"><span data-stu-id="7ecb8-114">Azure Event Hubs are used to collect event streams from connected devices, services and applications.</span></span> <span data-ttu-id="7ecb8-115">Si può usare l'archivio BLOB di Azure come origine di input per l'inserimento di dati in blocco come flusso.</span><span class="sxs-lookup"><span data-stu-id="7ecb8-115">Azure Blob storage can be used as an input source for ingesting bulk data as a stream.</span></span>  
* <span data-ttu-id="7ecb8-116">**Dati di riferimento**: l’analisi di flusso supporta un secondo tipo di input ausiliario denominato dati di riferimento.</span><span class="sxs-lookup"><span data-stu-id="7ecb8-116">**Reference data**: Stream Analytics supports a second type of auxiliary input called reference data.</span></span>  <span data-ttu-id="7ecb8-117">Al contrario dei dati in continua evoluzione, questi dati sono statici o cambiano molto lentamente.</span><span class="sxs-lookup"><span data-stu-id="7ecb8-117">As opposed to data in motion, this data is static or slowing changing.</span></span>  <span data-ttu-id="7ecb8-118">In genere vengono utilizzati per l'esecuzione di ricerche e correlazioni con flussi di dati per creare un set di dati più ampio.</span><span class="sxs-lookup"><span data-stu-id="7ecb8-118">It is typically used for performing look-ups and correlations with data streams to create a richer data set.</span></span>  <span data-ttu-id="7ecb8-119">L'archivio BLOB di Azure attualmente è l'unica origine di input supportata per i dati di riferimento.</span><span class="sxs-lookup"><span data-stu-id="7ecb8-119">Azure Blob storage is currently the only supported input source for reference data.</span></span>  

<span data-ttu-id="7ecb8-120">Per aggiungere un input al processo di analisi di flusso:</span><span class="sxs-lookup"><span data-stu-id="7ecb8-120">To add an input to your Stream Analytics job:</span></span>

1. <span data-ttu-id="7ecb8-121">Nel Portale di Azure fare clic su **Input** e poi scegliere **Aggiungere un input** nel processo di analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="7ecb8-121">In the Azure portal click **Inputs** and then click **Add an Input** in your Stream Analytics job.</span></span>
   
    ![Portale di Azure classico - aggiungere un input.](./media/stream-analytics-add-inputs/1-stream-analytics-add-inputs.png)  
   
    <span data-ttu-id="7ecb8-123">Nel portale di Azure fare clic sul riquadro **Input** nel processo di analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="7ecb8-123">In the Azure portal click the **Inputs** tile in your Stream Analytics job.</span></span>  
   
    ![Portale di Azure - aggiungere un input di dati.](./media/stream-analytics-add-inputs/7-stream-analytics-add-inputs.png)  
2. <span data-ttu-id="7ecb8-125">Specificare il tipo di input: **Flusso dei dati** o **Dati di riferimento**.</span><span class="sxs-lookup"><span data-stu-id="7ecb8-125">Specify the type of the input: either **Data stream** or **Reference data**.</span></span>
   
    ![Aggiungere l'input di dati corretto, di flusso o di riferimento](./media/stream-analytics-add-inputs/2-stream-analytics-add-inputs.png)  
   
    ![Aggiungere l'input di dati corretto, di flusso o di riferimento](./media/stream-analytics-add-inputs/8-stream-analytics-add-inputs.png)  
3. <span data-ttu-id="7ecb8-128">Se si crea un input del flusso di dati, specificare il tipo di origine per l'input.</span><span class="sxs-lookup"><span data-stu-id="7ecb8-128">If creating a Data Stream input, specify the source type for the input.</span></span>  <span data-ttu-id="7ecb8-129">Questo passaggio può essere ignorato durante la creazione dei dati di riferimento, poiché al momento è supportato soltanto l’archivio BLOB.</span><span class="sxs-lookup"><span data-stu-id="7ecb8-129">This step can be skipped during Reference Data creation as only Blob storage is supported at this time.</span></span>
   
    ![Aggiungere l'input di dati del flusso di dati](./media/stream-analytics-add-inputs/3-stream-analytics-add-inputs.png)  
   
    ![Aggiungere l'input di dati del flusso di dati](./media/stream-analytics-add-inputs/9-stream-analytics-add-inputs.png)  
4. <span data-ttu-id="7ecb8-132">Fornire un nome descrittivo per l'input nella finestra di Alias di Input.</span><span class="sxs-lookup"><span data-stu-id="7ecb8-132">Provide a friendly name for this input in the Input Alias box.</span></span>  <span data-ttu-id="7ecb8-133">Questo nome verrà utilizzare nella query del processo in un secondo momento per fare riferimento all'input.</span><span class="sxs-lookup"><span data-stu-id="7ecb8-133">This name will be used in your job's query later on to refer to the input.</span></span>
   
    <span data-ttu-id="7ecb8-134">Compilare il resto delle proprietà di connessione necessarie per connettersi all'origine dati.</span><span class="sxs-lookup"><span data-stu-id="7ecb8-134">Fill in the rest of the required connection properties to connect to your data source.</span></span> <span data-ttu-id="7ecb8-135">Questi campi variano in base al tipo di origine e di input e vengono definiti in modo dettagliato [qui](stream-analytics-create-a-job.md).</span><span class="sxs-lookup"><span data-stu-id="7ecb8-135">These fields vary by type of input and source type and are defined in detail [here](stream-analytics-create-a-job.md).</span></span>  
   
    ![Aggiungere l'input di dati dell'hub eventi](./media/stream-analytics-add-inputs/4-stream-analytics-add-inputs.png)  
5. <span data-ttu-id="7ecb8-137">Specificare le impostazioni di serializzazione per i dati di input:</span><span class="sxs-lookup"><span data-stu-id="7ecb8-137">Specify the serialization settings for the input data:</span></span>
   
   * <span data-ttu-id="7ecb8-138">Per assicurarsi che le query funzionino nel modo previsto, specificare il **Formato di serializzazione eventi** dei dati in arrivo.</span><span class="sxs-lookup"><span data-stu-id="7ecb8-138">To make sure your queries work the way you expect, specify the **Event Serialization Format** of incoming data.</span></span>  <span data-ttu-id="7ecb8-139">I formati di serializzazione supportati sono JSON, CSV e Avro.</span><span class="sxs-lookup"><span data-stu-id="7ecb8-139">Supported serialization formats are JSON, CSV, and Avro.</span></span>
   * <span data-ttu-id="7ecb8-140">Verificare la **Codifica** per i dati.</span><span class="sxs-lookup"><span data-stu-id="7ecb8-140">Verify the **Encoding** for the data.</span></span>  <span data-ttu-id="7ecb8-141">Al momento UTF-8 è l'unico formato di codifica supportato.</span><span class="sxs-lookup"><span data-stu-id="7ecb8-141">UTF-8 is the only supported encoding format at this time.</span></span>
     
     ![Impostazioni di serializzazione dei dati per l'input di dati](./media/stream-analytics-add-inputs/5-stream-analytics-add-inputs.png)  
     
     ![Impostazioni di serializzazione dei dati per l'input di dati](./media/stream-analytics-add-inputs/10-stream-analytics-add-inputs.png)  
6. <span data-ttu-id="7ecb8-144">Dopo aver completato la creazione dell’input, l’analisi di flusso verificherà che è possibile connettersi all'origine di input.</span><span class="sxs-lookup"><span data-stu-id="7ecb8-144">After completing the input creation, Stream Analytics will verify that it can connect to the input source.</span></span>  <span data-ttu-id="7ecb8-145">È possibile visualizzare lo stato dell'operazione di connessione di prova nell'hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="7ecb8-145">You can view the status of the Test Connection operation in the Notification hub.</span></span>
   
    ![Verificare la connessione dell'input dei flussi di dati](./media/stream-analytics-add-inputs/6-stream-analytics-add-inputs.png)  
   
    ![Verificare la connessione dell'input dei flussi di dati](./media/stream-analytics-add-inputs/11-stream-analytics-add-inputs.png)  

## <a name="get-help-with-streaming-data-inputs"></a><span data-ttu-id="7ecb8-148">Ottenere aiuto per gli input dei dati di streaming</span><span class="sxs-lookup"><span data-stu-id="7ecb8-148">Get help with streaming data inputs</span></span>
<span data-ttu-id="7ecb8-149">Per ulteriore assistenza, provare il [Forum di Analisi dei flussi di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="7ecb8-149">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ecb8-150">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7ecb8-150">Next steps</span></span>
* [<span data-ttu-id="7ecb8-151">Introduzione ad Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="7ecb8-151">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="7ecb8-152">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="7ecb8-152">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="7ecb8-153">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="7ecb8-153">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="7ecb8-154">Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="7ecb8-154">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="7ecb8-155">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="7ecb8-155">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

