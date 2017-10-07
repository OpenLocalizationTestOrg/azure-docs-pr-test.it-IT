---
title: aaaSynonyms anteprima esercitazione in ricerca di Azure | Documenti Microsoft
description: "Aggiungere l'indice di tooan funzionalità di anteprima di hello sinonimi in ricerca di Azure."
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
ms.openlocfilehash: 055c1cbafb945823a3dc4da0c522db236b1d192c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="synonym-preview-c-tutorial-for-azure-search"></a><span data-ttu-id="0c817-103">Esercitazione sui sinonimi (anteprima) in C# per Ricerca di Azure</span><span class="sxs-lookup"><span data-stu-id="0c817-103">Synonym (preview) C# tutorial for Azure Search</span></span>

<span data-ttu-id="0c817-104">Sinonimi espandere una query di corrispondenza in base alle esigenze considerato come termine di input toohello semanticamente equivalente.</span><span class="sxs-lookup"><span data-stu-id="0c817-104">Synonyms expand a query by matching on terms considered semantically equivalent toohello input term.</span></span> <span data-ttu-id="0c817-105">Ad esempio, è consigliabile che documenti toomatch "car" che contiene termini di hello "automobile" o "vehicle".</span><span class="sxs-lookup"><span data-stu-id="0c817-105">For example, you might want "car" toomatch documents containing hello terms "automobile" or "vehicle".</span></span>

<span data-ttu-id="0c817-106">In Ricerca di Azure i sinonimi sono definiti in una *mappa di sinonimi* tramite *regole di mapping* che associano termini equivalenti.</span><span class="sxs-lookup"><span data-stu-id="0c817-106">In Azure Search, synonyms are defined in a *synonym map*, through *mapping rules* that associate equivalent terms.</span></span> <span data-ttu-id="0c817-107">È possibile creare più mappe sinonimo, registrarli come indice tooany disponibile la risorsa a livello di servizio e quindi fare riferimento quali uno toouse a livello di campo hello.</span><span class="sxs-lookup"><span data-stu-id="0c817-107">You can create multiple synonym maps, post them as a service-wide resource available tooany index, and then reference which one toouse at hello field level.</span></span> <span data-ttu-id="0c817-108">In fase di query inoltre toosearching un indice, ricerca di Azure effettua una ricerca in una mappa del sinonimo, se ne è stato specificato nei campi utilizzati nella query hello.</span><span class="sxs-lookup"><span data-stu-id="0c817-108">At query time, in addition toosearching an index, Azure Search does a lookup in a synonym map, if one is specified on fields used in hello query.</span></span>

> [!NOTE]
> <span data-ttu-id="0c817-109">sinonimi Hello funzionalità è attualmente in anteprima e solo supportati in hello anteprima più recente di API e le versioni SDK (api-version = 2016-09-01-Preview, anteprima di SDK versione 4. x).</span><span class="sxs-lookup"><span data-stu-id="0c817-109">hello synonyms feature is currently in preview and only supported in hello latest preview API and SDK versions (api-version=2016-09-01-Preview, SDK version 4.x-preview).</span></span> <span data-ttu-id="0c817-110">Non è attualmente disponibile alcun supporto nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0c817-110">There is no Azure portal support at this time.</span></span> <span data-ttu-id="0c817-111">Le API disponibili in anteprima non rientrano nel Contratto di servizio e le funzionalità disponibili in anteprima possono subire modifiche, quindi non è consigliabile usarle nelle applicazioni di produzione.</span><span class="sxs-lookup"><span data-stu-id="0c817-111">Preview APIs are not under SLA and preview features may change, so we do not recommend using them in production applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0c817-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0c817-112">Prerequisites</span></span>

<span data-ttu-id="0c817-113">Requisiti dell'esercitazione includono hello informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="0c817-113">Tutorial requirements include hello following:</span></span>

* [<span data-ttu-id="0c817-114">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0c817-114">Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="0c817-115">Servizio Ricerca di Azure</span><span class="sxs-lookup"><span data-stu-id="0c817-115">Azure Search service</span></span>](search-create-service-portal.md)
* [<span data-ttu-id="0c817-116">Versione di anteprima della libreria Microsoft.Azure.Search .NET</span><span class="sxs-lookup"><span data-stu-id="0c817-116">Preview version of Microsoft.Azure.Search .NET library</span></span>](https://aka.ms/search-sdk-preview)
* [<span data-ttu-id="0c817-117">La modalità di ricerca di Azure toouse da un'applicazione .NET</span><span class="sxs-lookup"><span data-stu-id="0c817-117">How toouse Azure Search from a .NET Application</span></span>](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk)

## <a name="overview"></a><span data-ttu-id="0c817-118">Panoramica</span><span class="sxs-lookup"><span data-stu-id="0c817-118">Overview</span></span>

<span data-ttu-id="0c817-119">Query di prima e dopo illustrano valore hello di sinonimi.</span><span class="sxs-lookup"><span data-stu-id="0c817-119">Before-and-after queries demonstrate hello value of synonyms.</span></span> <span data-ttu-id="0c817-120">In questa esercitazione viene usata un'applicazione di esempio che esegue query e restituisce risultati in un indice di esempio.</span><span class="sxs-lookup"><span data-stu-id="0c817-120">In this tutorial, we use a sample application that executes queries and returns results on a sample index.</span></span> <span data-ttu-id="0c817-121">applicazione di esempio Hello crea un indice di dimensioni ridotte denominato "Hotel" popolato con i due documenti.</span><span class="sxs-lookup"><span data-stu-id="0c817-121">hello sample application creates a small index named "hotels" populated with two documents.</span></span> <span data-ttu-id="0c817-122">un'applicazione Hello esegue query di ricerca mediante i termini e le frasi che non sono presenti nell'indice hello, funzionalità hello sinonimi, quindi problemi hello ricerche stesso nuovamente.</span><span class="sxs-lookup"><span data-stu-id="0c817-122">hello application executes search queries using terms and phrases that do not appear in hello index, enables hello synonyms feature, then issues hello same searches again.</span></span> <span data-ttu-id="0c817-123">codice Hello riportato di seguito viene illustrato hello flusso globale.</span><span class="sxs-lookup"><span data-stu-id="0c817-123">hello code below demonstrates hello overall flow.</span></span>

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
      Thread.Sleep(10000); // Wait for hello changes toopropagate

      RunQueriesWithNonExistentTermsInIndex(indexClientForQueries);

      Console.WriteLine("{0}", "Complete.  Press any key tooend application...\n");

      Console.ReadKey();
  }
```
<span data-ttu-id="0c817-124">Hello toocreate passaggi e popolare l'indice di esempio hello vengono spiegate in [come toouse ricerca di Azure da un'applicazione .NET](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span><span class="sxs-lookup"><span data-stu-id="0c817-124">hello steps toocreate and populate hello sample index are explained in [How toouse Azure Search from a .NET Application](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span></span>

## <a name="before-queries"></a><span data-ttu-id="0c817-125">Query di tipo "prima"</span><span class="sxs-lookup"><span data-stu-id="0c817-125">"Before" queries</span></span>

<span data-ttu-id="0c817-126">In `RunQueriesWithNonExistentTermsInIndex` vengono eseguite query di ricerca con i termini "five star", "internet" ed "economy AND hotel".</span><span class="sxs-lookup"><span data-stu-id="0c817-126">In `RunQueriesWithNonExistentTermsInIndex`, we issue search queries with "five star", "internet", and "economy AND hotel".</span></span>
```csharp
Console.WriteLine("Search hello entire index for hello phrase \"five star\":\n");
results = indexClient.Documents.Search<Hotel>("\"five star\"", parameters);
WriteDocuments(results);

Console.WriteLine("Search hello entire index for hello term 'internet':\n");
results = indexClient.Documents.Search<Hotel>("internet", parameters);
WriteDocuments(results);

Console.WriteLine("Search hello entire index for hello terms 'economy' AND 'hotel':\n");
results = indexClient.Documents.Search<Hotel>("economy AND hotel", parameters);
WriteDocuments(results);
```
<span data-ttu-id="0c817-127">Nessuno dei documenti indicizzati due hello contengono termini di hello, per esempio hello prima di tutto l'output di hello `RunQueriesWithNonExistentTermsInIndex`.</span><span class="sxs-lookup"><span data-stu-id="0c817-127">Neither of hello two indexed documents contain hello terms, so we get hello following output from hello first `RunQueriesWithNonExistentTermsInIndex`.</span></span>
~~~
Search hello entire index for hello phrase "five star":

no document matched

Search hello entire index for hello term 'internet':

no document matched

Search hello entire index for hello terms 'economy' AND 'hotel':

no document matched
~~~

## <a name="enable-synonyms"></a><span data-ttu-id="0c817-128">Abilitare i sinonimi</span><span class="sxs-lookup"><span data-stu-id="0c817-128">Enable synonyms</span></span>

<span data-ttu-id="0c817-129">L'abilitazione dei sinonimi è un processo in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="0c817-129">Enabling synonyms is a two-step process.</span></span> <span data-ttu-id="0c817-130">È innanzitutto definire e caricare le regole di sinonimo e quindi configurare i campi toouse li.</span><span class="sxs-lookup"><span data-stu-id="0c817-130">We first define and upload synonym rules and then configure fields toouse them.</span></span> <span data-ttu-id="0c817-131">il processo di Hello è descritto in `UploadSynonyms` e `EnableSynonymsInHotelsIndex`.</span><span class="sxs-lookup"><span data-stu-id="0c817-131">hello process is outlined in `UploadSynonyms` and `EnableSynonymsInHotelsIndex`.</span></span>

1. <span data-ttu-id="0c817-132">Aggiungere un servizio di ricerca tooyour mappa sinonimo.</span><span class="sxs-lookup"><span data-stu-id="0c817-132">Add a synonym map tooyour search service.</span></span> <span data-ttu-id="0c817-133">In `UploadSynonyms`, si definiscono quattro regole nella mappa di sinonimo 'desc synonymmap' e toohello servizio di caricamento.</span><span class="sxs-lookup"><span data-stu-id="0c817-133">In `UploadSynonyms`, we define four rules in our synonym map 'desc-synonymmap' and upload toohello service.</span></span>
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
<span data-ttu-id="0c817-134">Una mappa di sinonimo deve essere conforme a standard di origine aprire toohello `solr` formato.</span><span class="sxs-lookup"><span data-stu-id="0c817-134">A synonym map must conform toohello open source standard `solr` format.</span></span> <span data-ttu-id="0c817-135">viene illustrato il formato di Hello in [sinonimi in ricerca di Azure](search-synonyms.md) nella sezione hello `Apache Solr synonym format`.</span><span class="sxs-lookup"><span data-stu-id="0c817-135">hello format is explained in [Synonyms in Azure Search](search-synonyms.md) under hello section `Apache Solr synonym format`.</span></span>

2. <span data-ttu-id="0c817-136">Configurare i campi ricercabili toouse hello sinonimo mappa nella definizione dell'indice hello.</span><span class="sxs-lookup"><span data-stu-id="0c817-136">Configure searchable fields toouse hello synonym map in hello index definition.</span></span> <span data-ttu-id="0c817-137">In `EnableSynonymsInHotelsIndex`, si abilita sinonimi due campi `category` e `tags` dall'impostazione hello `synonymMaps` toohello nome della proprietà di hello appena caricato mappa sinonimo.</span><span class="sxs-lookup"><span data-stu-id="0c817-137">In `EnableSynonymsInHotelsIndex`, we enable synonyms on two fields `category` and `tags` by setting hello `synonymMaps` property toohello name of hello newly uploaded synonym map.</span></span>
```csharp
  Index index = serviceClient.Indexes.Get("hotels");
  index.Fields.First(f => f.Name == "category").SynonymMaps = new[] { "desc-synonymmap" };
  index.Fields.First(f => f.Name == "tags").SynonymMaps = new[] { "desc-synonymmap" };

  serviceClient.Indexes.CreateOrUpdate(index);
```
<span data-ttu-id="0c817-138">Quando si aggiunge una mappa di sinonimi, non è necessario ricompilare l'indice.</span><span class="sxs-lookup"><span data-stu-id="0c817-138">When you add a synonym map, index rebuilds are not required.</span></span> <span data-ttu-id="0c817-139">È possibile aggiungere un servizio di tooyour sinonimo mappa e quindi modificare le definizioni di campo esistente in qualsiasi indice toouse hello nuovo sinonimo mapping.</span><span class="sxs-lookup"><span data-stu-id="0c817-139">You can add a synonym map tooyour service, and then amend existing field definitions in any index toouse hello new synonym map.</span></span> <span data-ttu-id="0c817-140">aggiunta di Hello di nuovi attributi non ha alcun impatto sulla disponibilità di indice.</span><span class="sxs-lookup"><span data-stu-id="0c817-140">hello addition of new attributes has no impact on index availability.</span></span> <span data-ttu-id="0c817-141">Ciò vale anche la disabilitazione di sinonimi per un campo di Hello.</span><span class="sxs-lookup"><span data-stu-id="0c817-141">hello same applies in disabling synonyms for a field.</span></span> <span data-ttu-id="0c817-142">È possibile impostare semplicemente hello `synonymMaps` elenco di proprietà tooan vuoto.</span><span class="sxs-lookup"><span data-stu-id="0c817-142">You can simply set hello `synonymMaps` property tooan empty list.</span></span>
```csharp
  index.Fields.First(f => f.Name == "category").SynonymMaps = new List<string>();
```

## <a name="after-queries"></a><span data-ttu-id="0c817-143">Query di tipo "dopo"</span><span class="sxs-lookup"><span data-stu-id="0c817-143">"After" queries</span></span>

<span data-ttu-id="0c817-144">Dopo la mappa di sinonimo hello viene caricata e indice hello è mappa sinonimo di hello toouse aggiornato, hello secondo `RunQueriesWithNonExistentTermsInIndex` chiamata genera seguente hello:</span><span class="sxs-lookup"><span data-stu-id="0c817-144">After hello synonym map is uploaded and hello index is updated toouse hello synonym map, hello second `RunQueriesWithNonExistentTermsInIndex` call outputs hello following:</span></span>

~~~
Search hello entire index for hello phrase "five star":

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search hello entire index for hello term 'internet':

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search hello entire index for hello terms 'economy' AND 'hotel':

Name: Roach Motel       Category: Budget        Tags: [motel, budget]
~~~
<span data-ttu-id="0c817-145">prima query Hello trova hello documento dalla regola hello `five star=>luxury`.</span><span class="sxs-lookup"><span data-stu-id="0c817-145">hello first query finds hello document from hello rule `five star=>luxury`.</span></span> <span data-ttu-id="0c817-146">seconda query Hello espande hello ricerca tramite `internet,wifi` e hello terzo utilizzando sia `hotel, motel` e `economy,inexpensive=>budget` nella ricerca di documenti hello di corrispondenza con.</span><span class="sxs-lookup"><span data-stu-id="0c817-146">hello second query expands hello search using `internet,wifi` and hello third using both `hotel, motel` and `economy,inexpensive=>budget` in finding hello documents they matched.</span></span>

<span data-ttu-id="0c817-147">Aggiunta di sinonimi completamente modifica hello un'esperienza di ricerca.</span><span class="sxs-lookup"><span data-stu-id="0c817-147">Adding synonyms completely changes hello search experience.</span></span> <span data-ttu-id="0c817-148">In questa esercitazione, query originale hello Impossibile risultati significativi tooreturn anche se erano rilevanti documenti hello nel nostro indice.</span><span class="sxs-lookup"><span data-stu-id="0c817-148">In this tutorial, hello original queries failed tooreturn meaningful results even though hello documents in our index were relevant.</span></span> <span data-ttu-id="0c817-149">Abilitando i sinonimi, è possibile espandere un tooinclude indice termini di uso comune, senza dati toounderlying modifiche nell'indice hello.</span><span class="sxs-lookup"><span data-stu-id="0c817-149">By enabling synonyms, we can expand an index tooinclude terms in common use, with no changes toounderlying data in hello index.</span></span>

## <a name="sample-application-source-code"></a><span data-ttu-id="0c817-150">Esempio di codice sorgente dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="0c817-150">Sample application source code</span></span>
<span data-ttu-id="0c817-151">È possibile trovare il codice sorgente completo hello dell'applicazione di esempio hello utilizzato in questa procedura dettagliata su [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms).</span><span class="sxs-lookup"><span data-stu-id="0c817-151">You can find hello full source code of hello sample application used in this walk through on [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c817-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0c817-152">Next steps</span></span>

* <span data-ttu-id="0c817-153">Revisione [come sinonimi toouse in ricerca di Azure](search-synonyms.md)</span><span class="sxs-lookup"><span data-stu-id="0c817-153">Review [How toouse synonyms in Azure Search](search-synonyms.md)</span></span>
* <span data-ttu-id="0c817-154">Vedere [Synonyms REST API documentation](https://aka.ms/rgm6rq) (Documentazione sull'API REST Synonyms)</span><span class="sxs-lookup"><span data-stu-id="0c817-154">Review [Synonyms REST API documentation](https://aka.ms/rgm6rq)</span></span>
* <span data-ttu-id="0c817-155">Individuare i riferimenti di hello per hello [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) e [API REST](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="0c817-155">Browse hello references for hello [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) and [REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
