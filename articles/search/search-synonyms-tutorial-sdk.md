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
# <a name="synonym-preview-c-tutorial-for-azure-search"></a>Esercitazione sui sinonimi (anteprima) in C# per Ricerca di Azure

Sinonimi espandere una query di corrispondenza in base alle esigenze considerato come termine di input toohello semanticamente equivalente. Ad esempio, è consigliabile che documenti toomatch "car" che contiene termini di hello "automobile" o "vehicle".

In Ricerca di Azure i sinonimi sono definiti in una *mappa di sinonimi* tramite *regole di mapping* che associano termini equivalenti. È possibile creare più mappe sinonimo, registrarli come indice tooany disponibile la risorsa a livello di servizio e quindi fare riferimento quali uno toouse a livello di campo hello. In fase di query inoltre toosearching un indice, ricerca di Azure effettua una ricerca in una mappa del sinonimo, se ne è stato specificato nei campi utilizzati nella query hello.

> [!NOTE]
> sinonimi Hello funzionalità è attualmente in anteprima e solo supportati in hello anteprima più recente di API e le versioni SDK (api-version = 2016-09-01-Preview, anteprima di SDK versione 4. x). Non è attualmente disponibile alcun supporto nel portale di Azure. Le API disponibili in anteprima non rientrano nel Contratto di servizio e le funzionalità disponibili in anteprima possono subire modifiche, quindi non è consigliabile usarle nelle applicazioni di produzione.

## <a name="prerequisites"></a>Prerequisiti

Requisiti dell'esercitazione includono hello informazioni seguenti:

* [Visual Studio](https://www.visualstudio.com/downloads/)
* [Servizio Ricerca di Azure](search-create-service-portal.md)
* [Versione di anteprima della libreria Microsoft.Azure.Search .NET](https://aka.ms/search-sdk-preview)
* [La modalità di ricerca di Azure toouse da un'applicazione .NET](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk)

## <a name="overview"></a>Panoramica

Query di prima e dopo illustrano valore hello di sinonimi. In questa esercitazione viene usata un'applicazione di esempio che esegue query e restituisce risultati in un indice di esempio. applicazione di esempio Hello crea un indice di dimensioni ridotte denominato "Hotel" popolato con i due documenti. un'applicazione Hello esegue query di ricerca mediante i termini e le frasi che non sono presenti nell'indice hello, funzionalità hello sinonimi, quindi problemi hello ricerche stesso nuovamente. codice Hello riportato di seguito viene illustrato hello flusso globale.

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
Hello toocreate passaggi e popolare l'indice di esempio hello vengono spiegate in [come toouse ricerca di Azure da un'applicazione .NET](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).

## <a name="before-queries"></a>Query di tipo "prima"

In `RunQueriesWithNonExistentTermsInIndex` vengono eseguite query di ricerca con i termini "five star", "internet" ed "economy AND hotel".
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
Nessuno dei documenti indicizzati due hello contengono termini di hello, per esempio hello prima di tutto l'output di hello `RunQueriesWithNonExistentTermsInIndex`.
~~~
Search hello entire index for hello phrase "five star":

no document matched

Search hello entire index for hello term 'internet':

no document matched

Search hello entire index for hello terms 'economy' AND 'hotel':

no document matched
~~~

## <a name="enable-synonyms"></a>Abilitare i sinonimi

L'abilitazione dei sinonimi è un processo in due passaggi. È innanzitutto definire e caricare le regole di sinonimo e quindi configurare i campi toouse li. il processo di Hello è descritto in `UploadSynonyms` e `EnableSynonymsInHotelsIndex`.

1. Aggiungere un servizio di ricerca tooyour mappa sinonimo. In `UploadSynonyms`, si definiscono quattro regole nella mappa di sinonimo 'desc synonymmap' e toohello servizio di caricamento.
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
Una mappa di sinonimo deve essere conforme a standard di origine aprire toohello `solr` formato. viene illustrato il formato di Hello in [sinonimi in ricerca di Azure](search-synonyms.md) nella sezione hello `Apache Solr synonym format`.

2. Configurare i campi ricercabili toouse hello sinonimo mappa nella definizione dell'indice hello. In `EnableSynonymsInHotelsIndex`, si abilita sinonimi due campi `category` e `tags` dall'impostazione hello `synonymMaps` toohello nome della proprietà di hello appena caricato mappa sinonimo.
```csharp
  Index index = serviceClient.Indexes.Get("hotels");
  index.Fields.First(f => f.Name == "category").SynonymMaps = new[] { "desc-synonymmap" };
  index.Fields.First(f => f.Name == "tags").SynonymMaps = new[] { "desc-synonymmap" };

  serviceClient.Indexes.CreateOrUpdate(index);
```
Quando si aggiunge una mappa di sinonimi, non è necessario ricompilare l'indice. È possibile aggiungere un servizio di tooyour sinonimo mappa e quindi modificare le definizioni di campo esistente in qualsiasi indice toouse hello nuovo sinonimo mapping. aggiunta di Hello di nuovi attributi non ha alcun impatto sulla disponibilità di indice. Ciò vale anche la disabilitazione di sinonimi per un campo di Hello. È possibile impostare semplicemente hello `synonymMaps` elenco di proprietà tooan vuoto.
```csharp
  index.Fields.First(f => f.Name == "category").SynonymMaps = new List<string>();
```

## <a name="after-queries"></a>Query di tipo "dopo"

Dopo la mappa di sinonimo hello viene caricata e indice hello è mappa sinonimo di hello toouse aggiornato, hello secondo `RunQueriesWithNonExistentTermsInIndex` chiamata genera seguente hello:

~~~
Search hello entire index for hello phrase "five star":

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search hello entire index for hello term 'internet':

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search hello entire index for hello terms 'economy' AND 'hotel':

Name: Roach Motel       Category: Budget        Tags: [motel, budget]
~~~
prima query Hello trova hello documento dalla regola hello `five star=>luxury`. seconda query Hello espande hello ricerca tramite `internet,wifi` e hello terzo utilizzando sia `hotel, motel` e `economy,inexpensive=>budget` nella ricerca di documenti hello di corrispondenza con.

Aggiunta di sinonimi completamente modifica hello un'esperienza di ricerca. In questa esercitazione, query originale hello Impossibile risultati significativi tooreturn anche se erano rilevanti documenti hello nel nostro indice. Abilitando i sinonimi, è possibile espandere un tooinclude indice termini di uso comune, senza dati toounderlying modifiche nell'indice hello.

## <a name="sample-application-source-code"></a>Esempio di codice sorgente dell'applicazione
È possibile trovare il codice sorgente completo hello dell'applicazione di esempio hello utilizzato in questa procedura dettagliata su [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms).

## <a name="next-steps"></a>Passaggi successivi

* Revisione [come sinonimi toouse in ricerca di Azure](search-synonyms.md)
* Vedere [Synonyms REST API documentation](https://aka.ms/rgm6rq) (Documentazione sull'API REST Synonyms)
* Individuare i riferimenti di hello per hello [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) e [API REST](https://docs.microsoft.com/rest/api/searchservice/).
