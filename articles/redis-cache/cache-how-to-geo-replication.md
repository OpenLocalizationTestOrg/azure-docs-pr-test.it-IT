---
title: aaaHow tooconfigure-replica geografica per Cache Redis di Azure | Documenti Microsoft
description: Informazioni su come tooreplicate istanze di Azure Redis Cache in aree geografiche diverse.
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 375643dc-dbac-4bab-8004-d9ae9570440d
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: sdanie
ms.openlocfilehash: edcd6f202b51055d1a4e47ecaf11f9977d50aa81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-geo-replication-for-azure-redis-cache"></a>Come tooconfigure replica geografica per Cache Redis di Azure

La replica geografica fornisce un meccanismo per il collegamento di due istanze di Cache Redis di Azure di livello Premium. Una cache viene definita come cache collegato primario hello e altri come cache collegato secondaria hello hello. cache collegato secondaria Hello diventa di sola lettura e cache primaria toohello scritti i dati replicati cache collegato secondaria toohello. Questa funzionalità può essere utilizzato tooreplicate una cache nelle aree di Azure. Questo articolo fornisce una Guida tooconfiguring replica geografica, per le istanze di Cache Redis di Azure di livello Premium.

## <a name="geo-replication-prerequisites"></a>Prerequisiti per la replica geografica

è necessario soddisfare tooconfigure replica geografica tra due cache, hello seguenti prerequisiti:

- Entrambe le cache devono essere cache di [livello Premium](cache-premium-tier-intro.md).
- Entrambe le cache devono essere in hello stessa sottoscrizione di Azure.
- cache collegato secondaria Hello deve essere di hello stesso prezzi livello o un piano tariffario maggiore rispetto a cache collegato primario hello.
- Se cache collegato primario hello è clustering abilitata, cache collegato secondaria hello deve disporre di clustering abilitata con hello cache collegato primario hello stesso numero di partizioni.
- Entrambe le cache devono essere create e in esecuzione.
- La persistenza non deve essere attivata in nessuna delle due cache.
- Replica geografica tra cache di hello che stessa rete virtuale è supportato. La replica geografica tra cache di diverse reti virtuali è supportata, come le reti virtuali hello due sono configurate in modo che le risorse in reti virtuali hello sono in grado di tooreach tra loro tramite connessioni TCP.

Dopo aver configurata la replica geografica, hello applicate restrizioni seguenti coppia cache collegato tooyour:

- cache collegato secondaria Hello è di sola lettura. è possibile leggere da esso, ma non è possibile scrivere tooit eventuali dati. 
- Tutti i dati presenti nella cache collegato secondaria hello prima che fosse aggiunto collegamento hello viene rimosso. Se hello-replica geografica viene successivamente rimosso, tuttavia, hello replicati dati restano nella cache collegato secondario hello.
- Non è possibile avviare un [l'operazione di ridimensionamento](cache-how-to-scale.md) nella cache o [modificare hello numero di partizioni](cache-how-to-premium-clustering.md) se cache di hello ha clustering abilitato.
- Non è possibile abilitare la persistenza in nessuna delle cache.
- È possibile utilizzare [esportare](cache-how-to-import-export-data.md#export) con una cache, ma è possibile solo [importazione](cache-how-to-import-export-data.md#import) in hello primario collegato della cache.
- È possibile eliminare la cache collegata o gruppo di risorse hello che li contiene, fino a quando non si rimuove il collegamento di replica geografica hello. Per ulteriori informazioni, vedere [perché hello operazione esito negativo quando si tenta di toodelete la cache collegata?](#why-did-the-operation-fail-when-i-tried-to-delete-my-linked-cache)
- Se due cache di hello si trovano in aree geografiche diverse, i costi di rete in uscita verranno applicate toohello dati replicati in cache collegato di aree toohello secondaria. Per ulteriori informazioni, vedere [non il costo tooreplicate dei dati nelle aree di Azure?](#how-much-does-it-cost-to-replicate-my-data-across-azure-regions)
- Non si verifica alcuna cache di failover automatico toohello secondaria collegato se scendere di cache di hello primario (e relativa replica). Nelle applicazioni client toofailover di ordine, è necessario un collegamento di replica geografica toomanually Rimuovi hello e punto hello client applicazioni toohello di memorizzare nella cache che precedentemente era cache collegato secondaria hello. Per ulteriori informazioni, vedere [come funziona l'esecuzione del failover cache collegato secondaria toohello?](#how-does-failing-over-to-the-secondary-linked-cache-work)

## <a name="add-a-geo-replication-link"></a>Aggiungere un collegamento di replica geografica

1. Fare clic su toolink premium due memorizza nella cache insieme per la replica geografica, **-replica geografica** dal menu di risorsa hello della cache di hello inteso come primario hello collegato memorizza nella cache e quindi fare clic su **Aggiungi collegamento di replica della cache**da hello **-replica geografica** blade.

    ![Aggiungi collegamento](./media/cache-how-to-geo-replication/cache-geo-location-menu.png)

2. Fare clic sul nome della cache secondaria di hello desiderato da hello hello **cache compatibile** elenco. Se la cache desiderata non viene visualizzata nell'elenco di hello, verificare che hello [prerequisiti di replica geografica](#geo-replication-prerequisites) per hello desiderato cache secondaria vengono soddisfatti. cache di hello toofilter per regione, fare clic su area geografica desiderata hello in hello mappa toodisplay solo quelli memorizza nella cache di hello **cache compatibile** elenco.

    ![Cache compatibili con la replica geografica](./media/cache-how-to-geo-replication/cache-geo-location-select-link.png)
    
    È inoltre possibile avviare il collegamento di processo o visualizzare i dettagli sulla cache di hello secondario tramite il menu di scelta rapida hello hello.

    ![Menu di scelta rapida della replica geografica](./media/cache-how-to-geo-replication/cache-geo-location-select-link-context-menu.png)

3. Fare clic su **collegamento** toolink hello due cache insieme e iniziare il processo di replica hello.

    ![Collega cache](./media/cache-how-to-geo-replication/cache-geo-location-confirm-link.png)

4. È possibile visualizzare lo stato di avanzamento hello del processo di replica hello in hello **-replica geografica** blade.

    ![Stato del collegamento](./media/cache-how-to-geo-replication/cache-geo-location-linking.png)

    È inoltre possibile visualizzare il collegamento stato hello hello **Panoramica** pannello per entrambe le cache di hello primario e secondario.

    ![Stato della cache](./media/cache-how-to-geo-replication/cache-geo-location-link-status.png)

    Una volta completato il processo di replica hello, hello **collegamento stato** cambia troppo**Succeeded**.

    ![Stato della cache](./media/cache-how-to-geo-replication/cache-geo-location-link-successful.png)

    Durante il processo di collegamento di hello, cache collegato primario hello rimane disponibile per l'utilizzo ma cache collegato secondaria hello non è disponibile fino al completamento di hello processo di collegamento.

## <a name="remove-a-geo-replication-link"></a>Rimuovere un collegamento di replica geografica

1. collegamento hello tooremove tra due cache e arrestare la replica geografica, fare clic su **scollegare cache** da hello **-replica geografica** blade.
    
    ![Scollega cache](./media/cache-how-to-geo-replication/cache-geo-location-unlink.png)

    Al termine del processo di scollegamento di hello, cache secondaria hello disponibile per entrambe le operazioni di lettura e scrittura.

>[!NOTE]
>Quando viene rimosso il collegamento di replica geografica hello, hello dati replicati hello primario cache collegato rimane nella cache di hello secondario.
>
>

## <a name="geo-replication-faq"></a>Domande frequenti sulla replica geografica

- [È possibile usare la replica geografica con una cache di livello Standard o Basic?](#can-i-use-geo-replication-with-a-standard-or-basic-tier-cache)
- [La cache può essere utilizzato durante il collegamento hello o un processo di scollegamento?](#is-my-cache-available-for-use-during-the-linking-or-unlinking-process)
- [È possibile collegare più di due cache?](#can-i-link-more-than-two-caches-together)
- [È possibile collegare due cache da diverse sottoscrizioni di Azure?](#can-i-link-two-caches-from-different-azure-subscriptions)
- [È possibile collegare due cache con dimensioni diverse?](#can-i-link-two-caches-with-different-sizes)
- [È possibile usare la replica geografica con il clustering abilitato?](#can-i-use-geo-replication-with-clustering-enabled)
- [È possibile usare la replica geografica con le cache in una rete virtuale?](#can-i-use-geo-replication-with-my-caches-in-a-vnet)
- [È possibile utilizzare PowerShell o Azure CLI toomanage replica geografica?](#can-i-use-powershell-or-azure-cli-to-manage-geo-replication)
- [Quanto costa tooreplicate dei dati nelle aree di Azure?](#how-much-does-it-cost-to-replicate-my-data-across-azure-regions)
- [Motivo per cui operazione hello non quando si tenta di toodelete la cache collegata?](#why-did-the-operation-fail-when-i-tried-to-delete-my-linked-cache)
- [Quale area si deve usare per la cache collegata secondaria?](#what-region-should-i-use-for-my-secondary-linked-cache)
- [Come funziona l'esecuzione del failover cache collegato secondaria toohello?](#how-does-failing-over-to-the-secondary-linked-cache-work)

### <a name="can-i-use-geo-replication-with-a-standard-or-basic-tier-cache"></a>È possibile usare la replica geografica con una cache di livello Standard o Basic?

No, la replica geografica è disponibile solo per le cache del livello Premium.

### <a name="is-my-cache-available-for-use-during-hello-linking-or-unlinking-process"></a>La cache può essere utilizzato durante il collegamento hello o un processo di scollegamento?

- Quando si collega due cache per la replica geografica, cache collegato primario hello rimane disponibile per l'utilizzo ma cache collegato secondaria hello non è disponibile fino al completamento di hello processo di collegamento.
- Quando si rimuove il collegamento di replica geografica hello tra due cache, entrambe le cache rimangono disponibili per l'utilizzo.

### <a name="can-i-link-more-than-two-caches-together"></a>È possibile collegare più di due cache?

No, quando si usa la replica geografica è possibile collegare solo due cache.

### <a name="can-i-link-two-caches-from-different-azure-subscriptions"></a>È possibile collegare due cache da diverse sottoscrizioni di Azure?

No, entrambe le cache devono essere in hello stessa sottoscrizione di Azure.

### <a name="can-i-link-two-caches-with-different-sizes"></a>È possibile collegare due cache di dimensioni diverse?

Sì, purché sia maggiore di cache collegato primario hello cache collegato secondaria hello.

### <a name="can-i-use-geo-replication-with-clustering-enabled"></a>È possibile usare la replica geografica con il clustering abilitato?

Sì, purché entrambe sono hello stesso numero di partizioni.

### <a name="can-i-use-geo-replication-with-my-caches-in-a-vnet"></a>È possibile usare la replica geografica con le cache in una rete virtuale?

Sì, la replica geografica di cache nelle reti virtuali è supportata. 

- Replica geografica tra cache di hello che stessa rete virtuale è supportato.
- La replica geografica tra cache di diverse reti virtuali è supportata, come le reti virtuali hello due sono configurate in modo che le risorse in reti virtuali hello sono in grado di tooreach tra loro tramite connessioni TCP.

### <a name="can-i-use-powershell-or-azure-cli-toomanage-geo-replication"></a>È possibile utilizzare PowerShell o Azure CLI toomanage replica geografica?

In questo momento è possibile gestire solo utilizzando la replica geografica hello portale di Azure.

### <a name="how-much-does-it-cost-tooreplicate-my-data-across-azure-regions"></a>Quanto costa tooreplicate dei dati nelle aree di Azure?

Quando si utilizza la replica geografica, i dati dalla cache collegato primario hello sono cache replicata toohello secondari collegato. Se collegato hello due cache presenti hello stessa regione di Azure, non è previsto alcun addebito per il trasferimento di dati hello. Se hello due collegate cache si trovano in diverse aree di Azure, costi di trasferimento dati-replica geografica hello sono il costo della larghezza di banda hello di replica che toohello dati di altre aree di Azure. Per altre informazioni, vedere [Dettagli sui prezzi per la larghezza di banda](https://azure.microsoft.com/pricing/details/bandwidth/).

### <a name="why-did-hello-operation-fail-when-i-tried-toodelete-my-linked-cache"></a>Motivo per cui operazione hello non quando si tenta di toodelete la cache collegata?

Quando due cache sono collegate tra loro, è possibile eliminare una cache o hello gruppo di risorse che li contiene fino a quando non si rimuove il collegamento di replica geografica hello. Se si tenta toodelete hello risorsa che contiene uno o entrambi hello collegato memorizza nella cache, hello altre risorse nel gruppo di risorse hello vengono eliminati, ma il gruppo di risorse hello rimane in hello `deleting` lo stato e qualsiasi collegato cache nel gruppo di risorse hello rimangono nella hello `running` stato. l'eliminazione di hello toocomplete del gruppo di risorse hello e hello collegato memorizza nella cache all'interno di esso, il collegamento di replica geografica hello interruzione come descritto in [rimuovere un collegamento di replica geografica](#remove-a-geo-replication-link).

### <a name="what-region-should-i-use-for-my-secondary-linked-cache"></a>Quale area si deve usare per la cache collegata secondaria?

In generale, è consigliabile per tooexist la cache di hello stessa regione di Azure come un'applicazione hello che vi accede. Se l'applicazione dispone di un'area primaria e di fallback, le cache primaria e secondaria devono essere presenti in quelle stesse aree. Per altre informazioni sulle aree abbinate, vedere [Continuità aziendale e ripristino di emergenza nelle aree geografiche abbinate di Azure](../best-practices-availability-paired-regions.md).

### <a name="how-does-failing-over-toohello-secondary-linked-cache-work"></a>Come funziona l'esecuzione del failover cache collegato secondaria toohello?

Nella versione iniziale di hello di replica geografica, Cache Redis di Azure non supporta il failover automatico nelle aree di Azure. La replica geografica è usata principalmente in uno scenario di ripristino di emergenza. In uno scenario di ripristino distater i clienti devono portare fino allo stack di tutta l'applicazione hello in un'area di backup in modo coordinato anziché di utilizzare singoli componenti delle applicazioni di decidere quando tooswitch tootheir backup in modo autonomo. Questo è particolarmente rilevante tooRedis. Uno dei principali vantaggi di hello di Redis è un archivio di bassa latenza. Se Redis utilizzato da un'applicazione viene eseguito il failover tooa altra area di Azure ma non il livello di calcolo di hello, hello aggiunto round trip ora avrebbe un impatto notevole sulle prestazioni. Per questo motivo, desideriamo tooavoid Redis errori su automaticamente a causa di problemi di disponibilità tootransient.

Attualmente, tooinitiate hello failover, è necessario tooremove hello replica geografica collegamento nel portale di Azure hello e quindi modificare l'endpoint di connessione hello client Redis hello dal database secondario hello cache collegato primaria toohello (collegato in precedenza) della cache. Quando vengono disassociate due cache, hello replica hello diventa una normale lettura-scrittura cache nuovamente e accetta le richieste da client di Redis.


## <a name="next-steps"></a>Passaggi successivi

Altre informazioni su hello [piano Premium di Cache Redis di Azure](cache-premium-tier-intro.md).

