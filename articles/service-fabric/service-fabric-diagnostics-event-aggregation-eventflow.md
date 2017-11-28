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
# <a name="event-aggregation-and-collection-using-eventflow"></a><span data-ttu-id="fba8d-103">Aggregazione e raccolta di eventi con EventFlow</span><span class="sxs-lookup"><span data-stu-id="fba8d-103">Event aggregation and collection using EventFlow</span></span>

<span data-ttu-id="fba8d-104">[Microsoft Diagnostics EventFlow](https://github.com/Azure/diagnostics-eventflow) possibile instradare gli eventi da un nodo tooone o più destinazioni di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="fba8d-104">[Microsoft Diagnostics EventFlow](https://github.com/Azure/diagnostics-eventflow) can route events from a node tooone or more monitoring destinations.</span></span> <span data-ttu-id="fba8d-105">Poiché è incluso come pacchetto NuGet nel progetto di servizio, configurazione e il codice EventFlow viaggiano con servizio hello, eliminando problema di configurazione per ogni nodo hello indicato in precedenza su diagnostica Azure.</span><span class="sxs-lookup"><span data-stu-id="fba8d-105">Because it is included as a NuGet package in your service project, EventFlow code and configuration travel with hello service, eliminating hello per-node configuration issue mentioned earlier about Azure Diagnostics.</span></span> <span data-ttu-id="fba8d-106">EventFlow viene eseguito all'interno del processo di servizio e si connette direttamente output toohello configurato.</span><span class="sxs-lookup"><span data-stu-id="fba8d-106">EventFlow runs within your service process, and connects directly toohello configured outputs.</span></span> <span data-ttu-id="fba8d-107">A causa di connessione diretta hello, EventFlow funziona per le distribuzioni del servizio locale, il contenitore e Azure.</span><span class="sxs-lookup"><span data-stu-id="fba8d-107">Because of hello direct connection, EventFlow works for Azure, container, and on-premises service deployments.</span></span> <span data-ttu-id="fba8d-108">Se si esegue EventFlow in scenari a densità elevata, ad esempio in un contenitore, è necessario prestare attenzione perché ogni pipeline di EventFlow stabilisce una connessione esterna.</span><span class="sxs-lookup"><span data-stu-id="fba8d-108">Be careful if you run EventFlow in high-density scenarios, such as in a container, because each EventFlow pipeline makes an external connection.</span></span> <span data-ttu-id="fba8d-109">Pertanto, se si ospitano molti processi, si ottengono molte connessioni in uscita.</span><span class="sxs-lookup"><span data-stu-id="fba8d-109">So, if you host several processes, you get several outbound connections!</span></span> <span data-ttu-id="fba8d-110">Questo non è più un problema per le applicazioni di Service Fabric, perché tutte le repliche di un `ServiceType` eseguire stessa procedura adottata in hello e questo limita il numero di hello di connessioni in uscita.</span><span class="sxs-lookup"><span data-stu-id="fba8d-110">This isn't as much a concern for Service Fabric applications, because all replicas of a `ServiceType` run in hello same process, and this limits hello number of outbound connections.</span></span> <span data-ttu-id="fba8d-111">EventFlow offre il filtraggio degli eventi, in modo che solo gli eventi di hello che corrispondono al filtro specificato hello vengono inviati.</span><span class="sxs-lookup"><span data-stu-id="fba8d-111">EventFlow also offers event filtering, so that only hello events that match hello specified filter are sent.</span></span>

## <a name="setting-up-eventflow"></a><span data-ttu-id="fba8d-112">Configurazione di EventFlow</span><span class="sxs-lookup"><span data-stu-id="fba8d-112">Setting up EventFlow</span></span>

<span data-ttu-id="fba8d-113">I file binari di EventFlow sono disponibili come set di pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="fba8d-113">EventFlow binaries are available as a set of NuGet packages.</span></span> <span data-ttu-id="fba8d-114">tooadd progetto del servizio Service Fabric tooa EventFlow, fare clic sul progetto in Esplora soluzioni hello hello e scegliere "Gestisci NuGet pacchetti".</span><span class="sxs-lookup"><span data-stu-id="fba8d-114">tooadd EventFlow tooa Service Fabric service project, right-click hello project in hello Solution Explorer and choose "Manage NuGet packages."</span></span> <span data-ttu-id="fba8d-115">Cambia la scheda "Sfoglia" toohello e cercare "`Diagnostics.EventFlow`":</span><span class="sxs-lookup"><span data-stu-id="fba8d-115">Switch toohello "Browse" tab and search for "`Diagnostics.EventFlow`":</span></span>

![Pacchetti NuGet di EventFlow nell'interfaccia utente di gestione pacchetti NuGet di Visual Studio](./media/service-fabric-diagnostics-event-aggregation-eventflow/eventflow-nuget.png)

<span data-ttu-id="fba8d-117">Verrà visualizzato un elenco dei vari pacchetti evidenziati, con etichetta "Input" e "Output".</span><span class="sxs-lookup"><span data-stu-id="fba8d-117">You will see a list of various packages show up, labeled with "Inputs" and "Outputs".</span></span> <span data-ttu-id="fba8d-118">EventFlow supporta diversi provider di accesso e analizzatori.</span><span class="sxs-lookup"><span data-stu-id="fba8d-118">EventFlow supports various different logging providers and analyzers.</span></span> <span data-ttu-id="fba8d-119">servizio Hello hosting EventFlow deve includere pacchetti appropriati a seconda di hello origine e di destinazione per i log applicazioni hello.</span><span class="sxs-lookup"><span data-stu-id="fba8d-119">hello service hosting EventFlow should include appropriate packages depending on hello source and destination for hello application logs.</span></span> <span data-ttu-id="fba8d-120">Inoltre pacchetto ServiceFabric di toohello core, è necessario almeno un Input e Output configurato.</span><span class="sxs-lookup"><span data-stu-id="fba8d-120">In addition toohello core ServiceFabric package, you also need at least one Input and Output configured.</span></span> <span data-ttu-id="fba8d-121">Per esempio, è possibile aggiungere i seguenti pacchetti toosent EventSource eventi tooApplication Insights hello:</span><span class="sxs-lookup"><span data-stu-id="fba8d-121">For exmaple, you can add hello following packages toosent EventSource events tooApplication Insights:</span></span>

* <span data-ttu-id="fba8d-122">`Microsoft.Diagnostics.EventFlow.Input.EventSource`dati toocapture dalla classe EventSource del servizio hello e da EventSources standard, ad esempio *ServiceFabric-Microsoft-Services* e *ServiceFabric-Microsoft-attori*)</span><span class="sxs-lookup"><span data-stu-id="fba8d-122">`Microsoft.Diagnostics.EventFlow.Input.EventSource` toocapture data from hello service's EventSource class, and from standard EventSources such as *Microsoft-ServiceFabric-Services* and *Microsoft-ServiceFabric-Actors*)</span></span>
* <span data-ttu-id="fba8d-123">`Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights`(si stabilirà una risorsa di Azure Application Insights tooan di toosend hello log)</span><span class="sxs-lookup"><span data-stu-id="fba8d-123">`Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights` (we are going toosend hello logs tooan Azure Application Insights resource)</span></span>
* <span data-ttu-id="fba8d-124">`Microsoft.Diagnostics.EventFlow.ServiceFabric`(consente l'inizializzazione della pipeline EventFlow hello dalla configurazione del servizio Service Fabric e segnala eventuali problemi con l'invio di dati di diagnostica come report di integrità dell'infrastruttura di servizio)</span><span class="sxs-lookup"><span data-stu-id="fba8d-124">`Microsoft.Diagnostics.EventFlow.ServiceFabric`(enables initialization of hello EventFlow pipeline from Service Fabric service configuration and reports any problems with sending diagnostic data as Service Fabric health reports)</span></span>

>[!NOTE]
><span data-ttu-id="fba8d-125">`Microsoft.Diagnostics.EventFlow.Input.EventSource`il pacchetto richiede hello servizio progetto tootarget .NET Framework 4.6 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="fba8d-125">`Microsoft.Diagnostics.EventFlow.Input.EventSource` package requires hello service project tootarget .NET Framework 4.6 or newer.</span></span> <span data-ttu-id="fba8d-126">Assicurarsi di impostare il framework di destinazione appropriata hello nelle proprietà del progetto prima di installare questo pacchetto.</span><span class="sxs-lookup"><span data-stu-id="fba8d-126">Make sure you set hello appropriate target framework in project properties before installing this package.</span></span>

<span data-ttu-id="fba8d-127">Dopo che tutti hello pacchetti installati, passaggio successivo hello è tooconfigure e abilitare EventFlow nel servizio hello.</span><span class="sxs-lookup"><span data-stu-id="fba8d-127">After all hello packages are installed, hello next step is tooconfigure and enable EventFlow in hello service.</span></span>

## <a name="configuring-and-enabling-log-collection"></a><span data-ttu-id="fba8d-128">Configurazione e abilitazione della raccolta di log</span><span class="sxs-lookup"><span data-stu-id="fba8d-128">Configuring and enabling log collection</span></span>
<span data-ttu-id="fba8d-129">pipeline EventFlow Hello responsabile per l'invio di log hello viene creata da una specifica archiviata in un file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="fba8d-129">hello EventFlow pipeline responsible for sending hello logs is created from a specification stored in a configuration file.</span></span> <span data-ttu-id="fba8d-130">Hello `Microsoft.Diagnostics.EventFlow.ServiceFabric` pacchetto viene installato un file di configurazione inizio di EventFlow in `PackageRoot\Config` cartella della soluzione, denominato `eventFlowConfig.json`.</span><span class="sxs-lookup"><span data-stu-id="fba8d-130">hello `Microsoft.Diagnostics.EventFlow.ServiceFabric` package installs a starting EventFlow configuration file under `PackageRoot\Config` solution folder, named `eventFlowConfig.json`.</span></span> <span data-ttu-id="fba8d-131">Questo file di configurazione deve toobe modificato toocapture dati dal servizio predefinito hello `EventSource` classe e input desiderate tooconfigure e inviare una posizione appropriata toohello di dati.</span><span class="sxs-lookup"><span data-stu-id="fba8d-131">This configuration file needs toobe modified toocapture data from hello default service `EventSource` class, and any other inputs you want tooconfigure, and send data toohello appropriate place.</span></span>

<span data-ttu-id="fba8d-132">Di seguito è riportato un esempio *eventFlowConfig.json* in base a pacchetti NuGet hello indicati in precedenza:</span><span class="sxs-lookup"><span data-stu-id="fba8d-132">Here is a sample *eventFlowConfig.json* based on hello NuGet packages mentioned above:</span></span>
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

<span data-ttu-id="fba8d-133">Hello ServiceEventSource del servizio è denominato valore hello hello proprietà Name di hello `EventSourceAttribute` toohello ServiceEventSource classe applicato.</span><span class="sxs-lookup"><span data-stu-id="fba8d-133">hello name of service's ServiceEventSource is hello value of hello Name property of hello `EventSourceAttribute` applied toohello ServiceEventSource class.</span></span> <span data-ttu-id="fba8d-134">Tutto è specificato in hello `ServiceEventSource.cs` file, che fa parte del codice del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="fba8d-134">It is all specified in hello `ServiceEventSource.cs` file, which is part of hello service code.</span></span> <span data-ttu-id="fba8d-135">Ad esempio, in hello seguente frammento di codice hello nome del codice hello ServiceEventSource è *MyCompany-Application1-Stateless1*:</span><span class="sxs-lookup"><span data-stu-id="fba8d-135">For example, in hello following code snippet hello name of hello ServiceEventSource is *MyCompany-Application1-Stateless1*:</span></span>

```csharp
[EventSource(Name = "MyCompany-Application1-Stateless1")]
internal sealed class ServiceEventSource : EventSource
{
    // (rest of ServiceEventSource implementation)
}
```

<span data-ttu-id="fba8d-136">Si noti che il file `eventFlowConfig.json` fa parte del pacchetto di configurazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="fba8d-136">Note that `eventFlowConfig.json` file is part of service configuration package.</span></span> <span data-ttu-id="fba8d-137">File toothis modifiche può essere inclusi in full o configurazione-solo gli aggiornamenti del servizio di hello, soggetto tooService aggiornamento controlli di integrità e il rollback automatico nel caso di errore di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="fba8d-137">Changes toothis file can be included in full- or configuration-only upgrades of hello service, subject tooService Fabric upgrade health checks and automatic rollback if there is upgrade failure.</span></span> <span data-ttu-id="fba8d-138">Per altre informazioni, vedere [Aggiornamento delle applicazioni di Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="fba8d-138">For more information, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="fba8d-139">Hello *filtri* sezione di configurazione hello consente toofurther personalizzare le informazioni hello toogo corso tramite hello EventFlow pipeline toohello output, consentendo toodrop includono determinate informazioni o modificare hello struttura di dati dell'evento hello.</span><span class="sxs-lookup"><span data-stu-id="fba8d-139">hello *filters* section of hello config allows you toofurther customize hello information that is going toogo through hello EventFlow pipeline toohello outputs, allowing you toodrop or include certain information, or change hello structure of hello event data.</span></span> <span data-ttu-id="fba8d-140">Per altre informazioni sui filtri, controllare i [filtri EventFlow](https://github.com/Azure/diagnostics-eventflow#filters).</span><span class="sxs-lookup"><span data-stu-id="fba8d-140">For more information on filtering, see [EventFlow filters](https://github.com/Azure/diagnostics-eventflow#filters).</span></span>

<span data-ttu-id="fba8d-141">passaggio finale Hello è tooinstantiate EventFlow pipeline nel codice di avvio del servizio, si trova `Program.cs` file:</span><span class="sxs-lookup"><span data-stu-id="fba8d-141">hello final step is tooinstantiate EventFlow pipeline in your service's startup code, located in `Program.cs` file:</span></span>

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

<span data-ttu-id="fba8d-142">il nome di Hello passato come parametro hello di hello `CreatePipeline` metodo hello `ServiceFabricDiagnosticsPipelineFactory` nome hello di hello *entità integrità* che rappresenta di pipeline di raccolta log EventFlow hello.</span><span class="sxs-lookup"><span data-stu-id="fba8d-142">hello name passed as hello parameter of hello `CreatePipeline` method of hello `ServiceFabricDiagnosticsPipelineFactory` is hello name of hello *health entity* representing hello EventFlow log collection pipeline.</span></span> <span data-ttu-id="fba8d-143">Questo nome viene utilizzato se viene rilevato EventFlow e di errore e la segnala tramite hello del sottosistema di integrità di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="fba8d-143">This name is used if EventFlow encounters and error and reports it through hello Service Fabric health subsystem.</span></span>

### <a name="using-service-fabric-settings-and-application-parameters-tooin-eventflowconfig"></a><span data-ttu-id="fba8d-144">Utilizzando le impostazioni dell'infrastruttura di servizio e applicazione parametri tooin eventFlowConfig</span><span class="sxs-lookup"><span data-stu-id="fba8d-144">Using Service Fabric settings and application parameters tooin eventFlowConfig</span></span>

<span data-ttu-id="fba8d-145">EventFlow supporta le impostazioni dell'infrastruttura di servizio e le impostazioni dell'applicazione validi tooconfigure EventFlow.</span><span class="sxs-lookup"><span data-stu-id="fba8d-145">EventFlow supports using Service Fabric settings and application paremeters tooconfigure EventFlow settings.</span></span> <span data-ttu-id="fba8d-146">È possibile fare riferimento a parametri per impostazioni di infrastruttura tooService utilizzando questa sintassi speciale per i valori:</span><span class="sxs-lookup"><span data-stu-id="fba8d-146">You can refer tooService Fabric settings parameters using this special syntax for values:</span></span>

```json
servicefabric:/<section-name>/<setting-name>
``` 

<span data-ttu-id="fba8d-147">`<section-name>`è il nome di hello della sezione di configurazione di Service Fabric, hello e `<setting-name>` è l'impostazione di configurazione hello fornire valore hello che verrà utilizzato tooconfigure un'impostazione EventFlow.</span><span class="sxs-lookup"><span data-stu-id="fba8d-147">`<section-name>` is hello name of hello Service Fabric configuration section, and `<setting-name>` is hello configuration setting providing hello value that will be used tooconfigure an EventFlow setting.</span></span> <span data-ttu-id="fba8d-148">altre informazioni su come tooread toodo scopo, passare troppo[il supporto per le impostazioni dell'infrastruttura di servizio e i parametri dell'applicazione](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters).</span><span class="sxs-lookup"><span data-stu-id="fba8d-148">tooread more about how toodo this, go too[Support for Service Fabric settings and application parameters](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters).</span></span>

## <a name="verification"></a><span data-ttu-id="fba8d-149">Verifica</span><span class="sxs-lookup"><span data-stu-id="fba8d-149">Verification</span></span>

<span data-ttu-id="fba8d-150">Avviare il servizio e osservare hello Debug la finestra di output in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fba8d-150">Start your service and observe hello Debug output window in Visual Studio.</span></span> <span data-ttu-id="fba8d-151">Una volta avviato il servizio di hello, è consigliabile iniziare a visualizzare la prova che il servizio invia Registra output toohello configurato.</span><span class="sxs-lookup"><span data-stu-id="fba8d-151">After hello service is started, you should start seeing evidence that your service is sending records toohello output that you have configured.</span></span> <span data-ttu-id="fba8d-152">Passare una piattaforma di analisi e la visualizzazione di eventi tooyour e verificare che i registri siano stati avviati tooshow up (potrebbe richiedere alcuni minuti).</span><span class="sxs-lookup"><span data-stu-id="fba8d-152">Navigate tooyour event analysis and visualization platform and confirm that logs have started tooshow up (could take a few minutes).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fba8d-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fba8d-153">Next steps</span></span>

* <span data-ttu-id="fba8d-154">[Event Analysis and Visualization with Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) (Analisi e visualizzazione degli eventi con Application Insights)</span><span class="sxs-lookup"><span data-stu-id="fba8d-154">[Event Analysis and Visualization with Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md)</span></span>
* <span data-ttu-id="fba8d-155">[Event Analysis and Visualization with OMS](service-fabric-diagnostics-event-analysis-oms.md) (Analisi e visualizzazione degli eventi con OMS)</span><span class="sxs-lookup"><span data-stu-id="fba8d-155">[Event Analysis and Visualization with OMS](service-fabric-diagnostics-event-analysis-oms.md)</span></span>
* [<span data-ttu-id="fba8d-156">Documentazione di EventFlow</span><span class="sxs-lookup"><span data-stu-id="fba8d-156">EventFlow documentation</span></span>](https://github.com/Azure/diagnostics-eventflow)