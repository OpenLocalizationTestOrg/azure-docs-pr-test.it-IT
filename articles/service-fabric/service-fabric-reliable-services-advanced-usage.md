---
title: utilizzo di aaaAdvanced dei servizi affidabili | Documenti Microsoft
description: "Informazioni sull'uso avanzato dei servizi Reliable Services di Service Fabric per una maggiore flessibilità nei servizi."
services: Service-Fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: masnider
ms.assetid: f2942871-863d-47c3-b14a-7cdad9a742c7
ms.service: Service-Fabric
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: e6d6310a4deae9edcfcd76551e1337f0e39e9e5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-usage-of-hello-reliable-services-programming-model"></a>Utilizzo dei servizi di hello affidabile modello di programmazione avanzate
Service Fabric di Azure semplifica la scrittura e la gestione di servizi affidabili con e senza stato. Questa Guida parla utilizzi avanzati di servizi affidabili toogain maggiore flessibilità e controllo tramite i servizi. Tooreading precedente questa Guida, acquisire familiarità con [modello di programmazione di servizi affidabili hello](service-fabric-reliable-services-introduction.md).

Sia i servizi con stato che i servizi senza stato hanno due punti di ingresso principali per il codice utente:

* `RunAsync(C#) / runAsync(Java)` è un punto di ingresso generico per il codice del servizio.
* `CreateServiceReplicaListeners(C#)` e `CreateServiceInstanceListeners(C#) / createServiceInstanceListeners(Java)` vengono usati per l'apertura di listener di comunicazione per le richieste client.

Per la maggior parte dei servizi questi due punti di ingresso sono sufficienti. In rari casi, quando è necessario un maggiore controllo sul ciclo di vita del servizio, sono disponibili eventi del ciclo di vita aggiuntivi.

## <a name="stateless-service-instance-lifecycle"></a>Ciclo di vita dell'istanza di servizio senza stato
Il ciclo di vita di un servizio senza stato è molto semplice. Un servizio senza stato può solo essere aperto, chiuso o interrotto. `RunAsync` viene eseguito in un servizio senza stato quando viene aperta un'istanza del servizio e viene annullato quando viene chiusa o interrotta un'istanza del servizio.

Sebbene `RunAsync` dovrebbe essere sufficiente in quasi tutti i casi, hello aprire, chiudere e gli eventi di interruzione in un servizio senza stato sono inoltre disponibili:

* `Task OnOpenAsync(IStatelessServicePartition, CancellationToken) - C# / CompletableFuture<String> onOpenAsync(CancellationToken) - Java`OnOpenAsync viene chiamato quando l'istanza del servizio senza stato hello sta toobe utilizzato. In questo momento è possibile avviare attività estese di inizializzazione del servizio.
* `Task OnCloseAsync(CancellationToken) - C# / CompletableFuture onCloseAsync(CancellationToken) - Java`OnCloseAsync viene chiamato quando l'istanza del servizio senza stato hello sta toobe arresto normalmente. Ciò può verificarsi quando viene aggiornato il codice del servizio di hello, istanza servizio hello viene spostato a causa di bilanciamento del carico tooload o viene rilevato un errore temporaneo. OnCloseAsync può essere utilizzato toosafely chiudere tutte le risorse, arrestare l'elaborazione in background, completare il salvataggio stato esterno o chiudere le connessioni esistenti.
* `void OnAbort() - C# / void onAbort() - Java`OnAbort viene chiamato quando l'istanza del servizio senza stato hello è viene arrestato in modo forzato. Si tratta in genere quando viene rilevato un errore permanente nel nodo hello o quando Service Fabric non è possibile gestire in modo affidabile del ciclo di vita dell'istanza del servizio hello a causa di errori toointernal.

## <a name="stateful-service-replica-lifecycle"></a>Ciclo di vita della replica del servizio con stato

> [!NOTE]
> Reliable Services con stato non è ancora supportato in Java.
>
>

Il ciclo di vita di una replica del servizio con stato è molto più complesso rispetto a quello di un'istanza del servizio senza stato. Inoltre tooopen, chiudere e interrompere gli eventi, una replica del servizio con stato vengono apportate modifiche di ruolo durante la relativa durata. Quando una replica del servizio con stato Modifica ruolo, hello `OnChangeRoleAsync` evento:

* `Task OnChangeRoleAsync(ReplicaRole, CancellationToken)`OnChangeRoleAsync viene chiamato durante la replica del servizio con stato hello Modifica ruolo, ad esempio tooprimary o secondario. Le repliche primarie vengono assegnate lo stato di scrittura (sono consentiti toocreate e scrivere tooReliable raccolte). Alle repliche secondarie viene assegnato lo stato di lettura (possono solo leggere da raccolte Reliable Collections esistenti). La maggior parte delle operazioni in un servizio con stato vengono eseguite nella replica primaria hello. Le repliche secondarie possono eseguire la convalida di sola lettura, la generazione di report, il data mining o altri processi di sola lettura.

In un servizio con stato, solo una replica primaria hello ha accesso in scrittura toostate e pertanto in genere quando il servizio hello sta eseguendo il lavoro effettivo. Hello `RunAsync` metodo in un servizio con stato viene eseguito solo quando replica del servizio con stato hello è primaria. Hello `RunAsync` metodo viene annullato quando le modifiche di ruolo della replica primaria dal database primario, nonché durante hello chiudono e interrompere gli eventi.

Utilizzo di hello `OnChangeRoleAsync` evento consente lavoro tooperform a seconda del ruolo della replica anche come modifica toorole di risposta.

Un servizio con stato fornisce inoltre gli eventi del ciclo di vita di hello quattro stesso come un servizio senza stato, con la stessa semantica di hello e casi d'uso:

```csharp
* Task OnOpenAsync(IStatefulServicePartition, CancellationToken)
* Task OnCloseAsync(CancellationToken)
* void OnAbort()
```

## <a name="next-steps"></a>Passaggi successivi
Per più avanzate argomenti correlati tooService dell'infrastruttura, vedere hello seguenti articoli:

* [Configurazione di Reliable Services con stato](service-fabric-reliable-services-configuration.md)
* [Introduzione all'integrità di Service Fabric](service-fabric-health-introduction.md)
* [Utilizzo dei report di integrità del sistema per la risoluzione dei problemi](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [Configurazione di servizi con hello gestione delle risorse Cluster di Service Fabric](service-fabric-cluster-resource-manager-configure-services.md)
