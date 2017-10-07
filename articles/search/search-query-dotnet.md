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
# <a name="query-your-azure-search-index-using-hello-net-sdk"></a>L'indice di ricerca di Azure utilizzando hello SDK .NET di query
> [!div class="op_single_selector"]
> * [Panoramica](search-query-overview.md)
> * [Portale](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
> 
> 

In questo articolo verrà illustrato come un indice utilizzando tooquery hello [Azure Search .NET SDK](https://aka.ms/search-sdk).

Prima di iniziare questa procedura dettagliata, è necessario avere [creato un indice di Ricerca di Azure](search-what-is-an-index.md) e [averlo popolato con dati](search-what-is-data-import.md).

> [!NOTE]
> Tutto il codice di esempio in questo articolo è scritto in C#. È possibile trovare il codice sorgente completo hello [su GitHub](http://aka.ms/search-dotnet-howto). È inoltre possibile leggere sulla hello [Azure Search .NET SDK](search-howto-dotnet-sdk.md) per una più dettagliata procedura hello del codice di esempio.

## <a name="identify-your-azure-search-services-query-api-key"></a>Identificare la chiave API di query del servizio Ricerca di Azure
Ora che è stato creato un indice di ricerca di Azure, si è quasi pronto tooissue query utilizzando hello .NET SDK. In primo luogo, è necessario tooobtain uno dei hello chiavi api di query che è stato generato per il servizio di ricerca hello che è effettuato il provisioning. Hello .NET SDK invierà questa chiave api nel servizio di tooyour ogni richiesta. Disporre di una chiave valida stabilisce relazioni di trust, un singolo per ogni richiesta, tra hello invio hello richiesta e il servizio di hello che la gestisce.

1. toofind chiavi di api del servizio è possibile accedere toohello [portale di Azure](https://portal.azure.com/)
2. Pannello del servizio di ricerca di Azure andare tooyour
3. Fare clic su hello icona "Chiavi"

Il servizio avrà *chiavi amministratore* e *chiavi di query*.

* Il database primario e secondario *chiavi amministratore* concedere diritti completi tooall operazioni, incluso hello possibilità toomanage hello servizio, creare ed eliminare origini di dati, gli indicizzatori e gli indici. Esistono due chiavi in modo che sia possibile continuare chiave secondaria di hello toouse se si decide di tooregenerate hello primary key e viceversa.
* Il *query chiavi* concedere l'accesso in sola lettura tooindexes e documenti e sono in genere distribuite tooclient applicazioni che inviano richieste di ricerca.

Ai fini di hello di query nell'indice, è possibile utilizzare una delle chiavi di query. Le chiavi amministratore utilizzabile anche per le query, ma è necessario usare una chiave di query nel codice dell'applicazione, come segue meglio hello [principio di privilegio minimo](https://en.wikipedia.org/wiki/Principle_of_least_privilege).

## <a name="create-an-instance-of-hello-searchindexclient-class"></a>Creare un'istanza della classe SearchIndexClient hello
query tooissue con hello Azure Search .NET SDK, sarà necessario toocreate un'istanza di hello `SearchIndexClient` classe. Questa classe ha diversi costruttori. Hello quello desiderato accetta il nome del servizio di ricerca, il nome dell'indice e un `SearchCredentials` oggetto come parametri. `SearchCredentials` esegue il wrapping della chiave API.

Crea un nuovo codice Hello riportato di seguito `SearchIndexClient` per l'indice "Hotel" hello (creato in [creare un indice di ricerca di Azure mediante .NET SDK hello](search-create-index-dotnet.md)) utilizzando i valori per nome del servizio ricerca hello e la chiave api che vengono archiviati nel file di configurazione dell'applicazione hello file (`appsettings.json` nel caso di hello di hello [applicazione di esempio](http://aka.ms/search-dotnet-howto)):

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

`SearchIndexClient` include una proprietà `Documents`. Questa proprietà fornisce che tutti hello metodi che è necessario tooquery gli indici di ricerca di Azure.

## <a name="query-your-index"></a>Eseguire query sull'indice
Ricerca con .NET SDK hello è semplice come chiamata hello `Documents.Search` metodo i `SearchIndexClient`. Questo metodo accetta alcuni parametri, incluso il testo di ricerca hello, insieme a un `SearchParameters` oggetto che può essere utilizzato toofurther rifinire hello query.

#### <a name="types-of-queries"></a>Tipi di query
main Hello due [tipi di query](search-query-overview.md#types-of-queries) si utilizzerà sono `search` e `filter`. Una query `search` esegue la ricerca di uno o più termini in tutti i campi *ricercabile* nell'indice. Una query `filter` valuta un'espressione booleana su tutti i campi *filtrabili* di un indice.

Le ricerche e i filtri vengono eseguiti hello `Documents.Search` metodo. Una query di ricerca può essere passata in hello `searchText` parametro, mentre un'espressione di filtro può essere passata in hello `Filter` proprietà di hello `SearchParameters` classe. toofilter senza eseguire ricerche, è sufficiente passare `"*"` per hello `searchText` parametro. toosearch senza filtri, lasciare hello `Filter` proprietà non è impostato, oppure non passare un `SearchParameters` istanza affatto.

#### <a name="example-queries"></a>Query di esempio
Hello codice di esempio seguente mostra alcuni modi tooquery hello "Hotel" indice definito in [creare un indice di ricerca di Azure mediante .NET SDK hello](search-create-index-dotnet.md#DefineIndex). Si noti che i documenti hello restituiti con i risultati della ricerca hello sono istanze di hello `Hotel` (classe), che è stato definito in [hello di importazione dei dati in ricerca di Azure mediante .NET SDK](search-import-data-dotnet.md#HotelClass). esempio di codice Hello si avvalgono di un `WriteDocuments` console toohello di metodo toooutput hello ricerca risultati. Questo metodo è descritto nella sezione successiva hello.

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

## <a name="handle-search-results"></a>Gestire i risultati della ricerca
Hello `Documents.Search` metodo restituisce un `DocumentSearchResult` oggetto che contiene i risultati della query hello hello. esempio Hello nella sezione precedente hello utilizzato un metodo denominato `WriteDocuments` console toohello di toooutput hello ricerca risultati:

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

Risultati hello un aspetto simile per le query hello nella sezione precedente di hello, presumendo un indice di hotel"hello" viene popolato con i dati di esempio hello in [hello di importazione dei dati in ricerca di Azure mediante .NET SDK](search-import-data-dotnet.md):

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

Hello esempio di codice precedente utilizza i risultati della ricerca toooutput console hello. Allo stesso modo, sarà necessario toodisplay i risultati della ricerca nella propria applicazione. Vedere [in questo esempio in GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample) per un esempio di come risultati della ricerca toorender in un'applicazione web basata su ASP.NET MVC.

