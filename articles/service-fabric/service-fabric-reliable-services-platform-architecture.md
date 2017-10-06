---
title: architettura del servizio aaaReliable | Documenti Microsoft
description: Panoramica dell'architettura di servizio affidabile hello per i servizi con stati e senza stati
services: service-fabric
documentationcenter: .net
author: AlanWarwick
manager: timlt
editor: vturecek
ms.assetid: af002ae6-7f6d-4769-b049-82aa1ba0891b
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/30/2016
ms.author: alanwar
redirect_url: /azure/service-fabric/service-fabric-reliable-services-introduction
ms.openlocfilehash: d2d0ec9600275ae248ab7717be269cc7204a1e4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="architecture-for-stateful-and-stateless-reliable-services"></a>Architettura per servizi Reliable Services con e senza stato
Un servizio Reliable Services di Azure Service Fabric può essere con o senza stato. Ogni tipo di servizio viene eseguito all'interno di un'architettura specifica, descritta in questo articolo.
Vedere hello [Cenni preliminari sul servizio affidabile](service-fabric-reliable-services-introduction.md) per ulteriori informazioni sulle differenze di hello tra i servizi con stati e senza stati.

## <a name="stateful-reliable-services"></a>Reliable Services con stato
### <a name="architecture-of-a-stateful-service"></a>Architettura di un servizio con stato
![Diagramma dell'architettura di un servizio con stato](./media/service-fabric-reliable-services-platform-architecture/reliable-stateful-service-architecture.png)

### <a name="stateful-reliable-service"></a>Reliable Services con stato
Un servizio affidabile con stato possono derivare da hello StatefulService o classe StatefulServiceBase. Queste classi di base sono entrambe fornite da Service Fabric Offrono vari livelli di astrazione per hello servizio con stato toointerface con Service Fabric - e tooparticipate come servizio all'interno di cluster di Service Fabric hello e supporto.

La classe StatefulService deriva dalla classe StatefulServiceBase, StatefulServiceBase più flessibile di servizi, ma richiede più comprensione delle caratteristiche interne di hello di Service Fabric.
Vedere hello [Cenni preliminari sul servizio affidabile](service-fabric-reliable-services-introduction.md) e [servizio affidabile utilizzo avanzato](service-fabric-reliable-services-advanced-usage.md) per ulteriori informazioni sulle specifiche di hello di scrittura di servizi utilizzando le classi StatefulService e StatefulServiceBase hello .

Entrambe le classi base gestiscono durata hello e ruolo hello dell'implementazione del servizio. implementazione del servizio Hello può eseguire l'override di metodi virtuali della classe base se implementazione del servizio hello ha toodo lavoro tali punti hello ciclo di vita per l'implementazione del servizio, o se è richiesto un oggetto listener di comunicazione toocreate. Si noti che anche se un'implementazione del servizio può implementare il proprio oggetto listener di comunicazione esposizione ICommunicationListener, nel diagramma hello precedente, il listener di comunicazione hello è implementato mediante Service Fabric--come hello implementazione del servizio utilizza un listener di comunicazione che viene implementato dall'infrastruttura del servizio.

Un servizio con stato affidabile utilizza hello stato affidabile manager tootake sfruttare raccolte affidabile. Raccolte affidabile sono strutture di dati locali servizio - toohello a disponibilità elevata, siano sempre disponibili, indipendentemente dal failover del servizio. Ogni tipo di raccolta Reliable Collections viene implementato da un provider di stato affidabile.
Per ulteriori informazioni sulle raccolte affidabile, vedere hello [informazioni generali sulle raccolte affidabile](service-fabric-reliable-services-reliable-collections.md).

### <a name="reliable-state-manager-and-state-providers"></a>Reliable state manager e provider di stato
gestore degli stati affidabile Hello è oggetto di hello che gestisce i provider di stato affidabile. Include toocreate funzionalità hello, eliminare, enumerare e verificare che il provider di stato affidabile hello siano persistenti e a disponibilità elevata. Un'istanza di un provider di stato affidabile rappresenta un'istanza di una struttura dati persistente e a disponibilità elevata, ad esempio un dizionario o una coda.

Ogni provider di stato affidabile espone un'interfaccia che viene utilizzata da un toointeract informazioni sullo stato del servizio con il provider di stato affidabile hello. Ad esempio, IReliableDictionary è toointerface utilizzati con dizionario affidabile hello, mentre IReliableQueue è toointerface utilizzato con la coda affidabile hello. Tutti i provider di stato affidabili implementano hello IReliableState.

gestore degli stati affidabile Hello è un'interfaccia denominata IReliableStateManager, che consente accesso tooit da un servizio con stato. Vengono restituiti i provider di stato di interfacce tooreliable tramite IReliableStateManager.

gestore degli stati affidabile Hello utilizza un'architettura plug-in modo che i nuovi tipi di raccolte affidabile possono essere collegati in modo dinamico.

dizionario affidabile Hello e affidabile coda vengono compilate al momento dell'implementazione di hello di un archivio differenziale ad alte prestazioni, con controllo delle versioni.

### <a name="transactional-replicator"></a>Transactional Replicator
componente replicatore transazionale di Hello è responsabile dell'applicazione che lo stato di hello di un servizio (ovvero, hello lo stato all'interno di hello affidabile di gestione dello stato e le raccolte affidabile hello) sia coerenza in tutte le repliche in esecuzione il servizio di hello. Garantisce inoltre che lo stato di hello è persistente nel registro hello. salve le interfacce di gestione stato affidabile con replicatore transazionale di hello tramite un meccanismo privato.

Replicatore transazionale di Hello utilizza uno stato toocommunicate protocollo di rete con altre repliche hello di istanze del servizio in modo che tutte le repliche informazioni aggiornate sullo stato.

Replicatore transazionale di Hello utilizza le informazioni sullo stato di toopersist un log in modo che le informazioni sullo stato di hello resta processo o arresti anomali di nodo. log di toohello interfaccia Hello è tramite un meccanismo privato.

### <a name="log"></a>Log
componente log Hello fornisce un archivio permanente ad alte prestazioni che può essere ottimizzato per la scrittura toospinning o dischi SSD.  progettazione di Hello del log hello è per l'archiviazione permanente (ad esempio, dischi rigidi) hello toobe toohello locale nodi che eseguono servizio con stato hello. Ciò consente di bassa latenza e velocità effettiva elevata, come archiviazione tooremote confrontati persistente, non è il nodo locale toohello.

componente log Hello utilizza più file di log. È un file di log condiviso a livello di nodo che tutte le repliche di utilizzano come può fornire latenza più bassa hello e velocità effettiva più elevata per l'archiviazione dei dati dello stato. Per impostazione predefinita log condiviso hello viene inserito nella directory di lavoro di hello Service Fabric nodo, ma può essere inoltre configurato toobe posizionato in corrispondenza di un altro percorso, in teoria su disco riservato solo i log condiviso hello. Ogni replica per il servizio hello include inoltre un file di log dedicato e log dedicato hello viene inserito nella directory di lavoro del servizio di hello. Non vi è alcun toobe di log meccanismo tooconfigure hello dedicato posizionato in corrispondenza di un percorso diverso.

log condiviso Hello è un'area di transizione per le informazioni sullo stato della replica hello è durante hello file di log dedicato in cui viene mantenuta la destinazione finale hello. In questa struttura, informazioni sullo stato hello primo file di log condiviso toohello scritta e quindi vengono spostati in modo differito toohello i file di log dedicato in background hello. In questo modo, hello scrittura toohello condivisa log avrebbe latenza più bassa hello e velocità effettiva più elevata che consente lo stato di avanzamento di hello servizio toomake più velocemente.

Legge e scrive i log condiviso toohello vengono eseguite tramite diretto IO toopreallocated lo spazio su disco hello hello condivisa file di log. tooallow un utilizzo ottimale dello spazio su disco nell'unità di hello con log dedicato, file di log dedicato hello viene creato come un file sparse NTFS. Si noti che in questo modo sarà overprovisioning di spazio su disco e hello del sistema operativo verrà visualizzato il file di log di hello dedicato con maggiore spazio su disco rispetto a quella effettivamente utilizzata.

A parte di un log toohello dell'interfaccia utente-modalità minima, i log hello viene scritta come un driver in modalità kernel. Eseguito come un driver in modalità kernel, log hello può offrire prestazioni più elevate hello tooall servizi che lo utilizzano.

Per ulteriori informazioni sulla configurazione di log di hello, vedere [configurazione servizi affidabili con stato](service-fabric-reliable-services-configuration.md).

## <a name="stateless-reliable-service"></a>Reliable Services senza stato
### <a name="architecture-of-a-stateless-service"></a>Architettura di un servizio senza stato
![Diagramma dell'architettura di un servizio senza stato](./media/service-fabric-reliable-services-platform-architecture/reliable-stateless-service-architecture.png)

### <a name="stateless-reliable-service"></a>Reliable Services senza stato
Le implementazioni del servizio senza stato derivano da hello StatelessService o classe StatelessServiceBase. classe StatelessServiceBase Hello consente una maggiore flessibilità rispetto hello StatelessService classe.
Entrambe le classi base gestiscono hello durata e il ruolo di un servizio.

implementazione del servizio Hello può eseguire l'override di metodi virtuali della classe base se servizio hello ha toodo lavoro tali punti nel ciclo di vita del servizio hello - o se vuole toocreate un oggetto listener di comunicazione. Si noti che anche se il servizio hello può implementare il proprio oggetto listener di comunicazione esposizione ICommunicationListener, nel diagramma hello precedente, il listener di comunicazione hello viene implementato dall'infrastruttura di servizio, come l'implementazione del servizio che utilizza una comunicazione listener che viene implementato dall'infrastruttura del servizio.

Vedere hello [Cenni preliminari sul servizio affidabile](service-fabric-reliable-services-introduction.md) e [servizio affidabile utilizzo avanzato](service-fabric-reliable-services-advanced-usage.md) per ulteriori informazioni sulle specifiche di hello di scrittura di servizi utilizzando le classi StatelessService e StatelessServiceBase hello .

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni su Service Fabric, vedere:

[Panoramica di Reliable Services](service-fabric-reliable-services-introduction.md)

[Avvio rapido](service-fabric-reliable-services-quick-start.md)

[Introduzione alle Reliable Collections](service-fabric-reliable-services-reliable-collections.md)

[Uso avanzato del modello di programmazione Reliable Services](service-fabric-reliable-services-advanced-usage.md)

[Configurazione di Reliable Services con stato](service-fabric-reliable-services-configuration.md)  

