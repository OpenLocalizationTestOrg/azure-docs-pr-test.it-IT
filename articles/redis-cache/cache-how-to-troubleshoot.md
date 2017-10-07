---
title: aaaHow tootroubleshoot Cache Redis di Azure | Documenti Microsoft
description: Informazioni su come tooresolve comuni problemi a Cache Redis di Azure.
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 928b9b9c-d64f-4252-884f-af7ba8309af6
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: sdanie
ms.openlocfilehash: 4e736fce2b6d5200a2a8d802f3f1384b63458cab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootroubleshoot-azure-redis-cache"></a>La modalità di Cache Redis di Azure di tootroubleshoot
In questo articolo vengono fornite indicazioni per la risoluzione dei problemi hello seguenti categorie di problemi di Cache Redis di Azure.

* [Risoluzione dei problemi sul lato client](#client-side-troubleshooting) : in questa sezione vengono fornite linee guida sull'identificazione e risoluzione dei problemi causati dall'applicazione hello connessione tooAzure Cache Redis.
* [Risoluzione dei problemi sul lato server](#server-side-troubleshooting) : in questa sezione vengono fornite linee guida sull'identificazione e risoluzione dei problemi ha causato su hello sul lato server di Cache Redis di Azure.
* [Eccezioni di timeout di stackexchange. Redis](#stackexchangeredis-timeout-exceptions) -in questa sezione vengono fornite informazioni sulla risoluzione dei problemi quando si utilizza client stackexchange. Redis hello.

> [!NOTE]
> Numerosi hello risoluzione dei problemi in questa guida include istruzioni toorun sui comandi di Redis e monitorare le metriche delle prestazioni diversi. Per ulteriori informazioni e istruzioni, vedere gli articoli di hello hello [informazioni aggiuntive](#additional-information) sezione.
> 
> 

## <a name="client-side-troubleshooting"></a>Risoluzione dei problemi lato client
Questa sezione illustra la risoluzione dei problemi che si verificano a causa di una condizione in un'applicazione hello client.

* [Utilizzo della memoria nei client hello](#memory-pressure-on-the-client)
* [Burst di traffico](#burst-of-traffic)
* [Utilizzo elevato della CPU client](#high-client-cpu-usage)
* [Larghezza di banda lato client superata](#client-side-bandwidth-exceeded)
* [Dimensioni elevate della richiesta/risposta](#large-requestresponse-size)
* [Quali dati toomy verificato anomalo in Redis?](#what-happened-to-my-data-in-redis)

### <a name="memory-pressure-on-hello-client"></a>Utilizzo della memoria nei client hello
#### <a name="problem"></a>Problema
Utilizzo della memoria nei computer client hello lead tooall tipi di problemi di prestazioni che possono ritardare l'elaborazione dei dati che è stati inviati dall'istanza di Redis hello senza alcun ritardo. Quando viene rilevato l'utilizzo della memoria, il sistema hello include in genere toopage dati dalla memoria toovirtual di memoria fisica che si trova su disco. Questo *generare un errore di pagina* cause hello sistema tooslow verso il basso in modo significativo.

#### <a name="measurement"></a>Misura
1. Monitorare l'utilizzo di memoria nel computer toomake assicurarsi che non superi la memoria disponibile. 
2. Hello monitoraggio `Page Faults/Sec` contatore delle prestazioni. Poiché la maggior parte dei sistemi presenterà alcuni errori di pagina anche durante il normale funzionamento, controllare i picchi in questo contatore delle prestazioni degli errori di pagina corrispondenti ai timeout.

#### <a name="resolution"></a>Risoluzione
Aggiornare il client di client tooa maggiore dimensioni delle macchine Virtuali con più memoria o esaminare la memoria consuption tooreduce di memoria utilizzo modelli.

### <a name="burst-of-traffic"></a>Burst di traffico
#### <a name="problem"></a>Problema
Picchi di traffico combinato con scarso `ThreadPool` impostazioni possono causare ritardi nell'elaborazione dei dati già inviati dal Server Redis hello ma non ancora utilizzato sul lato client hello.

#### <a name="measurement"></a>Misura
Monitorare il cambiamento delle statistiche `ThreadPool` nel corso del tempo usando un codice [come questo](https://github.com/JonCole/SampleCode/blob/master/ThreadPoolMonitor/ThreadPoolLogger.cs). È anche possibile esaminare hello `TimeoutException` messaggio da stackexchange. Redis. Di seguito è fornito un esempio:

    System.TimeoutException: Timeout performing EVAL, inst: 8, mgr: Inactive, queue: 0, qu: 0, qs: 0, qc: 0, wr: 0, wq: 0, in: 64221, ar: 0, 
    IOCP: (Busy=6,Free=999,Min=2,Max=1000), WORKER: (Busy=7,Free=8184,Min=2,Max=8191)

In hello sopra messaggio, esistono alcuni problemi che sono interessanti:

1. Si noti che in hello `IOCP` sezione e hello `WORKER` sezione, è che un `Busy` valore maggiore di hello `Min` valore. Ciò significa che le impostazioni `ThreadPool` devono essere modificate.
2. È anche possibile osservare `in: 64221` Indica che 64211 byte ricevuti a livello di socket kernel hello ma non sono state ancora lette dall'applicazione hello (ad esempio stackexchange. Redis). In genere, ciò significa che l'applicazione non lettura dei dati dalla rete hello rapidamente server hello invio tooyou.

#### <a name="resolution"></a>Risoluzione
Configurare il [impostazioni pool di thread](https://gist.github.com/JonCole/e65411214030f0d823cb) toomake assicurarsi che il pool di thread verrà scalare rapidamente in burst scenari.

### <a name="high-client-cpu-usage"></a>Utilizzo elevato della CPU client
#### <a name="problem"></a>Problema
Utilizzo CPU elevato sul client hello è un'indicazione che il sistema di hello non resta sincronizzata con lavoro hello che ne è stato richiesto tooperform. Ciò significa che il client hello potrebbe non riuscire tooprocess una risposta da Redis in tempi brevi anche se Redis inviata risposta hello molto rapidamente.

#### <a name="measurement"></a>Misura
Hello monitor utilizzo CPU a livello di sistema tramite il portale di Azure hello o hello associati contatore delle prestazioni. Prestare attenzione non toomonitor *processo* CPU hello stesso poiché un singolo processo può avere un basso utilizzo della CPU nel tempo che il sistema complessivo della CPU può essere elevato. Cercare nell'utilizzo della CPU i picchi corrispondenti ai timeout. In seguito a elevato utilizzo della CPU, è inoltre possibile visualizzare alto `in: XXX` valori `TimeoutException` messaggi di errore, come descritto in hello [Burst di traffico](#burst-of-traffic) sezione.

> [!NOTE]
> Stackexchange 1.1.603 e successivamente inclusione hello `local-cpu` metrica in `TimeoutException` messaggi di errore. Verificare che si usa la versione più recente di hello di hello [pacchetto NuGet stackexchange. Redis](https://www.nuget.org/packages/StackExchange.Redis/). Sono presenti bug costantemente risolto in toomake codice hello tootimeouts più affidabile in modo che la versione più recente di hello è importante.
> 
> 

#### <a name="resolution"></a>Risoluzione
Aggiornare tooa VM dimensioni con più capacità di CPU o analizzare la causa picchi di CPU. 

### <a name="client-side-bandwidth-exceeded"></a>Larghezza di banda lato client superata
#### <a name="problem"></a>Problema
Esistono limitazioni alla quantità di larghezza di banda disponibile per computer client con dimensioni diverse. Se il client hello supera hello larghezza di banda disponibile, quindi dati non verranno elaborati sul lato client hello rapidamente server hello invio. Questo può causare tootimeouts.

#### <a name="measurement"></a>Misura
Monitorare il cambiamento dell'utilizzo della larghezza di banda nel corso del tempo usando un codice [come questo](https://github.com/JonCole/SampleCode/blob/master/BandWidthMonitor/BandwidthLogger.cs). Si noti che non è possibile eseguire correttamente questo codice in alcuni ambienti con autorizzazioni con restrizioni (ad esempio, i siti Web Azure).

#### <a name="resolution"></a>Risoluzione
Aumentare le dimensioni della VM client o ridurre il consumo di larghezza di banda di rete.

### <a name="large-requestresponse-size"></a>Dimensioni elevate della richiesta/risposta
#### <a name="problem"></a>Problema
Una richiesta/risposta di grandi dimensioni può causare un timeout. Si supponga, ad esempio, che il valore di timeout configurato nel client sia di 1 secondo. L'applicazione richiede due chiavi, ad esempio 'A' e 'B') in hello contemporaneamente (utilizzando hello stessa connessione di rete fisica). La maggior parte dei client supportano "Pipelining" delle richieste, tale che entrambe le richieste 'A' e 'B' vengono inviate sul server di toohello transito hello uno hello altri senza attendere che le risposte hello. Hello server invierà le risposte hello nuovamente hello stesso ordine. Se la risposta 'A' è di grandi dimensioni è sufficientemente può influire notevolmente la maggior parte dei timeout hello per le richieste successive. 

Hello di esempio seguente viene illustrato questo scenario. In questo scenario, 'A' e 'B' inviati rapidamente, server hello inizia a inviare rapidamente le risposte 'A' e 'B', ma a causa di tempi di trasferimento di dati, 'B' improvvisi dietro richiesta hello altri richiesta e verifica il timeout, anche se il server di hello ha risposto rapidamente.

    |-------- 1 Second Timeout (A)----------|
    |-Request A-|
         |-------- 1 Second Timeout (B) ----------|
         |-Request B-|
                |- Read Response A --------|
                                           |- Read Response B-| (**TIMEOUT**)



#### <a name="measurement"></a>Misura
Si tratta di un difficile uno toomeasure. È fondamentalmente tooinstrument le richieste di grandi dimensioni tootrack codice client e le risposte. 

#### <a name="resolution"></a>Risoluzione
1. Redis è ottimizzato per molti valori bassi, invece che per pochi valori elevati. Hello preferito soluzione è toobreak backup dei dati in valori più piccoli correlati. Vedere hello [che cos'è l'intervallo di dimensioni hello valore ideale per redis? e se 100 KB sono troppi](https://groups.google.com/forum/#!searchin/redis-db/size/redis-db/n7aa2A4DZDs/3OeEPHSQBAAJ) per una spiegazione dettagliata del perché siano preferibili valori più bassi.
2. Aumentare le dimensioni di hello della macchina virtuale (per client e Server di Cache Redis), funzionalità della larghezza di banda superiore tooget, riduzione dei dati dei tempi per le risposte di dimensioni maggiori di trasferimento. Si noti che quando si ottiene maggiore larghezza di banda solo i server hello o ma solo sui client hello potrebbe non essere sufficiente. Misura l'utilizzo della larghezza di banda e lo confronterà toohello funzionalità delle dimensioni di hello della macchina virtuale è installata.
3. Aumentare il numero di hello di `ConnectionMultiplexer` oggetti utilizzo e le richieste di round robin su diverse connessioni.

### <a name="what-happened-toomy-data-in-redis"></a>Quali dati toomy verificato anomalo in Redis?
#### <a name="problem"></a>Problema
Previsti per alcuni dati toobe nell'istanza Cache Redis di Azure ma problemi toobe non esiste.

#### <a name="resolution"></a>Risoluzione
Vedere [quali dati toomy verificato anomalo in Redis?](https://gist.github.com/JonCole/b6354d92a2d51c141490f10142884ea4#file-whathappenedtomydatainredis-md) per le possibili cause e risoluzioni.

## <a name="server-side-troubleshooting"></a>Risoluzione dei problemi lato server
In questa sezione vengono illustrati i problemi di risoluzione dei problemi che si verificano a causa di una condizione nel server di cache di hello.

* [Utilizzo della memoria nei server hello](#memory-pressure-on-the-server)
* [Utilizzo della CPU/carico del server elevato](#high-cpu-usage-server-load)
* [Larghezza di banda lato server superata](#server-side-bandwidth-exceeded)

### <a name="memory-pressure-on-hello-server"></a>Utilizzo della memoria nei server hello
#### <a name="problem"></a>Problema
Richieste di memoria sul lato server hello lead tooall tipi di problemi di prestazioni che possono ritardare l'elaborazione delle richieste. Quando viene rilevato l'utilizzo della memoria, il sistema hello include in genere toopage dati dalla memoria toovirtual di memoria fisica che si trova su disco. Questo *generare un errore di pagina* cause hello sistema tooslow verso il basso in modo significativo. Le possibili cause di questo utilizzo elevato di memoria sono diverse: 

1. La capacità di toofull della cache di hello contenente dati. 
2. Redis visualizzi la frammentazione della memoria elevata - spesso causati da archiviare gli oggetti di grandi dimensioni (Redis è ottimizzato per oggetti di piccole dimensioni, vedere hello [che cos'è l'intervallo di dimensioni hello valore ideale per redis? e se 100 KB sono troppi](https://groups.google.com/forum/#!searchin/redis-db/size/redis-db/n7aa2A4DZDs/3OeEPHSQBAAJ) per i dettagli. 

#### <a name="measurement"></a>Misura
Redis espone due metriche che consentono di identificare questo problema. viene innanzitutto Hello `used_memory` e altri hello è `used_memory_rss`. [Queste metriche](cache-how-to-monitor.md#available-metrics-and-reporting-intervals) sono disponibili nel portale di Azure hello o tramite hello [Redis INFO](http://redis.io/commands/info) comando.

#### <a name="resolution"></a>Risoluzione
Esistono diverse possibili modifiche che è possibile rendere toohelp utilizzo della memoria di mantenere integri:

1. [Configurare un criterio per la memoria](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) e impostare scadenze per le chiavi. Si noti che questa risoluzione potrebbe non essere sufficiente in caso di frammentazione.
2. [Configurare un valore riservato maxmemory](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) che è sufficiente toocompensate per la frammentazione della memoria.
3. Suddividere gli oggetti di grandi dimensioni memorizzati nella cache in oggetti correlati più piccoli.
4. [Scala](cache-how-to-scale.md) tooa dimensioni della cache.
5. Se si utilizza un [cache premium con cluster Redis abilitato](cache-how-to-premium-clustering.md) è possibile [aumentare hello numero di partizioni](cache-how-to-premium-clustering.md#change-the-cluster-size-on-a-running-premium-cache).

### <a name="high-cpu-usage--server-load"></a>Utilizzo della CPU/carico del server elevato
#### <a name="problem"></a>Problema
Utilizzo elevato della CPU può significare che lato client hello può avere esito negativo di una risposta da Redis in modo tempestivo tooprocess anche se Redis inviata risposta hello molto rapidamente.

#### <a name="measurement"></a>Misura
Hello monitor utilizzo CPU a livello di sistema tramite il portale di Azure hello o hello associati contatore delle prestazioni. Prestare attenzione non toomonitor *processo* CPU hello stesso poiché un singolo processo può avere un basso utilizzo della CPU nel tempo che il sistema complessivo della CPU può essere elevato. Cercare nell'utilizzo della CPU i picchi corrispondenti ai timeout.

#### <a name="resolution"></a>Risoluzione
[Scala](cache-how-to-scale.md) tooa cache di dimensioni maggiori livelli con più capacità di CPU o analizzare la causa picchi di CPU. 

### <a name="server-side-bandwidth-exceeded"></a>Larghezza di banda lato server superata
#### <a name="problem"></a>Problema
Esistono limitazioni alla quantità di larghezza di banda disponibile per le istanze della cache con dimensioni diverse. Se il server di hello supera la larghezza di banda disponibile hello, quindi dati non verrà inviati toohello client più rapidamente. Questo può causare tootimeouts.

#### <a name="measurement"></a>Misura
È possibile monitorare hello `Cache Read` metrica, ovvero hello quantità dei dati letti dalla cache di hello in megabyte al secondo (MB/s) durante l'intervallo di reporting specificato hello. Questo valore corrisponde toohello larghezza di banda utilizzata da questa cache. Se si desidera tooset di avvisi per i limiti della larghezza di banda di rete sul lato server, è possibile crearli utilizzando questo `Cache Read` contatore. Confrontare i valori letti con i valori hello in [questa tabella](cache-faq.md#cache-performance) per hello osservato i limiti di larghezza di banda per vari cache prezzi livelli e dimensioni.

#### <a name="resolution"></a>Risoluzione
Se si è in modo coerente in prossimità di hello osservato larghezza di banda massima per la dimensione della cache e di livello dei prezzi, prendere in considerazione [scalabilità](cache-how-to-scale.md) tooa prezzi livello o le dimensioni che sono maggiore della larghezza di banda di rete, utilizzando i valori hello in [questatabella](cache-faq.md#cache-performance) come guida.

## <a name="stackexchangeredis-timeout-exceptions"></a>Eccezioni di timeout di StackExchange.Redis
StackExchange.Redis usa un'impostazione di configurazione denominata `synctimeout` per le operazioni sincrone, che ha un valore predefinito di 1000 ms. Se una chiamata sincrona non completata nel tempo, hello Stackexchange client genera hello stipulata toohello simile un timeout di errore riportato di seguito.

    System.TimeoutException: Timeout performing MGET 2728cc84-58ae-406b-8ec8-3f962419f641, inst: 1,mgr: Inactive, queue: 73, qu=6, qs=67, qc=0, wr=1/1, in=0/0 IOCP: (Busy=6, Free=999, Min=2,Max=1000), WORKER (Busy=7,Free=8184,Min=2,Max=8191)


Questo messaggio di errore contiene le metriche che consentono di indicare toohello cause e possibili la risoluzione del problema hello. Hello nella tabella seguente contiene dettagli su Metrica messaggio di errore hello.

| Metrica del messaggio di errore | Dettagli |
| --- | --- |
| inst |Nell'ultimo intervallo di tempo hello: 0 comandi rilasciati. |
| mgr |esecuzione di gestione di socket Hello `socket.select` vale a dire che richiede hello del sistema operativo tooindicate un socket che ha un elemento toodo; fondamentalmente: lettore hello è attivamente la lettura dalla rete hello perché non possa qualcosa toodo |
| coda |In totale sono in corso 73 operazioni. |
| qu |6 di operazioni in corso di hello presenti nella coda non inviati hello e non sono ancora state scritte toohello di rete in uscita |
| qs |67 operazioni in corso he sono stati inviati toohello server ma una risposta non è ancora disponibile. Hello risposta potrebbe essere `Not yet sent by hello server` o`sent by hello server but not yet processed by hello client.` |
| qc |0 di operazioni in corso di hello sono visualizzate le risposte, ma non sono ancora stati contrassegnati come completati a causa di toowaiting nel ciclo di completamento hello |
| wr |È un writer attivo (vale a dire hello 6 richieste non inviate non vengono ignorati) byte/activewriters |
| iniziare |Nessun lettore active e zero byte sono disponibili toobe leggere hello NIC byte/activereaders |

### <a name="steps-tooinvestigate"></a>Passaggi tooinvestigate
1. Come consigliabile verificare che si sta utilizzando hello seguente tooconnect modello quando si utilizza client stackexchange. Redis hello.

    ```c#
    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        return ConnectionMultiplexer.Connect("cachename.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");
    
    });
    
    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }
    ````

    Per ulteriori informazioni, vedere [connettersi cache toohello utilizzando stackexchange. Redis](cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-the-cache).

1. Verificare che la Cache Redis di Azure e l'applicazione client hello hello stessa area in Azure. Ad esempio, è possibile che venga timeout quando la cache è negli Stati Uniti orientali ma hello client si trova in Stati Uniti occidentali e hello richiesta non completata entro hello `synctimeout` intervallo o è possibile che venga timeout quando si esegue il debug dal computer di sviluppo locale. 
   
    È consigliabile toohave cache di hello e client hello in hello stessa regione di Azure. Se si dispone di uno scenario che include le chiamate tra aree, è necessario impostare hello `synctimeout` valore tooa dell'intervallo superiore hello predefinito 1000 ms intervallo includendo un `synctimeout` proprietà nella stringa di connessione hello. Hello esempio seguente viene illustrato un frammento di stringa connessione della cache stackexchange. Redis con un `synctimeout` di 2000 ms.
   
        synctimeout=2000,cachename.redis.cache.windows.net,abortConnect=false,ssl=true,password=...
2. Verificare che si usa la versione più recente di hello di hello [pacchetto NuGet stackexchange. Redis](https://www.nuget.org/packages/StackExchange.Redis/). Sono presenti bug costantemente risolto in toomake codice hello tootimeouts più affidabile in modo che la versione più recente di hello è importante.
3. Se sono presenti richieste di recupero associate di limitazioni della larghezza di banda nel client o server hello, richiederà più tempo per tali toocomplete e pertanto provocare il timeout. toosee se il timeout di scadenza della larghezza di banda toonetwork nel server di hello, vedere [larghezza di banda di lato Server superato](#server-side-bandwidth-exceeded). toosee se il timeout di scadenza tooclient larghezza di banda, vedere [larghezza di banda di lato Client superato](#client-side-bandwidth-exceeded).
4. È il recupero della CPU associati nel server di hello o nel client hello?
   
   * Verificare se sono Guida associate alla CPU nel client che potrebbero causare hello richiesta toonot elaborato all'interno di hello `synctimeout` intervallo, causando un timeout. Lo spostamento tooa dimensioni client o distribuzione del carico hello consente toocontrol questo. 
   * Verificare se si riceve una CPU associata hello server monitorando hello `CPU` [memorizzare nella cache di misurazione delle prestazioni](cache-how-to-monitor.md#available-metrics-and-reporting-intervals). Delle richieste in entrata mentre Redis è sulla CPU può causare richieste tootimeout. tooaddress questo è possibile distribuire hello il carico tra più partizioni in una cache premium o l'aggiornamento di dimensioni maggiori di tooa o livello di prezzo. Per altre informazioni, vedere [Larghezza di banda lato server superata](#server-side-bandwidth-exceeded).
5. Sono presenti comandi richiede molto tempo tooprocess sul server hello? I comandi che richiedono molto tempo tooprocess sul server di redis hello a esecuzione prolungata può provocare il timeout. Alcuni esempi di comandi con esecuzione di lunga durata sono `mget` con numeri di chiave elevati, `keys *` o script lua scritti in modo inadeguato. È possibile connettere tooyour istanza di Cache Redis di Azure tramite client redis-cli hello o usare hello [Console Redis](cache-configure.md#redis-console) esecuzione hello e [SlowLog](http://redis.io/commands/slowlog) toosee comando se sono presenti richieste richiede più tempo del previsto. Il server Redis e StackExchange.Redis sono ottimizzati per numerose richieste di piccole dimensioni invece che per meno richieste di grandi dimensioni. Dividere i dati in blocchi più piccoli può facilitare le operazioni. 
   
    Per informazioni sulla connessione dell'endpoint di Azure Redis Cache SSL toohello tramite redis-cli e stunnel, vedere hello [annuncio i Provider di stato sessione ASP.NET per la versione di anteprima Redis](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx) post di blog. Per altre informazioni, vedere [SlowLog](http://redis.io/commands/slowlog).
6. Un carico del server Redis elevato può causare timeout. È possibile monitorare hello del carico del server di monitoraggio hello `Redis Server Load` [memorizzare nella cache di misurazione delle prestazioni](cache-how-to-monitor.md#available-metrics-and-reporting-intervals). Un carico del server di 100 (valore massimo) indica che il server redis hello è impegnato a, con alcun tempo di inattività, l'elaborazione delle richieste. toosee se alcune richieste occupano le funzionalità server hello, eseguire il comando di SlowLog hello, come descritto nel paragrafo precedente hello. Per altre informazioni, vedere [Utilizzo della CPU/carico del server elevato](#high-cpu-usage-server-load).
7. Era presente qualsiasi altro evento sul lato client hello che hanno causato un acustico rete? Controllare se si è verificato un evento come scalabilità numero hello di istanze di client verso l'alto o verso il basso o distribuire una nuova versione del client hello client hello (web, ruolo di lavoro o una VM Iaas) o scalabilità automatica è abilitata? Durante il test che è stato rilevato che può causare la scalabilità automatica o scalabile su/giù può essere persa la connettività di rete in uscita per alcuni secondi. Codice di stackexchange. Redis è toosuch resilienti eventi e si riconnetterà. Durante l'operazione di riconnessione tutte le richieste in coda hello può causare il timeout.
8. Era presente una richiesta di grande precedente più richieste di piccole dimensioni toohello Cache Redis timeout? parametro Hello `qs` in errore hello messaggio indica il numero di richieste inviato dal server di hello client toohello, ma non è ancora stato elaborato una risposta. Questo valore può continuare ad aumentare perché StackExchange.Redis usa una sola connessione TCP e può leggere solo una risposta per volta. Anche se i timeout dell'operazione prima di hello, ma non interrompe i dati di hello inviati da e verso server hello e altre richieste vengono bloccate fino al termine, causando timeout. Una soluzione è il possibilità hello toominimize di timeout per garantire che la cache è sufficientemente grande per il carico di lavoro e la suddivisione dei valori di grandi dimensioni in blocchi più piccoli. Un'altra possibile soluzione è toouse un pool di `ConnectionMultiplexer` oggetti nel client e di scegliere hello minor caricata `ConnectionMultiplexer` durante l'invio di una nuova richiesta. Questo deve impedire un unico timeout a causa di timeout di tooalso altre richieste.
9. Se si utilizza `RedisSessionStateprovider`, verificare che sia stata impostata correttamente i timeout dei tentativi hello. `retrytimeoutInMilliseconds` deve essere maggiore di `operationTimeoutinMilliseonds`. In caso contrario, non verranno effettuati nuovi tentativi. Nell'esempio seguente hello `retrytimeoutInMilliseconds` è impostato too3000. Per ulteriori informazioni, vedere [Provider di stato sessione ASP.NET per Cache Redis di Azure](cache-aspnet-session-state-provider.md) e [come toouse hello parametri di configurazione di Provider di stato della sessione e il Provider di Cache di Output](https://github.com/Azure/aspnet-redis-providers/wiki/Configuration).

    <add
      name="AFRedisCacheSessionStateProvider"
      type="Microsoft.Web.Redis.RedisSessionStateProvider"
      host="enbwcache.redis.cache.windows.net"
      port="6380"
      accessKey="…"
      ssl="true"
      databaseId="0"
      applicationName="AFRedisCacheSessionState"
      connectionTimeoutInMilliseconds = "5000"
      operationTimeoutInMilliseconds = "1000"
      retryTimeoutInMilliseconds="3000" />


1. Controllare l'utilizzo della memoria nel server di Cache Redis di Azure hello [monitoraggio](cache-how-to-monitor.md#available-metrics-and-reporting-intervals) `Used Memory RSS` e `Used Memory`. Se un criterio di eliminazione è in uso, Redis avvia la rimozione di chiavi quando `Used_Memory` raggiunge la dimensione della cache di hello. Idealmente, `Used Memory RSS` deve essere solo di poco più elevato di `Used memory`. Una grande differenza indica la frammentazione della memoria (interna o esterna). Quando `Used Memory RSS` è minore di `Used Memory`, significa che è state invertite parte della memoria cache di hello dal sistema operativo hello. In questo caso, possono verificarsi alcune latenze significative. Poiché Redis non abbia il controllo come le allocazioni vengono mappati toomemory pagine, elevate `Used Memory RSS` risulta spesso hello un picco nell'utilizzo della memoria. Quando Redis libera la memoria, memoria hello viene nuovamente toohello allocatore e allocatore hello può o non offra hello memoria toohello indietro sistema. Può essere presente una discrepanza tra hello `Used Memory` consumo di memoria e di valore come riportato dal sistema operativo hello. Potrebbe essere dovuto toohello fatti memoria è stata utilizzata e rilasciata da Redis, ma non specificato sistema back-toohello. toohelp limitare i problemi di memoria è possibile eseguire hello alla procedura seguente.
   
   * Eseguire l'aggiornamento di dimensioni maggiori tooa cache di hello in modo che non vengono eseguiti con limiti di memoria nel sistema hello.
   * Impostare date di scadenza su chiavi hello in modo che i valori precedenti vengono eliminati in modo proattivo.
   * Hello hello monitoraggio `used_memory_rss` memorizzare nella cache di metrica. Quando questo valore si avvicina dimensioni hello di cache, si è probabilmente toostart visualizzare i problemi di prestazioni. Distribuire i dati di hello tra più partizioni, se si usa una cache premium, o aggiornare tooa dimensioni della cache.
   
   Per ulteriori informazioni, vedere [utilizzo della memoria nei server hello](#memory-pressure-on-the-server).

## <a name="additional-information"></a>Informazioni aggiuntive
* [Quali offerte e dimensioni della Cache Redis è consigliabile usare?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)
* [Come è possibile effettuare un benchmark e testare le prestazioni della cache di hello?](cache-faq.md#how-can-i-benchmark-and-test-the-performance-of-my-cache)
* [Come si eseguono i comandi Redis?](cache-faq.md#how-can-i-run-redis-commands)
* [La modalità di Cache Redis di Azure di toomonitor](cache-how-to-monitor.md)

