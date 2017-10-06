---
title: aaaOverview di hello del ciclo di vita di servizi di Azure Service Fabric affidabile | Documenti Microsoft
description: Informazioni sugli eventi del ciclo di vita diversi hello in servizi di Service Fabric affidabili
services: Service-Fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: vturecek;
ms.assetid: 
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 0d75ed5ee7cda85ac9af6a02e160727277804a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-services-lifecycle-overview"></a>Panoramica del ciclo di vita di Reliable Services
> [!div class="op_single_selector"]
> * [C# su Windows](service-fabric-reliable-services-lifecycle.md)
> * [Java su Linux](service-fabric-reliable-services-lifecycle-java.md)
>
>

Quando si pensa hello cicli di vita di servizi affidabili, funzionalità di base di hello del ciclo di vita hello sono hello più importante. In generale:

- Durante l'avvio
  - I servizi vengono costruiti
  - Hanno un tooconstruct opportunità e restituire zero o più listener
  - Qualsiasi listener restituito sono aperte, consentendo la comunicazione con il servizio hello
  - RunAsync Hello del servizio viene chiamato, consentendo di hello servizio toodo a esecuzione prolungata o lavoro in background
- Durante l'arresto
  - tooRunAsync passato di Hello annullamento token viene annullato e vengono chiuse listener hello
  - Una volta completato, hello servizio oggetto eliminato

Sono disponibili informazioni dettagliate sugli hello esatto di ordinamento di questi eventi. In particolare, ordine hello degli eventi può cambiare leggermente a seconda che sia di hello servizio affidabile Stateless o informazioni sullo stato. Inoltre, per i servizi con stati, abbiamo toodeal con uno scenario di scambio primario hello. Durante questa sequenza, ruolo hello database primario replica tooanother trasferiti (o torna) senza l'arresto del servizio hello. Infine, abbiamo toothink sulle condizioni di errore o di.

## <a name="stateless-service-startup"></a>Avvio di un servizio senza stato
Hello ciclo di vita di un servizio senza stato è piuttosto semplice. Ecco l'ordine di hello degli eventi:

1. Hello servizio viene costruito
2. Quindi si verificano due cose in parallelo:
    - Viene richiamato `StatelessService.CreateServiceInstanceListeners()` e vengono aperti eventuali listener restituiti. Viene richiamato `ICommunicationListener.OpenAsync()` su ogni listener
    - Hello del servizio `StatelessService.RunAsync()` viene chiamato
3. Se presente, hello del servizio `StatelessService.OnOpenAsync()` viene chiamato. Si tratta di un override insolito ma comunque disponibile.

È importante toonote che non vi sia alcun ordinamento tra toocreate chiamate hello e i listener hello aperto e RunAsync. listener Hello venga aperto prima dell'avvio di RunAsync. Analogamente, RunAsync rischia di richiamato prima che il listener di comunicazione hello è aperto o anche costruito. Se è necessario eseguire qualsiasi sincronizzazione, viene lasciato in qualità di implementatore toohello esercizio. Soluzioni comuni:

  - Talvolta i listener non possono funzionare fino a quando non vengono create altre informazioni o eseguite determinate operazioni. Per i servizi senza stato le cui operazioni possono essere in genere eseguite in altre posizioni, ad esempio: 
    - nel costruttore del servizio hello
    - durante la hello `CreateServiceInstanceListeners()` chiamare
    - come parte della costruzione di hello del listener hello stesso
  - Hello codice RunAsync non talvolta toostart fino a quando non sono aperti listener hello. In questo caso è necessario un po' di coordinamento in più. Una soluzione comune è alcuni flag all'interno di listener hello che indica quando è stata completata. Questo flag viene quindi archiviato RunAsync prima di continuare a utilizzare tooactual.

## <a name="stateless-service-shutdown"></a>Arresto di un servizio senza stato
Quando un servizio senza stato di arresto, hello stesso modello viene seguito, solo in senso inverso:

1. In parallelo
    - Gli eventuali listener aperti vengono chiusi. Viene richiamato `ICommunicationListener.CloseAsync()` su ogni listener.
    - token di annullamento Hello passato troppo`RunAsync()` viene annullata. Del controllo hello token di annullamento `IsCancellationRequested` proprietà restituisce true e se la chiamata del token hello `ThrowIfCancellationRequested` metodo genera un `OperationCanceledException`.
2. Una volta `CloseAsync()` completa per ogni listener e `RunAsync()` completa inoltre del servizio hello `StatelessService.OnCloseAsync()` metodo viene chiamato, se presente. È comune toooverride `StatelessService.OnCloseAsync()`.
3. Dopo aver `StatelessService.OnCloseAsync()` viene completato, viene eliminato l'oggetto servizio hello

## <a name="stateful-service-startup"></a>Avvio di un servizio con stato
Servizi con stati hanno un servizi toostateless modello simile, con poche modifiche. All'avvio di un servizio con stato, ordine di hello degli eventi è come segue:

1. Hello servizio viene costruito
2. Viene chiamato `StatefulServiceBase.OnOpenAsync()`. Questo viene eseguito l'override uncommonly nel servizio hello.
3. Hello eseguite le operazioni seguenti in parallelo
    - Viene richiamato `StatefulServiceBase.CreateServiceReplicaListeners()`. 
      - Se il servizio di hello è un database primario vengono aperti tutti i listener restituiti. Viene richiamato `ICommunicationListener.OpenAsync()` su ogni listener.
      - Se il servizio di hello è un database secondario, solo i listener è contrassegnato come `ListenOnSecondary = true` siano aperte. L'apertura di listener aperti su servizi di tipo secondario è meno comune.
    - Hello se hello servizio è attualmente un servizio hello primario, `StatefulServiceBase.RunAsync()` metodo viene chiamato
4. Una volta tutti hello del listener replica `OpenAsync()` effettua le chiamate e `RunAsync()` viene chiamato, `StatefulServiceBase.OnChangeRoleAsync()` viene chiamato. Questo viene eseguito l'override uncommonly nel servizio hello.

Allo stesso modo toostateless services, non vi è alcun ordine hello in cui hello listener sono creati e aperto di coordinamento e quando viene chiamato RunAsync. Se è necessario il coordinamento, soluzioni hello sono molto hello stesso. Caso aggiuntive: ad esempio che le chiamate di hello in arrivo presso il listener di comunicazione hello richiedono informazioni contenute in alcune [raccolte affidabile](service-fabric-reliable-services-reliable-collections.md). Poiché è stato possibile aprire il listener di comunicazione hello prima raccolte affidabile hello sono leggibile o scrivibile e prima di RunAsync è stato possibile avviare, alcuni coordinamento aggiuntivo è necessario. soluzione più semplice e più comune di Hello è per hello comunicazione listener tooreturn un codice di errore che hello client utilizza tooknow tooretry hello richiesta.

## <a name="stateful-service-shutdown"></a>Arresto di un servizio con stato
Allo stesso modo tooStateless servizi, gli eventi del ciclo di vita di hello durante l'arresto vengono hello stesso durante l'avvio, ma invertita. Quando un servizio con stato verrà arrestato, hello si verificano eventi seguenti:

1. In parallelo
    - Gli eventuali listener aperti vengono chiusi. Viene richiamato `ICommunicationListener.CloseAsync()` su ogni listener.
    - token di annullamento Hello passato troppo`RunAsync()` viene annullata. Del controllo hello token di annullamento `IsCancellationRequested` proprietà restituisce true e se la chiamata del token hello `ThrowIfCancellationRequested` metodo genera un `OperationCanceledException`.
2. Una volta `CloseAsync()` completa per ogni listener e `RunAsync()` completa inoltre del servizio hello `StatefulServiceBase.OnChangeRoleAsync()` viene chiamato. (Questo uncommonly sottoposto a override in servizio hello.)
    - In attesa di RunAsync toocomplete è necessaria solo se questa replica del servizio è un database primario.
3. Una volta hello `StatefulServiceBase.OnChangeRoleAsync()` metodo viene completato, hello `StatefulServiceBase.OnCloseAsync()` metodo viene chiamato. Si tratta di un override insolito ma comunque disponibile.
3. Dopo aver `StatefulServiceBase.OnCloseAsync()` viene completato, viene eliminato l'oggetto servizio hello.

## <a name="stateful-service-primary-swaps"></a>Scambi primari di un servizio con stato
Durante l'esecuzione di un servizio con stato hello repliche primarie di che i servizi con stato può contenere solo i listener di comunicazione aperti e il relativo metodo RunAsync chiamato. Quelli secondari vengono costruiti ma non vedono ulteriori chiamate. Durante l'esecuzione un servizio con stato, tuttavia, è possibile modificare la replica è attualmente hello primario. Cosa significa in termini di eventi del ciclo di vita hello che può visualizzare una replica? Hello comportamento hello replica con stato vede varia a seconda che si tratti di replica hello viene abbassato di livello o innalzate di livello durante lo scambio di hello.

### <a name="for-hello-primary-being-demoted"></a>Per hello viene abbassato di livello principale
Service Fabric deve toostop questa replica l'elaborazione dei messaggi e chiudere eventuali operazioni in background che viene eseguito. Di conseguenza, questo passaggio ha un aspetto simile toowhen hello servizio viene arrestato. Una differenza è che hello servizio non viene eliminato o chiuso, in quanto rimane un database secondario. viene chiamato Hello API seguenti:

1. In parallelo
    - Gli eventuali listener aperti vengono chiusi. Viene richiamato `ICommunicationListener.CloseAsync()` su ogni listener.
    - token di annullamento Hello passato troppo`RunAsync()` viene annullata. Del controllo hello token di annullamento `IsCancellationRequested` proprietà restituisce true e se la chiamata del token hello `ThrowIfCancellationRequested` metodo genera un `OperationCanceledException`.
2. Una volta `CloseAsync()` completa per ogni listener e `RunAsync()` completa inoltre del servizio hello `StatefulServiceBase.OnChangeRoleAsync()` viene chiamato. Questo viene eseguito l'override uncommonly nel servizio hello.

### <a name="for-hello-secondary-being-promoted"></a>Per hello secondario innalzato di livello
Analogamente, Service Fabric deve toostart questa replica in attesa di messaggi in transito hello e avviare qualsiasi attività in background che interessano le. Di conseguenza, ha un aspetto questo processo viene creato simile toowhen hello servizio, ad eccezione di quella replica hello stesso esiste già. viene chiamato Hello API seguenti:

1. In parallelo
    - `StatefulServiceBase.CreateServiceReplicaListeners()` viene richiamato e qualsiasi listener restituito è aperto. Viene richiamato `ICommunicationListener.OpenAsync()` su ogni listener.
    - Hello del servizio `StatefulServiceBase.RunAsync()` viene chiamato
2. Una volta tutti hello del listener replica `OpenAsync()` effettua le chiamate e `RunAsync()` è stato chiamato, `StatefulServiceBase.OnChangeRoleAsync()` viene chiamato. Questo viene eseguito l'override uncommonly nel servizio hello.

### <a name="common-issues-during-stateful-service-shutdown-and-primary-demotion"></a>Problemi comuni durante l'arresto del servizio con stato e l'abbassamento di livello primario
Modifiche di Service Fabric hello primario di un servizio con stato per una serie di motivi. sono Hello più frequente [cluster ribilanciamento](service-fabric-cluster-resource-manager-balancing.md) e [l'aggiornamento dell'applicazione](service-fabric-application-upgrade.md). Durante queste operazioni (nonché durante la chiusura normale del servizio, come è possibile visualizzare se il servizio di hello è stato eliminato), è importante che hello riguardo di hello servizio `CancellationToken`. I servizi che non gestiscono correttamente l'annullamento sperimenteranno diversi problemi. In particolare, queste operazioni sarà lente poiché Service Fabric è in attesa di hello servizi toostop normalmente. Questo può infine toofailed aggiornamenti che scadono e rollback. Token di annullamento hello toohonor errore può essere causato anche sbilanciato cluster perché accedere a caldo nodi, ma non è possibile ribilanciati servizi hello poiché toomove troppo lungo li altrove. 

Poiché i servizi di hello con stati, è inoltre probabile che utilizzano hello [raccolte affidabile](service-fabric-reliable-services-reliable-collections.md). Nell'infrastruttura del servizio, quando viene modificato un database primario, una delle operazioni che si verificano hello è che sia stato revocato l'accesso in scrittura toohello sottostante stato. In tal modo tooa secondo set di problemi che possono influire sulla hello del ciclo di vita del servizio. gli insiemi di Hello eccezioni restituite basate sull'intervallo hello e se è stato spostato replica hello o arresta. Queste eccezioni devono essere gestite correttamente. Le eccezioni generate da Service Fabric rientrano nelle categorie permanente [(`FabricException`)](https://docs.microsoft.com/en-us/dotnet/api/system.fabric.fabricexception?view=azure-dotnet) e temporanea [(`FabricTransientException`)](https://docs.microsoft.com/en-us/dotnet/api/system.fabric.fabrictransientexception?view=azure-dotnet). Eccezioni permanenti devono registrate e verrà generata un'eccezione, mentre possono essere ripetute eccezioni temporanee hello in base a una logica di ripetizione.

La gestione delle eccezioni hello provengono dall'uso di hello `ReliableCollections` in combinazione con gli eventi del ciclo di vita del servizio è una parte importante di test e convalidando un servizio affidabile. Hello raccomandazione è toorun il servizio in condizioni di carico durante l'esecuzione di aggiornamenti e [chaos test](service-fabric-controlled-chaos.md) prima di distribuire mai tooproduction. Questi passaggi di base contribuiscono ad assicurare che il servizio sia implementato correttamente e gestisca gli eventi del ciclo di vita nel modo giusto.


## <a name="notes-on-service-lifecycle"></a>Note sul ciclo di vita del servizio
  - Entrambi hello `RunAsync()` metodo e hello `CreateServiceReplicaListeners/CreateServiceInstanceListeners` chiamate sono facoltative. Un servizio può averne una, entrambe o nessuna. Ad esempio, se il servizio di hello non tutto il relativo lavoro risposta toouser chiamate, non è necessario per tale tooimplement `RunAsync()`. Sono necessari solo i listener di comunicazione hello e il codice associato. Analogamente, la creazione e la restituzione di listener di comunicazione è facoltativo, come servizio di hello potrebbe avere solo sfondo toodo di lavoro e deve pertanto solo tooimplement`RunAsync()`
  - È valido per un servizio toocomplete `RunAsync()` correttamente e restituito da esso. Il completamento non è una condizione di errore. Completamento `RunAsync()` indica il completamento di operazioni in background hello del servizio hello. Per i servizi reliable con stati, `RunAsync()` viene chiamato nuovamente se replica hello sono stati abbassato di livello da tooSecondary primaria e quindi promossa tooPrimary indietro.
  - Se un servizio esce da `RunAsync()` generando un'eccezione imprevista, questo è un errore. oggetto servizio Hello è stato arrestato e segnalato un errore di integrità.
  - Sebbene non esista alcun limite di tempo restituito da questi metodi, immediatamente perdere hello possibilità toowrite tooReliable raccolte e pertanto non è possibile completare qualsiasi lavoro effettivo. È consigliabile che venga restituito al più presto dopo aver ricevuto la richiesta di annullamento hello. Se il servizio non risponde toothese API chiamate in una quantità ragionevole di tempo che Service Fabric potrebbe forzare la terminazione del servizio. In genere ciò accade solo durante gli aggiornamenti delle applicazioni o quando viene eliminato un servizio. Questo timeout è di 15 minuti per impostazione predefinita.
  - Errori di hello `OnCloseAsync()` comporterà percorso `OnAbort()` la chiamata che è un'opportunità di sforzo ultima possibilità per hello service tooclean backup e rilasciare le risorse che sono richiesti.

## <a name="next-steps"></a>Passaggi successivi
- [Introduzione tooReliable servizi](service-fabric-reliable-services-introduction.md)
- [Guida introduttiva a Reliable Services di Microsoft Azure Service Fabric](service-fabric-reliable-services-quick-start.md)
- [Uso avanzato del modello di programmazione Reliable Services](service-fabric-reliable-services-advanced-usage.md)
