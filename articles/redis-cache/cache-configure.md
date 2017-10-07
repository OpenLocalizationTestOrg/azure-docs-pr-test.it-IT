---
title: aaaHow tooconfigure Cache Redis di Azure | Documenti Microsoft
description: Informazioni di configurazione di hello predefinita Redis per Cache Redis di Azure e informazioni su come tooconfigure di Azure Redis nella Cache istanze
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: d0bf2e1f-6a26-4e62-85ba-d82b35fc5aa6
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 08/22/2017
ms.author: sdanie
ms.openlocfilehash: 46bffb74cdf40e0e0a99c3a83dbe06d6fe1ea65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-azure-redis-cache"></a>La modalità di Cache Redis di Azure di tooconfigure
In questo argomento viene descritto come hello tooreview e aggiornamento configurazione per le istanze di Cache Redis di Azure e configurazione server Redis copre hello predefinita per le istanze di Cache Redis di Azure.

> [!NOTE]
> Per ulteriori informazioni sulla configurazione e utilizzo funzionalità di cache premium, vedere [come persistenza tooconfigure](cache-how-to-premium-persistence.md), [come tooconfigure clustering](cache-how-to-premium-clustering.md), e [supporto delle tooconfigure rete virtuale ](cache-how-to-premium-vnet.md).
> 
> 

## <a name="configure-redis-cache-settings"></a>Configurare le impostazioni di Cache Redis di Azure
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

Impostazioni Cache Redis di Azure vengono visualizzate e configurate in hello **Cache Redis** pannello utilizzando hello **risorsa Menu**.

![Impostazioni di Cache Redis](./media/cache-configure/redis-cache-settings.png)

È possibile visualizzare e configurare hello seguendo le impostazioni utilizzando hello **risorsa Menu**.

* [Panoramica](#overview)
* [Log attività](#activity-log)
* [Controllo di accesso (IAM)](#access-control-iam)
* [Tag](#tags)
* [Diagnostica e risoluzione dei problemi](#diagnose-and-solve-problems)
* [Impostazioni](#settings)
    * [Chiavi di accesso](#access-keys)
    * [Impostazioni avanzate](#advanced-settings)
    * [Redis Cache Advisor](#redis-cache-advisor)
    * [Ridimensionare](#scale)
    * [Dimensione del cluster Redis](#cluster-size)
    * [Persistenza dei dati Redis:](#redis-data-persistence)
    * [Pianificare gli aggiornamenti](#schedule-updates)
    * [Replica geografica](#geo-replication)
    * [Rete virtuale](#virtual-network)
    * [Firewall](#firewall)
    * [Proprietà](#properties)
    * [Blocchi](#locks)
    * [Script di automazione](#automation-script)
* [Amministrazione](#administration)
    * [Importazione dei dati](#importexport)
    * [Esportazione dei dati](#importexport)
    * [Reboot](#reboot)
* [Monitoraggio](#monitoring)
    * [Metriche di Redis](#redis-metrics)
    * [Regole di avviso](#alert-rules)
    * [Diagnostica](#diagnostics)
* [Supporto e impostazioni di risoluzione dei problemi](#support-amp-troubleshooting-settings)
    * [Integrità delle risorse](#resource-health)
    * [Nuova richiesta di supporto](#new-support-request)


## <a name="overview"></a>Panoramica

**Panoramica** include le informazioni di base sulla cache, ad esempio nome, porte, piano tariffario e le metriche della cache selezionata.

### <a name="activity-log"></a>Log attività

Fare clic su **log attività** tooview azioni eseguite nella cache. È inoltre possibile utilizzare tooexpand filtro tooinclude questa vista ad altre risorse. Per altre informazioni sull'uso dei log di controllo, vedere l'articolo relativo alle [operazioni di controllo con Resource Manager](../azure-resource-manager/resource-group-audit.md). Per altre informazioni sul monitoraggio degli eventi di Cache Redis di Azure, vedere [Operazioni e avvisi](cache-how-to-monitor.md#operations-and-alerts).

### <a name="access-control-iam"></a>Controllo di accesso (IAM)

Hello **Access control (IAM)** sezione fornisce supporto per il controllo di accesso basato sui ruoli (RBAC) in hello toohelp portale Azure organizzazioni soddisfino i requisiti di gestione accesso semplice e preciso. Per ulteriori informazioni, vedere [controllo di accesso basato sui ruoli nel portale di Azure hello](../active-directory/role-based-access-control-configure.md).

### <a name="tags"></a>Tag

Hello **tag** sezione consente di organizzare le risorse. Per ulteriori informazioni, vedere [tramite tag tooorganize le risorse di Azure](../azure-resource-manager/resource-group-using-tags.md).


### <a name="diagnose-and-solve-problems"></a>Diagnostica e risoluzione dei problemi

Fare clic su **diagnosticare e risolvere i problemi** toobe fornito con problemi comuni e le strategie per risolverli.



## <a name="settings"></a>Impostazioni
Hello **impostazioni** sezione per tooaccess e la configurazione seguente le impostazioni della cache di hello.

* [Chiavi di accesso](#access-keys)
* [Impostazioni avanzate](#advanced-settings)
* [Redis Cache Advisor](#redis-cache-advisor)
* [Ridimensionare](#scale)
* [Dimensione del cluster Redis](#cluster-size)
* [Persistenza dei dati Redis:](#redis-data-persistence)
* [Pianificare gli aggiornamenti](#schedule-updates)
* [Replica geografica](#geo-replication)
* [Rete virtuale](#virtual-network)
* [Firewall](#firewall)
* [Proprietà](#properties)
* [Blocchi](#locks)
* [Script di automazione](#automation-script)



### <a name="access-keys"></a>Chiavi di accesso
Fare clic su **le chiavi di accesso** accesso hello tooview o rigenerare le chiavi per la cache. Queste chiavi vengono utilizzate dai client hello tooyour cache di connessione.

![Chiavi di accesso di Cache Redis](./media/cache-configure/redis-cache-manage-keys.png)

### <a name="advanced-settings"></a>Impostazioni avanzate
Hello seguenti siano configurate su hello **impostazioni avanzate** blade.

* [Porte di accesso](#access-ports)
* [Criteri di memoria](#memory-policies)
* [Notifiche di Keyspace (impostazioni avanzate)](#keyspace-notifications-advanced-settings)

#### <a name="access-ports"></a>Porte di accesso
Per le nuove cache la porta senza SSL è disabilitata per impostazione predefinita. tooenable hello non SSL porta, fare clic su **n** per **consentire l'accesso solo tramite SSL** su hello **impostazioni avanzate** blade e quindi fare clic su **salvare**.

![Porte di accesso di Cache Redis](./media/cache-configure/redis-cache-access-ports.png)

<a name="maxmemory-policy-and-maxmemory-reserved"></a>
#### <a name="memory-policies"></a>Criteri di memoria
Hello **criteri di Maxmemory**, **riservato maxmemory**, e **riservato maxfragmentationmemory** impostazioni hello **Impostazioniavanzate**pannello configurare criteri di memoria hello per cache di hello.

![Criterio maxmemory di Cache Redis](./media/cache-configure/redis-cache-maxmemory-policy.png)

**Criteri di MaxMemory** consente di configurare i criteri di rimozione hello per cache di hello e consente toochoose da hello seguenti criteri di eliminazione:

* `volatile-lru`-si tratta hello predefinito.
* `allkeys-lru`
* `volatile-random`
* `allkeys-random`
* `volatile-ttl`
* `noeviction`

Per altre informazioni sui criteri `maxmemory`, vedere [Eviction policies](http://redis.io/topics/lru-cache#eviction-policies) (Criteri di rimozione).

Hello **riservato maxmemory** consente di configurare la quantità hello di memoria in MB è riservato per le operazioni non cache, ad esempio la replica durante il failover. Impostando questo valore consente un'esperienza più coerente di server Redis toohave quando il carico varia. Questo valore deve essere più alto per i carichi di lavoro ad intensa attività di scrittura. Quando la memoria è riservata per tali operazioni non è disponibile per l'archiviazione dei dati della cache.

Hello **riservato maxfragmentationmemory** consente di configurare la quantità hello di memoria in MB è tooaccommodate riservato per la frammentazione della memoria. Impostando questo valore consente un'esperienza più coerente di server Redis toohave quando la cache di hello è piena o Chiudi toofull e hello rapporto di frammentazione è elevata. Quando la memoria è riservata per tali operazioni non è disponibile per l'archiviazione dei dati della cache.

Tooconsider una cosa, quando si sceglie un nuovo valore di prenotazione di memoria (**riservato maxmemory** o **riservato maxfragmentationmemory**) è come questa modifica potrebbe influire su una cache che è già in esecuzione con grandi quantità di dati in essa contenuti. Ad esempio, se si dispone di una cache 53 GB con 49 GB di dati, modificare hello prenotazione valore too8 GB, questa verrà eliminata hello max la memoria disponibile per il sistema hello verso il basso too45 GB. Se il valore corrente `used_memory` oppure il `used_memory_rss` valori sono maggiori di nuovo limite di hello 45 GB, quindi sistema hello avrà tooevict dati fino a quando sia `used_memory` e `used_memory_rss` sono inferiori a 45 GB. La rimozione può aumentare il carico del server e la frammentazione della memoria. Per altre informazioni sulle metriche della cache come `used_memory` e `used_memory_rss` vedere [Available metrics and reporting intervals](cache-how-to-monitor.md#available-metrics-and-reporting-intervals) (Metriche disponibili e intervalli di report).

> [!IMPORTANT]
> Hello **riservato maxmemory** e **riservato maxfragmentationmemory** impostazioni sono disponibili solo per Standard e Premium memorizza nella cache.
> 
> 

#### <a name="keyspace-notifications-advanced-settings"></a>Notifiche di Keyspace (impostazioni avanzate)
Le notifiche sono configurate su hello spazio delle chiavi di redis **impostazioni avanzate** blade. Le notifiche di spazio delle chiavi consentono ai client tooreceive notifiche quando si verificano determinati eventi.

![Impostazioni avanzate di Cache Redis](./media/cache-configure/redis-cache-advanced-settings.png)

> [!IMPORTANT]
> Spazio delle chiavi le notifiche e hello **notifica eventi di spazio delle chiavi** impostazione sono disponibili solo per le cache Standard e Premium.
> 
> 

Per altre informazioni, vedere [Notifiche di Keyspace Redis](http://redis.io/topics/notifications). Per esempio di codice, vedere hello [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs) file hello [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) esempio.


<a name="recommendations"></a>
## <a name="redis-cache-advisor"></a>Redis Cache Advisor
Hello **Redis Cache Advisor** pannello Visualizza indicazioni per la cache. Durante il normale funzionamento non viene visualizzata nessuna raccomandazione. 

![Raccomandazioni](./media/cache-configure/redis-cache-no-recommendations.png)

Se tutte le condizioni si verificano durante le operazioni di hello della cache, ad esempio l'utilizzo elevato della memoria, larghezza di banda di rete o del carico del server, viene visualizzato un avviso su hello **Cache Redis** blade.

![Raccomandazioni](./media/cache-configure/redis-cache-recommendations-alert.png)

Per ulteriori informazioni possono trovarsi in hello **indicazioni** blade.

![Raccomandazioni](./media/cache-configure/redis-cache-recommendations.png)

È possibile monitorare queste metriche in hello [grafici di monitoraggio](cache-how-to-monitor.md#monitoring-charts) e [grafici relativi all'utilizzo](cache-how-to-monitor.md#usage-charts) sezioni di hello **Cache Redis** blade.

Ogni piano tariffario presenta diversi limiti di connessioni client, memoria e larghezza di banda. Se la cache rasenta la capacità massima di queste metriche per un periodo prolungato, viene creata una raccomandazione. Per ulteriori informazioni sulle metriche hello e limiti esaminati da hello **indicazioni** strumento, vedere hello nella tabella seguente:

| Metrica della cache Redis | Altre informazioni |
| --- | --- |
| Uso della larghezza di banda di rete |[Prestazioni della cache - Larghezza di banda disponibile](cache-faq.md#cache-performance) |
| Client connessi |[Configurazione predefinita del server Redis - maxclients](#maxclients) |
| Carico del server |[Grafici di utilizzo - Carico server Redis](cache-how-to-monitor.md#usage-charts) |
| Utilizzo della memoria |[Prestazioni della cache - Dimensioni](cache-faq.md#cache-performance) |

tooupgrade cache, fare clic su **Aggiorna** hello toochange livello di prezzo e [scala](#scale) la cache. Per altre informazioni su come scegliere un piano tariffario, vedere [Quali offerte e dimensioni della Cache Redis è consigliabile usare?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)


### <a name="scale"></a>Scalabilità
Fare clic su **scala** hello tooview o modificare piano tariffario per la cache. Per ulteriori informazioni sulla scalabilità, vedere [la modalità di Cache Redis di Azure di tooScale](cache-how-to-scale.md).

![Livello di prezzo di Cache Redis](./media/cache-configure/pricing-tier.png)

<a name="cluster-size"></a>

### <a name="redis-cluster-size"></a>Dimensione del cluster Redis
Fare clic su **dimensione del Cluster Redis (anteprima)** la cache di dimensione del cluster hello toochange un premio in esecuzione con clustering abilitato.

> [!NOTE]
> Si noti che mentre hello Azure Redis Cache Premium livello è stato rilasciato tooGeneral disponibilità, funzionalità di dimensioni del Cluster Redis hello sono attualmente in anteprima.
> 
> 

![Dimensione del cluster Redis](./media/cache-configure/redis-cache-redis-cluster-size.png)

dimensione del cluster toochange hello, utilizzare il dispositivo di scorrimento hello o digitare un numero compreso tra 1 e 10 hello **numero di partizioni** casella di testo e fare clic su **OK** toosave.

> [!IMPORTANT]
> Il clustering Redis è disponibile esclusivamente per le cache Premium. Per ulteriori informazioni, vedere [come tooconfigure clustering per una Cache Redis di Azure Premium](cache-how-to-premium-clustering.md).
> 
> 


### <a name="redis-data-persistence"></a>Persistenza dei dati Redis:
Fare clic su **persistenza dei dati Redis** tooenable, disabilitare o configurare la persistenza dei dati per la cache premium. Cache Redis di Azure offre la persistenza dei dati Redis tramite la [persistenza RDB](cache-how-to-premium-persistence.md#configure-rdb-persistence) o la [persistenza AOF](cache-how-to-premium-persistence.md#configure-aof-persistence).

Per ulteriori informazioni, vedere [come persistenza tooconfigure per una Cache Redis di Azure Premium](cache-how-to-premium-persistence.md).


> [!IMPORTANT]
> La persistenza dei dati Redis è disponibile solo per le cache Premium. 
> 
> 

### <a name="schedule-updates"></a>Pianificare gli aggiornamenti
Hello **pianificare aggiornamenti** pannello consente toodesignate una finestra di manutenzione per gli aggiornamenti server Redis per la cache. 

> [!IMPORTANT]
> finestra di manutenzione Hello si applica solo aggiornamenti di server tooRedis e tooany Azure aggiorna o aggiorna il sistema operativo toohello delle macchine virtuali di hello che ospitano una cache di hello.
> 
> 

![Pianificare gli aggiornamenti](./media/cache-configure/redis-schedule-updates.png)

toospecify una finestra di manutenzione, controllare i giorni hello desiderato e specificare l'ora di inizio finestra di manutenzione di hello per ogni giorno e fare clic su **OK**. Si noti che ora finestra di manutenzione hello è in formato UTC. 

> [!IMPORTANT]
> Hello **pianificare aggiornamenti** funzionalità è disponibile solo per le cache di livello Premium. Per altre informazioni e istruzioni, vedere [Come amministrare Cache Redis di Azure - Pianificare gli aggiornamenti](cache-administration.md#schedule-updates).
> 
> 

### <a name="geo-replication"></a>Replica geografica

Hello **-replica geografica** pannello fornisce un meccanismo per il collegamento di due istanze di Cache Redis di Azure di livello Premium. Una cache viene definita come cache collegato primario hello e altri come cache collegato secondaria hello hello. cache collegato secondaria Hello diventa di sola lettura e cache primaria toohello scritti i dati replicati cache collegato secondaria toohello. Questa funzionalità può essere utilizzato tooreplicate una cache nelle aree di Azure.

> [!IMPORTANT]
> **Replica geografica** è disponibile solo per le cache del piano Premium. Per ulteriori informazioni e istruzioni, vedere [come tooconfigure replica geografica per Cache Redis di Azure](cache-how-to-geo-replication.md).
> 
> 

### <a name="virtual-network"></a>Rete virtuale
Hello **rete virtuale** sezione consente di impostazioni della rete virtuale hello tooconfigure per la cache. Per informazioni sulla creazione di una cache premium con una rete virtuale supporta e aggiornamento delle impostazioni, vedere [come tooconfigure supporta la rete virtuale per una Cache Redis di Azure Premium](cache-how-to-premium-vnet.md).

> [!IMPORTANT]
> Le impostazioni della rete virtuale sono disponibili solo per le cache di livello Premium configurate con il supporto della rete virtuale durante la creazione della cache. 
> 
> 

### <a name="firewall"></a>Firewall

Fare clic su **Firewall** tooview e configurare le regole del firewall per la Cache Redis di Azure Premium.

![Firewall](./media/cache-configure/redis-firewall-rules.png)

È possibile specificare le regole del firewall con un intervallo di indirizzi IP iniziale e finale. Quando le regole del firewall sono configurate, solo le connessioni client da hello specificare intervalli di indirizzi IP possono connettersi toohello cache. Quando viene salvata di una regola del firewall è un breve ritardo prima regola hello è valida. Questo tempo è in genere meno di un minuto.

> [!IMPORTANT]
> Le connessioni dai sistemi di monitoraggio di Cache Redis di Azure sono sempre consentite, anche se le regole del firewall sono configurate.
> 
> Le regole del firewall sono disponibili solo per le cache del piano Premium.
> 
> 

### <a name="properties"></a>Proprietà
Fare clic su **proprietà** tooview informazioni sulla cache, incluse le porte ed endpoint della cache di hello.

![Proprietà di Cache Redis](./media/cache-configure/redis-cache-properties.png)

### <a name="locks"></a>Blocchi
Hello **blocca** sezione consente di toolock una sottoscrizione, gruppo di risorse o risorse tooprevent altri utenti nell'organizzazione da un'accidentale eliminazione o modifica di risorse critiche. Per altre informazioni, vedere [Bloccare le risorse con Gestione risorse di Azure](../azure-resource-manager/resource-group-lock-resources.md).

### <a name="automation-script"></a>Script di automazione

Fare clic su **script di automazione** toobuild ed esportare un modello di risorse distribuite per le distribuzioni future. Per altre informazioni sull'uso dei modelli, vedere [Distribuire le risorse con i modelli di Azure Resource Manager e Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="administration-settings"></a>Impostazioni di amministrazione
le impostazioni di hello Hello **amministrazione** sezione consentono di hello tooperform seguendo le attività amministrative per la cache. 

![Amministrazione](./media/cache-configure/redis-cache-administration.png)

* [Importazione dei dati](#importexport)
* [Esportazione dei dati](#importexport)
* [Reboot](#reboot)


### <a name="importexport"></a>Importazione/Esportazione
Importazione/esportazione è un'operazione di gestione di dati Cache Redis di Azure, che consente di tooimport ed esportare i dati nella cache di hello dall'importazione ed esportazione di uno snapshot del Database di Cache Redis (RDB) da un blob di pagine tooa cache premium in un Account di archiviazione di Azure. Importazione/esportazione consente toomigrate tra istanze diverse di Cache Redis di Azure o memorizzare nella cache di hello con i dati prima dell'uso.

Importazione può essere utilizzati toobring Redis compatibile RDB file da qualsiasi server Redis in esecuzione in qualsiasi cloud o di un ambiente, compresi Redis in esecuzione in Linux, Windows o di qualsiasi provider di cloud come Amazon Web Services e altre. Importazione di dati è un toocreate facilmente una cache con dati pre-popolati. Durante il processo di importazione hello Cache Redis di Azure Carica file RDB hello dall'archiviazione di Azure in memoria e quindi inserisce chiavi hello nella cache di hello.

Esporta consente dati hello tooexport archiviati nei file di Cache Redis di Azure tooRedis compatibili RDB. È possibile utilizzare i dati da una Cache Redis di Azure istanza tooanother o server Redis tooanother toomove funzionalità. Durante il processo di esportazione hello, viene creato un file temporaneo nella macchina virtuale che ospita hello istanza server di Cache Redis di Azure e file hello è caricato toohello definito account di archiviazione hello. Quando l'operazione di esportazione hello viene completato con stato di esito positivo o negativo, viene eliminato il file temporaneo hello.

> [!IMPORTANT]
> La funzionalità Importazione/Esportazione è disponibile solo per le cache del piano Premium. Per altre informazioni e istruzioni, vedere [Importare ed esportare dati in Cache Redis di Azure](cache-how-to-import-export-data.md).
> 
> 

### <a name="reboot"></a>Reboot
Hello **riavviare** pannello consente nodi hello tooreboot della cache. Questa funzionalità di riavvio consente si tootest all'applicazione per garantire la resilienza, se si verifica un errore di un nodo della cache.

![Reboot](./media/cache-configure/redis-cache-reboot.png)

Se si dispone di una cache premium con clustering abilitato, è possibile selezionare le partizioni di tooreboot cache di hello.

![Reboot](./media/cache-configure/redis-cache-reboot-cluster.png)

tooreboot uno o più nodi della cache, selezionare i nodi di hello desiderato e fare clic su **riavviare**. Se si dispone di una cache premium con clustering abilitato, selezionare tooreboot shard(s) hello e quindi fare clic su **riavviare**. Dopo alcuni minuti, hello il riavvio di nodi selezionato e sono in linea alcuni minuti in un secondo momento.

> [!IMPORTANT]
> Il riavvio ora è disponibile per tutti i piani tariffari. Per altre informazioni e istruzioni, vedere [Come amministrare Cache Redis di Azure - Riavvia](cache-administration.md#reboot).
> 
> 


## <a name="monitoring"></a>Monitoraggio

Hello **monitoraggio** sezione consente di tooconfigure diagnostica e monitoraggio per la Cache Redis. Per ulteriori informazioni sulla diagnostica e monitoraggio di Cache Redis di Azure, vedere [la modalità di Cache Redis di Azure di toomonitor](cache-how-to-monitor.md).

![Diagnostica](./media/cache-configure/redis-cache-diagnostics.png)

* [Metriche di Redis](#redis-metrics)
* [Regole di avviso](#alert-rules)
* [Diagnostica](#diagnostics)

### <a name="redis-metrics"></a>Metriche Redis
Fare clic su **Redis metriche** troppo[visualizzare le metriche](cache-how-to-monitor.md#view-cache-metrics) per la cache.

### <a name="alert-rules"></a>Regole di avviso

Fare clic su **regole di avviso** tooconfigure avvisi in base alle metriche di Cache Redis. Per altre informazioni, vedere [Avvisi](cache-how-to-monitor.md#alerts).

### <a name="diagnostics"></a>Diagnostica

Per impostazione predefinita, le metriche relative alla cache in Monitoraggio di Azure vengono [archiviate per 30 giorni](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive) e quindi vengono eliminate. Scegliere le metriche della cache per più di 30 giorni, toopersist **diagnostica** troppo[configurare account di archiviazione hello](cache-how-to-monitor.md#export-cache-metrics) utilizzato toostore della diagnostica della cache.

>[!NOTE]
>In aggiunta tooarchiving toostorage le metriche di cache, è anche possibile [trasmessi tooan hub di eventi o inviare loro tooLog Analitica](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).
>
>

## <a name="support--troubleshooting-settings"></a>Supporto e impostazioni di risoluzione dei problemi
le impostazioni di hello Hello **supporto + risoluzione dei problemi** sezione forniscono le opzioni per la risoluzione dei problemi con la cache.

![Supporto e risoluzione dei problemi](./media/cache-configure/redis-cache-support-troubleshooting.png)

* [Integrità delle risorse](#resource-health)
* [Nuova richiesta di supporto](#new-support-request)

### <a name="resource-health"></a>Integrità delle risorse
**Integrità risorsa** esamina la risorsa e indica se viene eseguita nel modo previsto. Per ulteriori informazioni su hello servizio di integrità delle risorse di Azure, vedere [Panoramica di integrità delle risorse di Azure](../resource-health/resource-health-overview.md).

> [!NOTE]
> Integrità delle risorse è attualmente in grado di tooreport integrità hello di istanze di Cache Redis di Azure ospitati in una rete virtuale. Per altre informazioni, vedere [Tutte le funzionalità della cache funzionano quando si ospita una cache in una rete virtuale?](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)
> 
> 

### <a name="new-support-request"></a>Nuova richiesta di supporto
Fare clic su **nuova richiesta di assistenza** tooopen una richiesta di supporto per la cache.





## <a name="default-redis-server-configuration"></a>Configurazione predefinita del server Redis
Nuova Cache Redis di Azure vengono configurate con hello seguente i valori predefiniti di configurazione di Redis.

> [!NOTE]
> impostazioni di Hello in questa sezione non possono essere modificate utilizzando hello `StackExchange.Redis.IServer.ConfigSet` metodo. Se questo metodo viene chiamato con uno dei comandi di hello in questa sezione, viene generata un' seguente toohello simile di eccezione:  
> 
> `StackExchange.Redis.RedisServerException: ERR unknown command 'CONFIG'`
> 
> I valori che sono configurabili, ad esempio **criteri di memoria max**, possono essere configurate tramite hello portale di Azure o gli strumenti di gestione della riga di comando, ad esempio CLI di Azure o PowerShell.
> 
> 

| Impostazione | Valore predefinito | Descrizione |
| --- | --- | --- |
| `databases` |16 |numero di database predefinito di Hello è 16, ma è possibile configurare un diverso numero hello in base a livello di prezzo. <sup>1</sup> database predefinito hello è DB 0, è possibile selezionare una diversa in ogni singola una connessione utilizzando `connection.GetDatabase(dbid)` in `dbid` è un numero compreso tra `0` e `databases - 1`. |
| `maxclients` |Dipende dal livello di prezzo hello<sup>2</sup> |Questo è hello il numero massimo di client connessi in hello stesso tempo. Quando viene raggiunto il limite di hello Redis chiude tutte le nuove connessioni a hello, restituendo un errore di 'numero massimo di client raggiunto'. |
| `maxmemory-policy` |`volatile-lru` |Criteri di MaxMemory sono l'impostazione di hello per la modalità di selezione quali tooremove Redis quando `maxmemory` viene raggiunta (hello dimensione della cache di hello offerta selezionato al momento della creazione della cache di hello). Impostazione predefinita di hello Cache Redis di Azure è `volatile-lru`, che rimuove le chiavi di hello con una scadenza impostata mediante l'algoritmo LRU. Questa impostazione può essere configurata in hello portale di Azure. Per altre informazioni, vedere [Criteri di memoria](#memory-policies). |
| `maxmemory-samples` |3 |memoria toosave, LRU e algoritmi TTL minimo sono algoritmi approssimativa anziché precisi. Per impostazione predefinita Redis controlli tre chiavi e i prelievi hello uno utilizzati meno recente. |
| `lua-time-limit` |5.000 |Tempo massimo di esecuzione di uno script Lua in millisecondi. Se viene raggiunto il tempo di esecuzione massimo hello, Redis registra uno script è ancora in esecuzione dopo hello massimo consentito di tempo che inizia tooreply tooqueries con un errore. |
| `lua-event-limit` |500 |Dimensione massima della coda di eventi di script. |
| `client-output-buffer-limit` `normalclient-output-buffer-limit` `pubsub` |0 0 032mb 8mb 60 |Hello i limiti del buffer di output di client possono essere utilizzato tooforce disconnessione dei client che non leggono i dati dal server hello sufficientemente veloce per qualche motivo (una causa comune è che un client di pubblicazione/sottoscrizione non può utilizzare la stessa velocità pubblicazione hello può produrre tali messaggi). Per altre informazioni, vedere [http://redis.io/topics/clients](http://redis.io/topics/clients). |

<a name="databases"></a>
<sup>1</sup>limite hello per `databases` è diverso per Azure Redis Cache di ogni livello di prezzo e può essere impostato al momento della creazione della cache. Se non `databases` impostazione viene specificato durante la creazione della cache predefinita hello è 16.

* Cache di base e Standard
  * C0 cache (250 MB): Backup database too16
  * C1 cache (1 GB) - backup di database too16
  * C2 cache (2,5 GB) - backup di database too16
  * C3 cache (6 GB) - backup di database too16
  * C4 cache (13 GB) - backup di database too32
  * C5 cache (26 GB) - backup di database too48
  * C6 cache (53 GB) - backup di database too64
* Cache Premium
  * P1 (6 GB - 60 GB) - backup di database too16
  * P2 (13 GB - 130 GB) - backup di database too32
  * P3 (26 GB - 260 GB) - backup di database too48
  * P4 (53 GB - 530 GB) - backup di database too64
  * Tutte le cache premium con cluster Redis abilitata - Redis cluster supporta solo l'uso di database 0 hello in modo `databases` limitare per tutte le cache premium con cluster Redis abilitata in modo efficace è di 1 e hello [selezionare](http://redis.io/commands/select) comando non è consentito. Per ulteriori informazioni, vedere [devo toomake qualsiasi toouse applicazione di modifiche toomy client clustering?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)

Per altre informazioni sui database SQL di Azure, vedere [What are Redis databases?](cache-faq.md#what-are-redis-databases) (Cosa sono i database Redis?)

> [!NOTE]
> Hello `databases` impostazione può essere configurata solo durante la creazione della cache e solo tramite PowerShell, CLI o altri client di gestione. Per un esempio di configurazione di `databases` durante la creazione della cache con PowerShell, vedere [New-AzureRmRedisCache](cache-howto-manage-redis-cache-powershell.md#databases).
> 
> 

<a name="maxclients"></a>
<sup>2</sup>Il valore di `maxclients` è diverso per ogni piano tariffario di Cache Redis di Azure.

* Cache di base e Standard
  * C0 cache (250 MB): le connessioni too256
  * C1 cache (1 GB) - backup too1, connessioni 000
  * C2 cache (2,5 GB) - backup too2, connessioni 000
  * C3 cache (6 GB) - backup too5, connessioni 000
  * C4 cache (13 GB) - backup too10, connessioni 000
  * C5 cache (26 GB) - backup too15, connessioni 000
  * C6 cache (53 GB) - backup too20, connessioni 000
* Cache Premium
  * P1 (6 GB - 60 GB) - backup too7, connessioni a 500
  * P2 (13 GB - 130 GB) - backup too15, connessioni 000
  * P3 (26 GB - 260 GB) - backup too30, connessioni 000
  * P4 (53 GB - 530 GB) - backup too40, connessioni 000

> [!NOTE]
> Mentre ogni dimensione della cache consente *fino a* un determinato numero di connessioni, ogni tooRedis connessione overhead è associato. Un esempio di questo sovraccarico potrebbe essere l'utilizzo della CPU e della memoria a causa della crittografia TLS/SSL. limite massimo di connessioni Hello per una dimensione della cache specificata si presuppone una cache con caricata ridotto. Se caricare dall'overhead connessione *più* carico dalle operazioni client supera la capacità di sistema di hello, cache di hello possa verificarsi problemi di capacità, anche se non è stato superato il limite di connessioni hello per la dimensione corrente della cache di hello.
> 
> 



## <a name="redis-commands-not-supported-in-azure-redis-cache"></a>Comandi di Redis non supportati in Cache Redis di Azure
> [!IMPORTANT]
> Poiché configurazione e gestione delle istanze di Cache Redis di Azure viene gestito da Microsoft, hello comandi seguenti sono disabilitati. Se si tenta di tooinvoke loro, viene visualizzato un messaggio di errore simile troppo`"(error) ERR unknown command"`.
> 
> * BGREWRITEAOF
> * BGSAVE
> * CONFIG
> * DEBUG
> * MIGRATE
> * Salva
> * SHUTDOWN
> * SLAVEOF
> * CLUSTER: i comandi di scrittura del cluster sono disabilitati, ma i comandi del cluster di sola lettura sono consentiti.
> 
> 

Per ulteriori informazioni sui comandi di Redis, vedere [http://redis.io/commands](http://redis.io/commands).

## <a name="redis-console"></a>Console Redis
In modo sicuro è possibile emettere comandi tooyour le istanze di Cache Redis di Azure utilizzando hello **Console Redis**, disponibile nel portale di Azure per tutti i livelli di cache di hello.

> [!IMPORTANT]
> - Hello Console Redis non funziona con [rete virtuale](cache-how-to-premium-vnet.md). Quando la cache fa parte di una rete virtuale, solo i client nella rete virtuale hello possono accedere cache di hello. La Console Redis viene eseguita nel browser locale, non è compreso hello rete virtuale, non è possibile connettersi tooyour cache.
> - Non tutti i comandi di Redis sono supportati in Cache Redis di Azure. Per un elenco di comandi di Redis che sono disabilitate per Cache Redis di Azure, vedere hello precedente [comandi non supportati in Cache Redis di Azure Redis](#redis-commands-not-supported-in-azure-redis-cache) sezione. Per ulteriori informazioni sui comandi di Redis, vedere [http://redis.io/commands](http://redis.io/commands).
> 
> 

hello tooaccess Console Redis, fare clic su **Console** da hello **Cache Redis** blade.

![Console Redis](./media/cache-configure/redis-console-menu.png)

comandi tooissue contro l'istanza di cache, semplicemente hello di tipo desiderato comando nella console di hello.

![Console Redis](./media/cache-configure/redis-console.png)


### <a name="using-hello-redis-console-with-a-premium-clustered-cache"></a>Utilizzando hello cache Redis Console con un premio cluster

Quando con un premio di hello Console Redis cache del cluster, è possibile eseguire una singola partizione tooa comandi della cache di hello. tooissue una partizione specifica tooa di comando, connettersi innanzitutto partizione desiderata toohello facendo doppio clic sul selettore di partizioni hello.

![Console Redis](./media/cache-configure/redis-console-premium-cluster.png)

Se si tenta di tooaccess una chiave archiviata in una partizione diversa rispetto a hello partizioni connesso, verrà visualizzato un toohello simile messaggio di errore seguente messaggio.

```
shard1>get myKey
(error) MOVED 866 13.90.202.154:13000 (shard 0)
```

Nell'esempio precedente hello partizione 1 è partizione selezionata hello, ma `myKey` si trova nella partizione 0, come indicato dal hello `(shard 0)` parte del messaggio di errore hello. In questo esempio, tooaccess `myKey`, selezionare 0 partizioni utilizzando hello selezione partizioni e quindi problema hello desiderato del comando.


## <a name="move-your-cache-tooa-new-subscription"></a>Spostare la nuova sottoscrizione tooa di cache
È possibile spostare la nuova sottoscrizione di tooa cache facendo **spostare**.

![Spostare la cache Redis](./media/cache-configure/redis-cache-move.png)

Per informazioni sullo spostamento di risorse da una risorsa gruppo tooanother e da una sottoscrizione tooanother, vedere [spostare sottoscrizione o il gruppo di risorse toonew risorse](../azure-resource-manager/resource-group-move-resources.md).

## <a name="next-steps"></a>Passaggi successivi
* Per altre informazioni sull'uso dei comandi di Redis, vedere [Come è possibile eseguire i comandi di Redis?](cache-faq.md#how-can-i-run-redis-commands)

