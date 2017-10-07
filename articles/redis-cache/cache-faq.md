---
title: domande frequenti di Cache Redis aaaAzure | Documenti Microsoft
description: Informazioni su hello le risposte alle domande toocommon, i modelli e procedure consigliate per Cache Redis di Azure
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: c2c52b7d-b2d1-433a-b635-c20180e5cab2
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: sdanie
ms.openlocfilehash: 2c6ed2f65f755bd08f04857b7af31f520cf4f158
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-redis-cache-faq"></a>Domande frequenti sulla Cache Redis di Azure
Informazioni su hello risponde alle domande toocommon, modelli e procedure consigliate per Cache Redis di Azure.

## <a name="what-if-my-question-isnt-answered-here"></a>Cosa fare se non è disponibile una risposta alla domanda?
Se la domanda non è elencata qui, invitiamo gli utenti a comunicarcela per consentirci di fornire il nostro aiuto.

* È possibile pubblicare una domanda nei commenti hello alla fine di hello di queste domande frequenti e contattare il team di Cache di Azure hello e altri membri della community su questo articolo.
* tooreach un gruppo di destinatari più ampio, è possibile inserire una domanda hello [Forum MSDN di Azure Cache](https://social.msdn.microsoft.com/forums/azure/home?forum=azurecache) e contattare il team di Cache di Azure hello e altri membri della Comunità hello.
* Se si desidera toomake una richiesta di funzionalità, è possibile inviare le richieste e idee troppo[Azure Redis Cache utente vocale](https://feedback.azure.com/forums/169382-cache).
* È anche possibile inviare un messaggio di posta elettronica toous in [Feedback esterno della Cache di Azure](mailto:azurecache@microsoft.com).

## <a name="azure-redis-cache-basics"></a>Informazioni di base sulla Cache Redis di Azure
Hello domande frequenti in questa sezione illustra alcuni concetti di base di hello della Cache Redis di Azure.

* [Informazioni su Cache Redis di Azure](#what-is-azure-redis-cache)
* [Come si procede per iniziare a usare Cache Redis di Azure?](#how-can-i-get-started-with-azure-redis-cache)

Hello domande frequenti seguenti illustrano i concetti di base e domande sulla Cache Redis di Azure e sono disponibili in uno dei hello altre sezioni di domande frequenti.

* [Quali offerte e dimensioni della Cache Redis è consigliabile usare?](#what-redis-cache-offering-and-size-should-i-use)
* [Quali client della cache Redis è possibile usare?](#what-redis-cache-clients-can-i-use)
* [Esiste un emulatore locale per la cache Redis di Azure?](#is-there-a-local-emulator-for-azure-redis-cache)
* [Come monitorare hello integrità e le prestazioni di my cache?](#how-do-i-monitor-the-health-and-performance-of-my-cache)

## <a name="planning-faqs"></a>Domande frequenti sulla pianificazione
* [Quali offerte e dimensioni della Cache Redis è consigliabile usare?](#what-redis-cache-offering-and-size-should-i-use)
* [Prestazioni di Cache Redis di Azure](#azure-redis-cache-performance)
* [In quale area è consigliabile posizionare la cache?](#in-what-region-should-i-locate-my-cache)
* [Quali sono i costi addebitati per Cache Redis di Azure?](#how-am-i-billed-for-azure-redis-cache)
* [È possibile usare Cache Redis di Azure con Azure Government Cloud, Azure China Cloud o Microsoft Azure Germania?](#can-i-use-azure-redis-cache-with-azure-government-cloud-azure-china-cloud-or-microsoft-azure-germany)

## <a name="development-faqs"></a>Domande frequenti sullo sviluppo
* [In che modo le opzioni di configurazione stackexchange. Redis hello?](#what-do-the-stackexchangeredis-configuration-options-do)
* [Quali client della cache Redis è possibile usare?](#what-redis-cache-clients-can-i-use)
* [Esiste un emulatore locale per la cache Redis di Azure?](#is-there-a-local-emulator-for-azure-redis-cache)
* [Come si eseguono i comandi Redis?](#how-can-i-run-redis-commands)
* [Perché non Cache Redis di Azure è presente un riferimento alla libreria di classe MSDN per alcune hello altri servizi di Azure?](#why-doesnt-azure-redis-cache-have-an-msdn-class-library-reference-like-some-of-the-other-azure-services)
* [Posso utilizzare Cache Redis di Azure come una cache di sessione PHP?](#can-i-use-azure-redis-cache-as-a-php-session-cache)
* [Cosa sono i database Redis?](#what-are-redis-databases)

## <a name="security-faqs"></a>Domande frequenti sulla sicurezza
* [Quando è necessario attivare la porta non SSL hello per la connessione tooRedis?](#when-should-i-enable-the-non-ssl-port-for-connecting-to-redis)

## <a name="production-faqs"></a>Domande frequenti sulla produzione
* [Quali sono alcune procedure consigliate per la produzione?](#what-are-some-production-best-practices)
* [Quando si usano i comandi di Redis più comuni, quali sono alcune considerazioni sull'hello?](#what-are-some-of-the-considerations-when-using-common-redis-commands)
* [Come è possibile effettuare un benchmark e testare le prestazioni della cache di hello?](#how-can-i-benchmark-and-test-the-performance-of-my-cache)
* [Informazioni importanti sulla crescita del pool di thread](#important-details-about-threadpool-growth)
* [Abilitare una velocità effettiva maggiore sul client hello tooget GC server quando si utilizza stackexchange. Redis](#enable-server-gc-to-get-more-throughput-on-the-client-when-using-stackexchangeredis)
* [Considerazioni sulle prestazioni per le connessioni](#performance-considerations-around-connections)

## <a name="monitoring-and-troubleshooting-faqs"></a>Domande sul monitoraggio e sulla risoluzione dei problemi
Hello domande frequenti in questa sezione copertura comuni di monitoraggio e risoluzione dei problemi di domande. Per ulteriori informazioni sul monitoraggio e risoluzione dei problemi di istanze di Cache Redis di Azure, vedere [la modalità di Cache Redis di Azure di toomonitor](cache-how-to-monitor.md) e [la modalità di Cache Redis di Azure di tootroubleshoot](cache-how-to-troubleshoot.md).

* [Come monitorare hello integrità e le prestazioni di my cache?](#how-do-i-monitor-the-health-and-performance-of-my-cache)
* [Perché vengono visualizzati timeout?](#why-am-i-seeing-timeouts)
* [Motivo per cui il client è stata disconnessa dalla cache di hello?](#why-was-my-client-disconnected-from-the-cache)

## <a name="prior-cache-offering-faqs"></a>Domande frequenti sulle offerte di Cache precedenti
* [Qual è l'offerta di Cache di Azure più adatta alle mie esigenze?](#which-azure-cache-offering-is-right-for-me)

### <a name="what-is-azure-redis-cache"></a>Informazioni su Cache Redis di Azure
Cache Redis di Azure si basa sull'open-source comuni hello [cache Redis](http://redis.io). Consente di accedere a tooa sicura e dedicata cache Redis, gestita da Microsoft e accessibile da qualsiasi applicazione in Azure. Per informazioni più dettagliate, vedere hello [Cache Redis di Azure](https://azure.microsoft.com/services/cache/) pagina del prodotto su Azure.com.

### <a name="how-can-i-get-started-with-azure-redis-cache"></a>Come si procede per iniziare a usare Cache Redis di Azure?
Esistono diversi modi per iniziare a usare Cache Redis di Azure.

* È possibile eseguire una delle esercitazioni disponibili per [.NET](cache-dotnet-how-to-use-azure-redis-cache.md), [ASP.NET](cache-web-app-howto.md), [Java](cache-java-get-started.md), [Node.js](cache-nodejs-get-started.md) e [Python](cache-python-get-started.md).
* È possibile guardare [come tooBuild ad alte prestazioni App utilizzando Microsoft Cache Redis di Azure](https://azure.microsoft.com/documentation/videos/how-to-build-high-performance-apps-using-microsoft-azure-cache/).
* È possibile leggere la documentazione di hello client per i client hello che corrispondono a linguaggio di sviluppo hello di toosee il progetto come toouse Redis. Esistono molti client Redis che possono essere utilizzati con Cache Redis di Azure. Per un elenco dei client Redis, vedere [http://redis.io/clients](http://redis.io/clients).

Se non si dispone di un account Azure, è possibile:

* [Aprire un account Azure gratuitamente](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero): È possibile ottenere crediti che possono essere utilizzati tootry out a pagamento di servizi di Azure. Anche dopo hello crediti, è possibile tenere conto di hello e utilizzare le funzionalità e servizi di Azure gratuiti.
* [Attivare i vantaggi della sottoscrizione Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero). con l'abbonamento MSDN ogni mese si accumulano crediti che è possibile usare per i servizi di Azure a pagamento.

<a name="cache-size"></a>

### <a name="what-redis-cache-offering-and-size-should-i-use"></a>Quali offerte e dimensioni della Cache Redis è consigliabile usare?
Ogni offerta della Cache Redis di Azure fornisce livelli diversi per le opzioni relative a **dimensioni**, **larghezza di banda**, **disponibilità elevata** e **Contratto di servizio**.

di seguito Hello sono considerazioni per la scelta di un'offerta di Cache.

* **Memoria**: livelli Basic e Standard di hello offrono 250 MB-53 GB. livello di Hello Premium offre too530 GB. Per altre informazioni, vedere [Prezzi di Cache Redis di Azure](https://azure.microsoft.com/pricing/details/cache/).
* **Prestazioni di rete**: se si dispone di un carico di lavoro che richiede una velocità effettiva elevata, livello Premium hello offre più larghezza di banda rispetto tooStandard o Basic. All'interno di ogni livello, anche le cache di dimensioni più grandi hanno maggiore larghezza di banda a causa di hello sottostante macchina virtuale che ospita la cache di hello. Vedere hello [seguenti tabella](#cache-performance) per ulteriori informazioni.
* **Velocità effettiva**: livello Premium hello offre hello disponibile la velocità effettiva massima. Se il client o server di cache di hello raggiunge i limiti di larghezza di banda hello, si potrebbe ricevere timeout sul lato client hello. Per ulteriori informazioni, vedere hello nella tabella seguente.
* **Elevata disponibilità/SLA**: Cache Redis di Azure garantisce che una cache Standard o Premium è disponibile almeno il 99,9% del tempo di hello. toolearn ulteriori informazioni su questo contratto di servizio, vedere [Azure Redis Cache prezzi](https://azure.microsoft.com/support/legal/sla/cache/v1_0/). contratto di servizio Hello descrive solo gli endpoint della Cache toohello di connettività. Hello contratto di servizio non viene descritta la protezione dalla perdita di dati. È consigliabile utilizzare funzionalità di persistenza dei dati Redis hello hello Premium livello tooincrease resilienza perdita di dati.
* **Persistenza dei dati redis**: livello Premium hello consente i dati nella cache di hello toopersist in un account di archiviazione di Azure. In una cache Basic/Standard, tutti i dati di hello viene archiviata solo in memoria. In caso di problemi per l'infrastruttura sottostante esiste il rischio di una potenziale perdita di dati. È consigliabile utilizzare funzionalità di persistenza dei dati Redis hello hello Premium livello tooincrease resilienza perdita di dati. Cache Redis di Azure offre le opzioni RDB e AOF (presto disponibile) per la persistenza di Redis. Per ulteriori informazioni, vedere [come persistenza tooconfigure per una Cache Redis di Azure Premium](cache-how-to-premium-persistence.md).
* **Cluster redis**: toocreate memorizza nella cache più grandi rispetto a 53 GB o tooshard dati tra più nodi di Redis, è possibile usare il clustering di Redis, disponibile nel livello Premium hello. Ogni nodo è costituito da una coppia di cache primaria/di replica per la disponibilità elevata. Per ulteriori informazioni, vedere [come tooconfigure clustering per una Cache Redis di Azure Premium](cache-how-to-premium-clustering.md).
* **Isolamento di rete e protezione avanzata**: distribuzione la rete virtuale di Azure (VNET) fornisce sicurezza avanzata e isolamento per Cache Redis di Azure, nonché le subnet, criteri di controllo di accesso e altre funzionalità toofurther limitare l'accesso. Per ulteriori informazioni, vedere [la modalità di supporto tooconfigure rete virtuale per una Cache Redis di Azure Premium](cache-how-to-premium-vnet.md).
* **Configurare Redis**: hello Standard e i livelli Premium, è possibile configurare Redis per le notifiche di spazio delle chiavi.
* **Numero massimo di connessioni client**: livello Premium hello offre numero massimo di hello del client in grado di connettersi tooRedis, con un numero elevato di connessioni per le cache di dimensioni più grandi. Per altre informazioni, vedere [Prezzi di Cache Redis di Azure](https://azure.microsoft.com/pricing/details/cache/).
* **Dedicato Core per Server Redis**: nel livello Premium hello, tutte le dimensioni della cache dispone di un core dedicato per Redis. Nei livelli Basic/Standard hello, hello dimensioni C1 e avere sopra un core dedicato per il server Redis.
* **Redis è a thread singolo** , la disponibilità di più di due core non offre vantaggi ulteriori rispetto alla disponibilità di soli due core, ma in genere dimensioni di macchina virtuale maggiori hanno una larghezza di banda più elevata rispetto alle dimensioni minori. Se il client o server di cache di hello raggiunge i limiti di larghezza di banda hello, verrà visualizzato timeout sul lato client hello.
* **Miglioramenti delle prestazioni**: cache di livello Premium hello vengono distribuiti in hardware con processori più veloci, dando migliori prestazioni rispetto toohello livello Basic o Standard. Le cache di livello Premium offrono una velocità effettiva più elevata e minori latenze.

<a name="cache-performance"></a>

### <a name="azure-redis-cache-performance"></a>Prestazioni di Cache Redis di Azure
Hello tabella seguente vengono illustrati i valori di larghezza di banda massima hello osservati durante il test di diverse dimensioni dello Standard e Premium memorizza nella cache utilizzando `redis-benchmark.exe` da una VM Iaas di endpoint di hello Cache Redis di Azure. 

>[!NOTE] 
>Questi valori non sono garantiti e che non è disponibile alcun contratto di servizio per questi numeri, che dovrebbero essere tuttavia tipici. È necessario caricare proprie dimensioni della cache adeguata hello toodetermine dell'applicazione per l'applicazione di test.
>
>

Da questa tabella, è possibile trarre hello seguenti conclusioni:

* Velocità effettiva per le cache hello hello stessa dimensione è maggiore di hello livello Premium come livello Standard toohello confrontati. Ad esempio, con una Cache di 6 GB, velocità effettiva di P1 è RPS 180.000 come too49 confrontati, 000 per C3.
* Con il clustering di Redis, aumento della velocità effettiva in modo lineare man mano che aumenta il numero di hello di partizioni (nodi) in cluster hello. Ad esempio, se si crea un cluster P4 di 10 partizioni, velocità effettiva disponibile hello è 400.000 * 10 = 4 milioni di RPS.
* Velocità effettiva per le dimensioni di chiave più grande è superiore nel livello Premium hello toohello confrontato livello Standard.

| Piano tariffario  | Dimensione | Core CPU | Larghezza di banda disponibile | Dimensioni del valore di 1 KB |
| --- | --- | --- | --- | --- |
| **Dimensioni della cache livello Standard** | | |**Megabit al secondo (Mb/s) / Megabyte al secondo (MB/s)** |**Richieste al secondo (RPS)** |
| C0 |250 MB |Condiviso |5 / 0,625 |600 |
| C1 |1 GB |1 |100 / 12,5 |12,200 |
| C2 |2,5 GB |2 |200 / 25 |24,000 |
| C3 |6 GB |4 |400 / 50 |49,000 |
| C4 |13 GB |2 |500 / 62,5 |61,000 |
| C5 |26 GB |4 |1,000 / 125 |115,000 |
| C6 |53 GB |8 |2,000 / 250 |150.000 |
| **Dimensioni della cache livello Premium** | |**Core CPU per partizione** | **Megabit al secondo (Mb/s) / Megabyte al secondo (MB/s)** |**Richieste al secondo (RPS) per partizione** |
| P1 |6 GB |2 |1,500 / 187.5 |180,000 |
| P2 |13 GB |4 |3,000 / 375 |360,000 |
| P3 |26 GB |4 |3,000 / 375 |360,000 |
| P4 |53 GB |8 |6,000 / 750 |400.000 |

Per istruzioni sul download hello Redis strumenti, ad esempio `redis-benchmark.exe`, vedere hello [come è possibile eseguire i comandi di Redis?](#cache-commands) sezione.

<a name="cache-region"></a>

### <a name="in-what-region-should-i-locate-my-cache"></a>In quale area è consigliabile posizionare la cache?
Per prestazioni ottimali e latenza più bassa, individuare la Cache Redis di Azure in hello stessa area dell'applicazione client della cache.

<a name="cache-billing"></a>

### <a name="how-am-i-billed-for-azure-redis-cache"></a>Quali sono i costi addebitati per Cache Redis di Azure?
I prezzi di Cache Redis di Azure sono indicati [qui](https://azure.microsoft.com/pricing/details/cache/) pagina dei prezzi Hello elenchi prezzi come una tariffa oraria. Le cache vengono fatturate con cadenza al minuto da ora hello hello cache viene creata finché non volta hello una cache viene eliminata. Non sono disponibili opzioni per l'arresto o sospensione fatturazione hello di una cache.

### <a name="can-i-use-azure-redis-cache-with-azure-government-cloud-azure-china-cloud-or-microsoft-azure-germany"></a>È possibile usare Cache Redis di Azure con Azure Government Cloud, Azure China Cloud o Microsoft Azure Germania?
Sì, è possibile usare Cache Redis di Azure con Azure Government Cloud, Azure China Cloud e Microsoft Azure Germania. URL di Hello per l'accesso e la gestione delle Cache Redis di Azure sono diversi in queste aree confrontati con Cloud pubblico di Azure. 

| Cloud   | Suffisso DNS per Redis            |
|---------|---------------------------------|
| Pubblico  | *.redis.cache.windows.net       |
| US Gov  | *.redis.cache.usgovcloudapi.net |
| Germania | *.redis.cache.cloudapi.de       |
| Cina   | *.redis.cache.chinacloudapi.cn  |

Per ulteriori informazioni su considerazioni sull'uso di Cache Redis di Azure con altri cloud, vedere hello seguenti collegamenti.

- [Database di Azure per enti pubblici - Cache Redis di Azure](../azure-government/documentation-government-services-database.md#azure-redis-cache)
- [Azure China Cloud - Cache Redis di Azure](https://www.azure.cn/documentation/services/redis-cache/)
- [Microsoft Azure Germania](https://azure.microsoft.com/overview/clouds/germany/)

Per informazioni sull'uso di Cache Redis di Azure con PowerShell in Azure per enti pubblici, Azure Cina Cloud e Microsoft Azure in Germania, vedere [come tooconnect tooother cloud - Azure Redis Cache PowerShell](cache-howto-manage-redis-cache-powershell.md#how-to-connect-to-other-clouds).

<a name="cache-configuration"></a>

### <a name="what-do-hello-stackexchangeredis-configuration-options-do"></a>In che modo le opzioni di configurazione stackexchange. Redis hello?
StackExchange.Redis include diverse opzioni. In questa sezione illustra alcune delle impostazioni comuni hello. Per informazioni più dettagliate sulle opzioni StackExchange.Redis, vedere la pagina relativa alla [configurazione di StackExchange.Redis](https://stackexchange.github.io/StackExchange.Redis/Configuration).

| Opzioni configurazione | Descrizione | Raccomandazione |
| --- | --- | --- |
| AbortOnConnectFail |Se impostato, tootrue connessione hello non si riconnetterà dopo un errore di rete. |Impostare toofalse e consente di riconnettersi automaticamente stackexchange. Redis. |
| ConnectRetry |numero Hello di tentativi toorepeat connessione iniziale durante la connessione. |Vedere hello note per linee guida seguenti. |
| ConnectTimeout |Timeout in millisecondi per le operazioni di connessione. |Vedere hello note per linee guida seguenti. |

In genere, i valori predefiniti di hello del client hello sono sufficienti. È possibile regolare le opzioni hello in base al carico di lavoro.

* **Tentativi**
  * Per ConnectRetry e ConnectTimeout, linee guida generali hello è toofail veloce e riprovare. Questa guida è basata sul carico di lavoro e il tempo in calcolarne la media accetta per il tooissue client un comando di Redis e ricevere una risposta.
  * Permettere la connessione automatica di StackExchange.Redis invece di controllare lo stato di connessione ed eseguire manualmente la riconnessione. **Evitare di usare proprietà ConnectionMultiplexer.IsConnected hello**.
  * Snowballing - in alcuni casi potrebbero verificarsi di un problema in cui Ritenta e hello ritenta l'errore mai eseguendo il ripristino. Se snowballing si verifica, è consigliabile utilizzare un algoritmo di backoff esponenziale tentativi, come descritto in [ripetere indicazioni generali](../best-practices-retry-general.md) pubblicati dal gruppo di Microsoft Patterns & Practices hello.
* **Valori di timeout**
  * Prendere in considerazione il carico di lavoro e impostare di conseguenza i valori hello. Se si archiviano i valori di grandi dimensioni, è possibile impostare valore più alto di hello timeout tooa.
  * Impostare `AbortOnConnectFail` toofalse e stackexchange. Redis riconnettersi automaticamente.
  * Utilizzare una singola istanza ConnectionMultiplexer per un'applicazione hello. È possibile utilizzare un toocreate LazyConnection una singola istanza restituito da una proprietà di connessione, come illustrato nella [connettersi toohello cache utilizzando una classe ConnectionMultiplexer hello](cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-the-cache).
  * Set hello `ConnectionMultiplexer.ClientName` proprietà tooan app istanza nome univoco per scopi diagnostici.
  * Usare più istanze di `ConnectionMultiplexer` per carichi di lavoro personalizzati.
      * È possibile seguire questo modello se l'applicazione include carichi variabili. Ad esempio:
      * È possibile avere un multiplexer per la gestione di chiavi di grandi dimensioni.
      * È possibile avere un multiplexer per la gestione di chiavi di piccole dimensioni.
      * È possibile impostare valori diversi per i timeout di connessione e la logica di ripetizione dei tentativi per ogni ConnectionMultiplexer usato.
      * Set hello `ClientName` proprietà ogni toohelp multiplexer, con la diagnostica.
      * Questa guida può causare latenza toomore semplificata per `ConnectionMultiplexer`.

### <a name="what-redis-cache-clients-can-i-use"></a>Quali client della cache Redis è possibile usare?
Uno dei principali vantaggi di hello di Redis è vi sono molti i client che supportano molti linguaggi di sviluppo diversi. Per un elenco aggiornato dei client, vedere l'articolo relativo ai [client Redis](http://redis.io/clients). Per le esercitazioni che illustrano diverse lingue e i client, vedere [la modalità di Cache Redis di Azure di toouse](cache-dotnet-how-to-use-azure-redis-cache.md) e fare clic su una lingua hello desiderato da Selezione lingua hello nella parte superiore di hello dell'articolo hello.

[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

<a name="cache-emulator"></a>

### <a name="is-there-a-local-emulator-for-azure-redis-cache"></a>Esiste un emulatore locale per la cache Redis di Azure?
Non vi è alcun emulatore locale per Cache Redis di Azure, ma è possibile eseguire una versione di hello MSOpenTech di redis server.exe da hello [Redis strumenti da riga di comando](https://github.com/MSOpenTech/redis/releases/) locale del computer e connettersi tooit tooget una cache locale di tooa esperienze simili emulatore, come illustrato nell'esempio seguente hello:

    private static Lazy<ConnectionMultiplexer>
          lazyConnection = new Lazy<ConnectionMultiplexer>
        (() =>
        {
            // Connect tooa locally running instance of Redis toosimulate a local cache emulator experience.
            return ConnectionMultiplexer.Connect("127.0.0.1:6379");
        });

        public static ConnectionMultiplexer Connection
        {
            get
            {
                return lazyConnection.Value;
            }
        }


È possibile configurare un [conf](http://redis.io/topics/config) toomore file corrisponde strettamente hello [impostazioni cache predefinite](cache-configure.md#default-redis-server-configuration) per la Cache Redis online Azure se lo si desidera.

<a name="cache-commands"></a>

### <a name="how-can-i-run-redis-commands"></a>Come si eseguono i comandi Redis?
È possibile utilizzare i comandi di hello elencati in [Redis comandi](http://redis.io/commands#) ad eccezione dei comandi di hello elencati in [comandi non supportati in Cache Redis di Azure Redis](cache-configure.md#redis-commands-not-supported-in-azure-redis-cache). Si dispone di comandi di Redis toorun opzioni diverse.

* Se si dispone di una cache Standard o Premium, è possibile eseguire i comandi di Redis usando hello [Console Redis](cache-configure.md#redis-console). console Redis Hello fornisce un toorun in modo sicuro i comandi di Redis nel portale di Azure hello.
* È anche possibile utilizzare strumenti da riga di comando di hello Redis. toouse, eseguire hello i passaggi seguenti:
* Scaricare hello [Redis strumenti da riga di comando](https://github.com/MSOpenTech/redis/releases/).
* Connettersi usando cache toohello `redis-cli.exe`. Passare a endpoint della cache di hello utilizzando l'opzione -h hello e chiave di hello utilizzando-come illustrato nell'esempio seguente hello:
* `redis-cli -h <your cache="" name="">
  .redis.cache.windows.net -a <key>
  `

> [!NOTE]
> Hello strumenti da riga di comando Redis non funzionano con hello porta SSL, ma è possibile utilizzare un'utilità, ad esempio `stunnel` toosecurely connettersi porta SSL di hello strumenti toohello seguendo le direzioni di hello in hello [annuncio i Provider di stato sessione ASP.NET per Versione di anteprima di redis](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx) post di blog.
>
>

<a name="cache-reference"></a>

### <a name="why-doesnt-azure-redis-cache-have-an-msdn-class-library-reference-like-some-of-hello-other-azure-services"></a>Perché non Cache Redis di Azure è presente un riferimento alla libreria di classe MSDN per alcune hello altri servizi di Azure?
Cache Redis di Microsoft Azure si basa sull'hello open source comuni Redis Cache ed è possibile accedervi da un'ampia gamma di [client Redis](http://redis.io/clients) per molti linguaggi di programmazione. Ogni client ne ha la propria API che rende chiama l'istanza di cache Redis toohello con [Redis comandi](http://redis.io/commands).

Poiché ogni client è diverso, non è disponibile alcun riferimento di classe centralizzato su MSDN. Ogni client offre documentazione di riferimento specifica. Documentazione di riferimento toohello inoltre, esistono diverse esercitazioni che mostra la modalità di avvio tooget con Cache Redis di Azure utilizzando diversi linguaggi e i client della cache. vedere queste esercitazioni tooaccess [la modalità di Cache Redis di Azure di toouse](cache-dotnet-how-to-use-azure-redis-cache.md) e fare clic su una lingua hello desiderato da Selezione lingua hello nella parte superiore di hello dell'articolo hello.

### <a name="can-i-use-azure-redis-cache-as-a-php-session-cache"></a>Posso utilizzare Cache Redis di Azure come una cache di sessione PHP?
Sì, toouse Cache Redis di Azure come un cache della sessione PHP, specificare l'istanza hello connessione stringa tooyour Cache Redis di Azure in `session.save_path`.

> [!IMPORTANT]
> Quando si utilizza la Cache Redis di Azure come un cache della sessione PHP, è necessario l'URL codificare hello sicurezza chiave tooconnect utilizzati toohello di cache, come illustrato nell'esempio seguente hello:
>
> `session.save_path = "tcp://mycache.redis.cache.windows.net:6379?auth=<url encoded primary or secondary key here>";`
>
> Se la chiave hello non è codificato in URL, venga visualizzato di un'eccezione con un messaggio simile a:`Failed tooparse session.save_path`
>
>

Per ulteriori informazioni sull'utilizzo di Cache Redis come cache di una sessione PHP con client PhpRedis hello, vedere [gestore di sessione PHP](https://github.com/phpredis/phpredis#php-session-handler).

### <a name="what-are-redis-databases"></a>Cosa sono i database Redis?

I database di redis sono semplicemente una separazione logica dei dati all'interno di hello stessa istanza di Redis. memoria cache di Hello è condivisa tra tutti i database hello e il consumo di memoria effettivo di un determinato database dipende da hello. chiavi/valori archiviati in tale database. Ad esempio una cache C6 ha 53 GB di memoria. È possibile scegliere tooput tutti 53 GB in un database oppure è possibile suddividere tra più database. 

> [!NOTE]
> Quando si usa una Cache Redis di Azure Premium con il clustering abilitato, è disponibile solo il database 0. Questa limitazione è un limite di Redis intrinseco e non è specifico tooAzure Cache Redis. Per ulteriori informazioni, vedere [devo toomake qualsiasi toouse applicazione di modifiche toomy client clustering?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)
> 
> 


<a name="cache-ssl"></a>

### <a name="when-should-i-enable-hello-non-ssl-port-for-connecting-tooredis"></a>Quando è necessario attivare la porta non SSL hello per la connessione tooRedis?
Il server Redis non offre il supporto nativo per SSL, ma tale supporto è disponibile nella Cache Redis di Azure. Se ci si connette tooAzure Cache Redis e il client supporta SSL, ad esempio stackexchange. Redis, è necessario utilizzare SSL.

>[!NOTE]
>porta non SSL Hello è disabilitata per impostazione predefinita per le nuove istanze di Cache Redis di Azure. Se il client non supporta SSL, quindi è necessario abilitare la porta non SSL hello seguendo le direzioni di hello in hello [porte di accesso](cache-configure.md#access-ports) sezione di hello [configurare una cache in Cache Redis di Azure](cache-configure.md) articolo.
>
>

Redis, ad esempio strumenti `redis-cli` non funzionano con hello porta SSL, ma è possibile utilizzare un'utilità, ad esempio `stunnel` toosecurely connettersi porta SSL di hello strumenti toohello seguendo le direzioni di hello in hello [annuncio di Provider di stato sessione ASP.NET per la versione di anteprima Redis](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx) post di blog.

Per istruzioni sul download hello Redis strumenti, vedere hello [come è possibile eseguire i comandi di Redis?](#cache-commands) sezione.

### <a name="what-are-some-production-best-practices"></a>Quali sono alcune procedure consigliate per la produzione?
* [Procedure consigliate di StackExchange.Redis](#stackexchangeredis-best-practices)
* [Configurazione e concetti](#configuration-and-concepts)
* [Test delle prestazioni](#performance-testing)

#### <a name="stackexchangeredis-best-practices"></a>Procedure consigliate di StackExchange.Redis
* Impostare `AbortConnect` toofalse, quindi consentire hello ConnectionMultiplexer riconnettersi automaticamente. [Per informazioni dettagliate, vedere qui](https://gist.github.com/JonCole/36ba6f60c274e89014dd#file-se-redis-setabortconnecttofalse-md).
* Riutilizzare hello ConnectionMultiplexer: non creare una nuova istanza per ogni richiesta. Hello `Lazy<ConnectionMultiplexer>` modello [qui](cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-the-cache) è consigliato.
* Redis funziona meglio con valori inferiori, quindi considerare di suddividere i dati più grandi in più chiavi. In [questa discussione di Redis](https://groups.google.com/forum/#!searchin/redis-db/size/redis-db/n7aa2A4DZDs/3OeEPHSQBAAJ), 100 kb viene considerato grande. Leggere [in questo articolo](https://gist.github.com/JonCole/db0e90bedeb3fc4823c2#large-requestresponse-size) per un problema di esempio che può essere causato da valori di grandi dimensioni.
* Configurare il [impostazioni pool di thread](#important-details-about-threadpool-growth) tooavoid timeout.
* Usare almeno hello connectTimeout predefinita di 5 secondi. Questo intervallo concederebbe toore tempo sufficiente stackexchange. Redis-connessione hello, in caso di un acustico di rete.
* Tenere presente i costi di prestazioni hello associati a diverse operazioni che è in esecuzione. Ad esempio, hello `KEYS` comando è un'operazione o (n) e deve essere evitato. Hello [redis.io sito](http://redis.io/commands/) contiene informazioni dettagliate sugli complessità della fase hello per ogni operazione che supporta. Fare clic su ogni complessità hello toosee di comando per ogni operazione.

#### <a name="configuration-and-concepts"></a>Configurazione e concetti
* Usare il livello Premium o Standard per i sistemi di produzione. Hello livello Basic è un sistema singolo nodo con alcuna replica di dati e di alcun contratto di servizio. Usare almeno una cache di livello C1. Le cache di livello C0 sono usate solitamente in scenari semplici di sviluppo e test.
* Tenere presente che Redis è un archivio dati **in memoria** . Leggere [questo articolo](https://gist.github.com/JonCole/b6354d92a2d51c141490f10142884ea4#file-whathappenedtomydatainredis-md) per acquisire familiarità con gli scenari in cui può verificarsi una perdita di dati.
* Sviluppare il sistema in modo che possa gestire blips connessione [scadenza toopatching e failover](https://gist.github.com/JonCole/317fe03805d5802e31cfa37e646e419d#file-azureredis-patchingexplained-md).

#### <a name="performance-testing"></a>Test delle prestazioni
* Iniziare a usare `redis-benchmark.exe` tooget un'idea di velocità effettiva possibili prima di scrivere i test delle prestazioni. Poiché `redis-benchmark` non supporta SSL, è necessario [consentono alla porta Non SSL hello tramite hello portale di Azure](cache-configure.md#access-ports) prima di eseguire test hello. Per esempi, vedere [come effettuare un benchmark e testare le prestazioni della cache di hello?](#how-can-i-benchmark-and-test-the-performance-of-my-cache)
* hello client Hello VM usata per il test deve essere l'istanza di cache Redis stessa area.
* È consigliabile utilizzare Dv2 serie di macchine Virtuali per il client, in quanto dispone di hardware migliori e deve fornire risultati ottimali hello.
* Verificare che il client come cache di hello che si esegue il test nella macchina virtuale si sceglie è altrettanto capacità di calcolo e di larghezza di banda.
* Abilitare VRSS nel computer client hello se si utilizza Windows. [Per informazioni dettagliate, vedere qui](https://technet.microsoft.com/library/dn383582.aspx).
* Le istanze del livello Premium di Redis hanno migliore latenza di rete e velocità effettiva, poiché sono in esecuzione su hardware migliori in CPU e rete.

<a name="cache-redis-commands"></a>

### <a name="what-are-some-of-hello-considerations-when-using-common-redis-commands"></a>Quando si usano i comandi di Redis più comuni, quali sono alcune considerazioni sull'hello?
* Non è necessario eseguire alcuni comandi di Redis che accettano un toocomplete molto tempo, senza conoscere l'impatto di hello di questi comandi.
  * Ad esempio, non eseguire hello [CHIAVI](http://redis.io/commands/keys) comando nell'ambiente di produzione e potrebbero richiedere un tooreturn molto tempo in base al numero di hello di chiavi. Redis è un server a thread singolo ed elabora un comando alla volta. Se si dispone di altri comandi rilasciati dopo le CHIAVI, non verrà elaborato fino a quando non Redis elabora comando CHIAVI hello. Hello [redis.io sito](http://redis.io/commands/) contiene informazioni dettagliate sugli complessità della fase hello per ogni operazione che supporta. Fare clic su ogni complessità hello toosee di comando per ogni operazione.
* È consigliabile usare coppie chiave-valore di piccole o di grandi dimensioni? In generale, dipende dallo scenario hello. Se lo scenario richiede chiavi, è possibile regolare hello ConnectionTimeout e valori nuovi tentativi e modificare la logica di ripetizione. Dalla prospettiva del server Redis, i valori minori si osservano toohave ottenere prestazioni migliori.
* Queste considerazioni non significa che è possibile archiviare i valori più grandi in Redis; è necessario essere consapevoli di hello seguenti considerazioni. Le latenze saranno più elevate. Se si dispone di un set di dati più grande e uno più piccoli, è possibile utilizzare più istanze di ConnectionMultiplexer, ognuno configurato con un set diverso di valori di timeout e ripetizione, come descritto nella precedente hello [cosa hello Opzioni di configurazione stackexchange. Redis](#cache-configuration) sezione.

<a name="cache-benchmarking"></a>

### <a name="how-can-i-benchmark-and-test-hello-performance-of-my-cache"></a>Come è possibile effettuare un benchmark e testare le prestazioni della cache di hello?
* [Abilitare la diagnostica della cache](cache-how-to-monitor.md#enable-cache-diagnostics) in modo da poter [monitoraggio](cache-how-to-monitor.md) hello integrità della cache. È possibile visualizzare le metriche nel portale di Azure hello e si possono anche hello [scaricare ed esaminare](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) loro utilizzando gli strumenti di hello di propria scelta.
* È possibile utilizzare test tooload redis benchmark.exe server Redis.
* Verificare che siano in hello client di test di carico hello e cache Redis hello stessa area.
* Utilizza redis cli.exe e monitorare la cache di hello tramite hello informazioni sul comando.
* Se il carico causa frammentazione della memoria elevata, deve applicare la scalabilità verticale tooa dimensioni della cache.
* Per istruzioni sul download hello Redis strumenti, vedere hello [come è possibile eseguire i comandi di Redis?](#cache-commands) sezione.

Hello comandi riportati di seguito forniscono un esempio di utilizzo di redis benchmark.exe. Per risultati accurati, eseguire questi comandi da una macchina virtuale in hello stessa regione della cache.

* Testare le richieste SET in pipeline usando un payload 1 k

  `redis-benchmark.exe -h **yourcache**.redis.cache.windows.net -a **yourAccesskey** -t SET -n 1000000 -d 1024 -P 50`
* Testare le richieste GET in pipeline usando un payload 1 k.
  Nota: Eseguire test SET hello illustrato in precedenza prima cache toopopulate

  `redis-benchmark.exe -h **yourcache**.redis.cache.windows.net -a **yourAccesskey** -t GET -n 1000000 -d 1024 -P 50`

<a name="threadpool"></a>

### <a name="important-details-about-threadpool-growth"></a>Informazioni importanti sulla crescita del pool di thread
Hello pool di thread CLR è disponibili due tipi di thread - "Lavoro" e "Porta completamento i/o" (noto anche come IOCP) di thread.

* I thread di lavoro vengono usati per operazioni come l'elaborazione dei metodi `Task.Run(…)` o `ThreadPool.QueueUserWorkItem(…)`. Questi thread utilizzati anche da vari componenti di hello CLR quando lavoro toohappen in un thread in background.
* IOCP vengono utilizzati quando si verifica dei / o asincroni (ad esempio, durante la lettura dalla rete hello).

il pool di thread di Hello fornisce nuovi thread di lavoro o thread di completamento i/o su richiesta (senza qualsiasi limitazione) fino a quando raggiunge l'impostazione "Minimo" hello per ogni tipo di thread. Per impostazione predefinita, numero minimo di hello di thread è toohello numero di processori in un sistema.

Una volta hello numero esistente thread (occupato) riscontri hello "minimo" del thread, hello ThreadPool verrà velocità hello in corrispondenza del quale inserisce il nuovo thread tooone di thread per 500 millisecondi. Solitamente, se il sistema riceve un picco di lavoro che necessita di un thread IOCP, il lavoro viene elaborato molto rapidamente. Tuttavia, se burst hello di lavoro è maggiore del hello configurata l'impostazione "Minimo", esisterà un ritardo nell'elaborazione di parte del lavoro hello come hello pool di thread in attesa di una delle due operazioni toohappen.

1. Un thread esistente diventa disponibile tooprocess hello lavoro.
2. Nessun thread esistente diventa disponibile per 500 ms e viene creato un nuovo thread.

In pratica, ciò significa che quando il numero di hello dei thread occupati è maggiore del numero minimo thread, probabile che pagamento un ritardo di 500 ms prima che il traffico di rete viene elaborato da un'applicazione hello. Inoltre, è importante toonote quando un oggetto esistente thread rimane inattiva per più di 15 secondi (basati su cosa ricordare), verrà pulita e ripetere il ciclo di crescita e ritiro.

Se si osserva un messaggio di errore di esempio da StackExchange.Redis, build 1.0.450 o versione successiva, si noterà che ora le statistiche dell'oggetto ThreadPool vengono stampate. Di seguito sono riportati i dettagli relativi a IOCP e WORKER.

    System.TimeoutException: Timeout performing GET MyKey, inst: 2, mgr: Inactive,
    queue: 6, qu: 0, qs: 6, qc: 0, wr: 0, wq: 0, in: 0, ar: 0,
    IOCP: (Busy=6,Free=994,Min=4,Max=1000),
    WORKER: (Busy=3,Free=997,Min=4,Max=1000)

Nell'esempio precedente hello, si noterà che per il thread IOCP esistono 6 thread occupati e sistema hello configurato tooallow 4 minimo di thread. In questo caso, il client hello sarebbe probabilmente verificato due ritardi di 500 ms perché 6 > 4.

Si noti che StackExchange.Redis può raggiungere il timeout se la crescita dei thread IOCP o WORKER viene limitata.

### <a name="recommendation"></a>Raccomandazione
Con queste informazioni, è consigliabile che i clienti hanno impostato valore di configurazione minima hello per toosomething di thread di lavoro e IOCP superiore rispetto al valore predefinito hello. È Impossibile assegnare giusto informazioni aggiuntive su ciò che questo valore deve essere perché hello valore corretto per un'applicazione è troppo alta o bassa per un'altra applicazione. Questa impostazione può inoltre influire hello di altre parti di applicazioni complesse, quindi ogni cliente deve ottimizzare toofine che deve tootheir questa impostazione specifica. Un buon punto di partenza è 200 o 300, da verificare e modificare a seconda delle necessità.

Come tooconfigure questa impostazione:

* In ASP.NET, utilizzare hello ["minIoThreads" impostazione di configurazione] [ "minIoThreads" configuration setting] in hello `<processModel>` elemento di configurazione in Web. config. Se è in esecuzione all'interno di siti Web di Azure, questa impostazione non viene esposto tramite le opzioni di configurazione hello. Tuttavia, deve ancora essere in grado di tooconfigure questa impostazione a livello di codice (vedere sotto) dal metodo Application_Start in global.asax.cs.

  > [!NOTE] 
  > Hello il valore specificato in questo elemento di configurazione è un *ogni core* impostazione. Ad esempio, se si dispone di una macchina a 4 core e si desidera toobe di impostazione del minIOThreads 200 in fase di esecuzione, utilizzerebbe `<processModel minIoThreads="50"/>`.
  >

* All'esterno di ASP.NET, utilizzare hello [ThreadPool.SetMinThreads(...) ](https://msdn.microsoft.com/library/system.threading.threadpool.setminthreads.aspx) API.

<a name="server-gc"></a>

### <a name="enable-server-gc-tooget-more-throughput-on-hello-client-when-using-stackexchangeredis"></a>Abilitare una velocità effettiva maggiore sul client hello tooget GC server quando si utilizza stackexchange. Redis
Attivazione di GC server, è possibile ottimizzare client hello e fornire la velocità effettiva e prestazioni migliori quando si utilizza stackexchange. Redis. Per ulteriori informazioni sul server di catalogo globale e come tooenable, vedere hello seguenti articoli:

* [GC server tooenable](https://msdn.microsoft.com/library/ms229357.aspx)
* [Nozioni fondamentali di Garbage Collection](https://msdn.microsoft.com/library/ee787088.aspx)
* [Garbage Collection e prestazioni](https://msdn.microsoft.com/library/ee851764.aspx)


### <a name="performance-considerations-around-connections"></a>Considerazioni sulle prestazioni per le connessioni

Ogni piano tariffario presenta diversi limiti di connessioni client, memoria e larghezza di banda. Mentre ogni dimensione della cache consente *fino a* un determinato numero di connessioni, ogni tooRedis connessione overhead è associato. Un esempio di questo sovraccarico potrebbe essere l'utilizzo della CPU e della memoria a causa della crittografia TLS/SSL. limite massimo di connessioni Hello per una dimensione della cache specificata si presuppone una cache con caricata ridotto. Se caricare dall'overhead connessione *più* carico dalle operazioni client supera la capacità di sistema di hello, cache di hello possa verificarsi problemi di capacità, anche se non è stato superato il limite di connessioni hello per la dimensione corrente della cache di hello.

Per ulteriori informazioni sui limiti di hello connessioni diverse per ogni livello, vedere [prezzi di Cache Redis di Azure](https://azure.microsoft.com/pricing/details/cache/). Per ulteriori informazioni sulle connessioni e altre configurazioni predefinite, vedere [Configurazione predefinita del server Redis](cache-configure.md#default-redis-server-configuration).

<a name="cache-monitor"></a>

### <a name="how-do-i-monitor-hello-health-and-performance-of-my-cache"></a>Come monitorare hello integrità e le prestazioni di my cache?
Le istanze di Cache Redis di Microsoft Azure possono essere monitorate nel hello [portale di Azure](https://portal.azure.com). È possibile visualizzare le metriche, aggiungere metriche grafici toohello schermata iniziale, personalizzare l'intervallo di data e ora hello di grafici di monitoraggio, aggiungere e rimuovere metriche dai grafici hello e impostare gli avvisi quando vengono soddisfatte determinate condizioni. Per altre informazioni, vedere [Come monitorare Cache Redis di Azure](cache-how-to-monitor.md).

Cache Redis Hello **menu Resource** contiene inoltre numerosi strumenti per il monitoraggio e risoluzione dei problemi delle cache.

* **Diagnostica e risoluzione dei problemi** fornisce informazioni sui problemi comuni e sulle strategie per risolverli.
* **Integrità risorsa** esamina la risorsa e indica se viene eseguita nel modo previsto. Per ulteriori informazioni su hello servizio di integrità delle risorse di Azure, vedere [Panoramica di integrità delle risorse di Azure](../resource-health/resource-health-overview.md).
* **Nuova richiesta di supporto** fornisce opzioni tooopen una richiesta di supporto per la cache.

Questi strumenti consentono di toomonitor hello integrità delle istanze di Cache Redis di Azure e consentono di gestire le applicazioni di memorizzazione nella cache. Per ulteriori informazioni, vedere hello "Impostazioni di risoluzione dei problemi e il supporto" sezione [la modalità di Cache Redis di Azure di tooconfigure](cache-configure.md).

<a name="cache-timeouts"></a>

### <a name="why-am-i-seeing-timeouts"></a>Perché vengono visualizzati timeout?
Timeout verificarsi nel client hello utilizzare tootalk tooRedis. Quando il server di Redis toohello viene inviato un comando, comando hello viene messo in coda e server Redis infine preleva comando hello e lo esegue. Tuttavia client hello può verificarsi un timeout durante l'operazione e se non un'eccezione viene generato per la chiamata sul lato hello. Per altre informazioni sulla risoluzione dei problemi di timeout, vedere [Risoluzione dei problemi lato client](cache-how-to-troubleshoot.md#client-side-troubleshooting) ed [Eccezioni di timeout StackExchange.Redis](cache-how-to-troubleshoot.md#stackexchangeredis-timeout-exceptions).

<a name="cache-disconnect"></a>

### <a name="why-was-my-client-disconnected-from-hello-cache"></a>Motivo per cui il client è stata disconnessa dalla cache di hello?
di seguito Hello sono motivi comuni per la disconnessione di una cache.

* Cause lato client
  * un'applicazione Hello client è stata ridistribuita.
  * un'applicazione client Hello eseguita un'operazione di ridimensionamento.
    * Nel caso di hello di servizi Cloud o le applicazioni Web, questo potrebbe essere dovuto tooauto-scaling.
  * livello di rete Hello sul lato client hello modificato.
  * Gli errori temporanei si è verificato in hello client o nei nodi di rete hello tra hello client e server di hello.
  * sono stati raggiunti i limiti di soglia della larghezza di banda di Hello.
  * Le operazioni associate alla CPU impiegato toocomplete troppo lungo.
* Cause lato server
  * In hello offerta di cache standard, hello servizio Cache Redis di Azure ha avviato un failover dal nodo secondario toohello di hello nodo primario.
  * Azure è l'applicazione di patch istanza hello in cui è stata distribuita cache di hello
    * Ciò può riguardare aggiornamenti del server Redis o manutenzione generale delle VM.

### <a name="which-azure-cache-offering-is-right-for-me"></a>Qual è l'offerta di Cache di Azure più adatta alle mie esigenze?
> [!IMPORTANT]
> Come da [annuncio](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/) dello scorso anno, il Servizio cache gestita di Azure e il servizio Cache nel ruolo di Azure **sono stati ritirati** il 30 novembre 2016. Il Consiglio è toouse [Cache Redis di Azure](https://azure.microsoft.com/services/cache/). Per informazioni sulla migrazione, vedere [migrazione dal servizio Cache gestita tooAzure Cache Redis](cache-migrate-to-redis.md).
>
>

### <a name="azure-redis-cache"></a>Cache Redis di Azure
Cache Redis di Azure è in genere disponibile in dimensioni too53 GB e dispone di un contratto di servizio pari al 99,9% di disponibilità. nuovo Hello [livello premium](cache-premium-tier-intro.md) offre le dimensioni di too530 GB e supporto per il clustering, reti VIRTUALI e la persistenza, con un contratto di servizio con disponibilità del 99,9%.

Azure Redis Cache offre ai clienti hello possibilità toouse una cache Redis sicura e dedicata, gestita da Microsoft. Grazie a questa offerta, si ottiene tooleverage hello ampia gamma di funzionalità e l'ecosistema di Redis e affidabili di hosting e monitoraggio di Microsoft.

A differenza delle cache tradizionali in grado di gestire solo coppie chiave-valore, Redis è nota per i tipi di dati ad alte prestazioni. Anche redis supporta l'esecuzione di operazioni atomiche su questi tipi, ad esempio stringa tooa; Incremento valore hello in un hash; elenco tooa push. calcolare l'intersezione, unione e differenza: o recupero hello membro con priorità più elevata in un set ordinato. Altre funzionalità include il supporto per le transazioni, pubblicazione/sottoscrizione, scripting Lua, chiavi con una limitata time-to-live e configurazione delle impostazioni toomake Redis comportano più come una cache tradizionale.

Esito positivo di un altro aspetto chiave tooRedis è hello integro, innovativo ecosistema intorno a esso. Ciò si riflette nel set diversi di hello di client Redis disponibile in più lingue. Questo ecosistema e una vasta gamma di client consentono toobe Cache Redis di Azure usata da quasi qualsiasi carico di lavoro creato in Azure.

Per ulteriori informazioni sui concetti introduttivi di Cache Redis di Azure, vedere [la modalità di Cache Redis di Azure di tooUse](cache-dotnet-how-to-use-azure-redis-cache.md) e [documentazione Cache Redis di Azure](index.md).

### <a name="managed-cache-service"></a>Servizio cache gestita
Il [Servizio cache gestita è stato ritirato il 30 novembre 2016](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).

tooview archiviati documentazione, vedere [archiviati gestiti Cache servizio documentazione](https://msdn.microsoft.com/library/azure/dn386094.aspx).

### <a name="in-role-cache"></a>Cache nel ruolo
Il [servizio Cache nel ruolo è stato ritirato il 30 novembre 2016](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).

tooview archiviati documentazione, vedere [archiviazione della documentazione di Cache nel ruolo](https://msdn.microsoft.com/library/azure/dn386103.aspx).

["minIoThreads" configuration setting]: https://msdn.microsoft.com/library/vstudio/7w2sway1(v=vs.100).aspx
