---
title: Esercitazione sulla distribuzione globale in Azure Cosmos DB per l'API di DocumentDB | Documentazione Microsoft
description: Informazioni su come configurare la distribuzione globale in Azure Cosmos DB mediante l'API di DocumentDB.
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
ms.openlocfilehash: f4d8efe9814bd28bb902567a23b541bc9b5414a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-setup-azure-cosmos-db-global-distribution-using-the-documentdb-api"></a><span data-ttu-id="deba4-104">Procedura di configurazione della distribuzione globale in Azure Cosmos DB mediante l'API di DocumentDB</span><span class="sxs-lookup"><span data-stu-id="deba4-104">How to setup Azure Cosmos DB global distribution using the DocumentDB API</span></span>

<span data-ttu-id="deba4-105">Questo articolo illustra come usare il portale di Azure per configurare la distribuzione globale in Azure Cosmos DB e quindi connettersi tramite l'API di DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="deba4-105">In this article, we show how to use the Azure portal to setup Azure Cosmos DB global distribution and then connect using the DocumentDB API.</span></span>

<span data-ttu-id="deba4-106">Questo articolo illustra le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="deba4-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="deba4-107">Configurare la distribuzione globale tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="deba4-107">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="deba4-108">Configurare la distribuzione globale tramite le [API di DocumentDB](documentdb-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="deba4-108">Configure global distribution using the [DocumentDB APIs](documentdb-introduction.md)</span></span>

<a id="portal"></a>
[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-to-a-preferred-region-using-the-documentdb-api"></a><span data-ttu-id="deba4-109">Connessione a un'area preferita tramite l'API di DocumentDB</span><span class="sxs-lookup"><span data-stu-id="deba4-109">Connecting to a preferred region using the DocumentDB API</span></span>

<span data-ttu-id="deba4-110">Per sfruttare la [distribuzione globale](distribute-data-globally.md), le applicazioni client possono specificare un elenco di aree, nell'ordine preferito, da usare per eseguire operazioni sui documenti.</span><span class="sxs-lookup"><span data-stu-id="deba4-110">In order to take advantage of [global distribution](distribute-data-globally.md), client applications can specify the ordered preference list of regions to be used to perform document operations.</span></span> <span data-ttu-id="deba4-111">Questa operazione può essere eseguita impostando il criterio di connessione.</span><span class="sxs-lookup"><span data-stu-id="deba4-111">This can be done by setting the connection policy.</span></span> <span data-ttu-id="deba4-112">A seconda della configurazione dell'account Azure Cosmos DB, della disponibilità corrente delle aree e dell'elenco delle preferenze specificato, l'SDK DocumentDB sceglierà l'endpoint ottimale per eseguire le operazioni di scrittura e lettura.</span><span class="sxs-lookup"><span data-stu-id="deba4-112">Based on the Azure Cosmos DB account configuration, current regional availability and the preference list specified, the most optimal endpoint will be chosen by the DocumentDB SDK to perform write and read operations.</span></span>

<span data-ttu-id="deba4-113">L'elenco delle preferenze viene specificato nella fase di inizializzazione di una connessione usando gli SDK DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="deba4-113">This preference list is specified when initializing a connection using the DocumentDB SDKs.</span></span> <span data-ttu-id="deba4-114">Gli SDK accettano il parametro facoltativo "PreferredLocations", ovvero un elenco ordinato di aree di Azure.</span><span class="sxs-lookup"><span data-stu-id="deba4-114">The SDKs accept an optional parameter "PreferredLocations" that is an ordered list of Azure regions.</span></span>

<span data-ttu-id="deba4-115">L'SDK invia automaticamente tutte le scritture all'area di scrittura corrente.</span><span class="sxs-lookup"><span data-stu-id="deba4-115">The SDK will automatically send all writes to the current write region.</span></span>

<span data-ttu-id="deba4-116">Tutte le letture verranno inviate alla prima area disponibile nell'elenco PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="deba4-116">All reads will be sent to the first available region in the PreferredLocations list.</span></span> <span data-ttu-id="deba4-117">Se la richiesta ha esito negativo, il client trasferisce l'elenco all'area successiva e così via.</span><span class="sxs-lookup"><span data-stu-id="deba4-117">If the request fails, the client will fail down the list to the next region, and so on.</span></span>

<span data-ttu-id="deba4-118">Gli SDK tenteranno di leggere solo dalle aree specificate nell'elenco PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="deba4-118">The SDKs will only attempt to read from the regions specified in PreferredLocations.</span></span> <span data-ttu-id="deba4-119">Quindi se l'Account di database è disponibile ad esempio in tre aree, ma il client specifica solo due delle aree di non scrittura per PreferredLocations, le letture non verranno distribuite fuori dall'area di scrittura, anche in caso di failover.</span><span class="sxs-lookup"><span data-stu-id="deba4-119">So, for example, if the Database Account is available in three regions, but the client only specifies two of the non-write regions for PreferredLocations, then no reads will be served out of the write region, even in the case of failover.</span></span>

<span data-ttu-id="deba4-120">L'applicazione può verificare l'endpoint di scrittura e lettura corrente scelto dall'SDK controllando due proprietà, WriteEndpoint e ReadEndpoint, disponibili nella versione dell'SDK 1.8 e nelle versioni successive.</span><span class="sxs-lookup"><span data-stu-id="deba4-120">The application can verify the current write endpoint and read endpoint chosen by the SDK by checking two properties, WriteEndpoint and ReadEndpoint, available in SDK version 1.8 and above.</span></span>

<span data-ttu-id="deba4-121">Se la proprietà PreferredLocations non è impostata, tutte le richieste verranno distribuite dall'area di scrittura corrente.</span><span class="sxs-lookup"><span data-stu-id="deba4-121">If the PreferredLocations property is not set, all requests will be served from the current write region.</span></span>

## <a name="net-sdk"></a><span data-ttu-id="deba4-122">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="deba4-122">.NET SDK</span></span>
<span data-ttu-id="deba4-123">L'SDK può essere usato senza alcuna modifica del codice.</span><span class="sxs-lookup"><span data-stu-id="deba4-123">The SDK can be used without any code changes.</span></span> <span data-ttu-id="deba4-124">In questo caso l'SDK reindirizza automaticamente sia le operazioni di lettura che di scrittura all'area di scrittura corrente.</span><span class="sxs-lookup"><span data-stu-id="deba4-124">In this case, the SDK automatically directs both reads and writes to the current write region.</span></span>

<span data-ttu-id="deba4-125">Nella versione 1.8 e nelle versioni successive di .NET SDK, il parametro ConnectionPolicy per il costruttore DocumentClient dispone di una proprietà denominata Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="deba4-125">In version 1.8 and later of the .NET SDK, the ConnectionPolicy parameter for the DocumentClient constructor has a property called Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="deba4-126">Questa proprietà è di tipo raccolta `<string>` e deve contenere un elenco di nomi di aree.</span><span class="sxs-lookup"><span data-stu-id="deba4-126">This property is of type Collection `<string>` and should contain a list of region names.</span></span> <span data-ttu-id="deba4-127">I valori della stringa vengono formattati secondo la colonna Nome dell'area nella pagina [Regioni di Azure][regions], senza spazi prima o dopo il primo e l'ultimo carattere.</span><span class="sxs-lookup"><span data-stu-id="deba4-127">The string values are formatted per the Region Name column on the [Azure Regions][regions] page, with no spaces before or after the first and last character respectively.</span></span>

<span data-ttu-id="deba4-128">Gli endpoint di lettura e scrittura correnti sono disponibili rispettivamente in DocumentClient.WriteEndpoint e DocumentClient.ReadEndpoint.</span><span class="sxs-lookup"><span data-stu-id="deba4-128">The current write and read endpoints are available in DocumentClient.WriteEndpoint and DocumentClient.ReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="deba4-129">Gli URL per gli endpoint non devono essere considerati come costanti di lunga durata.</span><span class="sxs-lookup"><span data-stu-id="deba4-129">The URLs for the endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="deba4-130">Il servizio può aggiornare gli URL in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="deba4-130">The service may update these at any point.</span></span> <span data-ttu-id="deba4-131">L'SDK gestisce la modifica in modo automatico.</span><span class="sxs-lookup"><span data-stu-id="deba4-131">The SDK handles this change automatically.</span></span>
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

// connect to DocDB
await docClient.OpenAsync().ConfigureAwait(false);
```

## <a name="nodejs-javascript-and-python-sdks"></a><span data-ttu-id="deba4-132">SDK di NodeJS, JavaScript e Python</span><span class="sxs-lookup"><span data-stu-id="deba4-132">NodeJS, JavaScript, and Python SDKs</span></span>
<span data-ttu-id="deba4-133">L'SDK può essere usato senza alcuna modifica del codice.</span><span class="sxs-lookup"><span data-stu-id="deba4-133">The SDK can be used without any code changes.</span></span> <span data-ttu-id="deba4-134">In questo caso, l'SDK reindirizzerà automaticamente sia le letture sia le scritture all'area di scrittura corrente.</span><span class="sxs-lookup"><span data-stu-id="deba4-134">In this case, the SDK will automatically direct both reads and writes to the current write region.</span></span>

<span data-ttu-id="deba4-135">Nella versione 1.8 e nelle versioni successive di ogni SDK, il parametro ConnectionPolicy per il costruttore DocumentClient dispone di una nuova proprietà denominata DocumentClient.ConnectionPolicy.PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="deba4-135">In version 1.8 and later of each SDK, the ConnectionPolicy parameter for the DocumentClient constructor a new property called DocumentClient.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="deba4-136">Questo parametro è una matrice di stringhe che accetta un elenco di nomi di aree.</span><span class="sxs-lookup"><span data-stu-id="deba4-136">This is parameter is an array of strings that takes a list of region names.</span></span> <span data-ttu-id="deba4-137">I nomi vengono formattati secondo la colonna Nome dell'area nella pagina [Regioni di Azure][regions].</span><span class="sxs-lookup"><span data-stu-id="deba4-137">The names are formatted per the Region Name column in the [Azure Regions][regions] page.</span></span> <span data-ttu-id="deba4-138">È anche possibile usare costanti predefinite nell'oggetto AzureDocuments.Regions</span><span class="sxs-lookup"><span data-stu-id="deba4-138">You can also use the predefined constants in the convenience object AzureDocuments.Regions</span></span>

<span data-ttu-id="deba4-139">Gli endpoint di lettura e scrittura correnti sono disponibili rispettivamente in DocumentClient.getWriteEndpoint e DocumentClient.getReadEndpoint.</span><span class="sxs-lookup"><span data-stu-id="deba4-139">The current write and read endpoints are available in DocumentClient.getWriteEndpoint and DocumentClient.getReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="deba4-140">Gli URL per gli endpoint non devono essere considerati come costanti di lunga durata.</span><span class="sxs-lookup"><span data-stu-id="deba4-140">The URLs for the endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="deba4-141">Il servizio può aggiornare gli URL in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="deba4-141">The service may update these at any point.</span></span> <span data-ttu-id="deba4-142">L'SDK gestirà questa modifica in automatico.</span><span class="sxs-lookup"><span data-stu-id="deba4-142">The SDK will handle this change automatically.</span></span>
>
>

<span data-ttu-id="deba4-143">Di seguito è riportato un esempio di codice per NodeJS/Javascript.</span><span class="sxs-lookup"><span data-stu-id="deba4-143">Below is a code example for NodeJS/Javascript.</span></span> <span data-ttu-id="deba4-144">Python e Java seguiranno lo stesso modello.</span><span class="sxs-lookup"><span data-stu-id="deba4-144">Python and Java will follow the same pattern.</span></span>

```java
// Creating a ConnectionPolicy object
var connectionPolicy = new DocumentBase.ConnectionPolicy();

// Setting read region selection preference, in the following order -
// 1 - West US
// 2 - East US
// 3 - North Europe
connectionPolicy.PreferredLocations = ['West US', 'East US', 'North Europe'];

// initialize the connection
var client = new DocumentDBClient(host, { masterKey: masterKey }, connectionPolicy);
```

## <a name="rest"></a><span data-ttu-id="deba4-145">REST</span><span class="sxs-lookup"><span data-stu-id="deba4-145">REST</span></span>
<span data-ttu-id="deba4-146">Dopo aver reso disponibile un account di database in più aree, i client possono eseguire query sulla relativa disponibilità tramite una richiesta GET all'URI seguente.</span><span class="sxs-lookup"><span data-stu-id="deba4-146">Once a database account has been made available in multiple regions, clients can query its availability by performing a GET request on the following URI.</span></span>

    https://{databaseaccount}.documents.azure.com/

<span data-ttu-id="deba4-147">Il servizio restituirà un elenco delle aree e i relativi URI dell'endpoint Azure Cosmos DB per le repliche.</span><span class="sxs-lookup"><span data-stu-id="deba4-147">The service will return a list of regions and their corresponding Azure Cosmos DB endpoint URIs for the replicas.</span></span> <span data-ttu-id="deba4-148">L'area di scrittura corrente verrà indicata nella risposta.</span><span class="sxs-lookup"><span data-stu-id="deba4-148">The current write region will be indicated in the response.</span></span> <span data-ttu-id="deba4-149">Il client può quindi selezionare l'endpoint appropriato per tutte le altre richieste dell'API REST come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="deba4-149">The client can then select the appropriate endpoint for all further REST API requests as follows.</span></span>

<span data-ttu-id="deba4-150">Risposta di esempio</span><span class="sxs-lookup"><span data-stu-id="deba4-150">Example response</span></span>

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


* <span data-ttu-id="deba4-151">Tutte le richieste PUT, POST e DELETE devono passare all'URI di scrittura indicato.</span><span class="sxs-lookup"><span data-stu-id="deba4-151">All PUT, POST and DELETE requests must go to the indicated write URI</span></span>
* <span data-ttu-id="deba4-152">Tutte le richieste di sola lettura e GET, ad esempio le query, possono passare a qualsiasi endpoint scelto dal client.</span><span class="sxs-lookup"><span data-stu-id="deba4-152">All GETs and other read-only requests (for example queries) may go to any endpoint of the client’s choice</span></span>

<span data-ttu-id="deba4-153">Le richieste di scrittura per le aree di sola lettura avranno esito negativo con codice di errore HTTP 403 ("Non consentito").</span><span class="sxs-lookup"><span data-stu-id="deba4-153">Write requests to read-only regions will fail with HTTP error code 403 (“Forbidden”).</span></span>

<span data-ttu-id="deba4-154">Se l'area di scrittura viene modificata dopo la fase di individuazione iniziale del client, le scritture successive all'area di scrittura precedente avranno esito negativo con codice di errore HTTP 403 ("Non consentito").</span><span class="sxs-lookup"><span data-stu-id="deba4-154">If the write region changes after the client’s initial discovery phase, subsequent writes to the previous write region will fail with HTTP error code 403 (“Forbidden”).</span></span> <span data-ttu-id="deba4-155">Il client deve quindi OTTENERE nuovamente l'elenco delle aree per aggiornare l'area di scrittura.</span><span class="sxs-lookup"><span data-stu-id="deba4-155">The client should then GET the list of regions again to get the updated write region.</span></span>

<span data-ttu-id="deba4-156">L'esercitazione è terminata.</span><span class="sxs-lookup"><span data-stu-id="deba4-156">That's it, that completes this tutorial.</span></span> <span data-ttu-id="deba4-157">Per informazioni su come gestire la coerenza dell'account con replica globale, vedere [Livelli di coerenza in Azure Cosmos DB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="deba4-157">You can learn how to manage the consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="deba4-158">Per informazioni sul funzionamento della replica di database globale in Azure Cosmos DB, vedere [Distribuire i dati a livello globale con Azure Cosmos DB](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="deba4-158">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="deba4-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="deba4-159">Next steps</span></span>

<span data-ttu-id="deba4-160">In questa esercitazione sono state eseguite le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="deba4-160">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="deba4-161">Configurare la distribuzione globale tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="deba4-161">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="deba4-162">Configurare la distribuzione globale tramite le API di DocumentDB</span><span class="sxs-lookup"><span data-stu-id="deba4-162">Configure global distribution using the DocumentDB APIs</span></span>

<span data-ttu-id="deba4-163">È ora possibile passare all'esercitazione successiva per imparare a sviluppare in locale usando l'emulatore locale di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="deba4-163">You can now proceed to the next tutorial to learn how to develop locally using the Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="deba4-164">Sviluppare in locale con l'emulatore</span><span class="sxs-lookup"><span data-stu-id="deba4-164">Develop locally with the emulator</span></span>](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

