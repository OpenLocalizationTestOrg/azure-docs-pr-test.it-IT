---
title: Aggregazione evento dei servizi dell'infrastruttura con EventFlow aaaAzure | Documenti Microsoft
description: Informazioni sull'aggregazione e la raccolta di eventi con EventFlow per il monitoraggio e la diagnostica dei cluster di Azure Service Fabric.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: c0141d3ed72d835139250af3589e298fd22d8f89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="event-aggregation-and-collection-using-eventflow"></a>Aggregazione e raccolta di eventi con EventFlow

[Microsoft Diagnostics EventFlow](https://github.com/Azure/diagnostics-eventflow) possibile instradare gli eventi da un nodo tooone o più destinazioni di monitoraggio. Poiché è incluso come pacchetto NuGet nel progetto di servizio, configurazione e il codice EventFlow viaggiano con servizio hello, eliminando problema di configurazione per ogni nodo hello indicato in precedenza su diagnostica Azure. EventFlow viene eseguito all'interno del processo di servizio e si connette direttamente output toohello configurato. A causa di connessione diretta hello, EventFlow funziona per le distribuzioni del servizio locale, il contenitore e Azure. Se si esegue EventFlow in scenari a densità elevata, ad esempio in un contenitore, è necessario prestare attenzione perché ogni pipeline di EventFlow stabilisce una connessione esterna. Pertanto, se si ospitano molti processi, si ottengono molte connessioni in uscita. Questo non è più un problema per le applicazioni di Service Fabric, perché tutte le repliche di un `ServiceType` eseguire stessa procedura adottata in hello e questo limita il numero di hello di connessioni in uscita. EventFlow offre il filtraggio degli eventi, in modo che solo gli eventi di hello che corrispondono al filtro specificato hello vengono inviati.

## <a name="setting-up-eventflow"></a>Configurazione di EventFlow

I file binari di EventFlow sono disponibili come set di pacchetti NuGet. tooadd progetto del servizio Service Fabric tooa EventFlow, fare clic sul progetto in Esplora soluzioni hello hello e scegliere "Gestisci NuGet pacchetti". Cambia la scheda "Sfoglia" toohello e cercare "`Diagnostics.EventFlow`":

![Pacchetti NuGet di EventFlow nell'interfaccia utente di gestione pacchetti NuGet di Visual Studio](./media/service-fabric-diagnostics-event-aggregation-eventflow/eventflow-nuget.png)

Verrà visualizzato un elenco dei vari pacchetti evidenziati, con etichetta "Input" e "Output". EventFlow supporta diversi provider di accesso e analizzatori. servizio Hello hosting EventFlow deve includere pacchetti appropriati a seconda di hello origine e di destinazione per i log applicazioni hello. Inoltre pacchetto ServiceFabric di toohello core, è necessario almeno un Input e Output configurato. Per esempio, è possibile aggiungere i seguenti pacchetti toosent EventSource eventi tooApplication Insights hello:

* `Microsoft.Diagnostics.EventFlow.Input.EventSource`dati toocapture dalla classe EventSource del servizio hello e da EventSources standard, ad esempio *ServiceFabric-Microsoft-Services* e *ServiceFabric-Microsoft-attori*)
* `Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights`(si stabilirà una risorsa di Azure Application Insights tooan di toosend hello log)
* `Microsoft.Diagnostics.EventFlow.ServiceFabric`(consente l'inizializzazione della pipeline EventFlow hello dalla configurazione del servizio Service Fabric e segnala eventuali problemi con l'invio di dati di diagnostica come report di integrità dell'infrastruttura di servizio)

>[!NOTE]
>`Microsoft.Diagnostics.EventFlow.Input.EventSource`il pacchetto richiede hello servizio progetto tootarget .NET Framework 4.6 o versione successiva. Assicurarsi di impostare il framework di destinazione appropriata hello nelle proprietà del progetto prima di installare questo pacchetto.

Dopo che tutti hello pacchetti installati, passaggio successivo hello è tooconfigure e abilitare EventFlow nel servizio hello.

## <a name="configuring-and-enabling-log-collection"></a>Configurazione e abilitazione della raccolta di log
pipeline EventFlow Hello responsabile per l'invio di log hello viene creata da una specifica archiviata in un file di configurazione. Hello `Microsoft.Diagnostics.EventFlow.ServiceFabric` pacchetto viene installato un file di configurazione inizio di EventFlow in `PackageRoot\Config` cartella della soluzione, denominato `eventFlowConfig.json`. Questo file di configurazione deve toobe modificato toocapture dati dal servizio predefinito hello `EventSource` classe e input desiderate tooconfigure e inviare una posizione appropriata toohello di dati.

Di seguito è riportato un esempio *eventFlowConfig.json* in base a pacchetti NuGet hello indicati in precedenza:
```json
{
  "inputs": [
    {
      "type": "EventSource",
      "sources": [
        { "providerName": "Microsoft-ServiceFabric-Services" },
        { "providerName": "Microsoft-ServiceFabric-Actors" },
        // (replace hello following value with your service's ServiceEventSource name)
        { "providerName": "your-service-EventSource-name" }
      ]
    }
  ],
  "filters": [
    {
      "type": "drop",
      "include": "Level == Verbose"
    }
  ],
  "outputs": [
    {
      "type": "ApplicationInsights",
      // (replace hello following value with your AI resource's instrumentation key)
      "instrumentationKey": "00000000-0000-0000-0000-000000000000"
    }
  ],
  "schemaVersion": "2016-08-11"
}
```

Hello ServiceEventSource del servizio è denominato valore hello hello proprietà Name di hello `EventSourceAttribute` toohello ServiceEventSource classe applicato. Tutto è specificato in hello `ServiceEventSource.cs` file, che fa parte del codice del servizio hello. Ad esempio, in hello seguente frammento di codice hello nome del codice hello ServiceEventSource è *MyCompany-Application1-Stateless1*:

```csharp
[EventSource(Name = "MyCompany-Application1-Stateless1")]
internal sealed class ServiceEventSource : EventSource
{
    // (rest of ServiceEventSource implementation)
}
```

Si noti che il file `eventFlowConfig.json` fa parte del pacchetto di configurazione del servizio. File toothis modifiche può essere inclusi in full o configurazione-solo gli aggiornamenti del servizio di hello, soggetto tooService aggiornamento controlli di integrità e il rollback automatico nel caso di errore di aggiornamento. Per altre informazioni, vedere [Aggiornamento delle applicazioni di Service Fabric](service-fabric-application-upgrade.md).

Hello *filtri* sezione di configurazione hello consente toofurther personalizzare le informazioni hello toogo corso tramite hello EventFlow pipeline toohello output, consentendo toodrop includono determinate informazioni o modificare hello struttura di dati dell'evento hello. Per altre informazioni sui filtri, controllare i [filtri EventFlow](https://github.com/Azure/diagnostics-eventflow#filters).

passaggio finale Hello è tooinstantiate EventFlow pipeline nel codice di avvio del servizio, si trova `Program.cs` file:

```csharp
using System;
using System.Diagnostics;
using System.Threading;
using Microsoft.ServiceFabric;
using Microsoft.ServiceFabric.Services.Runtime;

// **** EventFlow namespace
using Microsoft.Diagnostics.EventFlow.ServiceFabric;

namespace Stateless1
{
    internal static class Program
    {
        /// <summary>
        /// This is hello entry point of hello service host process.
        /// </summary>
        private static void Main()
        {
            try
            {
                // **** Instantiate log collection via EventFlow
                using (var diagnosticsPipeline = ServiceFabricDiagnosticPipelineFactory.CreatePipeline("MyApplication-MyService-DiagnosticsPipeline"))
                {

                    ServiceRuntime.RegisterServiceAsync("Stateless1Type",
                    context => new Stateless1(context)).GetAwaiter().GetResult();

                    ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(Stateless1).Name);

                    Thread.Sleep(Timeout.Infinite);
                }
            }
            catch (Exception e)
            {
                ServiceEventSource.Current.ServiceHostInitializationFailed(e.ToString());
                throw;
            }
        }
    }
}
```

il nome di Hello passato come parametro hello di hello `CreatePipeline` metodo hello `ServiceFabricDiagnosticsPipelineFactory` nome hello di hello *entità integrità* che rappresenta di pipeline di raccolta log EventFlow hello. Questo nome viene utilizzato se viene rilevato EventFlow e di errore e la segnala tramite hello del sottosistema di integrità di Service Fabric.

### <a name="using-service-fabric-settings-and-application-parameters-tooin-eventflowconfig"></a>Utilizzando le impostazioni dell'infrastruttura di servizio e applicazione parametri tooin eventFlowConfig

EventFlow supporta le impostazioni dell'infrastruttura di servizio e le impostazioni dell'applicazione validi tooconfigure EventFlow. È possibile fare riferimento a parametri per impostazioni di infrastruttura tooService utilizzando questa sintassi speciale per i valori:

```json
servicefabric:/<section-name>/<setting-name>
``` 

`<section-name>`è il nome di hello della sezione di configurazione di Service Fabric, hello e `<setting-name>` è l'impostazione di configurazione hello fornire valore hello che verrà utilizzato tooconfigure un'impostazione EventFlow. altre informazioni su come tooread toodo scopo, passare troppo[il supporto per le impostazioni dell'infrastruttura di servizio e i parametri dell'applicazione](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters).

## <a name="verification"></a>Verifica

Avviare il servizio e osservare hello Debug la finestra di output in Visual Studio. Una volta avviato il servizio di hello, è consigliabile iniziare a visualizzare la prova che il servizio invia Registra output toohello configurato. Passare una piattaforma di analisi e la visualizzazione di eventi tooyour e verificare che i registri siano stati avviati tooshow up (potrebbe richiedere alcuni minuti).

## <a name="next-steps"></a>Passaggi successivi

* [Event Analysis and Visualization with Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) (Analisi e visualizzazione degli eventi con Application Insights)
* [Event Analysis and Visualization with OMS](service-fabric-diagnostics-event-analysis-oms.md) (Analisi e visualizzazione degli eventi con OMS)
* [Documentazione di EventFlow](https://github.com/Azure/diagnostics-eventflow)