---
title: Come gestire le scritture simultanee nelle risorse in Ricerca di Azure
description: Usare la concorrenza ottimistica per evitare conflitti a livello di aggiornamento o di eliminazione in indici, indicizzatori e origini dati di Ricerca di Azure.
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 
ms.service: search
ms.devlang: 
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/21/2017
ms.author: heidist
ms.openlocfilehash: aee1b7376d4829e3e2f5a232525e3c3cb4df9d8e
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="how-to-manage-concurrency-in-azure-search"></a><span data-ttu-id="9bb98-103">Come gestire la concorrenza in Ricerca di Azure</span><span class="sxs-lookup"><span data-stu-id="9bb98-103">How to manage concurrency in Azure Search</span></span>

<span data-ttu-id="9bb98-104">Quando si gestiscono le risorse di Ricerca di Azure, ad esempio indici e origini dati, è importante aggiornare le risorse in modo sicuro, soprattutto se componenti diversi dell'applicazione accedono simultaneamente alle risorse.</span><span class="sxs-lookup"><span data-stu-id="9bb98-104">When managing Azure Search resources such as indexes and data sources, it's important to update resources safely, especially if resources are accessed concurrently by different components of your application.</span></span> <span data-ttu-id="9bb98-105">Quando due client aggiornano simultaneamente un risorsa senza coordinazione, si possono verificare race condition.</span><span class="sxs-lookup"><span data-stu-id="9bb98-105">When two clients concurrently update a resource without coordination, race conditions are possible.</span></span> <span data-ttu-id="9bb98-106">Per evitare questo problema, Ricerca di Azure offre un *modello di concorrenza ottimistica*.</span><span class="sxs-lookup"><span data-stu-id="9bb98-106">To prevent this, Azure Search offers an *optimistic concurrency model*.</span></span> <span data-ttu-id="9bb98-107">Non sono presenti blocchi su una risorsa,</span><span class="sxs-lookup"><span data-stu-id="9bb98-107">There are no locks on a resource.</span></span> <span data-ttu-id="9bb98-108">ma per ogni risorsa esiste un ETag che identifica la versione della risorsa in modo che sia possibile creare richieste che evitano sovrascritture accidentali.</span><span class="sxs-lookup"><span data-stu-id="9bb98-108">Instead, there is an ETag for every resource that identifies the resource version so that you can craft requests that avoid accidental overwrites.</span></span>

> [!Tip]
> <span data-ttu-id="9bb98-109">Il codice concettuale in una [soluzione C# di esempio](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer) illustra come funziona il controllo della concorrenza in Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="9bb98-109">Conceptual code in a [sample C# solution](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer) explains how concurrency control works in Azure Search.</span></span> <span data-ttu-id="9bb98-110">Il codice crea le condizioni che richiamano il controllo della concorrenza.</span><span class="sxs-lookup"><span data-stu-id="9bb98-110">The code creates conditions that invoke concurrency control.</span></span> <span data-ttu-id="9bb98-111">La lettura del [frammento di codice riportato più avanti](#samplecode) è probabilmente sufficiente per la maggior parte degli sviluppatori, ma, se lo si vuole eseguire, modificare appsettings.json per aggiungere il nome del servizio e una chiave API di amministrazione.</span><span class="sxs-lookup"><span data-stu-id="9bb98-111">Reading the [code fragment below](#samplecode) is probably sufficient for most developers, but if you want to run it, edit appsettings.json to add the service name and an admin api-key.</span></span> <span data-ttu-id="9bb98-112">Dato un URL del servizio `http://myservice.search.windows.net`, il nome del service è `myservice`.</span><span class="sxs-lookup"><span data-stu-id="9bb98-112">Given a service URL of `http://myservice.search.windows.net`, the service name is `myservice`.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="9bb98-113">Funzionamento</span><span class="sxs-lookup"><span data-stu-id="9bb98-113">How it works</span></span>

<span data-ttu-id="9bb98-114">La concorrenza ottimistica viene implementata tramite i controlli delle condizioni di accesso nelle chiamate API che scrivono in indici, indicizzatori, origini dati e risorse synonymMap.</span><span class="sxs-lookup"><span data-stu-id="9bb98-114">Optimistic concurrency is implemented through access condition checks in API calls writing to indexes, indexers, datasources, and synonymMap resources.</span></span> 

<span data-ttu-id="9bb98-115">Tutte le risorse hanno un [*tag di entità (ETag)*](https://en.wikipedia.org/wiki/HTTP_ETag) che fornisce informazioni sulla versione dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="9bb98-115">All resources have an [*entity tag (ETag)*](https://en.wikipedia.org/wiki/HTTP_ETag) that provides object version information.</span></span> <span data-ttu-id="9bb98-116">Controllando prima l'ETag, è possibile evitare aggiornamenti simultanei in un flusso di lavoro tipico (acquisizione, modifica locale, aggiornamento) assicurandosi che l'ETag della risorsa corrisponda alla copia locale.</span><span class="sxs-lookup"><span data-stu-id="9bb98-116">By checking the ETag first, you can avoid concurrent updates in a typical workflow (get, modify locally, update) by ensuring the resource's ETag matches your local copy.</span></span> 

+ <span data-ttu-id="9bb98-117">L'API REST usa un [ETag](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) nell'intestazione della richiesta.</span><span class="sxs-lookup"><span data-stu-id="9bb98-117">The REST API uses an [ETag](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) on the request header.</span></span>
+ <span data-ttu-id="9bb98-118">.NET SDK imposta l'ETag tramite un oggetto accessCondition, impostando l'[intestazione If-Match | If-Match-None](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) per la risorsa.</span><span class="sxs-lookup"><span data-stu-id="9bb98-118">The .NET SDK sets the ETag through an accessCondition object, setting the [If-Match | If-Match-None header](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) on the resource.</span></span> <span data-ttu-id="9bb98-119">Tutti gli oggetti che ereditano da [IResourceWithETag (.NET SDK)](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.iresourcewithetag) hanno un oggetto accessCondition.</span><span class="sxs-lookup"><span data-stu-id="9bb98-119">Any object inheriting from [IResourceWithETag (.NET SDK)](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.iresourcewithetag) has an accessCondition object.</span></span>

<span data-ttu-id="9bb98-120">Ogni volta che si aggiorna una risorsa, l'ETag cambia automaticamente.</span><span class="sxs-lookup"><span data-stu-id="9bb98-120">Every time you update a resource, its ETag changes automatically.</span></span> <span data-ttu-id="9bb98-121">Quando si implementa la gestione della concorrenza, si inserisce semplicemente una precondizione nella richiesta di aggiornamento, che obbliga la risorsa remota ad avere lo stesso ETag della copia della risorsa modificata nel client.</span><span class="sxs-lookup"><span data-stu-id="9bb98-121">When you implement concurrency management, all you're doing is putting a precondition on the update request that requires the remote resource to have the same ETag as the copy of the resource that you modified on the client.</span></span> <span data-ttu-id="9bb98-122">Se un processo simultaneo ha già modificato la risorsa remota, l'ETag non soddisferà la precondizione e la richiesta genererà l'errore HTTP 412.</span><span class="sxs-lookup"><span data-stu-id="9bb98-122">If a concurrent process has changed the remote resource already, the ETag will not match the precondition and the request will fail with HTTP 412.</span></span> <span data-ttu-id="9bb98-123">Se si usa .NET SDK, viene generata una `CloudException` in cui il metodo di estensione `IsAccessConditionFailed()` restituisce true.</span><span class="sxs-lookup"><span data-stu-id="9bb98-123">If you're using the .NET SDK, this manifests as a `CloudException` where the `IsAccessConditionFailed()` extension method returns true.</span></span>

> [!Note]
> <span data-ttu-id="9bb98-124">Esiste un solo meccanismo per la concorrenza,</span><span class="sxs-lookup"><span data-stu-id="9bb98-124">There is only one mechanism for concurrency.</span></span> <span data-ttu-id="9bb98-125">che viene sempre usato indipendentemente dall'API usata per gli aggiornamenti delle risorse.</span><span class="sxs-lookup"><span data-stu-id="9bb98-125">It's always used regardless of which API is used for resource updates.</span></span> 

<a name="samplecode"></a>
## <a name="use-cases-and-sample-code"></a><span data-ttu-id="9bb98-126">Casi d'uso e codici di esempio</span><span class="sxs-lookup"><span data-stu-id="9bb98-126">Use cases and sample code</span></span>

<span data-ttu-id="9bb98-127">Il codice seguente illustra i controlli accessCondition per le principali operazioni di aggiornamento:</span><span class="sxs-lookup"><span data-stu-id="9bb98-127">The following code demonstrates accessCondition checks for key update operations:</span></span>

+ <span data-ttu-id="9bb98-128">L'aggiornamento non riesce se la risorsa non esiste più</span><span class="sxs-lookup"><span data-stu-id="9bb98-128">Fail an update if the resource no longer exists</span></span>
+ <span data-ttu-id="9bb98-129">L'aggiornamento non riesce se la versione della risorsa viene modificata</span><span class="sxs-lookup"><span data-stu-id="9bb98-129">Fail an update if the resource version changes</span></span>

### <a name="sample-code-from-dotnetetagsexplainer-programhttpsgithubcomazure-samplessearch-dotnet-getting-startedtreemasterdotnetetagsexplainer"></a><span data-ttu-id="9bb98-130">Codice di esempio dal [programma DotNetETagsExplainer](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer)</span><span class="sxs-lookup"><span data-stu-id="9bb98-130">Sample code from [DotNetETagsExplainer program](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer)</span></span>

```
    class Program
    {
        // This sample shows how ETags work by performing conditional updates and deletes
        // on an Azure Search index.
        static void Main(string[] args)
        {
            IConfigurationBuilder builder = new ConfigurationBuilder().AddJsonFile("appsettings.json");
            IConfigurationRoot configuration = builder.Build();

            SearchServiceClient serviceClient = CreateSearchServiceClient(configuration);

            Console.WriteLine("Deleting index...\n");
            DeleteTestIndexIfExists(serviceClient);

            // Every top-level resource in Azure Search has an associated ETag that keeps track of which version
            // of the resource you're working on. When you first create a resource such as an index, its ETag is
            // empty.
            Index index = DefineTestIndex();
            Console.WriteLine(
                $"Test index hasn't been created yet, so its ETag should be blank. ETag: '{index.ETag}'");

            // Once the resource exists in Azure Search, its ETag will be populated. Make sure to use the object
            // returned by the SearchServiceClient! Otherwise, you will still have the old object with the
            // blank ETag.
            Console.WriteLine("Creating index...\n");
            index = serviceClient.Indexes.Create(index);
            
            Console.WriteLine($"Test index created; Its ETag should be populated. ETag: '{index.ETag}'");

            // ETags let you do some useful things you couldn't do otherwise. For example, by using an If-Match
            // condition, we can update an index using CreateOrUpdate and be guaranteed that the update will only
            // succeed if the index already exists.
            index.Fields.Add(new Field("name", AnalyzerName.EnMicrosoft));
            index =
                serviceClient.Indexes.CreateOrUpdate(
                    index,
                    accessCondition: AccessCondition.GenerateIfExistsCondition());

            Console.WriteLine(
                $"Test index updated; Its ETag should have changed since it was created. ETag: '{index.ETag}'");

            // More importantly, ETags protect you from concurrent updates to the same resource. If another
            // client tries to update the resource, it will fail as long as all clients are using the right
            // access conditions.
            Index indexForClient1 = index;
            Index indexForClient2 = serviceClient.Indexes.Get("test");

            Console.WriteLine("Simulating concurrent update. To start, both clients see the same ETag.");
            Console.WriteLine($"Client 1 ETag: '{indexForClient1.ETag}' Client 2 ETag: '{indexForClient2.ETag}'");

            // Client 1 successfully updates the index.
            indexForClient1.Fields.Add(new Field("a", DataType.Int32));
            indexForClient1 =
                serviceClient.Indexes.CreateOrUpdate(
                    indexForClient1,
                    accessCondition: AccessCondition.IfNotChanged(indexForClient1));

            Console.WriteLine($"Test index updated by client 1; ETag: '{indexForClient1.ETag}'");

            // Client 2 tries to update the index, but fails, thanks to the ETag check.
            try
            {
                indexForClient2.Fields.Add(new Field("b", DataType.Boolean));
                serviceClient.Indexes.CreateOrUpdate(
                    indexForClient2, 
                    accessCondition: AccessCondition.IfNotChanged(indexForClient2));

                Console.WriteLine("Whoops; This shouldn't happen");
                Environment.Exit(1);
            }
            catch (CloudException e) when (e.IsAccessConditionFailed())
            {
                Console.WriteLine("Client 2 failed to update the index, as expected.");
            }

            // You can also use access conditions with Delete operations. For example, you can implement an
            // atomic version of the DeleteTestIndexIfExists method from this sample like this:
            Console.WriteLine("Deleting index...\n");
            serviceClient.Indexes.Delete("test", accessCondition: AccessCondition.GenerateIfExistsCondition());

            // This is slightly better than using the Exists method since it makes only one round trip to
            // Azure Search instead of potentially two. It also avoids an extra Delete request in cases where
            // the resource is deleted concurrently, but this doesn't matter much since resource deletion in
            // Azure Search is idempotent.

            // And we're done! Bye!
            Console.WriteLine("Complete.  Press any key to end application...\n");
            Console.ReadKey();
        }

        private static SearchServiceClient CreateSearchServiceClient(IConfigurationRoot configuration)
        {
            string searchServiceName = configuration["SearchServiceName"];
            string adminApiKey = configuration["SearchServiceAdminApiKey"];

            SearchServiceClient serviceClient =
                new SearchServiceClient(searchServiceName, new SearchCredentials(adminApiKey));
            return serviceClient;
        }

        private static void DeleteTestIndexIfExists(SearchServiceClient serviceClient)
        {
            if (serviceClient.Indexes.Exists("test"))
            {
                serviceClient.Indexes.Delete("test");
            }
        }

        private static Index DefineTestIndex() =>
            new Index()
            {
                Name = "test",
                Fields = new[] { new Field("id", DataType.String) { IsKey = true } }
            };
    }
}
```

## <a name="design-pattern"></a><span data-ttu-id="9bb98-131">Schema progettuale</span><span class="sxs-lookup"><span data-stu-id="9bb98-131">Design pattern</span></span>

<span data-ttu-id="9bb98-132">Uno schema progettuale per l'implementazione della concorrenza ottimistica deve includere un ciclo che recupera il controllo della condizione di accesso, un test per la condizione di accesso e, facoltativamente, una risorsa aggiornata prima di provare ad applicare di nuovo le modifiche.</span><span class="sxs-lookup"><span data-stu-id="9bb98-132">A design pattern for implementing optimistic concurrency should include a loop that retries the access condition check, a test for the access condition, and optionally retrieves an updated resource before attempting to re-apply the changes.</span></span> 

<span data-ttu-id="9bb98-133">Questo frammento di codice illustra l'aggiunta di synonymMap a un indice già esistente.</span><span class="sxs-lookup"><span data-stu-id="9bb98-133">This code snippet illustrates the addition of a synonymMap to an index that already exists.</span></span> <span data-ttu-id="9bb98-134">Questo codice è tratto da [Esercitazione sui sinonimi (anteprima) in C# per Ricerca di Azure](https://docs.microsoft.com/azure/search/search-synonyms-tutorial-sdk).</span><span class="sxs-lookup"><span data-stu-id="9bb98-134">This code is from the [Synonym (preview) C# tutorial for Azure Search](https://docs.microsoft.com/azure/search/search-synonyms-tutorial-sdk).</span></span> 

<span data-ttu-id="9bb98-135">Il frammento ottiene l'indice "hotels", controlla la versione dell'oggetto in un'operazione di aggiornamento, genera un'eccezione se la condizione ha esito negativo e quindi esegue un nuovo tentativo di operazione (fino a tre volte), iniziando con il recupero dell'indice dal server per ottenere la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="9bb98-135">The snippet gets the "hotels" index, checks the object version on an update operation, throws an exception if the condition fails, and then retries the operation (up to three times), starting with index retrieval from the server to get the latest version.</span></span>

        private static void EnableSynonymsInHotelsIndexSafely(SearchServiceClient serviceClient)
        {
            int MaxNumTries = 3;

            for (int i = 0; i < MaxNumTries; ++i)
            {
                try
                {
                    Index index = serviceClient.Indexes.Get("hotels");
                    index = AddSynonymMapsToFields(index);

                    // The IfNotChanged condition ensures that the index is updated only if the ETags match.
                    serviceClient.Indexes.CreateOrUpdate(index, accessCondition: AccessCondition.IfNotChanged(index));

                    Console.WriteLine("Updated the index successfully.\n");
                    break;
                }
                catch (CloudException e) when (e.IsAccessConditionFailed())
                {
                    Console.WriteLine($"Index update failed : {e.Message}. Attempt({i}/{MaxNumTries}).\n");
                }
            }
        }
        
        private static Index AddSynonymMapsToFields(Index index)
        {
            index.Fields.First(f => f.Name == "category").SynonymMaps = new[] { "desc-synonymmap" };
            index.Fields.First(f => f.Name == "tags").SynonymMaps = new[] { "desc-synonymmap" };
            return index;
        }


## <a name="next-steps"></a><span data-ttu-id="9bb98-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9bb98-136">Next steps</span></span>

<span data-ttu-id="9bb98-137">Per altre informazioni su come aggiornare in modo sicuro un indice esistente, vedere l'[esempio in C# per i sinonimi](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms).</span><span class="sxs-lookup"><span data-stu-id="9bb98-137">Review the [synonyms C# sample](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms) for more context on how to safely update an existing index.</span></span>

<span data-ttu-id="9bb98-138">Provare a modificare uno dei due esempi seguenti per includere ETag o oggetti AccessCondition.</span><span class="sxs-lookup"><span data-stu-id="9bb98-138">Try modifying either of the following samples to include ETags or AccessCondition objects.</span></span>

+ [<span data-ttu-id="9bb98-139">Esempio di API REST in GitHub</span><span class="sxs-lookup"><span data-stu-id="9bb98-139">REST API sample on Github</span></span>](https://github.com/Azure-Samples/search-rest-api-getting-started) 
+ <span data-ttu-id="9bb98-140">[Esempio di .NET SDK in GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="9bb98-140">[.NET SDK sample on Github](https://github.com/Azure-Samples/search-dotnet-getting-started).</span></span> <span data-ttu-id="9bb98-141">Questa soluzione include il progetto "DotNetEtagsExplainer" contenente il codice presentato in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="9bb98-141">This solution includes the "DotNetEtagsExplainer" project containing the code presented in this article.</span></span>

## <a name="see-also"></a><span data-ttu-id="9bb98-142">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9bb98-142">See also</span></span>

  <span data-ttu-id="9bb98-143">[Common HTTP request and response headers](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search)   (Intestazioni della risposta e della richiesta HTTP comuni)</span><span class="sxs-lookup"><span data-stu-id="9bb98-143">[Common HTTP request and response headers](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search)  </span></span>  
  <span data-ttu-id="9bb98-144">[HTTP status codes](https://docs.microsoft.com/rest/api/searchservice/http-status-codes) (Codici di stato HTTP) [Index operations (REST API)](https://docs.microsoft.com/\rest/api/searchservice/index-operations) (Operazioni sugli indici - API REST)</span><span class="sxs-lookup"><span data-stu-id="9bb98-144">[HTTP status codes](https://docs.microsoft.com/rest/api/searchservice/http-status-codes) [Index operations (REST API)](https://docs.microsoft.com/\rest/api/searchservice/index-operations)</span></span>