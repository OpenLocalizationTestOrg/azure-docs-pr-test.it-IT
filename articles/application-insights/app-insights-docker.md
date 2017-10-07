---
title: applicazioni di aaaMonitor Docker in Azure Application Insights | Documenti Microsoft
description: Eccezioni, eventi e contatori delle prestazioni di docker possono essere visualizzate in Application Insights, insieme ai dati di telemetria hello da app hello contenitore.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 27a3083d-d67f-4a07-8f3c-4edb65a0a685
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 9aaf1076bae25485a396db1bb3dcd13bccd87c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-docker-applications-in-application-insights"></a><span data-ttu-id="b567c-103">Monitoraggio di applicazioni Docker in Application Insights</span><span class="sxs-lookup"><span data-stu-id="b567c-103">Monitor Docker applications in Application Insights</span></span>
<span data-ttu-id="b567c-104">I contatori delle prestazioni e degli eventi del ciclo di vita da contenitori [Docker](https://www.docker.com/) possono essere disegnati in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b567c-104">Lifecycle events and performance counters from [Docker](https://www.docker.com/) containers can be charted on Application Insights.</span></span> <span data-ttu-id="b567c-105">Installare hello [Application Insights](app-insights-overview.md) immagine in un contenitore dell'host e visualizzerà i contatori delle prestazioni per host hello, come anche di hello altre immagini.</span><span class="sxs-lookup"><span data-stu-id="b567c-105">Install hello [Application Insights](app-insights-overview.md) image in a container in your host, and it will display performance counters for hello host, as well as for hello other images.</span></span>

<span data-ttu-id="b567c-106">Con Docker si distribuiscono le app in contenitori leggeri completi di tutte le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="b567c-106">With Docker, you distribute your apps in lightweight containers complete with all dependencies.</span></span> <span data-ttu-id="b567c-107">Verranno eseguite su tutti i computer host che eseguono un motore Docker.</span><span class="sxs-lookup"><span data-stu-id="b567c-107">They'll run on any host machine that runs a Docker Engine.</span></span>

<span data-ttu-id="b567c-108">Quando si esegue hello [immagine di Application Insights](https://hub.docker.com/r/microsoft/applicationinsights/) sull'host Docker, si possono ottenere questi vantaggi:</span><span class="sxs-lookup"><span data-stu-id="b567c-108">When you run hello [Application Insights image](https://hub.docker.com/r/microsoft/applicationinsights/) on your Docker host, you get these benefits:</span></span>

* <span data-ttu-id="b567c-109">Dati di telemetria di ciclo di vita su tutti i contenitori di hello in esecuzione nell'host di hello - avviare, arrestare e così via.</span><span class="sxs-lookup"><span data-stu-id="b567c-109">Lifecycle telemetry about all hello containers running on hello host - start, stop, and so on.</span></span>
* <span data-ttu-id="b567c-110">Contatori delle prestazioni per tutti i contenitori di hello.</span><span class="sxs-lookup"><span data-stu-id="b567c-110">Performance counters for all hello containers.</span></span> <span data-ttu-id="b567c-111">CPU, memoria, utilizzo della rete e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="b567c-111">CPU, memory, network usage, and more.</span></span>
* <span data-ttu-id="b567c-112">Se si [installati Application Insights SDK per Java](app-insights-java-live.md) hello le App in esecuzione in contenitori hello, tutti i dati di telemetria hello di tali App hanno proprietà aggiuntive che identifica il contenitore di hello e computer host.</span><span class="sxs-lookup"><span data-stu-id="b567c-112">If you [installed Application Insights SDK for Java](app-insights-java-live.md) in hello apps running in hello containers, all hello telemetry of those apps will have additional properties identifying hello container and host machine.</span></span> <span data-ttu-id="b567c-113">Ad esempio, se si dispone di istanze di un'app in esecuzione in più host, è possibile filtrare facilmente dall'host i dati di telemetria dell'app.</span><span class="sxs-lookup"><span data-stu-id="b567c-113">So for example, if you have instances of an app running in more than one host, you can easily filter your app telemetry by host.</span></span>

![esempio](./media/app-insights-docker/00.png)

## <a name="set-up-your-application-insights-resource"></a><span data-ttu-id="b567c-115">Configurare la risorsa di Application Insights</span><span class="sxs-lookup"><span data-stu-id="b567c-115">Set up your Application Insights resource</span></span>
1. <span data-ttu-id="b567c-116">Accedere a [portale Microsoft Azure](https://azure.com) e aprire la risorsa di Application Insights hello per l'app; o [crearne uno nuovo](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="b567c-116">Sign into [Microsoft Azure portal](https://azure.com) and open hello Application Insights resource for your app; or [create a new one](app-insights-create-new-resource.md).</span></span> 
   
    <span data-ttu-id="b567c-117">*Quale risorsa si deve usare?*</span><span class="sxs-lookup"><span data-stu-id="b567c-117">*Which resource should I use?*</span></span> <span data-ttu-id="b567c-118">Se sono state sviluppate hello App in esecuzione sull'host da un altro utente, quindi è necessario troppo[creare una nuova risorsa di Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="b567c-118">If hello apps that you are running on your host were developed by someone else, then you need too[create a new Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="b567c-119">Si tratta in cui si consente di visualizzare e analizzare dati di telemetria hello.</span><span class="sxs-lookup"><span data-stu-id="b567c-119">This is where you view and analyze hello telemetry.</span></span> <span data-ttu-id="b567c-120">(Selezionare "Generale" per il tipo di app hello).</span><span class="sxs-lookup"><span data-stu-id="b567c-120">(Select 'General' for hello app type.)</span></span>
   
    <span data-ttu-id="b567c-121">Ma se lo sviluppatore di hello di hello App, quindi ci auguriamo che [aggiungere Application Insights SDK](app-insights-java-live.md) tooeach di essi.</span><span class="sxs-lookup"><span data-stu-id="b567c-121">But if you're hello developer of hello apps, then we hope you [added Application Insights SDK](app-insights-java-live.md) tooeach of them.</span></span> <span data-ttu-id="b567c-122">Se sono tutti effettivamente i componenti di un'applicazione di business, quindi è possibile configurare tutte le risorse di tooone toosend telemetria e si utilizzerà gli stessi risorsa toodisplay hello Docker ciclo di vita e delle prestazioni dati.</span><span class="sxs-lookup"><span data-stu-id="b567c-122">If they're all really components of a single business application, then you might configure all of them toosend telemetry tooone resource, and you'll use that same resource toodisplay hello Docker lifecycle and performance data.</span></span> 
   
    <span data-ttu-id="b567c-123">Un terzo scenario è che è stato sviluppato la maggior parte delle App hello, ma si utilizza risorse diverse toodisplay i dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="b567c-123">A third scenario is that you developed most of hello apps, but you are using separate resources toodisplay their telemetry.</span></span> <span data-ttu-id="b567c-124">In tal caso, è probabile che anche desidera toocreate una risorsa distinta per hello dati Docker.</span><span class="sxs-lookup"><span data-stu-id="b567c-124">In that case, you probably also want toocreate a separate resource for hello Docker data.</span></span> 
2. <span data-ttu-id="b567c-125">Aggiungi riquadro Docker di hello: scegliere **aggiungere riquadro**, trascinare il riquadro di Docker hello dalla raccolta di hello e quindi fare clic su **eseguita**.</span><span class="sxs-lookup"><span data-stu-id="b567c-125">Add hello Docker tile: Choose **Add Tile**, drag hello Docker tile from hello gallery, and then click **Done**.</span></span> 
   
    ![esempio](./media/app-insights-docker/03.png)
3. <span data-ttu-id="b567c-127">Fare clic su hello **Essentials** elenco a discesa e copiare hello chiave di strumentazione.</span><span class="sxs-lookup"><span data-stu-id="b567c-127">Click hello **Essentials** drop-down and copy hello Instrumentation Key.</span></span> <span data-ttu-id="b567c-128">Utilizzare questo hello tootell SDK in cui toosend la telemetria.</span><span class="sxs-lookup"><span data-stu-id="b567c-128">You use this tootell hello SDK where toosend its telemetry.</span></span>

    ![esempio](./media/app-insights-docker/02-props.png)

<span data-ttu-id="b567c-130">Mantenere la finestra del browser utili, come si ritornerà tooit appena toolook su dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="b567c-130">Keep that browser window handy, as you'll come back tooit soon toolook at your telemetry.</span></span>

## <a name="run-hello-application-insights-monitor-on-your-host"></a><span data-ttu-id="b567c-131">Esegui monitoraggio di Application Insights hello sull'host</span><span class="sxs-lookup"><span data-stu-id="b567c-131">Run hello Application Insights monitor on your host</span></span>
<span data-ttu-id="b567c-132">Ora che hai in un punto dati di telemetria hello toodisplay, è possibile impostare l'app nei contenitori hello che raccoglierà e inviarlo.</span><span class="sxs-lookup"><span data-stu-id="b567c-132">Now that you've got somewhere toodisplay hello telemetry, you can set up hello containerized app that will collect and send it.</span></span>

1. <span data-ttu-id="b567c-133">Connettere l'host Docker tooyour.</span><span class="sxs-lookup"><span data-stu-id="b567c-133">Connect tooyour Docker host.</span></span> 
2. <span data-ttu-id="b567c-134">Modificare la chiave di strumentazione in questo comando, e poi eseguirlo:</span><span class="sxs-lookup"><span data-stu-id="b567c-134">Edit your instrumentation key into this command, and then run it:</span></span>
   
   ```
   
   docker run -v /var/run/docker.sock:/docker.sock -d microsoft/applicationinsights ikey=000000-1111-2222-3333-444444444
   ```

<span data-ttu-id="b567c-135">Solo un'immagine di Application Insights è obbligatoria per ogni host Docker.</span><span class="sxs-lookup"><span data-stu-id="b567c-135">Only one Application Insights image is required per Docker host.</span></span> <span data-ttu-id="b567c-136">Se l'applicazione viene distribuita su più host Docker, quindi ripetere il comando di hello in ogni host.</span><span class="sxs-lookup"><span data-stu-id="b567c-136">If your application is deployed on multiple Docker hosts, then repeat hello command on every host.</span></span>

## <a name="update-your-app"></a><span data-ttu-id="b567c-137">Aggiornamento dell'app</span><span class="sxs-lookup"><span data-stu-id="b567c-137">Update your app</span></span>
<span data-ttu-id="b567c-138">Se l'applicazione è instrumentato con hello [Application Insights SDK per Java](app-insights-java-get-started.md), aggiungere hello seguente riga nel file ApplicationInsights.xml hello nel progetto, in hello `<TelemetryInitializers>` elemento:</span><span class="sxs-lookup"><span data-stu-id="b567c-138">If your application is instrumented with hello [Application Insights SDK for Java](app-insights-java-get-started.md), add hello following line into hello ApplicationInsights.xml file in your project, under hello `<TelemetryInitializers>` element:</span></span>

```xml

    <Add type="com.microsoft.applicationinsights.extensibility.initializer.docker.DockerContextInitializer"/> 
```

<span data-ttu-id="b567c-139">Aggiunge informazioni di Docker, ad esempio contenitore e host id tooevery telemetria item inviati dall'app.</span><span class="sxs-lookup"><span data-stu-id="b567c-139">This adds Docker information such as container and host id tooevery telemetry item sent from your app.</span></span>

## <a name="view-your-telemetry"></a><span data-ttu-id="b567c-140">Visualizzare i dati di telemetria</span><span class="sxs-lookup"><span data-stu-id="b567c-140">View your telemetry</span></span>
<span data-ttu-id="b567c-141">Tornare indietro di risorsa di Application Insights tooyour in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b567c-141">Go back tooyour Application Insights resource in hello Azure portal.</span></span>

<span data-ttu-id="b567c-142">Scorrere il riquadro di Docker hello.</span><span class="sxs-lookup"><span data-stu-id="b567c-142">Click through hello Docker tile.</span></span>

<span data-ttu-id="b567c-143">Si noterà subito dati provenienti da app Docker hello, soprattutto se si dispone di altri contenitori in esecuzione nel motore di Docker.</span><span class="sxs-lookup"><span data-stu-id="b567c-143">You'll shortly see data arriving from hello Docker app, especially if you have other containers running on your Docker engine.</span></span>

<span data-ttu-id="b567c-144">Ecco alcune delle viste hello che è possibile ottenere.</span><span class="sxs-lookup"><span data-stu-id="b567c-144">Here are some of hello views you can get.</span></span>

### <a name="perf-counters-by-host-activity-by-image"></a><span data-ttu-id="b567c-145">Contatori delle prestazioni per host, attività per immagine</span><span class="sxs-lookup"><span data-stu-id="b567c-145">Perf counters by host, activity by image</span></span>
![esempio](./media/app-insights-docker/10.png)

![esempio](./media/app-insights-docker/11.png)

<span data-ttu-id="b567c-148">Fare clic su un nome dell’host o dell’immagine per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="b567c-148">Click any host or image name for more detail.</span></span>

<span data-ttu-id="b567c-149">visualizzazione di hello toocustomize, fare clic su qualsiasi grafico, l'intestazione della griglia di hello oppure utilizzare Aggiungi grafico.</span><span class="sxs-lookup"><span data-stu-id="b567c-149">toocustomize hello view, click any chart, hello grid heading, or use Add Chart.</span></span> 

<span data-ttu-id="b567c-150">[Altre informazioni su Esplora metriche](app-insights-metrics-explorer.md)</span><span class="sxs-lookup"><span data-stu-id="b567c-150">[Learn more about metrics explorer](app-insights-metrics-explorer.md).</span></span>

### <a name="docker-container-events"></a><span data-ttu-id="b567c-151">Eventi del contenitore Docker</span><span class="sxs-lookup"><span data-stu-id="b567c-151">Docker container events</span></span>
![esempio](./media/app-insights-docker/13.png)

<span data-ttu-id="b567c-153">tooinvestigate singoli eventi, fare clic su [ricerca](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="b567c-153">tooinvestigate individual events, click [Search](app-insights-diagnostic-search.md).</span></span> <span data-ttu-id="b567c-154">Ricerca e filtro toofind hello eventi desiderati.</span><span class="sxs-lookup"><span data-stu-id="b567c-154">Search and filter toofind hello events you want.</span></span> <span data-ttu-id="b567c-155">Fare clic su qualsiasi tooget evento maggiori dettagli.</span><span class="sxs-lookup"><span data-stu-id="b567c-155">Click any event tooget more detail.</span></span>

### <a name="exceptions-by-container-name"></a><span data-ttu-id="b567c-156">Eccezioni per nome del contenitore</span><span class="sxs-lookup"><span data-stu-id="b567c-156">Exceptions by container name</span></span>
![esempio](./media/app-insights-docker/14.png)

### <a name="docker-context-added-tooapp-telemetry"></a><span data-ttu-id="b567c-158">Il contesto di docker aggiunto tooapp telemetria</span><span class="sxs-lookup"><span data-stu-id="b567c-158">Docker context added tooapp telemetry</span></span>
<span data-ttu-id="b567c-159">Telemetria di richiesta inviato da un'applicazione hello instrumentata con AI SDK, sono stati arricchiti con contesto Docker:</span><span class="sxs-lookup"><span data-stu-id="b567c-159">Request telemetry sent from hello application instrumented with AI SDK, enriched with Docker context:</span></span>

![esempio](./media/app-insights-docker/16.png)

<span data-ttu-id="b567c-161">Tempo di elaborazione e contatori delle prestazioni di memoria disponibile, arricchiti e raggruppati per nome del contenitore Docker:</span><span class="sxs-lookup"><span data-stu-id="b567c-161">Processor time and available memory performance counters, enriched and grouped by Docker container name:</span></span>

![esempio](./media/app-insights-docker/15.png)

## <a name="q--a"></a><span data-ttu-id="b567c-163">Domande e risposte</span><span class="sxs-lookup"><span data-stu-id="b567c-163">Q & A</span></span>
<span data-ttu-id="b567c-164">*Quali sono i vantaggi di Application Insights rispetto a Docker?*</span><span class="sxs-lookup"><span data-stu-id="b567c-164">*What does Application Insights give me that I can't get from Docker?*</span></span>

* <span data-ttu-id="b567c-165">Suddivisione dettagliata dei contatori delle prestazioni in base al contenitore e all'immagine.</span><span class="sxs-lookup"><span data-stu-id="b567c-165">Detailed breakdown of performance counters by container and image.</span></span>
* <span data-ttu-id="b567c-166">Integrazione dei dati dell'app e dei contenitori in un unico dashboard.</span><span class="sxs-lookup"><span data-stu-id="b567c-166">Integrate container and app data in one dashboard.</span></span>
* <span data-ttu-id="b567c-167">[Esportare i dati di telemetria](app-insights-export-telemetry.md) per database di tooa ulteriore analisi, Power BI o altri dashboard.</span><span class="sxs-lookup"><span data-stu-id="b567c-167">[Export telemetry](app-insights-export-telemetry.md) for further analysis tooa database, Power BI or other dashboard.</span></span>

<span data-ttu-id="b567c-168">*Come ottenere dati di telemetria da app hello stessa?*</span><span class="sxs-lookup"><span data-stu-id="b567c-168">*How do I get telemetry from hello app itself?*</span></span>

* <span data-ttu-id="b567c-169">Installare Application Insights SDK hello hello app.</span><span class="sxs-lookup"><span data-stu-id="b567c-169">Install hello Application Insights SDK in hello app.</span></span> <span data-ttu-id="b567c-170">Per informazioni, vedere [App Web Java](app-insights-java-get-started.md) e [App Web Windows](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="b567c-170">Learn how for: [Java web apps](app-insights-java-get-started.md), [Windows web apps](app-insights-asp-net.md).</span></span>

## <a name="video"></a><span data-ttu-id="b567c-171">Video</span><span class="sxs-lookup"><span data-stu-id="b567c-171">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="b567c-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b567c-172">Next steps</span></span>

* [<span data-ttu-id="b567c-173">Application Insights per Java</span><span class="sxs-lookup"><span data-stu-id="b567c-173">Application Insights for Java</span></span>](app-insights-java-get-started.md)
* [<span data-ttu-id="b567c-174">Application Insights per Node.js</span><span class="sxs-lookup"><span data-stu-id="b567c-174">Application Insights for Node.js</span></span>](app-insights-nodejs.md)
* [<span data-ttu-id="b567c-175">Application Insights per ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b567c-175">Application Insights for ASP.NET</span></span>](app-insights-asp-net.md)
