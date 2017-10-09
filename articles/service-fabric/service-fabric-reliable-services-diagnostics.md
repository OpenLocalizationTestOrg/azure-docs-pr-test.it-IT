---
title: diagnostica servizi affidabili aaaStateful | Documenti Microsoft
description: "Funzionalità di diagnostica per i servizi Reliable con stato"
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: ae0e8f99-69ab-4d45-896d-1fa80ed45659
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 6200800b858957c06039d9af062633b12a446318
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostic-functionality-for-stateful-reliable-services"></a>Funzionalità di diagnostica per i servizi Reliable con stato
Genera classe StatefulServiceBase servizi Reliable con stato Hello [EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) eventi che possono essere utilizzati toodebug hello servizio, che forniscono informazioni dettagliate in modalità runtime hello è operativo e la risoluzione dei problemi.

## <a name="eventsource-events"></a>Eventi EventSource
nome EventSource Hello hello classe StatefulServiceBase servizi Reliable con stato è "Microsoft-ServiceFabric-Services". Gli eventi dall'origine di eventi vengono visualizzati nel [gli eventi di diagnostica](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md#view-service-fabric-system-events-in-visual-studio) finestra quando è in corso servizio hello [il debug in Visual Studio](service-fabric-debugging-your-application.md).

Alcuni esempi di strumenti e tecnologie che consentono di raccogliere e/o visualizzare eventi EventSource sono [PerfView](http://www.microsoft.com/download/details.aspx?id=28567), [Diagnostica di Microsoft Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) e [Microsoft TraceEvent Library](http://www.nuget.org/packages/Microsoft.Diagnostics.Tracing.TraceEvent).

## <a name="events"></a>Events
| Nome evento | ID evento | Level | Descrizione evento |
| --- | --- | --- | --- |
| StatefulRunAsyncInvocation |1 |Informazioni |Emesso quando viene avviata l'attività RunAsync del servizio |
| StatefulRunAsyncCancellation |2 |Informazioni |Emesso quando viene annullata l'attività RunAsync del servizio |
| StatefulRunAsyncCompletion |3 |Informazioni |Emesso quando l'attività RunAsync del servizio è completata |
| StatefulRunAsyncSlowCancellation |4 |Avviso |Generato quando l'attività di RunAsync servizio accetta di annullamento toocomplete troppo lungo |
| StatefulRunAsyncFailure |5 |Errore |Emesso quando l'attività RunAsync del servizio genera un'eccezione |

## <a name="interpret-events"></a>Interpretazione degli eventi
Gli eventi di StatefulRunAsyncInvocation StatefulRunAsyncCompletion e StatefulRunAsyncCancellation sono utili toohello servizio writer toounderstand hello ciclo di vita di un servizio, nonché tempistica hello per quando un servizio viene avviato, annullato o completato . Può essere utile durante il debug di problemi del servizio o ciclo di vita del servizio hello comprensione.

Gli autori del servizio necessario prestare particolare attenzione tooStatefulRunAsyncSlowCancellation e gli eventi StatefulRunAsyncFailure perché indicano problemi con il servizio di hello.

StatefulRunAsyncFailure viene generato ogni volta che hello servizio RunAsync() attività genera un'eccezione. In genere, un'eccezione generata indica un errore o un bug nel servizio hello. Inoltre, hello eccezione provoca la toofail servizio hello, pertanto è spostato tooa altro nodo. Può trattarsi di un'operazione dispendiosa e può ritardare le richieste in ingresso, mentre questa viene spostata servizio hello. Gli autori del servizio devono determinare hello causa dell'eccezione hello e, se possibile, limitare il problema.

StatefulRunAsyncSlowCancellation viene generato ogni volta che una richiesta di annullamento per attività di RunAsync hello richiede più di 4 secondi. Quando un servizio richiede l'annullamento toocomplete troppo lungo, impatto il possibilità hello per hello servizio toobe riavviato rapidamente in un altro nodo. Questo può influire sulla disponibilità complessiva del servizio hello hello.

## <a name="next-steps"></a>Passaggi successivi
* [Provider di EventSource in PerfView](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/)
