---
title: aaa "caricamento di dati (.NET - ricerca di Azure) | Documenti di Microsoft"
description: Informazioni su come indice di tooan tooupload dati in ricerca di Azure tramite hello .NET SDK.
services: search
documentationcenter: 
author: brjohnstmsft
manager: jhubbard
editor: 
tags: 
ms.assetid: 0e0e7e7b-7178-4c26-95c6-2fd1e8015aca
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 01/13/2017
ms.author: brjohnst
ms.openlocfilehash: 78ddbefb522884d1f61cb275c25c091487aee639
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-tooazure-search-using-hello-net-sdk"></a>Caricamento dati tooAzure ricerca tramite hello .NET SDK
> [!div class="op_single_selector"]
> * [Panoramica](search-what-is-data-import.md)
> * [.NET](search-import-data-dotnet.md)
> * [REST](search-import-data-rest-api.md)
> 
> 

In questo articolo viene illustrato come hello toouse [Azure Search .NET SDK](https://aka.ms/search-sdk) tooimport dati in un indice di ricerca di Azure.

Prima di iniziare questa procedura dettagliata, è necessario avere [creato un indice di Ricerca di Azure](search-what-is-an-index.md). In questo articolo si presuppone inoltre che è già stato creato un `SearchServiceClient` dell'oggetto, come illustrato nella [creare un indice di ricerca di Azure mediante .NET SDK hello](search-create-index-dotnet.md#CreateSearchServiceClient).

> [!NOTE]
> Tutto il codice di esempio in questo articolo è scritto in C#. È possibile trovare il codice sorgente completo hello [su GitHub](http://aka.ms/search-dotnet-howto). È inoltre possibile leggere sulla hello [Azure Search .NET SDK](search-howto-dotnet-sdk.md) per una più dettagliata procedura hello del codice di esempio.

Nei documenti di ordine toopush nell'indice utilizzando hello .NET SDK, sarà necessario:

1. Creare un `SearchIndexClient` oggetto tooconnect tooyour indice di ricerca.
2. Creare un `IndexBatch` contenente hello documenti toobe aggiunti, modificati o eliminati.
3. Chiamare hello `Documents.Index` metodo i `SearchIndexClient` toosend hello `IndexBatch` tooyour indice di ricerca.

## <a name="create-an-instance-of-hello-searchindexclient-class"></a>Creare un'istanza della classe SearchIndexClient hello
l'indice utilizzando dati tooimport hello Azure Search .NET SDK, sarà necessario toocreate un'istanza di hello `SearchIndexClient` classe. È possibile creare questa istanza di se stessi, ma più semplice se si dispone già di un `SearchServiceClient` toocall istanza relativa `Indexes.GetClient` metodo. Ad esempio, ecco come è possibile ottenere un `SearchIndexClient` per hello indice denominata "Hotel" da un `SearchServiceClient` denominato `serviceClient`:

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> In un'applicazione di ricerca tipica, il popolamento e la gestione degli indici viene gestita da un componente separato dalle query di ricerca. `Indexes.GetClient`è utile per la compilazione di un indice perché si salva hello problemi di fornire un altro `SearchCredentials`. A tale scopo, passando la chiave di amministrazione hello hello toocreate utilizzati che si `SearchServiceClient` toohello nuova `SearchIndexClient`. Tuttavia, in parte dell'applicazione che esegue query hello è migliore hello toocreate `SearchIndexClient` direttamente in modo che è possibile passare una chiave di query anziché una chiave amministratore. Questo comportamento è coerente con hello [principio di privilegio minimo](https://en.wikipedia.org/wiki/Principle_of_least_privilege) e consentirà toomake l'applicazione più sicura. È possibile trovare ulteriori informazioni sulle chiavi amministratore e le chiavi di query in hello [riferimento API REST di ricerca di Azure](https://docs.microsoft.com/rest/api/searchservice/).
> 
> 

`SearchIndexClient` include una proprietà `Documents`. Questa proprietà fornisce tutti i metodi di hello è necessario tooadd, modificare, eliminare o eseguire query sui documenti nell'indice.

## <a name="decide-which-indexing-action-toouse"></a>Decidere quali indicizzazione toouse azione
dati tooimport utilizzando hello .NET SDK, sarà necessario toopackage backup dei dati in un `IndexBatch` oggetto. Un `IndexBatch` incapsula una raccolta di `IndexAction` oggetti, ognuno dei quali contiene un documento e una proprietà che indica quali tooperform azione di ricerca di Azure su tale documento (caricamento, unione, eliminazione e così via). A seconda di quale dei hello si sceglie di azioni riportate di seguito, solo alcuni campi devono essere inclusi per ogni documento:

| Azione | Description | Campi necessari per ogni documento | Note |
| --- | --- | --- | --- |
| `Upload` |Un `Upload` tooan simile "upsert" in cui verrà inserito se è nuovo e aggiornato/sostituito se esiste il documento hello è intervento dell'utente. |chiave, oltre a tutti gli altri campi che si desidera toodefine |Durante l'aggiornamento o la sostituzione di un documento esistente, qualsiasi campo che non è specificato nella richiesta di hello avrà il campo impostato troppo`null`. Questo errore si verifica anche quando il campo hello è stato impostato precedentemente valore non null tooa. |
| `Merge` |Gli aggiornamenti del documento esistente con hello specificati campi. Se non esiste alcun documento hello nell'indice hello, merge hello avrà esito negativo. |chiave, oltre a tutti gli altri campi che si desidera toodefine |Qualsiasi campo specificato in un'unione sostituirà campo esistente di hello nel documento hello. Sono inclusi anche i campi di tipo `DataType.Collection(DataType.String)`. Ad esempio, se hello documento contiene un campo `tags` con valore `["budget"]` e si esegue un'unione con valore `["economy", "pool"]` per `tags`, il valore finale di hello hello `tags` campo sarà `["economy", "pool"]`. e non `["budget", "economy", "pool"]`. |
| `MergeOrUpload` |Questa azione è analoga `Merge` se esiste un documento con hello data già chiave nell'indice hello. Se il documento hello non esiste, si comporta come `Upload` con un nuovo documento. |chiave, oltre a tutti gli altri campi che si desidera toodefine |- |
| `Delete` |Rimozione di documento specificato hello dall'indice di hello. |solo campo chiave |Tutti i campi specificare diverso hello chiave campo verrà ignorato. Se si desidera tooremove un singolo campo da un documento, utilizzare `Merge` invece e impostare semplicemente il campo hello in modo esplicito toonull. |

È possibile specificare quale azione si desidera toouse con diversi metodi statici di hello hello `IndexBatch` e `IndexAction` classi, come illustrato nella sezione successiva hello.

## <a name="construct-your-indexbatch"></a>Costruire IndexBatch
Ora che si conosce quali tooperform azioni sui documenti, si è pronti tooconstruct hello `IndexBatch`. Hello di esempio seguente viene illustrato come toocreate un batch con alcune azioni. Si noti che questo esempio Usa una classe personalizzata denominata `Hotel` tooa documento nell'indice "Hotel" hello che esegue il mapping.

```csharp
var actions =
    new IndexAction<Hotel>[]
    {
        IndexAction.Upload(
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
            }),
        IndexAction.Upload(
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
            }),
        IndexAction.MergeOrUpload(
            new Hotel()
            {
                HotelId = "3",
                BaseRate = 129.99,
                Description = "Close tootown hall and hello river"
            }),
        IndexAction.Delete(new Hotel() { HotelId = "6" })
    };

var batch = IndexBatch.New(actions);
```

In questo caso, si sta usando `Upload`, `MergeOrUpload`, e `Delete` come azioni la ricerca, come specificato dai metodi hello chiamati su hello `IndexAction` classe.

Si supponga che l'indice "hotels" di esempio sia già popolato con alcuni documenti. Si noti come non è toospecify tutti i campi del documento possibili hello quando si utilizza `MergeOrUpload` e come viene specificata solo la chiave di documento hello (`HotelId`) quando si utilizza `Delete`.

Si noti inoltre che è possibile includere solo i documenti too1000 in una singola richiesta di indicizzazione.

> [!NOTE]
> In questo esempio, viene applicata la documenti toodifferent azioni diverse. Se si desidera tooperform hello azioni stesso in tutti i documenti nel batch di hello, anziché chiamare `IndexBatch.New`, è possibile utilizzare altri metodi statici di hello `IndexBatch`. Ad esempio, è possibile creare batch chiamando `IndexBatch.Merge`, `IndexBatch.MergeOrUpload` o `IndexBatch.Delete`. Questi metodi accettano una raccolta di documenti (oggetti di tipo `Hotel` in questo esempio) invece di oggetti `IndexAction`.
> 
> 

## <a name="import-data-toohello-index"></a>Indice toohello di importazione dei dati
Dopo aver creato un oggetto inizializzato `IndexBatch` dell'oggetto, è possibile inviarlo indice toohello chiamando `Documents.Index` sul `SearchIndexClient` oggetto. Hello seguente esempio viene illustrato come toocall `Index`, nonché come alcuni passaggi aggiuntivi che sarà necessario tooperform:

```csharp
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
```

Hello nota `try` / `catch` circostanti hello chiamata toohello `Index` metodo. blocco catch Hello gestisce un caso di errore importanti per l'indicizzazione. Se il servizio di ricerca di Azure non riesce tooindex hello alcuni documenti nel batch di hello, un `IndexBatchException` viene generata da `Documents.Index`. Questa situazione può verificarsi se l'indicizzazione dei documenti avviene mentre il servizio è sovraccarico. **Si consiglia di gestire in modo esplicito questo caso nel codice.** È possibile ritardare e quindi ripetere l'indicizzazione documenti hello che non è riuscita oppure è possibile accedere e continuare come esempio hello non oppure è possibile eseguire qualcos'altro a seconda dei requisiti di coerenza dei dati dell'applicazione.

Infine, hello codice di esempio hello sopra ritardi di due secondi. L'indicizzazione avviene in modo asincrono nel servizio di ricerca di Azure, quindi l'applicazione di esempio hello deve toowait tooensure un breve periodo di tempo che sono disponibili per la ricerca di documenti di hello. Ritardi come questi in genere sono necessari solo in applicazioni di esempio, test e demo.

<a name="HotelClass"></a>

### <a name="how-hello-net-sdk-handles-documents"></a>La modalità di gestione di documenti hello .NET SDK
Per comprendere come hello Azure Search .NET SDK è istanze tooupload in grado di una classe definita dall'utente come `Hotel` toohello indice. toohelp rispondere alla domanda, si esaminerà hello `Hotel` (classe), che esegue il mapping dello schema di indice toohello definito in [creare un indice di ricerca di Azure mediante .NET SDK hello](search-create-index-dotnet.md#DefineIndex):

```csharp
[SerializePropertyNamesAsCamelCase]
public partial class Hotel
{
    [Key]
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

    // ToString() method omitted for brevity...
}
```

Hello in primo luogo toonotice è che ogni proprietà pubblica di `Hotel` corrisponde tooa campo nella definizione dell'indice hello, ma con una differenza fondamentale: nome hello di ogni campo inizia con una lettera minuscola ("caso camel"), mentre il nome di hello ogni pubblico proprietà di `Hotel` inizia con una lettera maiuscola ("convenzione Pascal"). Si tratta di uno scenario comune in applicazioni .NET che eseguire il binding di dati in cui lo schema di destinazione hello è controllo hello di fuori di sviluppatore dell'applicazione hello. Invece di tooviolate hello .NET convenzioni di denominazione rendendo proprietà nomi maiuscole-minuscole camel, è possibile indicare hello SDK toomap hello proprietà nomi toocamel caso automaticamente con hello `[SerializePropertyNamesAsCamelCase]` attributo.

> [!NOTE]
> Hello Azure Search .NET SDK Usa hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) tooserialize libreria e deserializzare tooand di oggetti del modello personalizzato da JSON. Se necessario, è possibile personalizzare questa serializzazione. Per altri dettagli, vedere [Serializzazione personalizzata con JSON.NET](search-howto-dotnet-sdk.md#JsonDotNet). Un esempio di questo è l'utilizzo di hello di hello `[JsonProperty]` attributo hello `DescriptionFr` proprietà nel codice di esempio hello precedente.
> 
> 

Hello secondo importante su hello `Hotel` classe sono tipi di dati hello delle proprietà pubbliche di hello. tipi di queste proprietà .NET Hello mappare i tipi di campo equivalente tootheir nella definizione dell'indice hello. Ad esempio, hello `Category` toohello esegue il mapping di proprietà stringa `category` campo, è di tipo `DataType.String`. Esistono mapping di tipi simili tra `bool?` e `DataType.Boolean`, `DateTimeOffset?` e `DataType.DateTimeOffset` e così via. regole specifiche di Hello per il mapping di tipo hello sono documentate con hello `Documents.Get` metodo hello [riferimento Azure Search .NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).

Questa possibilità toouse le proprie classi come documenti funziona in entrambe le direzioni; È anche possibile recuperare i risultati della ricerca e avere hello SDK automaticamente deserializzare li tooa tipo di propria scelta, come illustrato nell'hello [articolo successivo](search-query-dotnet.md).

> [!NOTE]
> Hello Azure Search .NET SDK supporta anche i documenti tipizzata in modo dinamico utilizzando hello `Document` (classe), ovvero un mapping di chiave/valore nomi toofield dei valori dei campi. Ciò è utile negli scenari in cui non si conosce dello schema di indice hello in fase di progettazione o in cui sarebbe scomodo toobind toospecific classi del modello. Tutti i metodi di hello hello SDK che gestiscono documenti presentano overload che funzionano con hello `Document` classe, come gli overload fortemente tipizzato che accettano un parametro di tipo generico. Hello solo quest'ultimo vengono utilizzati nel codice di esempio hello in questo articolo.
> 
> 

**Perché usare tipi di dati nullable**

Quando si progetta la propria indice di ricerca di Azure tooan toomap classi di modello, si consiglia di dichiarazione delle proprietà dei tipi di valore, ad esempio `bool` e `int` toobe ammette valori null (ad esempio, `bool?` anziché `bool`). Se si utilizza una proprietà che non ammette valori null, è necessario troppo**garantire** che nessun documenti nell'indice contengono un valore null per il campo corrispondente hello. Hello SDK né hello del servizio di ricerca di Azure consentirà si tooenforce questo.

Non è un problema di ipotetica: si consideri uno scenario in cui aggiungere un nuovo campo tooan esistente indice di tipo `DataType.Int32`. Dopo aver aggiornato la definizione dell'indice hello, tutti i documenti avrà un valore null per il nuovo campo (poiché tutti i tipi nullable in ricerca di Azure). Se si utilizza una classe di modello con un non-nullable `int` proprietà per il campo, si otterrà un `JsonSerializationException` simile durante il tentativo di tooretrieve documenti:

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

Per questo motivo, è consigliabile usare tipi nullable nelle classi di modelli.

## <a name="next-steps"></a>Passaggi successivi
Dopo avere popolato l'indice di ricerca di Azure, sarà pronto toostart emittente toosearch query per i documenti. Per informazioni dettagliate, vedere [Eseguire query su un indice di Ricerca di Azure](search-query-overview.md) .

