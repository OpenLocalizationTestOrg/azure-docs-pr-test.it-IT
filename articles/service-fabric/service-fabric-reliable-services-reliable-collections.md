---
title: aaaIntroduction tooReliable raccolte in servizi di Azure Service Fabric con stati | Documenti Microsoft
description: Servizi di Service Fabric con stati forniscono affidabile raccolte che consentono di applicazioni cloud altamente disponibile, scalabili e a bassa latenza toowrite.
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: masnider,rajak
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: mcoskun
ms.openlocfilehash: 9f67c48f13e8b91b84977e127e2545cbb9d9a158
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooreliable-collections-in-azure-service-fabric-stateful-services"></a>Introduzione tooReliable raccolte in servizi di Azure Service Fabric con stati
Affidabile raccolte consentono di applicazioni cloud altamente disponibile, scalabili e a bassa latenza toowrite come se si sono scrivendo applicazioni per singolo computer. classi di hello Hello **Microsoft.ServiceFabric.Data.Collections** dello spazio dei nomi forniscono un set di raccolte che automaticamente lo stato a disponibilità elevata. Gli sviluppatori devono tooprogram solo toohello API insieme affidabile e gestire raccolte affidabile hello replicati e lo stato locale.

Hello chiave differenza tra le raccolte affidabile e altre tecnologie di disponibilità elevata (ad esempio Redis, il servizio tabelle di Azure e servizio di Accodamento di Azure) consiste nel fatto che lo stato di hello viene mantenuto localmente nell'istanza di servizio hello mentre vengono applicate anche a disponibilità elevata. Ciò significa che:

* Tutte le operazioni di lettura sono locali, assicurando quindi bassa latenza e velocità effettiva elevata.
* Tutte le scritture comportano un numero minimo di hello come di rete IOs, determinando di bassa latenza e velocità effettiva elevata scrive.

![Immagine dell'evoluzione delle raccolte.](media/service-fabric-reliable-services-reliable-collections/ReliableCollectionsEvolution.png)

Raccolte affidabile possono essere considerate come hello naturale evoluzione hello **System. Collections** classi: un nuovo set di raccolte che sono progettati per le applicazioni cloud e multi-computer hello senza aumentare la complessità per developer Hello. Come tali, le raccolte Reliable Collections sono:

* Replicate: le modifiche apportate allo stato vengono replicate per assicurare disponibilità elevata.
* Persistente: I dati sono toodisk persistente per la durabilità da interruzioni di grandi dimensioni (ad esempio, un Data Center di alimentazione).
* Asincrono: API sono tooensure asincrona che i thread non vengono bloccati quando incorrere in IO.
* Transazionale: API utilizzano astrazione hello di transazioni in modo da gestire con facilità più affidabile raccolte all'interno di un servizio.

Raccolte affidabile garantisce una coerenza assoluta fuori toomake casella hello ragionamento sullo stato dell'applicazione più semplice.
Coerenza assoluta avviene garantendo transazione commit fine solo dopo che l'intera transazione hello è connesso un quorum maggioranza delle repliche, inclusa hello primario.
coerenza debole tooachieve, applicazioni possono riguardare toohello back-client/richiedente prima che venga restituito con commit asincrono hello.

API raccolte affidabile Hello sono un'evoluzione di raccolte concorrenti API (trovato nell'hello **System.Collections.Concurrent** dello spazio dei nomi):

* Asincrona: Restituisce un'attività poiché, diversamente dalle raccolte simultanee, le operazioni di hello vengono replicate e resi persistenti.
* Parametri out non: Usa `ConditionalValue<T>` tooreturn bool e un valore anziché i parametri out. `ConditionalValue<T>`è ad esempio `Nullable<T>` , ma non richiede T toobe uno struct.
* Transazioni: Usa un toogroup azioni dell'utente hello transazione oggetto tooenable in più raccolte affidabile in una transazione.

Attualmente **Microsoft.ServiceFabric.Data.Collections** include tre raccolte:

* [ReliableDictionary](https://msdn.microsoft.com/library/azure/dn971511.aspx): rappresenta una raccolta replicata, transazionale e asincrona di coppie chiave/valore. Simile troppo**ConcurrentDictionary**, entrambi hello chiave e valore hello può essere di qualsiasi tipo.
* [ReliableQueue](https://msdn.microsoft.com/library/azure/dn971527.aspx): rappresenta una coda FIFO (First-In First-Out) replicata, transazionale e asincrona. Simile troppo**ConcurrentQueue**, hello valore può essere di qualsiasi tipo.
* [ReliableConcurrentQueue](service-fabric-reliable-services-reliable-concurrent-queue.md): rappresenta una coda di ordinamento ottimale replicata, transazionale e asincrona per la velocità effettiva elevata. Toohello simile **ConcurrentQueue**, hello valore può essere di qualsiasi tipo.

## <a name="next-steps"></a>Passaggi successivi
* [Linee guida e consigli per Reliable Collections](service-fabric-reliable-services-reliable-collections-guidelines.md)
* [Lavorare con le raccolte Reliable Collections](service-fabric-work-with-reliable-collections.md)
* [Transazioni e blocchi](service-fabric-reliable-services-reliable-collections-transactions-locks.md)
* [Elementi interni di Reliable Collections e Reliable State Manager](service-fabric-reliable-services-reliable-collections-internals.md)
* Gestione dei dati
  * [Backup e ripristino](service-fabric-reliable-services-backup-restore.md)
  * [Notifications](service-fabric-reliable-services-notifications.md)
  * [Serializzazione di raccolte Reliable Collections](service-fabric-reliable-services-reliable-collections-serialization.md)
  * [Serializzazione e aggiornamento](service-fabric-application-upgrade-data-serialization.md)
  * [Reliable State Manager configuration (Configurazione di Reliable State Manager)](service-fabric-reliable-services-configuration.md)
* Altro
  * [Guida introduttiva a Reliable Services di Microsoft Azure Service Fabric](service-fabric-reliable-services-quick-start.md)
  * [Guida di riferimento per gli sviluppatori per Reliable Collections](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
