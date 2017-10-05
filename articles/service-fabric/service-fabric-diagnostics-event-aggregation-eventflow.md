---
title: Aggregazione di eventi di Azure Service Fabric con EventFlow | Microsoft Docs
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
ms.openlocfilehash: 90d26a77b749e70de3a7d910f15820653e2ef39b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="event-aggregation-and-collection-using-eventflow"></a><span data-ttu-id="21ac0-103">Aggregazione e raccolta di eventi con EventFlow</span><span class="sxs-lookup"><span data-stu-id="21ac0-103">Event aggregation and collection using EventFlow</span></span>

<span data-ttu-id="21ac0-104">[Microsoft Diagnostics EventFlow](https://github.com/Azure/diagnostics-eventflow) può indirizzare gli eventi da un nodo a una o più destinazioni di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="21ac0-104">[Microsoft Diagnostics EventFlow](https://github.com/Azure/diagnostics-eventflow) can route events from a node to one or more monitoring destinations.</span></span> <span data-ttu-id="21ac0-105">Poiché è incluso come pacchetto NuGet nel progetto del servizio, il codice e la configurazione di EventFlow vanno di pari passo con il servizio, eliminando i problemi di configurazione specifici di ogni nodo indicati in precedenza e relativi a Diagnostica di Azure.</span><span class="sxs-lookup"><span data-stu-id="21ac0-105">Because it is included as a NuGet package in your service project, EventFlow code and configuration travel with the service, eliminating the per-node configuration issue mentioned earlier about Azure Diagnostics.</span></span> <span data-ttu-id="21ac0-106">EventFlow viene eseguito nel processo del servizio e si connette direttamente agli output configurati.</span><span class="sxs-lookup"><span data-stu-id="21ac0-106">EventFlow runs within your service process, and connects directly to the configured outputs.</span></span> <span data-ttu-id="21ac0-107">A causa della connessione diretta, EventFlow funziona con le distribuzioni dei servizi in Azure, nei contenitori e in locale.</span><span class="sxs-lookup"><span data-stu-id="21ac0-107">Because of the direct connection, EventFlow works for Azure, container, and on-premises service deployments.</span></span> <span data-ttu-id="21ac0-108">Se si esegue EventFlow in scenari a densità elevata, ad esempio in un contenitore, è necessario prestare attenzione perché ogni pipeline di EventFlow stabilisce una connessione esterna.</span><span class="sxs-lookup"><span data-stu-id="21ac0-108">Be careful if you run EventFlow in high-density scenarios, such as in a container, because each EventFlow pipeline makes an external connection.</span></span> <span data-ttu-id="21ac0-109">Pertanto, se si ospitano molti processi, si ottengono molte connessioni in uscita.</span><span class="sxs-lookup"><span data-stu-id="21ac0-109">So, if you host several processes, you get several outbound connections!</span></span> <span data-ttu-id="21ac0-110">Questo non costituisce un problema per le applicazioni di Service Fabric, perché tutte le repliche di `ServiceType` sono eseguite nello stesso processo e ciò limita il numero di connessioni in uscita.</span><span class="sxs-lookup"><span data-stu-id="21ac0-110">This isn't as much a concern for Service Fabric applications, because all replicas of a `ServiceType` run in the same process, and this limits the number of outbound connections.</span></span> <span data-ttu-id="21ac0-111">EventFlow offre anche i filtri per gli eventi, in modo che vengano inviati solo gli eventi corrispondenti al filtro specificato.</span><span class="sxs-lookup"><span data-stu-id="21ac0-111">EventFlow also offers event filtering, so that only the events that match the specified filter are sent.</span></span>

## <a name="setting-up-eventflow"></a><span data-ttu-id="21ac0-112">Configurazione di EventFlow</span><span class="sxs-lookup"><span data-stu-id="21ac0-112">Setting up EventFlow</span></span>

<span data-ttu-id="21ac0-113">I file binari di EventFlow sono disponibili come set di pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="21ac0-113">EventFlow binaries are available as a set of NuGet packages.</span></span> <span data-ttu-id="21ac0-114">Per aggiungere EventFlow a un progetto di servizio di Service Fabric, fare clic sul progetto in Esplora soluzioni e scegliere "Gestisci pacchetti NuGet".</span><span class="sxs-lookup"><span data-stu-id="21ac0-114">To add EventFlow to a Service Fabric service project, right-click the project in the Solution Explorer and choose "Manage NuGet packages."</span></span> <span data-ttu-id="21ac0-115">Passare alla scheda "Sfoglia" e cercare "`Diagnostics.EventFlow`":</span><span class="sxs-lookup"><span data-stu-id="21ac0-115">Switch to the "Browse" tab and search for "`Diagnostics.EventFlow`":</span></span>

![Pacchetti NuGet di EventFlow nell'interfaccia utente di gestione pacchetti NuGet di Visual Studio](./media/service-fabric-diagnostics-event-aggregation-eventflow/eventflow-nuget.png)

<span data-ttu-id="21ac0-117">Verrà visualizzato un elenco dei vari pacchetti evidenziati, con etichetta "Input" e "Output".</span><span class="sxs-lookup"><span data-stu-id="21ac0-117">You will see a list of various packages show up, labeled with "Inputs" and "Outputs".</span></span> <span data-ttu-id="21ac0-118">EventFlow supporta diversi provider di accesso e analizzatori.</span><span class="sxs-lookup"><span data-stu-id="21ac0-118">EventFlow supports various different logging providers and analyzers.</span></span> <span data-ttu-id="21ac0-119">Il servizio che ospita EventFlow deve includere pacchetti appropriati a seconda dell'origine e della destinazione dei log applicazioni.</span><span class="sxs-lookup"><span data-stu-id="21ac0-119">The service hosting EventFlow should include appropriate packages depending on the source and destination for the application logs.</span></span> <span data-ttu-id="21ac0-120">Oltre al pacchetto di base ServiceFabric, è anche necessario aver configurato almeno un Input e un Output.</span><span class="sxs-lookup"><span data-stu-id="21ac0-120">In addition to the core ServiceFabric package, you also need at least one Input and Output configured.</span></span> <span data-ttu-id="21ac0-121">Ad esempio, è possibile aggiungere i pacchetti seguenti agli eventi EventSource inviati ad Application Insights:</span><span class="sxs-lookup"><span data-stu-id="21ac0-121">For exmaple, you can add the following packages to sent EventSource events to Application Insights:</span></span>

* <span data-ttu-id="21ac0-122">`Microsoft.Diagnostics.EventFlow.Input.EventSource` per acquisire dati dalla classe EventSource del servizio e da oggetti EventSource standard, ad esempio *Microsoft-ServiceFabric-Services* e *Microsoft-ServiceFabric-Actors*</span><span class="sxs-lookup"><span data-stu-id="21ac0-122">`Microsoft.Diagnostics.EventFlow.Input.EventSource` to capture data from the service's EventSource class, and from standard EventSources such as *Microsoft-ServiceFabric-Services* and *Microsoft-ServiceFabric-Actors*)</span></span>
* <span data-ttu-id="21ac0-123">`Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights`, i log verranno inviati a una risorsa di Azure Application Insights</span><span class="sxs-lookup"><span data-stu-id="21ac0-123">`Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights` (we are going to send the logs to an Azure Application Insights resource)</span></span>
* <span data-ttu-id="21ac0-124">`Microsoft.Diagnostics.EventFlow.ServiceFabric`, consente l'inizializzazione della pipeline EventFlow dalla configurazione del servizio di Service Fabric e segnala eventuali problemi tramite l'invio di dati di diagnostica in forma di report sull'integrità di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="21ac0-124">`Microsoft.Diagnostics.EventFlow.ServiceFabric`(enables initialization of the EventFlow pipeline from Service Fabric service configuration and reports any problems with sending diagnostic data as Service Fabric health reports)</span></span>

>[!NOTE]
><span data-ttu-id="21ac0-125">Per il pacchetto `Microsoft.Diagnostics.EventFlow.Input.EventSource` il progetto di servizio deve puntare a .NET Framework 4.6 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="21ac0-125">`Microsoft.Diagnostics.EventFlow.Input.EventSource` package requires the service project to target .NET Framework 4.6 or newer.</span></span> <span data-ttu-id="21ac0-126">Assicurarsi di impostare il framework di destinazione corretto nelle proprietà del progetto prima di installare questo pacchetto.</span><span class="sxs-lookup"><span data-stu-id="21ac0-126">Make sure you set the appropriate target framework in project properties before installing this package.</span></span>

<span data-ttu-id="21ac0-127">Dopo aver installato tutti i pacchetti, è necessario configurare e abilitare EventFlow nel servizio.</span><span class="sxs-lookup"><span data-stu-id="21ac0-127">After all the packages are installed, the next step is to configure and enable EventFlow in the service.</span></span>

## <a name="configuring-and-enabling-log-collection"></a><span data-ttu-id="21ac0-128">Configurazione e abilitazione della raccolta di log</span><span class="sxs-lookup"><span data-stu-id="21ac0-128">Configuring and enabling log collection</span></span>
<span data-ttu-id="21ac0-129">La pipeline EventFlow, responsabile dell'invio dei log, viene creata da una specifica archiviata in un file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="21ac0-129">The EventFlow pipeline responsible for sending the logs is created from a specification stored in a configuration file.</span></span> <span data-ttu-id="21ac0-130">Il pacchetto `Microsoft.Diagnostics.EventFlow.ServiceFabric` installa un file di configurazione EventFlow iniziale nella cartella `PackageRoot\Config` della soluzione denominata `eventFlowConfig.json`.</span><span class="sxs-lookup"><span data-stu-id="21ac0-130">The `Microsoft.Diagnostics.EventFlow.ServiceFabric` package installs a starting EventFlow configuration file under `PackageRoot\Config` solution folder, named `eventFlowConfig.json`.</span></span> <span data-ttu-id="21ac0-131">Questo file di configurazione deve essere modificato per l'acquisizione di dati dalla classe `EventSource` del servizio predefinito, oltre a qualsiasi altro input che si desidera configurare, e per l'invio di dati alla destinazione appropriata.</span><span class="sxs-lookup"><span data-stu-id="21ac0-131">This configuration file needs to be modified to capture data from the default service `EventSource` class, and any other inputs you want to configure, and send data to the appropriate place.</span></span>

<span data-ttu-id="21ac0-132">Ecco un esempio di *eventFlowConfig.json* basato sui pacchetti NuGet indicati in precedenza:</span><span class="sxs-lookup"><span data-stu-id="21ac0-132">Here is a sample *eventFlowConfig.json* based on the NuGet packages mentioned above:</span></span>
```json
{
  "inputs": [
    {
      "type": "EventSource",
      "sources": [
        { "providerName": "Microsoft-ServiceFabric-Services" },
        { "providerName": "Microsoft-ServiceFabric-Actors" },
        // (replace the following value with your service's ServiceEventSource name)
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
      // (replace the following value with your AI resource's instrumentation key)
      "instrumentationKey": "00000000-0000-0000-0000-000000000000"
    }
  ],
  "schemaVersion": "2016-08-11"
}
```

<span data-ttu-id="21ac0-133">Il nome dell'oggetto ServiceEventSource del servizio è il valore della proprietà Name dell'oggetto `EventSourceAttribute` applicato alla classe ServiceEventSource.</span><span class="sxs-lookup"><span data-stu-id="21ac0-133">The name of service's ServiceEventSource is the value of the Name property of the `EventSourceAttribute` applied to the ServiceEventSource class.</span></span> <span data-ttu-id="21ac0-134">Tutto questo è specificato nel file `ServiceEventSource.cs`, che fa parte del codice del servizio.</span><span class="sxs-lookup"><span data-stu-id="21ac0-134">It is all specified in the `ServiceEventSource.cs` file, which is part of the service code.</span></span> <span data-ttu-id="21ac0-135">Ad esempio, nel frammento di codice seguente il nome dell'oggetto ServiceEventSource è *MyCompany-Application1-Stateless1*:</span><span class="sxs-lookup"><span data-stu-id="21ac0-135">For example, in the following code snippet the name of the ServiceEventSource is *MyCompany-Application1-Stateless1*:</span></span>

```csharp
[EventSource(Name = "MyCompany-Application1-Stateless1")]
internal sealed class ServiceEventSource : EventSource
{
    // (rest of ServiceEventSource implementation)
}
```

<span data-ttu-id="21ac0-136">Si noti che il file `eventFlowConfig.json` fa parte del pacchetto di configurazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="21ac0-136">Note that `eventFlowConfig.json` file is part of service configuration package.</span></span> <span data-ttu-id="21ac0-137">Le modifiche apportate a questo file possono essere incluse in aggiornamenti del servizio completi o della sola configurazione, in base ai controlli di integrità dell'aggiornamento di Service Fabric e al ripristino dello stato precedente automatico in caso di errore di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="21ac0-137">Changes to this file can be included in full- or configuration-only upgrades of the service, subject to Service Fabric upgrade health checks and automatic rollback if there is upgrade failure.</span></span> <span data-ttu-id="21ac0-138">Per altre informazioni, vedere [Aggiornamento delle applicazioni di Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="21ac0-138">For more information, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="21ac0-139">La sezione dei *filtri* della configurazione consente di personalizzare ulteriormente le informazioni che si intende far passare attraverso la pipeline EventFlow fino agli output, consentendo di eliminare o includere determinate informazioni o di modificare la struttura dei dati dell'evento.</span><span class="sxs-lookup"><span data-stu-id="21ac0-139">The *filters* section of the config allows you to further customize the information that is going to go through the EventFlow pipeline to the outputs, allowing you to drop or include certain information, or change the structure of the event data.</span></span> <span data-ttu-id="21ac0-140">Per altre informazioni sui filtri, controllare i [filtri EventFlow](https://github.com/Azure/diagnostics-eventflow#filters).</span><span class="sxs-lookup"><span data-stu-id="21ac0-140">For more information on filtering, see [EventFlow filters](https://github.com/Azure/diagnostics-eventflow#filters).</span></span>

<span data-ttu-id="21ac0-141">Il passaggio finale consiste nel creare un'istanza della pipeline EventFlow nel codice di avvio del servizio, situato nel file `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="21ac0-141">The final step is to instantiate EventFlow pipeline in your service's startup code, located in `Program.cs` file:</span></span>

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
        /// This is the entry point of the service host process.
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

<span data-ttu-id="21ac0-142">Il nome passato come parametro del metodo `CreatePipeline` di `ServiceFabricDiagnosticsPipelineFactory` è il nome dell'*entità di integrità* che rappresenta la pipeline di raccolta di log EventFlow.</span><span class="sxs-lookup"><span data-stu-id="21ac0-142">The name passed as the parameter of the `CreatePipeline` method of the `ServiceFabricDiagnosticsPipelineFactory` is the name of the *health entity* representing the EventFlow log collection pipeline.</span></span> <span data-ttu-id="21ac0-143">Questo nome viene usato se EventFlow rileva un errore e lo segnala tramite il sottosistema di integrità di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="21ac0-143">This name is used if EventFlow encounters and error and reports it through the Service Fabric health subsystem.</span></span>

### <a name="using-service-fabric-settings-and-application-parameters-to-in-eventflowconfig"></a><span data-ttu-id="21ac0-144">Uso delle impostazioni di infrastruttura di Service Fabric e dei parametri dell'applicazione in eventFlowConfig</span><span class="sxs-lookup"><span data-stu-id="21ac0-144">Using Service Fabric settings and application parameters to in eventFlowConfig</span></span>

<span data-ttu-id="21ac0-145">EventFlow supporta l'uso delle impostazioni di Service Fabric e dei parametri dell'applicazione per configurare le impostazioni di EventFlow.</span><span class="sxs-lookup"><span data-stu-id="21ac0-145">EventFlow supports using Service Fabric settings and application paremeters to configure EventFlow settings.</span></span> <span data-ttu-id="21ac0-146">È possibile fare riferimento ai parametri delle impostazioni di Service Fabric usando questa sintassi speciale per i valori:</span><span class="sxs-lookup"><span data-stu-id="21ac0-146">You can refer to Service Fabric settings parameters using this special syntax for values:</span></span>

```json
servicefabric:/<section-name>/<setting-name>
``` 

<span data-ttu-id="21ac0-147">`<section-name>` è il nome della sezione di configurazione di Service Fabric e `<setting-name>` è l'impostazione di configurazione che indica il valore che verrà usato per configurare un'impostazione EventFlow.</span><span class="sxs-lookup"><span data-stu-id="21ac0-147">`<section-name>` is the name of the Service Fabric configuration section, and `<setting-name>` is the configuration setting providing the value that will be used to configure an EventFlow setting.</span></span> <span data-ttu-id="21ac0-148">Per altre informazioni su come effettuare questa operazione, passare a [Support for Service Fabric settings and application parameters](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters) (Supporto per le impostazioni e i parametri dell'applicazione Service Fabric).</span><span class="sxs-lookup"><span data-stu-id="21ac0-148">To read more about how to do this, go to [Support for Service Fabric settings and application parameters](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters).</span></span>

## <a name="verification"></a><span data-ttu-id="21ac0-149">Verifica</span><span class="sxs-lookup"><span data-stu-id="21ac0-149">Verification</span></span>

<span data-ttu-id="21ac0-150">Avviare il servizio e osservare la finestra dell'output di debug di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="21ac0-150">Start your service and observe the Debug output window in Visual Studio.</span></span> <span data-ttu-id="21ac0-151">Dopo l'avvio del servizio, dovrebbero essere visibili le prove dell'invio di record del servizio all'output configurato.</span><span class="sxs-lookup"><span data-stu-id="21ac0-151">After the service is started, you should start seeing evidence that your service is sending records to the output that you have configured.</span></span> <span data-ttu-id="21ac0-152">Passare alla piattaforma di analisi e visualizzazione di eventi e confermare che i registri vengono visualizzati. Questa operazione potrebbe richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="21ac0-152">Navigate to your event analysis and visualization platform and confirm that logs have started to show up (could take a few minutes).</span></span>

## <a name="next-steps"></a><span data-ttu-id="21ac0-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="21ac0-153">Next steps</span></span>

* <span data-ttu-id="21ac0-154">[Event Analysis and Visualization with Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) (Analisi e visualizzazione degli eventi con Application Insights)</span><span class="sxs-lookup"><span data-stu-id="21ac0-154">[Event Analysis and Visualization with Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md)</span></span>
* <span data-ttu-id="21ac0-155">[Event Analysis and Visualization with OMS](service-fabric-diagnostics-event-analysis-oms.md) (Analisi e visualizzazione degli eventi con OMS)</span><span class="sxs-lookup"><span data-stu-id="21ac0-155">[Event Analysis and Visualization with OMS](service-fabric-diagnostics-event-analysis-oms.md)</span></span>
* [<span data-ttu-id="21ac0-156">Documentazione di EventFlow</span><span class="sxs-lookup"><span data-stu-id="21ac0-156">EventFlow documentation</span></span>](https://github.com/Azure/diagnostics-eventflow)