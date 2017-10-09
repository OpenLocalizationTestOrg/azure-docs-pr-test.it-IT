---
title: elementi interni affidabile stato gestione di servizi dell'infrastruttura e un insieme affidabile aaaAzure | Documenti Microsoft
description: Approfondimento dei concetti e della progettazione delle raccolte Reliable Collections in Azure Service Fabric.
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: rajak
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: mcoskun
ms.openlocfilehash: 651bfb52785a2475e4840cd471e87220d1936391
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-reliable-state-manager-and-reliable-collection-internals"></a>Elementi interni delle raccolte Reliable Collections e di Reliable State Manager in Azure Service Fabric
Questo documento affronta all'interno di raccolte affidabile e affidabile di gestione dello stato toosee funzionano dei componenti di base di background hello.

> [!NOTE]
> Il documento è in continua evoluzione Aggiungere commenti toothis articolo tootell us l'argomento desiderato toolearn ulteriori informazioni.
>

##  <a name="local-persistence-model-log-and-checkpoint"></a>Modello di persistenza locale: log e checkpoint
Hello affidabile di gestione dello stato e le raccolte affidabile seguono un modello di persistenza che viene chiamato Log e dei Checkpoint.
In questo modello ogni cambiamento di stato viene registrato per prima cosa sul disco e quindi applicato in memoria.
Hello completo dallo stato viene mantenuto solo occasionalmente (anche noto come Checkpoint).
Il vantaggio di Hello è che delta viene convertiti in solo di Accodamento scritture sequenziali su disco per migliorare le prestazioni.

toobetter comprendere hello Log e il modello di Checkpoint, esaminiamo innanzitutto scenario disco infinito hello.
prima viene replicato, Hello affidabile di gestione dello stato registra ogni operazione.
La registrazione consente hello raccolte affidabile tooapply hello operazione solo in memoria.
Poiché i registri sono persistenti, anche quando si verifica un errore di replica hello e toobe riavviato, è necessario hello affidabile di gestione dello stato ha informazioni sufficienti nel relativo tooreplay log tutte le operazioni di hello ha perso la replica hello.
Come disco di hello è infinito, i record del log non necessario mai toobe rimosso e la raccolta affidabile hello deve toomanage solo lo stato di hello in memoria.

Ora esaminiamo scenario disco finito hello.
Come record di log si accumulano, verrà eseguita hello affidabile di gestione dello stato spazio su disco insufficiente.
Prima che si verifichi, hello affidabile di gestione dello stato deve tootruncate della sua room toomake log per i record più recenti di hello.
Le richieste di gestione dello stato di affidabile hello raccolte affidabile toocheckpoint toodisk loro stato in memoria.
A questo punto, hello raccolte affidabile' verrebbe persistente lo stato di in memoria.
Una volta raccolte affidabile hello completare i checkpoint, hello affidabile di gestione dello stato possibile troncare hello log toofree spazio su disco.
Quando replica hello deve toobe riavviato, raccolte affidabile ripristinare lo stato di Checkpoint e ripristina hello affidabile di gestione dello stato e tutte le modifiche di stato hello che si sono verificati dall'ultimo checkpoint hello viene riprodotto.

L'aggiunta di un altro valore di checkpoint migliora i tempi di ripristino negli scenari comuni. Log contiene tutte le operazioni che si sono verificati dall'ultimo checkpoint hello.
Pertanto, può includere più versioni di un elemento come più valori per una determinata riga in Reliable Dictionary.
Al contrario, un checkpoint insieme affidabile hello solo la versione più recente di ogni valore per una chiave.

## <a name="next-steps"></a>Passaggi successivi
* [Transazioni e blocchi](service-fabric-reliable-services-reliable-collections-transactions-locks.md)

