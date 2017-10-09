---
title: aaaGuidelines & indicazioni per le raccolte affidabile in Azure Service Fabric | Documenti Microsoft
description: Linee guida e consigli per l'uso di Reliable Collections in Service Fabric
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
ms.date: 5/3/2017
ms.author: mcoskun
ms.openlocfilehash: bcdbc9d013bc044e06c43761e7f515c7e4bf340c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="guidelines-and-recommendations-for-reliable-collections-in-azure-service-fabric"></a>Linee guida e consigli per Reliable Collections in Azure Service Fabric
Questa sezione fornisce le linee guida per l'uso di Reliable State Manager e Reliable Collections. obiettivo di Hello è toohelp utenti evitano trappole comuni.

linee guida Hello sono organizzate come semplici raccomandazione preceduti termini hello *si*, *provare a*, *evitare* e *non*.

* Non modificare un oggetto di tipo personalizzato restituito dalle operazioni di lettura, ad esempio `TryPeekAsync` o `TryGetValueAsync`. Raccolte affidabile, come raccolte concorrenti, restituiscono un oggetto di riferimento toohello e non una copia.
* Eseguire hello copia completa restituito l'oggetto di un tipo personalizzato prima di modificarla. Poiché le strutture e tipi incorporati sono pass-by-value, non è necessario toodo una copia completa su di essi.
* Non usare `TimeSpan.MaxValue` per i timeout. Valori di timeout deve essere utilizzato toodetect deadlock.
* Non usare una transazione dopo che ne è stato eseguito il commit, è stata interrotta o eliminata.
* Non utilizzare di fuori dell'ambito di transazione hello in che è stata creata un'enumerazione.
* Non creare una transazione all'interno dell'istruzione `using` di un'altra transazione. Questa operazione può causare deadlock.
* Verificare che l'implementazione di `IComparable<TKey>` sia corretta. sistema Hello assume una dipendenza dal `IComparable<TKey>` per unire i checkpoint e righe.
* Utilizzare il blocco di aggiornamento durante la lettura di un elemento con un tooupdate intenzione è tooprevent una determinata classe di deadlock.
* Si consiglia di conservare gli elementi (ad esempio, TKey + TValue per dizionario affidabile) inferiore a 80 Kbyte: hello più piccolo migliorato. In questo modo si riduce la quantità hello dei requisiti dei / o di utilizzo come disco e rete Heap oggetti grandi. Spesso, si riduce la replica dei dati duplicati quando viene aggiornata solo una piccola parte del valore di hello. Tooachieve modo comune nel dizionario affidabile, si tratta toobreak le righe in toomultiple righe.
* È consigliabile usare backup e ripristino di emergenza toohave funzionalità.
* Evitare di utilizzare operazioni di entità singola e a più entità (ad esempio `GetCountAsync`, `CreateEnumerableAsync`) in hello stessa transazione a causa di toohello diversi livelli di isolamento.
* Gestire InvalidOperationException. Le transazioni utente possono essere interrotta dal sistema hello per diversi motivi. Ad esempio, quando cambia il proprio ruolo fuori primario hello affidabile di gestione dello stato quando una transazione con esecuzione prolungata è bloccato o il troncamento del log delle transazioni hello. In questi casi, l'utente può ricevere un evento InvalidOperationException, che indica che la transazione è già stata terminata. Supponendo che, terminazione hello di transazione hello non è stata richiesta dall'utente hello, toohandle modo migliore questa eccezione è transazione hello toodispose, verificare se è stato segnalato il token di annullamento hello (o è stato modificato il ruolo di hello della replica di hello), e in caso contrario creare una nuova transazione e riprovare.  

Ecco alcuni aspetti tookeep presente:

* timeout predefinito Hello è 4 secondi per hello tutte le API insieme affidabile. La maggior parte degli utenti devono utilizzare timeout predefinito hello.
* è Hello token di annullamento predefinito `CancellationToken.None` in tutte le API raccolte affidabile.
* parametro di tipo chiave Hello (*TKey*) per un dizionario affidabile devono correttamente implementare `GetHashCode()` e `Equals()`. Le chiavi non devono essere modificabili.
* tooachieve la disponibilità elevata per le raccolte affidabile hello, ogni servizio deve disporre di almeno una destinazione e repliche minimo pari a 3.
* Le operazioni di lettura su hello secondaria possono leggere le versioni che non è stato eseguito il commit di quorum.
  Ciò significa che una versione dei dati che viene letta da un singolo secondario potrebbe essere elaborata in modo non corretto.
  Le letture della replica primaria sono sempre stabili: non sono mai elaborate in modo non corretto.

### <a name="next-steps"></a>Passaggi successivi
* [Lavorare con le raccolte Reliable Collections](service-fabric-work-with-reliable-collections.md)
* [Transazioni e blocchi](service-fabric-reliable-services-reliable-collections-transactions-locks.md)
* [Elementi interni di Reliable Collections e Reliable State Manager](service-fabric-reliable-services-reliable-collections-internals.md)
* Gestione dei dati
  * [Backup e ripristino](service-fabric-reliable-services-backup-restore.md)
  * [Notifications](service-fabric-reliable-services-notifications.md)
  * [Serializzazione e aggiornamento](service-fabric-application-upgrade-data-serialization.md)
  * [Reliable State Manager configuration (Configurazione di Reliable State Manager)](service-fabric-reliable-services-configuration.md)
* Altro
  * [Guida introduttiva a Reliable Services di Microsoft Azure Service Fabric](service-fabric-reliable-services-quick-start.md)
  * [Guida di riferimento per gli sviluppatori per Reliable Collections](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
