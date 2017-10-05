---
title: 'Eseguire query su un indice: API .NET e Ricerca di Azure | Microsoft Docs'
description: Compilare una query di ricerca in Ricerca di Azure e usare i parametri di ricerca per filtrare e ordinare i risultati della ricerca.
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
ms.openlocfilehash: 52bd0fd4cf70401dcf881c7f28d5cd91397bb059
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="query-your-azure-search-index-using-the-net-sdk"></a><span data-ttu-id="332ee-103">Eseguire query su un indice di Ricerca di Azure con .NET SDK</span><span class="sxs-lookup"><span data-stu-id="332ee-103">Query your Azure Search index using the .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="332ee-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="332ee-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="332ee-105">Portale</span><span class="sxs-lookup"><span data-stu-id="332ee-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="332ee-106">.NET</span><span class="sxs-lookup"><span data-stu-id="332ee-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="332ee-107">REST</span><span class="sxs-lookup"><span data-stu-id="332ee-107">REST</span></span>](search-query-rest-api.md)
> 
> 

<span data-ttu-id="332ee-108">Questo articolo illustra come eseguire query su un indice con [Azure Search .NET SDK](https://aka.ms/search-sdk).</span><span class="sxs-lookup"><span data-stu-id="332ee-108">This article will show you how to query an index using the [Azure Search .NET SDK](https://aka.ms/search-sdk).</span></span>

<span data-ttu-id="332ee-109">Prima di iniziare questa procedura dettagliata, è necessario avere [creato un indice di Ricerca di Azure](search-what-is-an-index.md) e [averlo popolato con dati](search-what-is-data-import.md).</span><span class="sxs-lookup"><span data-stu-id="332ee-109">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md) and [populated it with data](search-what-is-data-import.md).</span></span>

> [!NOTE]
> <span data-ttu-id="332ee-110">Tutto il codice di esempio in questo articolo è scritto in C#.</span><span class="sxs-lookup"><span data-stu-id="332ee-110">All sample code in this article is written in C#.</span></span> <span data-ttu-id="332ee-111">Il codice sorgente completo è disponibile su [GitHub](http://aka.ms/search-dotnet-howto).</span><span class="sxs-lookup"><span data-stu-id="332ee-111">You can find the full source code [on GitHub](http://aka.ms/search-dotnet-howto).</span></span> <span data-ttu-id="332ee-112">Per una descrizione più dettagliata del codice di esempio, vedere le informazioni relative a [Azure Search .NET SDK](search-howto-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="332ee-112">You can also read about the [Azure Search .NET SDK](search-howto-dotnet-sdk.md) for a more detailed walk through of the sample code.</span></span>

## <a name="identify-your-azure-search-services-query-api-key"></a><span data-ttu-id="332ee-113">Identificare la chiave API di query del servizio Ricerca di Azure</span><span class="sxs-lookup"><span data-stu-id="332ee-113">Identify your Azure Search service's query api-key</span></span>
<span data-ttu-id="332ee-114">Dopo avere creato un indice di Ricerca di Azure, si è quasi pronti per eseguire query con .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="332ee-114">Now that you have created an Azure Search index, you are almost ready to issue queries using the .NET SDK.</span></span> <span data-ttu-id="332ee-115">Prima di tutto è necessario ottenere una delle chiavi API di query generate per il servizio di ricerca di cui è stato effettuato il provisioning.</span><span class="sxs-lookup"><span data-stu-id="332ee-115">First, you will need to obtain one of the query api-keys that was generated for the search service you provisioned.</span></span> <span data-ttu-id="332ee-116">.NET SDK invierà questa chiave API a ogni richiesta al servizio.</span><span class="sxs-lookup"><span data-stu-id="332ee-116">The .NET SDK will send this api-key on every request to your service.</span></span> <span data-ttu-id="332ee-117">La presenza di una chiave valida stabilisce una relazione di trust, in base alle singole richieste, tra l'applicazione che invia la richiesta e il servizio che la gestisce.</span><span class="sxs-lookup"><span data-stu-id="332ee-117">Having a valid key establishes trust, on a per request basis, between the application sending the request and the service that handles it.</span></span>

1. <span data-ttu-id="332ee-118">Per trovare le chiavi API del servizio, è possibile accedere al [portale di Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="332ee-118">To find your service's api-keys you can sign in to the [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="332ee-119">Passare al pannello del servizio Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="332ee-119">Go to your Azure Search service's blade</span></span>
3. <span data-ttu-id="332ee-120">Fare clic sull'icona "Chiavi".</span><span class="sxs-lookup"><span data-stu-id="332ee-120">Click on the "Keys" icon</span></span>

<span data-ttu-id="332ee-121">Il servizio avrà *chiavi amministratore* e *chiavi di query*.</span><span class="sxs-lookup"><span data-stu-id="332ee-121">Your service will have *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="332ee-122">Le *chiavi amministratore* primarie e secondarie concedono diritti completi a tutte le operazioni, inclusa la possibilità di gestire il servizio, creare ed eliminare indici, indicizzatori e origini dati.</span><span class="sxs-lookup"><span data-stu-id="332ee-122">Your primary and secondary *admin keys* grant full rights to all operations, including the ability to manage the service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="332ee-123">Sono disponibili due chiavi, quindi è possibile continuare a usare la chiave secondaria se si decide di rigenerare la chiave primaria e viceversa.</span><span class="sxs-lookup"><span data-stu-id="332ee-123">There are two keys so that you can continue to use the secondary key if you decide to regenerate the primary key, and vice-versa.</span></span>
* <span data-ttu-id="332ee-124">Le *chiavi di query* concedono l'accesso in sola lettura agli indici e ai documenti e vengono in genere distribuite alle applicazioni client che inviano richieste di ricerca.</span><span class="sxs-lookup"><span data-stu-id="332ee-124">Your *query keys* grant read-only access to indexes and documents, and are typically distributed to client applications that issue search requests.</span></span>

<span data-ttu-id="332ee-125">Ai fini di una query su un indice, è possibile usare una delle chiavi di query.</span><span class="sxs-lookup"><span data-stu-id="332ee-125">For the purposes of querying an index, you can use one of your query keys.</span></span> <span data-ttu-id="332ee-126">Si possono anche usare le chiavi amministratore per le query, ma è necessario usare una chiave di query nel codice dell'applicazione, perché questo approccio è più coerente con il [principio del privilegio minimo](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span><span class="sxs-lookup"><span data-stu-id="332ee-126">Your admin keys can also be used for queries, but you should use a query key in your application code as this better follows the [Principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span></span>

## <a name="create-an-instance-of-the-searchindexclient-class"></a><span data-ttu-id="332ee-127">Creare un'istanza della classe SearchIndexClient</span><span class="sxs-lookup"><span data-stu-id="332ee-127">Create an instance of the SearchIndexClient class</span></span>
<span data-ttu-id="332ee-128">Per eseguire query con Azure Search .NET SDK, è necessario creare un'istanza della classe `SearchIndexClient` .</span><span class="sxs-lookup"><span data-stu-id="332ee-128">To issue queries with the Azure Search .NET SDK, you will need to create an instance of the `SearchIndexClient` class.</span></span> <span data-ttu-id="332ee-129">Questa classe ha diversi costruttori.</span><span class="sxs-lookup"><span data-stu-id="332ee-129">This class has several constructors.</span></span> <span data-ttu-id="332ee-130">Quello appropriato accetta il nome del servizio di ricerca, il nome dell'indice e un oggetto `SearchCredentials` come parametri.</span><span class="sxs-lookup"><span data-stu-id="332ee-130">The one you want takes your search service name, index name, and a `SearchCredentials` object as parameters.</span></span> <span data-ttu-id="332ee-131">`SearchCredentials` esegue il wrapping della chiave API.</span><span class="sxs-lookup"><span data-stu-id="332ee-131">`SearchCredentials` wraps your api-key.</span></span>

<span data-ttu-id="332ee-132">Il codice seguente crea un nuovo oggetto `SearchIndexClient` per l'indice "hotels" creato in [Creare un indice di Ricerca di Azure con .NET SDK](search-create-index-dotnet.md), usando i valori archiviati nel file di configurazione dell'applicazione, `appsettings.json` nel caso dell'[applicazione di esempio](http://aka.ms/search-dotnet-howto), per il nome del servizio di ricerca e la chiave API:</span><span class="sxs-lookup"><span data-stu-id="332ee-132">The code below creates a new `SearchIndexClient` for the "hotels" index (created in [Create an Azure Search index using the .NET SDK](search-create-index-dotnet.md)) using values for the search service name and api-key that are stored in the application's config file (`appsettings.json` in the case of the [sample application](http://aka.ms/search-dotnet-howto)):</span></span>

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

<span data-ttu-id="332ee-133">`SearchIndexClient` include una proprietà `Documents`.</span><span class="sxs-lookup"><span data-stu-id="332ee-133">`SearchIndexClient` has a `Documents` property.</span></span> <span data-ttu-id="332ee-134">Questa proprietà fornisce tutti i metodi necessari per eseguire query sugli indici di Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="332ee-134">This property provides all the methods you need to query Azure Search indexes.</span></span>

## <a name="query-your-index"></a><span data-ttu-id="332ee-135">Eseguire query sull'indice</span><span class="sxs-lookup"><span data-stu-id="332ee-135">Query your index</span></span>
<span data-ttu-id="332ee-136">Per eseguire una ricerca con .NET SDK è sufficiente chiamare il metodo `Documents.Search` sull'oggetto `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="332ee-136">Searching with the .NET SDK is as simple as calling the `Documents.Search` method on your `SearchIndexClient`.</span></span> <span data-ttu-id="332ee-137">Questo metodo accetta alcuni parametri, incluso il testo di ricerca, nonché un oggetto `SearchParameters` che può essere usato per perfezionare ulteriormente la query.</span><span class="sxs-lookup"><span data-stu-id="332ee-137">This method takes a few parameters, including the search text, along with a `SearchParameters` object that can be used to further refine the query.</span></span>

#### <a name="types-of-queries"></a><span data-ttu-id="332ee-138">Tipi di query</span><span class="sxs-lookup"><span data-stu-id="332ee-138">Types of Queries</span></span>
<span data-ttu-id="332ee-139">I due [tipi di query](search-query-overview.md#types-of-queries) principali che si useranno sono `search` e `filter`.</span><span class="sxs-lookup"><span data-stu-id="332ee-139">The two main [query types](search-query-overview.md#types-of-queries) you will use are `search` and `filter`.</span></span> <span data-ttu-id="332ee-140">Una query `search` esegue la ricerca di uno o più termini in tutti i campi *ricercabile* nell'indice.</span><span class="sxs-lookup"><span data-stu-id="332ee-140">A `search` query searches for one or more terms in all *searchable* fields in your index.</span></span> <span data-ttu-id="332ee-141">Una query `filter` valuta un'espressione booleana su tutti i campi *filtrabili* di un indice.</span><span class="sxs-lookup"><span data-stu-id="332ee-141">A `filter` query evaluates a boolean expression over all *filterable* fields in an index.</span></span>

<span data-ttu-id="332ee-142">Ricerche e filtri vengono eseguiti usando il metodo `Documents.Search` .</span><span class="sxs-lookup"><span data-stu-id="332ee-142">Both searches and filters are performed using the `Documents.Search` method.</span></span> <span data-ttu-id="332ee-143">Una query di ricerca può essere passata nel parametro `searchText`, mentre un'espressione di filtro può essere passata nella proprietà `Filter` della classe `SearchParameters`.</span><span class="sxs-lookup"><span data-stu-id="332ee-143">A search query can be passed in the `searchText` parameter, while a filter expression can be passed in the `Filter` property of the `SearchParameters` class.</span></span> <span data-ttu-id="332ee-144">Per filtrare senza eseguire ricerche, passare semplicemente `"*"` per il parametro `searchText`.</span><span class="sxs-lookup"><span data-stu-id="332ee-144">To filter without searching, just pass `"*"` for the `searchText` parameter.</span></span> <span data-ttu-id="332ee-145">Per eseguire una ricerca senza filtrare, lasciare la proprietà `Filter` non impostata oppure non passare un'istanza di `SearchParameters`.</span><span class="sxs-lookup"><span data-stu-id="332ee-145">To search without filtering, just leave the `Filter` property unset, or do not pass in a `SearchParameters` instance at all.</span></span>

#### <a name="example-queries"></a><span data-ttu-id="332ee-146">Query di esempio</span><span class="sxs-lookup"><span data-stu-id="332ee-146">Example Queries</span></span>
<span data-ttu-id="332ee-147">Il codice di esempio seguente mostra alcuni modi per eseguire una query sull'indice "hotels" definito in [Creare un indice di Ricerca di Azure con .NET SDK](search-create-index-dotnet.md#DefineIndex).</span><span class="sxs-lookup"><span data-stu-id="332ee-147">The following sample code shows a few different ways to query the "hotels" index defined in [Create an Azure Search index using the .NET SDK](search-create-index-dotnet.md#DefineIndex).</span></span> <span data-ttu-id="332ee-148">Si noti che i documenti restituiti con i risultati della ricerca sono istanze della classe `Hotel` , che è stata definita in [Importazione di dati in Ricerca di Azure tramite .NET SDK](search-import-data-dotnet.md#HotelClass).</span><span class="sxs-lookup"><span data-stu-id="332ee-148">Note that the documents returned with the search results are instances of the `Hotel` class, which was defined in [Data Import in Azure Search using the .NET SDK](search-import-data-dotnet.md#HotelClass).</span></span> <span data-ttu-id="332ee-149">Il codice di esempio usa un metodo `WriteDocuments` per restituire i risultati di ricerca nella console.</span><span class="sxs-lookup"><span data-stu-id="332ee-149">The sample code makes use of a `WriteDocuments` method to output the search results to the console.</span></span> <span data-ttu-id="332ee-150">Questo metodo è descritto nella sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="332ee-150">This method is described in the next section.</span></span>

```csharp
SearchParameters parameters;
DocumentSearchResult<Hotel> results;

Console.WriteLine("Search the entire index for the term 'budget' and return only the hotelName field:\n");

parameters =
    new SearchParameters()
    {
        Select = new[] { "hotelName" }
    };

results = indexClient.Documents.Search<Hotel>("budget", parameters);

WriteDocuments(results);

Console.Write("Apply a filter to the index to find hotels cheaper than $150 per night, ");
Console.WriteLine("and return the hotelId and description:\n");

parameters =
    new SearchParameters()
    {
        Filter = "baseRate lt 150",
        Select = new[] { "hotelId", "description" }
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);

Console.Write("Search the entire index, order by a specific field (lastRenovationDate) ");
Console.Write("in descending order, take the top two results, and show only hotelName and ");
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

Console.WriteLine("Search the entire index for the term 'motel':\n");

parameters = new SearchParameters();
results = indexClient.Documents.Search<Hotel>("motel", parameters);

WriteDocuments(results);
```

## <a name="handle-search-results"></a><span data-ttu-id="332ee-151">Gestire i risultati della ricerca</span><span class="sxs-lookup"><span data-stu-id="332ee-151">Handle search results</span></span>
<span data-ttu-id="332ee-152">Il metodo `Documents.Search` restituisce un oggetto `DocumentSearchResult` che contiene i risultati della query.</span><span class="sxs-lookup"><span data-stu-id="332ee-152">The `Documents.Search` method returns a `DocumentSearchResult` object that contains the results of the query.</span></span> <span data-ttu-id="332ee-153">Nell'esempio nella sezione precedente viene usato un metodo denominato `WriteDocuments` per restituire i risultati di ricerca nella console:</span><span class="sxs-lookup"><span data-stu-id="332ee-153">The example in the previous section used a method called `WriteDocuments` to output the search results to the console:</span></span>

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

<span data-ttu-id="332ee-154">Ecco i risultati per le query nella sezione precedente, supponendo che l'indice "hotels" sia popolato con i dati di esempio in [Importazione di dati in Ricerca di Azure tramite .NET SDK](search-import-data-dotnet.md):</span><span class="sxs-lookup"><span data-stu-id="332ee-154">Here is what the results look like for the queries in the previous section, assuming the "hotels" index is populated with the sample data in [Data Import in Azure Search using the .NET SDK](search-import-data-dotnet.md):</span></span>

```
Search the entire index for the term 'budget' and return only the hotelName field:

Name: Roach Motel

Apply a filter to the index to find hotels cheaper than $150 per night, and return the hotelId and description:

ID: 2   Description: Cheapest hotel in town
ID: 3   Description: Close to town hall and the river

Search the entire index, order by a specific field (lastRenovationDate) in descending order, take the top two results, and show only hotelName and lastRenovationDate:

Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

Search the entire index for the term 'motel':

ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577
```

<span data-ttu-id="332ee-155">Il codice di esempio precedente usa la console per restituire i risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="332ee-155">The sample code above uses the console to output search results.</span></span> <span data-ttu-id="332ee-156">Analogamente, sarà necessario visualizzare i risultati della ricerca nella propria applicazione.</span><span class="sxs-lookup"><span data-stu-id="332ee-156">You will likewise need to display search results in your own application.</span></span> <span data-ttu-id="332ee-157">Per un esempio di rendering dei risultati di ricerca in un'applicazione Web basata su ASP.NET MVC, vedere [questo esempio su GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample) .</span><span class="sxs-lookup"><span data-stu-id="332ee-157">See [this sample on GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample) for an example of how to render search results in an ASP.NET MVC-based web application.</span></span>

