---
title: "Modalità di blocco e in Azure Service Fabric affidabile raccolte aaaTransactions | Documenti Microsoft"
description: Transazioni e blocco delle raccolte Reliable Collections e di Reliable State Manager in Azure Service Fabric.
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
ms.openlocfilehash: 340e029aa98f43ad6e46b48f687dad01f9d96f69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="transactions-and-lock-modes-in-azure-service-fabric-reliable-collections"></a>Transazioni e modalità di blocco delle raccolte Reliable Collections in Azure Service Fabric

## <a name="transaction"></a>Transazione
Una transazione è una sequenza di operazioni eseguite in un'unica unità logica di lavoro
Una transazione deve presentare hello seguenti proprietà ACID. (vedere https://technet.microsoft.com/it-it/library/ms190612):
* **Atomicità**: una transazione deve essere un'unità di lavoro atomica. In altre parole, devono essere eseguite tutte le modifiche dei dati oppure non ne deve essere eseguita nessuna.
* **Coerenza**: al termine della transazione, tutti i dati devono essere coerenti Tutte le strutture dati interne devono essere corrette al termine di hello della transazione hello.
* **Isolamento**: le modifiche eseguite da transazioni simultanee devono essere isolate dalle modifiche apportate da altre transazioni simultanee hello. livello di isolamento Hello utilizzato per un'operazione all'interno di un ITransaction è determinato dal hello IReliableState l'operazione di hello.
* **Durabilità**: al termine di una transazione, gli effetti sono permanenti nel sistema hello. modifiche di Hello permangono anche nell'evento hello di un errore di sistema.

### <a name="isolation-levels"></a>Livelli di isolamento
Livello di isolamento definisce il grado di hello transazione hello toowhich deve essere isolate dalle modifiche apportate da altre transazioni.
Le raccolte Reliable Collections supportano due livelli di isolamento:

* **Lettura ripetibile**: Specifica che le istruzioni non possono leggere i dati che sono stati modificati ma non ancora eseguito il commit da altre transazioni e che nessun'altra transazione possono modificare i dati letti dalla transazione corrente di hello finché hello corrente al termine della transazione. Per altre informazioni, vedere [https://msdn.microsoft.com/library/ms173763.aspx](https://msdn.microsoft.com/library/ms173763.aspx).
* **Snapshot**: Specifica che i dati letti da qualsiasi istruzione in una transazione sono versione consistente dal punto di hello di hello i dati esistenti all'inizio di hello della transazione hello.
  transazione Hello in grado di riconoscere solo le modifiche dei dati che è sono eseguito il commit prima di inizio della transazione hello hello.
  Modifiche apportate da altre transazioni dopo hello avvio della transazione corrente di hello non sono visibili toostatements esecuzione nella transazione corrente hello.
  effetto Hello è come se istruzioni hello in una transazione ottenessero uno snapshot dei dati hello eseguito il commit si trovavano all'inizio di hello di transazione hello.
  Gli snapshot tra le Reliable Collections sono coerenti.
  Per altre informazioni, vedere [https://msdn.microsoft.com/library/ms173763.aspx](https://msdn.microsoft.com/library/ms173763.aspx).

Raccolte affidabile scegliere automaticamente hello toouse livello di isolamento per una determinata operazione di lettura a seconda operazione hello e ruolo hello della replica di hello in fase di hello della creazione della transazione.
Di seguito è tabella hello che raffigura impostazioni predefinite a livello di isolamento per le operazioni di dizionario affidabile e di Accodamento.

| Operazione\Ruolo | Primario | Secondario |
| --- |:--- |:--- |
| Lettura di entità singola |Repeatable Read |Snapshot |
| Enumerazione, conteggio |Snapshot |Snapshot |

> [!NOTE]
> Alcuni esempi comuni per le operazioni sulla singola entità sono `IReliableDictionary.TryGetValueAsync` e `IReliableQueue.TryPeekAsync`.
> 

Hello dizionario affidabile e hello coda affidabile supportano entrambi scrive di lettura.
In altre parole, qualsiasi scrittura all'interno di una transazione saranno visibili tooa seguente letti appartenente toohello stessa transazione.

## <a name="locks"></a>Blocchi
In raccolte affidabile, implementano tutti di transazioni rigorosi a due fasi di blocco: una transazione non rilascia i blocchi di hello ha acquisito finché non termina la transazione hello con un'interruzione o un'operazione di commit.

L'operazione Reliable Dictionary usa il blocco a livello di riga per tutte le operazioni sulla singola entità.
L'operazione Reliable Queue bilancia la concorrenza in cambio di una proprietà FIFO transazionale rigorosa.
Reliable Queue usa i blocchi a livello di operazione che consentono una transazione con `TryPeekAsync` e/o `TryDequeueAsync` e una transazione con `EnqueueAsync` per volta.
Si noti che toopreserve FIFO, se un `TryPeekAsync` o `TryDequeueAsync` mai osserva che hello affidabile coda è vuota, anche bloccherà `EnqueueAsync`.

Le operazioni di scrittura acquisiscono sempre blocchi esclusivi.
Per le operazioni di lettura, hello blocco dipende da due fattori.
Le operazioni di lettura eseguite con Shapshot Isolation sono prive di blocchi.
Per impostazione predefinita, ogni operazione di lettura ripetibile acquisisce blocchi condivisi.
Tuttavia, per qualsiasi operazione di lettura che supporta la lettura ripetibile, utente hello può richiedere un blocco di aggiornamento anziché hello blocco condiviso.
Un blocco di aggiornamento è che un blocco asimmetrico utilizzato tooprevent una forma comune di deadlock che si verifica quando più transazioni bloccate risorse quali aggiornamenti in un secondo momento.

Matrice di compatibilità dei blocchi Hello è reperibile in hello nella tabella seguente:

| Richiesto\Concesso | Nessuno | Condiviso | Aggiornamento | Esclusivo |
| --- |:--- |:--- |:--- |:--- |
| Condiviso |Nessun conflitto |Nessun conflitto |Conflitto |Conflitto |
| Aggiornamento |Nessun conflitto |Nessun conflitto |Conflitto |Conflitto |
| Esclusivo |Nessun conflitto |Conflitto |Conflitto |Conflitto |

Argomento timeout hello affidabile API raccolte viene utilizzata per il rilevamento dei deadlock.
Ad esempio, due transazioni (T1 e T2) siano tentando di tooread e aggiornare K1.
È possibile che li toodeadlock, perché entrambi finire con hello condiviso blocco.
In questo caso, una o entrambe le operazioni di hello scadrà.

Questo scenario di deadlock è un perfetto esempio di come il blocco di aggiornamento possa impedire i deadlock.

## <a name="next-steps"></a>Passaggi successivi
* [Lavorare con le raccolte Reliable Collections](service-fabric-work-with-reliable-collections.md)
* [Notifiche di Reliable Services](service-fabric-reliable-services-notifications.md)
* [Eseguire il backup e il ripristino di Reliable Services (ripristino di emergenza)](service-fabric-reliable-services-backup-restore.md)
* [Reliable State Manager configuration (Configurazione di Reliable State Manager)](service-fabric-reliable-services-configuration.md)
* [Guida di riferimento per gli sviluppatori per Reliable Collections](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

