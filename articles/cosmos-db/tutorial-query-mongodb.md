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
# <a name="azure-cosmos-db-how-tooquery-with-api-for-mongodb"></a>Azure Cosmos DB: Modalità tooquery con API per MongoDB?

Hello Azure Cosmos DB [API per MongoDB](mongodb-introduction.md) supporta [query shell MongoDB](https://docs.mongodb.com/manual/tutorial/query-documents/). 

Questo articolo descrive hello seguenti attività: 

> [!div class="checklist"]
> * Esecuzione di query sui dati con MongoDB

## <a name="sample-document"></a>Documento di esempio

query di Hello in questo articolo utilizzano hello successivo documento di esempio.

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
## <a id="examplequery1"></a>Query di esempio 1 

Dato hello famiglia documento di esempio precedente, restituisce i documenti hello in cui corrisponde il campo di id hello di query seguente hello `WakefieldFamily`.

**Query**
    
    db.families.find({ id: “WakefieldFamily”})

**Risultati**

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

## <a id="examplequery2"></a>Query di esempio 2 

la query successiva Hello restituisce tutti gli elementi figlio hello nella famiglia di hello. 

**Query**
    
    db.familes.find( { id: “WakefieldFamily” }, { children: true } )

**Risultati**

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


## <a id="examplequery3"></a>Query di esempio 3 

la query successiva Hello restituisce tutte le famiglie di hello che sono registrate. 

**Query**
    
    db.families.find( { "isRegistered" : true })
**Risultati** non verrà restituito alcun documento. 

## <a id="examplequery4"></a>Query di esempio 4

la query successiva Hello restituisce tutte le famiglie di hello che non sono registrate. 

**Query**
    
    db.families.find( { "isRegistered" : false })
**Risultati**

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
}

## <a id="examplequery5"></a>Query di esempio 5

la query successiva Hello restituisce tutte le famiglie di hello che non sono registrate e lo stato è NY. 

**Query**
    
     db.families.find( { "isRegistered" : false, "address.state" : "NY" })

**Risultati**

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
}


## <a id="examplequery6"></a>Query di esempio 6

la query successiva Hello restituisce tutte le famiglie di hello in cui i livelli di elementi figlio sono 8.

**Query**
  
     db.families.find( { children : { $elemMatch: { grade : 8 }} } )

**Risultati**

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
}

## <a id="examplequery7"></a>Query di esempio 7

la query successiva Hello restituisce tutte le famiglie di hello in cui le dimensioni della matrice di elementi figlio sono 3.

**Query**
  
      db.Family.find( {children: { $size:3} } )

**Risultati**

Poiché in nessuna famiglia sono presenti più di 2 figli, non viene restituito alcun risultato. Solo quando il parametro è 2 questa query verrà completata e hello completo documento restituito.

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione, effettuata seguente hello:

> [!div class="checklist"]
> * Appreso tooquery utilizzando MongoDB 

È ora possibile procedere come toolearn esercitazione successiva toohello toodistribute i dati a livello globale.

> [!div class="nextstepaction"]
> [Distribuire i dati a livello globale](tutorial-global-distribution-documentdb.md)

