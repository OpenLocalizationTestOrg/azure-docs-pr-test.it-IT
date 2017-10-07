---
title: aaaWorking con i dati geospaziali in Azure Cosmos DB | Documenti Microsoft
description: Comprendere come toocreate, indice e query oggetti spaziali con Azure Cosmos DB e hello API DocumentDB.
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: 82ce2898-a9f9-4acf-af4d-8ca4ba9c7b8f
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 05/22/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a1e40b78cb4595631d845d46c21d07a30c8b972f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-geospatial-and-geojson-location-data-in-azure-cosmos-db"></a>Uso dei dati geospaziali e dei dati località GeoJSON in Azure Cosmos DB
Questo articolo è una funzionalità di geospatial introduzione toohello in [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/). Dopo aver letto questo, sarà in grado di tooanswer hello seguenti domande:

* Come si archiviano i dati spaziali in Azure Cosmos DB?
* Come si eseguono query su dati geospaziali in Azure Cosmos DB in SQL e LINQ?
* Come si abilita o disabilita l'indicizzazione spaziale in Azure Cosmos DB?

Questo articolo illustra come toowork con i dati spaziali con hello API DocumentDB. Consultare il [progetto GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) per esempi di codice.

## <a name="introduction-toospatial-data"></a>Data di introduzione toospatial
I dati spaziali descrivono hello posizione e la forma degli oggetti nello spazio. Nella maggior parte delle applicazioni, che corrispondono tooobjects della terra hello, vale a dire i dati geospaziali. Dati spaziali possono essere utilizzati toorepresent hello percorso di una persona, un punto di interesse o limite hello di una città o un lago. Casi di utilizzo comuni includono spesso query di prossimità, ad esempio, "trova tutti i negozi vicino alla mia posizione attuale". 

### <a name="geojson"></a>GeoJSON
Azure Cosmos DB supporta l'indicizzazione e le query di dati geospaziali punto rappresentato utilizzando hello [GeoJSON specifica](https://tools.ietf.org/html/rfc7946). Le strutture di dati GeoJSON sono sempre oggetti JSON validi, quindi possono essere archiviate e sottoposte a query usando Azure Cosmos DB senza librerie o strumenti specializzati. Hello Azure Cosmos DB SDK forniscono classi di helper e metodi che rendono facilmente toowork con dati spaziali. 

### <a name="points-linestrings-and-polygons"></a>Punti, oggetti linestring e poligoni
Un **punto** indica una posizione singola nello spazio. Nei dati geospaziali, un punto rappresenta la posizione esatta di hello che può essere un indirizzo di un negozio di alimentari, continua, un'automobile o una città.  Un punto viene rappresentato in GeoJSON (e Azure Cosmos DB) tramite la sua coppia di coordinate o longitudine e latitudine. Di seguito è riportato un esempio JSON per un punto.

**Punti in Azure Cosmos DB**

```json
{
    "type":"Point",
    "coordinates":[ 31.9, -4.8 ]
}
```

> [!NOTE]
> Hello specifica GeoJSON specifica longitudine prima e la latitudine secondo. Come in altre applicazioni di mapping, longitudine e latitudine sono angoli e sono espresse in gradi. I valori di longitudine vengono misurati dal primo meridiano hello e sono compresi tra -180 e 180.0 gradi e latitudine vengono misurati dall'equatore hello di valori e sono compresi tra-90.0 e 90.0 gradi. 
> 
> Azure DB Cosmos interpreta le coordinate come indicato al sistema di riferimento WGS 84 hello. Per ulteriori informazioni sui sistemi di coordinate di riferimento, vedere di seguito.
> 
> 

I punti possono essere incorporati in un documento di Azure Cosmos DB come illustrato in questo esempio di profilo utente contenente dati di località:

**Usare un profilo con località archiviata in Azure Cosmos DB**

```json
{
    "id":"documentdb-profile",
    "screen_name":"@CosmosDB",
    "city":"Redmond",
    "topics":[ "global", "distributed" ],
    "location":{
        "type":"Point",
        "coordinates":[ 31.9, -4.8 ]
    }
}
```

Toopoints, GeoJSON inoltre supporta anche istanze linestring e poligoni. **Oggetti linestring** rappresentano una serie di due o più punti nello spazio e hello segmenti lineari che li connettono. In dati geospaziali, linestring sono comunemente usate toorepresent autostrade o fiumi. Un oggetto **poligono** è un perimetro costituito da punti connessi che forma un elemento LineString chiuso. Poligoni sono comunemente usate toorepresent formazioni naturali come laghi o politici giurisdizioni come città e province. Di seguito è riportato un esempio di poligono in Azure Cosmos DB. 

**Poligoni in GeoJSON**

```json
{
    "type":"Polygon",
    "coordinates":[
        [ 31.8, -5 ],
        [ 31.8, -4.7 ],
        [ 32, -4.7 ],
        [ 32, -5 ],
        [ 31.8, -5 ]
    ]
}
```

> [!NOTE]
> Hello GeoJSON specifica richiede che per i poligoni validi, hello ultima coppia di coordinate specificato deve essere uguale hello come hello innanzitutto toocreate una forma chiusa.
> 
> I punti all'interno di un poligono devono essere specificati in senso antiorario. Un poligono specificato nell'ordine in senso orario rappresenta inverso hello dell'area di hello in esso contenuti.
> 
> 

In aggiunta tooPoint, LineString e poligono, GeoJSON specifica inoltre la rappresentazione di hello come toogroup più posizioni geospaziale, e come le proprietà arbitrarie tooassociate con geolocation come un **funzionalità**. Trattandosi di oggetti JSON validi, essi possono essere archiviati ed elaborati tutti in Azure Cosmos DB. Azure Cosmos DB supporta tuttavia solo l'indicizzazione automatica dei punti.

### <a name="coordinate-reference-systems"></a>Sistemi di riferimento delle coordinate
Poiché la forma hello della terra hello è irregolare, le coordinate di dati geospaziali è rappresentato in molti sistemi di coordinate di riferimento (CR), ciascuno con i relativi frame di riferimento e le unità di misura. Ad esempio, "National griglia di Gran Bretagna" hello è un sistema di riferimento è molto accurato per hello Regno Unito, ma non al suo esterno. 

Hello CRS più diffusi in uso oggi è hello sistema World Geodetic System [WGS 84](http://earth-info.nga.mil/GandG/wgs84/). Dispositivi GPS e molti servizi di mapping, tra cui Google Maps e le API di Bing Maps, utilizzano WGS-84. Azure Cosmos DB supporta l'indicizzazione e le query di dati geospaziali tramite hello CRS WGS 84. 

## <a name="creating-documents-with-spatial-data"></a>Creazione di documenti con dati spaziali
Quando si creano i documenti che contengono valori GeoJSON, vengono indicizzati automaticamente con un indice spaziale in Criteri di indicizzazione toohello base della raccolta hello. Se si usa un SDK di Azure Cosmos DB in un linguaggio tipizzato in modo dinamico come Python o Node.js, è necessario creare un GeoJSON valido.

**Creare documenti con i dati geospaziali in Node.js**

```json
var userProfileDocument = {
    "name":"documentdb",
    "location":{
        "type":"Point",
        "coordinates":[ -122.12, 47.66 ]
    }
};

client.createDocument(`dbs/${databaseName}/colls/${collectionName}`, userProfileDocument, (err, created) => {
    // additional code within hello callback
});
```

Se si lavora con hello APIs DocumentDB, è possibile utilizzare hello `Point` e `Polygon` classi all'interno di hello `Microsoft.Azure.Documents.Spatial` informazioni sul percorso di spazio dei nomi tooembed all'interno di oggetti di applicazione. Queste classi consentono di semplificare hello serializzazione e deserializzazione dei dati spaziali in GeoJSON.

**Creare documenti con i dati geospaziali in .NET**

```json
using Microsoft.Azure.Documents.Spatial;

public class UserProfile
{
    [JsonProperty("name")]
    public string Name { get; set; }

    [JsonProperty("location")]
    public Point Location { get; set; }

    // More properties
}

await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "profiles"), 
    new UserProfile 
    { 
        Name = "documentdb", 
        Location = new Point (-122.12, 47.66) 
    });
```

Se si dispongano di informazioni di latitudine e longitudine hello, ma dispone di indirizzi fisici hello o nome di percorso, ad esempio città o paese, è possibile cercare le coordinate effettivo hello tramite un servizio di geocodifica come servizi REST di Bing Maps. Ulteriori informazioni sulla geocodifica di Bing Maps sono disponibili [qui](https://msdn.microsoft.com/library/ff701713.aspx).

## <a name="querying-spatial-types"></a>Query sui tipi spaziali
Ora che sono state utilizzate come esaminare i dati geospaziali tooinsert, esaminiamo come tooquery tali dati con database di Cosmos Azure usando SQL e LINQ.

### <a name="spatial-sql-built-in-functions"></a>Funzioni predefinite spaziali di SQL
DB Cosmos Azure supporta hello seguendo le funzioni predefinite di Open Geospatial Consortium (OGC) per l'esecuzione di query geospaziale. Per ulteriori informazioni sul set completo di hello delle funzioni predefinite in hello linguaggio SQL, consultare troppo[Query Azure Cosmos DB](documentdb-sql-query.md).

<table>
<tr>
  <td><strong>Utilizzo</strong></td>
  <td><strong>Descrizione</strong></td>
</tr>
<tr>
  <td>ST_DISTANCE (spatial_expr, spatial_expr)</td>
  <td>Restituisce la distanza hello tra espressioni di hello due LineString, Polygon o punto GeoJSON.</td>
</tr>
<tr>
  <td>ST_WITHIN (spatial_expr, spatial_expr)</td>
  <td>Restituisce un'espressione booleana che indica se hello prima GeoJSON oggetto (punto, poligono o LineString) all'interno di hello secondo GeoJSON oggetto (punto, poligono o LineString).</td>
</tr>
<tr>
  <td>ST_INTERSECTS (spatial_expr, spatial_expr)</td>
  <td>Restituisce un'espressione booleana che indica se si intersecano hello due GeoJSON oggetti specificati (punto, poligono o LineString).</td>
</tr>
<tr>
  <td>ST_ISVALID</td>
  <td>Restituisce un valore booleano che indica se hello LineString, Polygon o punto GeoJSON espressione è valida.</td>
</tr>
<tr>
  <td>ST_ISVALIDDETAILED</td>
  <td>Restituisce un valore JSON che contiene un valore booleano se hello specificato LineString, Polygon o punto GeoJSON espressione sia valido e se non è valido, è inoltre hello motivo come valore stringa.</td>
</tr>
</table>

Le funzioni spaziali possono essere utilizzati tooperform prossimità query sui dati spaziali. Ad esempio, ecco una query che restituisce che tutti i prodotti della famiglia di documenti che è all'interno di 30 km di hello posizione specificata usando hello ST_DISTANCE funzione predefinita. 

**Query**

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

**Risultati**

    [{
      "id": "WakefieldFamily"
    }]

Se si include l'indicizzazione spaziale nei criteri di indicizzazione, quindi "query di distanza" verrà utilizzata in modo efficiente tramite indice hello. Per ulteriori informazioni sugli indici spaziali, vedere sezione hello riportata di seguito. Se non è un indice per hello percorsi specificati, è comunque possibile eseguire le query spaziali specificando `x-ms-documentdb-query-enable-scan` impostare l'intestazione di richiesta con valore hello troppo "true". In .NET, questo scopo è possibile passare hello facoltativo **FeedOptions** tooqueries argomento con [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) impostare tootrue. 

ST_WITHIN può essere utilizzato toocheck se si trova un punto all'interno di un poligono. Poligoni sono, in genere limiti toorepresent usato come formazioni naturale, i limiti di stato o i codici postali zip. Nuovo se si include l'indicizzazione spaziale nei criteri di indicizzazione, quindi "all'interno di" query verrà utilizzata in modo efficiente tramite indice hello. 

Argomenti poligono ST_WITHIN possono contenere solo un anello singolo, ad esempio hello poligoni non deve contenere fori in essi contenuti. 

**Query**

    SELECT * 
    FROM Families f 
    WHERE ST_WITHIN(f.location, {
        'type':'Polygon', 
        'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
    })

**Risultati**

    [{
      "id": "WakefieldFamily",
    }]

> [!NOTE]
> Tipi simili di mancata corrispondenza toohow funziona in Azure Cosmos DB query, se hello percorso specificato l'argomento non è corretto o non valido, quindi viene valutata troppo**definito** e toobe documento hello valutata ignorati da hello risultati della query. Se la query non restituisce alcun risultato, eseguire toodebug ST_ISVALIDDETAILED perché hello spatail tipo non è valido.     
> 
> 

DB Cosmos Azure supporta inoltre l'esecuzione di query inversa, ad esempio, è possibile indicizzare poligoni o righe nel database di Azure Cosmos, quindi eseguire una query per le aree di hello che contengono un punto specificato. Questo modello viene comunemente usato in logistica tooidentify ad esempio, quando un autocarro entra o esce da un'area designata. 

**Query**

    SELECT * 
    FROM Areas a 
    WHERE ST_WITHIN({'type': 'Point', 'coordinates':[31.9, -4.8]}, a.location)


**Risultati**

    [{
      "id": "MyDesignatedLocation",
      "location": {
        "type":"Polygon", 
        "coordinates": [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
      }
    }]

ST_ISVALID e ST_ISVALIDDETAILED possono essere utilizzati toocheck se un oggetto spaziale è valido. Ad esempio, hello seguente query controlla la validità di hello di un punto con un timeout del valore di latitudine intervallo (-132.8). ST_ISVALID restituisce solo un valore booleano, e restituisce ST_ISVALIDDETAILED hello booleani e una stringa che contiene il motivo di hello perché è considerato non valido.

** Query **

    SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })

**Risultati**

    [{
      "$1": false
    }]

Queste funzioni possono essere utilizzati toovalidate poligoni. Ad esempio, qui utilizziamo ST_ISVALIDDETAILED toovalidate un poligono che non è stato chiuso. 

**Query**

    SELECT ST_ISVALIDDETAILED({ "type": "Polygon", "coordinates": [[ 
        [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] 
        ]]})

**Risultati**

    [{
       "$1": { 
            "valid": false, 
            "reason": "hello Polygon input is not valid because hello start and end points of hello ring number 1 are not hello same. Each ring of a Polygon must have hello same start and end points." 
          }
    }]

### <a name="linq-querying-in-hello-net-sdk"></a>Esecuzione di query LINQ in hello .NET SDK
Hello, DocumentDB .NET SDK anche provider stub metodi `Distance()` e `Within()` per l'utilizzo all'interno di espressioni LINQ. provider LINQ DocumentDB Hello converte queste metodo chiama toohello equivalente SQL chiamate alle funzioni predefinite (ST_DISTANCE e ST_WITHIN rispettivamente). 

Ecco un esempio di una query LINQ che consente di trovare tutti i documenti nella raccolta di Azure Cosmos DB hello è il cui valore di "location" entro un raggio di 30km di hello specificato punto utilizzando LINQ.

**Query LINQ per Distance**

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(u => u.ProfileType == "Public" && a.Location.Distance(new Point(32.33, -4.66)) < 30000))
    {
        Console.WriteLine("\t" + user);
    }

Analogamente, ecco una query per trovare tutti i documenti hello cui "location" è all'interno di hello specificato casella/poligono. 

**Query LINQ per Within**

    Polygon rectangularArea = new Polygon(
        new[]
        {
            new LinearRing(new [] {
                new Position(31.8, -5),
                new Position(32, -5),
                new Position(32, -4.7),
                new Position(31.8, -4.7),
                new Position(31.8, -5)
            })
        });

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(a => a.Location.Within(rectangularArea)))
    {
        Console.WriteLine("\t" + user);
    }


Ora che sono state utilizzate descritto tooquery documenti utilizzando LINQ e SQL, esaminiamo come tooconfigure DB Cosmos Azure per l'indicizzazione spaziale.

## <a name="indexing"></a>Indicizzazione
Come descritto in hello [Schema indipendente dall'indicizzazione con Azure Cosmos DB](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) carta, sono state progettate toobe motore di database del database di Azure Cosmos realmente indipendente di schema e forniscono un supporto eccellente per JSON. motore di database con ottimizzazione per la scrittura di Hello di Azure Cosmos DB a livello nativo riconosce i dati spaziali (punta, poligoni e linee) rappresentati nello standard GeoJSON hello.

In breve, geometry hello viene proiettato da coordinate geodetico su un piano 2D quindi suddiviso progressivamente in celle utilizzando un **quadtree**. Queste celle vengono mappate too1D in base alla posizione di hello della cella hello all'interno di un **curva di riempimento dello spazio di Hilbert**, che consente di mantenere la località di punti. Inoltre quando i dati sulla località sono indicizzati, passano attraverso un processo noto come **a mosaico**, vale a dire tutte hello le celle che intersecano una posizione vengono identificate e archiviate come chiavi di indice di hello Azure Cosmos DB. In fase di query argomenti quali punti e poligoni sono anche tooextract mosaico hello degli intervalli di ID cella appropriata, quindi tooretrieve dati dall'indice hello utilizzati.

Se si specifica un criterio di indicizzazione che include un indice spaziale per / * (tutti i percorsi), quindi vengono indicizzati tutti i punti di presente all'interno di raccolta hello per le query spaziali efficiente (ST_WITHIN e ST_DISTANCE). Gli indici spaziali non hanno un valore di precisione e utilizzano sempre un valore di precisione predefinito.

> [!NOTE]
> Azure Cosmos DB supporta l'indicizzazione automatica dei tipi di dati Point, Polygon e LineString.
> 
> 

Hello frammento di codice JSON seguente mostra un criterio di indicizzazione con abilitata l'indicizzazione spaziale, vale a dire qualsiasi punto GeoJSON trovato all'interno dei documenti per le query spaziali di indice. Se si modifica hello hello portale di Azure tramite criteri di indicizzazione, è possibile specificare hello seguente JSON per l'indicizzazione tooenable criteri spaziali l'indicizzazione nella raccolta.

**JSON criterio di indicizzazione della raccolta con Spatial abilitato per punti e poligoni**

    {
       "automatic":true,
       "indexingMode":"Consistent",
       "includedPaths":[
          {
             "path":"/*",
             "indexes":[
                {
                   "kind":"Range",
                   "dataType":"String",
                   "precision":-1
                },
                {
                   "kind":"Range",
                   "dataType":"Number",
                   "precision":-1
                },
                {
                   "kind":"Spatial",
                   "dataType":"Point"
                },
                {
                   "kind":"Spatial",
                   "dataType":"Polygon"
                }                
             ]
          }
       ],
       "excludedPaths":[
       ]
    }

Di seguito è un frammento di codice in .NET che illustra come una raccolta con l'indicizzazione spaziale toocreate attivata per tutti i percorsi contenenti punti. 

**Creare una raccolta con indicizzazione spaziale**

    DocumentCollection spatialData = new DocumentCollection()
    spatialData.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point)); //override tooturn spatial on by default
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), spatialData);

Di seguito è illustrato come modificare un vantaggio di tootake raccolta esistente di indicizzazione spaziale su tutti i punti che vengono archiviati all'interno dei documenti.

**Modificare una raccolta esistente con l'indicizzazione spaziale**

    Console.WriteLine("Updating collection with spatial indexing enabled in indexing policy...");
    collection.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point));
    await client.ReplaceDocumentCollectionAsync(collection);

    Console.WriteLine("Waiting for indexing toocomplete...");
    long indexTransformationProgress = 0;
    while (indexTransformationProgress < 100)
    {
        ResourceResponse<DocumentCollection> response = await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"));
        indexTransformationProgress = response.IndexTransformationProgress;

        await Task.Delay(TimeSpan.FromSeconds(1));
    }

> [!NOTE]
> Se il percorso di hello GeoJSON valore all'interno di documento hello è in formato non valido o non valido, quindi non ottenere indicizzata per le query spaziali. È possibile convalidare valori della posizione utilizzando ST_ISVALID e ST_ISVALIDDETAILED.
> 
> Se la definizione della raccolta include una chiave di partizione, non viene segnalato lo stato di avanzamento della trasformazione dell'indicizzazione. 
> 
> 

## <a name="next-steps"></a>Passaggi successivi
Ora che è stata apprese sull'avvio tooget con supporto geospaziali in Azure Cosmos DB, è possibile:

* Avviare la codifica con hello [esempi di codice Geospatial .NET su GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)
* Ottenere mani nei con geospatial query in hello [Azure Cosmos DB Query Playground](http://www.documentdb.com/sql/demo#geospatial)
* Altre informazioni sulle [query di Azure Cosmos DB](documentdb-sql-query.md)
* Altre informazioni sui [criteri di indicizzazione di Azure Cosmos DB](indexing-policies.md)

