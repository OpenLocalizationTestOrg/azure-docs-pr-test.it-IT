---
title: Procedura per l'esecuzione di query sui dati grafo in SQL in Azure Cosmos DB | Microsoft Docs
description: Informazioni sull'esecuzione di query sui dati grafo in Azure Cosmos DB
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
ms.openlocfilehash: 81713c72da037f127e81239d214d7a877247dca1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-how-to-query-with-the-graph-api-preview"></a><span data-ttu-id="94838-104">Azure Cosmos DB: procedura per l'esecuzione di query con l'API Graph (anteprima)</span><span class="sxs-lookup"><span data-stu-id="94838-104">Azure Cosmos DB: How to query with the Graph API (preview)?</span></span>

<span data-ttu-id="94838-105">L'[API Graph](graph-introduction.md) di Azure Cosmos DB (anteprima) supporta le query [Gremlin](https://docs.mongodb.com/manual/tutorial/query-documents/).</span><span class="sxs-lookup"><span data-stu-id="94838-105">The Azure Cosmos DB [Graph API](graph-introduction.md) (preview) supports [Gremlin](https://docs.mongodb.com/manual/tutorial/query-documents/) queries.</span></span> <span data-ttu-id="94838-106">Questo articolo include esempi di documenti e query per iniziare.</span><span class="sxs-lookup"><span data-stu-id="94838-106">This article provides sample documents and queries to get you started.</span></span> <span data-ttu-id="94838-107">L'articolo relativo al [supporto Gremlin](gremlin-support.md) include riferimenti Gremlin dettagliati.</span><span class="sxs-lookup"><span data-stu-id="94838-107">A detailed Gremlin reference is provided in the [Gremlin support](gremlin-support.md) article.</span></span>

<span data-ttu-id="94838-108">Questo articolo illustra le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="94838-108">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="94838-109">Esecuzione di query sui dati con Gremlin</span><span class="sxs-lookup"><span data-stu-id="94838-109">Querying data with Gremlin</span></span>

## <a name="prerequisites"></a><span data-ttu-id="94838-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="94838-110">Prerequisites</span></span>

<span data-ttu-id="94838-111">Per il funzionamento di queste query è necessario disporre di un account Azure Cosmos DB e nel contenitore devono essere presenti dati grafo.</span><span class="sxs-lookup"><span data-stu-id="94838-111">For these queries to work, you must have an Azure Cosmos DB account and have graph data in the container.</span></span> <span data-ttu-id="94838-112">Questi requisiti non sono disponibili?</span><span class="sxs-lookup"><span data-stu-id="94838-112">Don't have any of those?</span></span> <span data-ttu-id="94838-113">Completare la [Guida introduttiva di 5 minuti](create-graph-dotnet.md) o l'[esercitazione per sviluppatori](tutorial-query-graph.md) per creare un account e popolare il database.</span><span class="sxs-lookup"><span data-stu-id="94838-113">Complete the [5-minute quickstart](create-graph-dotnet.md) or the [developer tutorial](tutorial-query-graph.md) to create an account and populate your database.</span></span> <span data-ttu-id="94838-114">È possibile eseguire le query seguenti usando la [libreria .NET di grafi di Azure Cosmos DB](graph-sdk-dotnet.md), la [console Gremlin](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console), o il driver Gremlin preferito.</span><span class="sxs-lookup"><span data-stu-id="94838-114">You can run the following queries using the [Azure Cosmos DB .NET graph library](graph-sdk-dotnet.md), [Gremlin console](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console), or your favorite Gremlin driver.</span></span>

## <a name="count-vertices-in-the-graph"></a><span data-ttu-id="94838-115">Numero di vertici nel grafo</span><span class="sxs-lookup"><span data-stu-id="94838-115">Count vertices in the graph</span></span>

<span data-ttu-id="94838-116">Il frammento seguente illustra come contare il numero di vertici nel grafo:</span><span class="sxs-lookup"><span data-stu-id="94838-116">The following snippet shows how to count the number of vertices in the graph:</span></span>

```
g.V().count()
```

## <a name="filters"></a><span data-ttu-id="94838-117">Filtri</span><span class="sxs-lookup"><span data-stu-id="94838-117">Filters</span></span>

<span data-ttu-id="94838-118">È possibile applicare filtri usando i comandi `has` e `hasLabel` di Gremlin e combinarli usando `and`, `or` e `not` per creare filtri più complessi.</span><span class="sxs-lookup"><span data-stu-id="94838-118">You can perform filters using Gremlin's `has` and `hasLabel` steps, and combine them using `and`, `or`, and `not` to build more complex filters.</span></span> <span data-ttu-id="94838-119">Per velocizzare le query, Azure DB Cosmos consente l'indicizzazione senza schema di tutte le proprietà all'interno di vertici e gradi.</span><span class="sxs-lookup"><span data-stu-id="94838-119">Azure Cosmos DB provides schema-agnostic indexing of all properties within your vertices and degrees for fast queries:</span></span>

```
g.V().hasLabel('person').has('age', gt(40))
```

## <a name="projection"></a><span data-ttu-id="94838-120">Proiezione</span><span class="sxs-lookup"><span data-stu-id="94838-120">Projection</span></span>

<span data-ttu-id="94838-121">È possibile proiettare determinate proprietà nei risultati della query usando il comando `values`:</span><span class="sxs-lookup"><span data-stu-id="94838-121">You can project certain properties in the query results using the `values` step:</span></span>

```
g.V().hasLabel('person').values('firstName')
```

## <a name="find-related-edges-and-vertices"></a><span data-ttu-id="94838-122">Trovare vertici e archi correlati</span><span class="sxs-lookup"><span data-stu-id="94838-122">Find related edges and vertices</span></span>

<span data-ttu-id="94838-123">Finora sono stati esaminati solo gli operatori di query che è possibile usare in qualsiasi database.</span><span class="sxs-lookup"><span data-stu-id="94838-123">So far, we've only seen query operators that work in any database.</span></span> <span data-ttu-id="94838-124">I grafi sono veloci ed efficienti per le operazioni di attraversamento quando è necessario passare agli archi e ai vertici correlati.</span><span class="sxs-lookup"><span data-stu-id="94838-124">Graphs are fast and efficient for traversal operations when you need to navigate to related edges and vertices.</span></span> <span data-ttu-id="94838-125">Verranno ora individuati tutti gli amici di Thomas.</span><span class="sxs-lookup"><span data-stu-id="94838-125">Let's find all friends of Thomas.</span></span> <span data-ttu-id="94838-126">Questa operazione viene eseguita usando il comando `outE` di Gremlin per individuare tutti gli archi in uscita da Thomas, quindi attraversando i vertici in ingresso da tali archi usando il comando `inV` di Gremlin:</span><span class="sxs-lookup"><span data-stu-id="94838-126">We do this by using Gremlin's `outE` step to find all the out-edges from Thomas, then traversing to the in-vertices from those edges using Gremlin's `inV` step:</span></span>

```cs
g.V('thomas').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="94838-127">La query successiva esegue due passaggi per trovare tutti "gli amici di amici" di Thomas chiamando `outE` e `inV` due volte.</span><span class="sxs-lookup"><span data-stu-id="94838-127">The next query performs two hops to find all of Thomas' "friends of friends", by calling `outE` and `inV` two times.</span></span> 

```cs
g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="94838-128">È possibile creare query più complesse e implementare la potente logica di attraversamento di grafi usando Gremlin, incluse la combinazione di espressioni di filtro, l'esecuzione di cicli con il comando `loop` e l'implementazione dello spostamento condizionale usando il comando `choose`.</span><span class="sxs-lookup"><span data-stu-id="94838-128">You can build more complex queries and implement powerful graph traversal logic using Gremlin, including mixing filter expressions, performing looping using the `loop` step, and implementing conditional navigation using the `choose` step.</span></span> <span data-ttu-id="94838-129">Altre informazioni sulle operazioni che è possibile eseguire con il [supporto per Gremlin](gremlin-support.md).</span><span class="sxs-lookup"><span data-stu-id="94838-129">Learn more about what you can do with [Gremlin support](gremlin-support.md)!</span></span>

## <a name="next-steps"></a><span data-ttu-id="94838-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="94838-130">Next steps</span></span>

<span data-ttu-id="94838-131">In questa esercitazione sono state eseguite le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="94838-131">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="94838-132">È stato appreso come eseguire una query usando l'API Graph</span><span class="sxs-lookup"><span data-stu-id="94838-132">Learned how to query using Graph</span></span> 

<span data-ttu-id="94838-133">È ora possibile passare all'esercitazione successiva per imparare a distribuire i dati a livello globale.</span><span class="sxs-lookup"><span data-stu-id="94838-133">You can now proceed to the next tutorial to learn how to distribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="94838-134">Distribuire i dati a livello globale</span><span class="sxs-lookup"><span data-stu-id="94838-134">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)