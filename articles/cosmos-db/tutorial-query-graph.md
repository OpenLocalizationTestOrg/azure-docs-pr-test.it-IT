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
# <a name="azure-cosmos-db-how-tooquery-with-hello-graph-api-preview"></a>Azure Cosmos DB: Modalità tooquery con hello API Graph (anteprima)?

Hello Azure Cosmos DB [API Graph](graph-introduction.md) (anteprima) supporta [Gremlin](https://docs.mongodb.com/manual/tutorial/query-documents/) query. In questo articolo fornisce documenti di esempio e tooget che è stata avviata una query. Viene fornito un riferimento dettagliato di Gremlin in hello [supporto Gremlin](gremlin-support.md) articolo.

Questo articolo descrive hello seguenti attività: 

> [!div class="checklist"]
> * Esecuzione di query sui dati con Gremlin

## <a name="prerequisites"></a>Prerequisiti

Per toowork queste query, è necessario disporre di un account Azure Cosmos DB e disporre di dati del grafico nel contenitore hello. Questi requisiti non sono disponibili? Hello completo [avvio rapido di 5 minuti](create-graph-dotnet.md) o hello [esercitazione developer](tutorial-query-graph.md) toocreate un account e popolare il database. È possibile eseguire dopo le query che utilizzano hello hello [libreria graph di Azure Cosmos DB .NET](graph-sdk-dotnet.md), [console Gremlin](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console), o il driver Gremlin preferito.

## <a name="count-vertices-in-hello-graph"></a>Numero di vertici nel grafico hello

Hello frammento di codice seguente viene illustrato come toocount hello numero di vertici nel grafico hello:

```
g.V().count()
```

## <a name="filters"></a>Filtri

È possibile eseguire filtri utilizzando Gremlin `has` e `hasLabel` i passaggi e combinarli con `and`, `or`, e `not` toobuild più complessa di filtri. Per velocizzare le query, Azure DB Cosmos consente l'indicizzazione senza schema di tutte le proprietà all'interno di vertici e gradi.

```
g.V().hasLabel('person').has('age', gt(40))
```

## <a name="projection"></a>Proiezione

È possibile proiettare determinate proprietà nei risultati della query hello utilizzando hello `values` passaggio:

```
g.V().hasLabel('person').values('firstName')
```

## <a name="find-related-edges-and-vertices"></a>Trovare vertici e archi correlati

Finora sono stati esaminati solo gli operatori di query che è possibile usare in qualsiasi database. Grafici sono veloci ed efficienti per le operazioni di attraversamento quando è necessario toonavigate toorelated bordi e i vertici. Verranno ora individuati tutti gli amici di Thomas. Facciamo utilizzando del Gremlin `outE` passaggio toofind hello tutti i bordi in uscita da Thomas, quindi attraversamento toohello in vertici da tali usando del Gremlin `inV` passaggio:

```cs
g.V('thomas').outE('knows').inV().hasLabel('person')
```

la query successiva Hello esegue due hop toofind tutti "agli amici di Thomas di amici", chiamando `outE` e `inV` due volte. 

```cs
g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```

È possibile compilare query più complesse e implementare la logica di attraversamento potente grafico utilizzando Gremlin, tra cui filtro combinazione espressioni, esecuzione di ciclo tramite hello `loop` passaggio e la navigazione condizionale implementazione utilizzando hello `choose` passaggio. Altre informazioni sulle operazioni che è possibile eseguire con il [supporto per Gremlin](gremlin-support.md).

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione, effettuata seguente hello:

> [!div class="checklist"]
> * Appreso tooquery mediante Graph 

È ora possibile procedere come toolearn esercitazione successiva toohello toodistribute i dati a livello globale.

> [!div class="nextstepaction"]
> [Distribuire i dati a livello globale](tutorial-global-distribution-documentdb.md)