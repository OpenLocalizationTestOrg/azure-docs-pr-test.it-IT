---
title: aaaAzure ServiceFabric diagnostica e monitoraggio | Documenti Microsoft
description: "In questo articolo vengono descritte funzionalità di monitoraggio delle prestazioni hello in hello ServiceRemoting affidabile di servizio dell'infrastruttura runtime, ad esempio i contatori delle prestazioni generato da essa."
services: service-fabric
documentationcenter: .net
author: suchiagicha
manager: timlt
editor: suchiagicha
ms.assetid: 1c229923-670a-4634-ad59-468ff781ad18
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: suchiagicha
ms.openlocfilehash: 64db9a890bd59a1326e587d14b89c007b71a9059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-and-performance-monitoring-for-reliable-service-remoting"></a>Diagnostica e monitoraggio delle prestazioni per Reliable Service Remoting
dall'esecuzione affidabile ServiceRemoting Hello [i contatori delle prestazioni](https://msdn.microsoft.com/library/system.diagnostics.performancecounter.aspx). Questi forniscono informazioni dettagliate sui funzionamento hello ServiceRemoting e agevolare la risoluzione dei problemi e il monitoraggio delle prestazioni.


## <a name="performance-counters"></a>Contatori delle prestazioni
Hello ServiceRemoting affidabile runtime definisce hello seguenti categorie di contatori delle prestazioni:

| Categoria | Descrizione |
| --- | --- |
| Servizio Service Fabric |Contatori specifici tooAzure comunicazione remota del servizio Service Fabric, ad esempio, tooprocess tempo medio richiesta |
| Metodo del servizio Service Fabric |Toomethods specifici contatori implementato dal servizio di gestione remota di Service Fabric, ad esempio, la frequenza con cui viene richiamato un metodo di servizio |

Ciascuna hello precedente categorie dispone di uno o più contatori.

Hello [Windows Performance Monitor](https://technet.microsoft.com/library/cc749249.aspx) applicazione disponibile per impostazione predefinita nel sistema operativo di Windows hello può essere utilizzato toocollect e visualizzazione dati contatore delle prestazioni. [Diagnostica di Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) è un'altra opzione per raccogliere i dati dei contatori delle prestazioni e caricarli tooAzure tabelle.

### <a name="performance-counter-instance-names"></a>Nomi delle istanze dei contatori delle prestazioni
Un cluster con un numero elevato di servizi o partizioni di ServiceRemoting disporrà di un numero considerevole di istanze di contatori delle prestazioni. istanza del contatore delle prestazioni Hello nomi consentono di identificare la partizione specifica hello e metodo di servizio (se applicabile) a cui è associato tale istanza del contatore delle prestazioni hello.

#### <a name="service-fabric-service-category"></a>Categoria del servizio Service Fabric
Per categoria hello `Service Fabric Service`, sono i nomi delle istanze di contatore hello in hello seguente formato:

`ServiceFabricPartitionID_ServiceReplicaOrInstanceId_ServiceRuntimeInternalID`

*ServiceFabricPartitionID* è la rappresentazione di stringa hello di hello Service Fabric ID di partizione che hello istanza del contatore delle prestazioni è associato. ID di partizione Hello è un GUID e rappresentazione di stringa viene generato tramite hello [ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx) metodo con l'identificatore di formato "D".

*ServiceReplicaOrInstanceId* è la rappresentazione di stringa hello di hello è associato l'ID Replica/istanza dell'infrastruttura del servizio che hello istanza del contatore delle prestazioni.

*ServiceRuntimeInternalID* è la rappresentazione di stringa hello di un intero a 64 bit generati dal runtime del servizio di infrastruttura hello per l'uso interno. Questo è incluso nell'istanza del contatore delle prestazioni hello Nome tooensure l'unicità ed evitare conflitti con gli altri nomi di istanza del contatore delle prestazioni. Gli utenti non devono tentare toointerpret questa parte del nome dell'istanza del contatore delle prestazioni hello.

Hello seguito è riportato un esempio di un nome di istanza di contatore per un contatore che appartiene toohello `Service Fabric Service` categoria:

`2740af29-78aa-44bc-a20b-7e60fb783264_635650083799324046_5008379932`

Nell'esempio sopra riportato, hello `2740af29-78aa-44bc-a20b-7e60fb783264` è la rappresentazione di stringa hello dell'ID di partizione di Service Fabric hello, `635650083799324046` è la rappresentazione di stringa di Replica/InstanceId e `5008379932` hello 64-bit ID generato per interno del runtime di hello utilizzare.

#### <a name="service-fabric-service-method-category"></a>Categoria del metodo del servizio Service Fabric
Per categoria hello `Service Fabric Service Method`, sono i nomi delle istanze di contatore hello in hello seguente formato:

`MethodName_ServiceRuntimeMethodId_ServiceFabricPartitionID_ServiceReplicaOrInstanceId_ServiceRuntimeInternalID`

*NomeMetodo* è associato alcun nome hello del metodo di servizio hello che hello istanza del contatore delle prestazioni. formato di Hello del nome di metodo hello è determinato in base a una logica nel runtime di Service Fabric hello tale da bilanciare la leggibilità hello del nome hello con vincoli sulla lunghezza massima di hello di nomi di istanza del contatore delle prestazioni hello in Windows.

*ServiceRuntimeMethodId* è la rappresentazione di stringa hello di intero a 32 bit che viene generato dal runtime di Service Fabric hello per l'uso interno. Questo è incluso nell'istanza del contatore delle prestazioni hello Nome tooensure l'unicità ed evitare conflitti con gli altri nomi di istanza del contatore delle prestazioni. Gli utenti non devono tentare toointerpret questa parte del nome dell'istanza del contatore delle prestazioni hello.

*ServiceFabricPartitionID* è la rappresentazione di stringa hello di hello Service Fabric ID di partizione che hello istanza del contatore delle prestazioni è associato. ID di partizione Hello è un GUID e rappresentazione di stringa viene generato tramite hello [ `Guid.ToString` ](https://msdn.microsoft.com/library/97af8hh4.aspx) metodo con l'identificatore di formato "D".

*ServiceReplicaOrInstanceId* è la rappresentazione di stringa hello di hello è associato l'ID Replica/istanza dell'infrastruttura del servizio che hello istanza del contatore delle prestazioni.

*ServiceRuntimeInternalID* è la rappresentazione di stringa hello di un intero a 64 bit generati dal runtime del servizio di infrastruttura hello per l'uso interno. Questo è incluso nell'istanza del contatore delle prestazioni hello Nome tooensure l'unicità ed evitare conflitti con gli altri nomi di istanza del contatore delle prestazioni. Gli utenti non devono tentare toointerpret questa parte del nome dell'istanza del contatore delle prestazioni hello.

Hello seguito è riportato un esempio di un nome di istanza di contatore per un contatore che appartiene toohello `Service Fabric Service Method` categoria:

`ivoicemailboxservice.leavemessageasync_2_89383d32-e57e-4a9b-a6ad-57c6792aa521_635650083804480486_5008380`

Nell'esempio sopra riportato, hello `ivoicemailboxservice.leavemessageasync` è il nome di metodo hello, `2` è hello utilizzare 32 bit ID generato per interno del runtime di hello, `89383d32-e57e-4a9b-a6ad-57c6792aa521` è la rappresentazione di stringa hello dell'ID di partizione di Service Fabric hello,`635650083804480486` è la stringa hello rappresentazione di hello ID Replica e l'istanza del servizio dell'infrastruttura e `5008380` hello 64-bit ID generato per interno del runtime di hello utilizzare.

## <a name="list-of-performance-counters"></a>Elenco di contatori delle prestazioni
### <a name="service-method-performance-counters"></a>Contatori delle prestazioni dei metodi servizi

runtime del servizio affidabile Hello pubblica hello dopo l'esecuzione di toohello correlati i contatori delle prestazioni dei metodi del servizio.

| Nome categoria | Nome contatore | Descrizione |
| --- | --- | --- |
| Metodo del servizio Service Fabric |Invocations/Sec |Numero di volte in cui viene richiamato il metodo di servizio hello al secondo |
| Metodo del servizio Service Fabric |Average milliseconds per invocation |Metodo del servizio hello tooexecute di durata in millisecondi |
| Metodo del servizio Service Fabric |Exceptions thrown/Sec |Numero di volte in cui hello metodo del servizio ha generato un'eccezione al secondo |

### <a name="service-request-processing-performance-counters"></a>Contatori delle prestazioni di elaborazione delle richieste dei servizi
Quando un client richiama un metodo tramite un oggetto proxy del servizio, generato un messaggio di richiesta inviato servizio di gestione remota di hello rete toohello. servizio di Hello elabora il messaggio di richiesta di hello e invia un client toohello indietro di risposta. fase di esecuzione affidabile ServiceRemoting Hello pubblica hello dopo l'elaborazione della richiesta tooservice correlati i contatori delle prestazioni.

| Nome categoria | Nome contatore | Descrizione |
| --- | --- | --- |
| Servizio Service Fabric |# of outstanding requests |Numero di richieste elaborate nel servizio hello |
| Servizio Service Fabric |Average milliseconds per request |Tempo impiegato (in millisecondi) dal hello servizio tooprocess una richiesta |
| Servizio Service Fabric |Average milliseconds for request deserialization |Ora eseguito (in millisecondi) toodeserialize messaggio richiesta del servizio quando viene ricevuto nel servizio hello |
| Servizio Service Fabric |Average milliseconds for response serialization |Tempo tooserialize eseguito (in millisecondi) hello servizio messaggio di risposta al servizio hello prima dell'invio risposta hello client toohello |

## <a name="next-steps"></a>Passaggi successivi
* [Codice di esempio](https://github.com/Azure/servicefabric-samples)
* [Provider di EventSource in PerfView](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/)
