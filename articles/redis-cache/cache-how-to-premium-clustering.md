---
title: aaaHow tooconfigure Redis clustering per una Cache Redis di Azure Premium | Documenti Microsoft
description: Informazioni su come toocreate e gestire il servizio cluster per il livello Premium, le istanze di Cache Redis di Azure Redis
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 62208eec-52ae-4713-b077-62659fd844ab
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: sdanie
ms.openlocfilehash: 44d520facb9d1af145b69f1b58f082aabb655d4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-redis-clustering-for-a-premium-azure-redis-cache"></a>Come tooconfigure Redis clustering per una Cache Redis di Azure Premium
Cache Redis di Azure ha diverse offerte di cache, che forniscono flessibilità nella scelta di hello della dimensione della cache e le funzionalità, incluse le funzionalità di livello Premium, ad esempio clustering, persistenza e il supporto di rete virtuale. In questo articolo viene descritto come tooconfigure clustering in premium Azure Redis Cache istanza.

Per informazioni su altre funzionalità di cache premium, vedere [livello Premium di Cache Redis di Azure di introduzione toohello](cache-premium-tier-intro.md).

## <a name="what-is-redis-cluster"></a>Che cos'è un cluster Redis?
Cache Redis di Azure offre funzionalità di clustering Redis come nell' [implementazione in Redis](http://redis.io/topics/cluster-tutorial). Con Redis Cluster, si otterrà hello seguenti vantaggi: 

* Hello possibilità tooautomatically dividere il set di dati tra più nodi. 
* Hello possibilità toocontinue operazioni quando un sottoinsieme di nodi hello si sono verificati errori o sono Impossibile toocommunicate con rest hello del cluster di hello. 
* Maggiore velocità effettiva: velocità effettiva aumenta in modo lineare man mano che aumenta il numero di hello di partizioni. 
* Altre dimensioni della memoria: aumenta in modo lineare man mano che aumenta il numero di hello di partizioni.  

Per altre informazioni su dimensioni, velocità effettiva e larghezza di banda delle cache premium, vedere [Quali offerte e dimensioni della Cache Redis è consigliabile usare?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)

In Azure, Redis cluster viene offerto come un modello principale/replica in ogni partizione ha una coppia di principale/replica con replica in replica hello viene gestita dal servizio Cache Redis di Azure. 

## <a name="clustering"></a>Clustering
Il servizio cluster è stato attivato hello **nuova Cache Redis** pannello durante la creazione della cache. 

[!INCLUDE [redis-cache-create](../../includes/redis-cache-premium-create.md)]

Il servizio cluster è configurato su hello **Cluster Redis** blade.

![Clustering][redis-cache-clustering]

Possono esistere fino a partizioni too10 cluster hello. Fare clic su **abilitato** e far scorrere il dispositivo di scorrimento hello o digitare un numero compreso tra 1 e 10 per **numero di partizioni** e fare clic su **OK**.

Ogni partizione è una coppia di cache principale/replica gestita da Azure e dimensioni totali di hello della cache di hello viene calcolata moltiplicando il numero di hello di partizioni per dimensioni della cache di hello selezionata nel piano tariffario hello. 

![Clustering][redis-cache-clustering-selected]

Dopo la creazione della cache di hello ci si connette tooit e usare semplicemente come una cache non cluster e Redis distribuisce i dati di hello in partizioni di Cache di hello. Se è diagnostica [abilitato](cache-how-to-monitor.md#enable-cache-diagnostics), le metriche acquisite separatamente per ogni partizione e può essere [visualizzati](cache-how-to-monitor.md) nel pannello Cache Redis hello. 

> [!NOTE]
> 
> Sono richieste alcune lievi modifiche all'applicazione client quando le funzionalità di clustering vengono configurate. Per ulteriori informazioni, vedere [devo toomake qualsiasi toouse applicazione di modifiche toomy client clustering?](#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)
> 
> 

Per il codice di esempio sull'utilizzo di clustering con client stackexchange. Redis hello, vedere hello [clustering.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/Clustering.cs) parte hello [Hello World](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) esempio.

<a name="cluster-size"></a>

## <a name="change-hello-cluster-size-on-a-running-premium-cache"></a>Modificare dimensioni hello cluster in esecuzione cache premium
dimensione del cluster toochange hello in un premium in esecuzione la cache con clustering fare clic su abilitato, **dimensione del Cluster Redis** da hello **menu risorse**.

> [!NOTE]
> Mentre hello Azure Redis Cache Premium livello è stato rilasciato tooGeneral disponibilità, funzionalità di dimensioni del Cluster Redis hello è attualmente in anteprima.
> 
> 

![Dimensione del cluster Redis][redis-cache-redis-cluster-size]

dimensione del cluster toochange hello, utilizzare il dispositivo di scorrimento hello o digitare un numero compreso tra 1 e 10 hello **numero di partizioni** casella di testo e fare clic su **OK** toosave.

> [!NOTE]
> Ridimensionamento di un cluster esegue hello [migrazione](https://redis.io/commands/migrate) comando, che è un comando dispendiosa, pertanto, per un impatto minimo, si consiglia di eseguire questa operazione durante le ore non di punta. Durante il processo di migrazione hello, si noterà un picco di carico del server. Ridimensionamento di un cluster è un valore long processo in esecuzione e hello quantità di tempo dipende dalla hello numero di chiavi e le dimensioni dei valori di hello associati a tali chiavi.
> 
> 

## <a name="clustering-faq"></a>Domande frequenti sul clustering
Hello elenco seguente contiene le risposte toocommonly domande frequenti su cluster di Cache Redis di Azure.

* [È necessario toomake qualsiasi toouse applicazione di modifiche toomy client clustering?](#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)
* [Come vengono distribuite le chiavi in un cluster?](#how-are-keys-distributed-in-a-cluster)
* [Che cos'è una dimensione della cache più grande hello che posso creare?](#what-is-the-largest-cache-size-i-can-create)
* [Tutti i client Redis supportano il clustering?](#do-all-redis-clients-support-clustering)
* [Come connettersi toomy cache quando il servizio cluster è abilitato?](#how-do-i-connect-to-my-cache-when-clustering-is-enabled)
* [È possibile connettersi direttamente toohello singole partizioni di my cache?](#can-i-directly-connect-to-the-individual-shards-of-my-cache)
* [È possibile configurare il clustering per una cache creata in precedenza?](#can-i-configure-clustering-for-a-previously-created-cache)
* [È possibile configurare il clustering per una cache Basic o Standard?](#can-i-configure-clustering-for-a-basic-or-standard-cache)
* [È possibile utilizzare il clustering con i provider di stato della sessione ASP.NET Redis e la memorizzazione nella cache di Output di hello?](#can-i-use-clustering-with-the-redis-aspnet-session-state-and-output-caching-providers)
* [Usando StackExchange.Redis e il clustering si ottengono eccezioni MOVE. Cosa fare?](#i-am-getting-move-exceptions-when-using-stackexchangeredis-and-clustering-what-should-i-do)

### <a name="do-i-need-toomake-any-changes-toomy-client-application-toouse-clustering"></a>È necessario toomake qualsiasi toouse applicazione di modifiche toomy client clustering?
* Quando il clustering è abilitato, sarà disponibile solo il database 0. Se l'applicazione client utilizza più database e tenta di tooread o scrittura database tooa diverso da 0, hello seguente eccezione viene generata. `Unhandled Exception: StackExchange.Redis.RedisConnectionException: ProtocolFailure on GET --->``StackExchange.Redis.RedisCommandException: Multiple databases are not supported on this server; cannot switch toodatabase: 6`
  
  Per altre informazioni, vedere la [specifica sul cluster Redis: subset implementato](http://redis.io/topics/cluster-spec#implemented-subset).
* Se si usa [StackExchange.Redis](https://www.nuget.org/packages/StackExchange.Redis/), è necessario usare la versione 1.0.481 o successiva. La connessione della cache toohello utilizzando hello stesso [endpoint, porte e le chiavi](cache-configure.md#properties) utilizzati durante la connessione della cache tooa che non dispone di clustering abilitato. Hello unica differenza è che tutte le letture e scritture devono essere eseguite toodatabase 0.
  
  * Altri client possono avere requisiti diversi. Vedere [Tutti i client Redis supportano il clustering?](#do-all-redis-clients-support-clustering)
* Se l'applicazione usa più chiavi operazioni batch in un unico comando, tutte le chiavi devono trovarsi in hello stesso partizione. le chiavi toolocate in hello stesso partizione, vedere [modalità sono le chiavi di distribuzione in un cluster?](#how-are-keys-distributed-in-a-cluster)
* Se si usa il provider di stato della sessione ASP.NET Redis, è necessario usare la versione 2.0.1 o successiva. Vedere [è possibile utilizzare il clustering con i provider di stato della sessione ASP.NET Redis e la memorizzazione nella cache di Output di hello?](#can-i-use-clustering-with-the-redis-aspnet-session-state-and-output-caching-providers)

### <a name="how-are-keys-distributed-in-a-cluster"></a>Come vengono distribuite le chiavi in un cluster?
Per ogni hello Redis [il modello di distribuzione di chiavi](http://redis.io/topics/cluster-spec#keys-distribution-model) documentazione: spazio della chiave hello è suddiviso in 16384 slot. Ogni chiave è stato eseguito l'hashing e assegnato tooone di questi slot, cui sono distribuiti tra i nodi del cluster hello hello. È possibile configurare quale parte della chiave di hello è tooensure con hash che più chiavi si trovano nella stesso partizione con il tag di hash hello.

* Le chiavi con un tag - hash se qualsiasi parte della chiave di hello è racchiuso tra parentesi `{` e `}`, solo tale parte della chiave hello viene eseguito l'hashing per hello determinazione dello slot di hello hash di una chiave. Ad esempio, hello dopo 3 chiavi potrebbe trovarsi in hello partizione stesso: `{key}1`, `{key}2`, e `{key}3` dal solo hello `key` parte del nome hello viene eseguito l'hashing. Per un elenco completo di specifiche dei tag hash per le chiavi, vedere la pagina relativa ai [tag hash per le chiavi](http://redis.io/topics/cluster-spec#keys-hash-tags).
* Chiavi senza un tag di hash - nome della chiave intera hello viene utilizzato per l'hashing. Ciò comporta una distribuzione uniforme statisticamente tra partizioni hello della cache di hello.

Per ottimizzare le prestazioni e velocità effettiva, si consiglia di distribuire le chiavi di hello in modo uniforme. Se si usano le chiavi con un tag di hash è chiavi hello tooensure di responsabilità dell'applicazione hello siano distribuite uniformemente.

Per altre informazioni, vedere le pagine relative al [modello di distribuzione delle chiavi](http://redis.io/topics/cluster-spec#keys-distribution-model), al [partizionamento orizzontale del cluster Redis](http://redis.io/topics/cluster-tutorial#redis-cluster-data-sharding) e ai [tag hash per le chiavi](http://redis.io/topics/cluster-spec#keys-hash-tags).

Per il codice di esempio sull'utilizzo di clustering e l'individuazione di chiavi in hello stesso partizione con client stackexchange. Redis hello, vedere hello [clustering.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/Clustering.cs) parte hello [Hello World](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) esempio.

### <a name="what-is-hello-largest-cache-size-i-can-create"></a>Che cos'è una dimensione della cache più grande hello che posso creare?
dimensione della cache premium più grande di Hello è 53 GB. È possibile creare le partizioni too10 offrendo una dimensione massima di 530 GB. Se è necessaria una dimensione maggiore, è possibile [farne richiesta](mailto:wapteams@microsoft.com?subject=Redis%20Cache%20quota%20increase). Per altre informazioni, vedere [Prezzi di Cache Redis di Azure](https://azure.microsoft.com/pricing/details/cache/).

### <a name="do-all-redis-clients-support-clustering"></a>Tutti i client Redis supportano il clustering?
In hello ora corrente, non tutti i client supportano Redis clustering. StackExchange.Redis è uno dei client che supporta questa funzionalità. Per ulteriori informazioni su altri client, vedere hello [Playing with cluster hello](http://redis.io/topics/cluster-tutorial#playing-with-the-cluster) sezione di hello [esercitazione cluster Redis](http://redis.io/topics/cluster-tutorial).

> [!NOTE]
> Se si utilizza il client stackexchange. Redis, assicurarsi di utilizzare più recente di hello [stackexchange. Redis](https://www.nuget.org/packages/StackExchange.Redis/) 1.0.481 o versione successiva per il clustering toowork correttamente. Per altre informazioni in caso di problemi con le eccezioni MOVE, vedere la sezione relativa alle [eccezioni MOVE](#move-exceptions) .
> 
> 

### <a name="how-do-i-connect-toomy-cache-when-clustering-is-enabled"></a>Come connettersi toomy cache quando il servizio cluster è abilitato?
È possibile connettersi tooyour cache utilizzando hello stesso [endpoint](cache-configure.md#properties), [porte](cache-configure.md#properties), e [chiavi](cache-configure.md#access-keys) utilizzati durante la connessione della cache tooa che non dispone di clustering abilitato. Redis gestisce hello clustering nel back-end hello in modo non si dispone di toomanage dal client.

### <a name="can-i-directly-connect-toohello-individual-shards-of-my-cache"></a>È possibile connettersi direttamente toohello singole partizioni di my cache?
Questa operazione non è supportata ufficialmente. Ciò premesso, ogni partizione è costituita da una coppia di cache primaria/di replica nota complessivamente come un'istanza della cache. È possibile connettersi a istanze di cache toothese tramite l'utilità di redis-cli hello hello [instabile](http://redis.io/download) ramo del repository di Redis hello in GitHub. Questa versione implementa il supporto di base iniziali di hello `-c` passare. Per ulteriori informazioni vedere [Playing with cluster hello](http://redis.io/topics/cluster-tutorial#playing-with-the-cluster) su [http://redis.io](http://redis.io) in hello [esercitazione cluster Redis](http://redis.io/topics/cluster-tutorial).

Per non ssl, utilizzare hello i comandi seguenti.

    Redis-cli.exe –h <<cachename>> -p 13000 (tooconnect tooinstance 0)
    Redis-cli.exe –h <<cachename>> -p 13001 (tooconnect tooinstance 1)
    Redis-cli.exe –h <<cachename>> -p 13002 (tooconnect tooinstance 2)
    ...
    Redis-cli.exe –h <<cachename>> -p 1300N (tooconnect tooinstance N)

Per ssl, sostituire `1300N` con `1500N`.

### <a name="can-i-configure-clustering-for-a-previously-created-cache"></a>È possibile configurare il clustering per una cache creata in precedenza?
Al momento è possibile solo abilitare il clustering durante la creazione di una cache. È possibile modificare le dimensioni di cluster hello dopo la creazione di cache di hello, ma non è possibile aggiungere clustering tooa premium cache o rimuovere il servizio cluster da una cache premium dopo la creazione della cache di hello. Una cache premium con il clustering abilitato e solo una partizione è diversa da una cache premium di hello stesse dimensioni con alcun tipo di clustering.

### <a name="can-i-configure-clustering-for-a-basic-or-standard-cache"></a>È possibile configurare il clustering per una cache Basic o Standard?
Il clustering è disponibile esclusivamente per le cache Premium.

### <a name="can-i-use-clustering-with-hello-redis-aspnet-session-state-and-output-caching-providers"></a>È possibile utilizzare il clustering con i provider di stato della sessione ASP.NET Redis e la memorizzazione nella cache di Output di hello?
* **Provider di cache di output Redis** : nessuna modifica necessaria.
* **Provider di stato della sessione redis** -toouse clustering, è necessario utilizzare [RedisSessionStateProvider](https://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider) 2.0.1 o versione successiva o un'eccezione viene generata. Si tratta di una modifica significativa. Per altre informazioni, vedere la pagina relativa ai [dettagli delle modifiche significative della versione 2.0.0](https://github.com/Azure/aspnet-redis-providers/wiki/v2.0.0-Breaking-Change-Details).

<a name="move-exceptions"></a>

### <a name="i-am-getting-move-exceptions-when-using-stackexchangeredis-and-clustering-what-should-i-do"></a>Usando StackExchange.Redis e il clustering si ottengono eccezioni MOVE. Cosa fare?
Se si usa StackExchange.Redis e si ricevono eccezioni `MOVE` quando si usa il clustering, assicurarsi di usare [StackExchange.Redis 1.1.603](https://www.nuget.org/packages/StackExchange.Redis/) o versioni successive. Per istruzioni sulla configurazione del toouse di applicazioni .NET stackexchange. Redis, vedere [configurare i client della cache di hello](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).

## <a name="next-steps"></a>Passaggi successivi
Informazioni su come toouse premium più memorizzano nella cache le funzionalità.

* [Livello di introduzione toohello Premium di Cache Redis di Azure](cache-premium-tier-intro.md)

<!-- IMAGES -->

[redis-cache-clustering]: ./media/cache-how-to-premium-clustering/redis-cache-clustering.png

[redis-cache-clustering-selected]: ./media/cache-how-to-premium-clustering/redis-cache-clustering-selected.png

[redis-cache-redis-cluster-size]: ./media/cache-how-to-premium-clustering/redis-cache-redis-cluster-size.png







