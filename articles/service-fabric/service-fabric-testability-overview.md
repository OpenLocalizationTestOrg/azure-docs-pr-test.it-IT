---
title: Panoramica di Analysis Services aaaFault | Documenti Microsoft
description: Questo articolo descrive hello errore Analysis Services nell'infrastruttura del servizio per la generazione di errori e in esecuzione gli scenari di test per i servizi.
services: service-fabric
documentationcenter: .net
author: anmolah
manager: timlt
editor: vturecek
ms.assetid: 1f064276-293a-4989-a513-e0d0b9fdf703
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/15/2017
ms.author: anmola
ms.openlocfilehash: deac16ec830aa10d4e488e60691faa9ef2b6cd33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-fault-analysis-service"></a>Introduzione toohello errore Analysis Services
Hello errore Analysis Services è progettato per il test di servizi che si basano su Microsoft Azure Service Fabric. Con hello errore Analysis Services è possibile provocare errori significativi ed eseguire gli scenari dei test completa rispetto alle applicazioni. Questi errori e gli scenari di esercizio e convalidare hello numerosi Stati e transizioni che un servizio si verifica in tutta la durata, in modo controllato, sicuro e coerenza.

Le azioni sono errori di singoli hello come destinazione di un servizio per il testing. Uno sviluppatore del servizio è possibile utilizzare queste informazioni come blocchi predefiniti toowrite complicato scenari. ad esempio:

* Riavviare toosimulate un nodo qualsiasi numero di situazioni in cui viene riavviato un computer o macchina virtuale.
* Spostare una replica del servizio con stato toosimulate il bilanciamento del carico, il failover o aggiornamento dell'applicazione.
* Richiamare perdita del quorum in un toocreate di servizio con stato una situazione in cui le operazioni di scrittura non possono continuare perché non vi sono dati abbastanza nuovi tooaccept repliche "backup" o "secondario".
* Richiamare la perdita di dati in un toocreate di servizio con stato una situazione in cui tutti gli stati in memoria sono completamente cancellati out.

Gli scenari sono operazioni complesse costituite da una o più azioni. Hello errore Analysis Services sono disponibili due scenari completi predefiniti:

* Scenario di caos
* Scenario di failover

## <a name="testing-as-a-service"></a>Test come servizio
Hello errore Analysis Services è un servizio di sistema di Service Fabric che viene avviato automaticamente con un cluster di Service Fabric. Questo servizio funge da host hello per attacco intrusivo nel codice di errore, esecuzione di uno scenario di test e analisi di integrità. 

![Servizio di analisi degli errori][0]

Quando viene avviato uno scenario di test o di azione di errore, viene inviato un comando toohello errore Analysis Service toorun hello azione o un test di scenario di errore. Hello errore Analysis Services è stato in modo che può eseguire scenari e gli errori e convalidare i risultati in modo affidabile. Ad esempio, uno scenario di test con esecuzione prolungata può essere eseguito in modo affidabile dal hello errore Analysis Services. Poiché i test vengono eseguiti all'interno di cluster hello, servizio hello possibile ed esaminare lo stato di hello di cluster hello e tooprovide i servizi informazioni più dettagliate sugli errori.

## <a name="testing-distributed-systems"></a>Test dei sistemi distribuiti
Service Fabric rende il processo di hello di scrittura e la gestione di applicazioni scalabili distribuite molto più semplice. Hello errore Analysis Services esegue test di un'applicazione distribuita allo stesso modo più semplice. Esistono tre problemi principali che devono toobe risolto durante il test:

1. Simulazione/la generazione di errori che potrebbero verificarsi in scenari reali: uno degli aspetti importanti di hello di Service Fabric è che consente applicazioni distribuite toorecover a diversi errori. Tuttavia, tootest che hello applicazione è in grado di toorecover da questi errori, è necessario un toosimulate/generare meccanismo questi errori reali in un ambiente controllato.
2. Hello possibilità toogenerate correlati a errori: gli errori di base nel sistema di hello, ad esempio errori di rete e gli errori di computer, sono facilmente tooproduce singolarmente. Generazione di un numero significativo di scenari che possono verificarsi nel mondo reale di hello in seguito a interazioni hello di questi singoli errori è considerevole.
3. L'esperienza unificata tra vari livelli di sviluppo e distribuzione: esistono molti sistemi di fault injection che consentono di generare diversi tipi di errori. Tuttavia, esperienza hello in tutti questi elementi è scarsa quando lo spostamento da scenari di sviluppo di una casella, hello toorunning stesso test in ambienti di test di grandi dimensioni, toousing per test nell'ambiente di produzione.

Sebbene ci siano molti meccanismi toosolve questi problemi, un sistema con le garanzie necessarie - tutte le modalità di hello da un ambiente di sviluppo di una casella hello stesso tootest in cluster di produzione, è mancante. Hello errore Analysis Services consente agli sviluppatori di applicazioni hello concentrarsi sul test la logica di business. Hello errore Analysis Services fornisce che tutte le funzionalità di hello necessaria l'interazione di hello tootest del servizio hello con sistemi distribuiti di hello sottostante.

### <a name="simulatinggenerating-real-world-failure-scenarios"></a>Simulazione e generazione di scenari di errore reali
affidabilità di hello tootest di un sistema distribuito in caso di errori, è necessario un errori toogenerate meccanismo. In teoria, la generazione di un errore come un nodo verso il basso sembri semplice, che viene avviato raggiungendo hello stesso set di problemi di coerenza che Service Fabric sta tentando di toosolve. Ad esempio, se lo si desidera tooshut verso il basso un nodo, hello richiesta flusso di lavoro è la seguente hello:

1. Dal client hello, eseguire una richiesta di arresto del nodo.
2. Nodo di hello richiesta toohello corretto di trasmissione.
   
    a. Se non viene trovato il nodo di hello, deve avere esito negativo.
   
    b. Se viene trovato il nodo di hello, deve restituire solo se il nodo hello è stato arrestato.

Errore di hello tooverify da una prospettiva di test, test hello deve tooknow che quando è provocato l'errore, errore hello si verifica effettivamente. garanzia di Hello che fornisce Service Fabric è che uno dei nodi hello entra verso il basso o raggiungimento del nodo hello comando hello era già verso il basso. In entrambi caso hello test deve essere in grado di toocorrectly motivo sullo stato di hello ed esito positivo o eseguire correttamente la convalida. Un sistema implementato all'esterno di hello toodo Service Fabric stesso insieme di errori di stato hello hit che molti di rete, hardware e problemi software, che ne impedirebbero fornisce garanzie precedente. In presenza di hello di problemi di hello analizzati prima Service Fabric riconfigurare hello cluster stato toowork risoluzione dei problemi hello e pertanto hello errore Analysis Services verrà comunque in grado di toogive hello destro impostato di garanzie.

### <a name="generating-required-events-and-scenarios"></a>Generazione degli eventi e degli scenari richiesti
Mentre la simulazione di un errore del mondo reale in modo coerente è difficile toostart con, hello possibilità toogenerate correlato errori è anche più difficile. Ad esempio, in un servizio con stato persistente si verifica una perdita di dati quando si verifica hello seguenti operazioni:

1. Solo un quorum di scrittura delle repliche hello sono aggiornato sulla replica. Tutte le repliche secondarie hello un ritardo hello primario.
2. il quorum di scrittura Hello si arresta a causa di repliche hello risulti non disponibile (scadenza tooa pacchetto di codice o nodo risulti non disponibile).
3. il quorum di scrittura Hello non è possibile tornare perché i dati hello per le repliche hello vengono persi (scadenza toodisk danneggiamento o ricreando le immagini macchina).

Questi errori correlati vengono eseguiti nel mondo reale hello ma meno frequentemente come singoli errori. Hello possibilità tootest per questi scenari prima che si verificano nell'ambiente di produzione è fondamentale. Ancora più importante è hello possibilità toosimulate questi scenari con carichi di lavoro di produzione in condizioni controllate (hello mezzogiorno hello con tutti i tecnici del piano). Che è preferibile rispetto avendolo verificarsi per hello prima volta in produzione alle 2:00.

### <a name="unified-experience-across-different-environments"></a>Esperienza unificata tra ambienti diversi
procedure consigliate di Hello tradizionalmente toocreate tre set diversi di esperienze, uno per l'ambiente di sviluppo hello, uno per i test e uno per la produzione. modello di Hello era:

1. Nell'ambiente di sviluppo hello, produrre le transizioni di stato che consentono di unit test di singoli metodi.
2. Nell'ambiente di test hello, generare test end-to-end di tooallow errori che esercitano vari scenari di errore.
3. Mantenere tooprevent nuovo ambiente di produzione hello eventuali errori non naturale e tooensure che vi sia toofailure estremamente veloce risposta risorse umane.

Nell'infrastruttura del servizio, tramite hello errore Analysis Services, ci stiamo proposta tooturn giro e utilizzare hello stessa metodologia tooproduction ambiente di sviluppo. Esistono due modi tooachieve questo:

1. errori tooinduce controllato, utilizzare hello API servizio analisi di errore da un ambiente di una casella tooproduction modo di hello tutti i cluster.
2. hello toogive cluster un classica che causa induzione automatica degli errori, utilizzare hello errore Analysis Service toogenerate errori automatico. Frequenza di hello controllo di errori tramite la configurazione di consente hello stesso servizio toobe testato in modo diverso in ambienti diversi.

Con Service Fabric, anche se sarebbe diversa in ambienti diversi hello, scala hello di errori di meccanismi effettivi di hello saranno identici. In questo modo per molto più veloce codice di installazione, pipeline e hello possibilità tootest hello services carichi reali.

## <a name="using-hello-fault-analysis-service"></a>Utilizzo di hello errore Analysis Services
**C#**

Le funzionalità di Analysis Services di errore sono hello System.Fabric dello spazio dei nomi nel pacchetto Microsoft.ServiceFabric NuGet hello. le funzionalità del servizio di analisi di errore toouse hello, includere pacchetto nuget hello come riferimento nel progetto.

**PowerShell**

toouse PowerShell, è necessario installare hello Service Fabric SDK. Dopo aver installato SDK, hello hello ServiceFabric di PowerShell modulo viene automaticamente caricato per si toouse.

## <a name="next-steps"></a>Passaggi successivi
toocreate realmente a livello di cloud services, è critico tooensure, prima e dopo la distribuzione, che i servizi in grado di resistere errori reali. In servizi HelloWorld oggi, hello possibilità tooinnovate rapidamente e spostarsi rapidamente codice tooproduction è molto importante. Hello errore Analysis Services consente di servizio gli sviluppatori toodo precisamente che.

Iniziare a testare le applicazioni e servizi utilizzando hello incorporata [testare scenari](service-fabric-testability-scenarios.md), o creare i propri scenari di test utilizzando hello [azioni di errore](service-fabric-testability-actions.md) fornito da hello errore Analysis Services.

<!--Image references-->
[0]: ./media/service-fabric-testability-overview/faultanalysisservice.png
