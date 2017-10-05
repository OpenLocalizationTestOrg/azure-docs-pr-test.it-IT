---
title: Esercitazione sull'anteprima dei sinonimi in Ricerca di Azure | Microsoft Docs
description: "Aggiungere la funzionalità di anteprima dei sinonimi a un indice in Ricerca di Azure."
services: search
manager: jhubbard
documentationcenter: 
author: HeidiSteen
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 03/31/2017
ms.author: heidist
ms.openlocfilehash: 014959ed471f796d2184f0f8ff10d15cdc8a2ec6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="synonym-preview-c-tutorial-for-azure-search"></a><span data-ttu-id="a317b-103">Esercitazione sui sinonimi (anteprima) in C# per Ricerca di Azure</span><span class="sxs-lookup"><span data-stu-id="a317b-103">Synonym (preview) C# tutorial for Azure Search</span></span>

<span data-ttu-id="a317b-104">I sinonimi espandono una query tramite la corrispondenza con termini considerati semanticamente uguali al termine di input.</span><span class="sxs-lookup"><span data-stu-id="a317b-104">Synonyms expand a query by matching on terms considered semantically equivalent to the input term.</span></span> <span data-ttu-id="a317b-105">È ad esempio possibile che si voglia che il termine "auto" consenta di rilevare corrispondenze con documenti contenenti i termini "automobile" o "veicolo".</span><span class="sxs-lookup"><span data-stu-id="a317b-105">For example, you might want "car" to match documents containing the terms "automobile" or "vehicle".</span></span>

<span data-ttu-id="a317b-106">In Ricerca di Azure i sinonimi sono definiti in una *mappa di sinonimi* tramite *regole di mapping* che associano termini equivalenti.</span><span class="sxs-lookup"><span data-stu-id="a317b-106">In Azure Search, synonyms are defined in a *synonym map*, through *mapping rules* that associate equivalent terms.</span></span> <span data-ttu-id="a317b-107">È possibile creare più mappe di sinonimi, inserirle come risorse a livello di servizio disponibili per qualsiasi indice e quindi fare riferimento alla mappa da usare a livello di campo.</span><span class="sxs-lookup"><span data-stu-id="a317b-107">You can create multiple synonym maps, post them as a service-wide resource available to any index, and then reference which one to use at the field level.</span></span> <span data-ttu-id="a317b-108">In fase di query, oltre a eseguire ricerche in un indice, Ricerca di Azure esegue una ricerca in una mappa di sinonimi, se tale mappa viene specificata nei campi usati nella query.</span><span class="sxs-lookup"><span data-stu-id="a317b-108">At query time, in addition to searching an index, Azure Search does a lookup in a synonym map, if one is specified on fields used in the query.</span></span>

> [!NOTE]
> <span data-ttu-id="a317b-109">La funzionalità relativa ai sinonimi è attualmente disponibile in anteprima ed è supportata solo nelle versioni più recenti dell'anteprima di API e SDK (api-version=2016-09-01-Preview, SDK versione 4.x-anteprima).</span><span class="sxs-lookup"><span data-stu-id="a317b-109">The synonyms feature is currently in preview and only supported in the latest preview API and SDK versions (api-version=2016-09-01-Preview, SDK version 4.x-preview).</span></span> <span data-ttu-id="a317b-110">Non è attualmente disponibile alcun supporto nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a317b-110">There is no Azure portal support at this time.</span></span> <span data-ttu-id="a317b-111">Le API disponibili in anteprima non rientrano nel Contratto di servizio e le funzionalità disponibili in anteprima possono subire modifiche, quindi non è consigliabile usarle nelle applicazioni di produzione.</span><span class="sxs-lookup"><span data-stu-id="a317b-111">Preview APIs are not under SLA and preview features may change, so we do not recommend using them in production applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a317b-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a317b-112">Prerequisites</span></span>

<span data-ttu-id="a317b-113">I requisiti per l'esercitazione includono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="a317b-113">Tutorial requirements include the following:</span></span>

* [<span data-ttu-id="a317b-114">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a317b-114">Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="a317b-115">Servizio Ricerca di Azure</span><span class="sxs-lookup"><span data-stu-id="a317b-115">Azure Search service</span></span>](search-create-service-portal.md)
* [<span data-ttu-id="a317b-116">Versione di anteprima della libreria Microsoft.Azure.Search .NET</span><span class="sxs-lookup"><span data-stu-id="a317b-116">Preview version of Microsoft.Azure.Search .NET library</span></span>](https://aka.ms/search-sdk-preview)
* [<span data-ttu-id="a317b-117">Come utilizzare Ricerca di Azure da un'applicazione .NET</span><span class="sxs-lookup"><span data-stu-id="a317b-117">How to use Azure Search from a .NET Application</span></span>](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk)

## <a name="overview"></a><span data-ttu-id="a317b-118">Panoramica</span><span class="sxs-lookup"><span data-stu-id="a317b-118">Overview</span></span>

<span data-ttu-id="a317b-119">Le query di tipo "prima e dopo" illustrano il valore dei sinonimi.</span><span class="sxs-lookup"><span data-stu-id="a317b-119">Before-and-after queries demonstrate the value of synonyms.</span></span> <span data-ttu-id="a317b-120">In questa esercitazione viene usata un'applicazione di esempio che esegue query e restituisce risultati in un indice di esempio.</span><span class="sxs-lookup"><span data-stu-id="a317b-120">In this tutorial, we use a sample application that executes queries and returns results on a sample index.</span></span> <span data-ttu-id="a317b-121">L'applicazione di esempio crea un indice di dimensioni ridotte denominato "hotels", popolato con due documenti.</span><span class="sxs-lookup"><span data-stu-id="a317b-121">The sample application creates a small index named "hotels" populated with two documents.</span></span> <span data-ttu-id="a317b-122">L'applicazione esegue query di ricerca usando termini e frasi non visualizzati nell'indice, abilita la funzionalità relativa ai sinonimi e quindi esegue di nuovo le stesse ricerche.</span><span class="sxs-lookup"><span data-stu-id="a317b-122">The application executes search queries using terms and phrases that do not appear in the index, enables the synonyms feature, then issues the same searches again.</span></span> <span data-ttu-id="a317b-123">Il codice seguente illustra il flusso complessivo.</span><span class="sxs-lookup"><span data-stu-id="a317b-123">The code below demonstrates the overall flow.</span></span>

```csharp
  static void Main(string[] args)
  {
      SearchServiceClient serviceClient = CreateSearchServiceClient();

      Console.WriteLine("{0}", "Cleaning up resources...\n");
      CleanupResources(serviceClient);

      Console.WriteLine("{0}", "Creating index...\n");
      CreateHotelsIndex(serviceClient);

      ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");

      Console.WriteLine("{0}", "Uploading documents...\n");
      UploadDocuments(indexClient);

      ISearchIndexClient indexClientForQueries = CreateSearchIndexClient();

      RunQueriesWithNonExistentTermsInIndex(indexClientForQueries);

      Console.WriteLine("{0}", "Adding synonyms...\n");
      UploadSynonyms(serviceClient);
      EnableSynonymsInHotelsIndex(serviceClient);
      Thread.Sleep(10000); // Wait for the changes to propagate

      RunQueriesWithNonExistentTermsInIndex(indexClientForQueries);

      Console.WriteLine("{0}", "Complete.  Press any key to end application...\n");

      Console.ReadKey();
  }
```
<span data-ttu-id="a317b-124">Per informazioni sulla procedura per la creazione e il popolamento dell'indice di esempio, vedere [Come utilizzare Ricerca di Azure da un'applicazione .NET](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span><span class="sxs-lookup"><span data-stu-id="a317b-124">The steps to create and populate the sample index are explained in [How to use Azure Search from a .NET Application](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span></span>

## <a name="before-queries"></a><span data-ttu-id="a317b-125">Query di tipo "prima"</span><span class="sxs-lookup"><span data-stu-id="a317b-125">"Before" queries</span></span>

<span data-ttu-id="a317b-126">In `RunQueriesWithNonExistentTermsInIndex` vengono eseguite query di ricerca con i termini "five star", "internet" ed "economy AND hotel".</span><span class="sxs-lookup"><span data-stu-id="a317b-126">In `RunQueriesWithNonExistentTermsInIndex`, we issue search queries with "five star", "internet", and "economy AND hotel".</span></span>
```csharp
Console.WriteLine("Search the entire index for the phrase \"five star\":\n");
results = indexClient.Documents.Search<Hotel>("\"five star\"", parameters);
WriteDocuments(results);

Console.WriteLine("Search the entire index for the term 'internet':\n");
results = indexClient.Documents.Search<Hotel>("internet", parameters);
WriteDocuments(results);

Console.WriteLine("Search the entire index for the terms 'economy' AND 'hotel':\n");
results = indexClient.Documents.Search<Hotel>("economy AND hotel", parameters);
WriteDocuments(results);
```
<span data-ttu-id="a317b-127">Nessuno dei due documenti indicizzati contiene questi termini, quindi si ottiene l'output seguente dal primo comando `RunQueriesWithNonExistentTermsInIndex`.</span><span class="sxs-lookup"><span data-stu-id="a317b-127">Neither of the two indexed documents contain the terms, so we get the following output from the first `RunQueriesWithNonExistentTermsInIndex`.</span></span>
~~~
Search the entire index for the phrase "five star":

no document matched

Search the entire index for the term 'internet':

no document matched

Search the entire index for the terms 'economy' AND 'hotel':

no document matched
~~~

## <a name="enable-synonyms"></a><span data-ttu-id="a317b-128">Abilitare i sinonimi</span><span class="sxs-lookup"><span data-stu-id="a317b-128">Enable synonyms</span></span>

<span data-ttu-id="a317b-129">L'abilitazione dei sinonimi è un processo in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="a317b-129">Enabling synonyms is a two-step process.</span></span> <span data-ttu-id="a317b-130">Vengono prima di tutto definite e caricate le regole dei sinonimi e quindi vengono configurati i campi per usarle.</span><span class="sxs-lookup"><span data-stu-id="a317b-130">We first define and upload synonym rules and then configure fields to use them.</span></span> <span data-ttu-id="a317b-131">Il processo viene illustrato in `UploadSynonyms` e `EnableSynonymsInHotelsIndex`.</span><span class="sxs-lookup"><span data-stu-id="a317b-131">The process is outlined in `UploadSynonyms` and `EnableSynonymsInHotelsIndex`.</span></span>

1. <span data-ttu-id="a317b-132">Aggiungere una mappa di sinonimi al servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="a317b-132">Add a synonym map to your search service.</span></span> <span data-ttu-id="a317b-133">In `UploadSynonyms` vengono definite quattro regole nella mappa di sinonimi 'desc-synonymmap' e viene eseguito il caricamento nel servizio.</span><span class="sxs-lookup"><span data-stu-id="a317b-133">In `UploadSynonyms`, we define four rules in our synonym map 'desc-synonymmap' and upload to the service.</span></span>
```csharp
    var synonymMap = new SynonymMap()
    {
        Name = "desc-synonymmap",
        Format = "solr",
        Synonyms = "hotel, motel\n
                    internet,wifi\n
                    five star=>luxury\n
                    economy,inexpensive=>budget"
    };

    serviceClient.SynonymMaps.CreateOrUpdate(synonymMap);
```
<span data-ttu-id="a317b-134">Una mappa di sinonimi deve essere conforme al formato `solr` dello standard open source.</span><span class="sxs-lookup"><span data-stu-id="a317b-134">A synonym map must conform to the open source standard `solr` format.</span></span> <span data-ttu-id="a317b-135">Il formato viene illustrato in [Synonyms in Azure Search](search-synonyms.md) (Sinonimi in Ricerca di Azure) nella sezione `Apache Solr synonym format`.</span><span class="sxs-lookup"><span data-stu-id="a317b-135">The format is explained in [Synonyms in Azure Search](search-synonyms.md) under the section `Apache Solr synonym format`.</span></span>

2. <span data-ttu-id="a317b-136">Configurare i campi disponibili per la ricerca per l'uso della mappa di sinonimi nella definizione dell'indice.</span><span class="sxs-lookup"><span data-stu-id="a317b-136">Configure searchable fields to use the synonym map in the index definition.</span></span> <span data-ttu-id="a317b-137">In `EnableSynonymsInHotelsIndex` vengono abilitati i sinonimi in due campi, `category` e `tags`, tramite l'impostazione della proprietà `synonymMaps` sul nome della mappa di sinonimi appena caricata.</span><span class="sxs-lookup"><span data-stu-id="a317b-137">In `EnableSynonymsInHotelsIndex`, we enable synonyms on two fields `category` and `tags` by setting the `synonymMaps` property to the name of the newly uploaded synonym map.</span></span>
```csharp
  Index index = serviceClient.Indexes.Get("hotels");
  index.Fields.First(f => f.Name == "category").SynonymMaps = new[] { "desc-synonymmap" };
  index.Fields.First(f => f.Name == "tags").SynonymMaps = new[] { "desc-synonymmap" };

  serviceClient.Indexes.CreateOrUpdate(index);
```
<span data-ttu-id="a317b-138">Quando si aggiunge una mappa di sinonimi, non è necessario ricompilare l'indice.</span><span class="sxs-lookup"><span data-stu-id="a317b-138">When you add a synonym map, index rebuilds are not required.</span></span> <span data-ttu-id="a317b-139">È possibile aggiungere una mappa di sinonimi al servizio e quindi correggere le definizioni di campi esistenti in qualsiasi indice in modo da usare la nuova mappa di sinonimi.</span><span class="sxs-lookup"><span data-stu-id="a317b-139">You can add a synonym map to your service, and then amend existing field definitions in any index to use the new synonym map.</span></span> <span data-ttu-id="a317b-140">L'aggiunta di nuovi attributi non ha alcun impatto sulla disponibilità dell'indice.</span><span class="sxs-lookup"><span data-stu-id="a317b-140">The addition of new attributes has no impact on index availability.</span></span> <span data-ttu-id="a317b-141">Ciò vale anche per la disabilitazione dei sinonimi per un campo.</span><span class="sxs-lookup"><span data-stu-id="a317b-141">The same applies in disabling synonyms for a field.</span></span> <span data-ttu-id="a317b-142">È possibile impostare semplicemente la proprietà `synonymMaps` su un elenco vuoto.</span><span class="sxs-lookup"><span data-stu-id="a317b-142">You can simply set the `synonymMaps` property to an empty list.</span></span>
```csharp
  index.Fields.First(f => f.Name == "category").SynonymMaps = new List<string>();
```

## <a name="after-queries"></a><span data-ttu-id="a317b-143">Query di tipo "dopo"</span><span class="sxs-lookup"><span data-stu-id="a317b-143">"After" queries</span></span>

<span data-ttu-id="a317b-144">Dopo il caricamento della mappa di sinonimi e l'aggiornamento dell'indice per l'uso della mappa di sinonimi, la seconda chiamata `RunQueriesWithNonExistentTermsInIndex` restituisce quanto segue:</span><span class="sxs-lookup"><span data-stu-id="a317b-144">After the synonym map is uploaded and the index is updated to use the synonym map, the second `RunQueriesWithNonExistentTermsInIndex` call outputs the following:</span></span>

~~~
Search the entire index for the phrase "five star":

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search the entire index for the term 'internet':

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search the entire index for the terms 'economy' AND 'hotel':

Name: Roach Motel       Category: Budget        Tags: [motel, budget]
~~~
<span data-ttu-id="a317b-145">La prima query trova il documento dalla regola `five star=>luxury`.</span><span class="sxs-lookup"><span data-stu-id="a317b-145">The first query finds the document from the rule `five star=>luxury`.</span></span> <span data-ttu-id="a317b-146">La seconda query espande la ricerca usando `internet,wifi` e la terza usando `hotel, motel` e `economy,inexpensive=>budget` nell'individuazione di documenti corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="a317b-146">The second query expands the search using `internet,wifi` and the third using both `hotel, motel` and `economy,inexpensive=>budget` in finding the documents they matched.</span></span>

<span data-ttu-id="a317b-147">L'aggiunta di sinonimi modifica completamente l'esperienza di ricerca.</span><span class="sxs-lookup"><span data-stu-id="a317b-147">Adding synonyms completely changes the search experience.</span></span> <span data-ttu-id="a317b-148">In questa esercitazione le query originali non sono in grado di restituire risultati significativi, anche se i documenti nell'indice sono rilevanti.</span><span class="sxs-lookup"><span data-stu-id="a317b-148">In this tutorial, the original queries failed to return meaningful results even though the documents in our index were relevant.</span></span> <span data-ttu-id="a317b-149">Abilitando i sinonimi, è possibile espandere un indice in modo da includere termini di uso comune, senza modifiche ai dati sottostanti dell'indice.</span><span class="sxs-lookup"><span data-stu-id="a317b-149">By enabling synonyms, we can expand an index to include terms in common use, with no changes to underlying data in the index.</span></span>

## <a name="sample-application-source-code"></a><span data-ttu-id="a317b-150">Esempio di codice sorgente dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="a317b-150">Sample application source code</span></span>
<span data-ttu-id="a317b-151">Il codice sorgente completo dell'applicazione di esempio utilizzata è disponibile in questa procedura dettagliata su [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms).</span><span class="sxs-lookup"><span data-stu-id="a317b-151">You can find the full source code of the sample application used in this walk through on [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a317b-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a317b-152">Next steps</span></span>

* <span data-ttu-id="a317b-153">Vedere [How to use synonyms in Azure Search](search-synonyms.md) (Come usare i sinonimi in Ricerca di Azure)</span><span class="sxs-lookup"><span data-stu-id="a317b-153">Review [How to use synonyms in Azure Search](search-synonyms.md)</span></span>
* <span data-ttu-id="a317b-154">Vedere [Synonyms REST API documentation](https://aka.ms/rgm6rq) (Documentazione sull'API REST Synonyms)</span><span class="sxs-lookup"><span data-stu-id="a317b-154">Review [Synonyms REST API documentation](https://aka.ms/rgm6rq)</span></span>
* <span data-ttu-id="a317b-155">Vedere le guide di riferimento di [SDK di .NET](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) e [API REST](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="a317b-155">Browse the references for the [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) and [REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
