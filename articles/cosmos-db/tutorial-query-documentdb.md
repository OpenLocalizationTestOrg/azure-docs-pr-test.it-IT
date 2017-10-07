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
# <a name="azure-cosmos-db-how-tooquery-using-sql"></a>Azure Cosmos DB: Modalità tooquery utilizzando SQL?

Hello Azure Cosmos DB [API DocumentDB](documentdb-introduction.md) supporta l'esecuzione di query di documenti con SQL. Questo articolo include un documento di esempio e due esempi di query SQL e relativi risultati.

Questo articolo descrive hello seguenti attività: 

> [!div class="checklist"]
> * Esecuzione di query sui dati con SQL

## <a name="sample-document"></a>Documento di esempio

query SQL Hello in questo articolo utilizzare hello successivo documento di esempio.

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
## <a name="where-can-i-run-sql-queries"></a>Dove è possibile eseguire query SQL?

È possibile eseguire le query che utilizzano hello Esplora dati nel portale di Azure tramite hello hello [SDK e API REST](documentdb-sdk-dotnet.md)e anche hello [Query playground](https://www.documentdb.com/sql/demo), che consente di eseguire query su un set di dati di esempio esistente.

Per altre informazioni sulle query SQL, vedere:
* [Query e sintassi SQL](documentdb-sql-query.md)

## <a name="prerequisites"></a>Prerequisiti

L'esercitazione presuppone la presenza di un account e di una raccolta di Azure Cosmos DB. Questi requisiti non sono disponibili? Hello completo [avvio rapido di 5 minuti](create-mongodb-nodejs.md) o hello [esercitazione developer](tutorial-develop-mongodb.md) toocreate un account e una raccolta.

## <a name="example-query-1"></a>Query di esempio 1

Hello famiglia documento di esempio precedente, query SQL seguente restituisce documenti hello in cui corrisponde il campo di id hello `WakefieldFamily`. Poiché si tratta di un `SELECT *` istruzione, l'output di hello di query hello è documento JSON completo hello:

**Query**

    SELECT * 
    FROM Families f 
    WHERE f.id = "WakefieldFamily"

**Risultati**

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

## <a name="example-query-2"></a>Query di esempio 2

la query successiva Hello restituisce tutti i nomi di hello specificato di elementi figlio nella famiglia di hello il cui id corrisponde `WakefieldFamily` ordinati in base al loro grado.

**Query**

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.children.grade ASC

**Risultati**

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione, effettuata seguente hello:

> [!div class="checklist"]
> * Appreso tooquery tramite SQL  

È ora possibile procedere come toolearn esercitazione successiva toohello toodistribute i dati a livello globale.

> [!div class="nextstepaction"]
> [Distribuire i dati a livello globale](tutorial-global-distribution-documentdb.md)

