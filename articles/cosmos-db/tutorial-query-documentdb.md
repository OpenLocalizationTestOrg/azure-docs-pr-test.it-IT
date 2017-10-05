---
title: Procedura per l'esecuzione di query con SQL in Azure Cosmos DB | Microsoft Docs
description: Informazioni sull'esecuzione di query sui dati DocumentDB con SQL in Azure Cosmos DB
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
ms.openlocfilehash: a2a562c06c6302b9548e758b4c6754ec13b6001d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-how-to-query-using-sql"></a><span data-ttu-id="3d718-104">Azure Cosmos DB: procedura per l'esecuzione di query con SQL</span><span class="sxs-lookup"><span data-stu-id="3d718-104">Azure Cosmos DB: How to query using SQL?</span></span>

<span data-ttu-id="3d718-105">L'[API DocumentDB](documentdb-introduction.md) di Azure Cosmos DB supporta l'esecuzione di query sui documenti usando SQL.</span><span class="sxs-lookup"><span data-stu-id="3d718-105">The Azure Cosmos DB [DocumentDB API](documentdb-introduction.md) supports querying documents using SQL.</span></span> <span data-ttu-id="3d718-106">Questo articolo include un documento di esempio e due esempi di query SQL e relativi risultati.</span><span class="sxs-lookup"><span data-stu-id="3d718-106">This article provides a sample document and two sample SQL queries and results.</span></span>

<span data-ttu-id="3d718-107">Questo articolo illustra le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="3d718-107">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="3d718-108">Esecuzione di query sui dati con SQL</span><span class="sxs-lookup"><span data-stu-id="3d718-108">Querying data with SQL</span></span>

## <a name="sample-document"></a><span data-ttu-id="3d718-109">Documento di esempio</span><span class="sxs-lookup"><span data-stu-id="3d718-109">Sample document</span></span>

<span data-ttu-id="3d718-110">Le query SQL di questo articolo usano il documento di esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="3d718-110">The SQL queries in this article use the following sample document.</span></span>

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
## <a name="where-can-i-run-sql-queries"></a><span data-ttu-id="3d718-111">Dove è possibile eseguire query SQL?</span><span class="sxs-lookup"><span data-stu-id="3d718-111">Where can I run SQL queries?</span></span>

<span data-ttu-id="3d718-112">È possibile eseguire query usando Esplora dati nel Portale di Azure, tramite le [API REST e gli SDK](documentdb-sdk-dotnet.md) e anche usando [Query Playground](https://www.documentdb.com/sql/demo), che esegue query su un set di dati di esempio esistente.</span><span class="sxs-lookup"><span data-stu-id="3d718-112">You can run queries using the Data Explorer in the Azure portal, via the [REST API and SDKs](documentdb-sdk-dotnet.md), and even the [Query playground](https://www.documentdb.com/sql/demo), which runs queries on an existing set of sample data.</span></span>

<span data-ttu-id="3d718-113">Per altre informazioni sulle query SQL, vedere:</span><span class="sxs-lookup"><span data-stu-id="3d718-113">For more information about SQL queries, see:</span></span>
* [<span data-ttu-id="3d718-114">Query e sintassi SQL</span><span class="sxs-lookup"><span data-stu-id="3d718-114">SQL query and SQL syntax</span></span>](documentdb-sql-query.md)

## <a name="prerequisites"></a><span data-ttu-id="3d718-115">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="3d718-115">Prerequisites</span></span>

<span data-ttu-id="3d718-116">L'esercitazione presuppone la presenza di un account e di una raccolta di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3d718-116">This tutorial assumes you have an Azure Cosmos DB account and collection.</span></span> <span data-ttu-id="3d718-117">Questi requisiti non sono disponibili?</span><span class="sxs-lookup"><span data-stu-id="3d718-117">Don't have any of those?</span></span> <span data-ttu-id="3d718-118">Completare la [Guida introduttiva di 5 minuti](create-mongodb-nodejs.md) o l'[esercitazione per sviluppatori](tutorial-develop-mongodb.md) per creare un account e una raccolta.</span><span class="sxs-lookup"><span data-stu-id="3d718-118">Complete the [5-minute quickstart](create-mongodb-nodejs.md) or the [developer tutorial](tutorial-develop-mongodb.md) to create an account and collection.</span></span>

## <a name="example-query-1"></a><span data-ttu-id="3d718-119">Query di esempio 1</span><span class="sxs-lookup"><span data-stu-id="3d718-119">Example query 1</span></span>

<span data-ttu-id="3d718-120">Nel precedente documento della famiglia, la query SQL seguente restituisce i documenti in cui il campo ID corrisponde a `WakefieldFamily`.</span><span class="sxs-lookup"><span data-stu-id="3d718-120">Given the sample family document above, following SQL query returns the documents where the id field matches `WakefieldFamily`.</span></span> <span data-ttu-id="3d718-121">Poiché si tratta di un'istruzione `SELECT *`, l'output della query è il documento JSON completo:</span><span class="sxs-lookup"><span data-stu-id="3d718-121">Since it's a `SELECT *` statement, the output of the query is the complete JSON document:</span></span>

<span data-ttu-id="3d718-122">**Query**</span><span class="sxs-lookup"><span data-stu-id="3d718-122">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "WakefieldFamily"

<span data-ttu-id="3d718-123">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="3d718-123">**Results**</span></span>

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

## <a name="example-query-2"></a><span data-ttu-id="3d718-124">Query di esempio 2</span><span class="sxs-lookup"><span data-stu-id="3d718-124">Example query 2</span></span>

<span data-ttu-id="3d718-125">La query successiva restituisce tutti i nomi dei figli della famiglia il cui ID corrisponde a `WakefieldFamily`, ordinati in base al grado della classe frequentata.</span><span class="sxs-lookup"><span data-stu-id="3d718-125">The next query returns all the given names of children in the family whose id matches `WakefieldFamily` ordered by their grade.</span></span>

<span data-ttu-id="3d718-126">**Query**</span><span class="sxs-lookup"><span data-stu-id="3d718-126">**Query**</span></span>

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.children.grade ASC

<span data-ttu-id="3d718-127">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="3d718-127">**Results**</span></span>

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


## <a name="next-steps"></a><span data-ttu-id="3d718-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3d718-128">Next steps</span></span>

<span data-ttu-id="3d718-129">In questa esercitazione sono state eseguite le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="3d718-129">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3d718-130">È stato appreso come eseguire una query usando SQL</span><span class="sxs-lookup"><span data-stu-id="3d718-130">Learned how to query using SQL</span></span>  

<span data-ttu-id="3d718-131">È ora possibile passare all'esercitazione successiva per imparare a distribuire i dati a livello globale.</span><span class="sxs-lookup"><span data-stu-id="3d718-131">You can now proceed to the next tutorial to learn how to distribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3d718-132">Distribuire i dati a livello globale</span><span class="sxs-lookup"><span data-stu-id="3d718-132">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)

