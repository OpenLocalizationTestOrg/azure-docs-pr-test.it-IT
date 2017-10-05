---
title: Esercitazione sulla distribuzione globale in Azure Cosmos DB per l'API MongoDB | Documentazione Microsoft
description: Informazioni su come configurare la distribuzione globale in Azure Cosmos DB usando l'API MongoDB.
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
ms.openlocfilehash: a2747102f4d8cac412b67abc3fd07cfa3661bcee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-setup-azure-cosmos-db-global-distribution-using-the-mongodb-api"></a><span data-ttu-id="534a0-104">Procedura di configurazione della distribuzione globale in Azure Cosmos DB usando l'API MongoDB</span><span class="sxs-lookup"><span data-stu-id="534a0-104">How to setup Azure Cosmos DB global distribution using the MongoDB API</span></span>

<span data-ttu-id="534a0-105">Questo articolo illustra come usare il portale di Azure per configurare la distribuzione globale in Azure Cosmos DB e quindi connettersi tramite l'API MongoDB.</span><span class="sxs-lookup"><span data-stu-id="534a0-105">In this article, we show how to use the Azure portal to setup Azure Cosmos DB global distribution and then connect using the MongoDB API.</span></span>

<span data-ttu-id="534a0-106">Questo articolo illustra le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="534a0-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="534a0-107">Configurare la distribuzione globale tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="534a0-107">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="534a0-108">Configurare la distribuzione globale tramite l'[API MongoDB](mongodb-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="534a0-108">Configure global distribution using the [MongoDB API](mongodb-introduction.md)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]

## <a name="verifying-your-regional-setup-using-the-mongodb-api"></a><span data-ttu-id="534a0-109">Verifica della configurazione a livello di area usando l'API MongoDB</span><span class="sxs-lookup"><span data-stu-id="534a0-109">Verifying your regional setup using the MongoDB API</span></span>
<span data-ttu-id="534a0-110">Il modo più semplice per verificare in modo approfondito la configurazione globale nell'API per MongoDB consiste nell'eseguire il comando *isMaster()* da Mongo Shell.</span><span class="sxs-lookup"><span data-stu-id="534a0-110">The simplest way of double checking your global configuration within API for MongoDB is to run the *isMaster()* command from the Mongo Shell.</span></span>

<span data-ttu-id="534a0-111">Da Mongo Shell:</span><span class="sxs-lookup"><span data-stu-id="534a0-111">From your Mongo Shell:</span></span>

   ```
      db.isMaster()
   ```
   
<span data-ttu-id="534a0-112">Risultati dell'esempio:</span><span class="sxs-lookup"><span data-stu-id="534a0-112">Example results:</span></span>

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

## <a name="connecting-to-a-preferred-region-using-the-mongodb-api"></a><span data-ttu-id="534a0-113">Connessione a un'area preferita tramite l'API MongoDB</span><span class="sxs-lookup"><span data-stu-id="534a0-113">Connecting to a preferred region using the MongoDB API</span></span>

<span data-ttu-id="534a0-114">L'API MongoDB consente di specificare le preferenze di lettura della raccolta per un database distribuito globalmente.</span><span class="sxs-lookup"><span data-stu-id="534a0-114">The MongoDB API enables you to specify your collection's read preference for a globally distributed database.</span></span> <span data-ttu-id="534a0-115">Per ottenere letture a bassa latenza e disponibilità elevata globale, è consigliabile impostare le preferenze di lettura della raccolta su *nearest*.</span><span class="sxs-lookup"><span data-stu-id="534a0-115">For both low latency reads and global high availability, we recommend setting your collection's read preference to *nearest*.</span></span> <span data-ttu-id="534a0-116">Una preferenza di lettura di tipo *nearest* viene configurata per la lettura dall'area più vicina.</span><span class="sxs-lookup"><span data-stu-id="534a0-116">A read preference of *nearest* is configured to read from the closest region.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Nearest));
```

<span data-ttu-id="534a0-117">Per applicazioni con un'area di lettura/scrittura primaria e un'area secondaria per scenari di ripristino di emergenza, è consigliabile impostare le preferenze di lettura della raccolta su *secondary preferred*.</span><span class="sxs-lookup"><span data-stu-id="534a0-117">For applications with a primary read/write region and a secondary region for disaster recovery (DR) scenarios, we recommend setting your collection's read preference to *secondary preferred*.</span></span> <span data-ttu-id="534a0-118">Una preferenza di lettura di tipo *secondary preferred* viene configurata per la lettura dall'area secondaria quando l'area primaria non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="534a0-118">A read preference of *secondary preferred* is configured to read from the secondary region when the primary region is unavailable.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.SecondaryPreferred));
```

<span data-ttu-id="534a0-119">Se infine si vogliono specificare manualmente le aree di lettura,</span><span class="sxs-lookup"><span data-stu-id="534a0-119">Lastly, if you would like to manually specify your read regions.</span></span> <span data-ttu-id="534a0-120">è possibile impostare il valore Tag per l'area entro la preferenza di lettura.</span><span class="sxs-lookup"><span data-stu-id="534a0-120">You can set the region Tag within your read preference.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
var tag = new Tag("region", "Southeast Asia");
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Secondary, new[] { new TagSet(new[] { tag }) }));
```

<span data-ttu-id="534a0-121">L'esercitazione è terminata.</span><span class="sxs-lookup"><span data-stu-id="534a0-121">That's it, that completes this tutorial.</span></span> <span data-ttu-id="534a0-122">Per informazioni su come gestire la coerenza dell'account con replica globale, vedere [Livelli di coerenza in Azure Cosmos DB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="534a0-122">You can learn how to manage the consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="534a0-123">Per informazioni sul funzionamento della replica di database globale in Azure Cosmos DB, vedere [Distribuire i dati a livello globale con Azure Cosmos DB](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="534a0-123">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="534a0-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="534a0-124">Next steps</span></span>

<span data-ttu-id="534a0-125">In questa esercitazione sono state eseguite le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="534a0-125">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="534a0-126">Configurare la distribuzione globale tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="534a0-126">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="534a0-127">Configurare la distribuzione globale tramite le API di DocumentDB</span><span class="sxs-lookup"><span data-stu-id="534a0-127">Configure global distribution using the DocumentDB APIs</span></span>

<span data-ttu-id="534a0-128">È ora possibile passare all'esercitazione successiva per imparare a sviluppare in locale usando l'emulatore locale di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="534a0-128">You can now proceed to the next tutorial to learn how to develop locally using the Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="534a0-129">Sviluppare in locale con l'emulatore</span><span class="sxs-lookup"><span data-stu-id="534a0-129">Develop locally with the emulator</span></span>](local-emulator.md)