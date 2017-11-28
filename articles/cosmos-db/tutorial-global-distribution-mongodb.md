---
title: esercitazione di distribuzione globale aaaAzure DB Cosmos per MongoDB API | Documenti Microsoft
description: Informazioni su come distribuzione globale di Azure Cosmos DB toosetup utilizzando hello API MongoDB.
services: cosmos-db
keywords: distribuzione globale, MongoDB
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
ms.openlocfilehash: 0fc2d670bb4e21ac5f813f9586b407ba06ccf354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-mongodb-api"></a><span data-ttu-id="c40e3-104">La distribuzione globale di Azure Cosmos DB toosetup utilizzando hello MongoDB API</span><span class="sxs-lookup"><span data-stu-id="c40e3-104">How toosetup Azure Cosmos DB global distribution using hello MongoDB API</span></span>

<span data-ttu-id="c40e3-105">In questo articolo viene illustrata come toouse hello toosetup portale Azure distribuzione globale di Azure Cosmos DB e quindi connettersi usando l'API di MongoDB hello.</span><span class="sxs-lookup"><span data-stu-id="c40e3-105">In this article, we show how toouse hello Azure portal toosetup Azure Cosmos DB global distribution and then connect using hello MongoDB API.</span></span>

<span data-ttu-id="c40e3-106">Questo articolo descrive hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="c40e3-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="c40e3-107">Configurare la distribuzione globale mediante hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c40e3-107">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="c40e3-108">Configurare la distribuzione globale mediante hello [API MongoDB](mongodb-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="c40e3-108">Configure global distribution using hello [MongoDB API](mongodb-introduction.md)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]

## <a name="verifying-your-regional-setup-using-hello-mongodb-api"></a><span data-ttu-id="c40e3-109">Verifica della configurazione internazionale utilizzando hello MongoDB API</span><span class="sxs-lookup"><span data-stu-id="c40e3-109">Verifying your regional setup using hello MongoDB API</span></span>
<span data-ttu-id="c40e3-110">più semplice di controllo della configurazione globale all'interno di API per MongoDB è hello toorun double Hello *isMaster()* comando Shell di Mongo hello.</span><span class="sxs-lookup"><span data-stu-id="c40e3-110">hello simplest way of double checking your global configuration within API for MongoDB is toorun hello *isMaster()* command from hello Mongo Shell.</span></span>

<span data-ttu-id="c40e3-111">Da Mongo Shell:</span><span class="sxs-lookup"><span data-stu-id="c40e3-111">From your Mongo Shell:</span></span>

   ```
      db.isMaster()
   ```
   
<span data-ttu-id="c40e3-112">Risultati dell'esempio:</span><span class="sxs-lookup"><span data-stu-id="c40e3-112">Example results:</span></span>

   ```JSON
      {
         "_t": "IsMasterResponse",
         "ok": 1,
         "ismaster": true,
         "maxMessageSizeBytes": 4194304,
         "maxWriteBatchSize": 1000,
         "minWireVersion": 0,
         "maxWireVersion": 2,
         "tags": {
            "region": "South India"
         },
         "hosts": [
            "vishi-api-for-mongodb-southcentralus.documents.azure.com:10255",
            "vishi-api-for-mongodb-westeurope.documents.azure.com:10255",
            "vishi-api-for-mongodb-southindia.documents.azure.com:10255"
         ],
         "setName": "globaldb",
         "setVersion": 1,
         "primary": "vishi-api-for-mongodb-southindia.documents.azure.com:10255",
         "me": "vishi-api-for-mongodb-southindia.documents.azure.com:10255"
      }
   ```

## <a name="connecting-tooa-preferred-region-using-hello-mongodb-api"></a><span data-ttu-id="c40e3-113">Connessione area geografica preferita tooa utilizzando hello MongoDB API</span><span class="sxs-lookup"><span data-stu-id="c40e3-113">Connecting tooa preferred region using hello MongoDB API</span></span>

<span data-ttu-id="c40e3-114">Hello MongoDB API consente si toospecify delle preferenze di lettura della raccolta per un database distribuito a livello globale.</span><span class="sxs-lookup"><span data-stu-id="c40e3-114">hello MongoDB API enables you toospecify your collection's read preference for a globally distributed database.</span></span> <span data-ttu-id="c40e3-115">Per entrambi bassa latenza letture e disponibilità elevata, si consiglia di impostare preferenze di lettura della raccolta troppo*più vicino*.</span><span class="sxs-lookup"><span data-stu-id="c40e3-115">For both low latency reads and global high availability, we recommend setting your collection's read preference too*nearest*.</span></span> <span data-ttu-id="c40e3-116">Una lettura preferenza *più vicino* è tooread configurato dall'area più vicina hello.</span><span class="sxs-lookup"><span data-stu-id="c40e3-116">A read preference of *nearest* is configured tooread from hello closest region.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Nearest));
```

<span data-ttu-id="c40e3-117">Per le applicazioni con una replica primaria di lettura/scrittura area e un'area secondaria per il ripristino di emergenza (ripristino di emergenza) scenari si consiglia di impostare preferenze di lettura della raccolta troppo*secondario preferito*.</span><span class="sxs-lookup"><span data-stu-id="c40e3-117">For applications with a primary read/write region and a secondary region for disaster recovery (DR) scenarios, we recommend setting your collection's read preference too*secondary preferred*.</span></span> <span data-ttu-id="c40e3-118">Una lettura preferenza *secondario preferito* è tooread configurato dall'area secondaria hello quando l'area primaria hello è disponibile.</span><span class="sxs-lookup"><span data-stu-id="c40e3-118">A read preference of *secondary preferred* is configured tooread from hello secondary region when hello primary region is unavailable.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.SecondaryPreferred));
```

<span data-ttu-id="c40e3-119">Infine, se ad esempio toomanually specificare le aree di lettura.</span><span class="sxs-lookup"><span data-stu-id="c40e3-119">Lastly, if you would like toomanually specify your read regions.</span></span> <span data-ttu-id="c40e3-120">È possibile impostare l'area hello Tag all'interno delle preferenze di lettura.</span><span class="sxs-lookup"><span data-stu-id="c40e3-120">You can set hello region Tag within your read preference.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
var tag = new Tag("region", "Southeast Asia");
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Secondary, new[] { new TagSet(new[] { tag }) }));
```

<span data-ttu-id="c40e3-121">L'esercitazione è terminata.</span><span class="sxs-lookup"><span data-stu-id="c40e3-121">That's it, that completes this tutorial.</span></span> <span data-ttu-id="c40e3-122">È possibile ottenere informazioni come toomanage hello la coerenza dell'account di replicato globalmente leggendo [livelli di coerenza nel database di Azure Cosmos](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="c40e3-122">You can learn how toomanage hello consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="c40e3-123">Per informazioni sul funzionamento della replica di database globale in Azure Cosmos DB, vedere [Distribuire i dati a livello globale con Azure Cosmos DB](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="c40e3-123">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c40e3-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c40e3-124">Next steps</span></span>

<span data-ttu-id="c40e3-125">In questa esercitazione, effettuata seguente hello:</span><span class="sxs-lookup"><span data-stu-id="c40e3-125">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c40e3-126">Configurare la distribuzione globale mediante hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c40e3-126">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="c40e3-127">Configurare la distribuzione globale mediante hello APIs DocumentDB</span><span class="sxs-lookup"><span data-stu-id="c40e3-127">Configure global distribution using hello DocumentDB APIs</span></span>

<span data-ttu-id="c40e3-128">È ora possibile procedere toolearn esercitazione successiva toohello come toodevelop localmente tramite hello emulatore locale di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c40e3-128">You can now proceed toohello next tutorial toolearn how toodevelop locally using hello Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c40e3-129">Sviluppare in locale con emulator hello</span><span class="sxs-lookup"><span data-stu-id="c40e3-129">Develop locally with hello emulator</span></span>](local-emulator.md)
