---
title: "aaaAzure Application Insights il supporto per più componenti, microservizi e contenitori | Documenti Microsoft"
description: "Monitoraggio di applicazioni costituite da più componenti o ruoli per le prestazioni e l'uso."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/17/2017
ms.author: bwren
ms.openlocfilehash: 6185eedf32ec450d7541603b94de6c3dcdf64a85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-multi-component-applications-with-application-insights-preview"></a><span data-ttu-id="ad2df-103">Monitorare le applicazioni multi-componente con Application Insights (anteprima)</span><span class="sxs-lookup"><span data-stu-id="ad2df-103">Monitor multi-component applications with Application Insights (preview)</span></span>

<span data-ttu-id="ad2df-104">È possibile monitorare le app che sono costituite da più componenti, ruoli o servizi del server con [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ad2df-104">You can monitor apps that consist of multiple server components, roles, or services with [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="ad2df-105">stato di Hello dei componenti di hello e le reciproche relazioni hello vengono visualizzati in un singolo mapping di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="ad2df-105">hello health of hello components and hello relationships between them are displayed on a single Application Map.</span></span> <span data-ttu-id="ad2df-106">È possibile tracciare le singole operazioni tramite più componenti con correlazione automatica HTTP.</span><span class="sxs-lookup"><span data-stu-id="ad2df-106">You can trace individual operations through multiple components with automatic HTTP correlation.</span></span> <span data-ttu-id="ad2df-107">È possibile integrare e correlare la diagnostica del contenitore con i dati di telemetria dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ad2df-107">Container diagnostics can be integrated and correlated with application telemetry.</span></span> <span data-ttu-id="ad2df-108">Utilizzare una singola risorsa di Application Insights per tutti i componenti dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="ad2df-108">Use a single Application Insights resource for all hello components of your application.</span></span> 

![Mappa dell'applicazione multi-componente](./media/app-insights-monitor-multi-role-apps/app-map.png)

<span data-ttu-id="ad2df-110">Utilizziamo 'componente' toomean qui qualsiasi parte di un'applicazione di grandi dimensioni funzionante.</span><span class="sxs-lookup"><span data-stu-id="ad2df-110">We use 'component' here toomean any functioning part of a large application.</span></span> <span data-ttu-id="ad2df-111">Ad esempio, una tipica applicazione aziendale può essere costituito da codice client in esecuzione nel browser, parlando tooone o più servizi web di app, che a sua volta utilizza nuovamente terminano i servizi.</span><span class="sxs-lookup"><span data-stu-id="ad2df-111">For example, a typical business application may consist of client code running in web browsers, talking tooone or more web app services, which in turn use back end services.</span></span> <span data-ttu-id="ad2df-112">I componenti del server possono essere ospitato localmente nel cloud hello, potrebbero essere Azure ruoli web e di lavoro o possono essere eseguite in contenitori, ad esempio Docker o Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ad2df-112">Server components may be hosted on-premises on in hello cloud, or may be Azure web and worker roles, or may run in containers such as Docker or Service Fabric.</span></span> 

### <a name="sharing-a-single-application-insights-resource"></a><span data-ttu-id="ad2df-113">Condivisione di una singola risorsa di Application Insights</span><span class="sxs-lookup"><span data-stu-id="ad2df-113">Sharing a single Application Insights resource</span></span> 

<span data-ttu-id="ad2df-114">chiave tecnica qui Hello è telemetria toosend da ogni componente di toohello l'applicazione stessa risorsa di Application Insights, ma utilizzare hello `cloud_RoleName` componenti toodistinguish di proprietà quando necessario.</span><span class="sxs-lookup"><span data-stu-id="ad2df-114">hello key technique here is toosend telemetry from every component in your application toohello same Application Insights resource, but use hello `cloud_RoleName` property toodistinguish components when necessary.</span></span> <span data-ttu-id="ad2df-115">Hello Application Insights SDK aggiunge hello `cloud_RoleName` creare componenti di telemetria toohello di proprietà.</span><span class="sxs-lookup"><span data-stu-id="ad2df-115">hello Application Insights SDK adds hello `cloud_RoleName` property toohello telemetry components emit.</span></span> <span data-ttu-id="ad2df-116">Ad esempio, hello SDK si aggiungerà un nome del sito web o servizio ruolo nome toohello `cloud_RoleName` proprietà.</span><span class="sxs-lookup"><span data-stu-id="ad2df-116">For example, hello SDK will add a web site name, or service role name toohello `cloud_RoleName` property.</span></span> <span data-ttu-id="ad2df-117">È possibile eseguire l'override di questo valore con un Telemetryinitializer.</span><span class="sxs-lookup"><span data-stu-id="ad2df-117">You can override this value with a telemetryinitializer.</span></span> <span data-ttu-id="ad2df-118">Hello mappa delle applicazioni utilizza hello `cloud_RoleName` componenti hello tooidentify di proprietà sulla mappa hello.</span><span class="sxs-lookup"><span data-stu-id="ad2df-118">hello Application Map uses hello `cloud_RoleName` property tooidentify hello components on hello map.</span></span>

<span data-ttu-id="ad2df-119">Per ulteriori informazioni su come eseguire l'override hello `cloud_RoleName` vedere proprietà [aggiungere proprietà: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).</span><span class="sxs-lookup"><span data-stu-id="ad2df-119">For more information about how do override hello `cloud_RoleName` property see [Add properties: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).</span></span>  

<span data-ttu-id="ad2df-120">In alcuni casi, ciò potrebbe non essere appropriato e potrebbe essere preferibile toouse risorse diverse per diversi gruppi di componenti.</span><span class="sxs-lookup"><span data-stu-id="ad2df-120">In some cases, this may not be appropriate, and you may prefer toouse separate resources for different groups of components.</span></span> <span data-ttu-id="ad2df-121">È ad esempio, potrebbe essere necessario toouse diverse risorse per la gestione o ai fini della fatturazione.</span><span class="sxs-lookup"><span data-stu-id="ad2df-121">For example, you might need toouse different resources for management or billing purposes.</span></span> <span data-ttu-id="ad2df-122">Utilizzo di risorse separate significa che non viene visualizzato tutti i componenti di hello visualizzati in un singolo mapping di applicazioni; e che è possibile eseguire query tra componenti [Analitica](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="ad2df-122">Using separate resources means that you don't see all hello components displayed on a single Application Map; and that you can't query across components in [Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="ad2df-123">È inoltre possibile tooset delle risorse separato hello.</span><span class="sxs-lookup"><span data-stu-id="ad2df-123">You also have tooset up hello separate resources.</span></span>

<span data-ttu-id="ad2df-124">Con tale problema, si presupporrà che il resto di hello di questo documento che si desidera toosend dati da più componenti tooone risorsa di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ad2df-124">With that caveat, we'll assume in hello rest of this document that you want toosend data from multiple components tooone Application Insights resource.</span></span>

## <a name="configure-multi-component-applications"></a><span data-ttu-id="ad2df-125">Configurare le applicazioni multi-componente</span><span class="sxs-lookup"><span data-stu-id="ad2df-125">Configure multi-component applications</span></span>

<span data-ttu-id="ad2df-126">eseguire il mapping di un'applicazione con più componente tooget, è necessario tooachieve questi obiettivi:</span><span class="sxs-lookup"><span data-stu-id="ad2df-126">tooget a multi-component application map, you need tooachieve these goals:</span></span>

* <span data-ttu-id="ad2df-127">**Installare la versione precedente più recente di hello** pacchetto Application Insights in ogni componente dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="ad2df-127">**Install hello latest pre-release** Application Insights package in each component of hello application.</span></span> 
* <span data-ttu-id="ad2df-128">**Condividere una singola risorsa di Application Insights** per tutti i componenti dell'applicazione di hello.</span><span class="sxs-lookup"><span data-stu-id="ad2df-128">**Share a single Application Insights resource** for all hello components of your application.</span></span>
* <span data-ttu-id="ad2df-129">**Abilitare multi-ruolo applicazione mappa** nel Pannello di anteprime hello.</span><span class="sxs-lookup"><span data-stu-id="ad2df-129">**Enable Multi-role Application Map** in hello Previews blade.</span></span>

<span data-ttu-id="ad2df-130">Configurare ogni componente dell'applicazione metodo hello appropriato per il relativo tipo.</span><span class="sxs-lookup"><span data-stu-id="ad2df-130">Configure each component of your application using hello appropriate method for its type.</span></span> <span data-ttu-id="ad2df-131">([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md).)</span><span class="sxs-lookup"><span data-stu-id="ad2df-131">([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md).)</span></span>

### <a name="1-install-hello-latest-pre-release-package"></a><span data-ttu-id="ad2df-132">1. Installare il pacchetto di pre-release più recente di hello</span><span class="sxs-lookup"><span data-stu-id="ad2df-132">1. Install hello latest pre-release package</span></span>

<span data-ttu-id="ad2df-133">Aggiornare o installare i pacchetti hello Application Insights nel progetto hello per ogni componente.</span><span class="sxs-lookup"><span data-stu-id="ad2df-133">Update or install hello Appication Insights packages in hello project for each server component.</span></span> <span data-ttu-id="ad2df-134">Se si usa Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="ad2df-134">If you're using Visual Studio:</span></span>

1. <span data-ttu-id="ad2df-135">Fare clic con il pulsante destro del mouse sul progetto e selezionare **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="ad2df-135">Right-click a project and select **Manage NuGet Packages**.</span></span> 
2. <span data-ttu-id="ad2df-136">Selezionare **Includi versione preliminare**.</span><span class="sxs-lookup"><span data-stu-id="ad2df-136">Select **Include prerelease**.</span></span>
3. <span data-ttu-id="ad2df-137">Se i pacchetti di Application Insights vengono visualizzati negli aggiornamenti, selezionarli.</span><span class="sxs-lookup"><span data-stu-id="ad2df-137">If Application Insights packages appear in Updates, select them.</span></span> 

    <span data-ttu-id="ad2df-138">In caso contrario, individuare e installare il pacchetto appropriato hello:</span><span class="sxs-lookup"><span data-stu-id="ad2df-138">Otherwise, browse for and install hello appropriate package:</span></span>
    
    * <span data-ttu-id="ad2df-139">Microsoft.ApplicationInsights.WindowsServer</span><span class="sxs-lookup"><span data-stu-id="ad2df-139">Microsoft.ApplicationInsights.WindowsServer</span></span>
    * <span data-ttu-id="ad2df-140">Microsoft.ApplicationInsights.ServiceFabric - per componenti in esecuzione come file eseguibili guest e contenitori Docker in esecuzione nell'applicazione Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ad2df-140">Microsoft.ApplicationInsights.ServiceFabric - for components running as guest executables and Docker containers running a in Service Fabric application</span></span>
    * <span data-ttu-id="ad2df-141">Microsoft.ApplicationInsights.ServiceFabric.Native - per reliable services nelle applicazioni di ServiceFabric</span><span class="sxs-lookup"><span data-stu-id="ad2df-141">Microsoft.ApplicationInsights.ServiceFabric.Native - for reliable services in ServiceFabric applications</span></span>
    * <span data-ttu-id="ad2df-142">Microsoft.ApplicationInsights.Kubernetes per i componenti in esecuzione in Docker su Kubernetes</span><span class="sxs-lookup"><span data-stu-id="ad2df-142">Microsoft.ApplicationInsights.Kubernetes for components running in Docker on Kubernetes</span></span>

### <a name="2-share-a-single-application-insights-resource"></a><span data-ttu-id="ad2df-143">2. Condividere una singola risorsa di Application Insights</span><span class="sxs-lookup"><span data-stu-id="ad2df-143">2. Share a single Application Insights resource</span></span>

* <span data-ttu-id="ad2df-144">In Visual Studio fare clic con il pulsante destro del mouse sul progetto e selezionare **Configura Application Insights** oppure **Application Insights > Configurare**.</span><span class="sxs-lookup"><span data-stu-id="ad2df-144">In Visual Studio, right-click a project and select **Configure Application Insights**, or **Application Insights > Configure**.</span></span> <span data-ttu-id="ad2df-145">Per il progetto prima di hello, utilizzare hello guidata toocreate una risorsa di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ad2df-145">For hello first project, use hello wizard toocreate an Application Insights resource.</span></span> <span data-ttu-id="ad2df-146">Per i progetti successivi, selezionare hello stessa risorsa.</span><span class="sxs-lookup"><span data-stu-id="ad2df-146">For subsequent projects, select hello same resource.</span></span>
* <span data-ttu-id="ad2df-147">Se non è presente alcun menu di Application Insights, configurare manualmente:</span><span class="sxs-lookup"><span data-stu-id="ad2df-147">If there is no Application Insights menu, configure manually:</span></span>

   1. <span data-ttu-id="ad2df-148">In [portale di Azure](https://portal,azure.com), aprire una risorsa di Application Insights hello già stato creato per un altro componente.</span><span class="sxs-lookup"><span data-stu-id="ad2df-148">In [Azure portal](https://portal,azure.com), open hello Application Insights resource you already created for another component.</span></span>
   2. <span data-ttu-id="ad2df-149">Nel pannello della panoramica hello, scheda hello Apri menu a discesa Essentials e hello copia **chiave di strumentazione.**</span><span class="sxs-lookup"><span data-stu-id="ad2df-149">In hello Overview blade, open hello Essentials drop-down tab, and copy hello **Instrumentation Key.**</span></span>
   3. <span data-ttu-id="ad2df-150">Nel progetto aprire ApplicationInsights.config e inserire:`<InstrumentationKey>your copied key</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="ad2df-150">In your project, open ApplicationInsights.config and insert: `<InstrumentationKey>your copied key</InstrumentationKey>`</span></span>

![Copiare i file con estensione config hello strumentazione toohello chiave](./media/app-insights-monitor-multi-role-apps/copy-instrumentation-key.png)


### <a name="3-enable-multi-role-application-map"></a><span data-ttu-id="ad2df-152">3. Abilitare la Mappa delle applicazioni multiruolo</span><span class="sxs-lookup"><span data-stu-id="ad2df-152">3. Enable multi-role Application Map</span></span>

<span data-ttu-id="ad2df-153">Nel portale di Azure hello, aprire la risorsa hello per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ad2df-153">In hello Azure portal, open hello resource for your application.</span></span> <span data-ttu-id="ad2df-154">Nel Pannello di anteprime hello, abilitare *con più ruoli applicazione mappa*.</span><span class="sxs-lookup"><span data-stu-id="ad2df-154">In hello Previews blade, enable *Multi-role Application Map*.</span></span>

### <a name="4-enable-docker-metrics-optional"></a><span data-ttu-id="ad2df-155">4. Abilitare la metrica di Docker (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="ad2df-155">4. Enable Docker metrics (Optional)</span></span> 

<span data-ttu-id="ad2df-156">Se un componente viene eseguito una Docker ospitata in una macchina virtuale Windows Azure, è possibile raccogliere metriche aggiuntive dal contenitore hello.</span><span class="sxs-lookup"><span data-stu-id="ad2df-156">If a component runs in a Docker hosted on an Azure Windows VM, you can collect additional metrics from hello container.</span></span> <span data-ttu-id="ad2df-157">Inserire nel file di configurazione di [Diagnostica di Azure](../monitoring-and-diagnostics/azure-diagnostics.md):</span><span class="sxs-lookup"><span data-stu-id="ad2df-157">Insert this in your [Azure diagnostics](../monitoring-and-diagnostics/azure-diagnostics.md) configuration file:</span></span>

```
"DiagnosticMonitorConfiguration": {
        ...
        "sinks": "applicationInsights",
        "DockerSources": {
                "Stats": {
                    "enabled": true,
                    "sampleRate": "PT1M"
                }
            },
        ...
    }
    ...   
    "SinksConfig": {
        "Sink": [{
            "name": "applicationInsights",
            "ApplicationInsights": "<your instrumentation key here>"
        }]
    }
    ...
}

```

## <a name="use-cloudrolename-tooseparate-components"></a><span data-ttu-id="ad2df-158">Utilizzare i componenti tooseparate cloud_RoleName</span><span class="sxs-lookup"><span data-stu-id="ad2df-158">Use cloud_RoleName tooseparate components</span></span>

<span data-ttu-id="ad2df-159">Hello `cloud_RoleName` proprietà è telemetria tooall associata.</span><span class="sxs-lookup"><span data-stu-id="ad2df-159">hello `cloud_RoleName` property is attached tooall telemetry.</span></span> <span data-ttu-id="ad2df-160">Identifica un componente hello - ruolo hello o un servizio, che ha origine dati di telemetria hello.</span><span class="sxs-lookup"><span data-stu-id="ad2df-160">It identifies hello component - hello role or service - that originates hello telemetry.</span></span> <span data-ttu-id="ad2df-161">(È non hello stesso come cloud_RoleInstance, che separa identici ruoli che sono in esecuzione in parallelo in più processi del server o computer).</span><span class="sxs-lookup"><span data-stu-id="ad2df-161">(It is not hello same as cloud_RoleInstance, which separates identical roles that are running in parallel on multiple server processes or machines.)</span></span>

<span data-ttu-id="ad2df-162">Nel portale di hello, è possibile filtrare o segmento di dati di telemetria utilizzando questa proprietà.</span><span class="sxs-lookup"><span data-stu-id="ad2df-162">In hello portal, you can filter or segment your telemetry using this property.</span></span> <span data-ttu-id="ad2df-163">In questo esempio, pannello errori hello è filtrato tooshow informazioni solo dal servizio web front-end hello, filtrando gli errori di back-end CRM API hello:</span><span class="sxs-lookup"><span data-stu-id="ad2df-163">In this example, hello Failures blade is filtered tooshow just information from hello front-end web service, filtering out failures from hello CRM API backend:</span></span>

![Grafico della metrica segmentata in base al nome del ruolo Cloud](./media/app-insights-monitor-multi-role-apps/cloud-role-name.png)

## <a name="trace-operations-between-components"></a><span data-ttu-id="ad2df-165">Tracciare le operazioni tra i componenti</span><span class="sxs-lookup"><span data-stu-id="ad2df-165">Trace operations between components</span></span>

<span data-ttu-id="ad2df-166">È possibile tracciare da un componente tooanother, chiamate hello effettuate durante l'elaborazione di una singola operazione.</span><span class="sxs-lookup"><span data-stu-id="ad2df-166">You can trace from one component tooanother, hello calls made while processing an individual operation.</span></span>


![Mostrare i dati di telemetria per operazione](./media/app-insights-monitor-multi-role-apps/show-telemetry-for-operation.png)

<span data-ttu-id="ad2df-168">Fare clic su server web front-end hello e API back-end hello tooa elenco correlato di dati di telemetria per questa operazione:</span><span class="sxs-lookup"><span data-stu-id="ad2df-168">Click through tooa correlated list of telemetry for this operation across hello front-end web server and hello back-end API:</span></span>

![Ricerca tra i componenti](./media/app-insights-monitor-multi-role-apps/search-across-components.png)


## <a name="next-steps"></a><span data-ttu-id="ad2df-170">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ad2df-170">Next steps</span></span>

* [<span data-ttu-id="ad2df-171">Separare la telemetria da sviluppo, test e produzione</span><span class="sxs-lookup"><span data-stu-id="ad2df-171">Separate telemetry from Development, Test, and Production</span></span>](app-insights-separate-resources.md)
