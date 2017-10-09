---
title: aaaCollect log direttamente da un Azure Service Fabric processo del servizio | Microsoft Azure
description: Descrive le applicazioni possono inviare i log direttamente, come posizione centrale tooa Azure Application Insights o Elasticsearch, senza basarsi sull'agente di diagnostica di Azure di Service Fabric.
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
ms.openlocfilehash: d0681a2a6aaa76028d7cb469c31c006f24bbe954
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="collect-logs-directly-from-an-azure-service-fabric-service-process"></a><span data-ttu-id="0043c-103">Raccogliere log direttamente da un processo del servizio di Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="0043c-103">Collect logs directly from an Azure Service Fabric service process</span></span>
## <a name="in-process-log-collection"></a><span data-ttu-id="0043c-104">Raccolta di log nel processo</span><span class="sxs-lookup"><span data-stu-id="0043c-104">In-process log collection</span></span>
<span data-ttu-id="0043c-105">Applicazione di raccogliere i log di [l'estensione diagnostica Azure](service-fabric-diagnostics-how-to-setup-wad.md) è un'opzione valida per **Azure Service Fabric** servizi se set hello di log origini e destinazioni è ridotto, non cambiano spesso e non esiste rappresenta un mapping diretto tra origini hello e le destinazioni.</span><span class="sxs-lookup"><span data-stu-id="0043c-105">Collecting application logs using [Azure Diagnostics extension](service-fabric-diagnostics-how-to-setup-wad.md) is a good option for **Azure Service Fabric** services if hello set of log sources and destinations is small, does not change often, and there is a straightforward mapping between hello sources and their destinations.</span></span> <span data-ttu-id="0043c-106">In caso contrario, in alternativa, è toohave servizi inviano i log direttamente posizione centrale tooa.</span><span class="sxs-lookup"><span data-stu-id="0043c-106">If not, an alternative is toohave services send their logs directly tooa central location.</span></span> <span data-ttu-id="0043c-107">Questo processo è noto come **raccolta di log nel processo** e presenta diversi vantaggi potenziali:</span><span class="sxs-lookup"><span data-stu-id="0043c-107">This process is known as **in-process log collection** and has several potential advantages:</span></span>

* <span data-ttu-id="0043c-108">*Facilità di configurazione e distribuzione*</span><span class="sxs-lookup"><span data-stu-id="0043c-108">*Easy configuration and deployment*</span></span>

    * <span data-ttu-id="0043c-109">configurazione di Hello di raccolta dati di diagnostica è solo parte della configurazione del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="0043c-109">hello configuration of diagnostic data collection is just part of hello service configuration.</span></span> <span data-ttu-id="0043c-110">È facile tooalways keep "sincronizzato" con hello il resto dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="0043c-110">It is easy tooalways keep it "in sync" with hello rest of hello application.</span></span>
    * <span data-ttu-id="0043c-111">È facile ottenere la configurazione per ogni applicazione o servizio.</span><span class="sxs-lookup"><span data-stu-id="0043c-111">Per-application or per-service configuration is easily achievable.</span></span>
        * <span data-ttu-id="0043c-112">Raccolta di log basato su agenti richiede in genere una distribuzione separata e la configurazione dell'agente, diagnostica hello è un'attività amministrativa extra e una potenziale fonte di errori.</span><span class="sxs-lookup"><span data-stu-id="0043c-112">Agent-based log collection usually requires a separate deployment and configuration of hello diagnostic agent, which is an extra administrative task and a potential source of errors.</span></span> <span data-ttu-id="0043c-113">Spesso è presente solo un'istanza dell'agente di hello consentito per ogni macchina virtuale (nodo) e la configurazione dell'agente hello viene condiviso tra tutte le applicazioni e servizi in esecuzione su tale nodo.</span><span class="sxs-lookup"><span data-stu-id="0043c-113">Often there is only one instance of hello agent allowed per virtual machine (node) and hello agent configuration is shared among all applications and services running on that node.</span></span> 

* <span data-ttu-id="0043c-114">*Flessibilità*</span><span class="sxs-lookup"><span data-stu-id="0043c-114">*Flexibility*</span></span>
   
    * <span data-ttu-id="0043c-115">un'applicazione Hello può inviare dati di hello ogni volta che è necessario toogo, purché vi è una libreria client che supporta il sistema di archiviazione dati hello di destinazione.</span><span class="sxs-lookup"><span data-stu-id="0043c-115">hello application can send hello data wherever it needs toogo, as long as there is a client library that supports hello targeted data storage system.</span></span> <span data-ttu-id="0043c-116">È possibile aggiungere nuove destinazioni in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="0043c-116">New destinations can be added as desired.</span></span>
    * <span data-ttu-id="0043c-117">È possibile implementare complesse regole di acquisizione, filtro e aggregazione dati.</span><span class="sxs-lookup"><span data-stu-id="0043c-117">Complex capture, filtering, and data-aggregation rules can be implemented.</span></span>
    * <span data-ttu-id="0043c-118">Raccolta di log basato su agenti è spesso limitata dalla sink dati hello che hello agente supporta.</span><span class="sxs-lookup"><span data-stu-id="0043c-118">Agent-based log collection is often limited by hello data sinks that hello agent supports.</span></span> <span data-ttu-id="0043c-119">Alcuni agenti sono estendibili.</span><span class="sxs-lookup"><span data-stu-id="0043c-119">Some agents are extensible.</span></span>

* <span data-ttu-id="0043c-120">*Contesto e accedere ai dati di applicazione toointernal*</span><span class="sxs-lookup"><span data-stu-id="0043c-120">*Access toointernal application data and context*</span></span>
   
    * <span data-ttu-id="0043c-121">sottosistema di diagnostica Hello in esecuzione nel processo di applicazioni o servizi hello possibile integrare facilmente le tracce di hello con informazioni contestuali.</span><span class="sxs-lookup"><span data-stu-id="0043c-121">hello diagnostic subsystem running inside hello application/service process can easily augment hello traces with contextual information.</span></span>
    * <span data-ttu-id="0043c-122">Con la raccolta di log basato su agenti, hello devono essere inviati dati agente tooan tramite un meccanismo di comunicazione tra processi, ad esempio Event Tracing for Windows.</span><span class="sxs-lookup"><span data-stu-id="0043c-122">With agent-based log collection, hello data must be sent tooan agent via some inter-process communication mechanism, such as Event Tracing for Windows.</span></span> <span data-ttu-id="0043c-123">Questo meccanismo può imporre limitazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="0043c-123">This mechanism could impose additional limitations.</span></span>

<span data-ttu-id="0043c-124">È possibile toocombine e trarre vantaggio da entrambi i metodi di raccolta.</span><span class="sxs-lookup"><span data-stu-id="0043c-124">It is possible toocombine and benefit from both collection methods.</span></span> <span data-ttu-id="0043c-125">Infatti, potrebbe essere la soluzione migliore di hello per molte applicazioni.</span><span class="sxs-lookup"><span data-stu-id="0043c-125">Indeed, it might be hello best solution for many applications.</span></span> <span data-ttu-id="0043c-126">Basato su agenti di raccolta è una soluzione naturale per la raccolta dell'intero cluster toohello correlati registri e i singoli nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="0043c-126">Agent-based collection is a natural solution for collecting logs related toohello whole cluster and individual cluster nodes.</span></span> <span data-ttu-id="0043c-127">È molto più affidabile, rispetto alla raccolta di log in-process, problemi di avvio del servizio toodiagnose e arresti anomali del sistema.</span><span class="sxs-lookup"><span data-stu-id="0043c-127">It is much more reliable way, than in-process log collection, toodiagnose service startup problems and crashes.</span></span> <span data-ttu-id="0043c-128">Con molti servizi in esecuzione all'interno di un cluster di Service Fabric, inoltre, ogni servizio esegue la propria raccolta di log in-process comporta molte connessioni in uscita dal cluster hello.</span><span class="sxs-lookup"><span data-stu-id="0043c-128">Also, with many services running inside a Service Fabric cluster, each service doing its own in-process log collection results in numerous outgoing connections from hello cluster.</span></span> <span data-ttu-id="0043c-129">È un numero elevato di connessioni in uscita sovraccarico per il sottosistema di rete hello e per la destinazione di log hello.</span><span class="sxs-lookup"><span data-stu-id="0043c-129">Large number of outgoing connections is taxing both for hello network subsystem and for hello log destination.</span></span> <span data-ttu-id="0043c-130">Un agente come [**Diagnostica di Azure**](../cloud-services/cloud-services-dotnet-diagnostics.md) può raccogliere dati da più servizi e inviarli tutti tramite un numero limitato di connessioni, migliorando così la velocità effettiva.</span><span class="sxs-lookup"><span data-stu-id="0043c-130">An agent such as [**Azure Diagnostics**](../cloud-services/cloud-services-dotnet-diagnostics.md) can gather data from multiple services and send all data through a few connections, improving throughput.</span></span> 

<span data-ttu-id="0043c-131">In questo articolo viene illustrata la modalità tooset di un processo nel log insieme utilizzando [ **libreria open source EventFlow**](https://github.com/Azure/diagnostics-eventflow).</span><span class="sxs-lookup"><span data-stu-id="0043c-131">In this article, we show how tooset up an in-process log collection using [**EventFlow open-source library**](https://github.com/Azure/diagnostics-eventflow).</span></span> <span data-ttu-id="0043c-132">Altre librerie potrebbero essere utilizzate per hello stesso scopo, ma EventFlow ha il vantaggio di hello di che è stato progettato specificatamente per i servizi Service Fabric insieme e toosupport nel processo log.</span><span class="sxs-lookup"><span data-stu-id="0043c-132">Other libraries might be used for hello same purpose, but EventFlow has hello benefit of having been designed specifically for in-process log collection and toosupport Service Fabric services.</span></span> <span data-ttu-id="0043c-133">Utilizziamo [ **Azure Application Insights** ](https://azure.microsoft.com/services/application-insights/) come destinazione di log hello.</span><span class="sxs-lookup"><span data-stu-id="0043c-133">We use [**Azure Application Insights**](https://azure.microsoft.com/services/application-insights/) as hello log destination.</span></span> <span data-ttu-id="0043c-134">Sono supportate anche altre destinazioni, ad esempio [**Hub eventi**](https://azure.microsoft.com/services/event-hubs/) o [**Elasticsearch**](https://www.elastic.co/products/elasticsearch).</span><span class="sxs-lookup"><span data-stu-id="0043c-134">Other destinations such as [**Event Hubs**](https://azure.microsoft.com/services/event-hubs/) or [**Elasticsearch**](https://www.elastic.co/products/elasticsearch) are also supported.</span></span> <span data-ttu-id="0043c-135">È semplicemente una questione di installazione del pacchetto NuGet appropriato e la configurazione di destinazione hello nel file di configurazione EventFlow hello.</span><span class="sxs-lookup"><span data-stu-id="0043c-135">It is just a question of installing appropriate NuGet package and configuring hello destination in hello EventFlow configuration file.</span></span> <span data-ttu-id="0043c-136">Per altre informazioni sulle destinazioni di log diverse da Application Insights, vedere la [documentazione di EventFlow](https://github.com/Azure/diagnostics-eventflow).</span><span class="sxs-lookup"><span data-stu-id="0043c-136">For more information on log destinations other than Application Insights, see [EventFlow documentation](https://github.com/Azure/diagnostics-eventflow).</span></span>

## <a name="adding-eventflow-library-tooa-service-fabric-service-project"></a><span data-ttu-id="0043c-137">Aggiunta di progetto di servizio Service Fabric tooa EventFlow libreria</span><span class="sxs-lookup"><span data-stu-id="0043c-137">Adding EventFlow library tooa Service Fabric service project</span></span>
<span data-ttu-id="0043c-138">I file binari di EventFlow sono disponibili come set di pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="0043c-138">EventFlow binaries are available as a set of NuGet packages.</span></span> <span data-ttu-id="0043c-139">tooadd progetto del servizio Service Fabric tooa EventFlow, fare clic sul progetto in Esplora soluzioni hello hello e scegliere "Gestisci NuGet pacchetti".</span><span class="sxs-lookup"><span data-stu-id="0043c-139">tooadd EventFlow tooa Service Fabric service project, right-click hello project in hello Solution Explorer and choose "Manage NuGet packages."</span></span> <span data-ttu-id="0043c-140">Cambia la scheda "Sfoglia" toohello e cercare "`Diagnostics.EventFlow`":</span><span class="sxs-lookup"><span data-stu-id="0043c-140">Switch toohello "Browse" tab and search for "`Diagnostics.EventFlow`":</span></span>

![Pacchetti NuGet di EventFlow nell'interfaccia utente di gestione pacchetti NuGet di Visual Studio][1]

<span data-ttu-id="0043c-142">servizio Hello hosting EventFlow deve includere pacchetti appropriati a seconda di hello origine e di destinazione per i log applicazioni hello.</span><span class="sxs-lookup"><span data-stu-id="0043c-142">hello service hosting EventFlow should include appropriate packages depending on hello source and destination for hello application logs.</span></span> <span data-ttu-id="0043c-143">Aggiungere i seguenti pacchetti hello:</span><span class="sxs-lookup"><span data-stu-id="0043c-143">Add hello following packages:</span></span> 

* `Microsoft.Diagnostics.EventFlow.Inputs.EventSource` 
    * <span data-ttu-id="0043c-144">(toocapture dati dalla classe EventSource del servizio hello e da EventSources standard, ad esempio *ServiceFabric-Microsoft-Services* e *ServiceFabric-Microsoft-attori*)</span><span class="sxs-lookup"><span data-stu-id="0043c-144">(toocapture data from hello service's EventSource class, and from standard EventSources such as *Microsoft-ServiceFabric-Services* and *Microsoft-ServiceFabric-Actors*)</span></span>
* `Microsoft.Diagnostics.EventFlow.Outputs.ApplicationInsights` 
    * <span data-ttu-id="0043c-145">(si stabilirà una risorsa di Azure Application Insights tooan di toosend hello log)</span><span class="sxs-lookup"><span data-stu-id="0043c-145">(we are going toosend hello logs tooan Azure Application Insights resource)</span></span>  
* `Microsoft.Diagnostics.EventFlow.ServiceFabric` 
    * <span data-ttu-id="0043c-146">(consente l'inizializzazione della pipeline EventFlow hello dalla configurazione del servizio Service Fabric e segnala eventuali problemi con l'invio di dati di diagnostica come report di integrità dell'infrastruttura di servizio)</span><span class="sxs-lookup"><span data-stu-id="0043c-146">(enables initialization of hello EventFlow pipeline from Service Fabric service configuration and reports any problems with sending diagnostic data as Service Fabric health reports)</span></span>

> [!NOTE]
> <span data-ttu-id="0043c-147">`Microsoft.Diagnostics.EventFlow.Inputs.EventSource`il pacchetto richiede hello servizio progetto tootarget .NET Framework 4.6 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="0043c-147">`Microsoft.Diagnostics.EventFlow.Inputs.EventSource` package requires hello service project tootarget .NET Framework 4.6 or newer.</span></span> <span data-ttu-id="0043c-148">Assicurarsi di impostare il framework di destinazione appropriata hello nelle proprietà del progetto prima di installare questo pacchetto.</span><span class="sxs-lookup"><span data-stu-id="0043c-148">Make sure you set hello appropriate target framework in project properties before installing this package.</span></span> 

<span data-ttu-id="0043c-149">Dopo che tutti hello pacchetti installati, passaggio successivo hello è tooconfigure e abilitare EventFlow nel servizio hello.</span><span class="sxs-lookup"><span data-stu-id="0043c-149">After all hello packages are installed, hello next step is tooconfigure and enable EventFlow in hello service.</span></span>

## <a name="configuring-and-enabling-log-collection"></a><span data-ttu-id="0043c-150">Configurazione e abilitazione della raccolta di log</span><span class="sxs-lookup"><span data-stu-id="0043c-150">Configuring and enabling log collection</span></span>
<span data-ttu-id="0043c-151">Pipeline EventFlow, responsabile per l'invio di log di hello, viene creata da una specifica archiviata in un file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="0043c-151">EventFlow pipeline, responsible for sending hello logs, is created from a specification stored in a configuration file.</span></span> <span data-ttu-id="0043c-152">Il pacchetto `Microsoft.Diagnostics.EventFlow.ServiceFabric` installa un file di configurazione di iniziale di EventFlow nella cartella `PackageRoot\Config` della soluzione.</span><span class="sxs-lookup"><span data-stu-id="0043c-152">`Microsoft.Diagnostics.EventFlow.ServiceFabric` package installs a starting EventFlow configuration file under `PackageRoot\Config` solution folder.</span></span> <span data-ttu-id="0043c-153">nome del file Hello è `eventFlowConfig.json`.</span><span class="sxs-lookup"><span data-stu-id="0043c-153">hello file name is `eventFlowConfig.json`.</span></span> <span data-ttu-id="0043c-154">Questo file di configurazione deve toobe modificato toocapture dati dal servizio predefinito hello `EventSource` classe e di servizio dati di Insights tooApplication di trasmissione.</span><span class="sxs-lookup"><span data-stu-id="0043c-154">This configuration file needs toobe modified toocapture data from hello default service `EventSource` class and send data tooApplication Insights service.</span></span>

> [!NOTE]
> <span data-ttu-id="0043c-155">Si presuppone che si ha familiarità con **Azure Application Insights** servizio e disporre di una risorsa di Application Insights pianificare toouse toomonitor il servizio Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="0043c-155">We assume that you are familiar with **Azure Application Insights** service and that you have an Application Insights resource that you plan toouse toomonitor your Service Fabric service.</span></span> <span data-ttu-id="0043c-156">Per altre informazioni, vedere [Creare una risorsa di Application Insights](../application-insights/app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="0043c-156">If you need more information, please see [Create an Application Insights resource](../application-insights/app-insights-create-new-resource.md).</span></span>

<span data-ttu-id="0043c-157">Aprire hello `eventFlowConfig.json` file nell'editor di hello e modifica il contenuto, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="0043c-157">Open hello `eventFlowConfig.json` file in hello editor and change its content as shown below.</span></span> <span data-ttu-id="0043c-158">Verificare che tooreplace hello ServiceEventSource nome e la chiave di strumentazione di Application Insights in base toocomments.</span><span class="sxs-lookup"><span data-stu-id="0043c-158">Make sure tooreplace hello ServiceEventSource name and Application Insights instrumentation key according toocomments.</span></span> 

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

> [!NOTE]
> <span data-ttu-id="0043c-159">Hello ServiceEventSource del servizio è denominato valore hello hello proprietà Name di hello `EventSourceAttribute` toohello ServiceEventSource classe applicato.</span><span class="sxs-lookup"><span data-stu-id="0043c-159">hello name of service's ServiceEventSource is hello value of hello Name property of hello `EventSourceAttribute` applied toohello ServiceEventSource class.</span></span> <span data-ttu-id="0043c-160">Tutto è specificato in hello `ServiceEventSource.cs` file, che fa parte del codice del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="0043c-160">It is all specified in hello `ServiceEventSource.cs` file, which is part of hello service code.</span></span> <span data-ttu-id="0043c-161">Ad esempio, in hello seguente frammento di codice hello nome del codice hello ServiceEventSource è *MyCompany-Application1-Stateless1*:</span><span class="sxs-lookup"><span data-stu-id="0043c-161">For example, in hello following code snippet hello name of hello ServiceEventSource is *MyCompany-Application1-Stateless1*:</span></span>
> ```csharp
> [EventSource(Name = "MyCompany-Application1-Stateless1")]
> internal sealed class ServiceEventSource : EventSource
> {
>    // (rest of ServiceEventSource implementation)
>} 
> ```

<span data-ttu-id="0043c-162">Si noti che il file `eventFlowConfig.json` fa parte del pacchetto di configurazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="0043c-162">Note that `eventFlowConfig.json` file is part of service configuration package.</span></span> <span data-ttu-id="0043c-163">File toothis modifiche può essere inclusi in full o configurazione-solo gli aggiornamenti del servizio di hello, soggetto tooService aggiornamento controlli di integrità e il rollback automatico nel caso di errore di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="0043c-163">Changes toothis file can be included in full- or configuration-only upgrades of hello service, subject tooService Fabric upgrade health checks and automatic rollback if there is upgrade failure.</span></span> <span data-ttu-id="0043c-164">Per altre informazioni, vedere [Aggiornamento delle applicazioni di Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="0043c-164">For more information, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="0043c-165">passaggio finale Hello è tooinstantiate EventFlow pipeline nel codice di avvio del servizio, si trova `Program.cs` file.</span><span class="sxs-lookup"><span data-stu-id="0043c-165">hello final step is tooinstantiate EventFlow pipeline in your service's startup code, located in `Program.cs` file.</span></span> <span data-ttu-id="0043c-166">In hello aggiunte correlati EventFlow di esempio seguenti sono contrassegnate con commenti a partire da `****`:</span><span class="sxs-lookup"><span data-stu-id="0043c-166">In hello following example  EventFlow-related additions are marked with comments starting with `****`:</span></span>

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

<span data-ttu-id="0043c-167">il nome di Hello passato come parametro hello di hello `CreatePipeline` metodo hello `ServiceFabricDiagnosticsPipelineFactory` nome hello di hello *entità integrità* che rappresenta di pipeline di raccolta log EventFlow hello.</span><span class="sxs-lookup"><span data-stu-id="0043c-167">hello name passed as hello parameter of hello `CreatePipeline` method of hello `ServiceFabricDiagnosticsPipelineFactory` is hello name of hello *health entity* representing hello EventFlow log collection pipeline.</span></span> <span data-ttu-id="0043c-168">Questo nome viene utilizzato se viene rilevato EventFlow e di errore e la segnala tramite hello del sottosistema di integrità di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="0043c-168">This name is used if EventFlow encounters and error and reports it through hello Service Fabric health subsystem.</span></span>

## <a name="verification"></a><span data-ttu-id="0043c-169">Verifica</span><span class="sxs-lookup"><span data-stu-id="0043c-169">Verification</span></span>
<span data-ttu-id="0043c-170">Avviare il servizio e osservare hello Debug la finestra di output in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0043c-170">Start your service and observe hello Debug output window in Visual Studio.</span></span> <span data-ttu-id="0043c-171">Una volta avviato il servizio di hello, è consigliabile iniziare a visualizzare la prova che il servizio invia i record di "Telemetria di Application Insights".</span><span class="sxs-lookup"><span data-stu-id="0043c-171">After hello service is started, you should start seeing evidence that your service is sending "Application Insights Telemetry" records.</span></span> <span data-ttu-id="0043c-172">Aprire un web browser e passare la risorsa di Application Insights tooyour passare.</span><span class="sxs-lookup"><span data-stu-id="0043c-172">Open a web browser and navigate go tooyour Application Insights resource.</span></span> <span data-ttu-id="0043c-173">Aprire la scheda "Ricerca" (nella parte superiore di hello del Pannello di hello predefinito "Overview").</span><span class="sxs-lookup"><span data-stu-id="0043c-173">Open "Search" tab (at hello top of hello default "Overview" blade).</span></span> <span data-ttu-id="0043c-174">Dopo un breve ritardo si dovrebbe iniziare a vedere le tracce nel portale Application Insights hello:</span><span class="sxs-lookup"><span data-stu-id="0043c-174">After a short delay you should start seeing your traces in hello Application Insights portal:</span></span>

![Portale di Application Insights con i log da un'applicazione di Service Fabric][2]

## <a name="next-steps"></a><span data-ttu-id="0043c-176">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0043c-176">Next steps</span></span>
* [<span data-ttu-id="0043c-177">Altre informazioni sulla diagnostica e il monitoraggio di un servizio di infrastruttura di servizi</span><span class="sxs-lookup"><span data-stu-id="0043c-177">Learn more about diagnosing and monitoring a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
* [<span data-ttu-id="0043c-178">Documentazione di EventFlow</span><span class="sxs-lookup"><span data-stu-id="0043c-178">EventFlow documentation</span></span>](https://github.com/Azure/diagnostics-eventflow)


<!--Image references-->
[1]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/eventflow-nugets.png
[2]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/ai-traces.png
