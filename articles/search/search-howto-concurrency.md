---
title: toomanage aaaHow simultanee scrive tooresources in ricerca di Azure
description: Utilizzare conflitti di concorrenza ottimistica tooavoid aria intermedio gli indici di ricerca tooAzure aggiornamenti o eliminazioni, gli indicizzatori, origini dati.
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
ms.openlocfilehash: c061d2b5c4d2dbd0fd5633405b01ab2912fbc754
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-concurrency-in-azure-search"></a><span data-ttu-id="16bfa-103">Modalità concorrenza toomanage in ricerca di Azure</span><span class="sxs-lookup"><span data-stu-id="16bfa-103">How toomanage concurrency in Azure Search</span></span>

<span data-ttu-id="16bfa-104">Quando la gestione delle risorse di ricerca di Azure, ad esempio indici e le origini dati, è importante tooupdate risorse in modo sicuro, soprattutto se le risorse sono accedere contemporaneamente da diversi componenti dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="16bfa-104">When managing Azure Search resources such as indexes and data sources, it's important tooupdate resources safely, especially if resources are accessed concurrently by different components of your application.</span></span> <span data-ttu-id="16bfa-105">Quando due client aggiornano simultaneamente un risorsa senza coordinazione, si possono verificare race condition.</span><span class="sxs-lookup"><span data-stu-id="16bfa-105">When two clients concurrently update a resource without coordination, race conditions are possible.</span></span> <span data-ttu-id="16bfa-106">tooprevent, offerte di ricerca di Azure un *modello di concorrenza ottimistica*.</span><span class="sxs-lookup"><span data-stu-id="16bfa-106">tooprevent this, Azure Search offers an *optimistic concurrency model*.</span></span> <span data-ttu-id="16bfa-107">Non sono presenti blocchi su una risorsa,</span><span class="sxs-lookup"><span data-stu-id="16bfa-107">There are no locks on a resource.</span></span> <span data-ttu-id="16bfa-108">In alternativa, è un valore ETag per sovrascrive tutte le risorse che identifica la versione di risorsa hello in modo che è possibile elaborare le richieste che evitare accidentale.</span><span class="sxs-lookup"><span data-stu-id="16bfa-108">Instead, there is an ETag for every resource that identifies hello resource version so that you can craft requests that avoid accidental overwrites.</span></span>

> [!Tip]
> <span data-ttu-id="16bfa-109">Il codice concettuale in una [soluzione C# di esempio](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer) illustra come funziona il controllo della concorrenza in Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="16bfa-109">Conceptual code in a [sample C# solution](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer) explains how concurrency control works in Azure Search.</span></span> <span data-ttu-id="16bfa-110">codice Hello crea le condizioni che richiamano il controllo della concorrenza.</span><span class="sxs-lookup"><span data-stu-id="16bfa-110">hello code creates conditions that invoke concurrency control.</span></span> <span data-ttu-id="16bfa-111">Hello lettura [frammento di codice riportato di seguito](#samplecode) è probabilmente sufficiente per la maggior parte degli sviluppatori, ma se si desidera toorun, nome del servizio modifica appSettings. JSON tooadd hello e una chiave api di amministrazione.</span><span class="sxs-lookup"><span data-stu-id="16bfa-111">Reading hello [code fragment below](#samplecode) is probably sufficient for most developers, but if you want toorun it, edit appsettings.json tooadd hello service name and an admin api-key.</span></span> <span data-ttu-id="16bfa-112">Dato un URL del servizio di `http://myservice.search.windows.net`, nome del servizio hello è `myservice`.</span><span class="sxs-lookup"><span data-stu-id="16bfa-112">Given a service URL of `http://myservice.search.windows.net`, hello service name is `myservice`.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="16bfa-113">Funzionamento</span><span class="sxs-lookup"><span data-stu-id="16bfa-113">How it works</span></span>

<span data-ttu-id="16bfa-114">Viene implementata la concorrenza ottimistica tramite accesso condizione controlla nelle chiamate API scrittura tooindexes, gli indicizzatori, origini dati e risorse synonymMap.</span><span class="sxs-lookup"><span data-stu-id="16bfa-114">Optimistic concurrency is implemented through access condition checks in API calls writing tooindexes, indexers, datasources, and synonymMap resources.</span></span> 

<span data-ttu-id="16bfa-115">Tutte le risorse hanno un [*tag di entità (ETag)*](https://en.wikipedia.org/wiki/HTTP_ETag) che fornisce informazioni sulla versione dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="16bfa-115">All resources have an [*entity tag (ETag)*](https://en.wikipedia.org/wiki/HTTP_ETag) that provides object version information.</span></span> <span data-ttu-id="16bfa-116">Controllando innanzitutto hello ETag, è possibile evitare aggiornamenti simultanei in un flusso di lavoro tipico (ottenere, modificare localmente, aggiornare) assicurando corrispondenze ETag della risorsa hello la copia locale.</span><span class="sxs-lookup"><span data-stu-id="16bfa-116">By checking hello ETag first, you can avoid concurrent updates in a typical workflow (get, modify locally, update) by ensuring hello resource's ETag matches your local copy.</span></span> 

+ <span data-ttu-id="16bfa-117">Hello REST API utilizza un [ETag](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) nell'intestazione della richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="16bfa-117">hello REST API uses an [ETag](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) on hello request header.</span></span>
+ <span data-ttu-id="16bfa-118">Hello .NET SDK imposta hello ETag tramite un oggetto accessCondition, impostazione hello [If-Match | Intestazione If-Match-Nessuno](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) sulla risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="16bfa-118">hello .NET SDK sets hello ETag through an accessCondition object, setting hello [If-Match | If-Match-None header](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) on hello resource.</span></span> <span data-ttu-id="16bfa-119">Tutti gli oggetti che ereditano da [IResourceWithETag (.NET SDK)](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.iresourcewithetag) hanno un oggetto accessCondition.</span><span class="sxs-lookup"><span data-stu-id="16bfa-119">Any object inheriting from [IResourceWithETag (.NET SDK)](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.iresourcewithetag) has an accessCondition object.</span></span>

<span data-ttu-id="16bfa-120">Ogni volta che si aggiorna una risorsa, l'ETag cambia automaticamente.</span><span class="sxs-lookup"><span data-stu-id="16bfa-120">Every time you update a resource, its ETag changes automatically.</span></span> <span data-ttu-id="16bfa-121">Quando si implementa la gestione della concorrenza, tutto si sta eseguendo è l'inserimento di una precondizione su richiesta di aggiornamento hello che richiede una risorsa remota hello toohave hello ETag stesso come copia di hello della risorsa hello che è stato modificato in client hello.</span><span class="sxs-lookup"><span data-stu-id="16bfa-121">When you implement concurrency management, all you're doing is putting a precondition on hello update request that requires hello remote resource toohave hello same ETag as hello copy of hello resource that you modified on hello client.</span></span> <span data-ttu-id="16bfa-122">Se un processo simultaneo risorsa remota hello è già stato modificato, hello ETag non corrisponderanno precondizione hello e richiesta hello avrà esito negativo con HTTP 412.</span><span class="sxs-lookup"><span data-stu-id="16bfa-122">If a concurrent process has changed hello remote resource already, hello ETag will not match hello precondition and hello request will fail with HTTP 412.</span></span> <span data-ttu-id="16bfa-123">Se si usa hello .NET SDK, questa situazione si manifesta come una `CloudException` dove hello `IsAccessConditionFailed()` metodo di estensione restituisce true.</span><span class="sxs-lookup"><span data-stu-id="16bfa-123">If you're using hello .NET SDK, this manifests as a `CloudException` where hello `IsAccessConditionFailed()` extension method returns true.</span></span>

> [!Note]
> <span data-ttu-id="16bfa-124">Esiste un solo meccanismo per la concorrenza,</span><span class="sxs-lookup"><span data-stu-id="16bfa-124">There is only one mechanism for concurrency.</span></span> <span data-ttu-id="16bfa-125">che viene sempre usato indipendentemente dall'API usata per gli aggiornamenti delle risorse.</span><span class="sxs-lookup"><span data-stu-id="16bfa-125">It's always used regardless of which API is used for resource updates.</span></span> 

<a name="samplecode"></a>
## <a name="use-cases-and-sample-code"></a><span data-ttu-id="16bfa-126">Casi d'uso e codici di esempio</span><span class="sxs-lookup"><span data-stu-id="16bfa-126">Use cases and sample code</span></span>

<span data-ttu-id="16bfa-127">Hello di codice seguente viene illustrato come accessCondition verifica la presenza di operazioni di aggiornamento della chiave:</span><span class="sxs-lookup"><span data-stu-id="16bfa-127">hello following code demonstrates accessCondition checks for key update operations:</span></span>

+ <span data-ttu-id="16bfa-128">Esito negativo di un aggiornamento se la risorsa hello non esiste più</span><span class="sxs-lookup"><span data-stu-id="16bfa-128">Fail an update if hello resource no longer exists</span></span>
+ <span data-ttu-id="16bfa-129">Esito negativo di un aggiornamento se modifica della versione di hello risorsa</span><span class="sxs-lookup"><span data-stu-id="16bfa-129">Fail an update if hello resource version changes</span></span>

### <a name="sample-code-from-dotnetetagsexplainer-programhttpsgithubcomazure-samplessearch-dotnet-getting-startedtreemasterdotnetetagsexplainer"></a><span data-ttu-id="16bfa-130">Codice di esempio dal [programma DotNetETagsExplainer](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer)</span><span class="sxs-lookup"><span data-stu-id="16bfa-130">Sample code from [DotNetETagsExplainer program](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer)</span></span>

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
            // of hello resource you're working on. When you first create a resource such as an index, its ETag is
            // empty.
            Index index = DefineTestIndex();
            Console.WriteLine(
                $"Test index hasn't been created yet, so its ETag should be blank. ETag: '{index.ETag}'");

            // Once hello resource exists in Azure Search, its ETag will be populated. Make sure toouse hello object
            // returned by hello SearchServiceClient! Otherwise, you will still have hello old object with the
            // blank ETag.
            Console.WriteLine("Creating index...\n");
            index = serviceClient.Indexes.Create(index);
            
            Console.WriteLine($"Test index created; Its ETag should be populated. ETag: '{index.ETag}'");

            // ETags let you do some useful things you couldn't do otherwise. For example, by using an If-Match
            // condition, we can update an index using CreateOrUpdate and be guaranteed that hello update will only
            // succeed if hello index already exists.
            index.Fields.Add(new Field("name", AnalyzerName.EnMicrosoft));
            index =
                serviceClient.Indexes.CreateOrUpdate(
                    index,
                    accessCondition: AccessCondition.GenerateIfExistsCondition());

            Console.WriteLine(
                $"Test index updated; Its ETag should have changed since it was created. ETag: '{index.ETag}'");

            // More importantly, ETags protect you from concurrent updates toohello same resource. If another
            // client tries tooupdate hello resource, it will fail as long as all clients are using hello right
            // access conditions.
            Index indexForClient1 = index;
            Index indexForClient2 = serviceClient.Indexes.Get("test");

            Console.WriteLine("Simulating concurrent update. toostart, both clients see hello same ETag.");
            Console.WriteLine($"Client 1 ETag: '{indexForClient1.ETag}' Client 2 ETag: '{indexForClient2.ETag}'");

            // Client 1 successfully updates hello index.
            indexForClient1.Fields.Add(new Field("a", DataType.Int32));
            indexForClient1 =
                serviceClient.Indexes.CreateOrUpdate(
                    indexForClient1,
                    accessCondition: AccessCondition.IfNotChanged(indexForClient1));

            Console.WriteLine($"Test index updated by client 1; ETag: '{indexForClient1.ETag}'");

            // Client 2 tries tooupdate hello index, but fails, thanks toohello ETag check.
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
                Console.WriteLine("Client 2 failed tooupdate hello index, as expected.");
            }

            // You can also use access conditions with Delete operations. For example, you can implement an
            // atomic version of hello DeleteTestIndexIfExists method from this sample like this:
            Console.WriteLine("Deleting index...\n");
            serviceClient.Indexes.Delete("test", accessCondition: AccessCondition.GenerateIfExistsCondition());

            // This is slightly better than using hello Exists method since it makes only one round trip to
            // Azure Search instead of potentially two. It also avoids an extra Delete request in cases where
            // hello resource is deleted concurrently, but this doesn't matter much since resource deletion in
            // Azure Search is idempotent.

            // And we're done! Bye!
            Console.WriteLine("Complete.  Press any key tooend application...\n");
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

## <a name="design-pattern"></a><span data-ttu-id="16bfa-131">Schema progettuale</span><span class="sxs-lookup"><span data-stu-id="16bfa-131">Design pattern</span></span>

<span data-ttu-id="16bfa-132">Un modello di progettazione per l'implementazione della concorrenza ottimistica deve includere un ciclo di tentativi di verifica della condizione accesso hello, un test per la condizione di accesso, hello e facoltativamente recupera una risorsa aggiornata prima di tentare di toore-hello applicarle.</span><span class="sxs-lookup"><span data-stu-id="16bfa-132">A design pattern for implementing optimistic concurrency should include a loop that retries hello access condition check, a test for hello access condition, and optionally retrieves an updated resource before attempting toore-apply hello changes.</span></span> 

<span data-ttu-id="16bfa-133">Frammento di codice seguente viene illustrato inoltre hello di un indice tooan synonymMap già esistente.</span><span class="sxs-lookup"><span data-stu-id="16bfa-133">This code snippet illustrates hello addition of a synonymMap tooan index that already exists.</span></span> <span data-ttu-id="16bfa-134">Questo codice è tratto hello [esercitazione c# sinonimo (anteprima) per la ricerca di Azure](https://docs.microsoft.com/azure/search/search-synonyms-tutorial-sdk).</span><span class="sxs-lookup"><span data-stu-id="16bfa-134">This code is from hello [Synonym (preview) C# tutorial for Azure Search](https://docs.microsoft.com/azure/search/search-synonyms-tutorial-sdk).</span></span> 

<span data-ttu-id="16bfa-135">frammento di codice Hello Ottiene indice hotel"hello", controlla versione dell'oggetto hello in un'operazione di aggiornamento, viene generata un'eccezione se la condizione hello ha esito negativo e quindi tentativi hello operazione (i tempi di toothree), a partire da indice il recupero da hello tooget di hello server più recente Versione.</span><span class="sxs-lookup"><span data-stu-id="16bfa-135">hello snippet gets hello "hotels" index, checks hello object version on an update operation, throws an exception if hello condition fails, and then retries hello operation (up toothree times), starting with index retrieval from hello server tooget hello latest version.</span></span>

        private static void EnableSynonymsInHotelsIndexSafely(SearchServiceClient serviceClient)
        {
            int MaxNumTries = 3;

            for (int i = 0; i < MaxNumTries; ++i)
            {
                try
                {
                    Index index = serviceClient.Indexes.Get("hotels");
                    index = AddSynonymMapsToFields(index);

                    // hello IfNotChanged condition ensures that hello index is updated only if hello ETags match.
                    serviceClient.Indexes.CreateOrUpdate(index, accessCondition: AccessCondition.IfNotChanged(index));

                    Console.WriteLine("Updated hello index successfully.\n");
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


## <a name="next-steps"></a><span data-ttu-id="16bfa-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="16bfa-136">Next steps</span></span>

<span data-ttu-id="16bfa-137">Hello revisione [esempio sinonimi c#](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms) per ulteriori informazioni di contesto in modalità toosafely aggiornare un indice esistente.</span><span class="sxs-lookup"><span data-stu-id="16bfa-137">Review hello [synonyms C# sample](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms) for more context on how toosafely update an existing index.</span></span>

<span data-ttu-id="16bfa-138">Provare a modificare uno dei seguenti hello esempi tooinclude ETag o AccessCondition oggetti.</span><span class="sxs-lookup"><span data-stu-id="16bfa-138">Try modifying either of hello following samples tooinclude ETags or AccessCondition objects.</span></span>

+ [<span data-ttu-id="16bfa-139">Esempio di API REST in GitHub</span><span class="sxs-lookup"><span data-stu-id="16bfa-139">REST API sample on Github</span></span>](https://github.com/Azure-Samples/search-rest-api-getting-started) 
+ <span data-ttu-id="16bfa-140">[Esempio di .NET SDK in GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="16bfa-140">[.NET SDK sample on Github](https://github.com/Azure-Samples/search-dotnet-getting-started).</span></span> <span data-ttu-id="16bfa-141">Questa soluzione include progetti "DotNetEtagsExplainer" hello contenente codice hello presentato in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="16bfa-141">This solution includes hello "DotNetEtagsExplainer" project containing hello code presented in this article.</span></span>

## <a name="see-also"></a><span data-ttu-id="16bfa-142">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="16bfa-142">See also</span></span>

  <span data-ttu-id="16bfa-143">[Common HTTP request and response headers](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search)   (Intestazioni della risposta e della richiesta HTTP comuni)</span><span class="sxs-lookup"><span data-stu-id="16bfa-143">[Common HTTP request and response headers](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search)  </span></span>  
  <span data-ttu-id="16bfa-144">[HTTP status codes](https://docs.microsoft.com/rest/api/searchservice/http-status-codes) (Codici di stato HTTP) [Index operations (REST API)](https://docs.microsoft.com/\rest/api/searchservice/index-operations) (Operazioni sugli indici - API REST)</span><span class="sxs-lookup"><span data-stu-id="16bfa-144">[HTTP status codes](https://docs.microsoft.com/rest/api/searchservice/http-status-codes) [Index operations (REST API)](https://docs.microsoft.com/\rest/api/searchservice/index-operations)</span></span>