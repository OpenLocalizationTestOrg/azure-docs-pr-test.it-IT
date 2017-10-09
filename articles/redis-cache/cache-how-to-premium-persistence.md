---
title: persistenza dei dati per una Cache Redis di Azure Premium aaaHow tooconfigure
description: Informazioni su come tooconfigure e gestire le istanze di Cache Redis di Azure di livello Premium di persistenza dei dati
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: b01cf279-60a0-4711-8c5f-af22d9540d38
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: sdanie
ms.openlocfilehash: 62feb6f5522e0270487f045eb303bf852434143d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-data-persistence-for-a-premium-azure-redis-cache"></a>Come tooconfigure persistenza dei dati per una Cache Redis di Azure Premium
Cache Redis di Azure ha diverse offerte di cache che forniscono flessibilità nella scelta di hello della dimensione della cache e le funzionalità, incluse le funzionalità di livello Premium, ad esempio clustering, persistenza e il supporto di rete virtuale. In questo articolo viene descritto come persistenza tooconfigure in premium Azure Redis Cache istanza.

Per informazioni su altre funzionalità di cache premium, vedere [livello Premium di Cache Redis di Azure di introduzione toohello](cache-premium-tier-intro.md).

## <a name="what-is-data-persistence"></a>Che cos'è la persistenza dei dati?
[Persistenza di redis](https://redis.io/topics/persistence) consente dati toopersist memorizzati in Redis. È anche possibile acquisire snapshot, eseguire il backup dei dati di hello, che è possibile caricare in caso di errore hardware. Si tratta di un enorme vantaggio rispetto Basic o livello Standard in cui tutti hello dati verrà archiviato in memoria e può essere presente una perdita di dati in caso di errore in cui i nodi della Cache sono inattivi. 

Cache Redis di Azure offre Redis persistenza utilizzando i modelli di hello:

* **Persistenza RDB** -persistenza quando RDB (database Redis) è configurata, Cache Redis di Azure mantiene uno snapshot della cache Redis hello in un formato binario toodisk in base a una frequenza di backup configurabile di Redis. Se si verifica un errore irreversibile che disabilita hello primario sia della cache di replica, viene ricostruita cache di hello utilizzando snapshot più recente di hello. Altre informazioni su hello [vantaggi](https://redis.io/topics/persistence#rdb-advantages) e [svantaggi](https://redis.io/topics/persistence#rdb-disadvantages) di persistenza RDB.
* **Persistenza AOF** -persistenza quando AOF (Append solo file) sia configurata, Cache Redis di Azure vengono salvati ogni log tooa operazioni di scrittura che viene salvato almeno una volta al secondo in un account di archiviazione di Azure. Se si verifica un errore irreversibile che disabilita hello primario sia della cache di replica, cache di hello verrà ricostruita tramite operazioni di scrittura hello archiviato. Altre informazioni su hello [vantaggi](https://redis.io/topics/persistence#aof-advantages) e [svantaggi](https://redis.io/topics/persistence#aof-disadvantages) di persistenza AOF.

Persistenza verrà configurata dall'hello **nuova Cache Redis** pannello durante la creazione della cache e hello **menu Resource** per premium esistente memorizza nella cache.

[!INCLUDE [redis-cache-create](../../includes/redis-cache-premium-create.md)]

Dopo aver selezionato un piano tariffario Premium, fare clic su **Persistenza Redis**.

![Persistenza Redis][redis-cache-persistence]

Hello nella sezione successiva hello viene descritta la modalità tooconfigure persistenza Redis nella nuova cache premium. Una volta configurata la persistenza di Redis, fare clic su **crea** toocreate premium la nuova cache con Redis persistenza.

## <a name="enable-redis-persistence"></a>Abilitare la persistenza Redis

Redis è attivata la persistenza in hello **Redis persistenza dei dati** pannello scegliendo **RDB** o **AOF** persistenza. Per le nuove cache, questo pannello avviene durante il processo di creazione della cache di hello, come descritto nella sezione precedente hello. Per le cache esistente, hello **Redis persistenza dei dati** pannello è accessibile da hello **menu Resource** per la cache.

![Impostazioni di Redis][redis-cache-settings]


## <a name="configure-rdb-persistence"></a>Configurare la persistenza RDB

persistenza RDB tooenable, fare clic su **RDB**. persistenza RDB toodisable in una cache premium abilitato in precedenza, fare clic su **disabilitato**.

![Persistenza RDB di Redis][redis-cache-rdb-persistence]

tooconfigure hello l'intervallo di backup, seleziona un **frequenza di Backup** dall'elenco a discesa hello. Le opzioni disponibili includono **15 minuti**, **30 minuti**, **60 minuti**, **6 ore**, **12 ore** e **24 ore**. Questo intervallo inizia a contare verso il basso, dopo il completamento dell'operazione di backup precedente hello e quando trascorso un nuovo backup viene avviato.

Fare clic su **Account di archiviazione** tooselect hello toouse account di archiviazione e scegliere uno hello **chiave primaria** o **chiave secondaria** toouse da hello **archiviazione Chiave** elenco a discesa. È necessario scegliere un account di archiviazione in hello stessa area della cache di hello e un **archiviazione Premium** account è consigliato perché l'archiviazione premium ha una velocità effettiva. 

> [!IMPORTANT]
> Se la chiave di archiviazione hello per l'account di persistenza viene rigenerata, è necessario riconfigurare chiave desiderato hello hello **chiave di archiviazione** elenco a discesa.
> 
> 

Fare clic su **OK** configurazione di persistenza toosave hello.

backup successivo Hello (o il primo backup per le nuove cache) è stato avviato una volta allo scadere dell'intervallo di frequenza di backup hello.

## <a name="configure-aof-persistence"></a>Configurare la persistenza AOF

persistenza AOF tooenable, fare clic su **AOF**. persistenza AOF toodisable in una cache premium abilitato in precedenza, fare clic su **disabilitato**.

![Persistenza AOF di Redis][redis-cache-aof-persistence]

persistenza AOF tooconfigure, specificare un **primo Account di archiviazione**. Questo account di archiviazione deve trovarsi in hello stessa area della cache di hello e un **archiviazione Premium** account è consigliato perché l'archiviazione premium ha una velocità effettiva. Facoltativamente, è possibile configurare un account di archiviazione aggiuntivo denominato **secondo account di archiviazione**. Se è configurato un secondo account di archiviazione, hello scritture toohello replica cache vengono scritti toothis secondo account di archiviazione. Per ogni account di archiviazione configurato, scegliere uno hello **chiave primaria** o **chiave secondaria** toouse da hello **chiave di archiviazione** elenco a discesa. 

> [!IMPORTANT]
> Se la chiave di archiviazione hello per l'account di persistenza viene rigenerata, è necessario riconfigurare chiave desiderato hello hello **chiave di archiviazione** elenco a discesa.
> 
> 

Quando è abilitata la persistenza AOF, scrivere cache toohello operazioni vengono salvati toohello definito account di archiviazione (o se è stato configurato un secondo account di archiviazione di account). Nell'evento di hello di un errore irreversibile che accetta verso il basso sia hello primario e cache di replica, hello stored AOF log è utilizzata della cache di hello toorebuild.

## <a name="persistence-faq"></a>Domande frequenti sulla persistenza
Hello elenco seguente contiene le risposte toocommonly domande frequenti su persistenza Cache Redis di Azure.

* [È possibile abilitare la persistenza per una cache creata in precedenza?](#can-i-enable-persistence-on-a-previously-created-cache)
* [È possibile abilitare la persistenza AOF e RDB in hello contemporaneamente?](#can-i-enable-aof-and-rdb-persistence-at-the-same-time)
* [Quale modello di persistenza è consigliabile scegliere?](#which-persistence-model-should-i-choose)
* [Cosa accade se è stato ridimensionato tooa diverse dimensioni e viene ripristinato un backup effettuato prima che l'operazione di ridimensionamento hello?](#what-happens-if-i-have-scaled-to-a-different-size-and-a-backup-is-restored-that-was-made-before-the-scaling-operation)


### <a name="rdb-persistence"></a>Persistenza RDB
* [È possibile modificare la frequenza di backup RDB hello dopo che è possibile creare cache di hello?](#can-i-change-the-rdb-backup-frequency-after-i-create-the-cache)
* [Perché trascorrono più di 60 minuti tra i backup se è stata impostata una frequenza di backup RDB di 60 minuti?](#why-if-i-have-an-rdb-backup-frequency-of-60-minutes-there-is-more-than-60-minutes-between-backups)
* [Backup RDB precedenti toohello cosa accade quando viene effettuato un nuovo backup?](#what-happens-to-the-old-rdb-backups-when-a-new-backup-is-made)

### <a name="aof-persistence"></a>Persistenza AOF
* [Quando è consigliabile usare un secondo account di archiviazione?](#when-should-i-use-a-second-storage-account)
* [La persistenza AOF influisce sulla velocità effettiva, la latenza o le prestazioni della cache?](#does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache)
* [Come è possibile rimuovere l'account di archiviazione secondo hello?](#how-can-i-remove-the-second-storage-account)
* [Che cos'è un'operazione di riscrittura e in che modo influisce sulla cache?](#what-is-a-rewrite-and-how-does-it-affect-my-cache)
* [Quali potrebbero essere gli effetti del ridimensionamento di una cache con la persistenza AOF abilitata?](#what-should-i-expect-when-scaling-a-cache-with-aof-enabled)
* [Come vengono organizzati i dati AOF nello spazio di archiviazione?](#how-is-my-aof-data-organized-in-storage)


### <a name="can-i-enable-persistence-on-a-previously-created-cache"></a>È possibile abilitare la persistenza per una cache creata in precedenza?
Sì, la persistenza di Redis può essere configurata sia al momento della creazione della cache che nelle cache premium esistenti.

### <a name="can-i-enable-aof-and-rdb-persistence-at-hello-same-time"></a>È possibile abilitare la persistenza AOF e RDB in hello contemporaneamente?

No, è possibile abilitare solo RDB o AOF, ma non entrambe contemporaneamente hello contemporaneamente.

### <a name="which-persistence-model-should-i-choose"></a>Quale modello di persistenza è consigliabile scegliere?

Persistenza AOF Salva log di tooa ogni scrittura, che ha un impatto sulla velocità effettiva, confrontato con RDB della persistenza Salva i backup in base a hello configurato l'intervallo di backup, con un impatto minimo sulle prestazioni. Scegliere la persistenza AOF se l'obiettivo principale è la perdita di dati toominimize, ed è possibile gestire una diminuzione della velocità effettiva per la cache. Se si desidera che la velocità effettiva ottimale toomaintain nella cache, ma si desidera comunque un meccanismo per il ripristino dei dati, scegliere la persistenza del RDB.

* Altre informazioni su hello [vantaggi](https://redis.io/topics/persistence#rdb-advantages) e [svantaggi](https://redis.io/topics/persistence#rdb-disadvantages) di persistenza RDB.
* Altre informazioni su hello [vantaggi](https://redis.io/topics/persistence#aof-advantages) e [svantaggi](https://redis.io/topics/persistence#aof-disadvantages) di persistenza AOF.

Per altre informazioni sulle prestazioni quando si usa la persistenza AOF, vedere [La persistenza AOF influisce sulla velocità effettiva, la latenza o le prestazioni della cache?](#does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache)

### <a name="what-happens-if-i-have-scaled-tooa-different-size-and-a-backup-is-restored-that-was-made-before-hello-scaling-operation"></a>Cosa accade se è stato ridimensionato tooa diverse dimensioni e viene ripristinato un backup effettuato prima che l'operazione di ridimensionamento hello?

Per la persistenza sia RDB sia AOF:

* Se le prestazioni tooa di dimensioni maggiore, non vi è alcun impatto.
* Se le prestazioni tooa di dimensioni inferiore e si dispone di un oggetto personalizzato [database](cache-configure.md#databases) l'impostazione che è maggiore di hello [database limite](cache-configure.md#databases) per la nuova dimensione, non ripristinare i dati in tali database. Per altre informazioni, vedere [L'impostazione databases personalizzata viene modificata durante il ridimensionamento?](cache-how-to-scale.md#is-my-custom-databases-setting-affected-during-scaling)
* Se le prestazioni tooa di dimensioni inferiore e non è disponibile spazio sufficiente in hello toohold di dimensioni più piccole tutti i dati di hello dalle chiavi di backup, ultimo hello di eliminazione durante il processo di ripristino di hello, in genere utilizzando hello [allkeys lru](http://redis.io/topics/lru-cache) rimozione criteri.

### <a name="can-i-change-hello-rdb-backup-frequency-after-i-create-hello-cache"></a>È possibile modificare la frequenza di backup RDB hello dopo che è possibile creare cache di hello?
Sì, è possibile modificare la frequenza di backup hello per la persistenza RDB su hello **Redis persistenza dei dati** blade. Per istruzioni, vedere [Configurare la persistenza di Redis](#configure-redis-persistence).

### <a name="why-if-i-have-an-rdb-backup-frequency-of-60-minutes-there-is-more-than-60-minutes-between-backups"></a>Perché trascorrono più di 60 minuti tra i backup se è stata impostata una frequenza di backup RDB di 60 minuti?
intervallo di frequenza di backup di Hello RDB persistenza per avviare il processo di backup precedente di hello è stata completata. Se la frequenza di backup hello è di 60 minuti e accetta toosuccessfully di 15 minuti un processo di backup completo, non si avvia backup successivo hello fino a quando non 75 minuti dopo hello ora di inizio del backup precedente hello.

### <a name="what-happens-toohello-old-rdb-backups-when-a-new-backup-is-made"></a>Backup RDB precedenti toohello cosa accade quando viene effettuato un nuovo backup?
Tutti i backup di persistenza RDB ad eccezione di hello più recente vengono eliminati automaticamente. L'eliminazione potrebbe non avvenire immediatamente, ma i backup meno recenti non vengono mantenuti per un tempo illimitato.


### <a name="when-should-i-use-a-second-storage-account"></a>Quando è consigliabile usare un secondo account di archiviazione?

Utilizzare un secondo account di archiviazione per la persistenza AOF quando si ritiene che si dispone di maggiore rispetto alle operazioni della cache di hello set previsto.  Impostazione di account di archiviazione secondaria hello contribuisce a garantire che la cache non raggiunga i limiti di larghezza di banda di archiviazione.

### <a name="does-aof-persistence-affect-throughout-latency-or-performance-of-my-cache"></a>La persistenza AOF influisce sulla velocità effettiva, la latenza o le prestazioni della cache?

Persistenza AOF influisce sulla velocità effettiva da circa 15-20% quando la cache di hello è sotto carico massimo (CPU e carico del Server sia inferiore al 90%). Deve essere presente problemi di latenza quando la cache di hello è all'interno di questi limiti. Tuttavia, cache di hello raggiungerà questi limiti prima con AOF abilitato.

### <a name="how-can-i-remove-hello-second-storage-account"></a>Come è possibile rimuovere l'account di archiviazione secondo hello?

È possibile rimuovere l'account di archiviazione secondaria di hello AOF persistenza impostando hello secondo account di archiviazione toobe stesso hello come primo account di archiviazione hello. Per istruzioni, vedere [Configurare la persistenza AOF](#configure-aof-persistence).

### <a name="what-is-a-rewrite-and-how-does-it-affect-my-cache"></a>Che cos'è un'operazione di riscrittura e in che modo influisce sulla cache?

Quando il file AOF hello diventa sufficientemente grande, una riscrittura viene accodata automaticamente nella cache di hello. Hello riscrittura Ridimensiona file AOF hello con numero minimo di operazioni hello necessari toocreate hello set di dati corrente. Durante la riscrittura, prevede limiti sulle prestazioni tooreach prima soprattutto quando si utilizzano grandi set di dati. Riscrivere più volte si verificano meno spesso come file AOF hello diventa più grande, ma sarà necessaria una quantità significativa di tempo quando si verifica.

### <a name="what-should-i-expect-when-scaling-a-cache-with-aof-enabled"></a>Quali potrebbero essere gli effetti del ridimensionamento di una cache con la persistenza AOF abilitata?

Se il file AOF hello in fase di hello di scalabilità è molto grande, quindi prevedere hello tootake operazione di scala più tempo del previsto dal momento che verrà ricaricamento file hello termine scalabilità.

Per ulteriori informazioni sulla scalabilità, vedere [cosa accade se è stato ridimensionato tooa diverse dimensioni e viene ripristinato un backup effettuato prima che l'operazione di ridimensionamento hello?](#what-happens-if-i-have-scaled-to-a-different-size-and-a-backup-is-restored-that-was-made-before-the-scaling-operation)

### <a name="how-is-my-aof-data-organized-in-storage"></a>Come vengono organizzati i dati AOF nello spazio di archiviazione?

Dati archiviati nei file AOF sono suddivisa in più BLOB di pagine per le prestazioni di salvataggio hello dati toostorage tooincrease del nodo. Hello nella tabella seguente viene visualizzato il numero di BLOB di pagine vengono utilizzati per ogni livello di prezzo:

| Livello Premium | Blobs |
|--------------|-------|
| P1           | 4 per partizione    |
| P2           | 8 per partizione    |
| P3           | 16 per partizione   |
| P4           | 20 per partizione   |

Quando il servizio cluster è abilitato, ogni partizione nella cache di hello ha un proprio set di BLOB di pagine, come indicato nella tabella precedente hello. Una cache P2 con tre partizioni, ad esempio, distribuisce il proprio file AOF su 24 BLOB di pagine (8 BLOB per partizione, con 3 partizioni).

Dopo una riscrittura, nello spazio di archiviazione sono presenti due set di file AOF. Riscrive vengono eseguite in background hello e aggiungere toohello primo set di file, mentre le operazioni di impostazione che vengono inviate toohello cache durante la riscrittura hello aggiungere toohello secondo set. Una copia di backup viene archiviata temporaneamente durante la riscrittura in caso di errore, ma viene eliminata immediatamente dopo il completamento della riscrittura.


## <a name="next-steps"></a>Passaggi successivi
Informazioni su come toouse premium più memorizzano nella cache le funzionalità.

* [Livello di introduzione toohello Premium di Cache Redis di Azure](cache-premium-tier-intro.md)

<!-- IMAGES -->

[redis-cache-premium-pricing-tier]: ./media/cache-how-to-premium-persistence/redis-cache-premium-pricing-tier.png

[redis-cache-persistence]: ./media/cache-how-to-premium-persistence/redis-cache-persistence.png

[redis-cache-rdb-persistence]: ./media/cache-how-to-premium-persistence/redis-cache-rdb-persistence.png

[redis-cache-aof-persistence]: ./media/cache-how-to-premium-persistence/redis-cache-aof-persistence.png

[redis-cache-settings]: ./media/cache-how-to-premium-persistence/redis-cache-settings.png
