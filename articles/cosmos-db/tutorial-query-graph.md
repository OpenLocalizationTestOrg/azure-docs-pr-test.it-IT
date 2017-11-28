---
title: dati del grafico tooquery aaaHow nel database di Azure Cosmos? | Microsoft Docs
description: Informazioni su dati del grafico tooquery nel database di Azure Cosmos
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
tags: 
ms.assetid: 8bde5c80-581c-4f70-acb4-9578873c92fa
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: denlee
ms.openlocfilehash: fdde881edd6c488e2fea51e5c9665e1d736009fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-with-hello-graph-api-preview"></a><span data-ttu-id="d3833-104">Azure Cosmos DB: Modalità tooquery con hello API Graph (anteprima)?</span><span class="sxs-lookup"><span data-stu-id="d3833-104">Azure Cosmos DB: How tooquery with hello Graph API (preview)?</span></span>

<span data-ttu-id="d3833-105">Hello Azure Cosmos DB [API Graph](graph-introduction.md) (anteprima) supporta [Gremlin](https://docs.mongodb.com/manual/tutorial/query-documents/) query.</span><span class="sxs-lookup"><span data-stu-id="d3833-105">hello Azure Cosmos DB [Graph API](graph-introduction.md) (preview) supports [Gremlin](https://docs.mongodb.com/manual/tutorial/query-documents/) queries.</span></span> <span data-ttu-id="d3833-106">In questo articolo fornisce documenti di esempio e tooget che è stata avviata una query.</span><span class="sxs-lookup"><span data-stu-id="d3833-106">This article provides sample documents and queries tooget you started.</span></span> <span data-ttu-id="d3833-107">Viene fornito un riferimento dettagliato di Gremlin in hello [supporto Gremlin](gremlin-support.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="d3833-107">A detailed Gremlin reference is provided in hello [Gremlin support](gremlin-support.md) article.</span></span>

<span data-ttu-id="d3833-108">Questo articolo descrive hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="d3833-108">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="d3833-109">Esecuzione di query sui dati con Gremlin</span><span class="sxs-lookup"><span data-stu-id="d3833-109">Querying data with Gremlin</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d3833-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d3833-110">Prerequisites</span></span>

<span data-ttu-id="d3833-111">Per toowork queste query, è necessario disporre di un account Azure Cosmos DB e disporre di dati del grafico nel contenitore hello.</span><span class="sxs-lookup"><span data-stu-id="d3833-111">For these queries toowork, you must have an Azure Cosmos DB account and have graph data in hello container.</span></span> <span data-ttu-id="d3833-112">Questi requisiti non sono disponibili?</span><span class="sxs-lookup"><span data-stu-id="d3833-112">Don't have any of those?</span></span> <span data-ttu-id="d3833-113">Hello completo [avvio rapido di 5 minuti](create-graph-dotnet.md) o hello [esercitazione developer](tutorial-query-graph.md) toocreate un account e popolare il database.</span><span class="sxs-lookup"><span data-stu-id="d3833-113">Complete hello [5-minute quickstart](create-graph-dotnet.md) or hello [developer tutorial](tutorial-query-graph.md) toocreate an account and populate your database.</span></span> <span data-ttu-id="d3833-114">È possibile eseguire dopo le query che utilizzano hello hello [libreria graph di Azure Cosmos DB .NET](graph-sdk-dotnet.md), [console Gremlin](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console), o il driver Gremlin preferito.</span><span class="sxs-lookup"><span data-stu-id="d3833-114">You can run hello following queries using hello [Azure Cosmos DB .NET graph library](graph-sdk-dotnet.md), [Gremlin console](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console), or your favorite Gremlin driver.</span></span>

## <a name="count-vertices-in-hello-graph"></a><span data-ttu-id="d3833-115">Numero di vertici nel grafico hello</span><span class="sxs-lookup"><span data-stu-id="d3833-115">Count vertices in hello graph</span></span>

<span data-ttu-id="d3833-116">Hello frammento di codice seguente viene illustrato come toocount hello numero di vertici nel grafico hello:</span><span class="sxs-lookup"><span data-stu-id="d3833-116">hello following snippet shows how toocount hello number of vertices in hello graph:</span></span>

```
g.V().count()
```

## <a name="filters"></a><span data-ttu-id="d3833-117">Filtri</span><span class="sxs-lookup"><span data-stu-id="d3833-117">Filters</span></span>

<span data-ttu-id="d3833-118">È possibile eseguire filtri utilizzando Gremlin `has` e `hasLabel` i passaggi e combinarli con `and`, `or`, e `not` toobuild più complessa di filtri.</span><span class="sxs-lookup"><span data-stu-id="d3833-118">You can perform filters using Gremlin's `has` and `hasLabel` steps, and combine them using `and`, `or`, and `not` toobuild more complex filters.</span></span> <span data-ttu-id="d3833-119">Per velocizzare le query, Azure DB Cosmos consente l'indicizzazione senza schema di tutte le proprietà all'interno di vertici e gradi.</span><span class="sxs-lookup"><span data-stu-id="d3833-119">Azure Cosmos DB provides schema-agnostic indexing of all properties within your vertices and degrees for fast queries:</span></span>

```
g.V().hasLabel('person').has('age', gt(40))
```

## <a name="projection"></a><span data-ttu-id="d3833-120">Proiezione</span><span class="sxs-lookup"><span data-stu-id="d3833-120">Projection</span></span>

<span data-ttu-id="d3833-121">È possibile proiettare determinate proprietà nei risultati della query hello utilizzando hello `values` passaggio:</span><span class="sxs-lookup"><span data-stu-id="d3833-121">You can project certain properties in hello query results using hello `values` step:</span></span>

```
g.V().hasLabel('person').values('firstName')
```

## <a name="find-related-edges-and-vertices"></a><span data-ttu-id="d3833-122">Trovare vertici e archi correlati</span><span class="sxs-lookup"><span data-stu-id="d3833-122">Find related edges and vertices</span></span>

<span data-ttu-id="d3833-123">Finora sono stati esaminati solo gli operatori di query che è possibile usare in qualsiasi database.</span><span class="sxs-lookup"><span data-stu-id="d3833-123">So far, we've only seen query operators that work in any database.</span></span> <span data-ttu-id="d3833-124">Grafici sono veloci ed efficienti per le operazioni di attraversamento quando è necessario toonavigate toorelated bordi e i vertici.</span><span class="sxs-lookup"><span data-stu-id="d3833-124">Graphs are fast and efficient for traversal operations when you need toonavigate toorelated edges and vertices.</span></span> <span data-ttu-id="d3833-125">Verranno ora individuati tutti gli amici di Thomas.</span><span class="sxs-lookup"><span data-stu-id="d3833-125">Let's find all friends of Thomas.</span></span> <span data-ttu-id="d3833-126">Facciamo utilizzando del Gremlin `outE` passaggio toofind hello tutti i bordi in uscita da Thomas, quindi attraversamento toohello in vertici da tali usando del Gremlin `inV` passaggio:</span><span class="sxs-lookup"><span data-stu-id="d3833-126">We do this by using Gremlin's `outE` step toofind all hello out-edges from Thomas, then traversing toohello in-vertices from those edges using Gremlin's `inV` step:</span></span>

```cs
g.V('thomas').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="d3833-127">la query successiva Hello esegue due hop toofind tutti "agli amici di Thomas di amici", chiamando `outE` e `inV` due volte.</span><span class="sxs-lookup"><span data-stu-id="d3833-127">hello next query performs two hops toofind all of Thomas' "friends of friends", by calling `outE` and `inV` two times.</span></span> 

```cs
g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="d3833-128">È possibile compilare query più complesse e implementare la logica di attraversamento potente grafico utilizzando Gremlin, tra cui filtro combinazione espressioni, esecuzione di ciclo tramite hello `loop` passaggio e la navigazione condizionale implementazione utilizzando hello `choose` passaggio.</span><span class="sxs-lookup"><span data-stu-id="d3833-128">You can build more complex queries and implement powerful graph traversal logic using Gremlin, including mixing filter expressions, performing looping using hello `loop` step, and implementing conditional navigation using hello `choose` step.</span></span> <span data-ttu-id="d3833-129">Altre informazioni sulle operazioni che è possibile eseguire con il [supporto per Gremlin](gremlin-support.md).</span><span class="sxs-lookup"><span data-stu-id="d3833-129">Learn more about what you can do with [Gremlin support](gremlin-support.md)!</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3833-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d3833-130">Next steps</span></span>

<span data-ttu-id="d3833-131">In questa esercitazione, effettuata seguente hello:</span><span class="sxs-lookup"><span data-stu-id="d3833-131">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d3833-132">Appreso tooquery mediante Graph</span><span class="sxs-lookup"><span data-stu-id="d3833-132">Learned how tooquery using Graph</span></span> 

<span data-ttu-id="d3833-133">È ora possibile procedere come toolearn esercitazione successiva toohello toodistribute i dati a livello globale.</span><span class="sxs-lookup"><span data-stu-id="d3833-133">You can now proceed toohello next tutorial toolearn how toodistribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d3833-134">Distribuire i dati a livello globale</span><span class="sxs-lookup"><span data-stu-id="d3833-134">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)