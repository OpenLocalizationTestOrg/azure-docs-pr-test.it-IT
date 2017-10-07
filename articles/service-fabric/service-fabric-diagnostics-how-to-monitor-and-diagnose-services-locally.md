---
title: aaaDebug microservizi Azure Windows | Documenti Microsoft
description: Informazioni su come toomonitor e diagnosticare i servizi scritti con Microsoft Azure Service Fabric in un computer di sviluppo locale.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: edcc0631-ed2d-45a3-851d-2c4fa0f4a326
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/24/2017
ms.author: dekapur
ms.openlocfilehash: 24868aa194b8a28fa3e6de95c1de5506d912a544
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-diagnose-services-in-a-local-machine-development-setup"></a>Monitorare e diagnosticare servizi in una configurazione di sviluppo con computer locale
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
> * [Linux](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
> 
> 

Il monitoraggio, il rilevamento, la diagnosi e risoluzione dei problemi consentono di servizi toocontinue l'esperienza utente toohello un'interruzione minima. Anche se il monitoraggio e diagnostica è critica in un ambiente di produzione distribuito effettivo, l'efficienza di hello varia in base all'adozione di un modello simile durante lo sviluppo di servizi tooensure che funzionano quando si sposta il programma di installazione di tooa del mondo reale. Service Fabric rende più semplice per la diagnostica tooimplement agli sviluppatori di servizio che può funzionare senza problemi tra le impostazioni di sviluppo locale solo computer e le installazioni cluster di produzione reali.

## <a name="event-tracing-for-windows"></a>Event Tracing for Windows
[Traccia eventi per Windows](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx) (ETW) è hello consigliato di tecnologia per i messaggi di traccia nell'infrastruttura del servizio. Alcuni dei vantaggi di ETW sono i seguenti:

* **ETW è veloce.** È stata sviluppata come tecnologia di tracciamento con un impatto minimo sui tempi di esecuzione del codice.
* **ETW funziona perfettamente non solo in ambienti di sviluppo locali, ma anche in configurazioni cluster reali.** Ciò significa che non è l'analisi del codice quando si è pronti toodeploy toorewrite cluster tooa codice reali.
* **Anche il codice di sistema di Service Fabric usa ETW per il tracciamento interno.** In questo modo tooview interleaved le tracce dell'applicazione con le tracce di sistema di Service Fabric. È inoltre utile è toomore comprensione delle sequenze di hello e interrelazioni tra il codice dell'applicazione e gli eventi di sistema sottostante di hello.
* **È il supporto incorporato di Service Fabric Visual Studio tools eventi ETW tooview.** Eventi ETW vengono visualizzati nella vista di eventi di diagnostica di Visual Studio hello dopo Visual Studio sia configurata correttamente con Service Fabric. 

## <a name="view-service-fabric-system-events-in-visual-studio"></a>Visualizzare gli eventi di sistema di Service Fabric in Visual Studio
Service Fabric genera gli eventi ETW, gli sviluppatori di applicazioni toohelp comprendano ciò che avviene nella piattaforma hello. Se non già stato fatto, vado avanti e seguire i passaggi di hello in [creazione di un'applicazione in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md). Tali informazioni consentiranno diventare un'applicazione in esecuzione con hello Visualizzatore di eventi di diagnostica che mostra hello i messaggi di traccia.

1. Se la diagnostica hello finestra degli eventi non viene visualizzata automaticamente, toohello **vista** scheda in Visual Studio, scegliere **altre finestre** e quindi **Visualizzatore eventi di diagnostica**.
2. Informazioni sui metadati standard che indicano l'evento di hello nodo, l'applicazione e servizio hello proviene da ogni evento. È inoltre possibile filtrare l'elenco di hello di eventi tramite hello **filtrare gli eventi** casella nella parte superiore di hello della finestra eventi hello. Ad esempio, è possibile filtrare in base al **nome del nodo** o al **nome del servizio**. E quando si osservano i dettagli degli eventi, è anche possibile sospendere utilizzando hello **sospendere** pulsante nella parte superiore di hello della finestra eventi hello e di riprendere successivamente senza alcuna perdita di eventi.
   
   ![Visualizzatore eventi di diagnostica di Visual Studio](./media/service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally/DiagEventsExamples2.png)

## <a name="add-your-own-custom-traces-toohello-application-code"></a>Aggiungere il codice di applicazione toohello le tracce personalizzate
modelli di progetto di Visual Studio di Service Fabric Hello contengono codice di esempio. codice Hello Mostra il codice dell'applicazione personalizzata tooadd ETW tracce che mostrano backup nel Visualizzatore di Visual Studio ETW hello insieme alle tracce di sistema di Service Fabric. Hello vantaggio di questo metodo è che vengono automaticamente aggiunti tootraces metadati e hello Visualizzatore eventi di diagnostica di Visual Studio è già configurato toodisplay li.

Per i progetti creati da hello **i modelli di servizio** (con o senza informazioni stateful) solo cercare hello `RunAsync` implementazione:

1. Hello chiamata troppo`ServiceEventSource.Current.ServiceMessage` in hello `RunAsync` metodo mostra un esempio di una traccia ETW personalizzata dal codice dell'applicazione hello.
2. In hello **ServiceEventSource.cs** file, si noterà un overload per hello `ServiceEventSource.ServiceMessage` metodo che deve essere utilizzato per gli eventi ad alta frequenza a causa di motivi tooperformance.

Per i progetti creati da hello **modelli attore** (con stato o senza informazioni):

1. Aprire hello **. cs "ProjectName"** dove *ProjectName* hello nome scelto per il progetto di Visual Studio.  
2. Trovare codice hello `ActorEventSource.Current.ActorMessage(this, "Doing Work");` in hello *DoWorkAsync* metodo.  Questo è un esempio di una traccia ETW personalizzata scritta dal codice dell'applicazione.  
3. Nel file **ActorEventSource.cs**, si noterà un overload per hello `ActorEventSource.ActorMessage` metodo che deve essere utilizzato per gli eventi ad alta frequenza a causa di motivi tooperformance.

Dopo l'aggiunta di ETW personalizzato traccia tooyour codice del servizio, è possibile compilare, distribuire ed eseguire un'applicazione hello toosee nuovamente l'evento nel Visualizzatore eventi di diagnostica hello. Se si esegue il debug di un'applicazione hello con **F5**, hello Visualizzatore eventi di diagnostica verrà aperto automaticamente.

## <a name="next-steps"></a>Passaggi successivi
Hello stesso codice di traccia che è stato aggiunto tooyour applicazione sopra per la diagnostica locale funzionerà con gli strumenti che è possibile utilizzare tooview questi eventi quando si esegue l'applicazione in un cluster di Azure. Consultare questi articoli illustrano hello opzioni diverse per gli strumenti di hello e una descrivono di come è possibile impostare.

* [Modalità di registrazione toocollect con diagnostica di Azure](service-fabric-diagnostics-how-to-setup-wad.md)
* [Aggregazione e raccolta di eventi con EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md)

