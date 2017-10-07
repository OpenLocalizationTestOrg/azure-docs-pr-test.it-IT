---
title: esercitazione di distribuzione globale Cosmos DB aaaAzure per l'API DocumentDB | Documenti Microsoft
description: Informazioni su come distribuzione globale di Azure Cosmos DB toosetup utilizzando hello API DocumentDB.
services: cosmos-db
keywords: distribuzione globale, documentdb
documentationcenter: 
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: a1d5f01faa62407fbbc9c078ef4a9589a1a29219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-documentdb-api"></a>La distribuzione globale di Azure Cosmos DB toosetup utilizzando hello API DocumentDB

In questo articolo viene illustrata come toouse hello toosetup portale Azure distribuzione globale di Azure Cosmos DB e quindi connettersi usando l'API DocumentDB hello.

Questo articolo descrive hello seguenti attività: 

> [!div class="checklist"]
> * Configurare la distribuzione globale mediante hello portale di Azure
> * Configurare la distribuzione globale mediante hello [APIs DocumentDB](documentdb-introduction.md)

<a id="portal"></a>
[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-documentdb-api"></a>Connessione area geografica preferita tooa utilizzando l'API DocumentDB hello

In ordine tootake sfruttare la [distribuzione globale](distribute-data-globally.md), applicazioni client possono specificare hello ordinato l'elenco delle preferenze di aree toobe utilizzato tooperform documento operazioni. Questa operazione può essere eseguita mediante l'impostazione di criteri di connessione hello. Basato sulla configurazione dell'account Azure Cosmos DB hello, elenco delle preferenze hello e la disponibilità di internazionale corrente specificato, hello hello operazioni di lettura e scrittura di DocumentDB SDK tooperform sceglierà la maggior parte degli endpoint ottimale.

L'elenco delle preferenze viene specificato durante l'inizializzazione di una connessione utilizzando il SDK di DocumentDB hello. Hello SDK di accettare un parametro facoltativo "PreferredLocations" che rappresenta un elenco ordinato di aree di Azure.

Hello SDK invierà automaticamente area scrittura di tutte le operazioni di scrittura toohello corrente.

Tutte le letture verranno inviate toohello prima area disponibile nell'elenco PreferredLocations hello. Se hello richiesta non riesce, il client hello esito negativo all'area di hello elenco toohello successiva e così via.

Hello SDK tenterà solo tooread dalle aree hello specificato in PreferredLocations. In tal caso, ad esempio, se hello Account del Database è disponibile in tre aree, ma client hello specifica solo due delle aree non scrittura hello per PreferredLocations, quindi non letture verranno utilizzate da area di scrittura hello, anche nel caso di hello di failover.

un'applicazione Hello possibile verificare l'endpoint di scrittura corrente hello e leggere endpoint scelto da hello SDK dal controllo due proprietà, WriteEndpoint e ReadEndpoint, disponibili nella versione SDK 1.8 e versioni successive.

Se non è impostata la proprietà PreferredLocations hello, verranno utilizzate dall'area di scrittura corrente hello tutte le richieste.

## <a name="net-sdk"></a>.NET SDK
Hello SDK è utilizzabile senza alcuna modifica al codice. In questo caso, hello SDK automaticamente indirizza entrambe le operazioni di lettura e scrive toohello area di scrittura corrente.

Nella versione 1.8 e versioni successive di .NET SDK hello, hello del parametro ConnectionPolicy per costruttore DocumentClient hello è una proprietà denominata Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations. Questa proprietà è di tipo raccolta `<string>` e deve contenere un elenco di nomi di aree. per ogni colonna di nome dell'area di hello in hello vengono formattati i valori di stringa Hello [aree di Azure] [ regions] pagina, senza spazi prima o dopo hello prima e l'ultimo carattere rispettivamente.

scrittura corrente Hello e lettura di endpoint sono disponibili in DocumentClient.WriteEndpoint e DocumentClient.ReadEndpoint rispettivamente.

> [!NOTE]
> Hello URL per gli endpoint di hello non deve essere considerato come costanti di lunga durate. servizio Hello può aggiornare questi in qualsiasi momento. Hello SDK gestisce automaticamente questa modifica.
>
>

```csharp
// Getting endpoints from application settings or other configuration location
Uri accountEndPoint = new Uri(Properties.Settings.Default.GlobalDatabaseUri);
string accountKey = Properties.Settings.Default.GlobalDatabaseKey;
  
ConnectionPolicy connectionPolicy = new ConnectionPolicy();

//Setting read region selection preference
connectionPolicy.PreferredLocations.Add(LocationNames.WestUS); // first preference
connectionPolicy.PreferredLocations.Add(LocationNames.EastUS); // second preference
connectionPolicy.PreferredLocations.Add(LocationNames.NorthEurope); // third preference

// initialize connection
DocumentClient docClient = new DocumentClient(
    accountEndPoint,
    accountKey,
    connectionPolicy);

// connect tooDocDB
await docClient.OpenAsync().ConfigureAwait(false);
```

## <a name="nodejs-javascript-and-python-sdks"></a>SDK di NodeJS, JavaScript e Python
Hello SDK è utilizzabile senza alcuna modifica al codice. In questo caso, hello che SDK indirizzerà automaticamente sia legge e scrive toohello area di scrittura corrente.

Nella versione 1.8 e versioni successive di ogni SDK, hello ConnectionPolicy parametro hello DocumentClient costruttore una nuova proprietà denominata DocumentClient.ConnectionPolicy.PreferredLocations. Questo parametro è una matrice di stringhe che accetta un elenco di nomi di aree. i nomi di Hello vengono formattati per ogni colonna di nome dell'area di hello in hello [aree di Azure] [ regions] pagina. È inoltre possibile utilizzare costanti hello predefinito nell'oggetto praticità hello AzureDocuments.Regions

scrittura corrente Hello e lettura di endpoint sono disponibili in DocumentClient.getWriteEndpoint e DocumentClient.getReadEndpoint rispettivamente.

> [!NOTE]
> Hello URL per gli endpoint di hello non deve essere considerato come costanti di lunga durate. servizio Hello può aggiornare questi in qualsiasi momento. Hello SDK gestirà automaticamente questa modifica.
>
>

Di seguito è riportato un esempio di codice per NodeJS/Javascript. Python e Java seguirà hello stesso modello.

```java
// Creating a ConnectionPolicy object
var connectionPolicy = new DocumentBase.ConnectionPolicy();

// Setting read region selection preference, in hello following order -
// 1 - West US
// 2 - East US
// 3 - North Europe
connectionPolicy.PreferredLocations = ['West US', 'East US', 'North Europe'];

// initialize hello connection
var client = new DocumentDBClient(host, { masterKey: masterKey }, connectionPolicy);
```

## <a name="rest"></a>REST
Una volta che un account del database è stata resa disponibile in più aree, i client possono eseguire query la sua disponibilità eseguendo una richiesta GET su hello seguente URI.

    https://{databaseaccount}.documents.azure.com/

servizio Hello restituirà un elenco delle aree e i relativi endpoint di Azure Cosmos DB URI corrispondente per le repliche hello. area di scrittura corrente Hello viene indicato nella risposta hello. client Hello quindi possibile selezionare endpoint appropriato di hello per le richieste API REST di tutte le ulteriori come indicato di seguito.

Risposta di esempio

    {
        "_dbs": "//dbs/",
        "media": "//media/",
        "writableLocations": [
            {
                "Name": "West US",
                "DatabaseAccountEndpoint": "https://globaldbexample-westus.documents.azure.com:443/"
            }
        ],
        "readableLocations": [
            {
                "Name": "East US",
                "DatabaseAccountEndpoint": "https://globaldbexample-eastus.documents.azure.com:443/"
            }
        ],
        "MaxMediaStorageUsageInMB": 2048,
        "MediaStorageUsageInMB": 0,
        "ConsistencyPolicy": {
            "defaultConsistencyLevel": "Session",
            "maxStalenessPrefix": 100,
            "maxIntervalInSeconds": 5
        },
        "addresses": "//addresses/",
        "id": "globaldbexample",
        "_rid": "globaldbexample.documents.azure.com",
        "_self": "",
        "_ts": 0,
        "_etag": null
    }


* Le richieste di tutti i PUT, POST e DELETE è necessario che venga indicato toohello scrivere URI
* Ottiene tutti e altre richieste di sola lettura (ad esempio query) torni tooany endpoint scelto hello client

Scrivere le richieste solo tooread aree avrà esito negativo con codice di errore HTTP 403 ("accesso negato").

Se l'area di scrittura hello viene modificata dopo la fase di individuazione iniziale del client hello, successive scrive toohello precedente area scrittura avrà esito negativo con codice di errore HTTP 403 ("accesso negato"). client Hello deve quindi ottenere elenco hello delle aree nuovamente tooget hello scrittura aggiornato area.

L'esercitazione è terminata. È possibile ottenere informazioni come toomanage hello la coerenza dell'account di replicato globalmente leggendo [livelli di coerenza nel database di Azure Cosmos](consistency-levels.md). Per informazioni sul funzionamento della replica di database globale in Azure Cosmos DB, vedere [Distribuire i dati a livello globale con Azure Cosmos DB](distribute-data-globally.md).

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione, effettuata seguente hello:

> [!div class="checklist"]
> * Configurare la distribuzione globale mediante hello portale di Azure
> * Configurare la distribuzione globale mediante hello APIs DocumentDB

È ora possibile procedere toolearn esercitazione successiva toohello come toodevelop localmente tramite hello emulatore locale di Azure Cosmos DB.

> [!div class="nextstepaction"]
> [Sviluppare in locale con emulator hello](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

