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
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-mongodb-api"></a>La distribuzione globale di Azure Cosmos DB toosetup utilizzando hello MongoDB API

In questo articolo viene illustrata come toouse hello toosetup portale Azure distribuzione globale di Azure Cosmos DB e quindi connettersi usando l'API di MongoDB hello.

Questo articolo descrive hello seguenti attività: 

> [!div class="checklist"]
> * Configurare la distribuzione globale mediante hello portale di Azure
> * Configurare la distribuzione globale mediante hello [API MongoDB](mongodb-introduction.md)

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]

## <a name="verifying-your-regional-setup-using-hello-mongodb-api"></a>Verifica della configurazione internazionale utilizzando hello MongoDB API
più semplice di controllo della configurazione globale all'interno di API per MongoDB è hello toorun double Hello *isMaster()* comando Shell di Mongo hello.

Da Mongo Shell:

   ```
      db.isMaster()
   ```
   
Risultati dell'esempio:

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

## <a name="connecting-tooa-preferred-region-using-hello-mongodb-api"></a>Connessione area geografica preferita tooa utilizzando hello MongoDB API

Hello MongoDB API consente si toospecify delle preferenze di lettura della raccolta per un database distribuito a livello globale. Per entrambi bassa latenza letture e disponibilità elevata, si consiglia di impostare preferenze di lettura della raccolta troppo*più vicino*. Una lettura preferenza *più vicino* è tooread configurato dall'area più vicina hello.

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Nearest));
```

Per le applicazioni con una replica primaria di lettura/scrittura area e un'area secondaria per il ripristino di emergenza (ripristino di emergenza) scenari si consiglia di impostare preferenze di lettura della raccolta troppo*secondario preferito*. Una lettura preferenza *secondario preferito* è tooread configurato dall'area secondaria hello quando l'area primaria hello è disponibile.

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.SecondaryPreferred));
```

Infine, se ad esempio toomanually specificare le aree di lettura. È possibile impostare l'area hello Tag all'interno delle preferenze di lettura.

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
var tag = new Tag("region", "Southeast Asia");
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Secondary, new[] { new TagSet(new[] { tag }) }));
```

L'esercitazione è terminata. È possibile ottenere informazioni come toomanage hello la coerenza dell'account di replicato globalmente leggendo [livelli di coerenza nel database di Azure Cosmos](consistency-levels.md). Per informazioni sul funzionamento della replica di database globale in Azure Cosmos DB, vedere [Distribuire i dati a livello globale con Azure Cosmos DB](distribute-data-globally.md).

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione, effettuata seguente hello:

> [!div class="checklist"]
> * Configurare la distribuzione globale mediante hello portale di Azure
> * Configurare la distribuzione globale mediante hello APIs DocumentDB

È ora possibile procedere toolearn esercitazione successiva toohello come toodevelop localmente tramite hello emulatore locale di Azure Cosmos DB.

> [!div class="nextstepaction"]
> [Sviluppare in locale con emulator hello](local-emulator.md)
