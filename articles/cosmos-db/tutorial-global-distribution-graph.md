---
title: esercitazione di distribuzione globale Cosmos DB aaaAzure per l'API Graph | Documenti Microsoft
description: Informazioni su come distribuzione globale di Azure Cosmos DB toosetup utilizzando hello API Graph.
services: cosmos-db
keywords: distribuzione globale, graph, gremlin
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: denlee
ms.openlocfilehash: 1629a31e12a18079f63e07c4909862b36b5f4c0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-graph-api"></a>La distribuzione globale di Azure Cosmos DB toosetup utilizzando hello API Graph

In questo articolo viene illustrata come toouse hello distribuzione globale di Azure Cosmos DB toosetup portale Azure e quindi connettersi utilizzando hello API Graph (anteprima).

Questo articolo descrive hello seguenti attività: 

> [!div class="checklist"]
> * Configurare la distribuzione globale mediante hello portale di Azure
> * Configurare la distribuzione globale mediante hello [sulle API Graph](graph-introduction.md) (anteprima)

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-graph-api-using-hello-net-sdk"></a>La connessione usando l'API Graph hello mediante .NET SDK hello la regione preferita tooa

API Graph Hello viene esposto come una libreria di estensione su hello DocumentDB SDK.

In ordine tootake sfruttare la [distribuzione globale](distribute-data-globally.md), applicazioni client possono specificare hello ordinato l'elenco delle preferenze di aree toobe utilizzato tooperform documento operazioni. Questa operazione può essere eseguita mediante l'impostazione di criteri di connessione hello. Basato sulla configurazione dell'account Azure Cosmos DB hello, elenco delle preferenze hello e la disponibilità di internazionale corrente specificato, hello la maggior parte degli endpoint ottimale verrà scelto dal scrittura tooperform SDK di hello e operazioni di lettura.

L'elenco delle preferenze viene specificato durante l'inizializzazione di una connessione tramite hello SDK. Hello SDK di accettare un parametro facoltativo "PreferredLocations" che rappresenta un elenco ordinato di aree di Azure.

* **Scrive**: hello SDK invierà automaticamente tutti scrive toohello area di scrittura corrente.
* **Legge**: tutte le letture verranno inviate toohello prima area disponibile nell'elenco PreferredLocations hello. Se hello richiesta non riesce, il client hello esito negativo all'area di hello elenco toohello successiva e così via. Hello SDK tenterà solo tooread dalle aree hello specificato in PreferredLocations. In tal caso, ad esempio, se hello Cosmos DB account è disponibile in tre aree, ma client hello specifica solo due delle aree non scrittura hello per PreferredLocations, quindi non letture verranno utilizzate fuori area scrittura hello, anche nel caso di hello di failover.

un'applicazione Hello possibile verificare l'endpoint di scrittura corrente hello e leggere endpoint scelto da hello SDK dal controllo due proprietà, WriteEndpoint e ReadEndpoint, disponibili nella versione SDK 1.8 e versioni successive. Se non è impostata la proprietà PreferredLocations hello, verranno utilizzate dall'area di scrittura corrente hello tutte le richieste.

### <a name="using-hello-sdk"></a>Utilizzo di hello SDK

Ad esempio, hello .NET SDK, hello `ConnectionPolicy` parametro per hello `DocumentClient` costruttore ha una proprietà denominata `PreferredLocations`. Questa proprietà può essere impostata tooa elenco di nomi di area. nomi visualizzati Hello per [aree di Azure] [ regions] può essere specificato come parte di `PreferredLocations`.

> [!NOTE]
> Hello URL per gli endpoint di hello non deve essere considerato come costanti di lunga durate. servizio Hello può aggiornare questi in qualsiasi momento. Hello SDK gestisce automaticamente questa modifica.
>
>

```cs
// Getting endpoints from application settings or other configuration location
Uri accountEndPoint = new Uri(Properties.Settings.Default.GlobalDatabaseUri);
string accountKey = Properties.Settings.Default.GlobalDatabaseKey;

ConnectionPolicy connectionPolicy = new ConnectionPolicy();

//Setting read region selection preference
connectionPolicy.PreferredLocations.Add(LocationNames.WestUS); // first preference
connectionPolicy.PreferredLocations.Add(LocationNames.EastUS); // second preference
connectionPolicy.PreferredLocations.Add(LocationNames.NorthEurope); // third preference

// initialize connection
DocumentClient docClient = new DocumentClient(
    accountEndPoint,
    accountKey,
    connectionPolicy);

// connect tooAzure Cosmos DB
await docClient.OpenAsync().ConfigureAwait(false);
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

[regions]: https://azure.microsoft.com/regions/

