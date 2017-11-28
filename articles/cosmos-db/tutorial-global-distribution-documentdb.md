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
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-documentdb-api"></a><span data-ttu-id="8f533-104">La distribuzione globale di Azure Cosmos DB toosetup utilizzando hello API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="8f533-104">How toosetup Azure Cosmos DB global distribution using hello DocumentDB API</span></span>

<span data-ttu-id="8f533-105">In questo articolo viene illustrata come toouse hello toosetup portale Azure distribuzione globale di Azure Cosmos DB e quindi connettersi usando l'API DocumentDB hello.</span><span class="sxs-lookup"><span data-stu-id="8f533-105">In this article, we show how toouse hello Azure portal toosetup Azure Cosmos DB global distribution and then connect using hello DocumentDB API.</span></span>

<span data-ttu-id="8f533-106">Questo articolo descrive hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="8f533-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="8f533-107">Configurare la distribuzione globale mediante hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="8f533-107">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="8f533-108">Configurare la distribuzione globale mediante hello [APIs DocumentDB](documentdb-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="8f533-108">Configure global distribution using hello [DocumentDB APIs](documentdb-introduction.md)</span></span>

<a id="portal"></a>
[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-documentdb-api"></a><span data-ttu-id="8f533-109">Connessione area geografica preferita tooa utilizzando l'API DocumentDB hello</span><span class="sxs-lookup"><span data-stu-id="8f533-109">Connecting tooa preferred region using hello DocumentDB API</span></span>

<span data-ttu-id="8f533-110">In ordine tootake sfruttare la [distribuzione globale](distribute-data-globally.md), applicazioni client possono specificare hello ordinato l'elenco delle preferenze di aree toobe utilizzato tooperform documento operazioni.</span><span class="sxs-lookup"><span data-stu-id="8f533-110">In order tootake advantage of [global distribution](distribute-data-globally.md), client applications can specify hello ordered preference list of regions toobe used tooperform document operations.</span></span> <span data-ttu-id="8f533-111">Questa operazione può essere eseguita mediante l'impostazione di criteri di connessione hello.</span><span class="sxs-lookup"><span data-stu-id="8f533-111">This can be done by setting hello connection policy.</span></span> <span data-ttu-id="8f533-112">Basato sulla configurazione dell'account Azure Cosmos DB hello, elenco delle preferenze hello e la disponibilità di internazionale corrente specificato, hello hello operazioni di lettura e scrittura di DocumentDB SDK tooperform sceglierà la maggior parte degli endpoint ottimale.</span><span class="sxs-lookup"><span data-stu-id="8f533-112">Based on hello Azure Cosmos DB account configuration, current regional availability and hello preference list specified, hello most optimal endpoint will be chosen by hello DocumentDB SDK tooperform write and read operations.</span></span>

<span data-ttu-id="8f533-113">L'elenco delle preferenze viene specificato durante l'inizializzazione di una connessione utilizzando il SDK di DocumentDB hello.</span><span class="sxs-lookup"><span data-stu-id="8f533-113">This preference list is specified when initializing a connection using hello DocumentDB SDKs.</span></span> <span data-ttu-id="8f533-114">Hello SDK di accettare un parametro facoltativo "PreferredLocations" che rappresenta un elenco ordinato di aree di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f533-114">hello SDKs accept an optional parameter "PreferredLocations" that is an ordered list of Azure regions.</span></span>

<span data-ttu-id="8f533-115">Hello SDK invierà automaticamente area scrittura di tutte le operazioni di scrittura toohello corrente.</span><span class="sxs-lookup"><span data-stu-id="8f533-115">hello SDK will automatically send all writes toohello current write region.</span></span>

<span data-ttu-id="8f533-116">Tutte le letture verranno inviate toohello prima area disponibile nell'elenco PreferredLocations hello.</span><span class="sxs-lookup"><span data-stu-id="8f533-116">All reads will be sent toohello first available region in hello PreferredLocations list.</span></span> <span data-ttu-id="8f533-117">Se hello richiesta non riesce, il client hello esito negativo all'area di hello elenco toohello successiva e così via.</span><span class="sxs-lookup"><span data-stu-id="8f533-117">If hello request fails, hello client will fail down hello list toohello next region, and so on.</span></span>

<span data-ttu-id="8f533-118">Hello SDK tenterà solo tooread dalle aree hello specificato in PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="8f533-118">hello SDKs will only attempt tooread from hello regions specified in PreferredLocations.</span></span> <span data-ttu-id="8f533-119">In tal caso, ad esempio, se hello Account del Database è disponibile in tre aree, ma client hello specifica solo due delle aree non scrittura hello per PreferredLocations, quindi non letture verranno utilizzate da area di scrittura hello, anche nel caso di hello di failover.</span><span class="sxs-lookup"><span data-stu-id="8f533-119">So, for example, if hello Database Account is available in three regions, but hello client only specifies two of hello non-write regions for PreferredLocations, then no reads will be served out of hello write region, even in hello case of failover.</span></span>

<span data-ttu-id="8f533-120">un'applicazione Hello possibile verificare l'endpoint di scrittura corrente hello e leggere endpoint scelto da hello SDK dal controllo due proprietà, WriteEndpoint e ReadEndpoint, disponibili nella versione SDK 1.8 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="8f533-120">hello application can verify hello current write endpoint and read endpoint chosen by hello SDK by checking two properties, WriteEndpoint and ReadEndpoint, available in SDK version 1.8 and above.</span></span>

<span data-ttu-id="8f533-121">Se non è impostata la proprietà PreferredLocations hello, verranno utilizzate dall'area di scrittura corrente hello tutte le richieste.</span><span class="sxs-lookup"><span data-stu-id="8f533-121">If hello PreferredLocations property is not set, all requests will be served from hello current write region.</span></span>

## <a name="net-sdk"></a><span data-ttu-id="8f533-122">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="8f533-122">.NET SDK</span></span>
<span data-ttu-id="8f533-123">Hello SDK è utilizzabile senza alcuna modifica al codice.</span><span class="sxs-lookup"><span data-stu-id="8f533-123">hello SDK can be used without any code changes.</span></span> <span data-ttu-id="8f533-124">In questo caso, hello SDK automaticamente indirizza entrambe le operazioni di lettura e scrive toohello area di scrittura corrente.</span><span class="sxs-lookup"><span data-stu-id="8f533-124">In this case, hello SDK automatically directs both reads and writes toohello current write region.</span></span>

<span data-ttu-id="8f533-125">Nella versione 1.8 e versioni successive di .NET SDK hello, hello del parametro ConnectionPolicy per costruttore DocumentClient hello è una proprietà denominata Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="8f533-125">In version 1.8 and later of hello .NET SDK, hello ConnectionPolicy parameter for hello DocumentClient constructor has a property called Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="8f533-126">Questa proprietà è di tipo raccolta `<string>` e deve contenere un elenco di nomi di aree.</span><span class="sxs-lookup"><span data-stu-id="8f533-126">This property is of type Collection `<string>` and should contain a list of region names.</span></span> <span data-ttu-id="8f533-127">per ogni colonna di nome dell'area di hello in hello vengono formattati i valori di stringa Hello [aree di Azure] [ regions] pagina, senza spazi prima o dopo hello prima e l'ultimo carattere rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="8f533-127">hello string values are formatted per hello Region Name column on hello [Azure Regions][regions] page, with no spaces before or after hello first and last character respectively.</span></span>

<span data-ttu-id="8f533-128">scrittura corrente Hello e lettura di endpoint sono disponibili in DocumentClient.WriteEndpoint e DocumentClient.ReadEndpoint rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="8f533-128">hello current write and read endpoints are available in DocumentClient.WriteEndpoint and DocumentClient.ReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="8f533-129">Hello URL per gli endpoint di hello non deve essere considerato come costanti di lunga durate.</span><span class="sxs-lookup"><span data-stu-id="8f533-129">hello URLs for hello endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="8f533-130">servizio Hello può aggiornare questi in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="8f533-130">hello service may update these at any point.</span></span> <span data-ttu-id="8f533-131">Hello SDK gestisce automaticamente questa modifica.</span><span class="sxs-lookup"><span data-stu-id="8f533-131">hello SDK handles this change automatically.</span></span>
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

## <a name="nodejs-javascript-and-python-sdks"></a><span data-ttu-id="8f533-132">SDK di NodeJS, JavaScript e Python</span><span class="sxs-lookup"><span data-stu-id="8f533-132">NodeJS, JavaScript, and Python SDKs</span></span>
<span data-ttu-id="8f533-133">Hello SDK è utilizzabile senza alcuna modifica al codice.</span><span class="sxs-lookup"><span data-stu-id="8f533-133">hello SDK can be used without any code changes.</span></span> <span data-ttu-id="8f533-134">In questo caso, hello che SDK indirizzerà automaticamente sia legge e scrive toohello area di scrittura corrente.</span><span class="sxs-lookup"><span data-stu-id="8f533-134">In this case, hello SDK will automatically direct both reads and writes toohello current write region.</span></span>

<span data-ttu-id="8f533-135">Nella versione 1.8 e versioni successive di ogni SDK, hello ConnectionPolicy parametro hello DocumentClient costruttore una nuova proprietà denominata DocumentClient.ConnectionPolicy.PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="8f533-135">In version 1.8 and later of each SDK, hello ConnectionPolicy parameter for hello DocumentClient constructor a new property called DocumentClient.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="8f533-136">Questo parametro è una matrice di stringhe che accetta un elenco di nomi di aree.</span><span class="sxs-lookup"><span data-stu-id="8f533-136">This is parameter is an array of strings that takes a list of region names.</span></span> <span data-ttu-id="8f533-137">i nomi di Hello vengono formattati per ogni colonna di nome dell'area di hello in hello [aree di Azure] [ regions] pagina.</span><span class="sxs-lookup"><span data-stu-id="8f533-137">hello names are formatted per hello Region Name column in hello [Azure Regions][regions] page.</span></span> <span data-ttu-id="8f533-138">È inoltre possibile utilizzare costanti hello predefinito nell'oggetto praticità hello AzureDocuments.Regions</span><span class="sxs-lookup"><span data-stu-id="8f533-138">You can also use hello predefined constants in hello convenience object AzureDocuments.Regions</span></span>

<span data-ttu-id="8f533-139">scrittura corrente Hello e lettura di endpoint sono disponibili in DocumentClient.getWriteEndpoint e DocumentClient.getReadEndpoint rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="8f533-139">hello current write and read endpoints are available in DocumentClient.getWriteEndpoint and DocumentClient.getReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="8f533-140">Hello URL per gli endpoint di hello non deve essere considerato come costanti di lunga durate.</span><span class="sxs-lookup"><span data-stu-id="8f533-140">hello URLs for hello endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="8f533-141">servizio Hello può aggiornare questi in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="8f533-141">hello service may update these at any point.</span></span> <span data-ttu-id="8f533-142">Hello SDK gestirà automaticamente questa modifica.</span><span class="sxs-lookup"><span data-stu-id="8f533-142">hello SDK will handle this change automatically.</span></span>
>
>

<span data-ttu-id="8f533-143">Di seguito è riportato un esempio di codice per NodeJS/Javascript.</span><span class="sxs-lookup"><span data-stu-id="8f533-143">Below is a code example for NodeJS/Javascript.</span></span> <span data-ttu-id="8f533-144">Python e Java seguirà hello stesso modello.</span><span class="sxs-lookup"><span data-stu-id="8f533-144">Python and Java will follow hello same pattern.</span></span>

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

## <a name="rest"></a><span data-ttu-id="8f533-145">REST</span><span class="sxs-lookup"><span data-stu-id="8f533-145">REST</span></span>
<span data-ttu-id="8f533-146">Una volta che un account del database è stata resa disponibile in più aree, i client possono eseguire query la sua disponibilità eseguendo una richiesta GET su hello seguente URI.</span><span class="sxs-lookup"><span data-stu-id="8f533-146">Once a database account has been made available in multiple regions, clients can query its availability by performing a GET request on hello following URI.</span></span>

    https://{databaseaccount}.documents.azure.com/

<span data-ttu-id="8f533-147">servizio Hello restituirà un elenco delle aree e i relativi endpoint di Azure Cosmos DB URI corrispondente per le repliche hello.</span><span class="sxs-lookup"><span data-stu-id="8f533-147">hello service will return a list of regions and their corresponding Azure Cosmos DB endpoint URIs for hello replicas.</span></span> <span data-ttu-id="8f533-148">area di scrittura corrente Hello viene indicato nella risposta hello.</span><span class="sxs-lookup"><span data-stu-id="8f533-148">hello current write region will be indicated in hello response.</span></span> <span data-ttu-id="8f533-149">client Hello quindi possibile selezionare endpoint appropriato di hello per le richieste API REST di tutte le ulteriori come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="8f533-149">hello client can then select hello appropriate endpoint for all further REST API requests as follows.</span></span>

<span data-ttu-id="8f533-150">Risposta di esempio</span><span class="sxs-lookup"><span data-stu-id="8f533-150">Example response</span></span>

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


* <span data-ttu-id="8f533-151">Le richieste di tutti i PUT, POST e DELETE è necessario che venga indicato toohello scrivere URI</span><span class="sxs-lookup"><span data-stu-id="8f533-151">All PUT, POST and DELETE requests must go toohello indicated write URI</span></span>
* <span data-ttu-id="8f533-152">Ottiene tutti e altre richieste di sola lettura (ad esempio query) torni tooany endpoint scelto hello client</span><span class="sxs-lookup"><span data-stu-id="8f533-152">All GETs and other read-only requests (for example queries) may go tooany endpoint of hello client’s choice</span></span>

<span data-ttu-id="8f533-153">Scrivere le richieste solo tooread aree avrà esito negativo con codice di errore HTTP 403 ("accesso negato").</span><span class="sxs-lookup"><span data-stu-id="8f533-153">Write requests tooread-only regions will fail with HTTP error code 403 (“Forbidden”).</span></span>

<span data-ttu-id="8f533-154">Se l'area di scrittura hello viene modificata dopo la fase di individuazione iniziale del client hello, successive scrive toohello precedente area scrittura avrà esito negativo con codice di errore HTTP 403 ("accesso negato").</span><span class="sxs-lookup"><span data-stu-id="8f533-154">If hello write region changes after hello client’s initial discovery phase, subsequent writes toohello previous write region will fail with HTTP error code 403 (“Forbidden”).</span></span> <span data-ttu-id="8f533-155">client Hello deve quindi ottenere elenco hello delle aree nuovamente tooget hello scrittura aggiornato area.</span><span class="sxs-lookup"><span data-stu-id="8f533-155">hello client should then GET hello list of regions again tooget hello updated write region.</span></span>

<span data-ttu-id="8f533-156">L'esercitazione è terminata.</span><span class="sxs-lookup"><span data-stu-id="8f533-156">That's it, that completes this tutorial.</span></span> <span data-ttu-id="8f533-157">È possibile ottenere informazioni come toomanage hello la coerenza dell'account di replicato globalmente leggendo [livelli di coerenza nel database di Azure Cosmos](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="8f533-157">You can learn how toomanage hello consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="8f533-158">Per informazioni sul funzionamento della replica di database globale in Azure Cosmos DB, vedere [Distribuire i dati a livello globale con Azure Cosmos DB](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="8f533-158">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f533-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8f533-159">Next steps</span></span>

<span data-ttu-id="8f533-160">In questa esercitazione, effettuata seguente hello:</span><span class="sxs-lookup"><span data-stu-id="8f533-160">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8f533-161">Configurare la distribuzione globale mediante hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="8f533-161">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="8f533-162">Configurare la distribuzione globale mediante hello APIs DocumentDB</span><span class="sxs-lookup"><span data-stu-id="8f533-162">Configure global distribution using hello DocumentDB APIs</span></span>

<span data-ttu-id="8f533-163">È ora possibile procedere toolearn esercitazione successiva toohello come toodevelop localmente tramite hello emulatore locale di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8f533-163">You can now proceed toohello next tutorial toolearn how toodevelop locally using hello Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8f533-164">Sviluppare in locale con emulator hello</span><span class="sxs-lookup"><span data-stu-id="8f533-164">Develop locally with hello emulator</span></span>](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

