---
title: "Azure Cosmos DB: Modalità tooquery utilizzando hello API DocumentDB? | Microsoft Docs"
description: Informazioni su tooquery con hello API DocumentDB per Azure Cosmos DB
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
ms.openlocfilehash: e3e5a49f7510942bcfb15330e5f86c5dd8b1e5d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-with-api-for-mongodb"></a><span data-ttu-id="720a9-104">Azure Cosmos DB: Modalità tooquery con API per MongoDB?</span><span class="sxs-lookup"><span data-stu-id="720a9-104">Azure Cosmos DB: How tooquery with API for MongoDB?</span></span>

<span data-ttu-id="720a9-105">Hello Azure Cosmos DB [API per MongoDB](mongodb-introduction.md) supporta [query shell MongoDB](https://docs.mongodb.com/manual/tutorial/query-documents/).</span><span class="sxs-lookup"><span data-stu-id="720a9-105">hello Azure Cosmos DB [API for MongoDB](mongodb-introduction.md) supports [MongoDB shell queries](https://docs.mongodb.com/manual/tutorial/query-documents/).</span></span> 

<span data-ttu-id="720a9-106">Questo articolo descrive hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="720a9-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="720a9-107">Esecuzione di query sui dati con MongoDB</span><span class="sxs-lookup"><span data-stu-id="720a9-107">Querying data with MongoDB</span></span>

## <a name="sample-document"></a><span data-ttu-id="720a9-108">Documento di esempio</span><span class="sxs-lookup"><span data-stu-id="720a9-108">Sample document</span></span>

<span data-ttu-id="720a9-109">query di Hello in questo articolo utilizzano hello successivo documento di esempio.</span><span class="sxs-lookup"><span data-stu-id="720a9-109">hello queries in this article use hello following sample document.</span></span>

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
## <span data-ttu-id="720a9-110"><a id="examplequery1"></a>Query di esempio 1</span><span class="sxs-lookup"><span data-stu-id="720a9-110"><a id="examplequery1"></a> Example query 1</span></span> 

<span data-ttu-id="720a9-111">Dato hello famiglia documento di esempio precedente, restituisce i documenti hello in cui corrisponde il campo di id hello di query seguente hello `WakefieldFamily`.</span><span class="sxs-lookup"><span data-stu-id="720a9-111">Given hello sample family document above, hello following query returns hello documents where hello id field matches `WakefieldFamily`.</span></span>

<span data-ttu-id="720a9-112">**Query**</span><span class="sxs-lookup"><span data-stu-id="720a9-112">**Query**</span></span>
    
    db.families.find({ id: “WakefieldFamily”})

<span data-ttu-id="720a9-113">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="720a9-113">**Results**</span></span>

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

## <span data-ttu-id="720a9-114"><a id="examplequery2"></a>Query di esempio 2</span><span class="sxs-lookup"><span data-stu-id="720a9-114"><a id="examplequery2"></a>Example query 2</span></span> 

<span data-ttu-id="720a9-115">la query successiva Hello restituisce tutti gli elementi figlio hello nella famiglia di hello.</span><span class="sxs-lookup"><span data-stu-id="720a9-115">hello next query returns all hello children in hello family.</span></span> 

<span data-ttu-id="720a9-116">**Query**</span><span class="sxs-lookup"><span data-stu-id="720a9-116">**Query**</span></span>
    
    db.familes.find( { id: “WakefieldFamily” }, { children: true } )

<span data-ttu-id="720a9-117">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="720a9-117">**Results**</span></span>

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


## <span data-ttu-id="720a9-118"><a id="examplequery3"></a>Query di esempio 3</span><span class="sxs-lookup"><span data-stu-id="720a9-118"><a id="examplequery3"></a>Example query 3</span></span> 

<span data-ttu-id="720a9-119">la query successiva Hello restituisce tutte le famiglie di hello che sono registrate.</span><span class="sxs-lookup"><span data-stu-id="720a9-119">hello next query returns all hello families which are registered.</span></span> 

<span data-ttu-id="720a9-120">**Query**</span><span class="sxs-lookup"><span data-stu-id="720a9-120">**Query**</span></span>
    
    db.families.find( { "isRegistered" : true })
<span data-ttu-id="720a9-121">**Risultati** non verrà restituito alcun documento.</span><span class="sxs-lookup"><span data-stu-id="720a9-121">**Results** No document will be returned.</span></span> 

## <span data-ttu-id="720a9-122"><a id="examplequery4"></a>Query di esempio 4</span><span class="sxs-lookup"><span data-stu-id="720a9-122"><a id="examplequery4"></a>Example query 4</span></span>

<span data-ttu-id="720a9-123">la query successiva Hello restituisce tutte le famiglie di hello che non sono registrate.</span><span class="sxs-lookup"><span data-stu-id="720a9-123">hello next query returns all hello families which are not registered.</span></span> 

<span data-ttu-id="720a9-124">**Query**</span><span class="sxs-lookup"><span data-stu-id="720a9-124">**Query**</span></span>
    
    db.families.find( { "isRegistered" : false })
<span data-ttu-id="720a9-125">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="720a9-125">**Results**</span></span>

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
<span data-ttu-id="720a9-126">}</span><span class="sxs-lookup"><span data-stu-id="720a9-126">}</span></span>

## <span data-ttu-id="720a9-127"><a id="examplequery5"></a>Query di esempio 5</span><span class="sxs-lookup"><span data-stu-id="720a9-127"><a id="examplequery5"></a>Example query 5</span></span>

<span data-ttu-id="720a9-128">la query successiva Hello restituisce tutte le famiglie di hello che non sono registrate e lo stato è NY.</span><span class="sxs-lookup"><span data-stu-id="720a9-128">hello next query returns all hello families which are not registered and state is NY.</span></span> 

<span data-ttu-id="720a9-129">**Query**</span><span class="sxs-lookup"><span data-stu-id="720a9-129">**Query**</span></span>
    
     db.families.find( { "isRegistered" : false, "address.state" : "NY" })

<span data-ttu-id="720a9-130">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="720a9-130">**Results**</span></span>

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
<span data-ttu-id="720a9-131">}</span><span class="sxs-lookup"><span data-stu-id="720a9-131">}</span></span>


## <span data-ttu-id="720a9-132"><a id="examplequery6"></a>Query di esempio 6</span><span class="sxs-lookup"><span data-stu-id="720a9-132"><a id="examplequery6"></a>Example query 6</span></span>

<span data-ttu-id="720a9-133">la query successiva Hello restituisce tutte le famiglie di hello in cui i livelli di elementi figlio sono 8.</span><span class="sxs-lookup"><span data-stu-id="720a9-133">hello next query returns all hello families where children grades are 8.</span></span>

<span data-ttu-id="720a9-134">**Query**</span><span class="sxs-lookup"><span data-stu-id="720a9-134">**Query**</span></span>
  
     db.families.find( { children : { $elemMatch: { grade : 8 }} } )

<span data-ttu-id="720a9-135">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="720a9-135">**Results**</span></span>

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
<span data-ttu-id="720a9-136">}</span><span class="sxs-lookup"><span data-stu-id="720a9-136">}</span></span>

## <span data-ttu-id="720a9-137"><a id="examplequery7"></a>Query di esempio 7</span><span class="sxs-lookup"><span data-stu-id="720a9-137"><a id="examplequery7"></a>Example query 7</span></span>

<span data-ttu-id="720a9-138">la query successiva Hello restituisce tutte le famiglie di hello in cui le dimensioni della matrice di elementi figlio sono 3.</span><span class="sxs-lookup"><span data-stu-id="720a9-138">hello next query returns all hello families where size of children array is 3.</span></span>

<span data-ttu-id="720a9-139">**Query**</span><span class="sxs-lookup"><span data-stu-id="720a9-139">**Query**</span></span>
  
      db.Family.find( {children: { $size:3} } )

<span data-ttu-id="720a9-140">**Risultati**</span><span class="sxs-lookup"><span data-stu-id="720a9-140">**Results**</span></span>

<span data-ttu-id="720a9-141">Poiché in nessuna famiglia sono presenti più di 2 figli, non viene restituito alcun risultato.</span><span class="sxs-lookup"><span data-stu-id="720a9-141">No results will be returned as we do not have more than 2 children.</span></span> <span data-ttu-id="720a9-142">Solo quando il parametro è 2 questa query verrà completata e hello completo documento restituito.</span><span class="sxs-lookup"><span data-stu-id="720a9-142">Only when parameter is 2 this query will succeed and return hello full document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="720a9-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="720a9-143">Next steps</span></span>

<span data-ttu-id="720a9-144">In questa esercitazione, effettuata seguente hello:</span><span class="sxs-lookup"><span data-stu-id="720a9-144">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="720a9-145">Appreso tooquery utilizzando MongoDB</span><span class="sxs-lookup"><span data-stu-id="720a9-145">Learned how tooquery using MongoDB</span></span> 

<span data-ttu-id="720a9-146">È ora possibile procedere come toolearn esercitazione successiva toohello toodistribute i dati a livello globale.</span><span class="sxs-lookup"><span data-stu-id="720a9-146">You can now proceed toohello next tutorial toolearn how toodistribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="720a9-147">Distribuire i dati a livello globale</span><span class="sxs-lookup"><span data-stu-id="720a9-147">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)

