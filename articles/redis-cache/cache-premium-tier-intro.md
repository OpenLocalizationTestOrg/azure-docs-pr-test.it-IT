---
title: livello di Azure Redis Cache Premium toohello aaaIntroduction | Documenti Microsoft
description: Informazioni su come toocreate e gestire la persistenza di Redis, Redis clustering e il supporto di rete virtuale per le istanze di Cache Redis di Azure di livello Premium
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 30f46f9f-e6ec-4c38-a8cc-f9d4444856e5
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: sdanie
ms.openlocfilehash: 5b58a03647fbf1198509ac6f1acd04f1b682ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-azure-redis-cache-premium-tier"></a>Livello di introduzione toohello Premium di Cache Redis di Azure
Cache Redis di Azure è una cache distribuita e gestita che consente di compilare applicazioni estremamente scalabili e reattive fornendo i dati di un accesso velocissimo tooyour. 

Hello che nuovo di livello Premium è un livello di pronto dell'organizzazione, che include tutte le funzionalità di livello Standard hello e altro ancora, ad esempio prestazioni migliori, i carichi di lavoro più grande, il ripristino di emergenza, importazione/esportazione e la sicurezza avanzata. Continuare la lettura toolearn ulteriori informazioni sulle funzionalità aggiuntive di hello del livello di cache di hello Premium.

## <a name="better-performance-compared-toostandard-or-basic-tier"></a>Prestazioni migliori rispetto a tooStandard o livello Basic
**Prestazioni migliori a livello Standard o di base.** Cache nel livello Premium hello vengono distribuiti nell'hardware che dispone di processori più veloci e offre migliori prestazioni rispetto toohello, Basic o livello Standard. Le cache di livello Premium offrono una velocità effettiva più elevata e minori latenze. 

**Velocità effettiva per hello stessa Cache con dimensione è maggiore in Premium come livello tooStandard confrontati.** Ad esempio, velocità effettiva di hello di un 53 GB P4 cache (Premium) è 250K richieste al secondo come too150K confrontati per C6 (Standard).

Per maggiori informazioni su dimensioni, velocità e larghezza di banda con le cache Premium, vedere [Domande frequenti sulla Cache Redis di Azure](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)

## <a name="redis-data-persistence"></a>Persistenza dei dati Redis:
livello Premium Hello permette di dati della cache di hello toopersist in un account di archiviazione di Azure. In una cache Basic/Standard tutti i dati di hello viene archiviata solo in memoria. In caso di problemi per l'infrastruttura sottostante esiste il rischio di una potenziale perdita di dati. È consigliabile utilizzare funzionalità di persistenza dei dati Redis hello hello Premium livello tooincrease resilienza perdita di dati. Cache Redis di Azure offre le opzioni RDB e AOF (presto disponibile) per la [Persistenza di Redis](http://redis.io/topics/persistence). 

Per istruzioni sulla configurazione della persistenza, vedere [come persistenza tooconfigure per una Cache Redis di Azure Premium](cache-how-to-premium-persistence.md).

## <a name="redis-cluster"></a>Cluster Redis
Se si desidera toocreate cache maggiore a 53 GB o tooshard dati tra più nodi di Redis, è possibile utilizzare il clustering disponibile nel livello Premium hello Redis. Ogni nodo è costituito da una coppia di cache primaria/di replica gestita da Azure per la disponibilità elevata. 

**Il clustering di Redis consente scalabilità e velocità effettiva di alto livello.** Aumento della velocità effettiva in modo lineare man mano che aumenta il numero di hello di partizioni (nodi) in cluster hello. ed esempio Se si crea un cluster P4 di 10 partizioni e velocità effettiva disponibile hello è 250K * 10 = 2,5 milioni di richieste al secondo. Vedere hello [Azure Redis Cache FAQ](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) per ulteriori informazioni sulle dimensioni, velocità effettiva e la larghezza di banda con cache premium.

tooget avviato con il clustering, vedere [come tooconfigure clustering per una Cache Redis di Azure Premium](cache-how-to-premium-clustering.md).

## <a name="enhanced-security-and-isolation"></a>Isolamento e protezione avanzata
Cache create nel livello Basic o Standard hello siano accessibili in hello rete internet pubblica. Toohello di accesso che della Cache è limitata in base a una chiave di accesso hello. Con livello di hello Premium è possibile garantire ulteriormente accessibile solo ai client all'interno di una rete specificata hello Cache. È possibile distribuire Cache Redis in una [rete virtuale di Azure (VNet)](https://azure.microsoft.com/services/virtual-network/). È possibile utilizzare tutte le funzionalità di hello di rete virtuale, ad esempio subnet, criteri di controllo di accesso e altre funzionalità toofurther limitare l'accesso tooRedis.

Per ulteriori informazioni, vedere [la modalità di supporto tooconfigure rete virtuale per una Cache Redis di Azure Premium](cache-how-to-premium-vnet.md).

## <a name="importexport"></a>Importazione/Esportazione
Importazione/esportazione è un'operazione di gestione dati di Cache Redis di Azure che consente tooimport dati in Cache Redis di Azure o esportare i dati dalla Cache Redis di Azure mediante l'importazione e l'esportazione di uno snapshot del Database di Cache Redis (RDB) da un blob di pagine tooa cache premium in di Azure Account di archiviazione. Questo consente toomigrate tra istanze diverse di Cache Redis di Azure o memorizzare nella cache di hello con i dati prima dell'uso.

Importazione può essere utilizzato toobring Redis compatibile RDB file da qualsiasi server Redis in esecuzione in qualsiasi cloud o di un ambiente, compresi Redis in esecuzione in Linux, Windows o di qualsiasi provider di cloud come Amazon Web Services e altre. Importazione di dati è un toocreate facilmente una cache con dati pre-popolati. Durante il processo di importazione hello Cache Redis di Azure Carica file RDB hello dall'archiviazione di Azure in memoria e quindi inserisce chiavi hello nella cache di hello.

Esporta consente dati hello tooexport archiviati nei file di Cache Redis di Azure tooRedis compatibili RDB. È possibile utilizzare i dati da una Cache Redis di Azure istanza tooanother o server Redis tooanother toomove funzionalità. Durante il processo di esportazione hello, viene creato un file temporaneo nella macchina virtuale che ospita hello istanza server di Cache Redis di Azure e file hello è caricato toohello definito account di archiviazione hello. Quando l'operazione di esportazione hello viene completato con stato di esito positivo o negativo, viene eliminato il file temporaneo hello.

Per ulteriori informazioni, vedere [come dati tooimport ed esportare i dati dalla Cache Redis di Azure](cache-how-to-import-export-data.md).

## <a name="reboot"></a>Reboot
livello premium Hello consente tooreboot uno o più nodi della cache su richiesta. In questo modo è tootest l'applicazione per garantire la resilienza in caso di hello di un errore. È possibile riavviare i seguenti nodi hello.

* Nodo principale della cache
* Nodo slave della cache
* Nodi principali e slave della cache
* Quando si usa una cache premium con il clustering, è possibile riavviare hello master, secondario o entrambi i nodi per singole partizioni nella cache di hello

Per altre informazioni, vedere [Riavvia](cache-administration.md#reboot) e [Domande frequenti sulla funzionalità di riavvio](cache-administration.md#reboot-faq).

>[!NOTE]
>Il riavvio della funzionalità è ora abilitato per tutti i livelli di Cache Redis di Azure.
>
>

## <a name="schedule-updates"></a>Pianificare gli aggiornamenti
funzionalità di aggiornamenti pianificati Hello consente toodesignate una finestra di manutenzione per la cache. Quando la finestra di manutenzione hello è specificata, vengono eseguiti tutti gli aggiornamenti server Redis durante questa finestra. toodesignate una finestra di manutenzione, selezionare i giorni di hello desiderato e specificare l'ora di inizio finestra di manutenzione di hello per ogni giorno. Si noti che ora finestra di manutenzione hello è in formato UTC. 

Per altre informazioni, vedere [Pianificare gli aggiornamenti](cache-administration.md#schedule-updates) e [Domande frequenti sulla pianificazione degli aggiornamenti](cache-administration.md#schedule-updates-faq).

> [!NOTE]
> Redis solo gli aggiornamenti vengono eseguiti durante la finestra di manutenzione pianificata hello server. finestra di manutenzione Hello non applicare gli aggiornamenti di tooAzure o aggiorna toohello macchina virtuale del sistema operativo.
> 
> 

## <a name="geo-replication"></a>Replica geografica

La **replica geografica** fornisce un meccanismo per il collegamento di due istanze di Cache Redis di Azure di livello Premium. Una cache viene definita come cache collegato primario hello e altri come cache collegato secondaria hello hello. cache collegato secondaria Hello diventa di sola lettura e cache primaria toohello scritti i dati replicati cache collegato secondaria toohello. Questa funzionalità può essere utilizzato tooreplicate una cache nelle aree di Azure.

Per ulteriori informazioni, vedere [come tooconfigure replica geografica per Cache Redis di Azure](cache-how-to-geo-replication.md).


## <a name="tooscale-toohello-premium-tier"></a>livello di tooscale toohello premium
livello premium toohello tooscale semplicemente scegliere uno dei livelli premium hello hello **Modifica livello di prezzo** blade. È anche possibile ridimensionare il livello premium toohello di cache tramite PowerShell e CLI. Per istruzioni dettagliate, vedere [la modalità di Cache Redis di Azure di tooScale](cache-how-to-scale.md) e [come un'operazione di ridimensionamento tooautomate](cache-how-to-scale.md#how-to-automate-a-scaling-operation).

## <a name="next-steps"></a>Passaggi successivi
Creare una cache ed esplorare nuove funzionalità di livello premium hello.

* [Come la persistenza tooconfigure per una Cache Redis di Azure Premium](cache-how-to-premium-persistence.md)
* [La modalità di supporto tooconfigure rete virtuale per una Cache Redis di Azure Premium](cache-how-to-premium-vnet.md)
* [Come tooconfigure clustering per una Cache Redis di Azure Premium](cache-how-to-premium-clustering.md)
* [Come dati tooimport ed esportare i dati dalla Cache Redis di Azure](cache-how-to-import-export-data.md)
* [La modalità di Cache Redis di Azure di tooadminister](cache-administration.md)

