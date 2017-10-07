---
title: aaa "creare un indice (API .NET - ricerca di Azure) | Documenti di Microsoft"
description: Creare un indice nel codice utilizzando hello Azure Search .NET SDK.
services: search
documentationcenter: 
author: brjohnstmsft
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 3a851647-fc7b-4fb6-8506-6aaa519e77cd
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/22/2017
ms.author: brjohnst
ms.openlocfilehash: 7fa4030b8c3565bc02b1d6bb4426331657cf3a5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-index-using-hello-net-sdk"></a>Creare un indice di ricerca di Azure mediante .NET SDK hello
> [!div class="op_single_selector"]
> * [Panoramica](search-what-is-an-index.md)
> * [Portale](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
> 
> 

In questo articolo verrà illustrati il processo di hello di creazione di una ricerca di Azure [indice](https://docs.microsoft.com/rest/api/searchservice/Create-Index) utilizzando hello [Azure Search .NET SDK](https://aka.ms/search-sdk).

Prima di seguire le indicazioni di questa guida e creare un indice, è necessario [creare un servizio Ricerca di Azure](search-create-service-portal.md).

> [!NOTE]
> Tutto il codice di esempio in questo articolo è scritto in C#. È possibile trovare il codice sorgente completo hello [su GitHub](http://aka.ms/search-dotnet-howto). È inoltre possibile leggere sulla hello [Azure Search .NET SDK](search-howto-dotnet-sdk.md) per una più dettagliata procedura hello del codice di esempio.


## <a name="identify-your-azure-search-services-admin-api-key"></a>Identificare la chiave API amministratore del servizio Ricerca di Azure
Ora che è stato effettuato il provisioning di un servizio di ricerca di Azure, si è quasi pronto tooissue richieste con l'endpoint del servizio utilizzando hello .NET SDK. In primo luogo, è necessario tooobtain uno dei hello admin chiavi api che è stato generato per il servizio di ricerca hello che è effettuato il provisioning. Hello .NET SDK invierà questa chiave api nel servizio di tooyour ogni richiesta. Disporre di una chiave valida stabilisce relazioni di trust, un singolo per ogni richiesta, tra hello invio hello richiesta e il servizio di hello che la gestisce.

1. toofind le chiavi del servizio api, accedi toohello [portale di Azure](https://portal.azure.com/)
2. Pannello del servizio di ricerca di Azure andare tooyour
3. Fare clic su hello icona "Chiavi"

Il servizio avrà *chiavi amministratore* e *chiavi di query*.

* Il database primario e secondario *chiavi amministratore* concedere diritti completi tooall operazioni, incluso hello possibilità toomanage hello servizio, creare ed eliminare origini di dati, gli indicizzatori e gli indici. Esistono due chiavi in modo che sia possibile continuare chiave secondaria di hello toouse se si decide di tooregenerate hello primary key e viceversa.
* Il *query chiavi* concedere l'accesso in sola lettura tooindexes e documenti e sono in genere distribuite tooclient applicazioni che inviano richieste di ricerca.

Ai fini di hello di creazione di un indice, è possibile utilizzare la chiave amministratore primaria o secondaria.

<a name="CreateSearchServiceClient"></a>

## <a name="create-an-instance-of-hello-searchserviceclient-class"></a>Creare un'istanza della classe SearchServiceClient hello
utilizzando toostart hello Azure Search .NET SDK, sarà necessario toocreate un'istanza di hello `SearchServiceClient` classe. Questa classe ha diversi costruttori. Hello quello desiderato accetta il nome del servizio di ricerca e un `SearchCredentials` oggetto come parametri. `SearchCredentials` esegue il wrapping della chiave API.

Crea un nuovo codice Hello seguente `SearchServiceClient` utilizzando i valori per nome del servizio ricerca hello e la chiave api che vengono archiviati nel file di configurazione dell'applicazione hello (`appsettings.json` nel caso di hello di hello [applicazione di esempio](http://aka.ms/search-dotnet-howto)):

```csharp
private static SearchServiceClient CreateSearchServiceClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string adminApiKey = configuration["SearchServiceAdminApiKey"];

    SearchServiceClient serviceClient = new SearchServiceClient(searchServiceName, new SearchCredentials(adminApiKey));
    return serviceClient;
}
```

`SearchServiceClient` ha una proprietà `Indexes`. Questa proprietà fornisce tutti i metodi di hello necessità toocreate, elenco, aggiornamento o eliminazione di indici di ricerca di Azure.

> [!NOTE]
> Hello `SearchServiceClient` gestiti dalla classe servizio di ricerca tooyour connessioni. In ordine tooavoid apertura di un numero eccessivo di connessioni, è consigliabile provare tooshare una singola istanza di `SearchServiceClient` dell'applicazione, se possibile. I metodi è thread-safe tooenable tale condivisione.
> 
> 

<a name="DefineIndex"></a>

## <a name="define-your-azure-search-index"></a>Definire l'indice di ricerca di Azure
Una singola chiamata toohello `Indexes.Create` metodo verrà creato l'indice. Questo metodo accetta come parametro un oggetto `Index` che definisce l'indice di Ricerca di Azure. È necessario toocreate un `Index` dell'oggetto e inizializzarlo come indicato di seguito:

1. Set hello `Name` proprietà di hello `Index` toohello nome dell'oggetto dell'indice.
2. Set hello `Fields` proprietà di hello `Index` matrice di oggetti tooan di `Field` oggetti. hello toocreate modo più semplice di Hello `Field` oggetti è chiamata hello `FieldBuilder.BuildForType` , passando una classe di modello per il parametro di tipo hello. Una classe di modello dispone di proprietà che eseguono il mapping campi toohello dell'indice. In questo modo toobind documenti dal tooinstances di indice di ricerca della classe modello.

> [!NOTE]
> Se non si prevede di toouse una classe di modello, è possibile definire l'indice ancora creando `Field` direttamente gli oggetti. È possibile specificare il nome di hello di hello campo toohello costruttore con tipo di dati hello (o analyzer per i campi stringa). È inoltre possibile impostare altre proprietà come `IsSearchable`, `IsFilterable` e così via.
>
>

È importante tenere le esigenze di business e di esperienza utente ricerca presenti quando si progetta l'indice di ogni campo deve essere assegnato hello [proprietà pertinenti](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Queste proprietà di controllo che le funzionalità (applicazione di filtri, facet, ordinamento, ricerca full-text e così via) di ricerca si applicano toowhich campi. Per qualsiasi proprietà che non si imposta in modo esplicito, hello `Field` classe predefinite funzionalità di ricerca toodisabling hello corrispondente, a meno che non si abilitarlo in modo specifico.

All'indice di esempio è stato assegnato il nome "hotels" e i campi sono stati definiti usando una classe modello. Ogni proprietà della classe del modello hello dispone di attributi che determinano i comportamenti hello relative alla ricerca di campi di indice corrispondente hello. classe modello Hello è definito come segue:

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

Con attenzione, abbiamo scelto attributi hello per ogni proprietà in base a come si ritiene che verranno utilizzati in un'applicazione. Ad esempio, è probabile che gli utenti di cercare gli hotel saranno interessati corrispondenze di parole chiave in hello `description` campo, pertanto è abilitare la ricerca full-text per il campo aggiungendo hello `IsSearchable` attributo toohello `Description` proprietà.

Si noti che un solo campo nell'indice di tipo `string` deve essere hello designata come hello *chiave* campo aggiungendo hello `Key` attributo (vedere `HotelId` in hello esempio precedente).

definizione dell'indice Hello precedente Usa un analizzatore di lingua per hello `description_fr` campo perché è testo francese toostore desiderato. Vedere [argomento supporto lingua di hello](https://docs.microsoft.com/rest/api/searchservice/Language-support) nonché hello corrispondente [post di blog](https://azure.microsoft.com/blog/language-support-in-azure-search/) per ulteriori informazioni sugli analizzatori di linguaggio.

> [!NOTE]
> Per impostazione predefinita, il nome di hello di ogni proprietà nella classe del modello viene utilizzato come nome hello del campo corrispondente hello indice hello. Se si desidera toomap tutti i nomi di campo toocamel caso i nomi di proprietà, contrassegnare la classe hello con hello `SerializePropertyNamesAsCamelCase` attributo. Se si desidera toomap tooa altro nome, è possibile utilizzare hello `JsonProperty` attributo come hello `DescriptionFr` proprietà precedente. Hello `JsonProperty` attributo ha la precedenza su hello `SerializePropertyNamesAsCamelCase` attributo.
> 
> 

Dopo aver definito una classe modello, è possibile creare una definizione di indice in modo molto semplice:

```csharp
var definition = new Index()
{
    Name = "hotels",
    Fields = FieldBuilder.BuildForType<Hotel>()
};
```

## <a name="create-hello-index"></a>Creare l'indice di hello
Dopo aver creato un oggetto inizializzato `Index` dell'oggetto, è possibile creare l'indice di hello semplicemente chiamando `Indexes.Create` sul `SearchServiceClient` oggetto:

```csharp
serviceClient.Indexes.Create(definition);
```

Per una richiesta ha esito positivo, il metodo hello restituirà normalmente. Se si verifica un problema con la richiesta hello, ad esempio un parametro non valido, il metodo di hello genererà `CloudException`.

Una volta terminato con un toodelete indice e si desidera, chiamare solo hello `Indexes.Delete` metodo i `SearchServiceClient`. Ad esempio, ecco come si sarebbe eliminare l'indice "Hotel" hello:

```csharp
serviceClient.Indexes.Delete("hotels");
```

> [!NOTE]
> codice di esempio Hello in questo articolo utilizza metodi sincroni di hello di hello Azure Search .NET SDK per motivi di semplicità. È consigliabile utilizzare i metodi asincroni hello nel proprio tookeep applicazioni scalabili e reattive. Ad esempio, in hello esempi precedenti è possibile utilizzare `CreateAsync` e `DeleteAsync` anziché `Create` e `Delete`.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
Dopo aver creato un indice di ricerca di Azure, sarà possibile troppo[caricare i contenuti in indice hello](search-what-is-data-import.md) in modo è possibile avviare la ricerca dei dati.

