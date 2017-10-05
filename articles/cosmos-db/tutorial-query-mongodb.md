---
title: 'Azure Cosmos DB: procedura per l''esecuzione di query con l''API DocumentDB | Microsoft Docs'
description: Informazioni su come eseguire query con l'API DocumentDB per Azure Cosmos DB
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: feffc553a9aa931d96cec71c101674fce08a466b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-how-to-query-with-api-for-mongodb"></a><span data-ttu-id="f4b16-104">Azure Cosmos DB: procedura per l'esecuzione di query con l'API MongoDB</span><span class="sxs-lookup"><span data-stu-id="f4b16-104">Azure Cosmos DB: How to query with API for MongoDB?</span></span>

<span data-ttu-id="f4b16-105">L'[API per MongoDB](mongodb-introduction.md) supporta l'esecuzione di [query nella shell di MongoDB](https://docs.mongodb.com/manual/tutorial/query-documents/).</span><span class="sxs-lookup"><span data-stu-id="f4b16-105">The Azure Cosmos DB [API for MongoDB](mongodb-introduction.md) supports [MongoDB shell queries](https://docs.mongodb.com/manual/tutorial/query-documents/).</span></span> 

<span data-ttu-id="f4b16-106">Questo articolo illustra le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="f4b16-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="f4b16-107">Esecuzione di query sui dati con MongoDB</span><span class="sxs-lookup"><span data-stu-id="f4b16-107">Querying data with MongoDB</span></span>

## <a name="sample-document"></a><span data-ttu-id="f4b16-108">Documento di esempio</span><span class="sxs-lookup"><span data-stu-id="f4b16-108">Sample document</span></span>

<span data-ttu-id="f4b16-109">Le query di questo articolo usano il documento di esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="f4b16-109">The queries in this article use the following sample document.</span></span>

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
## <span data-ttu-id="f4b16-110"><a id="examplequery1"></a>Query di esempio 1</span><span class="sxs-lookup"><span data-stu-id="f4b16-110"><a id="examplequery1"></a> Example query 1</span></span> 

<span data-ttu-id="f4b16-111">Nel precedente documento della famiglia, la query seguente restituisce i documenti in cui il campo ID corrisponde a `WakefieldFamily`.</span><span class="sxs-lookup"><span data-stu-id="f4b16-111">Given the sample family document above, the following query returns the documents where the id field matches `WakefieldFamily`.</span></span>

<span data-ttu-id="f4b16-112">**Query**</span><span class="sxs-lookup"><span data-stu-id="f4b16-112">**Query**</span></span>
    
    db.families.find({ id: “WakefieldFamily”})

<span data-ttu-id="f4b16-113">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="f4b16-113">**Results**</span></span>

    {
    "_id": "ObjectId(\"58f65e1198f3a12c7090e68c\")",
    "id": "WakefieldFamily",
    "parents": [
      {
        "familyName": "Wakefield",
        "givenName": "Robin"
      },
      {
        "familyName": "Miller",
        "givenName": "Ben"
      }
    ],
    "children": [
      {
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [
          { "givenName": "Goofy" },
          { "givenName": "Shadow" }
        ]
      },
      {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
      }
    ],
    "address": {
      "state": "NY",
      "county": "Manhattan",
      "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
    }

## <span data-ttu-id="f4b16-114"><a id="examplequery2"></a>Query di esempio 2</span><span class="sxs-lookup"><span data-stu-id="f4b16-114"><a id="examplequery2"></a>Example query 2</span></span> 

<span data-ttu-id="f4b16-115">La query seguente restituisce tutti i figli della famiglia.</span><span class="sxs-lookup"><span data-stu-id="f4b16-115">The next query returns all the children in the family.</span></span> 

<span data-ttu-id="f4b16-116">**Query**</span><span class="sxs-lookup"><span data-stu-id="f4b16-116">**Query**</span></span>
    
    db.familes.find( { id: “WakefieldFamily” }, { children: true } )

<span data-ttu-id="f4b16-117">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="f4b16-117">**Results**</span></span>

    {
    "_id": "ObjectId("58f65e1198f3a12c7090e68c")",
    "children": [
      {
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [
          { "givenName": "Goofy" },
          { "givenName": "Shadow" }
        ]
      },
      {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
      }
    ]
    }


## <span data-ttu-id="f4b16-118"><a id="examplequery3"></a>Query di esempio 3</span><span class="sxs-lookup"><span data-stu-id="f4b16-118"><a id="examplequery3"></a>Example query 3</span></span> 

<span data-ttu-id="f4b16-119">La query seguente restituisce tutte le famiglie registrate.</span><span class="sxs-lookup"><span data-stu-id="f4b16-119">The next query returns all the families which are registered.</span></span> 

<span data-ttu-id="f4b16-120">**Query**</span><span class="sxs-lookup"><span data-stu-id="f4b16-120">**Query**</span></span>
    
    db.families.find( { "isRegistered" : true })
<span data-ttu-id="f4b16-121">**Risultati** non verrà restituito alcun documento.</span><span class="sxs-lookup"><span data-stu-id="f4b16-121">**Results** No document will be returned.</span></span> 

## <span data-ttu-id="f4b16-122"><a id="examplequery4"></a>Query di esempio 4</span><span class="sxs-lookup"><span data-stu-id="f4b16-122"><a id="examplequery4"></a>Example query 4</span></span>

<span data-ttu-id="f4b16-123">La query seguente restituisce tutte le famiglie non registrate.</span><span class="sxs-lookup"><span data-stu-id="f4b16-123">The next query returns all the families which are not registered.</span></span> 

<span data-ttu-id="f4b16-124">**Query**</span><span class="sxs-lookup"><span data-stu-id="f4b16-124">**Query**</span></span>
    
    db.families.find( { "isRegistered" : false })
<span data-ttu-id="f4b16-125">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="f4b16-125">**Results**</span></span>

     {
    "_id": ObjectId("58f65e1198f3a12c7090e68c"),
    "id": "WakefieldFamily",
    "parents": [{
        "familyName": "Wakefield",
        "givenName": "Robin"
    }, {
        "familyName": "Miller",
        "givenName": "Ben"
    }],
    "children": [{
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [{
            "givenName": "Goofy"
        }, {
            "givenName": "Shadow"
        }]
    }, {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
    }],
    "address": {
        "state": "NY",
        "county": "Manhattan",
        "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
<span data-ttu-id="f4b16-126">}</span><span class="sxs-lookup"><span data-stu-id="f4b16-126">}</span></span>

## <span data-ttu-id="f4b16-127"><a id="examplequery5"></a>Query di esempio 5</span><span class="sxs-lookup"><span data-stu-id="f4b16-127"><a id="examplequery5"></a>Example query 5</span></span>

<span data-ttu-id="f4b16-128">La query seguente restituisce tutte le famiglie non registrate e il cui stato di residenza è NY.</span><span class="sxs-lookup"><span data-stu-id="f4b16-128">The next query returns all the families which are not registered and state is NY.</span></span> 

<span data-ttu-id="f4b16-129">**Query**</span><span class="sxs-lookup"><span data-stu-id="f4b16-129">**Query**</span></span>
    
     db.families.find( { "isRegistered" : false, "address.state" : "NY" })

<span data-ttu-id="f4b16-130">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="f4b16-130">**Results**</span></span>

     {
    "_id": ObjectId("58f65e1198f3a12c7090e68c"),
    "id": "WakefieldFamily",
    "parents": [{
        "familyName": "Wakefield",
        "givenName": "Robin"
    }, {
        "familyName": "Miller",
        "givenName": "Ben"
    }],
    "children": [{
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [{
            "givenName": "Goofy"
        }, {
            "givenName": "Shadow"
        }]
    }, {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
    }],
    "address": {
        "state": "NY",
        "county": "Manhattan",
        "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
<span data-ttu-id="f4b16-131">}</span><span class="sxs-lookup"><span data-stu-id="f4b16-131">}</span></span>


## <span data-ttu-id="f4b16-132"><a id="examplequery6"></a>Query di esempio 6</span><span class="sxs-lookup"><span data-stu-id="f4b16-132"><a id="examplequery6"></a>Example query 6</span></span>

<span data-ttu-id="f4b16-133">La query seguente restituisce tutte le famiglie in cui il grado della classe frequentata dai figli corrisponde a 8.</span><span class="sxs-lookup"><span data-stu-id="f4b16-133">The next query returns all the families where children grades are 8.</span></span>

<span data-ttu-id="f4b16-134">**Query**</span><span class="sxs-lookup"><span data-stu-id="f4b16-134">**Query**</span></span>
  
     db.families.find( { children : { $elemMatch: { grade : 8 }} } )

<span data-ttu-id="f4b16-135">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="f4b16-135">**Results**</span></span>

     {
    "_id": ObjectId("58f65e1198f3a12c7090e68c"),
    "id": "WakefieldFamily",
    "parents": [{
        "familyName": "Wakefield",
        "givenName": "Robin"
    }, {
        "familyName": "Miller",
        "givenName": "Ben"
    }],
    "children": [{
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [{
            "givenName": "Goofy"
        }, {
            "givenName": "Shadow"
        }]
    }, {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
    }],
    "address": {
        "state": "NY",
        "county": "Manhattan",
        "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
<span data-ttu-id="f4b16-136">}</span><span class="sxs-lookup"><span data-stu-id="f4b16-136">}</span></span>

## <span data-ttu-id="f4b16-137"><a id="examplequery7"></a>Query di esempio 7</span><span class="sxs-lookup"><span data-stu-id="f4b16-137"><a id="examplequery7"></a>Example query 7</span></span>

<span data-ttu-id="f4b16-138">La query seguente restituisce tutte le famiglie in cui la dimensione della matrice dei figli corrisponde a 3.</span><span class="sxs-lookup"><span data-stu-id="f4b16-138">The next query returns all the families where size of children array is 3.</span></span>

<span data-ttu-id="f4b16-139">**Query**</span><span class="sxs-lookup"><span data-stu-id="f4b16-139">**Query**</span></span>
  
      db.Family.find( {children: { $size:3} } )

<span data-ttu-id="f4b16-140">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="f4b16-140">**Results**</span></span>

<span data-ttu-id="f4b16-141">Poiché in nessuna famiglia sono presenti più di 2 figli, non viene restituito alcun risultato.</span><span class="sxs-lookup"><span data-stu-id="f4b16-141">No results will be returned as we do not have more than 2 children.</span></span> <span data-ttu-id="f4b16-142">La query avrà esito positivo e restituirà l'intero documento solo quando il parametro è 2.</span><span class="sxs-lookup"><span data-stu-id="f4b16-142">Only when parameter is 2 this query will succeed and return the full document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4b16-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f4b16-143">Next steps</span></span>

<span data-ttu-id="f4b16-144">In questa esercitazione sono state eseguite le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="f4b16-144">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f4b16-145">È stato appreso come eseguire una query usando MongoDB</span><span class="sxs-lookup"><span data-stu-id="f4b16-145">Learned how to query using MongoDB</span></span> 

<span data-ttu-id="f4b16-146">È ora possibile passare all'esercitazione successiva per imparare a distribuire i dati a livello globale.</span><span class="sxs-lookup"><span data-stu-id="f4b16-146">You can now proceed to the next tutorial to learn how to distribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f4b16-147">Distribuire i dati a livello globale</span><span class="sxs-lookup"><span data-stu-id="f4b16-147">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)

