---
title: aaaActors diagnostica e monitoraggio | Documenti Microsoft
description: "Questo articolo descrive diagnostica hello e funzionalità nel runtime di Service Fabric Reliable Actors hello, inclusi gli eventi di hello e i contatori delle prestazioni generati dal componente di monitoraggio delle prestazioni."
services: service-fabric
documentationcenter: .net
author: abhishekram
manager: timlt
editor: vturecek
ms.assetid: 1c229923-670a-4634-ad59-468ff781ad18
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: abhisram
ms.openlocfilehash: 5b266d67875722feef5c5be8861bda6d8132a7d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-and-performance-monitoring-for-reliable-actors"></a>Diagnostica e monitoraggio delle prestazioni per Reliable Actors
Hello Reliable Actors runtime genera [EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) gli eventi e [i contatori delle prestazioni](https://msdn.microsoft.com/library/system.diagnostics.performancecounter.aspx). Questi forniscono informazioni dettagliate sui funzionamento runtime hello e agevolare la risoluzione dei problemi e il monitoraggio delle prestazioni.

## <a name="eventsource-events"></a>Eventi EventSource
nome del provider Hello EventSource per hello Reliable Actors runtime è "Microsoft-ServiceFabric-attori". Gli eventi dall'origine di eventi vengono visualizzati in hello [gli eventi di diagnostica](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md#view-service-fabric-system-events-in-visual-studio) finestra quando è in corso un'applicazione hello attore [il debug in Visual Studio](service-fabric-debugging-your-application.md).

Sono esempi di strumenti e tecnologie che consentono di raccogliere e/o la visualizzazione di eventi EventSource [PerfView](http://www.microsoft.com/download/details.aspx?id=28567), [diagnostica Azure](../cloud-services/cloud-services-dotnet-diagnostics.md), [registrazione semantica](https://msdn.microsoft.com/library/dn774980.aspx)e hello [ Oggetto TraceEvent libreria](http://www.nuget.org/packages/Microsoft.Diagnostics.Tracing.TraceEvent).

### <a name="keywords"></a>Parole chiave
Tutti gli eventi che appartengono toohello affidabile EventSource attori sono associati uno o più parole chiave. Questo consente di filtrare gli eventi che vengono raccolti. viene definito Hello seguente bits (parola chiave).

| Bit | Descrizione |
| --- | --- |
| 0x1 |Set di eventi importanti che riepilogano operazione hello di hello attori dell'infrastruttura runtime. |
| 0x2 |Set di eventi che descrivono le chiamate ai metodi degli attori. Per ulteriori informazioni, vedere hello [argomento introduttivo su attori](service-fabric-reliable-actors-introduction.md). |
| 0x4 |Set di eventi correlati tooactor stato. Per ulteriori informazioni, vedere l'argomento hello in [gestione dello stato actor](service-fabric-reliable-actors-state-management.md). |
| 0x8 |Set di eventi correlati tooturn concorrenza basata su attore hello. Per ulteriori informazioni, vedere l'argomento hello in [concorrenza](service-fabric-reliable-actors-introduction.md#concurrency). |

## <a name="performance-counters"></a>Contatori delle prestazioni
Hello Reliable Actors runtime definisce hello seguenti categorie di contatori delle prestazioni.

| Categoria | Descrizione |
| --- | --- |
| Service Fabric Actor |I contatori di attori di Service Fabric tooAzure specifico, ad esempio durata dello stato actor toosave |
| Service Fabric Actor Method |Contatori specifici toomethods implementata da attori di Service Fabric, ad esempio la frequenza con cui viene richiamato un metodo di attore |

Ciascuna hello sopra le categorie dispone di uno o più contatori.

Hello [Windows Performance Monitor](https://technet.microsoft.com/library/cc749249.aspx) applicazione disponibile per impostazione predefinita nel sistema operativo di Windows hello può essere utilizzato toocollect e visualizzazione dati contatore delle prestazioni. [Diagnostica di Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) è un'altra opzione per raccogliere i dati dei contatori delle prestazioni e caricarli tooAzure tabelle.

### <a name="performance-counter-instance-names"></a>Nomi delle istanze dei contatori delle prestazioni
Un cluster con un numero elevato di servizi attore o di partizioni di servizi attore disporrà di un numero considerevole di istanze di contatori delle prestazioni degli attori. Hello i nomi delle istanze di contatore di prestazioni consente di identificare specifici hello [partizione](service-fabric-reliable-actors-platform.md#service-fabric-partition-concepts-for-actors) e metodo actor (se applicabile) a cui è associata a tale istanza del contatore delle prestazioni hello.

#### <a name="service-fabric-actor-category"></a>Categoria Service Fabric Actor
Per categoria hello `Service Fabric Actor`, sono i nomi delle istanze di contatore hello in hello seguente formato:

`ServiceFabricPartitionID_ActorsRuntimeInternalID`

*ServiceFabricPartitionID* è la rappresentazione di stringa hello di hello Service Fabric ID di partizione che hello istanza del contatore delle prestazioni è associato. ID di partizione Hello è un GUID e rappresentazione di stringa viene generato tramite hello [ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx) metodo con l'identificatore di formato "D".

*ActorRuntimeInternalID* è la rappresentazione di stringa hello di un intero a 64 bit che viene generato dal runtime di hello attori dell'infrastruttura per l'uso interno. Questo è incluso nell'istanza del contatore delle prestazioni hello Nome tooensure l'unicità ed evitare conflitti con gli altri nomi di istanza del contatore delle prestazioni. Gli utenti non devono tentare toointerpret questa parte del nome dell'istanza del contatore delle prestazioni hello.

Hello seguito è riportato un esempio di un nome di istanza di contatore per un contatore che appartiene toohello `Service Fabric Actor` categoria:

`2740af29-78aa-44bc-a20b-7e60fb783264_635650083799324046`

Nell'esempio hello sopra, `2740af29-78aa-44bc-a20b-7e60fb783264` è la rappresentazione di stringa hello dell'ID di partizione di Service Fabric hello, e `635650083799324046` utilizzare hello 64-bit ID generato per hello runtime interno.

#### <a name="service-fabric-actor-method-category"></a>Categoria Service Fabric Actor Method
Per categoria hello `Service Fabric Actor Method`, sono i nomi delle istanze di contatore hello in hello seguente formato:

`MethodName_ActorsRuntimeMethodId_ServiceFabricPartitionID_ActorsRuntimeInternalID`

*NomeMetodo* è associato alcun nome di hello del metodo attore hello hello istanza del contatore delle prestazioni. formato di Hello del nome di metodo hello è determinato in base a una logica di runtime dell'infrastruttura attori hello tale da bilanciare la leggibilità hello del nome hello con vincoli sulla lunghezza massima di hello di nomi di istanza del contatore delle prestazioni hello in Windows.

*ActorsRuntimeMethodId* è la rappresentazione di stringa hello di intero a 32 bit che viene generato dal runtime di hello attori dell'infrastruttura per l'uso interno. Questo è incluso nell'istanza del contatore delle prestazioni hello Nome tooensure l'unicità ed evitare conflitti con gli altri nomi di istanza del contatore delle prestazioni. Gli utenti non devono tentare toointerpret questa parte del nome dell'istanza del contatore delle prestazioni hello.

*ServiceFabricPartitionID* è la rappresentazione di stringa hello di hello Service Fabric ID di partizione che hello istanza del contatore delle prestazioni è associato. ID di partizione Hello è un GUID e rappresentazione di stringa viene generato tramite hello [ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx) metodo con l'identificatore di formato "D".

*ActorRuntimeInternalID* è la rappresentazione di stringa hello di un intero a 64 bit che viene generato dal runtime di hello attori dell'infrastruttura per l'uso interno. Questo è incluso nell'istanza del contatore delle prestazioni hello Nome tooensure l'unicità ed evitare conflitti con gli altri nomi di istanza del contatore delle prestazioni. Gli utenti non devono tentare toointerpret questa parte del nome dell'istanza del contatore delle prestazioni hello.

Hello seguito è riportato un esempio di un nome di istanza di contatore per un contatore che appartiene toohello `Service Fabric Actor Method` categoria:

`ivoicemailboxactor.leavemessageasync_2_89383d32-e57e-4a9b-a6ad-57c6792aa521_635650083804480486`

Nell'esempio hello sopra, `ivoicemailboxactor.leavemessageasync` è il nome di metodo hello, `2` è hello utilizzare 32 bit ID generato per interno del runtime di hello, `89383d32-e57e-4a9b-a6ad-57c6792aa521` è la rappresentazione di stringa hello dell'ID di partizione di Service Fabric hello, e `635650083804480486` hello 64-bit ID generato per uso interno del runtime di hello.

## <a name="list-of-events-and-performance-counters"></a>Elenco degli eventi e dei contatori delle prestazioni
### <a name="actor-method-events-and-performance-counters"></a>Eventi dei metodi degli attori e relativi contatori delle prestazioni
Hello Reliable Actors dall'esecuzione hello dopo gli eventi correlati troppo[metodi attore](service-fabric-reliable-actors-introduction.md).

| Nome evento | ID evento | Level | Parole chiave | Descrizione |
| --- | --- | --- | --- | --- |
| ActorMethodStart |7 |Dettagliato |0x2 |Runtime di attori riguarda tooinvoke un metodo attore. |
| ActorMethodStop |8 |Dettagliato |0x2 |È terminata l'esecuzione di un metodo di un attore, Vale a dire, restituzione del metodo del runtime hello chiamata asincrona toohello attore e completamento dell'attività hello restituito dal metodo attore hello. |
| ActorMethodThrewException |9 |Avviso |0x3 |È stata generata un'eccezione durante l'esecuzione di hello di un metodo attore, durante il metodo actor toohello chiamata asincrona di hello del runtime o durante l'esecuzione di hello dell'attività hello restituito dal metodo actor di hello. Questo evento indica un tipo di errore nel codice attore hello analisi necessaria. |

runtime Reliable Actors Hello pubblica hello dopo l'esecuzione di toohello correlati i contatori delle prestazioni dei metodi attore.

| Nome categoria | Nome contatore | Descrizione |
| --- | --- | --- |
| Service Fabric Actor Method |Invocations/Sec |Numero di volte in cui viene chiamato metodo del servizio actor hello al secondo |
| Service Fabric Actor Method |Average milliseconds per invocation |Tempo impiegato tooexecute hello metodo del servizio actor in millisecondi |
| Service Fabric Actor Method |Exceptions thrown/Sec |Numero di volte in cui hello metodo del servizio actor ha generato un'eccezione al secondo |

### <a name="concurrency-events-and-performance-counters"></a>Eventi di concorrenza e relativi contatori delle prestazioni
Hello Reliable Actors dall'esecuzione hello dopo gli eventi correlati troppo[concorrenza](service-fabric-reliable-actors-introduction.md#concurrency).

| Nome evento | ID evento | Level | Parole chiave | Descrizione |
| --- | --- | --- | --- | --- |
| ActorMethodCallsWaitingForLock |12 |Dettagliato |0x8 |Questo evento viene scritto all'inizio di hello di ogni nuovo turno un attore. Contiene il numero di hello di chiamate actor in attesa di blocco actor di hello tooacquire che applica la concorrenza basato su in sospeso. |

runtime Reliable Actors Hello pubblica hello seguente tooconcurrency correlati di contatori delle prestazioni.

| Nome categoria | Nome contatore | Descrizione |
| --- | --- | --- |
| Service Fabric Actor |# of actor calls waiting for actor lock |Numero di chiamate actor in attesa di blocco actor di hello tooacquire che applica la concorrenza basato su in sospeso |
| Service Fabric Actor |Average milliseconds per lock wait |Tempo di blocco di hello tooacquire eseguito (in millisecondi) per ogni attore applica concorrenza basato su |
| Service Fabric Actor |Average milliseconds actor lock held |Tempo (in millisecondi) per cui hello actor blocco |

### <a name="actor-state-management-events-and-performance-counters"></a>Eventi di gestione dello stato degli attori e relativi contatori delle prestazioni
Hello Reliable Actors dall'esecuzione hello dopo gli eventi correlati troppo[gestione dello stato actor](service-fabric-reliable-actors-state-management.md).

| Nome evento | ID evento | Level | Parole chiave | Descrizione |
| --- | --- | --- | --- | --- |
| ActorSaveStateStart |10 |Dettagliato |0x4 |Runtime di attori è sullo stato di toosave hello attore. |
| ActorSaveStateStop |11 |Dettagliato |0x4 |Runtime di attori ha terminato il salvataggio dello stato actor hello. |

runtime Reliable Actors Hello pubblica hello seguendo la gestione dello stato di tooactor correlati i contatori delle prestazioni.

| Nome categoria | Nome contatore | Descrizione |
| --- | --- | --- |
| Service Fabric Actor |Average milliseconds per save state operation |Tempo impiegato toosave dello stato di actor in millisecondi |
| Service Fabric Actor |Average milliseconds per load state operation |Tempo impiegato dello stato di tooload actor in millisecondi |

### <a name="events-related-tooactor-replicas"></a>Gli eventi correlati tooactor repliche
Hello Reliable Actors dall'esecuzione hello dopo gli eventi correlati troppo[repliche attore](service-fabric-reliable-actors-platform.md#service-fabric-partition-concepts-for-actors).

| Nome evento | ID evento | Level | Parole chiave | Descrizione |
| --- | --- | --- | --- | --- |
| ReplicaChangeRoleToPrimary |1 |Informazioni |0x1 |Replica attore modificato tooPrimary ruolo. Ciò implica che gli attori hello per la partizione verranno creati all'interno di questa replica. |
| ReplicaChangeRoleFromPrimary |2 |Informazioni |0x1 |Replica attore modificato toonon ruolo primario. Ciò implica che non è più attori hello per la partizione verranno creati all'interno di questa replica. Nessuna nuova richiesta verrà recapitata tooactors già creati all'interno di questa replica. gli attori Hello verranno eliminati dopo il completamento di tutte le richieste in corso. |

### <a name="actor-activation-and-deactivation-events-and-performance-counters"></a>Eventi di attivazione e disattivazione degli attori e contatori delle prestazioni
Hello Reliable Actors dall'esecuzione hello dopo gli eventi correlati troppo[attore attivazione e disattivazione](service-fabric-reliable-actors-lifecycle.md).

| Nome evento | ID evento | Level | Parole chiave | Descrizione |
| --- | --- | --- | --- | --- |
| ActorActivated |5 |Informazioni |0x1 |Un attore è stato attivato. |
| ActorDeactivated |6 |Informazioni |0x1 |Un attore è stato disattivato. |

runtime Reliable Actors Hello pubblica hello seguenti contatori delle prestazioni correlati tooactor attivazione e disattivazione.

| Nome categoria | Nome contatore | Descrizione |
| --- | --- | --- |
| Service Fabric Actor |Average OnActivateAsync milliseconds |Tempo tooexecute del metodo OnActivateAsync in millisecondi |

### <a name="actor-request-processing-performance-counters"></a>Contatori delle prestazioni di elaborazione delle richieste degli attori
Quando un client richiama un metodo tramite un oggetto proxy attore, comporta un messaggio di richiesta inviato servizio actor toohello di rete hello. servizio di Hello elabora il messaggio di richiesta di hello e invia un client toohello indietro di risposta. runtime Reliable Actors Hello pubblica hello dopo l'elaborazione della richiesta tooactor correlati i contatori delle prestazioni.

| Nome categoria | Nome contatore | Descrizione |
| --- | --- | --- |
| Service Fabric Actor |# of outstanding requests |Numero di richieste elaborate nel servizio hello |
| Service Fabric Actor |Average milliseconds per request |Tempo impiegato (in millisecondi) dal hello servizio tooprocess una richiesta |
| Service Fabric Actor |Average milliseconds for request deserialization |Ora ottenuta (in millisecondi) toodeserialize attore messaggio di richiesta quando viene ricevuto nel servizio hello |
| Service Fabric Actor |Average milliseconds for response serialization |Tempo tooserialize eseguito (in millisecondi) hello attore messaggio di risposta al servizio hello prima dell'invio risposta hello client toohello |

## <a name="next-steps"></a>Passaggi successivi
* [Utilizzo di piattaforma Service Fabric hello Reliable Actors](service-fabric-reliable-actors-platform.md)
* [Documentazione di riferimento delle API di Actors](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [Codice di esempio](https://github.com/Azure/servicefabric-samples)
* [Provider di EventSource in PerfView](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/)
