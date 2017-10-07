---
title: "Cosmos Azure DB: Attività di sviluppo hello API Graph in .NET | Documenti Microsoft"
description: Informazioni su come toodevelop con l'API DocumentDB Azure Cosmos DB usando .NET
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: cc8df0be-672b-493e-95a4-26dd52632261
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: denlee
ms.custom: mvc
ms.openlocfilehash: 12e435d8169aeee6e818dac4a3b66c7a0ec5f2d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-develop-with-hello-graph-api-in-net"></a>Cosmos Azure DB: Attività di sviluppo hello API Graph in .NET
Azure Cosmos DB è il servizio di database di Microsoft multimodello distribuito a livello globale. Creare rapidamente e query chiave/valore, il documento e database grafico, ognuno dei quali trarre vantaggio dalla distribuzione globale hello e funzionalità di scalabilità orizzontale di base di Azure Cosmos DB hello. 

Questa esercitazione viene illustrato come toocreate un account Azure Cosmos DB usando hello portale di Azure e come toocreate un database di grafico e un contenitore. quindi, l'applicazione Hello crea un social network semplice con quattro utenti che utilizzano hello [API Graph](graph-sdk-dotnet.md) (anteprima), quindi consente di scorrere e grafico hello Gremlin utilizzando una query.

Questa esercitazione sono trattati hello seguenti attività:

> [!div class="checklist"]
> * Creare un account Azure Cosmos DB 
> * Creare un contenitore e un database di grafi
> * Serializzare oggetti too.NET vertici e bordi
> * Aggiungere vertici e archi
> * Grafico di query hello utilizzando Gremlin

## <a name="graphs-in-azure-cosmos-db"></a>Grafi in Azure Cosmos DB
È possibile utilizzare Azure Cosmos DB toocreate, update e grafici delle query tramite hello [Microsoft.Azure.Graphs](graph-sdk-dotnet.md) libreria. libreria Microsoft.Azure.Graph Hello fornisce un metodo di estensione singolo `CreateGremlinQuery<T>` sopra hello `DocumentClient` classe query Gremlin tooexecute.

Il linguaggio di programmazione funzionale Gremlin supporta operazioni di scrittura (DML) e le operazioni di query e attraversamento. Trattati alcuni esempi in questo articolo di tooget i primi passi Gremlin. Vedere [Query di Gremlin](gremlin-support.md) per una procedura dettagliata delle funzionalità Gremlin disponibili in Azure Cosmos DB. 

## <a name="prerequisites"></a>Prerequisiti
Assicurarsi di avere hello segue:

* Un account Azure attivo. Se non si ha un account, è possibile iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/free/). 
    * In alternativa, è possibile utilizzare hello [emulatore di Azure DocumentDB](local-emulator.md) per questa esercitazione.
* [Visual Studio](http://www.visualstudio.com/)

## <a name="create-database-account"></a>Creare un account di database

Iniziamo mediante la creazione di un account Azure Cosmos DB in hello portale di Azure.  

> [!TIP]
> * È stato già creato un account Azure Cosmos DB? In caso affermativo, andare troppo[configurazione della soluzione di Visual Studio](#SetupVS)
> * Si dispone di un account Azure DocumentDB? Se in tal caso, l'account è un account Azure Cosmos DB ed è possibile andare troppo[configurazione della soluzione di Visual Studio](#SetupVS).  
> * Se si utilizza hello Azure Cosmos DB emulatore, eseguire le operazioni di hello in [emulatore di Azure Cosmos DB](local-emulator.md) toosetup hello emulatore e andare troppo[configurare la soluzione di Visual Studio](#SetupVS). 
>
> 

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a id="SetupVS"></a>Configurare la soluzione di Visual Studio
1. Aprire **Visual Studio** nel computer.
2. In hello **File** dal menu **New**, quindi scegliere **progetto**.
3. In hello **nuovo progetto** finestra di dialogo Seleziona **modelli** / **Visual c#** / **applicazione Console (.NET Framework)**, denominare il progetto e quindi fare clic su **OK**.
4. In hello **Esplora**, fare clic con il pulsante destro sulla nuova applicazione console, ovvero in una soluzione di Visual Studio, e quindi fare clic su **Gestisci pacchetti NuGet...**
5. In hello **NuGet** scheda, fare clic su **Sfoglia**e il tipo **Microsoft.Azure.Graphs** nella casella di ricerca hello e controllo hello **includono le versioni non definitive**.
6. All'interno dei risultati di hello, trovare **Microsoft.Azure.Graphs** e fare clic su **installare**.
   
   Se viene visualizzato un messaggio sull'esaminato soluzione toohello modifiche, fare clic su **OK**. Se viene visualizzato un messaggio sull'accettazione della licenza, fare clic su **Accetto**.
   
    Hello `Microsoft.Azure.Graphs` libreria fornisce un metodo di estensione singolo `CreateGremlinQuery<T>` per l'esecuzione di operazioni Gremlin. Il linguaggio di programmazione funzionale Gremlin supporta operazioni di scrittura (DML) e le operazioni di query e attraversamento. Trattati alcuni esempi in questo articolo di tooget i primi passi Gremlin. [Query Gremlin](gremlin-support.md) include una procedura dettagliata delle funzionalità di Gremlin in Azure Cosmos DB.

## <a id="add-references"></a>Connessione dell'app

Aggiungere queste due costanti e la variabile *client* nell'applicazione. 

```csharp
string endpoint = ConfigurationManager.AppSettings["Endpoint"]; 
string authKey = ConfigurationManager.AppSettings["AuthKey"]; 
``` 
Successivamente, head nuovamente toohello [portale di Azure](https://portal.azure.com) tooretrieve l'URL dell'endpoint e la chiave primaria. URL dell'endpoint Hello e la chiave primaria sono necessari per l'applicazione toounderstand in tooconnect e per Azure Cosmos DB tootrust connessione dell'applicazione. 

In hello portale di Azure passare tooyour Azure Cosmos DB account, fare clic su **chiavi**, quindi fare clic su **le chiavi di lettura / scrittura**. 

Copiare hello URI dal portale di hello e incollarla su `Endpoint` nella proprietà endpoint hello precedente. Quindi copia hello chiave primaria dal portale hello e incollarlo in hello `AuthKey` proprietà precedente. 

! [Cattura di schermata del portale di Azure hello utilizzato da toocreate esercitazione hello un'applicazione c#. Mostra un hello account Azure Cosmos DB pulsante CHIAVI evidenziato nella hello Azure Cosmos DB spostamento e i valori URI e chiave primaria di hello evidenziati in hello pannello chiavi] [chiavi] 
 
## <a id="instantiate"></a>Creare un'istanza di hello DocumentClient 
Successivamente, creare una nuova istanza di hello **DocumentClient**.  

```csharp 
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey); 
``` 

## <a id="create-database"></a>Creare un database 

A questo punto, creare un database di Azure Cosmos [database](documentdb-resources.md#databases) utilizzando hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) metodo o [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) metodo hello  **DocumentClient** classe da hello [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).  

```csharp 
Database database = await client.CreateDatabaseIfNotExistsAsync(new Database { Id = "graphdb" }); 
``` 
 
## <a name="create-a-graph"></a>Creare un grafo 

Successivamente, creare un contenitore grafico con hello utilizzando hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) metodo o [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) metodo hello **DocumentClient**  classe. Una raccolta è un contenitore di entità di grafi. 

```csharp 
DocumentCollection graph = await client.CreateDocumentCollectionIfNotExistsAsync( 
    UriFactory.CreateDatabaseUri("graphdb"), 
    new DocumentCollection { Id = "graphcollz" }, 
    new RequestOptions { OfferThroughput = 1000 }); 
``` 

## <a id="serializing"></a>Serializzare oggetti too.NET vertici e bordi
Azure DB Cosmos utilizza hello [formato wire GraphSON](gremlin-support.md), che definisce uno schema JSON per vertici, bordi e le proprietà. In questo modo tooserialize/deserializzare GraphSON in oggetti .NET che è possibile utilizzare nel codice Hello Azure Cosmos DB .NET SDK include JSON.NET come dipendenza.

Ad esempio, è possibile usare una social network semplice con quattro utenti. Viene illustrato come toocreate `Person` vertici, aggiungere `Knows` relazioni tra di essi, quindi eseguire una query e attraversare le relazioni di hello grafico toofind "friend di friend". 

Hello `Microsoft.Azure.Graphs.Elements` spazio dei nomi fornisce `Vertex`, `Edge`, `Property` e `VertexProperty` classi per la deserializzazione di oggetti .NET definiti toowell di GraphSON le risposte.

## <a name="run-gremlin-using-creategremlinquery"></a>Eseguire Gremlin usando CreateGremlinQuery
Gremlin, come SQL, supporta le operazioni di lettura, scrittura e le query. Ad esempio, hello frammento di codice seguente mostra come toocreate vertici, bordi, eseguono alcune query di esempio utilizzando `CreateGremlinQuery<T>`e scorrere in modo asincrono da questi risultati tramite `ExecuteNextAsync` e ' HasMoreResults.

```cs
Dictionary<string, string> gremlinQueries = new Dictionary<string, string>
{
    { "Cleanup",        "g.V().drop()" },
    { "AddVertex 1",    "g.addV('person').property('id', 'thomas').property('firstName', 'Thomas').property('age', 44)" },
    { "AddVertex 2",    "g.addV('person').property('id', 'mary').property('firstName', 'Mary').property('lastName', 'Andersen').property('age', 39)" },
    { "AddVertex 3",    "g.addV('person').property('id', 'ben').property('firstName', 'Ben').property('lastName', 'Miller')" },
    { "AddVertex 4",    "g.addV('person').property('id', 'robin').property('firstName', 'Robin').property('lastName', 'Wakefield')" },
    { "AddEdge 1",      "g.V('thomas').addE('knows').to(g.V('mary'))" },
    { "AddEdge 2",      "g.V('thomas').addE('knows').to(g.V('ben'))" },
    { "AddEdge 3",      "g.V('ben').addE('knows').to(g.V('robin'))" },
    { "UpdateVertex",   "g.V('thomas').property('age', 44)" },
    { "CountVertices",  "g.V().count()" },
    { "Filter Range",   "g.V().hasLabel('person').has('age', gt(40))" },
    { "Project",        "g.V().hasLabel('person').values('firstName')" },
    { "Sort",           "g.V().hasLabel('person').order().by('firstName', decr)" },
    { "Traverse",       "g.V('thomas').outE('knows').inV().hasLabel('person')" },
    { "Traverse 2x",    "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')" },
    { "Loop",           "g.V('thomas').repeat(out()).until(has('id', 'robin')).path()" },
    { "DropEdge",       "g.V('thomas').outE('knows').where(inV().has('id', 'mary')).drop()" },
    { "CountEdges",     "g.E().count()" },
    { "DropVertex",     "g.V('thomas').drop()" },
};

foreach (KeyValuePair<string, string> gremlinQuery in gremlinQueries)
{
    Console.WriteLine($"Running {gremlinQuery.Key}: {gremlinQuery.Value}");

    // hello CreateGremlinQuery method extensions allow you tooexecute Gremlin queries and iterate
    // results asychronously
    IDocumentQuery<dynamic> query = client.CreateGremlinQuery<dynamic>(graph, gremlinQuery.Value);
    while (query.HasMoreResults)
    {
        foreach (dynamic result in await query.ExecuteNextAsync())
        {
            Console.WriteLine($"\t {JsonConvert.SerializeObject(result)}");
        }
    }

    Console.WriteLine();
}
```

## <a name="add-vertices-and-edges"></a>Aggiungere vertici e archi

Esaminare le istruzioni Gremlin hello mostrate nella precedente sezione hello maggiori dettagli. Prima si aggiungono vertici usando il metodo `addV` Gremlin. Ad esempio, hello frammento di codice seguente crea un vertice "Thomas Andersen" di tipo "Person", con le proprietà per nome, cognome ed età.

```cs
// Create a vertex
IDocumentQuery<Vertex> createVertexQuery = client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.addV('person').property('firstName', 'Thomas')");

while (createVertexQuery.HasMoreResults)
{
    Vertex thomas = (await create.ExecuteNextAsync<Vertex>()).First();
}
```

Creare quindi alcuni archi tra i vertici usando il metodo `addE` Gremlin. 

```cs
// Add a "knows" edge
IDocumentQuery<Edge> createEdgeQuery = client.CreateGremlinQuery<Edge>(
    graphCollection, 
    "g.V('thomas').addE('knows').to(g.V('mary'))");

while (create.HasMoreResults)
{
    Edge thomasKnowsMaryEdge = (await create.ExecuteNextAsync<Edge>()).First();
}
```

È possibile aggiornare un vertice esistente usando il comando `properties` Gremlin. Vengono ignorate query hello di hello chiamata tooexecute tramite `HasMoreResults` e `ExecuteNextAsync` per rest hello degli esempi di hello.

```cs
// Update a vertex
client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.V('thomas').property('age', 45)");
```

È possibile trascinare gli archi e i vertici usando il comando `drop` Gremlin. Di seguito è riportato un frammento che mostra come toodelete vertice e un bordo. Si noti che l'eliminazione di un vertice esegue un'eliminazione a catena di hello associati bordi.

```cs
// Drop an edge
client.CreateGremlinQuery(graphCollection, "g.E('thomasKnowsRobin').drop()");

// Drop a vertex
client.CreateGremlinQuery(graphCollection, "g.V('robin').drop()");
```

## <a name="query-hello-graph"></a>Grafico di query hello

È possibile anche eseguire operazioni di query e attraversamento usando Gremlin. Ad esempio, hello frammento di codice seguente viene illustrato come toocount hello numero di vertici nel grafico hello:

```cs
// Run a query toocount vertices
IDocumentQuery<int> countQuery = client.CreateGremlinQuery<int>(graphCollection, "g.V().count()");
```
È possibile eseguire filtri utilizzando Gremlin `has` e `hasLabel` i passaggi e combinarli con `and`, `or`, e `not` toobuild più complessa di filtri:

```cs
// Run a query with filter
IDocumentQuery<Vertex> personsByAge = client.CreateGremlinQuery<Vertex>(
  graphCollection, 
  "g.V().hasLabel('person').has('age', gt(40))");
```

È possibile proiettare determinate proprietà nei risultati della query hello utilizzando hello `values` passaggio:

```cs
// Run a query with projection
IDocumentQuery<string> firstNames = client.CreateGremlinQuery<string>(
  graphCollection, 
  $"g.V().hasLabel('person').values('firstName')");
```

Finora sono stati esaminati solo gli operatori di query che è possibile usare in qualsiasi database. Grafici sono veloci ed efficienti per le operazioni di attraversamento quando è necessario toonavigate toorelated bordi e i vertici. Verranno ora individuati tutti gli amici di Thomas. Facciamo utilizzando del Gremlin `outE` passaggio toofind hello tutti i bordi in uscita da Thomas, quindi attraversamento toohello in vertici da tali usando del Gremlin `inV` passaggio:

```cs
// Run a traversal (find friends of Thomas)
IDocumentQuery<Vertex> friendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person')");
```

la query successiva Hello esegue due hop toofind tutti "agli amici di Thomas di amici", chiamando `outE` e `inV` due volte. 

```cs
// Run a traversal (find friends of friends of Thomas)
IDocumentQuery<Vertex> friendsOfFriendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')");
```

È possibile compilare query più complesse e implementare la logica di attraversamento potente grafico utilizzando Gremlin, tra cui filtro combinazione espressioni, esecuzione di ciclo tramite hello `loop` passaggio e la navigazione condizionale implementazione utilizzando hello `choose` passaggio. Altre informazioni sulle operazioni che è possibile eseguire con il [supporto per Gremlin](gremlin-support.md).

L'esercitazione di Azure Cosmos DB è stata completata. 

## <a name="clean-up-resources"></a>Pulire le risorse

Se non si ha intenzione toocontinue toouse questa app, utilizzare hello seguendo i passaggi toodelete tutte le risorse create da questa esercitazione in hello portale di Azure.  

1. Dal menu a sinistra di hello in hello portale di Azure, fare clic su **gruppi di risorse** e quindi fare clic su nome hello della risorsa di hello è stato creato. 
2. Nella pagina di gruppo di risorse, fare clic su **eliminare**, digitare il nome di hello di hello risorsa toodelete nella casella di testo hello e quindi fare clic su **eliminare**.

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione, effettuata seguente hello:

> [!div class="checklist"]
> * Creazione di un account Azure Cosmos DB 
> * Creazione di un contenitore e un database di grafi
> * Oggetti too.NET vertici e bordi serializzati
> * Aggiunta di vertici e archi
> * Grafico di query hello mediante Gremlin

È ora possibile creare query più complesse e implementare la potente logica di attraversamento dei grafi usando Gremlin. 

> [!div class="nextstepaction"]
> [Eseguire query con Gremlin](tutorial-query-graph.md)
