---
title: domande frequenti sull'hub di eventi aaaAzure | Documenti Microsoft
description: Domande frequenti sugli Hub eventi di Azure (FAQ)
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: bfa10984-eb22-4671-861a-f377a90d9372
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm;shvija
ms.openlocfilehash: cc0844edcc38ad167cde9497d58d44155fc90b7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-frequently-asked-questions"></a>Domande frequenti sugli Hub eventi di Azure

## <a name="general"></a>Generale

### <a name="what-is-hello-difference-between-event-hubs-basic-and-standard-tiers"></a>Qual è la differenza hello tra livelli evento hub Basic e Standard?

Hello livello Standard di hub di eventi di Azure offre funzionalità oltre a quelli disponibili nel livello Basic hello. Hello seguenti caratteristiche è incluso in Standard:
* Periodo di conservazione degli eventi più lungo
* Connessioni negoziate aggiuntive, con un costo eccedenza per più di numero hello incluso
* Più di un singolo gruppo di consumer
* [Acquisire](https://docs.microsoft.com/azure/event-hubs/event-hubs-capture-overview)

Per ulteriori informazioni sui prezzi dei livelli, tra cui dedicato hub di eventi, vedere hello [dettagli prezzi degli hub di eventi](https://azure.microsoft.com/pricing/details/event-hubs/).

### <a name="what-are-event-hubs-throughput-units"></a>Cosa sono le unità elaborate in Hub eventi?

Selezionare in modo esplicito l'unità di velocità effettiva degli hub di eventi, tramite il portale di Azure hello o modelli di gestione di risorse hub eventi. Unità di velocità effettiva applicano tooall hub di eventi in uno spazio dei nomi dell'hub eventi, e ogni unità di velocità effettiva dà hello toohello di spazio dei nomi seguenti funzionalità:

* Backup too1 MB al secondo di eventi in ingresso (inviati a un hub di eventi), ma non più di 1000 eventi in ingresso, operazioni di gestione o controllo chiamate API al secondo.
* Backup too2 MB al secondo di eventi in uscita (utilizzati da un hub di eventi).
* Too84 GB di spazio di archiviazione di eventi (sufficiente per il periodo di memorizzazione di 24 ore di hello predefinito).

Unità di velocità effettiva degli hub di eventi vengono fatturate con tariffe orarie, in base al numero massimo di hello di unità selezionate in hello data ora.

### <a name="how-are-event-hubs-throughput-unit-limits-enforced"></a>Come vengono applicati i limiti di unità elaborate in Hub eventi
Se la velocità effettiva totale in ingresso hello o hello frequenza degli eventi totali in ingresso fra tutti gli hub di eventi in uno spazio dei nomi supera consentita delle unità di velocità effettiva aggregata di hello, i mittenti sono limitati e riceveranno errori indicanti che hello in ingresso è stato superato.

Se la velocità effettiva totale in uscita hello o velocità in uscita totale degli eventi di hello fra tutti gli hub di eventi in uno spazio dei nomi supera consentita delle unità di velocità effettiva aggregata di hello, ricevitori sono limitati e riceveranno errori indicanti che hello in uscita è stato superato. Le quote di ingresso e in uscita vengono applicate separatamente, in modo che nessun mittente possa causare evento consumo tooslow verso il basso, né è possibile un ricevitore impedisce l'invio di un hub eventi.

### <a name="is-there-a-limit-on-hello-number-of-throughput-units-that-can-be-selected"></a>È previsto un limite al numero di hello di unità di velocità effettiva che possono essere selezionati?
Esiste una quota predefinita di 20 unità elaborate per ogni spazio dei nomi. È possibile richiedere una quota maggiore di unità elaborate creando un ticket di supporto. Oltre al limite di unità di velocità effettiva 20 hello, sono disponibili 20 e 100 unità di velocità effettiva bundle. Si noti che l'utilizzo di più di 20 unità di velocità effettiva viene rimosso hello possibilità toochange hello numero di unità di velocità effettiva senza un ticket di supporto di archiviazione.

### <a name="can-i-use-a-single-amqp-connection-toosend-and-receive-from-multiple-event-hubs"></a>È possibile usare un singola toosend connessione AMQP e di ricezione dagli hub di eventi più?
Sì, purché siano tutti gli hub di eventi di hello in hello stesso spazio dei nomi.

### <a name="what-is-hello-maximum-retention-period-for-events"></a>Che cos'è il periodo di memorizzazione massimo hello per gli eventi?
Il livello Standard di Hub eventi supporta attualmente un periodo di conservazione massimo di 7 giorni. Si noti che gli hub eventi non sono intesi come archivi dati permanenti. Maggiore di 24 ore sono destinate a scenari in cui è utile tooreplay il flusso di un evento in periodi di memorizzazione hello stessi sistemi, ad esempio, tootrain o verificare un nuovo modello di machine learning sui dati esistenti. Se è necessario messaggio memorizzazione oltre 7 giorni, abilitazione [acquisire gli hub di eventi](https://docs.microsoft.com/azure/event-hubs/event-hubs-capture-overview) nel tuo evento hub vengono utilizzati i dati hello l'account di archiviazione toohello hub eventi o l'account del servizio di Azure Data Lake di propria scelta. L'abilitazione dell'acquisizione prevede un costo in base alle unità elaborate acquistate.

### <a name="where-is-azure-event-hubs-available"></a>Dove sono disponibili gli hub eventi di Azure?
Hub eventi di Azure è disponibile in tutte le aree di Azure supportate. Per un elenco, visitare hello [aree di Azure](https://azure.microsoft.com/regions/) pagina.  

## <a name="best-practices"></a>Procedure consigliate

### <a name="how-many-partitions-do-i-need"></a>Quante partizioni sono necessarie?
Tenere presente che hello conteggio delle partizioni in un hub eventi Impossibile modificare dopo l'installazione. Tenendo presente, è importante toothink sul numero di partizioni è necessario prima di iniziare. 

Hub eventi è progettato tooallow lettore una singola partizione per ogni gruppo di consumer. Nella maggior parte dei casi d'uso, è sufficiente impostazione hello di quattro partizioni. Se si vuole tooscale l'elaborazione di eventi, è consigliabile tooconsider aggiunta di altre partizioni. Non sono previsti limiti di velocità effettiva specifico in una partizione, tuttavia la velocità effettiva aggregata di hello nello spazio dei nomi è limitata dal numero di hello di unità di velocità effettiva. Quando si aumenta il numero di hello di unità di velocità effettiva nello spazio dei nomi, è opportuno partizioni aggiuntive tooallow lettori simultanei tooachieve i propri velocità effettiva massima.

Tuttavia, se si dispone di un modello in cui l'applicazione dispone di una partizione particolare tooa di affinità, aumentare il numero di hello partizioni potrebbe non essere di qualsiasi tooyou vantaggio. Per altre informazioni al riguardo, vedere l'argomento relativo a [disponibilità e coerenza](event-hubs-availability-and-consistency.md).

## <a name="pricing"></a>Prezzi

### <a name="where-can-i-find-more-pricing-information"></a>Dove sono reperibili altre informazioni sui prezzi?
Per informazioni complete sui prezzi di hub eventi, vedere hello [dettagli prezzi degli hub di eventi](https://azure.microsoft.com/pricing/details/event-hubs/).

### <a name="is-there-a-charge-for-retaining-event-hubs-events-for-more-than-24-hours"></a>È previsto un addebito per conservare gli eventi di Hub eventi per più di 24 ore?
livello Standard hub di eventi Hello consente periodi più di 24 ore, per un massimo di 7 giorni di memorizzazione dei messaggi. Se le dimensioni di hello del numero totale di hello di eventi stored superano capacità di archiviazione consentita hello per il numero di unità di velocità effettiva selezionate (84 GB per unità di velocità effettiva) hello, hello cui dimensione supera la capacità consentita hello viene addebitato ai hello pubblicati tariffa di archiviazione Blob di Azure. capacità di archiviazione consentita Hello in ogni unità di velocità effettiva copre tutti i costi di archiviazione per periodi di conservazione di 24 ore (impostazione predefinita hello), anche se viene utilizzata l'unità di velocità effettiva hello backup indennità massimo in ingresso toohello.

### <a name="how-is-hello-event-hubs-storage-size-calculated-and-charged"></a>Come viene calcolata e addebitata hello dimensioni di archiviazione degli hub di eventi?
dimensioni totali di Hello di tutti gli eventi archiviati, inclusi eventuali overhead interni per le intestazioni degli eventi o sulle strutture di archiviazione su disco in tutti gli hub di eventi, viene misurata durante tutto il giorno hello. Alla fine di hello del giorno hello, dimensione di archiviazione massima hello viene calcolata. indennità archiviazione giornaliera Hello viene calcolato in base al numero minimo di hello di unità di velocità effettiva che sono stati selezionati durante il giorno hello (ogni unità di velocità effettiva fornisce una capacità consentita di 84 GB). Se supera la dimensione totale di hello hello calcolato ogni giorno capacità di archiviazione consentita, hello in eccesso viene fatturata in base alle tariffe di archiviazione Blob di Azure con (in hello **archiviazione con ridondanza locale** frequenza).

### <a name="how-are-event-hubs-ingress-events-calculated"></a>Come vengono calcolati gli eventi in ingresso di Hub eventi?
Ogni evento inviato tooan hub di eventi conta come messaggio fatturabile. Un *evento in ingresso* è definito come un'unità di dati che sono minore o uguale too64 KB. Qualsiasi evento che è minore o uguale dimensioni too64 KB viene considerato un evento fatturabile toobe. Se l'evento hello è maggiore di 64 KB, il numero di hello degli eventi fatturabili viene calcolato in base a dimensioni evento toohello in multipli di 64 KB. Ad esempio, un evento di 8 KB inviato toohello hub di eventi viene fatturato come un evento, ma un messaggio di 96 KB inviato toohello hub di eventi viene fatturato come due eventi.

Eventi utilizzati da un hub di eventi, nonché le operazioni di gestione e controllo chiama ad esempio i checkpoint, non vengono conteggiati come eventi in ingresso fatturabili, ma comportano un aumento dei backup indennità unità di velocità effettiva toohello.

### <a name="do-brokered-connection-charges-apply-tooevent-hubs"></a>Gli addebiti di connessione negoziata si applicano tooEvent hub?
Costi di connessione si applicano solo quando viene utilizzato il protocollo AMQP hello. Non sono previsti costi di connessione per l'invio di eventi tramite HTTP, indipendentemente dal numero di hello di invio dei sistemi o dispositivi. Se si prevede di toouse AMQP (ad esempio, tooachieve più efficiente evento streaming o tooenable la comunicazione bidirezionale negli scenari di comando e controllo IoT), vedere hello [hub eventi, informazioni sui prezzi](https://azure.microsoft.com/pricing/details/event-hubs/) pagina per informazioni dettagliate su come numero di connessioni è inclusi in ogni livello di servizio.

### <a name="how-is-event-hubs-capture-billed"></a>Come viene fatturata l'acquisizione di Hub eventi?
Capture è abilitato quando un hub eventi nello spazio dei nomi hello è abilitata l'opzione di acquisizione hello. L'acquisizione di Hub eventi viene fatturata su base oraria per le unità elaborate acquistate. Come numero di unità di velocità effettiva di hello è aumentato o diminuito, fatturazione di acquisire gli hub di eventi riflette le modifiche con incrementi di ore intere. Per altre informazioni sulla fatturazione dell'acquisizione di Hub eventi, vedere [Prezzi di Hub eventi](https://azure.microsoft.com/pricing/details/event-hubs/).

### <a name="will-i-be-billed-for-hello-storage-account-i-select-for-event-hubs-capture"></a>Verrà fatturato hello account di archiviazione selezionate per acquisire gli hub di eventi?
L'acquisizione usa un account di archiviazione fornito dall'utente, quando la funzione è abilitata in un hub eventi. Poiché si tratta di account di archiviazione, le modifiche per questa configurazione vengono fatturati tooyour sottoscrizione di Azure.

## <a name="quotas"></a>Quote

### <a name="are-there-any-quotas-associated-with-event-hubs"></a>Sono previste quote associate all'hub eventi?
Per un elenco di tutte le quote dell'hub eventi, vedere [quote](event-hubs-quotas.md).

## <a name="troubleshooting"></a>Risoluzione dei problemi

### <a name="what-are-some-of-hello-exceptions-generated-by-event-hubs-and-their-suggested-actions"></a>Quali sono le eccezioni di hello generate dall'hub eventi e le relative azioni suggerite?
Per un elenco delle possibili eccezioni degli hub eventi, vedere [Eccezioni della messaggistica di Hub eventi](event-hubs-messaging-exceptions.md).

### <a name="diagnostic-logs"></a>Log di diagnostica
Gli hub di eventi supporta due tipi di [log di diagnostica](event-hubs-diagnostic-logs.md) -log degli errori di acquisizione e registri - che entrambi sono rappresentati in json e può essere attivate tramite hello portale di Azure.

### <a name="support-and-sla"></a>Contratto di servizio e supporto
Il supporto tecnico per gli hub eventi è disponibile tramite hello [forum della community](https://social.msdn.microsoft.com/forums/azure/home). Il supporto per fatturazione e gestione delle sottoscrizioni viene fornito gratuitamente.

toolearn ulteriori informazioni su questo contratto di servizio, vedere hello [i contratti di servizio](https://azure.microsoft.com/support/legal/sla/) pagina.

## <a name="next-steps"></a>Passaggi successivi
Sono disponibili ulteriori informazioni sugli hub di eventi visitando hello seguenti collegamenti:

* [Panoramica di Hub eventi](event-hubs-what-is-event-hubs.md)
* [Create an Event Hub](event-hubs-create.md) (Creare un Hub eventi)
