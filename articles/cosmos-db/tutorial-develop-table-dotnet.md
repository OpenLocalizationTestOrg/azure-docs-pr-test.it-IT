---
title: 'Azure Cosmos DB: Sviluppare con API di tabelle in .NET hello | Documenti Microsoft'
description: Informazioni su come toodevelop con API di tabelle del database di Azure Cosmos usando .NET
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 4b22cb49-8ea2-483d-bc95-1172cd009498
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: arramac
ms.custom: mvc
ms.openlocfilehash: 70c6985a1dffdbcdb07e377f8ad10355bb97712a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-develop-with-hello-table-api-in-net"></a>Cosmos Azure DB: Attività di sviluppo hello tabella API in .NET

Azure Cosmos DB è il servizio di database multimodello distribuito a livello globale di Microsoft. Creare rapidamente e query chiave/valore, il documento e database grafico, ognuno dei quali trarre vantaggio dalla distribuzione globale hello e funzionalità di scalabilità orizzontale di base di Azure Cosmos DB hello.

Questa esercitazione sono trattati hello seguenti attività: 

> [!div class="checklist"] 
> * Creare un account Azure Cosmos DB 
> * Abilitare la funzionalità nel file app. config hello 
> * Creare una tabella utilizzando hello [tabella API](table-introduction.md) (anteprima)
> * Aggiungere una tabella tooa entità 
> * Inserire un batch di entità 
> * Recuperare una singola entità 
> * Eseguire query su entità tramite indici secondari automatici 
> * Sostituire un'entità 
> * Eliminare un'entità 
> * Eliminare una tabella
 
## <a name="tables-in-azure-cosmos-db"></a>Tabelle in Azure Cosmos DB 

DB Cosmos Azure fornisce hello [tabella API](table-introduction.md) (anteprima) per applicazioni che richiedono un archivio chiave-valore con una progettazione senza schema. [Archiviazione tabelle di Azure](../storage/common/storage-introduction.md) SDK e API REST possono essere utilizzati toowork con Azure Cosmos DB. È possibile utilizzare le tabelle di Azure Cosmos DB toocreate con requisiti di velocità effettiva elevata. Azure Cosmos DB supporta le tabelle ottimizzate per la velocità effettiva, chiamate in modo informale "tabelle Premium", attualmente disponibili in anteprima pubblica. 

È possibile continuare toouse archiviazione tabelle di Azure per le tabelle con archiviazione elevate e minori requisiti di velocità effettiva. Azure DB Cosmos introduce anche il supporto per le tabelle con ottimizzazione per la memoria in un aggiornamento futuro e tabelle di Azure di nuove ed esistenti saranno facilmente gli account di archiviazione aggiornato tooAzure DB Cosmos.

Se si utilizza archiviazione tabelle di Azure, si otterranno i seguenti vantaggi con anteprima di "tabella premium" hello hello:

- [Distribuzione globale](distribute-data-globally.md) chiavi in mano con multihosting e [failover automatici e manuali](regional-failover.md)
- Supporto per l'indicizzazione automatica indipendente dallo schema su tutte le proprietà ("indici secondari") e query rapide 
- Supporto per la [scalabilità indipendente di archiviazione e velocità effettiva](partition-data.md) in un numero qualsiasi di aree
- Supporto per [velocità effettiva dedicata per ogni tabella](request-units.md) che possono essere scalati da centinaia toomillions di richieste al secondo
- Supporto per [cinque livelli di coerenza ottimizzabili](consistency-levels.md) tootrade off disponibilità, latenza e la coerenza in base alle esigenze dell'applicazione
- disponibilità del 99,99% all'interno di una singola area e possibilità tooadd altre aree per una maggiore disponibilità, e [SLA completi leader del settore](https://azure.microsoft.com/support/legal/sla/cosmos-db/) sulla disponibilità generale
- Utilizzo di archiviazione di Azure esistente hello .NET SDK e nessuna applicazione tooyour modifiche di codice

Durante l'anteprima di hello, Azure Cosmos DB supporta hello API tabelle utilizzando hello .NET SDK. È possibile scaricare hello [anteprima di Azure Storage SDK](https://aka.ms/premiumtablenuget) da NuGet, che ha hello stesse classi e le firme del metodo come hello [Azure Storage SDK](https://www.nuget.org/packages/WindowsAzure.Storage), ma anche possibile connettersi tooAzure DB Cosmos account utilizzando hello Tabella API.

toolearn sulle attività di archiviazione Azure Table complesse, vedere:

* [Introduzione tooAzure DB Cosmos: API di tabella](table-introduction.md)
* la documentazione di riferimento del servizio di tabella per informazioni dettagliate sulle API disponibili Hello [libreria Client di archiviazione per il riferimento di .NET](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)

### <a name="about-this-tutorial"></a>Informazioni sull'esercitazione
Per gli sviluppatori che hanno familiarità con hello archiviazione tabelle di Azure SDK e si desiderano toouse hello premium le funzionalità disponibili in questa esercitazione è utilizzando Azure Cosmos DB. È basato su [Introduzione all'archiviazione tabelle di Azure usando .NET](table-storage-how-to-use-dotnet.md) e Mostra come tootake sfruttare le funzionalità aggiuntive come indici secondari, velocità effettiva di provisioning e multihoming. Viene illustrata la modalità toouse hello toocreate portale Azure un account Azure Cosmos DB, quindi compilare e distribuire un'applicazione di tabella. Verranno esaminati anche esempi .NET per la creazione e l'eliminazione di una tabella, l'inserimento, l'aggiornamento, l'eliminazione e l'esecuzione di query per i dati delle tabelle. 

Se si dispone già di Visual Studio 2017, che installata, è possibile scaricare e utilizzare hello **libero** [2017 di Visual Studio Community Edition](https://www.visualstudio.com/downloads/). Assicurarsi di abilitare **lo sviluppo di Azure** durante l'installazione di Visual Studio hello.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Creare un account di database

Iniziamo mediante la creazione di un account Azure Cosmos DB in hello portale di Azure.  

> [!TIP]
> * È stato già creato un account Azure Cosmos DB? In caso affermativo, andare troppo[configurazione della soluzione di Visual Studio](#SetupVS).
> * Si dispone di un account Azure DocumentDB? Se in tal caso, l'account è un account Azure Cosmos DB ed è possibile andare troppo[configurazione della soluzione di Visual Studio](#SetupVS).  
> * Se si utilizza hello Azure Cosmos DB emulatore, eseguire le operazioni di hello in [emulatore di Azure Cosmos DB](local-emulator.md) toosetup hello emulatore e andare troppo[configurare la soluzione di Visual Studio](#SetupVS).
<!---Loc Comment: Please, check link [Set up your Visual Studio solution] since it's not redirecting tooany location.---> 
>
>

[!INCLUDE [cosmosdb-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)] 

## <a name="clone-hello-sample-application"></a>Applicazione di esempio hello clonare

Ora si clonare un'app di tabella da github, impostare la stringa di connessione hello ed eseguirlo.

1. Aprire una finestra terminale git, ad esempio git bash, e `cd` tooa directory di lavoro.  

2. Eseguire hello seguenti repository di esempio di comando tooclone hello. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started
    ```

3. Aprire quindi il file di soluzione hello in Visual Studio.

## <a name="update-your-connection-string"></a>Aggiornare la stringa di connessione

Tornare toohello tooget portale Azure le informazioni sulla stringa di connessione e copiarla in app hello.

1. In hello [portale di Azure](http://portal.azure.com/)il Cosmos Azure DB account, nel riquadro di spostamento sinistro hello fare clic su **chiavi**, quindi fare clic su **le chiavi di lettura / scrittura**. Si userà pulsanti copia hello sul lato destro hello hello schermata toocopy hello della stringa di connessione nel file app. config hello nel passaggio successivo hello.

2. In Visual Studio, aprire il file app. config hello. 

3. Copiare il valore dell'URI dal portale di hello (con il pulsante di copia hello) e renderlo hello valore della chiave account hello in App. config. Utilizzare il nome di account hello creato in precedenza per il nome di account in App. config.
  
```
<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;TableEndpoint=https://account-name.documents.azure.com" />
```

> [!NOTE]
> toouse questa app con l'archiviazione tabelle di Azure standard, è necessario toochange hello stringa di connessione `app.config file`. Usa il nome di account di hello come nome dell'account di tabella e la chiave come chiave primaria di archiviazione di Azure. <br>
>`<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;EndpointSuffix=core.windows.net" />`
> 
>

## <a name="build-and-deploy-hello-app"></a>Compilare e distribuire l'applicazione hello
1. In Visual Studio, fare clic su progetto hello in **Esplora** e quindi fare clic su **Gestisci pacchetti NuGet**. 

2. In hello NuGet **Sfoglia** digitare ***Windowsazure PremiumTable***. Selezionare **Includi versione preliminare**.

3. Dai risultati di hello, installare hello **Windowsazure PremiumTable** e scegliere una build di anteprima hello `0.0.1-preview`. Questa azione Installa pacchetto di archiviazione Azure Table hello e tutte le dipendenze.

4. Premere CTRL + F5 applicazione hello toorun. 

È ora possibile tornare tooData Explorer e vedere query, modificare e lavorare con i dati nella tabella. 

> [!NOTE]
> toouse toochange hello stringa di connessione è necessario che l'app con un emulatore DB Cosmos di Azure, è sufficiente `app.config file`. Hello utilizzare sotto il valore per l'emulatore. <br>
>`<add key="StorageConnectionString" value=DefaultEndpointsProtocol=https;AccountName=localhost;AccountKey=<insertkey>==;TableEndpoint=https://localhost -->`
> 
>

## <a name="azure-cosmos-db-capabilities"></a>Funzionalità di Azure Cosmos DB
DB Cosmos Azure supporta un numero di funzionalità che non sono disponibili nell'API di archiviazione Azure Table hello. Hello nuova funzionalità può essere abilitata tramite il seguente hello `appSettings` i valori di configurazione. Non si introdurre qualsiasi nuovo firme di overload toohello anteprima o Azure Storage SDK. In questo modo si tooconnect tooboth standard e premium tabelle e lavoro con altri servizi di archiviazione di Azure come BLOB e code. 


| Chiave | Descrizione |
| --- | --- |
| TableConnectionMode  | Azure Cosmos DB supporta due modalità di connettività. In `Gateway` modalità, le richieste vengono inviate sempre toohello DB Cosmos Azure gateway, che inoltra toohello partizioni di dati corrispondente. In `Direct` modalità di connettività client hello recupera i mapping di hello di toopartitions di tabelle e le richieste vengono effettuate direttamente per le partizioni di dati. È consigliabile `Direct`, hello predefinito.  |
| TableConnectionProtocol | Azure Cosmos DB supporta due protocolli di connessione: `Https` e `Tcp`. `Tcp`hello predefinito e consigliato perché è più semplice. |
| TablePreferredLocations | Elenco delimitato da virgole dei percorsi (multihosting) preferiti per le letture. Ogni account Azure Cosmos DB può essere associato a 1-30+ aree. Ogni istanza del client è possibile specificare un subset di queste aree nell'ordine preferito hello per le letture di bassa latenza. aree Hello devono essere denominate con i relativi [i nomi visualizzati](https://msdn.microsoft.com/library/azure/gg441293.aspx), ad esempio, `West US`. Vedere anche [API multihosting](tutorial-global-distribution-table.md).
| TableConsistencyLevel | È possibile ottenere un compromesso ottimale tra disponibilità, coerenza e latenza scegliendo tra cinque livelli di coerenza ben definiti: `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix` ed `Eventual`. Il valore predefinito è `Session`. scelta di Hello del livello di coerenza rende una differenza significativa nelle installazioni con più aree. Per i dettagli, vedere [Livelli di coerenza](consistency-levels.md). |
| TableThroughput | Velocità effettiva riservati per la tabella hello espressa in unità di richiesta (RU) al secondo. Le singole tabelle possono supportare centinaia di milioni di UR/s. Vedere [Unità richiesta](request-units.md). Il valore predefinito è `400` |
| TableIndexingPolicy | Indicizzazione secondaria coerente e automatica di tutte le colonne all'interno di tabelle | JSON stringa conforme toohello specifica di criteri di indicizzazione. Vedere [criteri di indicizzazione](indexing-policies.md) toosee come è possibile modificare l'indicizzazione di colonne specifiche dei criteri di tooinclude/exclude. | Indicizzazione automatica di tutte le proprietà (hash per le stringhe e range per i numeri) |
| TableQueryMaxItemCount | Configurare hello il numero massimo di elementi restituiti per ogni query di tabella in un unico round trip. Valore predefinito è `-1`, che consente di determinare in modo dinamico il valore di hello in fase di esecuzione Azure Cosmos DB. |
| TableQueryEnableScan | Se query hello non è possibile utilizzare indice hello per qualsiasi filtro, quindi eseguirlo comunque tramite un'analisi. Il valore predefinito è `false`.|
| TableQueryMaxDegreeOfParallelism | Hello grado di parallelismo per l'esecuzione di una query tra partizioni. `0`seriale con nessun recupero preliminare, `1` seriale con la prelettura e i valori più elevati di velocità di aumento hello di parallelismo. Valore predefinito è `-1`, che consente di determinare in modo dinamico il valore di hello in fase di esecuzione Azure Cosmos DB. |

valore predefinito di hello toochange, aprire hello `app.config` file da Esplora soluzioni in Visual Studio. Aggiungere contenuto hello di hello `<appSettings>` elemento riportato di seguito. Sostituire `account-name` con nome hello dell'account di archiviazione, e `account-key` con la chiave di accesso di account. 

```xml
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
    </startup>
    <appSettings>
      <!-- Client options -->
      <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key; TableEndpoint=https://account-name.documents.azure.com" />
      <add key="TableConnectionMode" value="Direct"/>
      <add key="TableConnectionProtocol" value="Tcp"/>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>
      <add key="TableConsistencyLevel" value="Eventual"/>

      <!--Table creation options -->
      <add key="TableThroughput" value="700"/>
      <add key="TableIndexingPolicy" value="{""indexingMode"": ""Consistent""}"/>

      <!-- Table query options -->
      <add key="TableQueryMaxItemCount" value="-1"/>
      <add key="TableQueryEnableScan" value="false"/>
      <add key="TableQueryMaxDegreeOfParallelism" value="-1"/>
      <add key="TableQueryContinuationTokenLimitInKb" value="16"/>
            
    </appSettings>
</configuration>
```

Questo punto, eseguire una rapida panoramica delle operazioni eseguite nell'applicazione hello. Aprire hello `Program.cs` file si scopre che le righe di codice creano hello risorse tabella. 

## <a name="create-hello-table-client"></a>Creare hello tabella client
Inizializzare un `CloudTableClient` conto tabella di tooconnect toohello.

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```
Questo client viene inizializzato con hello `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel`, e `TablePreferredLocations` i valori di configurazione se è specificato nelle impostazioni dell'app hello.
    
## <a name="create-a-table"></a>Creare una tabella
Creare quindi una tabella usando `CloudTable`. Le tabelle nel database di Azure Cosmos possono aumentare in modo indipendente in termini di archiviazione e la velocità effettiva e il partizionamento viene gestito automaticamente dal servizio hello. Azure Cosmos DB supporta le tabelle sia senza limitazioni sia con dimensioni fisse. Vedere [Partizionamento in Azure Cosmos DB](partition-data.md) per informazioni dettagliate. 

```csharp
CloudTable table = tableClient.GetTableReference("people");

table.CreateIfNotExists();
```

Esiste una differenza importante nella creazione delle tabelle. Azure Cosmos DB riserva la velocità effettiva, a differenza del modello in base al consumo di Archiviazione di Azure per le transazioni. modello di prenotazione Hello presenta due vantaggi principali:

* La velocità effettiva è dedicata/riservata e quindi non viene mai limitata, se la frequenza di richiesta è pari o inferiore alla velocità effettiva con provisioning
* modello di prenotazione Hello è più [economicamente conveniente per carichi di lavoro elevati in termini di velocità effettiva](key-value-store-cost.md)

È possibile configurare la velocità effettiva di hello predefinito configurando l'impostazione di hello per `TableThroughput` in termini di UR (unità di richiesta) al secondo. 

Una lettura di un'entità di 1 KB viene normalizzata come 1 UR e altre operazioni vengono normalizzato tooa UR valore in base al loro consumo di CPU, memoria e IOPS fissato. Altre informazioni sulle [unità richiesta in Azure Cosmos DB](request-units.md).

> [!NOTE]
> Durante l'archiviazione tabelle SDK attualmente non supporta la modifica della velocità effettiva, è possibile modificare la velocità effettiva hello immediatamente in qualsiasi momento usando hello portale di Azure o CLI di Azure.

Successivamente, si analizzerà lettura semplice hello operazioni e scrittura (CRUD) utilizza hello l'archiviazione tabelle di Azure SDK. Questa esercitazione illustra le latenze pari a singole unità di millisecondi e le query rapide fornite da Azure Cosmos DB.

## <a name="add-an-entity-tooa-table"></a>Aggiungere una tabella tooa entità
Entità nell'archiviazione tabelle di Azure si estendono da hello `TableEntity` classe e deve avere `PartitionKey` e `RowKey` proprietà. Di seguito è riportata una definizione di esempio per un'entità cliente.

```csharp
public class CustomerEntity : TableEntity
{
    public CustomerEntity(string lastName, string firstName)
    {
        this.PartitionKey = lastName;
        this.RowKey = firstName;
    }

    public CustomerEntity() { }

    public string Email { get; set; }

    public string PhoneNumber { get; set; }
}
```

Hello frammento di codice seguente viene illustrato come tooinsert un'entità con hello Azure storage SDK. Azure DB Cosmos è progettato per garantito a bassa latenza la scala, tutto il mondo hello.

Completamento di scritture < 15 ms p99 e ms ~ 6 in p50 per le applicazioni in esecuzione in hello hello account Azure Cosmos DB stessa area. E questa durata gli account per il fatto di hello che scrive vengano riconosciuti toohello indietro client solo dopo che vengono replicati in modo sincrono, in modo durevole committed, e tutto il contenuto viene indicizzato.

API di tabelle di Azure Cosmos DB Hello è in anteprima. Al momento della disponibilità generale, le garanzie di latenza p99 hello sono supportate da contratti di servizio come altre API DB Cosmos di Azure. 

```csharp
// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create hello TableOperation object that inserts hello customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute hello insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a>Inserire un batch di entità
Archiviazione tabella Azure supporta un'API di operazione batch, che consente di combina aggiornamenti, eliminazioni e inserimenti in hello stessa singola operazione batch. Azure Cosmos DB non è disponibile alcune delle limitazioni di hello in batch hello API come archiviazione tabelle di Azure. Ad esempio, è possibile eseguire più operazioni di lettura in un batch, è possibile eseguire più operazioni di scrittura toohello stessa entità all'interno di un batch, e non vi sono limiti su 100 operazioni per ogni batch. 

```csharp
// Create hello batch operation.
TableBatchOperation batchOperation = new TableBatchOperation();

// Create a customer entity and add it toohello table.
CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
customer1.Email = "Jeff@contoso.com";
customer1.PhoneNumber = "425-555-0104";

// Create another customer entity and add it toohello table.
CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
customer2.Email = "Ben@contoso.com";
customer2.PhoneNumber = "425-555-0102";

// Add both customer entities toohello batch insert operation.
batchOperation.Insert(customer1);
batchOperation.Insert(customer2);

// Execute hello batch operation.
table.ExecuteBatch(batchOperation);
```
## <a name="retrieve-a-single-entity"></a>Recuperare una singola entità
Recupera (ottiene) nel database di Azure Cosmos completo < 10 ms p99 e ~ 1 ms in p50 in hello stessa area di Azure. È possibile aggiungere account di tooyour tante aree per le letture di bassa latenza e distribuire applicazioni tooread da loro area locale ("multihomed") tramite l'impostazione `TablePreferredLocations`. 

È possibile recuperare una singola entità utilizzando hello frammento di codice seguente:

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
> [!TIP]
> Informazioni sulle API multihosting in [Sviluppo con più aree](tutorial-global-distribution-table.md)
>

## <a name="query-entities-using-automatic-secondary-indexes"></a>Eseguire query su entità tramite indici secondari automatici
Le tabelle possono essere eseguite utilizzando hello `TableQuery` classe. Azure Cosmos DB dispone di un motore di database con ottimizzazione per la scrittura che indicizza automaticamente tutte le colonne all'interno della tabella. L'indicizzazione nel database di Azure Cosmos è tooschema agnostico. Pertanto, anche se lo schema è diverso tra le righe o schema hello si evolve nel tempo, viene automaticamente indicizzato. Poiché Azure Cosmos DB supporta gli indici secondari automatico, le query su qualsiasi proprietà possono utilizzare l'indice di hello e fornite in modo efficiente.

```csharp
CloudTable table = tableClient.GetTableReference("people");

// Filter against a property that's not partition key or row key
TableQuery<CustomerEntity> emailQuery = new TableQuery<CustomerEntity>().Where(
    TableQuery.GenerateFilterCondition("Email", QueryComparisons.Equal, "Ben@contoso.com"));

foreach (CustomerEntity entity in table.ExecuteQuery(emailQuery))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

Nell'anteprima di Azure Cosmos DB supporta hello stessa funzionalità dell'archiviazione tabelle di Azure per hello tabella API di query. Azure Cosmos DB supporta anche l'ordinamento, le aggregazioni, le query geospaziali, la gerarchia e un'ampia gamma di funzioni predefinite. funzionalità aggiuntive di Hello verrà fornita in hello API tabelle in un futuro aggiornamento del servizio. Vedere [Query in Azure Cosmos DB](documentdb-sql-query.md) per una panoramica di queste funzionalità. 

## <a name="replace-an-entity"></a>Sostituire un'entità
tooupdate un'entità, recuperarlo dal servizio tabelle hello, modificare l'oggetto entità hello e quindi salvare le modifiche apportate hello eseguire il servizio tabelle toohello. Hello codice seguente modifica il numero di telefono del cliente esistente. 

```csharp
TableOperation updateOperation = TableOperation.Replace(updateEntity);
table.Execute(updateOperation);
```
Analogamente, è possibile eseguire operazioni `InsertOrMerge` o `Merge`.  

## <a name="delete-an-entity"></a>Eliminare un'entità
È possibile eliminare un'entità facilmente dopo avere recuperato utilizzando hello stesso modello visualizzato per l'aggiornamento di un'entità. Hello seguente codice recupera ed elimina un'entità customer.

```csharp
TableOperation deleteOperation = TableOperation.Delete(deleteEntity);
table.Execute(deleteOperation);
```

## <a name="delete-a-table"></a>Eliminare una tabella
Infine, hello esempio di codice seguente elimina una tabella da un account di archiviazione. È possibile eliminare e ricreare una tabella immediatamente con Azure Cosmos DB.

```csharp
CloudTable table = tableClient.GetTableReference("people");
table.DeleteIfExists();
```

## <a name="clean-up-resources"></a>Pulire le risorse 

Se non si ha intenzione toocontinue toouse questa app, utilizzare hello seguendo i passaggi toodelete tutte le risorse create da questa esercitazione in hello portale di Azure.   

1. Dal menu a sinistra di hello in hello portale di Azure, fare clic su **gruppi di risorse** e quindi fare clic su nome hello della risorsa di hello è stato creato.  
2. Nella pagina di gruppo di risorse, fare clic su **eliminare**, digitare il nome di hello di hello risorsa toodelete nella casella di testo hello e quindi fare clic su **eliminare**. 

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione, trattati come tooget iniziare con Azure Cosmos DB hello tabella API e aver eseguito l'esempio hello: 

> [!div class="checklist"] 
> * Creazione di un account Azure Cosmos DB 
> * Funzionalità abilitata nel file app. config hello 
> * Creazione di una tabella 
> * Aggiunta di una tabella tooa entità 
> * Inserimento di un batch di entità 
> * Recupero di una singola entità 
> * Esecuzione di query di entità tramite indici secondari automatici 
> * Sostituzione di un'entità 
> * Eliminazione di un'entità 
> * Eliminazione di una tabella  

È possibile continuare l'esercitazione successiva toohello e altre informazioni su come eseguire query di dati della tabella. 

> [!div class="nextstepaction"]
> [Eseguire una query con hello tabella API](tutorial-query-table.md)
