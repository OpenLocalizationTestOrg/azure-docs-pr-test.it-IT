---
title: aaaTroubleshooting con event Tracing for | Documenti Microsoft
description: problemi di Hello comuni riscontrati durante la distribuzione di servizi in Microsoft Azure Service Fabric.
services: service-fabric
documentationcenter: .net
author: mattrowmsft
manager: timlt
editor: 
ms.assetid: 5eb8ef21-da04-4ac8-8b9a-5f7ff1e0a180
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/31/2016
ms.author: mattrow
redirect_url: /azure/service-fabric/service-fabric-diagnostics-overview
ms.openlocfilehash: f5adb7e15fa1e2c964bbbc5726246630c95e13f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-common-issues-when-you-deploy-services-on-azure-service-fabric"></a>Risolvere i problemi comuni quando si distribuiscono servizi in Azure Service Fabric
Quando si esegue i servizi nel computer di sviluppo, è facile toouse [strumenti di debug di Visual Studio](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md). Per i cluster remoti, [rapporti di stato](service-fabric-view-entities-aggregated-health.md) sono sempre toostart un buon punto. Hello più semplice tooaccess modi questi report sono tramite PowerShell o [SFX](service-fabric-visualizing-your-cluster.md). Questo articolo si presuppone che si sta eseguendo il debug di un cluster remoto e avere una conoscenza di base di toouse uno di questi strumenti.

## <a name="application-crash"></a>Arresto anomalo dell’applicazione
Hello "partizione è inferiore al numero di istanze o di replica di destinazione" report è molto probabile che il servizio è arrestato in modo anomalo. toofind out in un arresto anomalo del servizio richiede qualche ulteriore analisi. Quando si esegue su vasta scala, sarà necessario un set di tracce ben studiate.  È consigliabile provare [diagnostica Azure](service-fabric-diagnostics-how-to-setup-wad.md) per raccogliere le tracce e l'utilizzo di una soluzione, ad esempio [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) per la visualizzazione e la ricerca delle tracce hello.

![Integrità della partizione SFX](./media/service-fabric-diagnostics-troubleshoot-common-scenarios/crashNewApp.png)

### <a name="during-service-or-actor-initialization"></a>Durante l'inizializzazione dell’attore o del servizio
Tutte le eccezioni prima dell'inizializzazione tipo di servizio hello causerà toocrash processo hello. Per questi tipi di arresti anomali del sistema, log eventi dell'applicazione hello visualizzerà l'errore hello dal servizio.
Si tratta di toosee eccezioni più comuni di hello prima hello servizio viene inizializzato.

***System.IO.FileNotFoundException***

Questo errore è spesso dovuto toomissing le dipendenze dell'assembly. Controllare la proprietà CopyLocal hello in Visual Studio o hello global assembly cache per il nodo hello.

***COMException*** *in System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory (IntPtr, IFabricStatefulServiceFactory)*

 Questo indica che il nome del tipo servizio registrato hello non corrisponde a manifesto del servizio hello.

[Diagnostica di Azure](service-fabric-diagnostics-how-to-setup-wad.md) possono il registro eventi dell'applicazione hello tooupload configurato per tutti i nodi.

### <a name="runasync-or-onactivateasync"></a>RunAsync() or OnActivateAsync()
In caso di arresto anomalo di hello durante l'inizializzazione di hello o l'esecuzione del tipo di servizio registrato o attore, hello eccezione verrà rilevata da Azure Service Fabric. È possibile visualizzare questi dai provider di EventSource hello descritta in dettaglio nella sezione "Passaggi successivi" hello.

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni sulla diagnostica esistente fornita dall'infrastruttura di servizi:

* [Diagnostica di Reliable actors](service-fabric-reliable-actors-diagnostics.md)
* [Diagnostica di Reliable Services](service-fabric-reliable-services-diagnostics.md)

