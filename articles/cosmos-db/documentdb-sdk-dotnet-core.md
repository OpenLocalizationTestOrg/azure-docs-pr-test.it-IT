---
title: aaaAzure Cosmos DB .NET Core API, risorse e SDK | Documenti Microsoft
description: Altre informazioni sui hello .NET Core API e SDK tra date di rilascio, date di ritiro e le modifiche apportate tra ogni versione di hello Azure Cosmos DB .NET Core SDK.
services: cosmos-db
documentationcenter: .net
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: f899b314-26ac-4ddb-86b2-bfdf05c2abf2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/11/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1269cafe0ea1caaa871404d507b12632dbb3ed82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-net-core-sdk-release-notes-and-resources"></a>Azure Cosmos DB .NET Core SDK: risorse e note sulla versione
> [!div class="op_single_selector"]
> * [.NET](documentdb-sdk-dotnet.md)
> * [Feed delle modifiche .NET](documentdb-sdk-dotnet-changefeed.md)
> * [.NET Core](documentdb-sdk-dotnet-core.md)
> * [Node.js](documentdb-sdk-node.md)
> * [Java](documentdb-sdk-java.md)
> * [Python](documentdb-sdk-python.md)
> * [REST](https://docs.microsoft.com/rest/api/documentdb/)
> * [Provider di risorse REST](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [SQL](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td>**Download dell'SDK**</td><td>[NuGet](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core/)</td></tr>

<tr><td>**Documentazione sull'API**</td><td>[Documentazione di riferimento API .NET](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)</td></tr>

<tr><td>**Esempi**</td><td>[Esempi di codice .NET](documentdb-dotnet-samples.md)</td></tr>

<tr><td>**Introduzione**</td><td>[Introduzione a hello Azure Cosmos DB .NET Core SDK](documentdb-dotnetcore-get-started.md)</td></tr>

<tr><td>**Esercitazione sull'app Web**</td><td>[Sviluppo di applicazioni Web con Azure Cosmos DB](documentdb-dotnet-application.md)</td></tr>

<tr><td>**Framework attualmente supportato**</td><td>[.NET standard 1.6 e .NET Standard 1.5](https://www.nuget.org/packages/NETStandard.Library)</td></tr>
</table></br>

## <a name="release-notes"></a>Note sulla versione

Hello Azure Cosmos DB .NET Core SDK dispone di parità di funzionalità con la versione più recente di hello di hello [SDK .NET di Azure Cosmos DB](documentdb-sdk-dotnet.md).

> [!NOTE] 
> non ancora Hello Azure Cosmos DB .NET Core SDK è compatibile con le app Universal Windows Platform (UWP). Se è interessati a hello .NET Core SDK che supporta le app UWP, inviare posta elettronica troppo[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0 

* Aggiunta del supporto per PartitionKeyRangeId come un FeedOption per definire l'ambito di valore di intervallo di chiavi di query risultati tooa partizione specifica. 
* Aggiunta del supporto per StartTime come un toostart ChangeFeedOption cercando modifiche hello dopo tale periodo di tempo. 

### <a name="a-name141141"></a><a name="1.4.1"/>1.4.1

*   Risolto un problema in hello classe JsonSerializable che potrebbe causare un'eccezione di overflow dello stack.

### <a name="a-name140140"></a><a name="1.4.0"/>1.4.0

*   Aggiunta del supporto per la definizione di JsonSerializerSettings personalizzate durante la creazione di un'istanza di [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet).

### <a name="a-name132132"></a><a name="1.3.2"/>1.3.2

*   Supporto .NET Standard 1.5 come uno dei framework di destinazione hello.

### <a name="a-name131131"></a><a name="1.3.1"/>1.3.1

*   Risoluzione di un problema riguardante i computer x64 che non supportano l'istruzione SSE4 e generano SEHException durante l'esecuzione di query di Azure Cosmos DB.

### <a name="a-name130130"></a><a name="1.3.0"/>1.3.0

*   Aggiunta del supporto per un nuovo livello di coerenza denominato ConsistentPrefix.
*   Aggiunta del supporto per le metriche delle query per le singole partizioni.
*   Aggiunta del supporto per la limitazione delle dimensioni di hello hello del token di continuazione per le query.
*   Aggiunta del supporto per una traccia più dettagliata delle richieste non riuscite.
*   Introdotti alcuni miglioramenti delle prestazioni hello SDK.

### <a name="a-name122122"></a><a name="1.2.2"/>1.2.2

* Risolto un problema che ignorati valore PartitionKey hello fornito FeedOptions per le query di aggregazione.
* Risolto un problema nella gestione trasparente delle partizioni durante l'esecuzione dell'ordinamento per query della partizione trasversale intermedia.

### <a name="a-name121121"></a><a name="1.2.1"/>1.2.1

* Risolto un problema che ha causato deadlock in alcune hello async API quando utilizzato all'interno di contesto ASP.NET.

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0

* Consente di correggere toomake SDK più failover tooautomatic resiliente a determinate condizioni.

### <a name="a-name112112"></a><a name="1.1.2"/>1.1.2

* Correzione di un problema che causa un'eccezione WebException: Impossibile risolto nome remoto hello.
* Hello aggiunto il supporto per lettura diretta di un documento tipizzato tramite l'aggiunta di nuove API tooReadDocumentAsync di overload.

### <a name="a-name111111"></a><a name="1.1.1"/>1.1.1

* Aggiunta del supporto LINQ per le query di aggregazione (COUNT, MIN, MAX, SUM e AVG).
* Correzione per un problema di perdita di memoria per oggetto ConnectionPolicy hello causato dall'uso di hello del gestore eventi.
* Correzione per un problema relativo al mancato funzionamento di UpsertAttachmentAsync in caso di uso di ETag.
* Correzione di un problema relativo al mancato funzionamento della continuazione della query di tipo order-by tra partizioni in caso di ordinamento in un campo di tipo stringa.

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0

* Aggiunta del supporto per le query di aggregazione (COUNT, MIN, MAX, SUM e AVG). Vedere [Supporto dell'aggregazione](documentdb-sql-query.md#Aggregates).
* Più basso di velocità effettiva minima per le raccolte partizionate da 10,100 UR/sec too2500 UR/sec.

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0

Hello Azure Cosmos DB .NET Core SDK consente toobuild veloci, multipiattaforma [ASP.NET Core](https://www.asp.net/core) e [.NET Core](https://www.microsoft.com/net/core#windows) toorun App in Windows, Mac e Linux. Hello ultima versione di hello Azure Cosmos DB .NET Core SDK è completamente [Xamarin](https://www.xamarin.com) compatibile e applicazioni usati toobuild destinate Mono (Linux), iOS e Android.  

### <a name="a-name010-preview010-preview"></a><a name="0.1.0-preview"/>0.1.0-preview

Hello Azure Cosmos DB .NET Core anteprima SDK consente toobuild veloci, multipiattaforma [ASP.NET Core](https://www.asp.net/core) e [.NET Core](https://www.microsoft.com/net/core#windows) toorun App in Windows, Mac e Linux.

Hello Azure Cosmos DB .NET Core anteprima SDK dispone di parità di funzionalità con la versione più recente di hello di hello [SDK .NET di Azure Cosmos DB](documentdb-sdk-dotnet.md) e supporta hello seguenti:
* Tutte le [modalità di connessione](performance-tips.md#networking): modalità gateway, TCP diretto e HTTP diretti. 
* Tutti i [livelli di coerenza](consistency-levels.md): assoluta, di sessione, con decadimento ristretto e finale.
* [Raccolte partizionate](partition-data.md). 
* [Account di database tra più aree e replica geografica](distribute-data-globally.md).

Nel caso di domande correlate toothis SDK, registrare troppo[StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb), o il file di un problema in hello [repository github](https://github.com/Azure/azure-documentdb-dotnet/issues). 

## <a name="release--retirement-dates"></a>Date di rilascio e di ritiro

| Version | Data di rilascio | Data di ritiro |
| --- | --- | --- |
| [1.5.0](#1.5.0) |10 agosto 2017 |--- | 
| [1.4.1](#1.4.1) |07 agosto 2017 |--- |
| [1.4.0](#1.4.0) |02 agosto 2017 |--- |
| [1.3.2](#1.3.2) |12 giugno 2017 |--- |
| [1.3.1](#1.3.1) |23 maggio 2017 |--- |
| [1.3.0](#1.3.0) |10 maggio 2017 |--- |
| [1.2.2](#1.2.2) |19 aprile 2017 |--- |
| [1.2.1](#1.2.1) |29 marzo 2017 |--- |
| [1.2.0](#1.2.0) |25 marzo 2017 |--- |
| [1.1.2](#1.1.2) |20 marzo 2017 |--- |
| [1.1.1](#1.1.1) |14 marzo 2017 |--- |
| [1.1.0](#1.1.0) |16 febbraio 2017 |--- |
| [1.0.0](#1.0.0) |21 dicembre 2016 |--- |
| [0.1.0-preview](#0.1.0-preview) |15 novembre 2016 |31 dicembre 2016 |

## <a name="see-also"></a>Vedere anche
toolearn ulteriori informazioni su Cosmos DB, vedere [DB di Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) pagina del servizio. 

