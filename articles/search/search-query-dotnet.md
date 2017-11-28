---
title: aaa "Query di un indice (API .NET - ricerca di Azure) | Documenti di Microsoft"
description: Compilare una query di ricerca in ricerca di Azure e usare i parametri toofilter e ordinamento ricerca risultati della ricerca.
services: search
manager: jhubbard
documentationcenter: 
author: brjohnstmsft
ms.assetid: 12c3efba-ea99-4187-9d2d-f63b5ec7040d
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/19/2017
ms.author: brjohnst
ms.openlocfilehash: 8b3ba1cd1270aad038fb48d9053fcff35d243e13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="query-your-azure-search-index-using-hello-net-sdk"></a><span data-ttu-id="33531-103">L'indice di ricerca di Azure utilizzando hello SDK .NET di query</span><span class="sxs-lookup"><span data-stu-id="33531-103">Query your Azure Search index using hello .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="33531-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="33531-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="33531-105">Portale</span><span class="sxs-lookup"><span data-stu-id="33531-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="33531-106">.NET</span><span class="sxs-lookup"><span data-stu-id="33531-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="33531-107">REST</span><span class="sxs-lookup"><span data-stu-id="33531-107">REST</span></span>](search-query-rest-api.md)
> 
> 

<span data-ttu-id="33531-108">In questo articolo verrà illustrato come un indice utilizzando tooquery hello [Azure Search .NET SDK](https://aka.ms/search-sdk).</span><span class="sxs-lookup"><span data-stu-id="33531-108">This article will show you how tooquery an index using hello [Azure Search .NET SDK](https://aka.ms/search-sdk).</span></span>

<span data-ttu-id="33531-109">Prima di iniziare questa procedura dettagliata, è necessario avere [creato un indice di Ricerca di Azure](search-what-is-an-index.md) e [averlo popolato con dati](search-what-is-data-import.md).</span><span class="sxs-lookup"><span data-stu-id="33531-109">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md) and [populated it with data](search-what-is-data-import.md).</span></span>

> [!NOTE]
> <span data-ttu-id="33531-110">Tutto il codice di esempio in questo articolo è scritto in C#.</span><span class="sxs-lookup"><span data-stu-id="33531-110">All sample code in this article is written in C#.</span></span> <span data-ttu-id="33531-111">È possibile trovare il codice sorgente completo hello [su GitHub](http://aka.ms/search-dotnet-howto).</span><span class="sxs-lookup"><span data-stu-id="33531-111">You can find hello full source code [on GitHub](http://aka.ms/search-dotnet-howto).</span></span> <span data-ttu-id="33531-112">È inoltre possibile leggere sulla hello [Azure Search .NET SDK](search-howto-dotnet-sdk.md) per una più dettagliata procedura hello del codice di esempio.</span><span class="sxs-lookup"><span data-stu-id="33531-112">You can also read about hello [Azure Search .NET SDK](search-howto-dotnet-sdk.md) for a more detailed walk through of hello sample code.</span></span>

## <a name="identify-your-azure-search-services-query-api-key"></a><span data-ttu-id="33531-113">Identificare la chiave API di query del servizio Ricerca di Azure</span><span class="sxs-lookup"><span data-stu-id="33531-113">Identify your Azure Search service's query api-key</span></span>
<span data-ttu-id="33531-114">Ora che è stato creato un indice di ricerca di Azure, si è quasi pronto tooissue query utilizzando hello .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="33531-114">Now that you have created an Azure Search index, you are almost ready tooissue queries using hello .NET SDK.</span></span> <span data-ttu-id="33531-115">In primo luogo, è necessario tooobtain uno dei hello chiavi api di query che è stato generato per il servizio di ricerca hello che è effettuato il provisioning.</span><span class="sxs-lookup"><span data-stu-id="33531-115">First, you will need tooobtain one of hello query api-keys that was generated for hello search service you provisioned.</span></span> <span data-ttu-id="33531-116">Hello .NET SDK invierà questa chiave api nel servizio di tooyour ogni richiesta.</span><span class="sxs-lookup"><span data-stu-id="33531-116">hello .NET SDK will send this api-key on every request tooyour service.</span></span> <span data-ttu-id="33531-117">Disporre di una chiave valida stabilisce relazioni di trust, un singolo per ogni richiesta, tra hello invio hello richiesta e il servizio di hello che la gestisce.</span><span class="sxs-lookup"><span data-stu-id="33531-117">Having a valid key establishes trust, on a per request basis, between hello application sending hello request and hello service that handles it.</span></span>

1. <span data-ttu-id="33531-118">toofind chiavi di api del servizio è possibile accedere toohello [portale di Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="33531-118">toofind your service's api-keys you can sign in toohello [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="33531-119">Pannello del servizio di ricerca di Azure andare tooyour</span><span class="sxs-lookup"><span data-stu-id="33531-119">Go tooyour Azure Search service's blade</span></span>
3. <span data-ttu-id="33531-120">Fare clic su hello icona "Chiavi"</span><span class="sxs-lookup"><span data-stu-id="33531-120">Click on hello "Keys" icon</span></span>

<span data-ttu-id="33531-121">Il servizio avrà *chiavi amministratore* e *chiavi di query*.</span><span class="sxs-lookup"><span data-stu-id="33531-121">Your service will have *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="33531-122">Il database primario e secondario *chiavi amministratore* concedere diritti completi tooall operazioni, incluso hello possibilità toomanage hello servizio, creare ed eliminare origini di dati, gli indicizzatori e gli indici.</span><span class="sxs-lookup"><span data-stu-id="33531-122">Your primary and secondary *admin keys* grant full rights tooall operations, including hello ability toomanage hello service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="33531-123">Esistono due chiavi in modo che sia possibile continuare chiave secondaria di hello toouse se si decide di tooregenerate hello primary key e viceversa.</span><span class="sxs-lookup"><span data-stu-id="33531-123">There are two keys so that you can continue toouse hello secondary key if you decide tooregenerate hello primary key, and vice-versa.</span></span>
* <span data-ttu-id="33531-124">Il *query chiavi* concedere l'accesso in sola lettura tooindexes e documenti e sono in genere distribuite tooclient applicazioni che inviano richieste di ricerca.</span><span class="sxs-lookup"><span data-stu-id="33531-124">Your *query keys* grant read-only access tooindexes and documents, and are typically distributed tooclient applications that issue search requests.</span></span>

<span data-ttu-id="33531-125">Ai fini di hello di query nell'indice, è possibile utilizzare una delle chiavi di query.</span><span class="sxs-lookup"><span data-stu-id="33531-125">For hello purposes of querying an index, you can use one of your query keys.</span></span> <span data-ttu-id="33531-126">Le chiavi amministratore utilizzabile anche per le query, ma è necessario usare una chiave di query nel codice dell'applicazione, come segue meglio hello [principio di privilegio minimo](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span><span class="sxs-lookup"><span data-stu-id="33531-126">Your admin keys can also be used for queries, but you should use a query key in your application code as this better follows hello [Principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span></span>

## <a name="create-an-instance-of-hello-searchindexclient-class"></a><span data-ttu-id="33531-127">Creare un'istanza della classe SearchIndexClient hello</span><span class="sxs-lookup"><span data-stu-id="33531-127">Create an instance of hello SearchIndexClient class</span></span>
<span data-ttu-id="33531-128">query tooissue con hello Azure Search .NET SDK, sarà necessario toocreate un'istanza di hello `SearchIndexClient` classe.</span><span class="sxs-lookup"><span data-stu-id="33531-128">tooissue queries with hello Azure Search .NET SDK, you will need toocreate an instance of hello `SearchIndexClient` class.</span></span> <span data-ttu-id="33531-129">Questa classe ha diversi costruttori.</span><span class="sxs-lookup"><span data-stu-id="33531-129">This class has several constructors.</span></span> <span data-ttu-id="33531-130">Hello quello desiderato accetta il nome del servizio di ricerca, il nome dell'indice e un `SearchCredentials` oggetto come parametri.</span><span class="sxs-lookup"><span data-stu-id="33531-130">hello one you want takes your search service name, index name, and a `SearchCredentials` object as parameters.</span></span> <span data-ttu-id="33531-131">`SearchCredentials` esegue il wrapping della chiave API.</span><span class="sxs-lookup"><span data-stu-id="33531-131">`SearchCredentials` wraps your api-key.</span></span>

<span data-ttu-id="33531-132">Crea un nuovo codice Hello riportato di seguito `SearchIndexClient` per l'indice "Hotel" hello (creato in [creare un indice di ricerca di Azure mediante .NET SDK hello](search-create-index-dotnet.md)) utilizzando i valori per nome del servizio ricerca hello e la chiave api che vengono archiviati nel file di configurazione dell'applicazione hello file (`appsettings.json` nel caso di hello di hello [applicazione di esempio](http://aka.ms/search-dotnet-howto)):</span><span class="sxs-lookup"><span data-stu-id="33531-132">hello code below creates a new `SearchIndexClient` for hello "hotels" index (created in [Create an Azure Search index using hello .NET SDK](search-create-index-dotnet.md)) using values for hello search service name and api-key that are stored in hello application's config file (`appsettings.json` in hello case of hello [sample application](http://aka.ms/search-dotnet-howto)):</span></span>

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

<span data-ttu-id="33531-133">`SearchIndexClient` include una proprietà `Documents`.</span><span class="sxs-lookup"><span data-stu-id="33531-133">`SearchIndexClient` has a `Documents` property.</span></span> <span data-ttu-id="33531-134">Questa proprietà fornisce che tutti hello metodi che è necessario tooquery gli indici di ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="33531-134">This property provides all hello methods you need tooquery Azure Search indexes.</span></span>

## <a name="query-your-index"></a><span data-ttu-id="33531-135">Eseguire query sull'indice</span><span class="sxs-lookup"><span data-stu-id="33531-135">Query your index</span></span>
<span data-ttu-id="33531-136">Ricerca con .NET SDK hello è semplice come chiamata hello `Documents.Search` metodo i `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="33531-136">Searching with hello .NET SDK is as simple as calling hello `Documents.Search` method on your `SearchIndexClient`.</span></span> <span data-ttu-id="33531-137">Questo metodo accetta alcuni parametri, incluso il testo di ricerca hello, insieme a un `SearchParameters` oggetto che può essere utilizzato toofurther rifinire hello query.</span><span class="sxs-lookup"><span data-stu-id="33531-137">This method takes a few parameters, including hello search text, along with a `SearchParameters` object that can be used toofurther refine hello query.</span></span>

#### <a name="types-of-queries"></a><span data-ttu-id="33531-138">Tipi di query</span><span class="sxs-lookup"><span data-stu-id="33531-138">Types of Queries</span></span>
<span data-ttu-id="33531-139">main Hello due [tipi di query](search-query-overview.md#types-of-queries) si utilizzerà sono `search` e `filter`.</span><span class="sxs-lookup"><span data-stu-id="33531-139">hello two main [query types](search-query-overview.md#types-of-queries) you will use are `search` and `filter`.</span></span> <span data-ttu-id="33531-140">Una query `search` esegue la ricerca di uno o più termini in tutti i campi *ricercabile* nell'indice.</span><span class="sxs-lookup"><span data-stu-id="33531-140">A `search` query searches for one or more terms in all *searchable* fields in your index.</span></span> <span data-ttu-id="33531-141">Una query `filter` valuta un'espressione booleana su tutti i campi *filtrabili* di un indice.</span><span class="sxs-lookup"><span data-stu-id="33531-141">A `filter` query evaluates a boolean expression over all *filterable* fields in an index.</span></span>

<span data-ttu-id="33531-142">Le ricerche e i filtri vengono eseguiti hello `Documents.Search` metodo.</span><span class="sxs-lookup"><span data-stu-id="33531-142">Both searches and filters are performed using hello `Documents.Search` method.</span></span> <span data-ttu-id="33531-143">Una query di ricerca può essere passata in hello `searchText` parametro, mentre un'espressione di filtro può essere passata in hello `Filter` proprietà di hello `SearchParameters` classe.</span><span class="sxs-lookup"><span data-stu-id="33531-143">A search query can be passed in hello `searchText` parameter, while a filter expression can be passed in hello `Filter` property of hello `SearchParameters` class.</span></span> <span data-ttu-id="33531-144">toofilter senza eseguire ricerche, è sufficiente passare `"*"` per hello `searchText` parametro.</span><span class="sxs-lookup"><span data-stu-id="33531-144">toofilter without searching, just pass `"*"` for hello `searchText` parameter.</span></span> <span data-ttu-id="33531-145">toosearch senza filtri, lasciare hello `Filter` proprietà non è impostato, oppure non passare un `SearchParameters` istanza affatto.</span><span class="sxs-lookup"><span data-stu-id="33531-145">toosearch without filtering, just leave hello `Filter` property unset, or do not pass in a `SearchParameters` instance at all.</span></span>

#### <a name="example-queries"></a><span data-ttu-id="33531-146">Query di esempio</span><span class="sxs-lookup"><span data-stu-id="33531-146">Example Queries</span></span>
<span data-ttu-id="33531-147">Hello codice di esempio seguente mostra alcuni modi tooquery hello "Hotel" indice definito in [creare un indice di ricerca di Azure mediante .NET SDK hello](search-create-index-dotnet.md#DefineIndex).</span><span class="sxs-lookup"><span data-stu-id="33531-147">hello following sample code shows a few different ways tooquery hello "hotels" index defined in [Create an Azure Search index using hello .NET SDK](search-create-index-dotnet.md#DefineIndex).</span></span> <span data-ttu-id="33531-148">Si noti che i documenti hello restituiti con i risultati della ricerca hello sono istanze di hello `Hotel` (classe), che è stato definito in [hello di importazione dei dati in ricerca di Azure mediante .NET SDK](search-import-data-dotnet.md#HotelClass).</span><span class="sxs-lookup"><span data-stu-id="33531-148">Note that hello documents returned with hello search results are instances of hello `Hotel` class, which was defined in [Data Import in Azure Search using hello .NET SDK](search-import-data-dotnet.md#HotelClass).</span></span> <span data-ttu-id="33531-149">esempio di codice Hello si avvalgono di un `WriteDocuments` console toohello di metodo toooutput hello ricerca risultati.</span><span class="sxs-lookup"><span data-stu-id="33531-149">hello sample code makes use of a `WriteDocuments` method toooutput hello search results toohello console.</span></span> <span data-ttu-id="33531-150">Questo metodo è descritto nella sezione successiva hello.</span><span class="sxs-lookup"><span data-stu-id="33531-150">This method is described in hello next section.</span></span>

```csharp
SearchParameters parameters;
DocumentSearchResult<Hotel> results;

Console.WriteLine("Search hello entire index for hello term 'budget' and return only hello hotelName field:\n");

parameters =
    new SearchParameters()
    {
        Select = new[] { "hotelName" }
    };

results = indexClient.Documents.Search<Hotel>("budget", parameters);

WriteDocuments(results);

Console.Write("Apply a filter toohello index toofind hotels cheaper than $150 per night, ");
Console.WriteLine("and return hello hotelId and description:\n");

parameters =
    new SearchParameters()
    {
        Filter = "baseRate lt 150",
        Select = new[] { "hotelId", "description" }
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);

Console.Write("Search hello entire index, order by a specific field (lastRenovationDate) ");
Console.Write("in descending order, take hello top two results, and show only hotelName and ");
Console.WriteLine("lastRenovationDate:\n");

parameters =
    new SearchParameters()
    {
        OrderBy = new[] { "lastRenovationDate desc" },
        Select = new[] { "hotelName", "lastRenovationDate" },
        Top = 2
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);

Console.WriteLine("Search hello entire index for hello term 'motel':\n");

parameters = new SearchParameters();
results = indexClient.Documents.Search<Hotel>("motel", parameters);

WriteDocuments(results);
```

## <a name="handle-search-results"></a><span data-ttu-id="33531-151">Gestire i risultati della ricerca</span><span class="sxs-lookup"><span data-stu-id="33531-151">Handle search results</span></span>
<span data-ttu-id="33531-152">Hello `Documents.Search` metodo restituisce un `DocumentSearchResult` oggetto che contiene i risultati della query hello hello.</span><span class="sxs-lookup"><span data-stu-id="33531-152">hello `Documents.Search` method returns a `DocumentSearchResult` object that contains hello results of hello query.</span></span> <span data-ttu-id="33531-153">esempio Hello nella sezione precedente hello utilizzato un metodo denominato `WriteDocuments` console toohello di toooutput hello ricerca risultati:</span><span class="sxs-lookup"><span data-stu-id="33531-153">hello example in hello previous section used a method called `WriteDocuments` toooutput hello search results toohello console:</span></span>

```csharp
private static void WriteDocuments(DocumentSearchResult<Hotel> searchResults)
{
    foreach (SearchResult<Hotel> result in searchResults.Results)
    {
        Console.WriteLine(result.Document);
    }

    Console.WriteLine();
}
```

<span data-ttu-id="33531-154">Risultati hello un aspetto simile per le query hello nella sezione precedente di hello, presumendo un indice di hotel"hello" viene popolato con i dati di esempio hello in [hello di importazione dei dati in ricerca di Azure mediante .NET SDK](search-import-data-dotnet.md):</span><span class="sxs-lookup"><span data-stu-id="33531-154">Here is what hello results look like for hello queries in hello previous section, assuming hello "hotels" index is populated with hello sample data in [Data Import in Azure Search using hello .NET SDK](search-import-data-dotnet.md):</span></span>

```
Search hello entire index for hello term 'budget' and return only hello hotelName field:

Name: Roach Motel

Apply a filter toohello index toofind hotels cheaper than $150 per night, and return hello hotelId and description:

ID: 2   Description: Cheapest hotel in town
ID: 3   Description: Close tootown hall and hello river

Search hello entire index, order by a specific field (lastRenovationDate) in descending order, take hello top two results, and show only hotelName and lastRenovationDate:

Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

Search hello entire index for hello term 'motel':

ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577
```

<span data-ttu-id="33531-155">Hello esempio di codice precedente utilizza i risultati della ricerca toooutput console hello.</span><span class="sxs-lookup"><span data-stu-id="33531-155">hello sample code above uses hello console toooutput search results.</span></span> <span data-ttu-id="33531-156">Allo stesso modo, sarà necessario toodisplay i risultati della ricerca nella propria applicazione.</span><span class="sxs-lookup"><span data-stu-id="33531-156">You will likewise need toodisplay search results in your own application.</span></span> <span data-ttu-id="33531-157">Vedere [in questo esempio in GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample) per un esempio di come risultati della ricerca toorender in un'applicazione web basata su ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="33531-157">See [this sample on GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample) for an example of how toorender search results in an ASP.NET MVC-based web application.</span></span>

