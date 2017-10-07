---
title: aaaHow toouse ricerca di Azure da un'applicazione .NET | Documenti Microsoft
description: "La modalità di ricerca di Azure toouse da un'applicazione .NET"
services: search
documentationcenter: 
author: brjohnstmsft
manager: jlembicz
editor: 
ms.assetid: 93653341-c05f-4cfd-be45-bb877f964fcb
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/22/2017
ms.author: brjohnst
ms.openlocfilehash: 8e13fbe5549547d65941b856ce5a90611261388f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-search-from-a-net-application"></a>La modalità di ricerca di Azure toouse da un'applicazione .NET
Questo articolo è tooget una procedura dettagliata è attivo e in esecuzione con hello [Azure Search .NET SDK](https://aka.ms/search-sdk). È possibile utilizzare hello .NET SDK tooimplement un'avanzata esperienza di ricerca in un'applicazione con ricerca di Azure.

## <a name="whats-in-hello-azure-search-sdk"></a>Che cos'è hello ricerca di Azure SDK
Hello SDK è costituito da una libreria client, `Microsoft.Azure.Search`. Consente di toomanage gli indici e le origini dati, gli indicizzatori, nonché caricare e gestire documenti ed esecuzione di query, tutto senza dover toodeal con i dettagli di hello di HTTP e JSON.

libreria client Hello definisce classi come `Index`, `Field`, e `Document`, nonché operazioni quali `Indexes.Create` e `Documents.Search` su hello `SearchServiceClient` e `SearchIndexClient` classi. Queste classi sono organizzate in hello spazi dei nomi seguenti:

* [Microsoft.Azure.Search](https://docs.microsoft.com/dotnet/api/microsoft.azure.search)
* [Microsoft.Azure.Search.Models](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models)

versione corrente di Hello di hello Azure Search .NET SDK è ora disponibile a livello generale. Se si desidera tooprovide feedback per noi tooincorporate nella versione successiva di hello, visitare il nostro [pagina commenti e suggerimenti](https://feedback.azure.com/forums/263029-azure-search/).

Hello .NET SDK supporta la versione `2016-09-01` di hello [API REST di ricerca di Azure](https://docs.microsoft.com/rest/api/searchservice/). Questa versione include ora il supporto per gli analizzatori personalizzati, BLOB di Azure e l'Indicizzatore di tabelle di Azure. Le funzionalità di anteprima *non* parte di questa versione, quali il supporto per l'indicizzazione di file JSON e CSV, sono [anteprima](search-api-2015-02-28-preview.md) e disponibile tramite hello precedente [versione 2.0 per l'anteprima di hello .NET SDK ](https://aka.ms/search-sdk-preview).

Questo SDK non supporta [operazioni di gestione](https://docs.microsoft.com/rest/api/searchmanagement/), come la creazione e la scalabilità di servizi di ricerca e la gestione delle chiavi API. Se è necessario toomanage le risorse di ricerca da un'applicazione .NET, è possibile utilizzare hello [Azure Search .NET SDK di gestione](https://aka.ms/search-mgmt-sdk).

## <a name="upgrading-toohello-latest-version-of-hello-sdk"></a>L'aggiornamento più recente di hello SDK toohello
Se già in uso una versione precedente di hello Azure Search .NET SDK e si desidera tooupgrade toohello nuovo generalmente disponibili versione, [questo articolo](search-dotnet-sdk-migration.md) spiega come.

## <a name="requirements-for-hello-sdk"></a>Requisiti per hello SDK
1. Visual Studio 2017.
2. Un servizio di Ricerca di Azure. In hello toouse ordine SDK, sarà necessario nome hello del servizio e una o più chiavi API. [Creare un servizio nel portale di hello](search-create-service-portal.md) consentono di eseguire questi passaggi.
3. Scaricare hello Azure Search .NET SDK [pacchetto NuGet](http://www.nuget.org/packages/Microsoft.Azure.Search) utilizzando "Gestisci pacchetti NuGet" in Visual Studio. Solo la ricerca per nome del pacchetto hello `Microsoft.Azure.Search` in NuGet.org.

Hello Azure Search .NET SDK supporta le applicazioni destinate a .NET Framework 4.6 hello e .NET Core.

## <a name="core-scenarios"></a>Scenari chiave
Ci sono vari aspetti, occorre toodo nell'applicazione di ricerca. In questa esercitazione saranno illustrati questi scenari chiave:

* Creazione di un indice
* La compilazione di indice hello con i documenti
* Ricerca di documenti mediante filtri e ricerca con testo completo

codice di esempio Hello che segue illustra ognuno di questi. Se i frammenti di codice hello toouse disponibile nell'applicazione.

### <a name="overview"></a>Panoramica
Hello è sarà possibile esplorare l'applicazione di esempio crea un nuovo indice denominato "Hotel", viene popolato con alcuni documenti, quindi esegue alcune query di ricerca. Ecco programma principale hello, che mostra hello flusso generale:

```csharp
// This sample shows how toodelete, create, upload documents and query an index
static void Main(string[] args)
{
    IConfigurationBuilder builder = new ConfigurationBuilder().AddJsonFile("appsettings.json");
    IConfigurationRoot configuration = builder.Build();

    SearchServiceClient serviceClient = CreateSearchServiceClient(configuration);

    Console.WriteLine("{0}", "Deleting index...\n");
    DeleteHotelsIndexIfExists(serviceClient);

    Console.WriteLine("{0}", "Creating index...\n");
    CreateHotelsIndex(serviceClient);

    ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");

    Console.WriteLine("{0}", "Uploading documents...\n");
    UploadDocuments(indexClient);

    ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

    RunQueries(indexClientForQueries);

    Console.WriteLine("{0}", "Complete.  Press any key tooend application...\n");
    Console.ReadKey();
}
```

> [!NOTE]
> È possibile trovare il codice sorgente completo hello dell'applicazione di esempio hello utilizzato in questa procedura dettagliata su [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).
> 
>

La procedura verrà illustrata passo per passo. È prima necessario toocreate un nuovo `SearchServiceClient`. Questo oggetto consente toomanage indici. In ordine tooconstruct uno, è necessario tooprovide il nome del servizio di ricerca di Azure, nonché una chiave API di amministrazione. È possibile immettere queste informazioni in hello `appsettings.json` file hello [applicazione di esempio](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).

```csharp
private static SearchServiceClient CreateSearchServiceClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string adminApiKey = configuration["SearchServiceAdminApiKey"];

    SearchServiceClient serviceClient = new SearchServiceClient(searchServiceName, new SearchCredentials(adminApiKey));
    return serviceClient;
}
```

> [!NOTE]
> Se si specifica una chiave non corretta (ad esempio, una chiave di query in cui una chiave amministratore è obbligatoria), hello `SearchServiceClient` genererà un `CloudException` con hello "Non consentito" messaggio di errore hello prima volta è chiamare un metodo dell'operazione, ad esempio `Indexes.Create`. In questo caso tooyou, verificare la chiave API.
> 
> 

Hello righe successive chiamare metodi toocreate un indice denominato "Hotel", l'eliminazione prima di tutto se esiste già. Tali metodi saranno illustrati più avanti.

```csharp
Console.WriteLine("{0}", "Deleting index...\n");
DeleteHotelsIndexIfExists(serviceClient);

Console.WriteLine("{0}", "Creating index...\n");
CreateHotelsIndex(serviceClient);
```

Successivamente, l'indice hello deve toobe popolato. toodo, è necessario un `SearchIndexClient`. Esistono due i modi tooobtain uno: costruendo, oppure chiamando `Indexes.GetClient` su hello `SearchServiceClient`. Utilizziamo hello quest'ultimo per praticità.

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> In un'applicazione di ricerca tipica, il popolamento e la gestione degli indici viene gestita da un componente separato dalle query di ricerca. `Indexes.GetClient`è utile per la compilazione di un indice perché si salva hello problemi di fornire un altro `SearchCredentials`. A tale scopo, passando la chiave di amministrazione hello hello toocreate utilizzati che si `SearchServiceClient` toohello nuova `SearchIndexClient`. Tuttavia, in parte dell'applicazione che esegue query hello è migliore hello toocreate `SearchIndexClient` direttamente in modo che è possibile passare una chiave di query anziché una chiave amministratore. Ciò è coerenza con il principio di hello dei privilegi minimi e aiutano toomake l'applicazione più sicura. È possibile trovare ulteriori informazioni su chiavi di amministrazione e chiavi di query [qui](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).
> 
> 

Ora che è disponibile un `SearchIndexClient`, è possibile popolare l'indice di hello. A tal fine verrà utilizzato un altro metodo che verrà descritto più avanti.

```csharp
Console.WriteLine("{0}", "Uploading documents...\n");
UploadDocuments(indexClient);
```

Infine, è eseguire alcune query di ricerca e visualizzare i risultati di hello. In questo caso viene utilizzato un `SearchIndexClient` diverso:

```csharp
ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

RunQueries(indexClientForQueries);
```

Verrà usato da vicino hello `RunQueries` metodo in un secondo momento. Ecco hello toocreate di codice hello nuovo `SearchIndexClient`:

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

In questo caso viene utilizzata una chiave di query perché non è necessario l'accesso in scrittura toohello indice. È possibile immettere queste informazioni in hello `appsettings.json` file hello [applicazione di esempio](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).

Se si esegue l'applicazione con un nome di servizio valido e le chiavi API, l'output di hello dovrebbe essere simile al seguente:

    Deleting index...
    
    Creating index...
    
    Uploading documents...
    
    Waiting for documents toobe indexed...
    
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
    
    Complete.  Press any key tooend application...

il codice sorgente completo Hello di un'applicazione hello viene fornito alla fine di hello di questo articolo.

Successivamente, verrà usato informazioni dettagliate su ciascuno dei metodi di hello chiamati da `Main`.

### <a name="creating-an-index"></a>Creazione di un indice
Dopo aver creato un `SearchServiceClient`, cosa Avanti hello `Main` does è indice di hotel"delete hello", se esiste già. Che viene eseguita al metodo hello:

```csharp
private static void DeleteHotelsIndexIfExists(SearchServiceClient serviceClient)
{
    if (serviceClient.Indexes.Exists("hotels"))
    {
        serviceClient.Indexes.Delete("hotels");
    }
}
```

Questo metodo utilizza hello dato `SearchServiceClient` toocheck se hello indice esistente e, in caso affermativo, eliminarlo.

> [!NOTE]
> codice di esempio Hello in questo articolo utilizza metodi sincroni di hello di hello Azure Search .NET SDK per motivi di semplicità. È consigliabile utilizzare i metodi asincroni hello nel proprio tookeep applicazioni scalabili e reattive. Ad esempio, in hello metodo sopra riportato è possibile utilizzare `ExistsAsync` e `DeleteAsync` anziché `Exists` e `Delete`.
> 
> 

Successivamente, `Main` crea un nuovo indice "hotel" chiamando questo metodo:

```csharp
private static void CreateHotelsIndex(SearchServiceClient serviceClient)
{
    var definition = new Index()
    {
        Name = "hotels",
        Fields = FieldBuilder.BuildForType<Hotel>()
    };

    serviceClient.Indexes.Create(definition);
}
```

Questo metodo crea un nuovo `Index` oggetto con un elenco di `Field` gli oggetti che definisce schema hello del nuovo indice hello. Ogni campo ha un nome, un tipo di dati e diversi attributi che definiscono il comportamento della ricerca. Hello `FieldBuilder` classe utilizza la reflection toocreate un elenco di `Field` oggetti per l'indice di hello esaminando hello proprietà pubbliche e gli attributi di base hello `Hotel` classe del modello. Ti guideremo vicino hello `Hotel` classe in un secondo momento.

> [!NOTE]
> È sempre possibile creare l'elenco di hello di `Field` oggetti direttamente anziché `FieldBuilder` se necessario. Ad esempio, non è una classe di modello toouse o potrebbe essere necessario toouse una classe di modello esistente che non si desidera toomodify aggiungendo attributi.
>
> 

Inoltre toofields, è possibile anche aggiungere i profili di punteggio, suggerimento o toohello opzioni CORS indice (omesso dall'esempio hello per brevità). È possibile trovare ulteriori informazioni sull'oggetto Index hello e le relative parti costituenti in hello [riferimento SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index), nonché in hello [riferimento API REST di ricerca di Azure](https://docs.microsoft.com/rest/api/searchservice/).

### <a name="populating-hello-index"></a>La compilazione di indice hello
passaggio successivo di Hello in `Main` toopopulate hello nuovo indice. Questa operazione viene eseguita in hello seguente metodo:

```csharp
private static void UploadDocuments(ISearchIndexClient indexClient)
{
    var hotels = new Hotel[]
    {
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
        },
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
        },
        new Hotel() 
        { 
            HotelId = "3", 
            BaseRate = 129.99,
            Description = "Close tootown hall and hello river"
        }
    };

    var batch = IndexBatch.Upload(hotels);

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
}
```

Questo metodo è costituito da quattro parti. Hello crea innanzitutto una matrice di `Hotel` gli oggetti che verranno utilizzato come indice di toohello tooupload i dati di input. Questi dati sono hardcoded per motivi di semplicità. Nell'applicazione, i dati probabilmente proverranno da un'origine dati esterna, ad esempio un database SQL.

seconda parte Hello crea un `IndexBatch` che contengono i documenti hello. Specificare hello operazione che si desidera tooapply toohello batch hello momento della creazione, in questo caso chiamando `IndexBatch.Upload`. Hello batch viene quindi caricato toohello ricerca di Azure di indice da hello `Documents.Index` metodo.

> [!NOTE]
> In questo esempio, verranno semplicemente caricati i documenti. Se si desidera toomerge assuma la forma documenti esistenti o eliminare i documenti, è possibile creare batch chiamando `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, o `IndexBatch.Delete` invece. È inoltre possibile combinare diverse operazioni in un singolo batch chiamando `IndexBatch.New`, che accetta una raccolta di `IndexAction` oggetti, ognuno dei quali indica un'operazione specifica in un documento a tooperform di ricerca di Azure. È possibile creare ogni `IndexAction` con il proprio operazione mediante la chiamata di metodo corrispondente hello, ad esempio `IndexAction.Merge`, `IndexAction.Upload`e così via.
> 
> 

Hello terza parte di questo metodo è un blocco catch che gestisce un caso di errore importanti per l'indicizzazione. Se il servizio di ricerca di Azure non riesce tooindex hello alcuni documenti nel batch di hello, un `IndexBatchException` viene generata da `Documents.Index`. Questa situazione può verificarsi se l'indicizzazione dei documenti avviene mentre il servizio è sovraccarico. **Si consiglia di gestire in modo esplicito questo caso nel codice.** È possibile ritardare e quindi ripetere l'indicizzazione documenti hello che non è riuscita oppure è possibile accedere e continuare come esempio hello non oppure è possibile eseguire qualcos'altro a seconda dei requisiti di coerenza dei dati dell'applicazione.

> [!NOTE]
> È possibile utilizzare hello `FindFailedActionsToRetry` tooconstruct metodo un nuovo batch contenente hello solo le azioni che non è riuscito a una precedente chiamata troppo`Index`. metodo Hello è documentato [qui](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) ed è presente una discussione sulle modalità d'uso da tooproperly [su StackOverflow](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry).
>
>

Infine, hello `UploadDocuments` ritardi di metodo di due secondi. L'indicizzazione avviene in modo asincrono nel servizio di ricerca di Azure, quindi l'applicazione di esempio hello deve toowait tooensure un breve periodo di tempo che sono disponibili per la ricerca di documenti di hello. Ritardi come questi in genere sono necessari solo in applicazioni di esempio, test e demo.

#### <a name="how-hello-net-sdk-handles-documents"></a>La modalità di gestione di documenti hello .NET SDK
Per comprendere come hello Azure Search .NET SDK è istanze tooupload in grado di una classe definita dall'utente come `Hotel` toohello indice. toohelp rispondere alla domanda, si esaminerà hello `Hotel` classe:

```csharp
using System;
using Microsoft.Azure.Search;
using Microsoft.Azure.Search.Models;
using Microsoft.Spatial;
using Newtonsoft.Json;

// hello SerializePropertyNamesAsCamelCase attribute is defined in hello Azure Search .NET SDK.
// It ensures that Pascal-case property names in hello model class are mapped toocamel-case
// field names in hello index.
[SerializePropertyNamesAsCamelCase]
public partial class Hotel
{
    [System.ComponentModel.DataAnnotations.Key]
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
}
```

Hello in primo luogo toonotice è che ogni proprietà pubblica di `Hotel` corrisponde tooa campo nella definizione dell'indice hello, ma con una differenza fondamentale: nome hello di ogni campo inizia con una lettera minuscola ("caso camel"), mentre il nome di hello ogni pubblico proprietà di `Hotel` inizia con una lettera maiuscola ("convenzione Pascal"). Si tratta di uno scenario comune in applicazioni .NET che eseguire il binding di dati in cui lo schema di destinazione hello è controllo hello di fuori di sviluppatore dell'applicazione hello. Invece di tooviolate hello .NET convenzioni di denominazione rendendo proprietà nomi maiuscole-minuscole camel, è possibile indicare hello SDK toomap hello proprietà nomi toocamel caso automaticamente con hello `[SerializePropertyNamesAsCamelCase]` attributo.

> [!NOTE]
> Hello Azure Search .NET SDK Usa hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) tooserialize libreria e deserializzare tooand di oggetti del modello personalizzato da JSON. Se necessario, è possibile personalizzare questa serializzazione. Per altre informazioni, vedere [Serializzazione personalizzata con JSON.NET](#JsonDotNet).
> 
> 

Hello secondo toonotice cosa sono gli attributi di hello come `IsFilterable`, `IsSearchable`, `Key`, e `Analyzer` che decorano ogni proprietà pubblica. Questi attributi eseguono il mapping direttamente toohello [attributi corrispondenti dell'indice di ricerca di Azure hello](https://docs.microsoft.com/rest/api/searchservice/create-index#request). Hello `FieldBuilder` classe utilizza le definizioni di campo tooconstruct per indice hello.

Hello terzo importante su hello `Hotel` classe sono tipi di dati hello delle proprietà pubbliche di hello. tipi di queste proprietà .NET Hello mappare i tipi di campo equivalente tootheir nella definizione dell'indice hello. Ad esempio, hello `Category` toohello esegue il mapping di proprietà stringa `category` campo, è di tipo `Edm.String`. Mapping di tipo simile tra `bool?` e `Edm.Boolean`, `DateTimeOffset?` e `Edm.DateTimeOffset`, regole specifiche di hello e così via per il mapping di tipo hello sono documentate con hello `Documents.Get` metodo hello [Azure Search .NET SDK riferimento](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_). Hello `FieldBuilder` classe si occupa di questo mapping per l'utente, ma può comunque essere toounderstand utile nel caso in cui è necessario tootroubleshoot eventuali problemi di serializzazione.

Questa possibilità toouse le proprie classi come documenti funziona in entrambe le direzioni; È anche possibile recuperare i risultati della ricerca e avere hello SDK automaticamente deserializzare li tooa tipo di propria scelta, come verrà illustrato nella sezione successiva hello.

> [!NOTE]
> Hello Azure Search .NET SDK supporta anche i documenti tipizzata in modo dinamico utilizzando hello `Document` (classe), ovvero un mapping di chiave/valore nomi toofield dei valori dei campi. Ciò è utile negli scenari in cui non si conosce dello schema di indice hello in fase di progettazione o in cui sarebbe scomodo toobind toospecific classi del modello. Tutti i metodi di hello hello SDK che gestiscono documenti presentano overload che funzionano con hello `Document` classe, come gli overload fortemente tipizzato che accettano un parametro di tipo generico. Hello solo quest'ultimo vengono utilizzati nel codice di esempio hello in questa esercitazione. Hello `Document` classe eredita da `Dictionary<string, object>`. Per informazioni più dettagliate, vedere [qui](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).
> 
> 

**Perché usare tipi di dati nullable**

Quando si progetta la propria indice di ricerca di Azure tooan toomap classi di modello, si consiglia di dichiarazione delle proprietà dei tipi di valore, ad esempio `bool` e `int` toobe ammette valori null (ad esempio, `bool?` anziché `bool`). Se si utilizza una proprietà che non ammette valori null, è necessario troppo**garantire** che nessun documenti nell'indice contengono un valore null per il campo corrispondente hello. Hello SDK né hello del servizio di ricerca di Azure consentirà si tooenforce questo.

Non è un problema di ipotetica: si consideri uno scenario in cui aggiungere un nuovo campo tooan esistente indice di tipo `Edm.Int32`. Dopo aver aggiornato la definizione dell'indice hello, tutti i documenti avrà un valore null per il nuovo campo (poiché tutti i tipi nullable in ricerca di Azure). Se si utilizza una classe di modello con un non-nullable `int` proprietà per il campo, si otterrà un `JsonSerializationException` simile durante il tentativo di tooretrieve documenti:

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

Per questo motivo, è consigliabile usare tipi nullable nelle classi di modelli.

<a name="JsonDotNet"></a>

#### <a name="custom-serialization-with-jsonnet"></a>Serializzazione personalizzata con JSON.NET
Hello SDK utilizza JSON.NET per la serializzazione e la deserializzazione di documenti. È possibile personalizzare la serializzazione e la deserializzazione se necessario definendo la propria `JsonConverter` o `IContractResolver` (vedere hello [JSON.NET documentazione](http://www.newtonsoft.com/json/help/html/Introduction.htm) per altri dettagli). Può essere utile quando si desidera che una classe di modello esistente tooadapt dall'applicazione per l'utilizzo con ricerca di Azure e altri scenari più avanzati. Con la serializzazione personalizzata, ad esempio, è possibile:

* Includere o escludere determinate proprietà della classe modello da archiviare come campi di un documento.
* Eseguire il mapping tra i nomi di proprietà nel codice e i nomi di campo nell'indice.
* Creare attributi personalizzati che possono essere utilizzati per il mapping dei campi di proprietà toodocument.

È possibile trovare esempi di implementazione di serializzazione personalizzata in hello unit test per hello Azure Search .NET SDK in GitHub. È consigliabile iniziare da [questa cartella](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models), Contiene classi che vengono utilizzate dai test di serializzazione personalizzata hello.

### <a name="searching-for-documents-in-hello-index"></a>Ricerca di documenti nell'indice hello
ultimo passaggio di Hello nell'applicazione di esempio hello è toosearch per alcuni documenti nell'indice hello. metodo Hello esegue questa operazione:

```csharp
private static void RunQueries(ISearchIndexClient indexClient)
{
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
}
```

Ogni volta che viene eseguita una query, questo metodo crea prima un nuovo oggetto `SearchParameters`. Si tratta di toospecify utilizzate opzioni aggiuntive per query hello, ad esempio l'ordinamento, filtro, paging e facet. In questo metodo, è in corso configurazione hello `Filter`, `Select`, `OrderBy`, e `Top` proprietà per query diverse. Hello tutti `SearchParameters` le proprietà vengono documentate [qui](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).

passaggio successivo Hello è tooactually eseguire query di ricerca hello. Questa operazione viene eseguita utilizzando hello `Documents.Search` metodo. Per ogni query, hello ricerca testo toouse viene passato come stringa (o `"*"` se non è presente testo di ricerca), nonché hello creati in precedenza di parametri di ricerca. È inoltre possibile specificare `Hotel` come parametro di tipo hello `Documents.Search`, che indica i documenti toodeserialize SDK hello nei risultati della ricerca hello in oggetti di tipo `Hotel`.

> [!NOTE]
> È possibile trovare ulteriori informazioni sulla sintassi delle espressioni di query ricerca hello [qui](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).
> 
> 

Infine, dopo ogni query questo metodo scorre tutte le corrispondenze di hello nei risultati della ricerca hello, stampa di ogni console toohello documento:

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

Prendiamo a sua volta informazioni dettagliate su ognuna delle query hello. Ecco hello codice tooexecute hello prima query:

```csharp
parameters =
    new SearchParameters()
    {
        Select = new[] { "hotelName" }
    };

results = indexClient.Documents.Search<Hotel>("budget", parameters);

WriteDocuments(results);
```

In questo caso, viene eseguita la ricerca per gli alberghi parola hello "budget" e si desidera tooget nuovamente solo hello hotel i nomi, come specificato da hello `Select` parametro. Di seguito sono risultati hello:

    Name: Roach Motel

Successivamente, si desidera che gli hotel hello toofind con una frequenza minore di $ 150 notturna e restituire solo hello hotel ID e la descrizione:

```csharp
parameters =
    new SearchParameters()
    {
        Filter = "baseRate lt 150",
        Select = new[] { "hotelId", "description" }
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);
```

Questa query utilizza OData `$filter` espressione, `baseRate lt 150`, documenti hello toofilter nell'indice hello. È possibile trovare ulteriori informazioni su sintassi OData che supporta la ricerca di Azure hello [qui](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).

Di seguito sono risultati hello di query di hello:

    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close tootown hall and hello river

A questo punto, è opportuno toofind hello superiore due gli hotel sono stati rimodernati più di recente, che mostrano il nome di hotel hello e data di rinnovo. Ecco il codice hello: 

```csharp
parameters =
    new SearchParameters()
    {
        OrderBy = new[] { "lastRenovationDate desc" },
        Select = new[] { "hotelName", "lastRenovationDate" },
        Top = 2
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);
```

In questo caso, utilizziamo nuovamente hello toospecify sintassi di OData `OrderBy` parametro come `lastRenovationDate desc`. È inoltre possibile impostare `Top` too2 tooensure è solo ottenere hello primi due documenti. Come prima, impostiamo `Select` toospecify i campi devono essere restituiti.

Di seguito sono risultati hello:

    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

Infine, è necessario toofind tutti gli alberghi parola hello "motel":

```csharp
parameters = new SearchParameters();
results = indexClient.Documents.Search<Hotel>("motel", parameters);

WriteDocuments(results);
```

Ecco i risultati di hello, che includono tutti i campi, poiché non è stato specificato hello `Select` proprietà:

    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577

Questo passaggio di completamento dell'esercitazione hello, ma non interrompere qui. **Passaggi successivi** vengono fornite risorse aggiuntive per ottenere ulteriori informazioni su Ricerca di Azure.

## <a name="next-steps"></a>Passaggi successivi
* Individuare i riferimenti di hello per hello [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) e [API REST](https://docs.microsoft.com/rest/api/searchservice/).
* Approfondire l'argomento tramite [video e altri esempi ed esercitazioni](search-video-demo-tutorial-list.md).
* Revisione [convenzioni di denominazione](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) regole hello toolearn per la denominazione dei vari oggetti.
* Rivedere i [tipi di dati supportati](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) in Ricerca di Azure.
