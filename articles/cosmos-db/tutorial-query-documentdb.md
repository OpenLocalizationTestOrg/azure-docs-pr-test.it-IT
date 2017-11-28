---
title: tooquery aaaHow con SQL nel database di Azure Cosmos? | Microsoft Docs
description: Informazioni su tooquery con dati DocumentDB con SQL nel database di Azure Cosmos
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: tutorial-develop
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: d3dc51acf92cb78d4f4d9dbac7ec54b1382431cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-using-sql"></a><span data-ttu-id="4f458-104">Azure Cosmos DB: Modalità tooquery utilizzando SQL?</span><span class="sxs-lookup"><span data-stu-id="4f458-104">Azure Cosmos DB: How tooquery using SQL?</span></span>

<span data-ttu-id="4f458-105">Hello Azure Cosmos DB [API DocumentDB](documentdb-introduction.md) supporta l'esecuzione di query di documenti con SQL.</span><span class="sxs-lookup"><span data-stu-id="4f458-105">hello Azure Cosmos DB [DocumentDB API](documentdb-introduction.md) supports querying documents using SQL.</span></span> <span data-ttu-id="4f458-106">Questo articolo include un documento di esempio e due esempi di query SQL e relativi risultati.</span><span class="sxs-lookup"><span data-stu-id="4f458-106">This article provides a sample document and two sample SQL queries and results.</span></span>

<span data-ttu-id="4f458-107">Questo articolo descrive hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="4f458-107">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="4f458-108">Esecuzione di query sui dati con SQL</span><span class="sxs-lookup"><span data-stu-id="4f458-108">Querying data with SQL</span></span>

## <a name="sample-document"></a><span data-ttu-id="4f458-109">Documento di esempio</span><span class="sxs-lookup"><span data-stu-id="4f458-109">Sample document</span></span>

<span data-ttu-id="4f458-110">query SQL Hello in questo articolo utilizzare hello successivo documento di esempio.</span><span class="sxs-lookup"><span data-stu-id="4f458-110">hello SQL queries in this article use hello following sample document.</span></span>

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam", 
        "givenName": "Jesse", 
        "gender": "female", "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller", 
         "givenName": "Lisa", 
         "gender": "female", 
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```
## <a name="where-can-i-run-sql-queries"></a><span data-ttu-id="4f458-111">Dove è possibile eseguire query SQL?</span><span class="sxs-lookup"><span data-stu-id="4f458-111">Where can I run SQL queries?</span></span>

<span data-ttu-id="4f458-112">È possibile eseguire le query che utilizzano hello Esplora dati nel portale di Azure tramite hello hello [SDK e API REST](documentdb-sdk-dotnet.md)e anche hello [Query playground](https://www.documentdb.com/sql/demo), che consente di eseguire query su un set di dati di esempio esistente.</span><span class="sxs-lookup"><span data-stu-id="4f458-112">You can run queries using hello Data Explorer in hello Azure portal, via hello [REST API and SDKs](documentdb-sdk-dotnet.md), and even hello [Query playground](https://www.documentdb.com/sql/demo), which runs queries on an existing set of sample data.</span></span>

<span data-ttu-id="4f458-113">Per altre informazioni sulle query SQL, vedere:</span><span class="sxs-lookup"><span data-stu-id="4f458-113">For more information about SQL queries, see:</span></span>
* [<span data-ttu-id="4f458-114">Query e sintassi SQL</span><span class="sxs-lookup"><span data-stu-id="4f458-114">SQL query and SQL syntax</span></span>](documentdb-sql-query.md)

## <a name="prerequisites"></a><span data-ttu-id="4f458-115">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4f458-115">Prerequisites</span></span>

<span data-ttu-id="4f458-116">L'esercitazione presuppone la presenza di un account e di una raccolta di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="4f458-116">This tutorial assumes you have an Azure Cosmos DB account and collection.</span></span> <span data-ttu-id="4f458-117">Questi requisiti non sono disponibili?</span><span class="sxs-lookup"><span data-stu-id="4f458-117">Don't have any of those?</span></span> <span data-ttu-id="4f458-118">Hello completo [avvio rapido di 5 minuti](create-mongodb-nodejs.md) o hello [esercitazione developer](tutorial-develop-mongodb.md) toocreate un account e una raccolta.</span><span class="sxs-lookup"><span data-stu-id="4f458-118">Complete hello [5-minute quickstart](create-mongodb-nodejs.md) or hello [developer tutorial](tutorial-develop-mongodb.md) toocreate an account and collection.</span></span>

## <a name="example-query-1"></a><span data-ttu-id="4f458-119">Query di esempio 1</span><span class="sxs-lookup"><span data-stu-id="4f458-119">Example query 1</span></span>

<span data-ttu-id="4f458-120">Hello famiglia documento di esempio precedente, query SQL seguente restituisce documenti hello in cui corrisponde il campo di id hello `WakefieldFamily`.</span><span class="sxs-lookup"><span data-stu-id="4f458-120">Given hello sample family document above, following SQL query returns hello documents where hello id field matches `WakefieldFamily`.</span></span> <span data-ttu-id="4f458-121">Poiché si tratta di un `SELECT *` istruzione, l'output di hello di query hello è documento JSON completo hello:</span><span class="sxs-lookup"><span data-stu-id="4f458-121">Since it's a `SELECT *` statement, hello output of hello query is hello complete JSON document:</span></span>

<span data-ttu-id="4f458-122">**Query**</span><span class="sxs-lookup"><span data-stu-id="4f458-122">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "WakefieldFamily"

<span data-ttu-id="4f458-123">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="4f458-123">**Results**</span></span>

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam", 
        "givenName": "Jesse", 
        "gender": "female", "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller", 
         "givenName": "Lisa", 
         "gender": "female", 
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```

## <a name="example-query-2"></a><span data-ttu-id="4f458-124">Query di esempio 2</span><span class="sxs-lookup"><span data-stu-id="4f458-124">Example query 2</span></span>

<span data-ttu-id="4f458-125">la query successiva Hello restituisce tutti i nomi di hello specificato di elementi figlio nella famiglia di hello il cui id corrisponde `WakefieldFamily` ordinati in base al loro grado.</span><span class="sxs-lookup"><span data-stu-id="4f458-125">hello next query returns all hello given names of children in hello family whose id matches `WakefieldFamily` ordered by their grade.</span></span>

<span data-ttu-id="4f458-126">**Query**</span><span class="sxs-lookup"><span data-stu-id="4f458-126">**Query**</span></span>

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.children.grade ASC

<span data-ttu-id="4f458-127">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="4f458-127">**Results**</span></span>

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


## <a name="next-steps"></a><span data-ttu-id="4f458-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4f458-128">Next steps</span></span>

<span data-ttu-id="4f458-129">In questa esercitazione, effettuata seguente hello:</span><span class="sxs-lookup"><span data-stu-id="4f458-129">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4f458-130">Appreso tooquery tramite SQL</span><span class="sxs-lookup"><span data-stu-id="4f458-130">Learned how tooquery using SQL</span></span>  

<span data-ttu-id="4f458-131">È ora possibile procedere come toolearn esercitazione successiva toohello toodistribute i dati a livello globale.</span><span class="sxs-lookup"><span data-stu-id="4f458-131">You can now proceed toohello next tutorial toolearn how toodistribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4f458-132">Distribuire i dati a livello globale</span><span class="sxs-lookup"><span data-stu-id="4f458-132">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)

