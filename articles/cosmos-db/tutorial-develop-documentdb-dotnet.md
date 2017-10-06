---
title: "Cosmos Azure DB: Attività di sviluppo hello API DocumentDB in .NET | Documenti Microsoft"
description: Informazioni su come toodevelop con l'API DocumentDB Azure Cosmos DB usando .NET
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: mimig
ms.custom: mvc
ms.openlocfilehash: 0d3d17afa782054c8fdf3cbac421e5a5d0a6800c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmosdb-develop-with-hello-documentdb-api-in-net"></a>Azure CosmosDB: Sviluppare con hello API DocumentDB in .NET

Azure Cosmos DB è il servizio di database multimodello distribuito a livello globale di Microsoft. Creare rapidamente e query chiave/valore, il documento e database grafico, ognuno dei quali trarre vantaggio dalla distribuzione globale hello e funzionalità di scalabilità orizzontale di base di Azure Cosmos DB hello. 

Questa esercitazione viene illustrato come toocreate un account Azure Cosmos DB usando hello portale di Azure e quindi creare un database di documenti e una raccolta con un [chiave di partizione](documentdb-partition-data.md#partition-keys) utilizzando hello [API .NET di DocumentDB](documentdb-introduction.md). Definendo una chiave di partizione quando si crea una raccolta, l'applicazione è pronta tooscale facilmente alla crescita dei dati. 

Seguito hello esercitazione vengono illustrate le attività tramite hello [API .NET di DocumentDB](documentdb-sdk-dotnet.md):

> [!div class="checklist"]
> * Creare un account Azure Cosmos DB
> * Creare una raccolta e un database con una chiave di partizione
> * Creare documenti JSON
> * Aggiornare un documento
> * Eseguire query su raccolte partizionate
> * Eseguire stored procedure
> * Eliminare un documento
> * Eliminare un database

## <a name="prerequisites"></a>Prerequisiti
Assicurarsi di avere hello segue:

* Un account Azure attivo. Se non si ha un account, è possibile iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/free/). 
    * In alternativa, è possibile utilizzare hello [Azure Cosmos DB emulatore](local-emulator.md) per questa esercitazione, se si desidera toouse un ambiente locale che emula il servizio di Azure DocumentDB hello per scopi di sviluppo.
* [Visual Studio](http://www.visualstudio.com/)

## <a name="create-an-azure-cosmos-db-account"></a>Creare un account Azure Cosmos DB

Iniziamo mediante la creazione di un account Azure Cosmos DB in hello portale di Azure.

> [!TIP]
> * È stato già creato un account Azure Cosmos DB? In caso affermativo, andare troppo[configurazione della soluzione di Visual Studio](#SetupVS)
> * Si dispone di un account Azure DocumentDB? Se in tal caso, l'account è un account Azure Cosmos DB ed è possibile andare troppo[configurazione della soluzione di Visual Studio](#SetupVS).  
> * Se si utilizza hello Azure Cosmos DB emulatore, eseguire le operazioni di hello in [emulatore di Azure Cosmos DB](local-emulator.md) toosetup hello emulatore e andare troppo[configurare la soluzione di Visual Studio](#SetupVS). 
>
>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupVS"></a>Configurare la soluzione di Visual Studio
1. Aprire **Visual Studio** nel computer.
2. In hello **File** dal menu **New**, quindi scegliere **progetto**.
3. In hello **nuovo progetto** finestra di dialogo Seleziona **modelli** / **Visual c#** / **applicazione Console (.NET Framework)**, denominare il progetto e quindi fare clic su **OK**.
   ![Cattura di schermata della finestra Nuovo progetto hello](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-new-project-2.png)

4. In hello **Esplora**, fare clic con il pulsante destro sulla nuova applicazione console, ovvero in una soluzione di Visual Studio, e quindi fare clic su **Gestisci pacchetti NuGet...**
    
    ![Cattura di schermata del diritto hello Menu selezionato per hello progetto](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges.png)
5. In hello **NuGet** scheda, fare clic su **Sfoglia**e il tipo **documentdb** nella casella di ricerca hello.
<!---stopped here--->
6. All'interno dei risultati di hello, trovare **Microsoft.Azure.DocumentDB** e fare clic su **installare**.
   ID del pacchetto per la libreria Client di Azure Cosmos DB hello Hello è [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB).
   ![Cattura di schermata di hello NuGet Menu per la ricerca di Azure Cosmos DB Client SDK](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges-2.png)

    Se viene visualizzato un messaggio sull'esaminato soluzione toohello modifiche, fare clic su **OK**. Se viene visualizzato un messaggio sull'accettazione della licenza, fare clic su **Accetto**.

## <a id="Connect"></a>Aggiungere riferimenti tooyour progetto
Hello rimanenti passaggi di questa esercitazione specificare hello API DocumentDB codice frammenti toocreate e aggiornare Azure Cosmos DB risorse necessarie nel progetto.

Innanzitutto, aggiungere tali applicazioni, tooyour riferimenti.
<!---These aren't added by default when you install hello pkg?--->

```csharp
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

## <a id="add-references"></a>Connessione dell'app

Aggiungere quindi queste due costanti e la variabile *client* nell'applicazione.

```csharp
private const string EndpointUrl = "<your endpoint URL>";
private const string PrimaryKey = "<your primary key>";
private DocumentClient client;
```

Head nuovamente toohello [portale di Azure](https://portal.azure.com) tooretrieve l'URL dell'endpoint e la chiave primaria. URL dell'endpoint Hello e la chiave primaria sono necessari per l'applicazione toounderstand in tooconnect e per Azure Cosmos DB tootrust connessione dell'applicazione.

In hello portale di Azure passare tooyour Azure Cosmos DB account, fare clic su **chiavi**, quindi fare clic su **le chiavi di lettura / scrittura**.

Copiare hello URI dal portale di hello e incollarla su `<your endpoint URL>` nel file program.cs hello. Quindi copia hello chiave primaria dal portale hello e incollarla su `<your primary key>`. Essere certi hello tooremove `<` e `>` dai valori.

![Cattura di schermata del portale di Azure hello utilizzato hello NoSQL esercitazione toocreate un'applicazione console c#. Viene illustrato un account Azure Cosmos DB, con CHIAVI evidenziate nel Pannello di account Azure Cosmos DB hello, hello e hello URI e i valori di chiave primaria evidenziati nel Pannello di chiavi hello](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-keys.png)

## <a id="instantiate"></a>Creare un'istanza di hello DocumentClient

A questo punto, creare una nuova istanza di hello **DocumentClient**.

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
```

## <a id="create-database"></a>Creare un database

Successivamente, creare un database di Azure Cosmos [database](documentdb-resources.md#databases) utilizzando hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) metodo o [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) metodo hello  **DocumentClient** classe da hello [DocumentDB .NET SDK](documentdb-sdk-dotnet.md). Un database è contenitore logico di hello di archiviazione di documenti JSON partizionato nelle raccolte.

```csharp
await client.CreateDatabaseAsync(new Database { Id = "db" });
```
## <a name="decide-on-a-partition-key"></a>Scegliere una chiave di partizione 

Le raccolte sono contenitori per l'archiviazione di documenti. Le raccolte sono risorse logiche e possono [comprendere una o più partizioni fisiche](partition-data.md). Oggetto [chiave di partizione](documentdb-partition-data.md) è una proprietà (o percorso) all'interno dei documenti che viene utilizzato toodistribute i dati tra server hello o partizioni. Tutti i documenti con hello stessa chiave di partizione vengono archiviati in hello stessa partizione. 

Individuazione di una chiave di partizione è un'importante decisione toomake prima di creare una raccolta. Le chiavi di partizione sono una proprietà (o percorso) all'interno dei documenti che possono essere utilizzati da Azure Cosmos DB toodistribute i dati tra più server o le partizioni. COSMOS DB genera un hash per valore di chiave di partizione hello e partizione di hello eseguito l'hashing risultato toodetermine hello nella quale documento hello toostore. Tutti i documenti con hello stessa chiave di partizione vengono archiviati nella stessa partizione di hello e le chiavi di partizione non possono essere modificate dopo aver creata una raccolta. 

Per questa esercitazione, si userà la chiave di partizione hello tooset troppo`/deviceId` così che hello tutti i dati di hello per un singolo dispositivo è archiviato in una singola partizione. Si desidera toochoose una chiave di partizione che include un numero elevato di valori, ognuno dei quali vengono utilizzati in su hello stessa frequenza tooensure DB Cosmos possibile bilanciare il carico dei dati cresce e raggiungere una velocità effettiva completo hello dell'insieme di hello. 

Per ulteriori informazioni sul partizionamento, vedere [come toopartition e la scala in Azure Cosmos DB?](partition-data.md) 

## <a id="CreateColl"></a>Creare una raccolta 

Ora che si conosce la chiave di partizione, `/deviceId`, consente di creare un [raccolta](documentdb-resources.md#collections) utilizzando hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) metodo o [ CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) metodo hello **DocumentClient** classe. Una raccolta è un contenitore di documenti JSON e di eventuale logica dell'applicazione JavaScript associata. 

> [!WARNING]
> Creazione di una raccolta ha implicazioni, prezzi che si desidera riservare una velocità effettiva per toocommunicate applicazione hello con Azure Cosmos DB. Per altre informazioni, visitare la [pagina relativa ai prezzi](https://azure.microsoft.com/pricing/details/cosmos-db/).
> 
> 

```csharp
// Collection for device telemetry. Here hello JSON property deviceId is used  
// as hello partition key toospread across partitions. Configured for 2500 RU/s  
// throughput and an indexing policy that supports sorting against any  
// number or string property. .
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 2500 });
```

Metodo lo rende un'API REST chiamare tooAzure DB Cosmos e hello esegue il provisioning del servizio di un numero di partizioni in base alla velocità effettiva richiesta hello. È possibile modificare la velocità effettiva hello di una raccolta necessarie prestazioni più elevate evolvere utilizzando hello SDK o hello [portale di Azure](set-throughput.md).

## <a id="CreateDoc"></a>Creare documenti JSON
Verranno ora inseriti alcuni documenti JSON in Azure Cosmos DB. Oggetto [documento](documentdb-resources.md#documents) possono essere create usando hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) metodo hello **DocumentClient** classe. I documenti sono contenuto JSON definito dall'utente (arbitrario). Questa classe di esempio contiene la lettura di un dispositivo e un tooinsert tooCreateDocumentAsync chiamata di un nuovo dispositivo di lettura in una raccolta.

```csharp
public class DeviceReading
{
    [JsonProperty("id")]
    public string Id;

    [JsonProperty("deviceId")]
    public string DeviceId;

    [JsonConverter(typeof(IsoDateTimeConverter))]
    [JsonProperty("readingTime")]
    public DateTime ReadingTime;

    [JsonProperty("metricType")]
    public string MetricType;

    [JsonProperty("unit")]
    public string Unit;

    [JsonProperty("metricValue")]
    public double MetricValue;
  }

// Create a document. Here hello partition key is extracted 
// as "XMS-0001" based on hello collection definition
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "coll"),
    new DeviceReading
    {
        Id = "XMS-001-FE24C",
        DeviceId = "XMS-0001",
        MetricType = "Temperature",
        MetricValue = 105.00,
        Unit = "Fahrenheit",
        ReadingTime = DateTime.UtcNow
    });
```
## <a name="read-data"></a>Leggere i dati

Di seguito, leggere il documento di hello la chiave di partizione e Id utilizzando il metodo ReadDocumentAsync hello. Si noti che le letture hello includano un valore PartitionKey (toohello corrispondente `x-ms-documentdb-partitionkey` intestazione della richiesta in hello API REST).

```csharp
// Read document. Needs hello partition key and hello Id toobe specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;
```

## <a name="update-data"></a>Aggiornare i dati

Ora consente di aggiornare alcuni dati utilizzando il metodo ReplaceDocumentAsync hello.

```csharp
// Update hello document. Partition key is not required, again extracted from hello document
reading.MetricValue = 104;
reading.ReadingTime = DateTime.UtcNow;

await client.ReplaceDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  reading);
```

## <a name="delete-data"></a>Eliminare i dati

Ora consente di eliminare un documento con chiave di partizione e id utilizzando il metodo DeleteDocumentAsync hello.

```csharp
// Delete a document. hello partition key is required.
await client.DeleteDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```
## <a name="query-partitioned-collections"></a>Eseguire query su raccolte partizionate

Quando si eseguono query dati in raccolte partizionate, Azure Cosmos DB automaticamente le route hello partizioni toohello query corrispondenti valori di chiave partizione toohello specificati nel filtro hello (se presenti). Ad esempio, questa query è indirizzato toojust hello partizione contenente hello chiave di partizione "XMS-0001".

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
Hello query seguente non dispone di un filtro sulla chiave di partizione hello (DeviceId) e viene disposta tooall partizioni in cui viene eseguita sull'indice della partizione hello. Si noti che è necessario toospecify hello EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in hello API REST) toohave hello SDK tooexecute una query tra partizioni.

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

## <a name="parallel-query-execution"></a>Esecuzione di query in parallelo
Hello Azure Cosmos DB DocumentDB SDK alla 1.9.0 e versioni successive supportano opzioni di esecuzione di query parallele, che consentono a bassa latenza tooperform esegue query su raccolte partizionate, anche quando sono necessari tootouch un numero elevato di partizioni. Ad esempio, hello seguente query è configurato toorun in parallelo tra partizioni.

```csharp
// Cross-partition Order By queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
È possibile gestire l'esecuzione parallela di query ottimizzando hello seguenti parametri:

* Impostando `MaxDegreeOfParallelism`, è possibile controllare hello grado di parallelismo, ovvero hello massimo numero di partizioni della raccolta toohello connessioni di rete simultanee. Se si imposta questo troppo-1, livello hello di parallelismo è gestito da hello SDK. Se hello `MaxDegreeOfParallelism` viene omesso o impostato too0, ovvero il valore di predefinito hello, saranno presenti partizioni di rete singola connessione toohello di una raccolta.
* Impostando `MaxBufferedItemCount` è possibile raggiungere un compromesso tra latenza della query e uso della memoria dal lato client. Se si omette questo parametro o impostare troppo-1, numero di hello di elementi memorizzato nel buffer durante l'esecuzione di query parallele è gestito da hello SDK.

Dato hello stesso stato dell'insieme di hello, una query parallela restituisce risultati hello stesso ordine come in esecuzione seriale. Quando si esegue una query tra partizioni che include l'ordinamento (ORDER BY e/o superiore), hello DocumentDB SDK genera query hello in parallelo tra le partizioni e unisce parzialmente ordinato i risultati in hello client side tooproduce risultati ordinati globalmente.

## <a name="execute-stored-procedures"></a>Eseguire stored procedure
Infine, è possibile eseguire le transazioni atomiche sui documenti con hello stesso ID del dispositivo, ad esempio, se si gestiscono le aggregazioni o hello stato più recente di un dispositivo in un unico documento aggiungendo hello progetto tooyour di codice seguente.

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```

L'attività è terminata. Questi sono i componenti principali di hello di un'applicazione Azure Cosmos DB che utilizza una distribuzione di dati di partizione tooefficiently chiave scala tra partizioni.  

## <a name="clean-up-resources"></a>Pulire le risorse

Se non si ha intenzione toocontinue toouse questa app, eliminare tutte le risorse create da questa esercitazione hello portale di Azure con hello alla procedura seguente:

1. Dal menu a sinistra di hello in hello portale di Azure, fare clic su **gruppi di risorse** e quindi fare clic hello nome univoco della risorsa hello è stato creato. 
2. Nella pagina di gruppo di risorse, fare clic su **eliminare**, digitare il nome di hello di hello risorsa toodelete nella casella di testo hello e quindi fare clic su **eliminare**.

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione, effettuata seguente hello: 

> [!div class="checklist"]
> * Creazione di un account Azure Cosmos DB
> * Creazione di una raccolta e un database con una chiave di partizione
> * Creazione di documenti JSON
> * Aggiornamento di un documento
> * Esecuzione di query su raccolte partizionate
> * Esecuzione di una stored procedure
> * Eliminazione di un documento
> * Eliminazione di un database

È possibile continuare l'esercitazione successiva toohello e importare dati aggiuntivi tooyour DB Cosmos account. 

> [!div class="nextstepaction"]
> [Importare dati in Azure Cosmos DB](import-data.md)
