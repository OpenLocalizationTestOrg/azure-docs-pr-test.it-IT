---
title: Raccogliere log direttamente da un processo del servizio di Azure Service Fabric | Microsoft Azure
description: Questo articolo illustra come usare le applicazioni di Service Fabric per inviare log direttamente a una posizione centralizzata, come Azure Application Insights o Elasticsearch, senza basarsi sull'agente di Diagnostica di Azure.
services: service-fabric
documentationcenter: .net
author: karolz-ms
manager: rwike77
editor: 
ms.assetid: ab92c99b-1edd-4677-8c28-4e591d909b47
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/18/2017
ms.author: karolz
redirect_url: /azure/service-fabric/service-fabric-diagnostics-event-aggregation-eventflow
ms.openlocfilehash: b7d2541928f4248750417a77d99033c8b4354dcc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="collect-logs-directly-from-an-azure-service-fabric-service-process"></a><span data-ttu-id="2f4c0-103">Raccogliere log direttamente da un processo del servizio di Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2f4c0-103">Collect logs directly from an Azure Service Fabric service process</span></span>
## <a name="in-process-log-collection"></a><span data-ttu-id="2f4c0-104">Raccolta di log nel processo</span><span class="sxs-lookup"><span data-stu-id="2f4c0-104">In-process log collection</span></span>
<span data-ttu-id="2f4c0-105">Nei servizi di **Azure Service Fabric** è possibile raccogliere log applicazioni tramite l'[estensione Diagnostica di Azure](service-fabric-diagnostics-how-to-setup-wad.md) se il set di origini e destinazioni di log è di piccole dimensioni e non cambia spesso e se il mapping tra le origini e le relative destinazioni è semplice.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-105">Collecting application logs using [Azure Diagnostics extension](service-fabric-diagnostics-how-to-setup-wad.md) is a good option for **Azure Service Fabric** services if the set of log sources and destinations is small, does not change often, and there is a straightforward mapping between the sources and their destinations.</span></span> <span data-ttu-id="2f4c0-106">In caso contrario, è possibile consentire ai servizi di inviare i log direttamente a una posizione centralizzata.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-106">If not, an alternative is to have services send their logs directly to a central location.</span></span> <span data-ttu-id="2f4c0-107">Questo processo è noto come **raccolta di log nel processo** e presenta diversi vantaggi potenziali:</span><span class="sxs-lookup"><span data-stu-id="2f4c0-107">This process is known as **in-process log collection** and has several potential advantages:</span></span>

* <span data-ttu-id="2f4c0-108">*Facilità di configurazione e distribuzione*</span><span class="sxs-lookup"><span data-stu-id="2f4c0-108">*Easy configuration and deployment*</span></span>

    * <span data-ttu-id="2f4c0-109">La configurazione della raccolta dei dati di diagnostica è solo una parte della configurazione del servizio</span><span class="sxs-lookup"><span data-stu-id="2f4c0-109">The configuration of diagnostic data collection is just part of the service configuration.</span></span> <span data-ttu-id="2f4c0-110">ed è facile mantenerla sempre "sincronizzata" con il resto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-110">It is easy to always keep it "in sync" with the rest of the application.</span></span>
    * <span data-ttu-id="2f4c0-111">È facile ottenere la configurazione per ogni applicazione o servizio.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-111">Per-application or per-service configuration is easily achievable.</span></span>
        * <span data-ttu-id="2f4c0-112">La raccolta di log basata su agenti richiede in genere una distribuzione e configurazione separate dell'agente di diagnostica, che costituisce un'attività amministrativa aggiuntiva e una potenziale fonte di errori.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-112">Agent-based log collection usually requires a separate deployment and configuration of the diagnostic agent, which is an extra administrative task and a potential source of errors.</span></span> <span data-ttu-id="2f4c0-113">Spesso è consentita solo un'istanza dell'agente per ogni macchina virtuale (nodo) e la configurazione dell'agente è condivisa tra tutte le applicazioni e i servizi in esecuzione nel nodo.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-113">Often there is only one instance of the agent allowed per virtual machine (node) and the agent configuration is shared among all applications and services running on that node.</span></span> 

* <span data-ttu-id="2f4c0-114">*Flessibilità*</span><span class="sxs-lookup"><span data-stu-id="2f4c0-114">*Flexibility*</span></span>
   
    * <span data-ttu-id="2f4c0-115">L'applicazione può inviare i dati ogni volta che è necessario, purché sia disponibile una libreria client che supporta il sistema di archiviazione dati di destinazione.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-115">The application can send the data wherever it needs to go, as long as there is a client library that supports the targeted data storage system.</span></span> <span data-ttu-id="2f4c0-116">È possibile aggiungere nuove destinazioni in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-116">New destinations can be added as desired.</span></span>
    * <span data-ttu-id="2f4c0-117">È possibile implementare complesse regole di acquisizione, filtro e aggregazione dati.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-117">Complex capture, filtering, and data-aggregation rules can be implemented.</span></span>
    * <span data-ttu-id="2f4c0-118">La raccolta di log basata su agenti è spesso limitata dai sink di dati supportati dall'agente.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-118">Agent-based log collection is often limited by the data sinks that the agent supports.</span></span> <span data-ttu-id="2f4c0-119">Alcuni agenti sono estendibili.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-119">Some agents are extensible.</span></span>

* <span data-ttu-id="2f4c0-120">*Accesso al contesto e ai dati di applicazione interni*</span><span class="sxs-lookup"><span data-stu-id="2f4c0-120">*Access to internal application data and context*</span></span>
   
    * <span data-ttu-id="2f4c0-121">Il sottosistema di diagnostica in esecuzione nel processo dell'applicazione o del servizio può facilmente aumentare le tracce con informazioni contestuali.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-121">The diagnostic subsystem running inside the application/service process can easily augment the traces with contextual information.</span></span>
    * <span data-ttu-id="2f4c0-122">Nella raccolta di log basata su agenti i dati devono essere inviati a un agente tramite un meccanismo di comunicazione interprocesso, ad esempio Event Tracing for Windows (ETW).</span><span class="sxs-lookup"><span data-stu-id="2f4c0-122">With agent-based log collection, the data must be sent to an agent via some inter-process communication mechanism, such as Event Tracing for Windows.</span></span> <span data-ttu-id="2f4c0-123">Questo meccanismo può imporre limitazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-123">This mechanism could impose additional limitations.</span></span>

<span data-ttu-id="2f4c0-124">È possibile combinare i due metodi di raccolta e trarre vantaggio da entrambi.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-124">It is possible to combine and benefit from both collection methods.</span></span> <span data-ttu-id="2f4c0-125">In realtà, potrebbe essere la soluzione migliore per molte applicazioni.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-125">Indeed, it might be the best solution for many applications.</span></span> <span data-ttu-id="2f4c0-126">La raccolta basata su agenti è una soluzione naturale per la raccolta di log correlati all'intero cluster e a singoli nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-126">Agent-based collection is a natural solution for collecting logs related to the whole cluster and individual cluster nodes.</span></span> <span data-ttu-id="2f4c0-127">Rispetto alla raccolta di log nel processo, è un modo molto più affidabile per diagnosticare i problemi di avvio e gli arresti anomali del servizio.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-127">It is much more reliable way, than in-process log collection, to diagnose service startup problems and crashes.</span></span> <span data-ttu-id="2f4c0-128">In presenza di molti servizi in esecuzione all'interno di un cluster di Service Fabric, se ogni servizio esegue autonomamente la raccolta di log nel processo si avrà un gran numero di connessioni in uscita dal cluster.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-128">Also, with many services running inside a Service Fabric cluster, each service doing its own in-process log collection results in numerous outgoing connections from the cluster.</span></span> <span data-ttu-id="2f4c0-129">Questo può mettere a dura prova sia il sottosistema di rete che la destinazione di log.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-129">Large number of outgoing connections is taxing both for the network subsystem and for the log destination.</span></span> <span data-ttu-id="2f4c0-130">Un agente come [**Diagnostica di Azure**](../cloud-services/cloud-services-dotnet-diagnostics.md) può raccogliere dati da più servizi e inviarli tutti tramite un numero limitato di connessioni, migliorando così la velocità effettiva.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-130">An agent such as [**Azure Diagnostics**](../cloud-services/cloud-services-dotnet-diagnostics.md) can gather data from multiple services and send all data through a few connections, improving throughput.</span></span> 

<span data-ttu-id="2f4c0-131">Questo articolo illustra come configurare una raccolta di log nel processo usando la [**libreria open-source EventFlow**](https://github.com/Azure/diagnostics-eventflow).</span><span class="sxs-lookup"><span data-stu-id="2f4c0-131">In this article, we show how to set up an in-process log collection using [**EventFlow open-source library**](https://github.com/Azure/diagnostics-eventflow).</span></span> <span data-ttu-id="2f4c0-132">È possibile usare altre librerie per lo stesso scopo, ma EventFlow ha il vantaggio di essere stata progettata specificamente per la raccolta di log nel processo e per supportare i servizi di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-132">Other libraries might be used for the same purpose, but EventFlow has the benefit of having been designed specifically for in-process log collection and to support Service Fabric services.</span></span> <span data-ttu-id="2f4c0-133">Come destinazione di log viene usato [**Azure Application Insights**](https://azure.microsoft.com/services/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="2f4c0-133">We use [**Azure Application Insights**](https://azure.microsoft.com/services/application-insights/) as the log destination.</span></span> <span data-ttu-id="2f4c0-134">Sono supportate anche altre destinazioni, ad esempio [**Hub eventi**](https://azure.microsoft.com/services/event-hubs/) o [**Elasticsearch**](https://www.elastic.co/products/elasticsearch).</span><span class="sxs-lookup"><span data-stu-id="2f4c0-134">Other destinations such as [**Event Hubs**](https://azure.microsoft.com/services/event-hubs/) or [**Elasticsearch**](https://www.elastic.co/products/elasticsearch) are also supported.</span></span> <span data-ttu-id="2f4c0-135">È sufficiente installare il pacchetto NuGet appropriato e configurare la destinazione nel file di configurazione EventFlow.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-135">It is just a question of installing appropriate NuGet package and configuring the destination in the EventFlow configuration file.</span></span> <span data-ttu-id="2f4c0-136">Per altre informazioni sulle destinazioni di log diverse da Application Insights, vedere la [documentazione di EventFlow](https://github.com/Azure/diagnostics-eventflow).</span><span class="sxs-lookup"><span data-stu-id="2f4c0-136">For more information on log destinations other than Application Insights, see [EventFlow documentation](https://github.com/Azure/diagnostics-eventflow).</span></span>

## <a name="adding-eventflow-library-to-a-service-fabric-service-project"></a><span data-ttu-id="2f4c0-137">Aggiunta della libreria EventFlow a un progetto di servizio di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2f4c0-137">Adding EventFlow library to a Service Fabric service project</span></span>
<span data-ttu-id="2f4c0-138">I file binari di EventFlow sono disponibili come set di pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-138">EventFlow binaries are available as a set of NuGet packages.</span></span> <span data-ttu-id="2f4c0-139">Per aggiungere EventFlow a un progetto di servizio di Service Fabric, fare clic sul progetto in Esplora soluzioni e scegliere "Gestisci pacchetti NuGet".</span><span class="sxs-lookup"><span data-stu-id="2f4c0-139">To add EventFlow to a Service Fabric service project, right-click the project in the Solution Explorer and choose "Manage NuGet packages."</span></span> <span data-ttu-id="2f4c0-140">Passare alla scheda "Sfoglia" e cercare "`Diagnostics.EventFlow`":</span><span class="sxs-lookup"><span data-stu-id="2f4c0-140">Switch to the "Browse" tab and search for "`Diagnostics.EventFlow`":</span></span>

![Pacchetti NuGet di EventFlow nell'interfaccia utente di gestione pacchetti NuGet di Visual Studio][1]

<span data-ttu-id="2f4c0-142">Il servizio che ospita EventFlow deve includere pacchetti appropriati a seconda dell'origine e della destinazione dei log applicazioni.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-142">The service hosting EventFlow should include appropriate packages depending on the source and destination for the application logs.</span></span> <span data-ttu-id="2f4c0-143">Aggiungere i pacchetti seguenti:</span><span class="sxs-lookup"><span data-stu-id="2f4c0-143">Add the following packages:</span></span> 

* `Microsoft.Diagnostics.EventFlow.Inputs.EventSource` 
    * <span data-ttu-id="2f4c0-144">Per acquisire dati dalla classe EventSource del servizio e da oggetti EventSource standard, ad esempio *Microsoft-ServiceFabric-Services* e *Microsoft-ServiceFabric-Actors*.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-144">(to capture data from the service's EventSource class, and from standard EventSources such as *Microsoft-ServiceFabric-Services* and *Microsoft-ServiceFabric-Actors*)</span></span>
* `Microsoft.Diagnostics.EventFlow.Outputs.ApplicationInsights` 
    * <span data-ttu-id="2f4c0-145">I log verranno inviati a una risorsa di Azure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-145">(we are going to send the logs to an Azure Application Insights resource)</span></span>  
* `Microsoft.Diagnostics.EventFlow.ServiceFabric` 
    * <span data-ttu-id="2f4c0-146">Consente l'inizializzazione della pipeline EventFlow dalla configurazione del servizio di Service Fabric e segnala eventuali problemi tramite l'invio di dati di diagnostica in forma di report sull'integrità di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-146">(enables initialization of the EventFlow pipeline from Service Fabric service configuration and reports any problems with sending diagnostic data as Service Fabric health reports)</span></span>

> [!NOTE]
> <span data-ttu-id="2f4c0-147">Per il pacchetto `Microsoft.Diagnostics.EventFlow.Inputs.EventSource` il progetto di servizio deve puntare a .NET Framework 4.6 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-147">`Microsoft.Diagnostics.EventFlow.Inputs.EventSource` package requires the service project to target .NET Framework 4.6 or newer.</span></span> <span data-ttu-id="2f4c0-148">Assicurarsi di impostare il framework di destinazione corretto nelle proprietà del progetto prima di installare questo pacchetto.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-148">Make sure you set the appropriate target framework in project properties before installing this package.</span></span> 

<span data-ttu-id="2f4c0-149">Dopo aver installato tutti i pacchetti, è necessario configurare e abilitare EventFlow nel servizio.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-149">After all the packages are installed, the next step is to configure and enable EventFlow in the service.</span></span>

## <a name="configuring-and-enabling-log-collection"></a><span data-ttu-id="2f4c0-150">Configurazione e abilitazione della raccolta di log</span><span class="sxs-lookup"><span data-stu-id="2f4c0-150">Configuring and enabling log collection</span></span>
<span data-ttu-id="2f4c0-151">La pipeline EventFlow, responsabile dell'invio dei log, viene creata da una specifica archiviata in un file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-151">EventFlow pipeline, responsible for sending the logs, is created from a specification stored in a configuration file.</span></span> <span data-ttu-id="2f4c0-152">Il pacchetto `Microsoft.Diagnostics.EventFlow.ServiceFabric` installa un file di configurazione di iniziale di EventFlow nella cartella `PackageRoot\Config` della soluzione.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-152">`Microsoft.Diagnostics.EventFlow.ServiceFabric` package installs a starting EventFlow configuration file under `PackageRoot\Config` solution folder.</span></span> <span data-ttu-id="2f4c0-153">Il nome del file è `eventFlowConfig.json`.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-153">The file name is `eventFlowConfig.json`.</span></span> <span data-ttu-id="2f4c0-154">Questo file di configurazione deve essere modificato per l'acquisizione di dati dalla classe `EventSource` del servizio predefinito e l'invio di dati al servizio Application Insights.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-154">This configuration file needs to be modified to capture data from the default service `EventSource` class and send data to Application Insights service.</span></span>

> [!NOTE]
> <span data-ttu-id="2f4c0-155">Si presuppone che si abbia familiarità con il servizio **Azure Application Insights** e che sia disponibile una risorsa di Application Insights da usare per monitorare il servizio di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-155">We assume that you are familiar with **Azure Application Insights** service and that you have an Application Insights resource that you plan to use to monitor your Service Fabric service.</span></span> <span data-ttu-id="2f4c0-156">Per altre informazioni, vedere [Creare una risorsa di Application Insights](../application-insights/app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="2f4c0-156">If you need more information, please see [Create an Application Insights resource](../application-insights/app-insights-create-new-resource.md).</span></span>

<span data-ttu-id="2f4c0-157">Aprire il file `eventFlowConfig.json` nell'editor e modificarne il contenuto, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-157">Open the `eventFlowConfig.json` file in the editor and change its content as shown below.</span></span> <span data-ttu-id="2f4c0-158">Assicurarsi di sostituire il nome ServiceEventSource e la chiave di strumentazione di Application Insights in base ai commenti.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-158">Make sure to replace the ServiceEventSource name and Application Insights instrumentation key according to comments.</span></span> 

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

> [!NOTE]
> <span data-ttu-id="2f4c0-159">Il nome dell'oggetto ServiceEventSource del servizio è il valore della proprietà Name dell'oggetto `EventSourceAttribute` applicato alla classe ServiceEventSource.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-159">The name of service's ServiceEventSource is the value of the Name property of the `EventSourceAttribute` applied to the ServiceEventSource class.</span></span> <span data-ttu-id="2f4c0-160">Tutto questo è specificato nel file `ServiceEventSource.cs`, che fa parte del codice del servizio.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-160">It is all specified in the `ServiceEventSource.cs` file, which is part of the service code.</span></span> <span data-ttu-id="2f4c0-161">Ad esempio, nel frammento di codice seguente il nome dell'oggetto ServiceEventSource è *MyCompany-Application1-Stateless1*:</span><span class="sxs-lookup"><span data-stu-id="2f4c0-161">For example, in the following code snippet the name of the ServiceEventSource is *MyCompany-Application1-Stateless1*:</span></span>
> ```csharp
> [EventSource(Name = "MyCompany-Application1-Stateless1")]
> internal sealed class ServiceEventSource : EventSource
> {
>    // (rest of ServiceEventSource implementation)
>} 
> ```

<span data-ttu-id="2f4c0-162">Si noti che il file `eventFlowConfig.json` fa parte del pacchetto di configurazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-162">Note that `eventFlowConfig.json` file is part of service configuration package.</span></span> <span data-ttu-id="2f4c0-163">Le modifiche apportate a questo file possono essere incluse in aggiornamenti del servizio completi o della sola configurazione, in base ai controlli di integrità dell'aggiornamento di Service Fabric e al ripristino dello stato precedente automatico in caso di errore di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-163">Changes to this file can be included in full- or configuration-only upgrades of the service, subject to Service Fabric upgrade health checks and automatic rollback if there is upgrade failure.</span></span> <span data-ttu-id="2f4c0-164">Per altre informazioni, vedere [Aggiornamento delle applicazioni di Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="2f4c0-164">For more information, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="2f4c0-165">Il passaggio finale consiste nel creare un'istanza della pipeline EventFlow nel codice di avvio del servizio, situato nel file `Program.cs`.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-165">The final step is to instantiate EventFlow pipeline in your service's startup code, located in `Program.cs` file.</span></span> <span data-ttu-id="2f4c0-166">L'esempio seguente mostra le aggiunte correlate a EventFlow contrassegnate con commenti, a partire da `****`:</span><span class="sxs-lookup"><span data-stu-id="2f4c0-166">In the following example  EventFlow-related additions are marked with comments starting with `****`:</span></span>

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

<span data-ttu-id="2f4c0-167">Il nome passato come parametro del metodo `CreatePipeline` di `ServiceFabricDiagnosticsPipelineFactory` è il nome dell'*entità di integrità* che rappresenta la pipeline di raccolta di log EventFlow.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-167">The name passed as the parameter of the `CreatePipeline` method of the `ServiceFabricDiagnosticsPipelineFactory` is the name of the *health entity* representing the EventFlow log collection pipeline.</span></span> <span data-ttu-id="2f4c0-168">Questo nome viene usato se EventFlow rileva un errore e lo segnala tramite il sottosistema di integrità di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-168">This name is used if EventFlow encounters and error and reports it through the Service Fabric health subsystem.</span></span>

## <a name="verification"></a><span data-ttu-id="2f4c0-169">Verifica</span><span class="sxs-lookup"><span data-stu-id="2f4c0-169">Verification</span></span>
<span data-ttu-id="2f4c0-170">Avviare il servizio e osservare la finestra dell'output di debug di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-170">Start your service and observe the Debug output window in Visual Studio.</span></span> <span data-ttu-id="2f4c0-171">Dopo l'avvio del servizio, dovrebbero essere visibili le prove dell'invio di record di Application Insights Telemetry.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-171">After the service is started, you should start seeing evidence that your service is sending "Application Insights Telemetry" records.</span></span> <span data-ttu-id="2f4c0-172">Aprire un Web browser e passare alla risorsa di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="2f4c0-172">Open a web browser and navigate go to your Application Insights resource.</span></span> <span data-ttu-id="2f4c0-173">Aprire la scheda "Ricerca", nella parte superiore del pannello predefinito "Panoramica".</span><span class="sxs-lookup"><span data-stu-id="2f4c0-173">Open "Search" tab (at the top of the default "Overview" blade).</span></span> <span data-ttu-id="2f4c0-174">Dopo alcuni istanti, le tracce dovrebbero essere visibili nel portale di Application Insights:</span><span class="sxs-lookup"><span data-stu-id="2f4c0-174">After a short delay you should start seeing your traces in the Application Insights portal:</span></span>

![Portale di Application Insights con i log da un'applicazione di Service Fabric][2]

## <a name="next-steps"></a><span data-ttu-id="2f4c0-176">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2f4c0-176">Next steps</span></span>
* [<span data-ttu-id="2f4c0-177">Altre informazioni sulla diagnostica e il monitoraggio di un servizio di infrastruttura di servizi</span><span class="sxs-lookup"><span data-stu-id="2f4c0-177">Learn more about diagnosing and monitoring a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
* [<span data-ttu-id="2f4c0-178">Documentazione di EventFlow</span><span class="sxs-lookup"><span data-stu-id="2f4c0-178">EventFlow documentation</span></span>](https://github.com/Azure/diagnostics-eventflow)


<!--Image references-->
[1]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/eventflow-nugets.png
[2]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/ai-traces.png
