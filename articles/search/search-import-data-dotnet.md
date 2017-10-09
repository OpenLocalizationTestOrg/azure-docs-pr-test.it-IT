---
title: aaa "caricamento di dati (.NET - ricerca di Azure) | Documenti di Microsoft"
description: Informazioni su come indice di tooan tooupload dati in ricerca di Azure tramite hello .NET SDK.
services: search
documentationcenter: 
author: brjohnstmsft
manager: jhubbard
editor: 
tags: 
ms.assetid: 0e0e7e7b-7178-4c26-95c6-2fd1e8015aca
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 01/13/2017
ms.author: brjohnst
ms.openlocfilehash: 78ddbefb522884d1f61cb275c25c091487aee639
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-tooazure-search-using-hello-net-sdk"></a><span data-ttu-id="ce86f-103">Caricamento dati tooAzure ricerca tramite hello .NET SDK</span><span class="sxs-lookup"><span data-stu-id="ce86f-103">Upload data tooAzure Search using hello .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ce86f-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="ce86f-104">Overview</span></span>](search-what-is-data-import.md)
> * [<span data-ttu-id="ce86f-105">.NET</span><span class="sxs-lookup"><span data-stu-id="ce86f-105">.NET</span></span>](search-import-data-dotnet.md)
> * [<span data-ttu-id="ce86f-106">REST</span><span class="sxs-lookup"><span data-stu-id="ce86f-106">REST</span></span>](search-import-data-rest-api.md)
> 
> 

<span data-ttu-id="ce86f-107">In questo articolo viene illustrato come hello toouse [Azure Search .NET SDK](https://aka.ms/search-sdk) tooimport dati in un indice di ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="ce86f-107">This article will show you how toouse hello [Azure Search .NET SDK](https://aka.ms/search-sdk) tooimport data into an Azure Search index.</span></span>

<span data-ttu-id="ce86f-108">Prima di iniziare questa procedura dettagliata, è necessario avere [creato un indice di Ricerca di Azure](search-what-is-an-index.md).</span><span class="sxs-lookup"><span data-stu-id="ce86f-108">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md).</span></span> <span data-ttu-id="ce86f-109">In questo articolo si presuppone inoltre che è già stato creato un `SearchServiceClient` dell'oggetto, come illustrato nella [creare un indice di ricerca di Azure mediante .NET SDK hello](search-create-index-dotnet.md#CreateSearchServiceClient).</span><span class="sxs-lookup"><span data-stu-id="ce86f-109">This article also assumes that you have already created a `SearchServiceClient` object, as shown in [Create an Azure Search index using hello .NET SDK](search-create-index-dotnet.md#CreateSearchServiceClient).</span></span>

> [!NOTE]
> <span data-ttu-id="ce86f-110">Tutto il codice di esempio in questo articolo è scritto in C#.</span><span class="sxs-lookup"><span data-stu-id="ce86f-110">All sample code in this article is written in C#.</span></span> <span data-ttu-id="ce86f-111">È possibile trovare il codice sorgente completo hello [su GitHub](http://aka.ms/search-dotnet-howto).</span><span class="sxs-lookup"><span data-stu-id="ce86f-111">You can find hello full source code [on GitHub](http://aka.ms/search-dotnet-howto).</span></span> <span data-ttu-id="ce86f-112">È inoltre possibile leggere sulla hello [Azure Search .NET SDK](search-howto-dotnet-sdk.md) per una più dettagliata procedura hello del codice di esempio.</span><span class="sxs-lookup"><span data-stu-id="ce86f-112">You can also read about hello [Azure Search .NET SDK](search-howto-dotnet-sdk.md) for a more detailed walk through of hello sample code.</span></span>

<span data-ttu-id="ce86f-113">Nei documenti di ordine toopush nell'indice utilizzando hello .NET SDK, sarà necessario:</span><span class="sxs-lookup"><span data-stu-id="ce86f-113">In order toopush documents into your index using hello .NET SDK, you will need to:</span></span>

1. <span data-ttu-id="ce86f-114">Creare un `SearchIndexClient` oggetto tooconnect tooyour indice di ricerca.</span><span class="sxs-lookup"><span data-stu-id="ce86f-114">Create a `SearchIndexClient` object tooconnect tooyour search index.</span></span>
2. <span data-ttu-id="ce86f-115">Creare un `IndexBatch` contenente hello documenti toobe aggiunti, modificati o eliminati.</span><span class="sxs-lookup"><span data-stu-id="ce86f-115">Create an `IndexBatch` containing hello documents toobe added, modified, or deleted.</span></span>
3. <span data-ttu-id="ce86f-116">Chiamare hello `Documents.Index` metodo i `SearchIndexClient` toosend hello `IndexBatch` tooyour indice di ricerca.</span><span class="sxs-lookup"><span data-stu-id="ce86f-116">Call hello `Documents.Index` method of your `SearchIndexClient` toosend hello `IndexBatch` tooyour search index.</span></span>

## <a name="create-an-instance-of-hello-searchindexclient-class"></a><span data-ttu-id="ce86f-117">Creare un'istanza della classe SearchIndexClient hello</span><span class="sxs-lookup"><span data-stu-id="ce86f-117">Create an instance of hello SearchIndexClient class</span></span>
<span data-ttu-id="ce86f-118">l'indice utilizzando dati tooimport hello Azure Search .NET SDK, sarà necessario toocreate un'istanza di hello `SearchIndexClient` classe.</span><span class="sxs-lookup"><span data-stu-id="ce86f-118">tooimport data into your index using hello Azure Search .NET SDK, you will need toocreate an instance of hello `SearchIndexClient` class.</span></span> <span data-ttu-id="ce86f-119">È possibile creare questa istanza di se stessi, ma più semplice se si dispone già di un `SearchServiceClient` toocall istanza relativa `Indexes.GetClient` metodo.</span><span class="sxs-lookup"><span data-stu-id="ce86f-119">You can construct this instance yourself, but it's easier if you already have a `SearchServiceClient` instance toocall its `Indexes.GetClient` method.</span></span> <span data-ttu-id="ce86f-120">Ad esempio, ecco come è possibile ottenere un `SearchIndexClient` per hello indice denominata "Hotel" da un `SearchServiceClient` denominato `serviceClient`:</span><span class="sxs-lookup"><span data-stu-id="ce86f-120">For example, here is how you would obtain a `SearchIndexClient` for hello index named "hotels" from a `SearchServiceClient` named `serviceClient`:</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> <span data-ttu-id="ce86f-121">In un'applicazione di ricerca tipica, il popolamento e la gestione degli indici viene gestita da un componente separato dalle query di ricerca.</span><span class="sxs-lookup"><span data-stu-id="ce86f-121">In a typical search application, index management and population is handled by a separate component from search queries.</span></span> <span data-ttu-id="ce86f-122">`Indexes.GetClient`è utile per la compilazione di un indice perché si salva hello problemi di fornire un altro `SearchCredentials`.</span><span class="sxs-lookup"><span data-stu-id="ce86f-122">`Indexes.GetClient` is convenient for populating an index because it saves you hello trouble of providing another `SearchCredentials`.</span></span> <span data-ttu-id="ce86f-123">A tale scopo, passando la chiave di amministrazione hello hello toocreate utilizzati che si `SearchServiceClient` toohello nuova `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="ce86f-123">It does this by passing hello admin key that you used toocreate hello `SearchServiceClient` toohello new `SearchIndexClient`.</span></span> <span data-ttu-id="ce86f-124">Tuttavia, in parte dell'applicazione che esegue query hello è migliore hello toocreate `SearchIndexClient` direttamente in modo che è possibile passare una chiave di query anziché una chiave amministratore.</span><span class="sxs-lookup"><span data-stu-id="ce86f-124">However, in hello part of your application that executes queries, it is better toocreate hello `SearchIndexClient` directly so that you can pass in a query key instead of an admin key.</span></span> <span data-ttu-id="ce86f-125">Questo comportamento è coerente con hello [principio di privilegio minimo](https://en.wikipedia.org/wiki/Principle_of_least_privilege) e consentirà toomake l'applicazione più sicura.</span><span class="sxs-lookup"><span data-stu-id="ce86f-125">This is consistent with hello [principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege) and will help toomake your application more secure.</span></span> <span data-ttu-id="ce86f-126">È possibile trovare ulteriori informazioni sulle chiavi amministratore e le chiavi di query in hello [riferimento API REST di ricerca di Azure](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="ce86f-126">You can find out more about admin keys and query keys in hello [Azure Search REST API reference](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
> 
> 

<span data-ttu-id="ce86f-127">`SearchIndexClient` include una proprietà `Documents`.</span><span class="sxs-lookup"><span data-stu-id="ce86f-127">`SearchIndexClient` has a `Documents` property.</span></span> <span data-ttu-id="ce86f-128">Questa proprietà fornisce tutti i metodi di hello è necessario tooadd, modificare, eliminare o eseguire query sui documenti nell'indice.</span><span class="sxs-lookup"><span data-stu-id="ce86f-128">This property provides all hello methods you need tooadd, modify, delete, or query documents in your index.</span></span>

## <a name="decide-which-indexing-action-toouse"></a><span data-ttu-id="ce86f-129">Decidere quali indicizzazione toouse azione</span><span class="sxs-lookup"><span data-stu-id="ce86f-129">Decide which indexing action toouse</span></span>
<span data-ttu-id="ce86f-130">dati tooimport utilizzando hello .NET SDK, sarà necessario toopackage backup dei dati in un `IndexBatch` oggetto.</span><span class="sxs-lookup"><span data-stu-id="ce86f-130">tooimport data using hello .NET SDK, you will need toopackage up your data into an `IndexBatch` object.</span></span> <span data-ttu-id="ce86f-131">Un `IndexBatch` incapsula una raccolta di `IndexAction` oggetti, ognuno dei quali contiene un documento e una proprietà che indica quali tooperform azione di ricerca di Azure su tale documento (caricamento, unione, eliminazione e così via).</span><span class="sxs-lookup"><span data-stu-id="ce86f-131">An `IndexBatch` encapsulates a collection of `IndexAction` objects, each of which contains a document and a property that tells Azure Search what action tooperform on that document (upload, merge, delete, etc).</span></span> <span data-ttu-id="ce86f-132">A seconda di quale dei hello si sceglie di azioni riportate di seguito, solo alcuni campi devono essere inclusi per ogni documento:</span><span class="sxs-lookup"><span data-stu-id="ce86f-132">Depending on which of hello below actions you choose, only certain fields must be included for each document:</span></span>

| <span data-ttu-id="ce86f-133">Azione</span><span class="sxs-lookup"><span data-stu-id="ce86f-133">Action</span></span> | <span data-ttu-id="ce86f-134">Description</span><span class="sxs-lookup"><span data-stu-id="ce86f-134">Description</span></span> | <span data-ttu-id="ce86f-135">Campi necessari per ogni documento</span><span class="sxs-lookup"><span data-stu-id="ce86f-135">Necessary fields for each document</span></span> | <span data-ttu-id="ce86f-136">Note</span><span class="sxs-lookup"><span data-stu-id="ce86f-136">Notes</span></span> |
| --- | --- | --- | --- |
| `Upload` |<span data-ttu-id="ce86f-137">Un `Upload` tooan simile "upsert" in cui verrà inserito se è nuovo e aggiornato/sostituito se esiste il documento hello è intervento dell'utente.</span><span class="sxs-lookup"><span data-stu-id="ce86f-137">An `Upload` action is similar tooan "upsert" where hello document will be inserted if it is new and updated/replaced if it exists.</span></span> |<span data-ttu-id="ce86f-138">chiave, oltre a tutti gli altri campi che si desidera toodefine</span><span class="sxs-lookup"><span data-stu-id="ce86f-138">key, plus any other fields you wish toodefine</span></span> |<span data-ttu-id="ce86f-139">Durante l'aggiornamento o la sostituzione di un documento esistente, qualsiasi campo che non è specificato nella richiesta di hello avrà il campo impostato troppo`null`.</span><span class="sxs-lookup"><span data-stu-id="ce86f-139">When updating/replacing an existing document, any field that is not specified in hello request will have its field set too`null`.</span></span> <span data-ttu-id="ce86f-140">Questo errore si verifica anche quando il campo hello è stato impostato precedentemente valore non null tooa.</span><span class="sxs-lookup"><span data-stu-id="ce86f-140">This occurs even when hello field was previously set tooa non-null value.</span></span> |
| `Merge` |<span data-ttu-id="ce86f-141">Gli aggiornamenti del documento esistente con hello specificati campi.</span><span class="sxs-lookup"><span data-stu-id="ce86f-141">Updates an existing document with hello specified fields.</span></span> <span data-ttu-id="ce86f-142">Se non esiste alcun documento hello nell'indice hello, merge hello avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="ce86f-142">If hello document does not exist in hello index, hello merge will fail.</span></span> |<span data-ttu-id="ce86f-143">chiave, oltre a tutti gli altri campi che si desidera toodefine</span><span class="sxs-lookup"><span data-stu-id="ce86f-143">key, plus any other fields you wish toodefine</span></span> |<span data-ttu-id="ce86f-144">Qualsiasi campo specificato in un'unione sostituirà campo esistente di hello nel documento hello.</span><span class="sxs-lookup"><span data-stu-id="ce86f-144">Any field you specify in a merge will replace hello existing field in hello document.</span></span> <span data-ttu-id="ce86f-145">Sono inclusi anche i campi di tipo `DataType.Collection(DataType.String)`.</span><span class="sxs-lookup"><span data-stu-id="ce86f-145">This includes fields of type `DataType.Collection(DataType.String)`.</span></span> <span data-ttu-id="ce86f-146">Ad esempio, se hello documento contiene un campo `tags` con valore `["budget"]` e si esegue un'unione con valore `["economy", "pool"]` per `tags`, il valore finale di hello hello `tags` campo sarà `["economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="ce86f-146">For example, if hello document contains a field `tags` with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for `tags`, hello final value of hello `tags` field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="ce86f-147">e non `["budget", "economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="ce86f-147">It will not be `["budget", "economy", "pool"]`.</span></span> |
| `MergeOrUpload` |<span data-ttu-id="ce86f-148">Questa azione è analoga `Merge` se esiste un documento con hello data già chiave nell'indice hello.</span><span class="sxs-lookup"><span data-stu-id="ce86f-148">This action behaves like `Merge` if a document with hello given key already exists in hello index.</span></span> <span data-ttu-id="ce86f-149">Se il documento hello non esiste, si comporta come `Upload` con un nuovo documento.</span><span class="sxs-lookup"><span data-stu-id="ce86f-149">If hello document does not exist, it behaves like `Upload` with a new document.</span></span> |<span data-ttu-id="ce86f-150">chiave, oltre a tutti gli altri campi che si desidera toodefine</span><span class="sxs-lookup"><span data-stu-id="ce86f-150">key, plus any other fields you wish toodefine</span></span> |- |
| `Delete` |<span data-ttu-id="ce86f-151">Rimozione di documento specificato hello dall'indice di hello.</span><span class="sxs-lookup"><span data-stu-id="ce86f-151">Removes hello specified document from hello index.</span></span> |<span data-ttu-id="ce86f-152">solo campo chiave</span><span class="sxs-lookup"><span data-stu-id="ce86f-152">key only</span></span> |<span data-ttu-id="ce86f-153">Tutti i campi specificare diverso hello chiave campo verrà ignorato.</span><span class="sxs-lookup"><span data-stu-id="ce86f-153">Any fields you specify other than hello key field will be ignored.</span></span> <span data-ttu-id="ce86f-154">Se si desidera tooremove un singolo campo da un documento, utilizzare `Merge` invece e impostare semplicemente il campo hello in modo esplicito toonull.</span><span class="sxs-lookup"><span data-stu-id="ce86f-154">If you want tooremove an individual field from a document, use `Merge` instead and simply set hello field explicitly toonull.</span></span> |

<span data-ttu-id="ce86f-155">È possibile specificare quale azione si desidera toouse con diversi metodi statici di hello hello `IndexBatch` e `IndexAction` classi, come illustrato nella sezione successiva hello.</span><span class="sxs-lookup"><span data-stu-id="ce86f-155">You can specify what action you want toouse with hello various static methods of hello `IndexBatch` and `IndexAction` classes, as shown in hello next section.</span></span>

## <a name="construct-your-indexbatch"></a><span data-ttu-id="ce86f-156">Costruire IndexBatch</span><span class="sxs-lookup"><span data-stu-id="ce86f-156">Construct your IndexBatch</span></span>
<span data-ttu-id="ce86f-157">Ora che si conosce quali tooperform azioni sui documenti, si è pronti tooconstruct hello `IndexBatch`.</span><span class="sxs-lookup"><span data-stu-id="ce86f-157">Now that you know which actions tooperform on your documents, you are ready tooconstruct hello `IndexBatch`.</span></span> <span data-ttu-id="ce86f-158">Hello di esempio seguente viene illustrato come toocreate un batch con alcune azioni.</span><span class="sxs-lookup"><span data-stu-id="ce86f-158">hello example below shows how toocreate a batch with a few different actions.</span></span> <span data-ttu-id="ce86f-159">Si noti che questo esempio Usa una classe personalizzata denominata `Hotel` tooa documento nell'indice "Hotel" hello che esegue il mapping.</span><span class="sxs-lookup"><span data-stu-id="ce86f-159">Note that our example uses a custom class called `Hotel` that maps tooa document in hello "hotels" index.</span></span>

```csharp
var actions =
    new IndexAction<Hotel>[]
    {
        IndexAction.Upload(
            new Hotel()
            {
                HotelId = "1",
                BaseRate = 199.0,
                Description = "Best hotel in town",
                DescriptionFr = "Meilleur hôtel en ville",
                HotelName = "Fancy Stay",
                Category = "Luxury",
                Tags = new[] { "pool", "view", "wifi", "concierge" },
                ParkingIncluded = false,
                SmokingAllowed = false,
                LastRenovationDate = new DateTimeOffset(2010, 6, 27, 0, 0, 0, TimeSpan.Zero),
                Rating = 5,
                Location = GeographyPoint.Create(47.678581, -122.131577)
            }),
        IndexAction.Upload(
            new Hotel()
            {
                HotelId = "2",
                BaseRate = 79.99,
                Description = "Cheapest hotel in town",
                DescriptionFr = "Hôtel le moins cher en ville",
                HotelName = "Roach Motel",
                Category = "Budget",
                Tags = new[] { "motel", "budget" },
                ParkingIncluded = true,
                SmokingAllowed = true,
                LastRenovationDate = new DateTimeOffset(1982, 4, 28, 0, 0, 0, TimeSpan.Zero),
                Rating = 1,
                Location = GeographyPoint.Create(49.678581, -122.131577)
            }),
        IndexAction.MergeOrUpload(
            new Hotel()
            {
                HotelId = "3",
                BaseRate = 129.99,
                Description = "Close tootown hall and hello river"
            }),
        IndexAction.Delete(new Hotel() { HotelId = "6" })
    };

var batch = IndexBatch.New(actions);
```

<span data-ttu-id="ce86f-160">In questo caso, si sta usando `Upload`, `MergeOrUpload`, e `Delete` come azioni la ricerca, come specificato dai metodi hello chiamati su hello `IndexAction` classe.</span><span class="sxs-lookup"><span data-stu-id="ce86f-160">In this case, we are using `Upload`, `MergeOrUpload`, and `Delete` as our search actions, as specified by hello methods called on hello `IndexAction` class.</span></span>

<span data-ttu-id="ce86f-161">Si supponga che l'indice "hotels" di esempio sia già popolato con alcuni documenti.</span><span class="sxs-lookup"><span data-stu-id="ce86f-161">Assume that this example "hotels" index is already populated with a number of documents.</span></span> <span data-ttu-id="ce86f-162">Si noti come non è toospecify tutti i campi del documento possibili hello quando si utilizza `MergeOrUpload` e come viene specificata solo la chiave di documento hello (`HotelId`) quando si utilizza `Delete`.</span><span class="sxs-lookup"><span data-stu-id="ce86f-162">Note how we did not have toospecify all hello possible document fields when using `MergeOrUpload` and how we only specified hello document key (`HotelId`) when using `Delete`.</span></span>

<span data-ttu-id="ce86f-163">Si noti inoltre che è possibile includere solo i documenti too1000 in una singola richiesta di indicizzazione.</span><span class="sxs-lookup"><span data-stu-id="ce86f-163">Also, note that you can only include up too1000 documents in a single indexing request.</span></span>

> [!NOTE]
> <span data-ttu-id="ce86f-164">In questo esempio, viene applicata la documenti toodifferent azioni diverse.</span><span class="sxs-lookup"><span data-stu-id="ce86f-164">In this example, we are applying different actions toodifferent documents.</span></span> <span data-ttu-id="ce86f-165">Se si desidera tooperform hello azioni stesso in tutti i documenti nel batch di hello, anziché chiamare `IndexBatch.New`, è possibile utilizzare altri metodi statici di hello `IndexBatch`.</span><span class="sxs-lookup"><span data-stu-id="ce86f-165">If you wanted tooperform hello same actions across all documents in hello batch, instead of calling `IndexBatch.New`, you could use hello other static methods of `IndexBatch`.</span></span> <span data-ttu-id="ce86f-166">Ad esempio, è possibile creare batch chiamando `IndexBatch.Merge`, `IndexBatch.MergeOrUpload` o `IndexBatch.Delete`.</span><span class="sxs-lookup"><span data-stu-id="ce86f-166">For example, you could create batches by calling `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, or `IndexBatch.Delete`.</span></span> <span data-ttu-id="ce86f-167">Questi metodi accettano una raccolta di documenti (oggetti di tipo `Hotel` in questo esempio) invece di oggetti `IndexAction`.</span><span class="sxs-lookup"><span data-stu-id="ce86f-167">These methods take a collection of documents (objects of type `Hotel` in this example) instead of `IndexAction` objects.</span></span>
> 
> 

## <a name="import-data-toohello-index"></a><span data-ttu-id="ce86f-168">Indice toohello di importazione dei dati</span><span class="sxs-lookup"><span data-stu-id="ce86f-168">Import data toohello index</span></span>
<span data-ttu-id="ce86f-169">Dopo aver creato un oggetto inizializzato `IndexBatch` dell'oggetto, è possibile inviarlo indice toohello chiamando `Documents.Index` sul `SearchIndexClient` oggetto.</span><span class="sxs-lookup"><span data-stu-id="ce86f-169">Now that you have an initialized `IndexBatch` object, you can send it toohello index by calling `Documents.Index` on your `SearchIndexClient` object.</span></span> <span data-ttu-id="ce86f-170">Hello seguente esempio viene illustrato come toocall `Index`, nonché come alcuni passaggi aggiuntivi che sarà necessario tooperform:</span><span class="sxs-lookup"><span data-stu-id="ce86f-170">hello following example shows how toocall `Index`, as well as some extra steps you will need tooperform:</span></span>

```csharp
try
{
    indexClient.Documents.Index(batch);
}
catch (IndexBatchException e)
{
    // Sometimes when your Search service is under load, indexing will fail for some of hello documents in
    // hello batch. Depending on your application, you can take compensating actions like delaying and
    // retrying. For this simple demo, we just log hello failed document keys and continue.
    Console.WriteLine(
        "Failed tooindex some of hello documents: {0}",
        String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
}

Console.WriteLine("Waiting for documents toobe indexed...\n");
Thread.Sleep(2000);
```

<span data-ttu-id="ce86f-171">Hello nota `try` / `catch` circostanti hello chiamata toohello `Index` metodo.</span><span class="sxs-lookup"><span data-stu-id="ce86f-171">Note hello `try`/`catch` surrounding hello call toohello `Index` method.</span></span> <span data-ttu-id="ce86f-172">blocco catch Hello gestisce un caso di errore importanti per l'indicizzazione.</span><span class="sxs-lookup"><span data-stu-id="ce86f-172">hello catch block handles an important error case for indexing.</span></span> <span data-ttu-id="ce86f-173">Se il servizio di ricerca di Azure non riesce tooindex hello alcuni documenti nel batch di hello, un `IndexBatchException` viene generata da `Documents.Index`.</span><span class="sxs-lookup"><span data-stu-id="ce86f-173">If your Azure Search service fails tooindex some of hello documents in hello batch, an `IndexBatchException` is thrown by `Documents.Index`.</span></span> <span data-ttu-id="ce86f-174">Questa situazione può verificarsi se l'indicizzazione dei documenti avviene mentre il servizio è sovraccarico.</span><span class="sxs-lookup"><span data-stu-id="ce86f-174">This can happen if you are indexing documents while your service is under heavy load.</span></span> <span data-ttu-id="ce86f-175">**Si consiglia di gestire in modo esplicito questo caso nel codice.**</span><span class="sxs-lookup"><span data-stu-id="ce86f-175">**We strongly recommend explicitly handling this case in your code.**</span></span> <span data-ttu-id="ce86f-176">È possibile ritardare e quindi ripetere l'indicizzazione documenti hello che non è riuscita oppure è possibile accedere e continuare come esempio hello non oppure è possibile eseguire qualcos'altro a seconda dei requisiti di coerenza dei dati dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ce86f-176">You can delay and then retry indexing hello documents that failed, or you can log and continue like hello sample does, or you can do something else depending on your application's data consistency requirements.</span></span>

<span data-ttu-id="ce86f-177">Infine, hello codice di esempio hello sopra ritardi di due secondi.</span><span class="sxs-lookup"><span data-stu-id="ce86f-177">Finally, hello code in hello example above delays for two seconds.</span></span> <span data-ttu-id="ce86f-178">L'indicizzazione avviene in modo asincrono nel servizio di ricerca di Azure, quindi l'applicazione di esempio hello deve toowait tooensure un breve periodo di tempo che sono disponibili per la ricerca di documenti di hello.</span><span class="sxs-lookup"><span data-stu-id="ce86f-178">Indexing happens asynchronously in your Azure Search service, so hello sample application needs toowait a short time tooensure that hello documents are available for searching.</span></span> <span data-ttu-id="ce86f-179">Ritardi come questi in genere sono necessari solo in applicazioni di esempio, test e demo.</span><span class="sxs-lookup"><span data-stu-id="ce86f-179">Delays like this are typically only necessary in demos, tests, and sample applications.</span></span>

<a name="HotelClass"></a>

### <a name="how-hello-net-sdk-handles-documents"></a><span data-ttu-id="ce86f-180">La modalità di gestione di documenti hello .NET SDK</span><span class="sxs-lookup"><span data-stu-id="ce86f-180">How hello .NET SDK handles documents</span></span>
<span data-ttu-id="ce86f-181">Per comprendere come hello Azure Search .NET SDK è istanze tooupload in grado di una classe definita dall'utente come `Hotel` toohello indice.</span><span class="sxs-lookup"><span data-stu-id="ce86f-181">You may be wondering how hello Azure Search .NET SDK is able tooupload instances of a user-defined class like `Hotel` toohello index.</span></span> <span data-ttu-id="ce86f-182">toohelp rispondere alla domanda, si esaminerà hello `Hotel` (classe), che esegue il mapping dello schema di indice toohello definito in [creare un indice di ricerca di Azure mediante .NET SDK hello](search-create-index-dotnet.md#DefineIndex):</span><span class="sxs-lookup"><span data-stu-id="ce86f-182">toohelp answer that question, let's look at hello `Hotel` class, which maps toohello index schema defined in [Create an Azure Search index using hello .NET SDK](search-create-index-dotnet.md#DefineIndex):</span></span>

```csharp
[SerializePropertyNamesAsCamelCase]
public partial class Hotel
{
    [Key]
    [IsFilterable]
    public string HotelId { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public double? BaseRate { get; set; }

    [IsSearchable]
    public string Description { get; set; }

    [IsSearchable]
    [Analyzer(AnalyzerName.AsString.FrLucene)]
    [JsonProperty("description_fr")]
    public string DescriptionFr { get; set; }

    [IsSearchable, IsFilterable, IsSortable]
    public string HotelName { get; set; }

    [IsSearchable, IsFilterable, IsSortable, IsFacetable]
    public string Category { get; set; }

    [IsSearchable, IsFilterable, IsFacetable]
    public string[] Tags { get; set; }

    [IsFilterable, IsFacetable]
    public bool? ParkingIncluded { get; set; }

    [IsFilterable, IsFacetable]
    public bool? SmokingAllowed { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public DateTimeOffset? LastRenovationDate { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public int? Rating { get; set; }

    [IsFilterable, IsSortable]
    public GeographyPoint Location { get; set; }

    // ToString() method omitted for brevity...
}
```

<span data-ttu-id="ce86f-183">Hello in primo luogo toonotice è che ogni proprietà pubblica di `Hotel` corrisponde tooa campo nella definizione dell'indice hello, ma con una differenza fondamentale: nome hello di ogni campo inizia con una lettera minuscola ("caso camel"), mentre il nome di hello ogni pubblico proprietà di `Hotel` inizia con una lettera maiuscola ("convenzione Pascal").</span><span class="sxs-lookup"><span data-stu-id="ce86f-183">hello first thing toonotice is that each public property of `Hotel` corresponds tooa field in hello index definition, but with one crucial difference: hello name of each field starts with a lower-case letter ("camel case"), while hello name of each public property of `Hotel` starts with an upper-case letter ("Pascal case").</span></span> <span data-ttu-id="ce86f-184">Si tratta di uno scenario comune in applicazioni .NET che eseguire il binding di dati in cui lo schema di destinazione hello è controllo hello di fuori di sviluppatore dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="ce86f-184">This is a common scenario in .NET applications that perform data-binding where hello target schema is outside hello control of hello application developer.</span></span> <span data-ttu-id="ce86f-185">Invece di tooviolate hello .NET convenzioni di denominazione rendendo proprietà nomi maiuscole-minuscole camel, è possibile indicare hello SDK toomap hello proprietà nomi toocamel caso automaticamente con hello `[SerializePropertyNamesAsCamelCase]` attributo.</span><span class="sxs-lookup"><span data-stu-id="ce86f-185">Rather than having tooviolate hello .NET naming guidelines by making property names camel-case, you can tell hello SDK toomap hello property names toocamel-case automatically with hello `[SerializePropertyNamesAsCamelCase]` attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="ce86f-186">Hello Azure Search .NET SDK Usa hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) tooserialize libreria e deserializzare tooand di oggetti del modello personalizzato da JSON.</span><span class="sxs-lookup"><span data-stu-id="ce86f-186">hello Azure Search .NET SDK uses hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) library tooserialize and deserialize your custom model objects tooand from JSON.</span></span> <span data-ttu-id="ce86f-187">Se necessario, è possibile personalizzare questa serializzazione.</span><span class="sxs-lookup"><span data-stu-id="ce86f-187">You can customize this serialization if needed.</span></span> <span data-ttu-id="ce86f-188">Per altri dettagli, vedere [Serializzazione personalizzata con JSON.NET](search-howto-dotnet-sdk.md#JsonDotNet).</span><span class="sxs-lookup"><span data-stu-id="ce86f-188">You can find more details in [Custom Serialization with JSON.NET](search-howto-dotnet-sdk.md#JsonDotNet).</span></span> <span data-ttu-id="ce86f-189">Un esempio di questo è l'utilizzo di hello di hello `[JsonProperty]` attributo hello `DescriptionFr` proprietà nel codice di esempio hello precedente.</span><span class="sxs-lookup"><span data-stu-id="ce86f-189">One example of this is hello use of hello `[JsonProperty]` attribute on hello `DescriptionFr` property in hello sample code above.</span></span>
> 
> 

<span data-ttu-id="ce86f-190">Hello secondo importante su hello `Hotel` classe sono tipi di dati hello delle proprietà pubbliche di hello.</span><span class="sxs-lookup"><span data-stu-id="ce86f-190">hello second important thing about hello `Hotel` class are hello data types of hello public properties.</span></span> <span data-ttu-id="ce86f-191">tipi di queste proprietà .NET Hello mappare i tipi di campo equivalente tootheir nella definizione dell'indice hello.</span><span class="sxs-lookup"><span data-stu-id="ce86f-191">hello .NET types of these properties map tootheir equivalent field types in hello index definition.</span></span> <span data-ttu-id="ce86f-192">Ad esempio, hello `Category` toohello esegue il mapping di proprietà stringa `category` campo, è di tipo `DataType.String`.</span><span class="sxs-lookup"><span data-stu-id="ce86f-192">For example, hello `Category` string property maps toohello `category` field, which is of type `DataType.String`.</span></span> <span data-ttu-id="ce86f-193">Esistono mapping di tipi simili tra `bool?` e `DataType.Boolean`, `DateTimeOffset?` e `DataType.DateTimeOffset` e così via.</span><span class="sxs-lookup"><span data-stu-id="ce86f-193">There are similar type mappings between `bool?` and `DataType.Boolean`, `DateTimeOffset?` and `DataType.DateTimeOffset`, and so forth.</span></span> <span data-ttu-id="ce86f-194">regole specifiche di Hello per il mapping di tipo hello sono documentate con hello `Documents.Get` metodo hello [riferimento Azure Search .NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span><span class="sxs-lookup"><span data-stu-id="ce86f-194">hello specific rules for hello type mapping are documented with hello `Documents.Get` method in hello [Azure Search .NET SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span></span>

<span data-ttu-id="ce86f-195">Questa possibilità toouse le proprie classi come documenti funziona in entrambe le direzioni; È anche possibile recuperare i risultati della ricerca e avere hello SDK automaticamente deserializzare li tooa tipo di propria scelta, come illustrato nell'hello [articolo successivo](search-query-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="ce86f-195">This ability toouse your own classes as documents works in both directions; You can also retrieve search results and have hello SDK automatically deserialize them tooa type of your choice, as shown in hello [next article](search-query-dotnet.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ce86f-196">Hello Azure Search .NET SDK supporta anche i documenti tipizzata in modo dinamico utilizzando hello `Document` (classe), ovvero un mapping di chiave/valore nomi toofield dei valori dei campi.</span><span class="sxs-lookup"><span data-stu-id="ce86f-196">hello Azure Search .NET SDK also supports dynamically-typed documents using hello `Document` class, which is a key/value mapping of field names toofield values.</span></span> <span data-ttu-id="ce86f-197">Ciò è utile negli scenari in cui non si conosce dello schema di indice hello in fase di progettazione o in cui sarebbe scomodo toobind toospecific classi del modello.</span><span class="sxs-lookup"><span data-stu-id="ce86f-197">This is useful in scenarios where you don't know hello index schema at design-time, or where it would be inconvenient toobind toospecific model classes.</span></span> <span data-ttu-id="ce86f-198">Tutti i metodi di hello hello SDK che gestiscono documenti presentano overload che funzionano con hello `Document` classe, come gli overload fortemente tipizzato che accettano un parametro di tipo generico.</span><span class="sxs-lookup"><span data-stu-id="ce86f-198">All hello methods in hello SDK that deal with documents have overloads that work with hello `Document` class, as well as strongly-typed overloads that take a generic type parameter.</span></span> <span data-ttu-id="ce86f-199">Hello solo quest'ultimo vengono utilizzati nel codice di esempio hello in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="ce86f-199">Only hello latter are used in hello sample code in this article.</span></span>
> 
> 

<span data-ttu-id="ce86f-200">**Perché usare tipi di dati nullable**</span><span class="sxs-lookup"><span data-stu-id="ce86f-200">**Why you should use nullable data types**</span></span>

<span data-ttu-id="ce86f-201">Quando si progetta la propria indice di ricerca di Azure tooan toomap classi di modello, si consiglia di dichiarazione delle proprietà dei tipi di valore, ad esempio `bool` e `int` toobe ammette valori null (ad esempio, `bool?` anziché `bool`).</span><span class="sxs-lookup"><span data-stu-id="ce86f-201">When designing your own model classes toomap tooan Azure Search index, we recommend declaring properties of value types such as `bool` and `int` toobe nullable (for example, `bool?` instead of `bool`).</span></span> <span data-ttu-id="ce86f-202">Se si utilizza una proprietà che non ammette valori null, è necessario troppo**garantire** che nessun documenti nell'indice contengono un valore null per il campo corrispondente hello.</span><span class="sxs-lookup"><span data-stu-id="ce86f-202">If you use a non-nullable property, you have too**guarantee** that no documents in your index contain a null value for hello corresponding field.</span></span> <span data-ttu-id="ce86f-203">Hello SDK né hello del servizio di ricerca di Azure consentirà si tooenforce questo.</span><span class="sxs-lookup"><span data-stu-id="ce86f-203">Neither hello SDK nor hello Azure Search service will help you tooenforce this.</span></span>

<span data-ttu-id="ce86f-204">Non è un problema di ipotetica: si consideri uno scenario in cui aggiungere un nuovo campo tooan esistente indice di tipo `DataType.Int32`.</span><span class="sxs-lookup"><span data-stu-id="ce86f-204">This is not just a hypothetical concern: Imagine a scenario where you add a new field tooan existing index that is of type `DataType.Int32`.</span></span> <span data-ttu-id="ce86f-205">Dopo aver aggiornato la definizione dell'indice hello, tutti i documenti avrà un valore null per il nuovo campo (poiché tutti i tipi nullable in ricerca di Azure).</span><span class="sxs-lookup"><span data-stu-id="ce86f-205">After updating hello index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="ce86f-206">Se si utilizza una classe di modello con un non-nullable `int` proprietà per il campo, si otterrà un `JsonSerializationException` simile durante il tentativo di tooretrieve documenti:</span><span class="sxs-lookup"><span data-stu-id="ce86f-206">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying tooretrieve documents:</span></span>

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="ce86f-207">Per questo motivo, è consigliabile usare tipi nullable nelle classi di modelli.</span><span class="sxs-lookup"><span data-stu-id="ce86f-207">For this reason, we recommend that you use nullable types in your model classes as a best practice.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce86f-208">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ce86f-208">Next steps</span></span>
<span data-ttu-id="ce86f-209">Dopo avere popolato l'indice di ricerca di Azure, sarà pronto toostart emittente toosearch query per i documenti.</span><span class="sxs-lookup"><span data-stu-id="ce86f-209">After populating your Azure Search index, you will be ready toostart issuing queries toosearch for documents.</span></span> <span data-ttu-id="ce86f-210">Per informazioni dettagliate, vedere [Eseguire query su un indice di Ricerca di Azure](search-query-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="ce86f-210">See [Query Your Azure Search Index](search-query-overview.md) for details.</span></span>

