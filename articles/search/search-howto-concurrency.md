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
# <a name="how-toomanage-concurrency-in-azure-search"></a>Modalità concorrenza toomanage in ricerca di Azure

Quando la gestione delle risorse di ricerca di Azure, ad esempio indici e le origini dati, è importante tooupdate risorse in modo sicuro, soprattutto se le risorse sono accedere contemporaneamente da diversi componenti dell'applicazione. Quando due client aggiornano simultaneamente un risorsa senza coordinazione, si possono verificare race condition. tooprevent, offerte di ricerca di Azure un *modello di concorrenza ottimistica*. Non sono presenti blocchi su una risorsa, In alternativa, è un valore ETag per sovrascrive tutte le risorse che identifica la versione di risorsa hello in modo che è possibile elaborare le richieste che evitare accidentale.

> [!Tip]
> Il codice concettuale in una [soluzione C# di esempio](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer) illustra come funziona il controllo della concorrenza in Ricerca di Azure. codice Hello crea le condizioni che richiamano il controllo della concorrenza. Hello lettura [frammento di codice riportato di seguito](#samplecode) è probabilmente sufficiente per la maggior parte degli sviluppatori, ma se si desidera toorun, nome del servizio modifica appSettings. JSON tooadd hello e una chiave api di amministrazione. Dato un URL del servizio di `http://myservice.search.windows.net`, nome del servizio hello è `myservice`.

## <a name="how-it-works"></a>Funzionamento

Viene implementata la concorrenza ottimistica tramite accesso condizione controlla nelle chiamate API scrittura tooindexes, gli indicizzatori, origini dati e risorse synonymMap. 

Tutte le risorse hanno un [*tag di entità (ETag)*](https://en.wikipedia.org/wiki/HTTP_ETag) che fornisce informazioni sulla versione dell'oggetto. Controllando innanzitutto hello ETag, è possibile evitare aggiornamenti simultanei in un flusso di lavoro tipico (ottenere, modificare localmente, aggiornare) assicurando corrispondenze ETag della risorsa hello la copia locale. 

+ Hello REST API utilizza un [ETag](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) nell'intestazione della richiesta hello.
+ Hello .NET SDK imposta hello ETag tramite un oggetto accessCondition, impostazione hello [If-Match | Intestazione If-Match-Nessuno](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) sulla risorsa hello. Tutti gli oggetti che ereditano da [IResourceWithETag (.NET SDK)](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.iresourcewithetag) hanno un oggetto accessCondition.

Ogni volta che si aggiorna una risorsa, l'ETag cambia automaticamente. Quando si implementa la gestione della concorrenza, tutto si sta eseguendo è l'inserimento di una precondizione su richiesta di aggiornamento hello che richiede una risorsa remota hello toohave hello ETag stesso come copia di hello della risorsa hello che è stato modificato in client hello. Se un processo simultaneo risorsa remota hello è già stato modificato, hello ETag non corrisponderanno precondizione hello e richiesta hello avrà esito negativo con HTTP 412. Se si usa hello .NET SDK, questa situazione si manifesta come una `CloudException` dove hello `IsAccessConditionFailed()` metodo di estensione restituisce true.

> [!Note]
> Esiste un solo meccanismo per la concorrenza, che viene sempre usato indipendentemente dall'API usata per gli aggiornamenti delle risorse. 

<a name="samplecode"></a>
## <a name="use-cases-and-sample-code"></a>Casi d'uso e codici di esempio

Hello di codice seguente viene illustrato come accessCondition verifica la presenza di operazioni di aggiornamento della chiave:

+ Esito negativo di un aggiornamento se la risorsa hello non esiste più
+ Esito negativo di un aggiornamento se modifica della versione di hello risorsa

### <a name="sample-code-from-dotnetetagsexplainer-programhttpsgithubcomazure-samplessearch-dotnet-getting-startedtreemasterdotnetetagsexplainer"></a>Codice di esempio dal [programma DotNetETagsExplainer](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer)

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

## <a name="design-pattern"></a>Schema progettuale

Un modello di progettazione per l'implementazione della concorrenza ottimistica deve includere un ciclo di tentativi di verifica della condizione accesso hello, un test per la condizione di accesso, hello e facoltativamente recupera una risorsa aggiornata prima di tentare di toore-hello applicarle. 

Frammento di codice seguente viene illustrato inoltre hello di un indice tooan synonymMap già esistente. Questo codice è tratto hello [esercitazione c# sinonimo (anteprima) per la ricerca di Azure](https://docs.microsoft.com/azure/search/search-synonyms-tutorial-sdk). 

frammento di codice Hello Ottiene indice hotel"hello", controlla versione dell'oggetto hello in un'operazione di aggiornamento, viene generata un'eccezione se la condizione hello ha esito negativo e quindi tentativi hello operazione (i tempi di toothree), a partire da indice il recupero da hello tooget di hello server più recente Versione.

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


## <a name="next-steps"></a>Passaggi successivi

Hello revisione [esempio sinonimi c#](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms) per ulteriori informazioni di contesto in modalità toosafely aggiornare un indice esistente.

Provare a modificare uno dei seguenti hello esempi tooinclude ETag o AccessCondition oggetti.

+ [Esempio di API REST in GitHub](https://github.com/Azure-Samples/search-rest-api-getting-started) 
+ [Esempio di .NET SDK in GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started). Questa soluzione include progetti "DotNetEtagsExplainer" hello contenente codice hello presentato in questo articolo.

## <a name="see-also"></a>Vedere anche

  [Common HTTP request and response headers](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search)   (Intestazioni della risposta e della richiesta HTTP comuni)  
  [HTTP status codes](https://docs.microsoft.com/rest/api/searchservice/http-status-codes) (Codici di stato HTTP) [Index operations (REST API)](https://docs.microsoft.com/\rest/api/searchservice/index-operations) (Operazioni sugli indici - API REST)