---
title: Servizio Cache gestita applicazioni tooRedis - Azure aaaMigrate | Documenti Microsoft
description: Informazioni su come toomigrate servizio Cache gestita e Cache nel ruolo di applicazioni tooAzure Cache Redis
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 041f077b-8c8e-4d7c-a3fc-89d334ed70d6
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 05/30/2017
ms.author: sdanie
ms.openlocfilehash: bd81722820acf0d2637828fbb6100c723aafeba5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-managed-cache-service-tooazure-redis-cache"></a>Eseguire la migrazione da servizio Cache gestita tooAzure Cache Redis
La migrazione delle applicazioni che utilizzano tooAzure servizio Cache gestita di Azure Redis Cache può essere eseguita con applicazione tooyour modifiche minime, a seconda delle funzionalità del servizio Cache gestito di hello utilizzati dall'applicazione di memorizzazione nella cache. Hello API non sono esattamente hello stesso sono simili, mentre la maggior parte del codice esistente che utilizza tooaccess servizio Cache gestita una cache può essere riutilizzata con modifiche minime. In questo argomento viene illustrato come applicazione e configurazione necessarie di hello toomake cambia toomigrate toouse di applicazioni del servizio Cache gestita Cache Redis di Azure e viene illustrato come alcune delle funzionalità di hello di Cache Redis di Azure può essere utilizzato tooimplement hello funzionalità di una cache del servizio Cache gestita.

>[!NOTE]
>Servizio cache gestita e Cache nel ruolo sono stati [ritirati](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/) il 30 novembre 2016. Se si dispone di tutte le distribuzioni di Cache nel ruolo che si desidera toomigrate tooAzure Cache Redis, è possibile seguire i passaggi di hello in questo articolo.

## <a name="migration-steps"></a>Passaggi della migrazione
Hello seguendo i passaggi è necessari toomigrate un toouse di applicazione del servizio Cache gestito Cache Redis di Azure.

* Eseguire il mapping del servizio Cache gestito funzionalità tooAzure Cache Redis
* Scegliere un'offerta per il servizio cache
* Creare una cache
* Configurare i client della Cache di hello
  * Rimuovere hello configurazione del servizio Cache gestito
  * Configurare un client della cache mediante hello pacchetto NuGet stackexchange. Redis
* Eseguire la migrazione del codice del Servizio cache gestita
  * La connessione della cache toohello utilizzando classe ConnectionMultiplexer hello
  * Tipi di dati primitivi di accesso nella cache di hello
  * Utilizzo di oggetti .NET nella cache di hello
* Eseguire la migrazione di stato della sessione ASP.NET e la memorizzazione nella cache tooAzure Redis Cache di Output 

## <a name="map-managed-cache-service-features-tooazure-redis-cache"></a>Eseguire il mapping del servizio Cache gestito funzionalità tooAzure Cache Redis
Il Servizio cache gestita di Azure e la Cache Redis di Azure sono simili, ma implementano alcune funzionalità in modi diversi. In questa sezione vengono descritte alcune delle differenze di hello e vengono fornite informazioni aggiuntive sull'implementazione della funzionalità di hello del servizio Cache gestita in Cache Redis di Azure.

| Funzionalità del Servizio cache gestita | Supporto del Servizio cache gestita | Supporto della Cache Redis di Azure |
| --- | --- | --- |
| Cache denominate |La cache predefinita è configurata e in hello Standard e Premium offerte di cache, backup toonine altre cache denominate possono essere configurate se si desidera. |Cache Redis di Azure dispone di un numero configurabile di database (valore predefinito è 16) che possono essere utilizzati tooimplement memorizza nella cache un toonamed funzionalità simili. Per altre informazioni, vedere [Informazioni sui database Redis](cache-faq.md#what-are-redis-databases) e [Configurazione predefinita del server Redis](cache-configure.md#default-redis-server-configuration). |
| Disponibilità elevata |Fornisce la disponibilità elevata per gli elementi nella cache di hello nelle offerte di cache Standard e Premium hello. Se gli elementi vengono persi a causa di un errore tooa, le copie di backup di elementi di hello nella cache di hello sono ancora disponibili. Scrive la cache secondaria toohello vengono eseguite in modo sincrono. |Disponibilità elevata è disponibile in hello Standard e Premium offerte di cache, che dispongono di una configurazione principale/Replica due nodi (ogni partizione in una cache Premium ha una coppia di principale/replica). Replica toohello operazioni di scrittura vengono eseguite in modo asincrono. Per altre informazioni, vedere [Prezzi di Cache Redis di Azure](https://azure.microsoft.com/pricing/details/cache/). |
| Notifiche |Consente ai client tooreceive le notifiche asincrone quando un'ampia gamma di operazioni della cache si verificano in una cache denominata. |Applicazioni client possono utilizzare Redis pub/sub o [le notifiche di spazio delle chiavi](cache-configure.md#keyspace-notifications-advanced-settings) tooachieve un toonotifications funzionalità simili. |
| Cache locale |Archivia una copia di oggetti memorizzati nella cache in locale sul client hello per un accesso molto veloce. |Applicazioni client dovrebbero essere tooimplement questa funzionalità usando un dizionario o una simile struttura dei dati. |
| Criteri di rimozione |Nessuno o utilizzati meno di recente (LRU). criteri predefiniti Hello sono LRU. |Cache Redis di Azure supporta i seguenti criteri di eliminazione hello: volatile-lru, allkeys-lru, volatile-casuali, allkeys casuale volatile-durata (TTL), noeviction. criteri predefiniti Hello sono volatile-lru. Per altre informazioni, vedere [Configurazione predefinita del server Redis](cache-configure.md#default-redis-server-configuration). |
| Criteri di scadenza |il criterio di scadenza predefinito Hello è assoluto e intervallo di scadenza predefinita hello è dieci minuti. Sono disponibili anche i criteri Scorrevole e Mai. |Per impostazione predefinita gli elementi nella cache di hello non scadono, ma una data di scadenza può essere configurata in base a ogni scrittura usando gli overload di set di cache. Per ulteriori informazioni, vedere [aggiungere e recuperare oggetti dalla cache di hello](cache-dotnet-how-to-use-azure-redis-cache.md#add-and-retrieve-objects-from-the-cache). |
| Aree e aggiunta di tag |Le aree sono sottogruppi degli elementi memorizzati nella cache. Le aree supportano anche l'annotazione di hello degli elementi della cache con stringhe descrittive aggiuntive denominate tag. Le aree supportano operazioni di ricerca di hello possibilità tooperform sugli elementi con tag in tale area. Tutti gli elementi all'interno di un'area si trovano all'interno di un singolo nodo del cluster di cache di hello. |Una cache Redis costituito da un singolo nodo (a meno che non è stato abilitato cluster Redis) in modo hello concetto di aree del servizio Cache gestito non è applicabile. Redis supporta la ricerca e operazioni con caratteri jolly durante il recupero delle chiavi in modo che tag descrittivi può essere incorporato all'interno dei nomi chiave hello e utilizzati in un secondo momento gli elementi di hello tooretrieve. Per un esempio di implementazione di una soluzione di aggiunta di tag con Redis, vedere la pagina relativa all' [implementazione dell'aggiunta di tag della cache con Redis](http://stackify.com/implementing-cache-tagging-redis/). |
| Serializzazione |Cache gestita supporta NetDataContractSerializer, BinaryFormatter e utilizzo di hello di serializzatori personalizzati. Hello predefinito è NetDataContractSerializer. |È responsabilità di hello hello oggetti del client dell'applicazione tooserialize .NET prima di inserirli nella cache di hello, con la scelta hello del serializzatore hello backup toohello sviluppatore dell'applicazione client. Per ulteriori informazioni e codice di esempio, vedere [funziona con oggetti .NET nella cache di hello](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache). |
| Emulatore di cache |Il servizio Cache gestita offre un emulatore di cache locale. |Cache Redis di Azure non dispone di un emulatore, ma è possibile [eseguito localmente compilazione MSOpenTech hello di redis server.exe](cache-faq.md#cache-emulator) tooprovide un'esperienza di emulatore. |

## <a name="choose-a-cache-offering"></a>Scegliere un'offerta per il servizio cache
Cache Redis di Microsoft Azure è disponibile in hello livelli seguenti:

* **Basic**: singolo nodo. Più dimensioni too53 GB.
* **Standard**: principale/replica a due nodi. Più dimensioni too53 GB. Contratti di servizio del 99,9%.
* **Premium** : due nodi primario/Replica con backup too10 partizioni. Più dimensioni che vanno da 6 GB too530 GB. Supporto per tutte le funzionalità del piano Standard e altre, tra cui [cluster Redis](cache-how-to-premium-clustering.md), [persistenza Redis](cache-how-to-premium-persistence.md) e [Rete virtuale di Azure](cache-how-to-premium-vnet.md). Contratti di servizio del 99,9%.

Ogni livello presenta differenze in termini di funzionalità e prezzi. Hello funzionalità sono illustrate più avanti in questa Guida e per ulteriori informazioni sui prezzi, vedere [dettagli prezzi di Cache](https://azure.microsoft.com/pricing/details/cache/).

Un punto di partenza per la migrazione è toopick hello dimensione che corrisponde alle dimensioni della cache del servizio Cache gestito precedente hello e quindi aumentare o diminuire a seconda dei requisiti di hello dell'applicazione. Per ulteriori informazioni sulla scelta hello destra offerta di Cache Redis di Azure, vedere [quali offerta di Cache Redis e dimensioni è consigliabile usare?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).

## <a name="create-a-cache"></a>Creare una cache
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="configure-hello-cache-clients"></a>Configurare i client della Cache di hello
Dopo aver creato e configurata cache di hello, configurazione del servizio Cache gestito di hello tooremove passaggio successivo hello e aggiungere hello aggiungere i riferimenti e configurazione di Cache Redis di Azure di hello in modo che i client della cache possono accedere alle cache di hello.

* Rimuovere hello configurazione del servizio Cache gestito
* Configurare un client della cache mediante hello pacchetto NuGet stackexchange. Redis

### <a name="remove-hello-managed-cache-service-configuration"></a>Rimuovere hello configurazione del servizio Cache gestito
Prima di hello applicazioni client possono essere configurate per Cache Redis di Azure, configurazione del servizio Cache gestito esistente hello e riferimenti all'assembly deve essere rimossa mediante disinstallazione del pacchetto NuGet del servizio Cache gestito di hello.

hello toouninstall pacchetto NuGet del servizio Cache gestito, fare doppio clic su progetto client hello in **Esplora** e scegliere **Gestisci pacchetti NuGet**. Seleziona hello **i pacchetti installati** nodo e tipo W**indowsAzure.Caching** in hello Cerca in casella pacchetti installati. Selezionare **Windows** **Cache di Azure** (o **Windows** **la memorizzazione nella cache di Azure** a seconda della versione di hello del pacchetto NuGet hello), fare clic su  **Disinstallare**, quindi fare clic su **Chiudi**.

![Disinstallare il pacchetto NuGet del Servizio cache gestita di Azure](./media/cache-migrate-to-redis/IC757666.jpg)

Pacchetto NuGet del servizio Cache gestito di hello disinstallazione rimuove gli assembly del servizio Cache gestito di hello e le voci del servizio Cache gestito di hello hello file app. config o Web. config dell'applicazione client hello. Poiché alcune impostazioni personalizzate non possono essere rimossi quando si disinstalla il pacchetto NuGet di hello, aprire Web. config o App. config e verificare che hello segue gli elementi vengono completamente rimossi.

Verificare che hello `dataCacheClients` voce viene rimossa dal hello `configSections` elemento. Non rimuovere hello intero `configSections` elemento; solo remove hello `dataCacheClients` voce, se presente.

```xml
<configSections>
  <!-- Existing sections omitted for clarity. -->
  <section name="dataCacheClients"type="Microsoft.ApplicationServer.Caching.DataCacheClientsSection, Microsoft.ApplicationServer.Caching.Core" allowLocation="true" allowDefinition="Everywhere"/>
</configSections>
```

Verificare che hello `dataCacheClients` sezione è stata rimossa. Hello `dataCacheClients` sezione sarà simile toohello esempio seguente.

```xml
<dataCacheClients>
  <dataCacheClientname="default">
    <!--toouse hello in-role flavor of Azure Cache, set identifier toobe hello cache cluster role name -->
    <!--toouse hello Azure Managed Cache Service, set identifier toobe hello endpoint of hello cache cluster -->
    <autoDiscoverisEnabled="true"identifier="[Cache role name or Service Endpoint]"/>

    <!--<localCache isEnabled="true" sync="TimeoutBased" objectCount="100000" ttlValue="300" />-->
    <!--Use this section toospecify security settings for connecting tooyour cache. This section is not required if your cache is hosted on a role that is a part of your cloud service. -->
    <!--<securityProperties mode="Message" sslEnabled="true">
      <messageSecurity authorizationInfo="[Authentication Key]" />
    </securityProperties>-->
  </dataCacheClient>
</dataCacheClients>
```

Dopo la rimozione di configurazione del servizio Cache gestito di hello, è possibile configurare i client della cache di hello come descritto nella seguente sezione hello.

### <a name="configure-a-cache-client-using-hello-stackexchangeredis-nuget-package"></a>Configurare un client della cache mediante hello pacchetto NuGet stackexchange. Redis
[!INCLUDE [redis-cache-configure](../../includes/redis-cache-configure-stackexchange-redis-nuget.md)]

## <a name="migrate-managed-cache-service-code"></a>Eseguire la migrazione del codice del Servizio cache gestita
Hello API per client della cache di hello stackexchange. Redis è simile toohello servizio Cache gestito. In questa sezione viene fornita una panoramica delle differenze di hello.

### <a name="connect-toohello-cache-using-hello-connectionmultiplexer-class"></a>La connessione della cache toohello utilizzando classe ConnectionMultiplexer hello
Nel servizio Cache gestita, cache toohello le connessioni gestite dalla hello `DataCacheFactory` e `DataCache` classi. In Cache Redis di Azure, queste connessioni vengono gestite dall'hello `ConnectionMultiplexer` classe.

Aggiungere il seguente hello utilizzando l'istruzione toohello superiore di qualsiasi file da cui si desidera tooaccess hello cache.

```c#
using StackExchange.Redis
```

Se questo spazio dei nomi non viene risolto, assicurarsi di aver aggiunto hello pacchetto NuGet stackexchange. Redis come descritto in [configurare i client della cache di hello](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).

> [!NOTE]
> Si noti che il client stackexchange. Redis hello richiede .NET Framework 4 o versione successiva.
> 
> 

istanza di Cache Redis di Azure tooan tooconnect, chiamata hello statico `ConnectionMultiplexer.Connect` (metodo) e passare hello endpoint e la chiave. Un approccio toosharing un `ConnectionMultiplexer` istanza dell'applicazione è toohave una proprietà statica che restituisce un'istanza connessa, simile toohello esempio seguente. Fornisce un modo thread-safe di tooinitialize solo una singola connessione `ConnectionMultiplexer` istanza. In questo esempio `abortConnect` è toofalse set, il che significa che la chiamata hello avrà esito positivo anche se non viene stabilita una cache toohello di connessione. Una caratteristica fondamentale di `ConnectionMultiplexer` è che ripristinare automaticamente la cache toohello connettività quando vengono risolte i problemi di rete hello o altre cause.

```c#
private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
{
    return ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");
});

public static ConnectionMultiplexer Connection
{
    get
    {
        return lazyConnection.Value;
    }
}
```

Hello endpoint della cache, le chiavi e porte possono essere ottenute dalla hello **Cache Redis** pannello per l'istanza di cache. Per altre informazioni, vedere [Proprietà di Cache Redis](cache-configure.md#properties).

Una volta stabilita la connessione hello, restituire un database di riferimento toohello Redis cache dal chiamante hello `ConnectionMultiplexer.GetDatabase` metodo. oggetto Hello restituito da hello `GetDatabase` metodo è un oggetto passthrough semplice e non è necessario toobe archiviati.

```c#
IDatabase cache = Connection.GetDatabase();

// Perform cache operations using hello cache object...
// Simple put of integral data types into hello cache
cache.StringSet("key1", "value");
cache.StringSet("key2", 25);

// Simple get of data types from hello cache
string key1 = cache.StringGet("key1");
int key2 = (int)cache.StringGet("key2");
```

client stackexchange. Redis Hello utilizza hello `RedisKey` e `RedisValue` tipi per l'accesso e l'archiviazione di elementi nella cache di hello. Questi tipi eseguono il mapping ai tipi di linguaggio più primitivi, incluse le stringhe, e spesso non vengono usati direttamente. Redis stringhe sono hello il tipo di base del valore di Redis e possono contenere molti tipi di dati, inclusi flussi binari serializzati, mentre non è possibile utilizzare direttamente il tipo di hello, si utilizzerà metodi contenenti `String` nel nome hello. Per i tipi di dati primitivi più archiviare e recuperare elementi dalla cache di hello con hello `StringSet` e `StringGet` metodi, a meno che non si desidera archiviare le raccolte o altri tipi di dati Redis nella cache di hello. 

`StringSet`e `StringGet` sono molto simile toohello servizio Cache gestito `Put` e `Get` metodi, con uno principali differenze che prima di impostare e ottenere un oggetto .NET nella cache di hello è necessario serializzare prima. 

Quando si chiama `StringGet`, viene restituito se l'oggetto hello esiste, e in caso contrario, viene restituito null. In questo caso è possibile recuperare il valore di hello dall'origine dati desiderata hello e memorizzarlo nella cache di hello per un utilizzo successivo. Questo è noto come modello cache-aside hello.

scadenza hello toospecify di un elemento nella cache di hello, utilizzare hello `TimeSpan` parametro di `StringSet`.

```c#
cache.StringSet("key1", "value1", TimeSpan.FromMinutes(90));
```

Cache Redis di Azure può usare sia oggetti .NET che tipi di dati primitivi, ma prima della memorizzazione nella cache un oggetto .NET deve essere serializzato. Si tratta di sviluppatore hello dell'applicazione hello. In questo modo hello developer scelta hello del serializzatore hello. Per ulteriori informazioni e codice di esempio, vedere [funziona con oggetti .NET nella cache di hello](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).

## <a name="migrate-aspnet-session-state-and-output-caching-tooazure-redis-cache"></a>Eseguire la migrazione di stato della sessione ASP.NET e la memorizzazione nella cache tooAzure Redis Cache di Output
La Cache Redis di Azure include provider sia per lo stato della sessione ASP.NET che per la memorizzazione nella cache dell'output delle pagine. toomigrate l'applicazione che utilizza le versioni del servizio Cache gestito di hello di questi provider, rimuovere innanzitutto hello sezioni esistenti dal file Web. config e quindi configurare le versioni di Cache Redis di Azure hello dei provider hello. Per istruzioni sull'utilizzo di hello provider ASP.NET di Cache Redis di Azure, vedere [Provider di stato sessione ASP.NET per Cache Redis di Azure](cache-aspnet-session-state-provider.md) e [Provider di Cache di Output ASP.NET per Cache Redis di Azure](cache-aspnet-output-cache-provider.md).

## <a name="next-steps"></a>Passaggi successivi
Esplorare hello [documentazione Cache Redis di Azure](https://azure.microsoft.com/documentation/services/cache/) per esercitazioni, esempi, video e altro ancora.

