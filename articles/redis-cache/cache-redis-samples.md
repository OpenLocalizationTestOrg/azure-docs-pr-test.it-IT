---
title: esempi di Cache Redis aaaAzure | Documenti Microsoft
description: Informazioni su come toouse Redis di Azure memorizzano nella Cache
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 1f8d210c-ee09-4fe2-b63f-1e69246a27d8
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: multiple
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: 5cf9287b577758b5d880d1ca3928c1bee643a8ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-redis-cache-samples"></a>Esempi di Cache Redis di Azure
In questo argomento fornisce un elenco di esempi di Cache Redis di Azure, copertura di scenari, ad esempio la connessione della cache tooa, durante la lettura e scrittura tooand dati da una cache usando il provider di Cache Redis ASP.NET hello. Alcuni degli esempi di hello sono progetti scaricabili e alcune e fornite istruzioni dettagliate per includere i frammenti di codice ma non collegare progetto scaricabile tooa.

## <a name="hello-world-samples"></a>Esempi Hello World
esempi di Hello in questa sezione mostrano hello nozioni di base connessione tooan istanza di Cache Redis di Azure e la lettura e scrittura cache toohello dei dati tramite una vasta gamma di lingue e client Redis.

Hello [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) esempio viene illustrata la modalità tooperform diverse cache operazioni utilizzando hello [stackexchange. Redis](https://github.com/StackExchange/StackExchange.Redis) client .NET.

In questo esempio viene illustrato come:

* Utilizzare varie opzioni di connessione
* Leggere e scrivere oggetti tooand dalla cache di hello con operazioni sincrone e asincrone
* Usare Redis MGET/MSET comandi tooreturn valori di chiavi specificate
* Eseguire operazioni Redis transazionali
* Utilizzare gli elenchi e i set ordinati di Redis
* Archiviare oggetti .NET mediante i serializzatori JsonConvert
* Utilizza Redis imposta tooimplement tag
* Lavorare con Cluster Redis

Per ulteriori informazioni, vedere hello [stackexchange. Redis](https://github.com/StackExchange/StackExchange.Redis) documentazione su github e per scenari di utilizzo più vedere hello [StackExchange.Redis.Tests](https://github.com/StackExchange/StackExchange.Redis/tree/master/StackExchange.Redis.Tests) unit test.

[Come toouse Cache Redis di Azure con Python](cache-python-get-started.md) viene illustrata la modalità di avvio con Cache Redis di Azure usando Python e hello tooget [redis py](https://github.com/andymccurdy/redis-py) client.

[Utilizzo di oggetti .NET nella cache di hello](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache) illustrato è un modo tooserialize .NET oggetti è possibile scriverli tooand leggerli da un'istanza di Cache Redis di Azure. 

## <a name="use-redis-cache-as-a-scale-out-backplane-for-aspnet-signalr"></a>Usare Cache Redis come backplane con scalabilità orizzontale per ASP.NET SignalR
Hello [usare Cache Redis come scalabilità Backplane per ASP.NET SignalR](https://github.com/rustd/RedisSamples/tree/master/RedisAsSignalRBackplane) esempio viene illustrato come usare Cache Redis di Azure come backplane di SignalR. Per altre informazioni sul backplane, vedere l’argomento relativo alla [scalabilità orizzontale di SignalR con Redis](http://www.asp.net/signalr/overview/performance/scaleout-with-redis).

## <a name="redis-cache-customer-query-sample"></a>Esempio di query dei clienti su Cache Redis
Questo esempio mette a confronto le prestazioni di accesso ai dati da una cache e di accesso ai dati da un archivio di salvataggio permanente. L'esempio contiene due progetti.

* [Demo su come Cache Redis può migliorare le prestazioni grazie alla memorizzazione dei dati nella cache](https://github.com/rustd/RedisSamples/tree/master/RedisCacheCustomerQuerySample)
* [Valore di inizializzazione hello Database e la Cache per demo hello](https://github.com/rustd/RedisSamples/tree/master/SeedCacheForCustomerQuerySample)

## <a name="aspnet-session-state-and-output-caching"></a>Memorizzazione nella cache dell'output e dello stato sessione ASP.NET
Hello [toostore Cache Redis di Azure usare ASP.NET SessionState e OutputCache](https://github.com/rustd/RedisSamples/tree/master/SessionState_OutputCaching) esempio viene illustrato come si toouse Cache Redis di Azure toostore sessione ASP.NET e l'utilizzo di Cache di Output hello provider SessionState e OutputCache per Redis.

## <a name="manage-azure-redis-cache-with-maml"></a>Gestire Cache Redis di Azure con MAML
Hello [gestire Cache Redis di Azure mediante Azure Management Libraries](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) esempio viene illustrato come è possibile utilizzare Azure Management Libraries toomanage - (Crea / Aggiorna / Elimina) la Cache. 

## <a name="custom-monitoring-sample"></a>Esempio di monitoraggio personalizzato
Hello [dati di monitoraggio di Cache Redis accesso](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) esempio viene illustrato come accedere a dati di monitoraggio per la Cache Redis di Azure di fuori di hello portale di Azure.

## <a name="a-twitter-style-clone-written-using-php-and-redis"></a>Clone in stile Twitter scritto utilizzando PHP e Redis
Hello [Retwis](https://github.com/SyntaxC4-MSFT/retwis) è di esempio hello World Hello di Redis. È un clone di social network Twitter stile minimo scritto utilizzando Redis e PHP con hello [Predis](https://github.com/nrk/predis) client. codice sorgente Hello è progettato toobe molto semplice e in hello stessa fase tooshow diverse strutture di dati Redis.

## <a name="bandwidth-monitor"></a>Monitor della larghezza di banda
Hello [monitoraggio della larghezza di banda](https://github.com/JonCole/SampleCode/tree/master/BandWidthMonitor) esempio larghezza di banda è toomonitor hello usate hello client. toomeasure hello della larghezza di banda: esempio hello in computer client della cache di hello, effettuare chiamate toohello cache ed eseguire osservare la larghezza di banda hello riportato nell'esempio di monitoraggio della larghezza di banda hello.

