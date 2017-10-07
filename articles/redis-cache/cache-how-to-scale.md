---
title: aaaHow tooScale Cache Redis di Azure | Documenti Microsoft
description: Informazioni su come tooscale di Azure Redis nella Cache istanze
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 350db214-3b7c-4877-bd43-fef6df2db96c
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 04/11/2017
ms.author: sdanie
ms.openlocfilehash: 8d7c015a539f872913056392aa080bf3f445bd03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-azure-redis-cache"></a>La modalità di Cache Redis di Azure di tooScale
Cache Redis di Azure ha diverse offerte di cache, che forniscono flessibilità nella scelta di hello di dimensioni della cache e le funzionalità. Dopo aver creata una cache, è possibile ridimensionare dimensioni hello e hello tariffario della cache di hello se hello i requisiti dell'applicazione cambiano. Questo articolo illustra come tooscale la cache nel portale di Azure hello e utilizzando strumenti quali Azure PowerShell e CLI di Azure.

## <a name="when-tooscale"></a>Quando tooscale
È possibile utilizzare hello [monitoraggio](cache-how-to-monitor.md) funzionalità di Cache Redis di Azure toomonitor hello integrità e le prestazioni della cache e determinare quando tooscale hello cache. 

È possibile monitorare i seguenti hello metriche toohelp determinare se è necessario tooscale.

* Carico server Redis
* Utilizzo della memoria
* Larghezza di banda della rete
* Utilizzo di CPU

Se si determina che la cache non soddisfa i requisiti dell'applicazione, è possibile ridimensionare tooa o ridurre le dimensioni della cache tariffario appropriato per l'applicazione. Per ulteriori informazioni su come determinare quale memorizzare nella cache toouse livello dei prezzi, vedere [quali offerta di Cache Redis e dimensioni è consigliabile usare](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).

## <a name="scale-a-cache"></a>Ridimensionare una cache
tooscale cache, [Sfoglia cache toohello](cache-configure.md#configure-redis-cache-settings) in hello [portale di Azure](https://portal.azure.com) e fare clic su **scala** da hello **menu risorse**.

![Scalabilità](./media/cache-how-to-scale/redis-cache-scale-menu.png)

Seleziona hello desiderato da hello piano tariffario **selezionare tariffario** pannello e fare clic su **selezionare**.

![Piano tariffario ][redis-cache-pricing-tier-blade]


È possibile scalare tooa diverso livello di prezzo con hello seguenti restrizioni:

* Non è possibile scalare da un piano tariffario superiore tooa livello inferiore a livello di prezzo.
  * Non è possibile scalare da un **Premium** cache verso il basso tooa **Standard** o **base** della cache.
  * Non è possibile scalare da un **Standard** cache verso il basso tooa **base** della cache.
* È possibile scalare da un **base** cache tooa **Standard** cache ma è Impossibile modificare la dimensione di hello in hello contemporaneamente. Se è necessario dimensioni diverse, è possibile eseguire una successiva dimensione toohello desiderato operazione.
* Non è possibile scalare da un **base** memorizzare nella cache direttamente tooa **Premium** cache. È necessario applicare la scalabilità da **base** troppo**Standard** in un'unica operazione di ridimensionamento e quindi da **Standard** troppo**Premium** una scalabilità successivi operazione.
* Non è possibile scalare da una dimensione maggiore verso il basso toohello **C0 (250 MB)** dimensioni.
 
Mentre è hello scalabilità toohello nuovo piano tariffario, un **Scaling** stato viene visualizzato in hello **Cache Redis** blade.

![Ridimensionamento][redis-cache-scaling]

Quando la scalabilità è stata completata, lo stato di hello cambia da **Scaling** troppo**esecuzione**.

## <a name="how-tooautomate-a-scaling-operation"></a>Come tooautomate un'operazione di ridimensionamento
In aggiunta tooscaling delle istanze di cache di hello portale di Azure, è possibile scalare tramite i cmdlet di PowerShell, CLI di Azure e utilizzando hello Microsoft Azure Gestione librerie (MAML). 

* [Ridimensionare la cache tramite PowerShell](#scale-using-powershell)
* [Ridimensionare la cache tramite l'interfaccia della riga di comando di Azure](#scale-using-azure-cli)
* [Ridimensionare la cache tramite le librerie di gestione di Microsoft Azure](#scale-using-maml)

### <a name="scale-using-powershell"></a>Ridimensionare la cache tramite PowerShell
È possibile ridimensionare le istanze di Cache Redis di Azure con PowerShell tramite hello [Set AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet quando hello `Size`, `Sku`, o `ShardCount` si modificano le proprietà. Hello esempio seguente viene illustrato come tooscale una cache denominata `myCache` tooa 2,5 GB cache. 

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

Per ulteriori informazioni sulla scalabilità con PowerShell, vedere [tooscale un Redis nella cache utilizzando Powershell](cache-howto-manage-redis-cache-powershell.md#scale).

### <a name="scale-using-azure-cli"></a>Ridimensionare la cache tramite l'interfaccia della riga di comando di Azure
chiamare le istanze di Cache Redis di Azure mediante Azure CLI, tooscale hello `azure rediscache set` comando e passare le modifiche di configurazione hello lo si desidera includere una nuova dimensione, sku o le dimensioni di cluster, a seconda di hello desiderato l'operazione di ridimensionamento.

Per altre informazioni sul ridimensionamento tramite l'interfaccia della riga di comando di Azure, vedere [Modificare le impostazioni di una Cache Redis esistente](cache-manage-cli.md#scale).

### <a name="scale-using-maml"></a>Ridimensionare la cache tramite le librerie di gestione di Microsoft Azure
tooscale le istanze di Cache Redis di Azure utilizzando hello [Microsoft Azure Gestione librerie (MAML)](http://azure.microsoft.com/updates/management-libraries-for-net-release-announcement/), chiamata hello `IRedisOperations.CreateOrUpdate` (metodo) e passare hello nuove dimensioni hello `RedisProperties.SKU.Capacity`.

    static void Main(string[] args)
    {
        // For instructions on getting hello access token, see
        // https://azure.microsoft.com/documentation/articles/cache-configure/#access-keys
        string token = GetAuthorizationHeader();

        TokenCloudCredentials creds = new TokenCloudCredentials(subscriptionId,token);

        RedisManagementClient client = new RedisManagementClient(creds);
        var redisProperties = new RedisProperties();

        // tooscale, set a new size for hello redisSKUCapacity parameter.
        redisProperties.Sku = new Sku(redisSKUName,redisSKUFamily,redisSKUCapacity);
        redisProperties.RedisVersion = redisVersion;
        var redisParams = new RedisCreateOrUpdateParameters(redisProperties, redisCacheRegion);
        client.Redis.CreateOrUpdate(resourceGroupName,cacheName, redisParams);
    }

Per ulteriori informazioni, vedere hello [gestire Cache Redis tramite MAML](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) esempio.

## <a name="scaling-faq"></a>Domande frequenti relative al ridimensionamento
Hello elenco seguente contiene le risposte toocommonly domande frequenti sulla scalabilità di Cache Redis di Azure.

* [È possibile eseguire un ridimensionamento verso, da o in una cache Premium?](#can-i-scale-to-from-or-within-a-premium-cache)
* [Dopo il ridimensionamento, è necessario toochange personali chiavi di accesso o nome della cache?](#after-scaling-do-i-have-to-change-my-cache-name-or-access-keys)
* [Come funziona il ridimensionamento?](#how-does-scaling-work)
* [Durante il ridimensionamento i dati nella cache andranno persi?](#will-i-lose-data-from-my-cache-during-scaling)
* [L'impostazione databases personalizzata viene modificata durante il ridimensionamento?](#is-my-custom-databases-setting-affected-during-scaling)
* [La cache rimarrà disponibile durante il ridimensionamento?](#will-my-cache-be-available-during-scaling)
* [Operazioni non supportate](#operations-that-are-not-supported)
* [Quanto tempo richiede il ridimensionamento?](#how-long-does-scaling-take)
* [Come è possibile stabilire quando il ridimensionamento è completato?](#how-can-i-tell-when-scaling-is-complete)

### <a name="can-i-scale-to-from-or-within-a-premium-cache"></a>È possibile eseguire un ridimensionamento verso, da o in una cache Premium?
* Non è possibile scalare da un **Premium** cache verso il basso tooa **base** o **Standard** piano tariffario.
* È possibile scalare da una **Premium** prezzi tooanother a livello di cache.
* Non è possibile scalare da un **base** memorizzare nella cache direttamente tooa **Premium** cache. È innanzitutto necessario scalare da **base** troppo**Standard** in un'unica operazione di ridimensionamento e quindi da **Standard** troppo**Premium** in una successiva l'operazione di ridimensionamento.
* Se è stato abilitato il servizio cluster al momento della creazione del **Premium** cache, è possibile [modificare dimensioni cluster hello](cache-how-to-premium-clustering.md#cluster-size). Se la cache è stata creata senza clustering abilitato, non è possibile configurare il clustering in un secondo momento.
  
  Per ulteriori informazioni, vedere [come tooconfigure clustering per una Cache Redis di Azure Premium](cache-how-to-premium-clustering.md).

### <a name="after-scaling-do-i-have-toochange-my-cache-name-or-access-keys"></a>Dopo il ridimensionamento, è necessario toochange personali chiavi di accesso o nome della cache?
No, il nome della cache e le chiavi restano invariati durante un'operazione di ridimensionamento.

### <a name="how-does-scaling-work"></a>Come funziona il ridimensionamento?
* Quando un **base** cache viene scalata tooa dimensioni diverse, viene arrestata e viene eseguito il provisioning di una nuova cache utilizzando hello nuova dimensione. Durante questo periodo, non è disponibile della cache di hello e tutti i dati nella cache di hello viene perso.
* Quando un **base** cache viene scalata tooa **Standard** cache, viene eseguito il provisioning di una cache di replica e dati hello viene copiati dalla cache di hello cache primaria toohello replica. cache di Hello resta disponibile durante il ridimensionamento processo hello.
* Quando un **Standard** cache è di dimensioni diverse scalato tooa o tooa **Premium** cache, una delle repliche hello viene chiuso e rieffettuare il provisioning toohello nuova dimensione e hello dati trasferiti e altri hello replica esegue un failover prima di nuovo il provisioning, il processo toohello simile che si verifica durante un errore di uno dei nodi della cache di hello.

### <a name="will-i-lose-data-from-my-cache-during-scaling"></a>Durante il ridimensionamento i dati nella cache andranno persi?
* Quando un **base** cache viene scalata tooa nuove dimensioni, tutti i dati vengono persa e cache di hello è disponibile durante l'operazione di ridimensionamento hello.
* Quando un **base** cache viene scalata tooa **Standard** memorizzare nella cache, hello i dati nella cache di hello sono in genere mantenuti.
* Quando un **Standard** cache è di dimensioni maggiori tooa scalato o livello, o un **Premium** cache viene scalata tooa dimensioni, tutti i dati in genere viene mantenuta. Quando si ridimensiona un **Standard** o **Premium** cache verso il basso tooa dimensioni inferiori, dati potrebbe andare persa a seconda della quantità di dati nella cache di hello relativi toohello nuove dimensioni quando viene ridimensionato. Se i dati vengono persi in caso di ridimensionamento verso il basso, le chiavi vengono rimossi utilizzando hello [allkeys lru](http://redis.io/topics/lru-cache) criteri di rimozione. 

### <a name="is-my-custom-databases-setting-affected-during-scaling"></a>L'impostazione databases personalizzata viene modificata durante il ridimensionamento?
Alcuni piani tariffari presentano diversi [database limiti](cache-configure.md#databases), pertanto vi sono alcune considerazioni quando scalabilità verso il basso se è configurato un valore personalizzato per hello `databases` impostazione durante la creazione della cache.

* Quando la scalabilità tooa tariffario con inferiore `databases` limite rispetto al livello corrente di hello:
  * Se si utilizza il numero predefinito di hello di `databases` che è 16 per tutti i piani tariffari, nessun dato venga perso.
  * Se si utilizza un numero personalizzato di `databases` che rientra nei limiti di hello di hello livello toowhich è possibile scalare, questo `databases` impostazione viene mantenuta e nessun dato venga perso.
  * Se si utilizza un numero personalizzato di `databases` che supera i limiti di hello del nuovo livello hello, hello `databases` impostazione è data dai limiti toohello abbassato di livello nuovo hello e tutti i dati nei database hello rimosso viene perso.
* Quando la scalabilità tooa tariffario con hello uguale o maggiore `databases` limite rispetto al livello corrente di hello del `databases` impostazione viene mantenuta e nessun dato venga perso.

Si noti che mentre le cache Standard e Premium dispongono di un contratto di servizio pari al 99,9% di disponibilità, non esiste un contratto di servizio per la perdita dei dati.

### <a name="will-my-cache-be-available-during-scaling"></a>La cache rimarrà disponibile durante il ridimensionamento?
* **Standard** e **Premium** cache rimangano disponibile durante l'operazione di ridimensionamento hello.
* **Base** cache sono offline durante l'adattamento delle dimensioni di operazioni tooa diverse, ma rimangono disponibili anche quando la scalabilità da **base** troppo**Standard**.

### <a name="operations-that-are-not-supported"></a>Operazioni non supportate
* Non è possibile scalare da un piano tariffario superiore tooa livello inferiore a livello di prezzo.
  * Non è possibile scalare da un **Premium** cache verso il basso tooa **Standard** o **base** della cache.
  * Non è possibile scalare da un **Standard** cache verso il basso tooa **base** della cache.
* È possibile scalare da un **base** cache tooa **Standard** cache ma è Impossibile modificare la dimensione di hello in hello contemporaneamente. Se è necessario dimensioni diverse, è possibile eseguire una successiva dimensione toohello desiderato operazione.
* Non è possibile scalare da un **base** memorizzare nella cache direttamente tooa **Premium** cache. È innanzitutto necessario scalare da **base** troppo**Standard** in un'unica operazione di ridimensionamento e quindi da **Standard** troppo**Premium** in una successiva l'operazione di ridimensionamento.
* Non è possibile scalare da una dimensione maggiore verso il basso toohello **C0 (250 MB)** dimensioni.

Se un'operazione di ridimensionamento non riesce, il servizio di hello tenterà operazione hello toorevert e cache di hello verrà ripristinato dimensioni originali toohello.

### <a name="how-long-does-scaling-take"></a>Quanto tempo richiede il ridimensionamento?
Il ridimensionamento richiede circa 20 minuti, a seconda della quantità di dati nella cache di hello.

### <a name="how-can-i-tell-when-scaling-is-complete"></a>Come è possibile stabilire quando il ridimensionamento è completato?
Nel portale di Azure hello è possibile visualizzare hello l'operazione di ridimensionamento in corso. Al termine scalabilità, hello dello stato delle modifiche di cache di hello troppo**esecuzione**.

<!-- IMAGES -->

[redis-cache-pricing-tier-blade]: ./media/cache-how-to-scale/redis-cache-pricing-tier-blade.png

[redis-cache-scaling]: ./media/cache-how-to-scale/redis-cache-scaling.png



