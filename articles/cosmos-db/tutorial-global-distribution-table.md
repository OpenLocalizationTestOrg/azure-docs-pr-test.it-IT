---
title: esercitazione di distribuzione globale aaaAzure DB Cosmos per tabella API | Documenti Microsoft
description: Informazioni su come distribuzione globale di Azure Cosmos DB toosetup utilizzando hello API di tabella.
services: cosmos-db
keywords: Distribuzione globale, Table
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
ms.openlocfilehash: d2a995e09c37f9449856aef2ab707e95eb8a540c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-table-api"></a>La distribuzione globale di Azure Cosmos DB toosetup utilizzando hello tabella API

In questo articolo viene illustrata come toouse hello distribuzione globale di Azure Cosmos DB toosetup portale Azure e quindi connettersi utilizzando hello tabella API (anteprima).

Questo articolo descrive hello seguenti attività: 

> [!div class="checklist"]
> * Configurare la distribuzione globale mediante hello portale di Azure
> * Configurare la distribuzione globale mediante hello [tabella API](table-introduction.md)

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-table-api"></a>Connessione area geografica preferita tooa utilizzando hello tabella API

In ordine tootake sfruttare la [distribuzione globale](distribute-data-globally.md), applicazioni client possono specificare hello ordinato l'elenco delle preferenze di aree toobe utilizzato tooperform documento operazioni. Questa operazione può essere eseguita dall'impostazione hello `TablePreferredLocations` il valore di configurazione nel file di configurazione app hello per l'anteprima di hello Azure Storage SDK. Basato sulla configurazione dell'account Azure Cosmos DB hello, disponibilità internazionali corrente ed elenco preferenza hello specificato, verrà scelta la maggior parte degli endpoint ottimale da hello Azure Storage SDK tooperform hello scrivere e operazioni di lettura.

Hello `TablePreferredLocations` deve contenere un elenco delimitato da virgole di indirizzi (multihosting) preferiti per le letture. Ogni istanza del client è possibile specificare un subset di queste aree nell'ordine preferito hello per le letture di bassa latenza. aree Hello devono essere denominate con i relativi [i nomi visualizzati](https://msdn.microsoft.com/library/azure/gg441293.aspx), ad esempio, `West US`.

Tutte le letture che verranno inviate toohello prima area disponibile in hello `TablePreferredLocations` elenco. Se hello richiesta non riesce, il client hello esito negativo all'area di hello elenco toohello successiva e così via.

Hello SDK tenterà solo tooread dalle aree hello specificato in `TablePreferredLocations`. In tal caso, ad esempio, se hello Account del Database è disponibile in tre aree, ma il client di hello specifica solo due delle hello non scrittura aree per `TablePreferredLocations`, quindi non verranno utilizzate alcun letture fuori area scrittura hello, anche nel caso di hello di failover.

Hello SDK invierà automaticamente area scrittura di tutte le operazioni di scrittura toohello corrente.

Se hello `TablePreferredLocations` non è impostata, verranno utilizzate dall'area di scrittura corrente hello tutte le richieste.

```xml
    <appSettings>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>           
    </appSettings>
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
