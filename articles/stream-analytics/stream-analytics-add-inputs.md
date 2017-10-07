---
title: aaaAdd un tipo di dati di input i processi di flusso Analitica tooyour | Documenti Microsoft
description: Informazioni su come toohook backup un tooyour di origine dati Analitica di flusso di processo come flusso dati di input dai dati di riferimento o hub eventi dall'archiviazione BLOB.
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
ms.openlocfilehash: 674000268fcdf9bc000af3e2f166cb66f1366922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-streaming-data-input-or-reference-data-tooa-stream-analytics-job"></a><span data-ttu-id="3d0c3-104">Aggiungere un flusso dati di input o riferimento dati tooa Analitica flusso processo</span><span class="sxs-lookup"><span data-stu-id="3d0c3-104">Add a streaming data input or reference data tooa Stream Analytics job</span></span>
<span data-ttu-id="3d0c3-105">Informazioni su come toohook backup un tooyour di origine dati Analitica di flusso di processo come flusso dati di input dai dati di riferimento o hub eventi dall'archiviazione Blob.</span><span class="sxs-lookup"><span data-stu-id="3d0c3-105">Learn how toohook up a data source tooyour Stream Analytics job as streaming data input from Event Hubs or reference data from Blob storage.</span></span>

<span data-ttu-id="3d0c3-106">I processi di flusso Analitica Azure possono essere connesso tooone dati di input o altre, ciascuno dei quali definisce un'origine dati esistente tooan di connessione.</span><span class="sxs-lookup"><span data-stu-id="3d0c3-106">Azure Stream Analytics jobs can be connected tooone data input or more, each of which define a connection tooan existing data source.</span></span> <span data-ttu-id="3d0c3-107">Come origine dati toothat vengono inviati dati, è utilizzata dal processo di flusso Analitica hello ed elaborato in tempo reale come flusso di dati.</span><span class="sxs-lookup"><span data-stu-id="3d0c3-107">As data is sent toothat data source, it is consumed by hello Stream Analytics job and processed in real time as streaming data.</span></span> <span data-ttu-id="3d0c3-108">Flusso Analitica dispone di prima classe integrazione con [hub eventi di Azure](https://azure.microsoft.com/services/event-hubs/) e [archiviazione Blob di Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) all'interno e all'esterno di sottoscrizione del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="3d0c3-108">Stream Analytics has first class integration with [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) and [Azure Blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md) both within and outside of hello job's subscription.</span></span>

<span data-ttu-id="3d0c3-109">In questo articolo è un passaggio hello [percorso di apprendimento Analitica flusso](/documentation/learning-paths/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="3d0c3-109">This article is a step in hello [Stream Analytics learning path](/documentation/learning-paths/stream-analytics/).</span></span>

## <a name="data-input-streaming-data-and-reference-data"></a><span data-ttu-id="3d0c3-110">Input di dati: dati di streaming e dati di riferimento</span><span class="sxs-lookup"><span data-stu-id="3d0c3-110">Data input: Streaming data and reference data</span></span>
<span data-ttu-id="3d0c3-111">Esistono due tipi di input distinti in Analisi di flusso: dati di riferimento e flussi di dati.</span><span class="sxs-lookup"><span data-stu-id="3d0c3-111">There are two distinct types of inputs in Stream Analytics: data streams and reference data.</span></span>

* <span data-ttu-id="3d0c3-112">**Flussi di dati**: i processi di flusso Analitica devono includere almeno un dati flusso input toobe utilizzati e trasformati da processo hello.</span><span class="sxs-lookup"><span data-stu-id="3d0c3-112">**Data Streams**: Stream Analytics jobs must include at least one data stream input toobe consumed and transformed by hello job.</span></span> <span data-ttu-id="3d0c3-113">L'archivio BLOB di Azure e Hub eventi di Azure sono supportati come origini di input del flusso dei dati.</span><span class="sxs-lookup"><span data-stu-id="3d0c3-113">Azure Blob storage and Azure Event Hubs are supported as data stream input sources.</span></span> <span data-ttu-id="3d0c3-114">Hub eventi di Azure sono flussi di eventi toocollect utilizzati da dispositivi connessi, servizi e applicazioni.</span><span class="sxs-lookup"><span data-stu-id="3d0c3-114">Azure Event Hubs are used toocollect event streams from connected devices, services and applications.</span></span> <span data-ttu-id="3d0c3-115">Si può usare l'archivio BLOB di Azure come origine di input per l'inserimento di dati in blocco come flusso.</span><span class="sxs-lookup"><span data-stu-id="3d0c3-115">Azure Blob storage can be used as an input source for ingesting bulk data as a stream.</span></span>  
* <span data-ttu-id="3d0c3-116">**Dati di riferimento**: l’analisi di flusso supporta un secondo tipo di input ausiliario denominato dati di riferimento.</span><span class="sxs-lookup"><span data-stu-id="3d0c3-116">**Reference data**: Stream Analytics supports a second type of auxiliary input called reference data.</span></span>  <span data-ttu-id="3d0c3-117">Come toodata anziché in movimento, i dati sono statici o a modifica lenta.</span><span class="sxs-lookup"><span data-stu-id="3d0c3-117">As opposed toodata in motion, this data is static or slowing changing.</span></span>  <span data-ttu-id="3d0c3-118">In genere utilizzato per l'esecuzione di ricerche e correlazioni con flussi di dati toocreate un set di dati più completo.</span><span class="sxs-lookup"><span data-stu-id="3d0c3-118">It is typically used for performing look-ups and correlations with data streams toocreate a richer data set.</span></span>  <span data-ttu-id="3d0c3-119">Archiviazione Blob di Azure è attualmente origine di input hello è supportato solo per i dati di riferimento.</span><span class="sxs-lookup"><span data-stu-id="3d0c3-119">Azure Blob storage is currently hello only supported input source for reference data.</span></span>  

<span data-ttu-id="3d0c3-120">un processo di flusso Analitica tooyour input tooadd:</span><span class="sxs-lookup"><span data-stu-id="3d0c3-120">tooadd an input tooyour Stream Analytics job:</span></span>

1. <span data-ttu-id="3d0c3-121">Nel portale di Azure hello fare clic su **input** e quindi fare clic su **aggiungere un Input** nel processo di flusso Analitica.</span><span class="sxs-lookup"><span data-stu-id="3d0c3-121">In hello Azure portal click **Inputs** and then click **Add an Input** in your Stream Analytics job.</span></span>
   
    ![Portale di Azure classico - aggiungere un input.](./media/stream-analytics-add-inputs/1-stream-analytics-add-inputs.png)  
   
    <span data-ttu-id="3d0c3-123">In hello portale di Azure, fare clic su hello **input** riquadro nel processo di flusso Analitica.</span><span class="sxs-lookup"><span data-stu-id="3d0c3-123">In hello Azure portal click hello **Inputs** tile in your Stream Analytics job.</span></span>  
   
    ![Portale di Azure - aggiungere un input di dati.](./media/stream-analytics-add-inputs/7-stream-analytics-add-inputs.png)  
2. <span data-ttu-id="3d0c3-125">Specificare il tipo di hello dell'input hello: entrambi **flusso di dati** o **dati di riferimento**.</span><span class="sxs-lookup"><span data-stu-id="3d0c3-125">Specify hello type of hello input: either **Data stream** or **Reference data**.</span></span>
   
    ![Aggiungere i dati corretti hello di input, flusso o fare riferimento a](./media/stream-analytics-add-inputs/2-stream-analytics-add-inputs.png)  
   
    ![Aggiungere i dati corretti hello di input, flusso o fare riferimento a](./media/stream-analytics-add-inputs/8-stream-analytics-add-inputs.png)  
3. <span data-ttu-id="3d0c3-128">Se la creazione di un input del flusso di dati, specificare il tipo di origine hello per l'input hello.</span><span class="sxs-lookup"><span data-stu-id="3d0c3-128">If creating a Data Stream input, specify hello source type for hello input.</span></span>  <span data-ttu-id="3d0c3-129">Questo passaggio può essere ignorato durante la creazione dei dati di riferimento, poiché al momento è supportato soltanto l’archivio BLOB.</span><span class="sxs-lookup"><span data-stu-id="3d0c3-129">This step can be skipped during Reference Data creation as only Blob storage is supported at this time.</span></span>
   
    ![Aggiungere l'input di dati del flusso di dati](./media/stream-analytics-add-inputs/3-stream-analytics-add-inputs.png)  
   
    ![Aggiungere l'input di dati del flusso di dati](./media/stream-analytics-add-inputs/9-stream-analytics-add-inputs.png)  
4. <span data-ttu-id="3d0c3-132">Specificare un nome descrittivo per questo hello input nella casella di Alias di Input.</span><span class="sxs-lookup"><span data-stu-id="3d0c3-132">Provide a friendly name for this input in hello Input Alias box.</span></span>  <span data-ttu-id="3d0c3-133">Questo nome verrà utilizzato nella query del processo in un secondo momento nel toorefer toohello input.</span><span class="sxs-lookup"><span data-stu-id="3d0c3-133">This name will be used in your job's query later on toorefer toohello input.</span></span>
   
    <span data-ttu-id="3d0c3-134">Compilare il resto di hello di origine dei dati tooyour proprietà tooconnect hello necessarie per la connessione.</span><span class="sxs-lookup"><span data-stu-id="3d0c3-134">Fill in hello rest of hello required connection properties tooconnect tooyour data source.</span></span> <span data-ttu-id="3d0c3-135">Questi campi variano in base al tipo di origine e di input e vengono definiti in modo dettagliato [qui](stream-analytics-create-a-job.md).</span><span class="sxs-lookup"><span data-stu-id="3d0c3-135">These fields vary by type of input and source type and are defined in detail [here](stream-analytics-create-a-job.md).</span></span>  
   
    ![Aggiungere l'input di dati dell'hub eventi](./media/stream-analytics-add-inputs/4-stream-analytics-add-inputs.png)  
5. <span data-ttu-id="3d0c3-137">Specificare le impostazioni di serializzazione hello per dati di input hello:</span><span class="sxs-lookup"><span data-stu-id="3d0c3-137">Specify hello serialization settings for hello input data:</span></span>
   
   * <span data-ttu-id="3d0c3-138">toomake che le query funzionino come hello previsto, specificare hello **il formato di serializzazione di eventi** dei dati in arrivo.</span><span class="sxs-lookup"><span data-stu-id="3d0c3-138">toomake sure your queries work hello way you expect, specify hello **Event Serialization Format** of incoming data.</span></span>  <span data-ttu-id="3d0c3-139">I formati di serializzazione supportati sono JSON, CSV e Avro.</span><span class="sxs-lookup"><span data-stu-id="3d0c3-139">Supported serialization formats are JSON, CSV, and Avro.</span></span>
   * <span data-ttu-id="3d0c3-140">Verificare hello **codifica** per i dati di hello.</span><span class="sxs-lookup"><span data-stu-id="3d0c3-140">Verify hello **Encoding** for hello data.</span></span>  <span data-ttu-id="3d0c3-141">UTF-8 è hello formato di codifica è supportata solo in questo momento.</span><span class="sxs-lookup"><span data-stu-id="3d0c3-141">UTF-8 is hello only supported encoding format at this time.</span></span>
     
     ![Impostazioni di serializzazione di dati per l'input di dati hello](./media/stream-analytics-add-inputs/5-stream-analytics-add-inputs.png)  
     
     ![Impostazioni di serializzazione di dati per l'input di dati hello](./media/stream-analytics-add-inputs/10-stream-analytics-add-inputs.png)  
6. <span data-ttu-id="3d0c3-144">Dopo aver completato la creazione di input hello, flusso Analitica verificherà che è possibile connettere l'origine di input toohello.</span><span class="sxs-lookup"><span data-stu-id="3d0c3-144">After completing hello input creation, Stream Analytics will verify that it can connect toohello input source.</span></span>  <span data-ttu-id="3d0c3-145">È possibile visualizzare lo stato di hello di hello operazione di connessione di Test nell'hub di notifica hello.</span><span class="sxs-lookup"><span data-stu-id="3d0c3-145">You can view hello status of hello Test Connection operation in hello Notification hub.</span></span>
   
    ![Test della connessione di hello flusso di dati di input](./media/stream-analytics-add-inputs/6-stream-analytics-add-inputs.png)  
   
    ![Test della connessione di hello flusso di dati di input](./media/stream-analytics-add-inputs/11-stream-analytics-add-inputs.png)  

## <a name="get-help-with-streaming-data-inputs"></a><span data-ttu-id="3d0c3-148">Ottenere aiuto per gli input dei dati di streaming</span><span class="sxs-lookup"><span data-stu-id="3d0c3-148">Get help with streaming data inputs</span></span>
<span data-ttu-id="3d0c3-149">Per ulteriore assistenza, provare il [Forum di Analisi dei flussi di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="3d0c3-149">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d0c3-150">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3d0c3-150">Next steps</span></span>
* [<span data-ttu-id="3d0c3-151">Introduzione tooAzure flusso Analitica</span><span class="sxs-lookup"><span data-stu-id="3d0c3-151">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="3d0c3-152">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="3d0c3-152">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="3d0c3-153">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="3d0c3-153">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="3d0c3-154">Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="3d0c3-154">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="3d0c3-155">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="3d0c3-155">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

