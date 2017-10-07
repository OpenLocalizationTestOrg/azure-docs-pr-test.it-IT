---
title: 'Aggiornamento di un''applicazione: serializzazione dei dati | Microsoft Docs'
description: "Procedure consigliate per la serializzazione dei dati e descrizione della sua influenza sugli aggiornamenti dell’applicazione in sequenza."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: a5f36366-a2ab-4ae3-bb08-bc2f9533bc5a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 1b65dfd3813423550631490640a81953864f58e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-data-serialization-affects-an-application-upgrade"></a>Come la serializzazione dei dati influenzi l’aggiornamento di un’applicazione
In un [aggiornamento in sequenza](service-fabric-application-upgrade.md), hello aggiornamento è stato applicato tooa sottoinsieme di nodi, un dominio di aggiornamento alla volta. Durante questo processo, alcuni domini di aggiornamento sono nella versione più recente di hello dell'applicazione e alcuni domini di aggiornamento sono in una versione precedente dell'applicazione hello. Durante l'implementazione di hello, hello nuova versione dell'applicazione deve essere in grado di tooread hello precedente dei dati e hello precedente versione dell'applicazione deve essere in grado di tooread hello nuova dei dati. Se formato dati hello non avanti e indietro aggiornamento hello compatibile, potrebbero non viene eseguito o, ancora peggio, dati potrebbe essere perso o danneggiato. Questo articolo illustra come è costituito il formato dei dati e riporta le procedure consigliate per garantire che i dati siano compatibili con le versioni successive e precedenti.

## <a name="what-makes-up-your-data-format"></a>Come è costituito il formato dei dati
In Azure Service Fabric, dati hello sono persistente e replicati provengono dalle classi c#. Per le applicazioni che utilizzano [raccolte affidabile](service-fabric-reliable-services-reliable-collections.md), che i dati sono oggetti hello in dizionari affidabile hello e code. Per le applicazioni che utilizzano [Reliable Actors](service-fabric-reliable-actors-introduction.md), vale a dire hello il backup dello stato per attore hello. Queste classi c# devono essere serializzabili toobe persistente e replicato. Pertanto, il formato di dati hello è definito da hello campi e proprietà che vengono serializzate, nonché come vengono serializzate. Ad esempio, in un `IReliableDictionary<int, MyClass>` dati hello viene serializzata `int` e serializzata `MyClass`.

### <a name="code-changes-that-result-in-a-data-format-change"></a>Il codice modifica quel risultato trasformandolo in una modifica del formato dei dati
Poiché il formato di dati hello è determinato dalle classi in c#, classi toohello modifiche possono provocare una modifica di formato di dati. Prestare attenzione tooensure in grado di gestire un aggiornamento in sequenza modifica il formato hello. Esempi di operazioni che possono comportare modifiche del formato dei dati:

* Aggiunta o rimozione di campi o proprietà
* Ridenominazione di campi o proprietà
* Modifica dei tipi di campi o proprietà hello
* Modifica il nome di classe hello o dello spazio dei nomi

### <a name="data-contract-as-hello-default-serializer"></a>Contratto dati come serializzatore predefinito hello
serializzatore Hello è in genere responsabile della lettura dei dati hello e la deserializzazione nella versione corrente di hello, anche se i dati di hello in una precedente o *più recente* versione. serializzatore predefinito Hello è hello [serializzatore dei contratti dati](https://msdn.microsoft.com/library/ms733127.aspx), che dispone di regole di controllo delle versioni ben definito. Le raccolte consentono hello serializzatore toobe sottoposto a override, ma Reliable Actors attualmente non è affidabile. serializzatore dei dati Hello svolge un ruolo importante per consentire gli aggiornamenti in sequenza. serializzatore dei contratti dati Hello è il serializzatore hello che è consigliabile per le applicazioni di Service Fabric.

## <a name="how-hello-data-format-affects-a-rolling-upgrade"></a>Impatto di un aggiornamento in sequenza formato dati hello
Durante un aggiornamento in sequenza, esistono due scenari principali in cui può verificarsi una serializzatore hello o *più recente* versione dei dati:

1. Dopo che un nodo è aggiornato e inizia a eseguire il backup, serializzatore nuovo hello caricherà i dati di hello che è stato persistente toodisk dalla versione precedente di hello.
2. Durante l'aggiornamento in sequenza di hello, cluster hello conterrà una combinazione di versioni nuove e precedenti di hello del codice. Poiché le repliche possono essere inserite in diversi domini di aggiornamento e le repliche inviano dati tooeach altri, hello nuovi e/o precedente versione dei dati può essere rilevati dalla versione nuovi e/o precedente di hello del serializzatore.

> [!NOTE]
> Hello "nuova versione" e "precedente" riferimento qui toohello versione del codice che è in esecuzione. Hello "nuovo serializzatore" fa riferimento codice serializzatore toohello è in esecuzione nella nuova versione di hello dell'applicazione. Hello "nuovi dati" si riferisce classe c# toohello serializzato dalla nuova versione di hello dell'applicazione.
> 
> 

Hello due versioni del codice e il formato di dati deve essere avanti e indietro compatibile. Se non sono compatibili, hello aggiornamento in sequenza potrebbe non riuscire o dati potrebbero andare persi. Hello aggiornamento in sequenza potrebbe non riuscire perché codice hello o serializzatore può generare eccezioni o un errore quando rileva hello altra versione. Dati potrebbero essere persi se, ad esempio, è stata aggiunta una nuova proprietà ma serializzatore precedente hello vengono eliminati durante la deserializzazione.

Contratto dati è hello consigliata le soluzioni per assicurare che i dati siano compatibili. Include regole ben definite di controllo delle versioni per l'aggiunta, la rimozione e la modifica di campi. Include inoltre il supporto per occupa campi sconosciuti, associazione nel processo di serializzazione e deserializzazione hello e gestiscono l'ereditarietà della classe. Per altre informazioni, vedere [Utilizzo di contratti dati](https://msdn.microsoft.com/library/ms733127.aspx).

## <a name="next-steps"></a>Passaggi successivi
[Esercitazione sull'aggiornamento di un'applicazione di Service Fabric tramite Visual Studio](service-fabric-application-upgrade-tutorial.md) descrive la procedura di aggiornamento di un'applicazione con Visual Studio.

[Aggiornamento di un'applicazione di Service Fabric mediante PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) descrive la procedura di aggiornamento di un'applicazione tramite PowerShell.

Controllare l’aggiornamento dell'applicazione tramite [Parametri di aggiornamento](service-fabric-application-upgrade-parameters.md).

Informazioni su come toouse funzionalità avanzate durante l'aggiornamento dell'applicazione riferendosi troppo[argomenti avanzati](service-fabric-application-upgrade-advanced.md).

Risolvere i problemi comuni negli aggiornamenti dell'applicazione riferendosi passaggi toohello [risoluzione dei problemi gli aggiornamenti dell'applicazione ](service-fabric-application-upgrade-troubleshooting.md).

