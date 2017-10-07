---
title: una rete virtuale per una Cache Redis di Azure Premium aaaConfigure | Documenti Microsoft
description: Informazioni su come toocreate e gestire il supporto di rete virtuale per le istanze di Cache Redis di Azure di livello Premium
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 8b1e43a0-a70e-41e6-8994-0ac246d8bf7f
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: sdanie
ms.openlocfilehash: fab715f4d9365ee4c2f8b89d2e2e58768c25b671
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-virtual-network-support-for-a-premium-azure-redis-cache"></a>Come tooconfigure supporta la rete virtuale per una Cache Redis di Azure Premium
Cache Redis di Azure ha diverse offerte di cache, che forniscono flessibilità nella scelta di hello della dimensione della cache e le funzionalità, incluse le funzionalità di livello Premium, ad esempio clustering, persistenza e il supporto di rete virtuale. Una rete virtuale è una rete privata nel cloud hello. Quando un'istanza di Cache Redis di Azure è configurata con una rete virtuale, non è indirizzabile pubblicamente e accessibile solo dalle macchine virtuali e le applicazioni all'interno di hello rete virtuale. In questo articolo viene descritto come la rete virtuale tooconfigure il supporto per un'istanza di Cache Redis di Azure premium.

> [!NOTE]
> Cache Redis di Azure supporta le reti virtuali classiche e di Resource Manager.
> 
> 

Per informazioni su altre funzionalità di cache premium, vedere [livello Premium di Cache Redis di Azure di introduzione toohello](cache-premium-tier-intro.md).

## <a name="why-vnet"></a>Perché usare una rete virtuale?
[Rete virtuale di Azure (VNet)](https://azure.microsoft.com/services/virtual-network/) distribuzione fornisce sicurezza avanzata e isolamento per Cache Redis di Azure, nonché le subnet, criteri di controllo di accesso e altre funzionalità toofurther limitare l'accesso.

## <a name="virtual-network-support"></a>Supporto della rete virtuale
Supporto di rete virtuale è configurato su hello **nuova Cache Redis** pannello durante la creazione della cache. 

[!INCLUDE [redis-cache-create](../../includes/redis-cache-premium-create.md)]

Dopo aver selezionato un vantaggio a livello di prezzo, è possibile configurare l'integrazione della rete virtuale Redis selezionando una rete virtuale in hello stessa sottoscrizione e il percorso della cache. toouse una nuova rete virtuale, prima è necessario crearla eseguendo la procedura descritta hello in [creare una rete virtuale usando il portale di Azure hello](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) o [creare una rete virtuale (classico) tramite il portale di Azure hello](../virtual-network/virtual-networks-create-vnet-classic-pportal.md) e quindi restituire toohello **Nuova Cache Redis** toocreate blade e configurare la cache premium.

tooconfigure hello rete virtuale per la nuova cache, fare clic su **rete virtuale** su hello **nuova Cache Redis** pannello e seleziona hello desiderato rete virtuale dall'elenco a discesa hello.

![Rete virtuale][redis-cache-vnet]

Selezionare hello subnet desiderato da hello **Subnet** elenco a discesa elenco e specificare hello desiderato **indirizzo IP statico**. Se si utilizza un classico hello di rete virtuale **indirizzo IP statico** campo è facoltativo e, se non viene specificato, dalla subnet hello selezionato viene scelto uno.

> [!IMPORTANT]
> Quando si distribuisce un tooa Cache Redis di Azure Resource Manager VNet, cache di hello deve essere in una subnet dedicata che non contiene altre risorse, ad eccezione delle istanze di Cache Redis di Azure. Se viene effettuato un tentativo di toodeploy un tooa Cache Redis di Azure Resource Manager VNet tooa subnet che contiene altre risorse, distribuzione hello ha esito negativo.
> 
> 

![Rete virtuale][redis-cache-vnet-ip]

> [!IMPORTANT]
> Azure riserva alcuni indirizzi IP all'interno di ogni subnet e questi indirizzi non possono essere usati. gli indirizzi IP e il cognome di subnet hello Hello sono riservati per conformità al protocollo, insieme a tre ulteriori indirizzi utilizzato per i servizi di Azure. Per altre informazioni, vedere [Esistono restrizioni sull'uso di indirizzi IP all'interno di tali subnet?](../virtual-network/virtual-networks-faq.md#are-there-any-restrictions-on-using-ip-addresses-within-these-subnets)
> 
> In aggiunta toohello gli indirizzi IP utilizzati dall'infrastruttura di rete virtuale di Azure hello, ogni Redis istanza hello indirizzi IP della subnet usa due per partizione e un indirizzo IP aggiuntivo di bilanciamento del carico hello. Una cache non cluster è considerata toohave una partizione.
> 
> 

Dopo la creazione della cache di hello, si può visualizzare la configurazione di hello per hello rete virtuale, fare clic su **rete virtuale** da hello **menu risorse**.

![Rete virtuale][redis-cache-vnet-info]

tooconnect tooyour Azure Redis cache istanza quando si utilizza una rete virtuale, specificare il nome host hello della cache nella stringa di connessione hello, come illustrato nell'esempio seguente hello:

    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        return ConnectionMultiplexer.Connect("contoso5premium.redis.cache.windows.net,abortConnect=false,ssl=true,password=password");
    });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

## <a name="azure-redis-cache-vnet-faq"></a>Domande frequenti sulla rete virtuale di Cache Redis di Azure
Hello seguente elenco contiene le risposte toocommonly domande frequenti sulla scalabilità di hello Cache Redis di Azure.

* [Quali sono alcuni problemi comuni di configurazione errata per Cache Redis di Azure e le reti virtuali?](#what-are-some-common-misconfiguration-issues-with-azure-redis-cache-and-vnets)
* [Come è possibile verificare che la cache funzioni in una rete virtuale?](#how-can-i-verify-that-my-cache-is-working-in-a-vnet)
* [È possibile usare reti virtuali con una cache Standard o Basic?](#can-i-use-vnets-with-a-standard-or-basic-cache)
* [Perché la creazione di una cache Redis ha esito negativo in alcune subnet e non in altre?](#why-does-creating-a-redis-cache-fail-in-some-subnets-but-not-others)
* [Quali sono i requisiti dello spazio di indirizzi subnet hello?](#what-are-the-subnet-address-space-requirements)
* [Tutte le funzionalità della cache funzionano quando si ospita una cache in una rete virtuale?](#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)

## <a name="what-are-some-common-misconfiguration-issues-with-azure-redis-cache-and-vnets"></a>Quali sono alcuni problemi comuni di configurazione errata per Cache Redis di Azure e le reti virtuali?
Quando la Cache Redis di Azure è ospitata in una rete virtuale, vengono utilizzate porte hello in hello le tabelle seguenti. 

>[!IMPORTANT]
>Se le porte hello in hello le tabelle seguenti sono bloccate, cache di hello potrebbe non funzionare correttamente. Con uno o più di queste porte bloccate è il problema errata configurazione più comune di hello quando si usa una Cache Redis di Azure in una rete virtuale.
> 
> 

- [Requisiti delle porte in uscita](#outbound-port-requirements)
- [Requisiti delle porte in ingresso](#inbound-port-requirements)

### <a name="outbound-port-requirements"></a>Requisiti delle porte in uscita

Vi sono sette requisiti delle porte in uscita.

- Se si desidera, tutte le connessioni in uscita toohello, internet può essere eseguita tramite un client controllo dispositivo locale.
- Tre delle porte hello indirizzare endpoint tooAzure traffico per la manutenzione di archiviazione di Azure e DNS di Azure.
- Hello rimanenti gli intervalli di porte e per le comunicazioni di subnet interne Redis. Per le comunicazioni subnet interne di Redis non è richiesta alcuna regola NSG subnet.

| Porte | Direzione | Protocollo di trasporto | Scopo | IP locale | IP remoto |
| --- | --- | --- | --- | --- | --- |
| 80, 443 |In uscita |TCP |Dipendenze Redis in Archiviazione di Azure/PKI (Internet) | (Subnet Redis) |* |
| 53 |In uscita |TCP/UDP |Dipendenze Redis nel DNS (Internet/rete virtuale) | (Subnet Redis) |* |
| 8443 |In uscita |TCP |Comunicazioni interne per Redis | (Subnet Redis) | (Subnet Redis) |
| 10221-10231 |In uscita |TCP |Comunicazioni interne per Redis | (Subnet Redis) | (Subnet Redis) |
| 20226 |In uscita |TCP |Comunicazioni interne per Redis | (Subnet Redis) |(Subnet Redis) |
| 13000-13999 |In uscita |TCP |Comunicazioni interne per Redis | (Subnet Redis) |(Subnet Redis) |
| 15000-15999 |In uscita |TCP |Comunicazioni interne per Redis | (Subnet Redis) |(Subnet Redis) |


### <a name="inbound-port-requirements"></a>Requisiti delle porte in ingresso

Vi sono otto requisiti delle porte in ingresso. Sono richieste in ingresso in questi intervalli in ingresso da altri servizi ospitati in hello stessa rete virtuale o interno toohello comunicazioni subnet Redis.

| Porte | Direzione | Protocollo di trasporto | Scopo | IP locale | IP remoto |
| --- | --- | --- | --- | --- | --- |
| 6379, 6380 |In ingresso |TCP |TooRedis di comunicazione client, Azure il bilanciamento del carico | (Subnet Redis) |Rete virtuale, Bilanciamento carico di Azure |
| 8443 |In ingresso |TCP |Comunicazioni interne per Redis | (Subnet Redis) |(Subnet Redis) |
| 8500 |In ingresso |TCP/UDP |Bilanciamento del carico di Azure | (Subnet Redis) |Azure Load Balancer |
| 10221-10231 |In ingresso |TCP |Comunicazioni interne per Redis | (Subnet Redis) |(Subnet Redis), bilanciamento del carico di Azure |
| 13000-13999 |In ingresso |TCP |TooRedis di comunicazione client, i cluster di bilanciamento del carico di Azure | (Subnet Redis) |Rete virtuale, Bilanciamento carico di Azure |
| 15000-15999 |In ingresso |TCP |TooRedis di comunicazione client cluster di Azure, il bilanciamento del carico | (Subnet Redis) |Rete virtuale, Bilanciamento carico di Azure |
| 16001 |In ingresso |TCP/UDP |Bilanciamento del carico di Azure | (Subnet Redis) |Azure Load Balancer |
| 20226 |In ingresso |TCP |Comunicazioni interne per Redis | (Subnet Redis) |(Subnet Redis) |

### <a name="additional-vnet-network-connectivity-requirements"></a>Ulteriori requisiti di connettività della rete VNET

Esistono requisiti di connettività di rete per Cache Redis di Azure che potrebbero non essere inizialmente soddisfatti in una rete virtuale. Cache Redis di Azure richiede che tutti hello segue gli elementi toofunction correttamente se utilizzato in una rete virtuale.

* In uscita connettività tooAzure archiviazione gli endpoint di rete in tutto il mondo. Sono inclusi gli endpoint si trova in hello stessa area come istanza di Cache Redis di Azure hello, nonché gli endpoint di archiviazione si trova **altri** aree di Azure. Endpoint di archiviazione Azure risolvere in hello seguenti domini DNS: *t*, *>.BLOB.Core.Windows.NET*, *queue.core.windows.net*e *file.core.windows.net*. 
* In uscita connettività di rete troppo*ocsp.msocsp.com*, *mscrl.microsoft.com*, e *crl.microsoft.com*. La connettività è la funzionalità SSL toosupport necessari.
* configurazione del DNS per la rete virtuale hello Hello deve essere in grado di risolvere tutti gli endpoint hello e domini indicati hello punti precedenti. Questi requisiti di DNS possono essere soddisfatto garantendo un'infrastruttura DNS valida viene configurata e gestita per la rete virtuale hello.
* Toohello di connettività di rete in uscita seguente endpoint Azure Monitoring, risolvere in hello seguenti domini DNS: shoebox2 black.shoebox2.metrics.nsatc.net, Nord-prod2.prod2.metrics.nsatc.net, azglobal-black.azglobal.metrics.nsatc.net, shoebox2-red.shoebox2.metrics.nsatc.net, est-prod2.prod2.metrics.nsatc.net, azglobal-red.azglobal.metrics.nsatc.net.

### <a name="how-can-i-verify-that-my-cache-is-working-in-a-vnet"></a>Come è possibile verificare che la cache funzioni in una rete virtuale?

>[!IMPORTANT]
>Quando ci si connette l'istanza di Cache Redis di Azure tooan che è ospitato in una rete virtuale, la cache client devono essere in hello stessa rete virtuale, inclusi eventuali applicazioni di test o gli strumenti di diagnostica ping.
>
>

Una volta requisiti hello per le porte configurati come descritto nella sezione precedente di hello, è possibile verificare che la cache funziona eseguendo hello alla procedura seguente.

- [Riavviare il computer](cache-administration.md#reboot) tutti hello memorizzare nella cache i nodi. Se tutti hello richiesto non è possibile raggiungere le dipendenze della cache (come descritto in [in ingresso requisiti delle porte](cache-how-to-premium-vnet.md#inbound-port-requirements) e [requisiti delle porte in uscita](cache-how-to-premium-vnet.md#outbound-port-requirements)), cache di hello non sarà in grado di toorestart correttamente.
- Una volta che i nodi della cache di hello riavvio (come riportato dallo stato della cache di hello in hello portale di Azure), è possibile eseguire hello seguenti test:
  - eseguire il ping hello endpoint della cache (tramite la porta 6380) da un computer che si trova all'interno di hello stessa rete virtuale come hello nella cache, utilizzando [tcping](https://www.elifulkerson.com/projects/tcping.php). ad esempio:
    
    `tcping.exe contosocache.redis.cache.windows.net 6380`
    
    Se hello `tcping` strumento segnala che hello porta è aperta, la cache di hello è disponibile per la connessione dal client nella rete virtuale hello.

  - Un altro modo tootest è toocreate un client della cache di test (che può essere una semplice applicazione console tramite stackexchange. Redis) che si connette toohello cache e aggiunge e recupera alcuni elementi dalla cache di hello. Installare l'applicazione client di esempio hello in una macchina virtuale nella stessa rete virtuale come cache di hello hello ed eseguirlo come cache di toohello tooverify connettività.


### <a name="can-i-use-vnets-with-a-standard-or-basic-cache"></a>È possibile usare reti virtuali con una cache Standard o Basic?
Le reti virtuali possono essere usate solo con cache Premium.

### <a name="why-does-creating-a-redis-cache-fail-in-some-subnets-but-not-others"></a>Perché la creazione di una cache Redis ha esito negativo in alcune subnet e non in altre?
Se si distribuisce un tooa Cache Redis di Azure Resource Manager VNet, in una subnet dedicata che contiene l'altro tipo di risorsa deve essere cache di hello. Se viene effettuato un tentativo di toodeploy un tooa Cache Redis di Azure Resource Manager VNet subnet che contiene altre risorse, distribuzione hello ha esito negativo. È necessario eliminare le risorse esistenti hello interno hello subnet prima di poter creare una nuova cache Redis.

È possibile distribuire più tipi di risorse tooa classico tra reti virtuali purché si disponga di sufficiente IP indirizzi disponibili.

### <a name="what-are-hello-subnet-address-space-requirements"></a>Quali sono i requisiti dello spazio di indirizzi subnet hello?
Azure riserva alcuni indirizzi IP all'interno di ogni subnet e questi indirizzi non possono essere usati. gli indirizzi IP e il cognome di subnet hello Hello sono riservati per conformità al protocollo, insieme a tre ulteriori indirizzi utilizzato per i servizi di Azure. Per altre informazioni, vedere [Esistono restrizioni sull'uso di indirizzi IP all'interno di tali subnet?](../virtual-network/virtual-networks-faq.md#are-there-any-restrictions-on-using-ip-addresses-within-these-subnets)

In aggiunta toohello gli indirizzi IP utilizzati dall'infrastruttura di rete virtuale di Azure hello, ogni Redis istanza hello indirizzi IP della subnet usa due per partizione e un indirizzo IP aggiuntivo di bilanciamento del carico hello. Una cache non cluster è considerata toohave una partizione.

### <a name="do-all-cache-features-work-when-hosting-a-cache-in-a-vnet"></a>Tutte le funzionalità della cache funzionano quando si ospita una cache in una rete virtuale?
Quando la cache fa parte di una rete virtuale, solo i client nella rete virtuale hello possono accedere cache di hello. Di conseguenza, hello seguenti funzionalità di gestione della cache non funzionano in questo momento.

* Console redis: la Console Redis viene eseguita nel browser locale, non è compreso hello rete virtuale, non è possibile connettersi tooyour cache.

## <a name="use-expressroute-with-azure-redis-cache"></a>Usare ExpressRoute con Cache Redis di Azure
I clienti possono collegare un [Azure ExpressRoute](https://azure.microsoft.com/services/expressroute/) infrastruttura di rete virtuale tootheir circuito, e quindi di estendere i tooAzure di rete locale. 

Per impostazione predefinita, un circuito ExpressRoute appena creato non esegue il tunneling forzato (annuncio della route predefinita, 0.0.0.0/0) in una rete virtuale. Di conseguenza, la connettività Internet in uscita è consentita direttamente dalla rete virtuale hello e applicazioni client sono in grado di tooconnect tooother Azure endpoint incluso Cache Redis di Azure.

Tuttavia una configurazione personalizzata comune è il tunneling forzato toouse (annunciano una route predefinita) che forza in uscita Internet traffico tooinstead flusso locale. Questo flusso di traffico si interrompe la connettività con Cache Redis di Azure, se il traffico in uscita hello è quindi bloccato in locale, tale hello istanza di Cache Redis di Azure non è in grado di toocommunicate con le relative dipendenze.

soluzione hello è toodefine (più) definito dall'utente route (UDRs) nella subnet hello contenente hello Cache Redis di Azure. Un UDR definisce le route di subnet specifiche che verranno utilizzato il valore anziché route predefinita hello.

Se possibile, è consigliabile hello toouse seguente configurazione:

* configurazione di ExpressRoute Hello annuncia 0.0.0.0/0 e per impostazione predefinita force tunnel tutto il traffico in uscita in locale.
* subnet toohello UDR applicato contenente hello Cache Redis di Azure Hello definisce 0.0.0.0/0 con una route di lavoro per TCP/IP traffico toohello internet pubblica. ad esempio dall'impostazione hello hop successivo too'Internet di tipo '.

Hello effetto combinato di questi passaggi è che il livello di subnet hello UDR ha la precedenza su hello garantendo l'accesso a Internet in uscita da hello Cache Redis di Azure, tunneling forzato ExpressRoute.

Istanza di Cache Redis di Azure tooan connessione da un'applicazione locale tramite ExpressRoute non è uno scenario di utilizzo tipico a causa di motivi tooperformance (per ottimizzare le prestazioni della Cache Redis di Azure, i client devono trovarsi in hello stessa area hello Cache Redis di Azure).

>[!IMPORTANT] 
>Hello route definite in un UDR **deve** essere sufficientemente specifica tootake precedenza su qualsiasi route annunciate dalla configurazione di ExpressRoute hello. Hello seguente utilizza l'intervallo di indirizzi 0.0.0.0/0 ampie hello e di conseguenza possa accidentalmente sottoposto a override dagli annunci della route utilizzando più specifici intervalli di indirizzi.

>[!WARNING]  
>Cache Redis di Azure non è supportata con ExpressRoute configurazioni che **in modo non corretto tra-annunciare le route da hello peering percorso toohello privata percorso di peering pubblico**. Le configurazioni di ExpressRoute per cui è configurato il peering pubblico riceveranno gli annunci delle route da Microsoft per un elevato numero di intervalli di indirizzi IP di Microsoft Azure. Se questi intervalli di indirizzi in modo non corretto tra annunciati nel percorso di peering privato hello, risultato hello è che tutti i pacchetti di rete in uscita dalla subnet dell'istanza di Cache Redis di Azure hello sono rete locale del cliente in modo errato il tunneling forzato tooa infrastruttura. Questo flusso di rete interromperà Cache Redis di Azure. problema di toothis soluzione hello è toostop le route tra annunci hello peering percorso toohello privata percorso di peering pubblico.


Le informazioni generali sulle route definite dall'utente sono disponibili in questa [panoramica](../virtual-network/virtual-networks-udr-overview.md).

Per altre informazioni su ExpressRoute, vedere [Panoramica tecnica relativa a ExpressRoute](../expressroute/expressroute-introduction.md).

## <a name="next-steps"></a>Passaggi successivi
Informazioni su come toouse premium più memorizzano nella cache le funzionalità.

* [Livello di introduzione toohello Premium di Cache Redis di Azure](cache-premium-tier-intro.md)

<!-- IMAGES -->

[redis-cache-vnet]: ./media/cache-how-to-premium-vnet/redis-cache-vnet.png

[redis-cache-vnet-ip]: ./media/cache-how-to-premium-vnet/redis-cache-vnet-ip.png

[redis-cache-vnet-info]: ./media/cache-how-to-premium-vnet/redis-cache-vnet-info.png

