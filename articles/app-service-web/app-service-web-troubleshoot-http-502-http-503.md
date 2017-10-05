---
title: Correggere gli errori "502 - Gateway non valido" e "503 - Servizio non disponibile"| Documentazione Microsoft
description: Risoluzione degli errori "502 - Gateway non valido" e "503 - Servizio non disponibile" nelle app Web ospitate in un servizio App di Azure.
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: top-support-issue
keywords: 502 - Gateway non valido, 503 - Servizio non disponibile, errore 503, errore 502
ms.assetid: 51cd331a-a3fa-438f-90ef-385e755e50d5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: 397a6aaf7dc27adfa0fc0e722b8a2be5cc1d75f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-http-errors-of-502-bad-gateway-and-503-service-unavailable-in-your-azure-web-apps"></a><span data-ttu-id="1d7ec-104">Risolvere gli errori HTTP "502 - Gateway non valido" e "503 - Servizio non disponibile" nelle App Web di Azure</span><span class="sxs-lookup"><span data-stu-id="1d7ec-104">Troubleshoot HTTP errors of "502 bad gateway" and "503 service unavailable" in your Azure web apps</span></span>
<span data-ttu-id="1d7ec-105">Gli errori "502 - Gateway non valido" e "503 - Servizio non disponibile" sono comuni nelle applicazioni Web ospitate in un [Servizio app di Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="1d7ec-105">"502 bad gateway" and "503 service unavailable" are common errors in your web app hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="1d7ec-106">Questo articolo fornisce informazioni utili per la risoluzione di questi errori.</span><span class="sxs-lookup"><span data-stu-id="1d7ec-106">This article helps you troubleshoot these errors.</span></span>

<span data-ttu-id="1d7ec-107">Se in qualsiasi punto dell'articolo sono necessarie altre informazioni, è possibile contattare gli esperti di Azure nei [forum MSDN e overflow dello stack relativi ad Azure](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="1d7ec-107">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and the Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="1d7ec-108">In alternativa, è anche possibile archiviare un evento imprevisto di supporto tecnico di Azure.</span><span class="sxs-lookup"><span data-stu-id="1d7ec-108">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="1d7ec-109">Passare al [sito di supporto per Azure](https://azure.microsoft.com/support/options/) e fare clic su **Ottenere supporto**.</span><span class="sxs-lookup"><span data-stu-id="1d7ec-109">Go to the [Azure Support site](https://azure.microsoft.com/support/options/) and click on **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="1d7ec-110">Sintomo</span><span class="sxs-lookup"><span data-stu-id="1d7ec-110">Symptom</span></span>
<span data-ttu-id="1d7ec-111">Quando si passa all'app Web, viene restituito un errore HTTP "502 - Gateway non valido" o HTTP "503 - Servizio non disponibile".</span><span class="sxs-lookup"><span data-stu-id="1d7ec-111">When you browse to the web app, it returns a HTTP "502 Bad Gateway" error or a HTTP "503 Service Unavailable" error.</span></span>

## <a name="cause"></a><span data-ttu-id="1d7ec-112">Causa</span><span class="sxs-lookup"><span data-stu-id="1d7ec-112">Cause</span></span>
<span data-ttu-id="1d7ec-113">Spesso la causa dell'errore deriva da problemi a livello dell'applicazione, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="1d7ec-113">This problem is often caused by application level issues, such as:</span></span>

* <span data-ttu-id="1d7ec-114">le richieste impiegano troppo tempo</span><span class="sxs-lookup"><span data-stu-id="1d7ec-114">requests taking a long time</span></span>
* <span data-ttu-id="1d7ec-115">utilizzo elevato di memoria/CPU da parte dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="1d7ec-115">application using high memory/CPU</span></span>
* <span data-ttu-id="1d7ec-116">arresto anomalo dell'applicazione a causa di un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="1d7ec-116">application crashing due to an exception.</span></span>

## <a name="troubleshooting-steps-to-solve-502-bad-gateway-and-503-service-unavailable-errors"></a><span data-ttu-id="1d7ec-117">Passaggi per la risoluzione degli errori "503 - Servizio non disponibile" e "502 - Gateway non valido"</span><span class="sxs-lookup"><span data-stu-id="1d7ec-117">Troubleshooting steps to solve "502 bad gateway" and "503 service unavailable" errors</span></span>
<span data-ttu-id="1d7ec-118">La risoluzione dei problemi prevede tre attività distinte, in ordine sequenziale:</span><span class="sxs-lookup"><span data-stu-id="1d7ec-118">Troubleshooting can be divided into three distinct tasks, in sequential order:</span></span>

1. [<span data-ttu-id="1d7ec-119">Osservare e monitorare il comportamento dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="1d7ec-119">Observe and monitor application behavior</span></span>](#observe)
2. [<span data-ttu-id="1d7ec-120">Raccogliere i dati</span><span class="sxs-lookup"><span data-stu-id="1d7ec-120">Collect data</span></span>](#collect)
3. [<span data-ttu-id="1d7ec-121">Attenuare il problema</span><span class="sxs-lookup"><span data-stu-id="1d7ec-121">Mitigate the issue</span></span>](#mitigate)

<span data-ttu-id="1d7ec-122">[app Web del servizio app](/services/app-service/web/) vengono presentate diverse opzioni per ogni passaggio.</span><span class="sxs-lookup"><span data-stu-id="1d7ec-122">[App Service Web Apps](/services/app-service/web/) gives you various options at each step.</span></span>

<a name="observe" />

### <a name="1-observe-and-monitor-application-behavior"></a><span data-ttu-id="1d7ec-123">1. Osservare e monitorare il comportamento dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="1d7ec-123">1. Observe and monitor application behavior</span></span>
#### <a name="track-service-health"></a><span data-ttu-id="1d7ec-124">Tenere traccia dell'integrità del servizio</span><span class="sxs-lookup"><span data-stu-id="1d7ec-124">Track Service health</span></span>
<span data-ttu-id="1d7ec-125">Microsoft Azure pubblica un annuncio ogni volta che si verifica un'interruzione del servizio o una riduzione delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="1d7ec-125">Microsoft Azure publicizes each time there is a service interruption or performance degradation.</span></span> <span data-ttu-id="1d7ec-126">È possibile verificare l'integrità del servizio nel [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1d7ec-126">You can track the health of the service on the [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="1d7ec-127">Per altre informazioni, vedere [Tenere traccia dell’integrità del servizio](../monitoring-and-diagnostics/insights-service-health.md).</span><span class="sxs-lookup"><span data-stu-id="1d7ec-127">For more information, see [Track service health](../monitoring-and-diagnostics/insights-service-health.md).</span></span>

#### <a name="monitor-your-web-app"></a><span data-ttu-id="1d7ec-128">Monitorare l'app Web</span><span class="sxs-lookup"><span data-stu-id="1d7ec-128">Monitor your web app</span></span>
<span data-ttu-id="1d7ec-129">Questa opzione consente di trovare eventuali problemi nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1d7ec-129">This option enables you to find out if your application is having any issues.</span></span> <span data-ttu-id="1d7ec-130">Nel pannello dell'app Web fare clic sul riquadro **Richieste ed errori** .</span><span class="sxs-lookup"><span data-stu-id="1d7ec-130">In your web app’s blade, click the **Requests and errors** tile.</span></span> <span data-ttu-id="1d7ec-131">Il pannello **Metrica** mostra le metriche che si possono aggiungere.</span><span class="sxs-lookup"><span data-stu-id="1d7ec-131">The **Metric** blade will show you all the metrics you can add.</span></span>

<span data-ttu-id="1d7ec-132">Le metriche più comunemente monitorate per le app Web sono</span><span class="sxs-lookup"><span data-stu-id="1d7ec-132">Some of the metrics that you might want to monitor for your web app are</span></span>

* <span data-ttu-id="1d7ec-133">Working set della memoria medio</span><span class="sxs-lookup"><span data-stu-id="1d7ec-133">Average memory working set</span></span>
* <span data-ttu-id="1d7ec-134">Tempo di risposta medio</span><span class="sxs-lookup"><span data-stu-id="1d7ec-134">Average response time</span></span>
* <span data-ttu-id="1d7ec-135">Tempo CPU</span><span class="sxs-lookup"><span data-stu-id="1d7ec-135">CPU time</span></span>
* <span data-ttu-id="1d7ec-136">Working set della memoria</span><span class="sxs-lookup"><span data-stu-id="1d7ec-136">Memory working set</span></span>
* <span data-ttu-id="1d7ec-137">Richieste</span><span class="sxs-lookup"><span data-stu-id="1d7ec-137">Requests</span></span>

![monitorare le app Web per risolvere gli errori HTTP "502 - Gateway non valido" e "503 - Servizio non disponibile"](./media/app-service-web-troubleshoot-HTTP-502-503/1-monitor-metrics.png)

<span data-ttu-id="1d7ec-139">Per altre informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="1d7ec-139">For more information, see:</span></span>

* [<span data-ttu-id="1d7ec-140">Eseguire il monitoraggio delle app Web nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="1d7ec-140">Monitor Web Apps in Azure App Service</span></span>](web-sites-monitor.md)
* [<span data-ttu-id="1d7ec-141">Ricevere notifiche di avviso</span><span class="sxs-lookup"><span data-stu-id="1d7ec-141">Receive alert notifications</span></span>](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

<a name="collect" />

### <a name="2-collect-data"></a><span data-ttu-id="1d7ec-142">2. Raccogliere i dati</span><span class="sxs-lookup"><span data-stu-id="1d7ec-142">2. Collect data</span></span>
#### <a name="use-the-azure-app-service-support-portal"></a><span data-ttu-id="1d7ec-143">Usare il portale di supporto del servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="1d7ec-143">Use the Azure App Service Support Portal</span></span>
<span data-ttu-id="1d7ec-144">Il servizio app Web consente di risolvere i problemi relativi all'app Web grazie ai dati disponibili nei log HTTP, nei log eventi, nei dump dei processi e così via.</span><span class="sxs-lookup"><span data-stu-id="1d7ec-144">Web Apps provides you with the ability to troubleshoot issues related to your web app by looking at HTTP logs, event logs, process dumps, and more.</span></span> <span data-ttu-id="1d7ec-145">È possibile accedere a tutte queste informazioni tramite il portale di supporto disponibile all'indirizzo **http://&lt;nome app>.scm.azurewebsites.net/Support**</span><span class="sxs-lookup"><span data-stu-id="1d7ec-145">You can access all this information using our Support portal at **http://&lt;your app name>.scm.azurewebsites.net/Support**</span></span>

<span data-ttu-id="1d7ec-146">Il portale di supporto del servizio app di Azure contiene tre schede separate per supportare i tre passaggi di uno scenario di risoluzione dei problemi comune:</span><span class="sxs-lookup"><span data-stu-id="1d7ec-146">The Azure App Service Support portal provides you with three separate tabs to support the three steps of a common troubleshooting scenario:</span></span>

1. <span data-ttu-id="1d7ec-147">Osservare il comportamento corrente</span><span class="sxs-lookup"><span data-stu-id="1d7ec-147">Observe current behavior</span></span>
2. <span data-ttu-id="1d7ec-148">Eseguire l'analisi tramite la raccolta di informazioni di diagnostica e l'esecuzione di analizzatori predefiniti</span><span class="sxs-lookup"><span data-stu-id="1d7ec-148">Analyze by collecting diagnostics information and running the built-in analyzers</span></span>
3. <span data-ttu-id="1d7ec-149">Attenuare il problema</span><span class="sxs-lookup"><span data-stu-id="1d7ec-149">Mitigate</span></span>

<span data-ttu-id="1d7ec-150">Se si riscontra il problema in questo preciso istante, fare clic su **Analizza** > **Diagnostica** > **Esegui diagnosi adesso** per creare una sessione di diagnostica in cui verranno raccolti log HTTP, log del visualizzatore eventi, dump della memoria, log degli errori PHP e report sui processi PHP.</span><span class="sxs-lookup"><span data-stu-id="1d7ec-150">If the issue is happening right now, click **Analyze** > **Diagnostics** > **Diagnose Now** to create a diagnostic session for you, which will collect HTTP logs, event viewer logs, memory dumps, PHP error logs and PHP process report.</span></span>

<span data-ttu-id="1d7ec-151">Una volta raccolti i dati, verrà eseguita l'analisi dei dati e verrà generato un report HTML.</span><span class="sxs-lookup"><span data-stu-id="1d7ec-151">Once the data is collected, it will also run an analysis on the data and provide you with an HTML report.</span></span>

<span data-ttu-id="1d7ec-152">Per impostazione predefinita, i dati verranno archiviati nella cartella D:\home\data\DaaS, da cui sarà possibile scaricarli.</span><span class="sxs-lookup"><span data-stu-id="1d7ec-152">In case you want to download the data, by default, it would be stored in the D:\home\data\DaaS folder.</span></span>

<span data-ttu-id="1d7ec-153">Per altre informazioni sul portale di supporto del servizio app di Azure, vedere il post di blog relativo ai [nuovi aggiornamenti all'estensione del sito di supporto per Siti Web di Azure](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).</span><span class="sxs-lookup"><span data-stu-id="1d7ec-153">For more information on the Azure App Service Support portal, see [New Updates to Support Site Extension for Azure Websites](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).</span></span>

#### <a name="use-the-kudu-debug-console"></a><span data-ttu-id="1d7ec-154">Usare la console di debug Kudu</span><span class="sxs-lookup"><span data-stu-id="1d7ec-154">Use the Kudu Debug Console</span></span>
<span data-ttu-id="1d7ec-155">Il servizio App Web include una console di debug che è possibile usare per il debug, l'esplorazione e il caricamento di file, nonché endpoint JSON per ottenere informazioni sull'ambiente in uso.</span><span class="sxs-lookup"><span data-stu-id="1d7ec-155">Web Apps comes with a debug console that you can use for debugging, exploring, uploading files, as well as JSON endpoints for getting information about your environment.</span></span> <span data-ttu-id="1d7ec-156">Questa console è chiamata *console Kudu* o *dashboard SCM* dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="1d7ec-156">This is called the *Kudu Console* or the *SCM Dashboard* for your web app.</span></span>

<span data-ttu-id="1d7ec-157">È possibile accedere a questo dashboard selezionando il collegamento **https://&lt;nome app>.scm.azurewebsites.net/**.</span><span class="sxs-lookup"><span data-stu-id="1d7ec-157">You can access this dashboard by going to the link **https://&lt;Your app name>.scm.azurewebsites.net/**.</span></span>

<span data-ttu-id="1d7ec-158">Elementi forniti dalla console Kudu:</span><span class="sxs-lookup"><span data-stu-id="1d7ec-158">Some of the things that Kudu provides are:</span></span>

* <span data-ttu-id="1d7ec-159">impostazioni di ambiente per l'applicazione</span><span class="sxs-lookup"><span data-stu-id="1d7ec-159">environment settings for your application</span></span>
* <span data-ttu-id="1d7ec-160">log in streaming</span><span class="sxs-lookup"><span data-stu-id="1d7ec-160">log stream</span></span>
* <span data-ttu-id="1d7ec-161">dump di diagnostica</span><span class="sxs-lookup"><span data-stu-id="1d7ec-161">diagnostic dump</span></span>
* <span data-ttu-id="1d7ec-162">console di debug in cui è possibile eseguire cmdlet di PowerShell e comandi DOS di base.</span><span class="sxs-lookup"><span data-stu-id="1d7ec-162">debug console in which you can run Powershell cmdlets and basic DOS commands.</span></span>

<span data-ttu-id="1d7ec-163">Inoltre, nel caso in cui l'applicazione generi eccezioni first-chance, è possibile usare Kudu e l'utilità della riga di comando Procdump dello strumento SysInternals per creare dump della memoria.</span><span class="sxs-lookup"><span data-stu-id="1d7ec-163">Another useful feature of Kudu is that, in case your application is throwing first-chance exceptions, you can use Kudu and the SysInternals tool Procdump to create memory dumps.</span></span> <span data-ttu-id="1d7ec-164">I dump della memoria sono snapshot del processo e semplificano la risoluzione di problemi più complessi riscontrati nell'app Web.</span><span class="sxs-lookup"><span data-stu-id="1d7ec-164">These memory dumps are snapshots of the process and can often help you troubleshoot more complicated issues with your web app.</span></span>

<span data-ttu-id="1d7ec-165">Per altre informazioni sulle funzionalità disponibili in Kudu, vedere il post di blog relativo agli [strumenti online di Siti Web di Azure che è opportuno conoscere](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).</span><span class="sxs-lookup"><span data-stu-id="1d7ec-165">For more information on features available in Kudu, see [Azure Websites online tools you should know about](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).</span></span>

<a name="mitigate" />

### <a name="3-mitigate-the-issue"></a><span data-ttu-id="1d7ec-166">3. Attenuare il problema</span><span class="sxs-lookup"><span data-stu-id="1d7ec-166">3. Mitigate the issue</span></span>
#### <a name="scale-the-web-app"></a><span data-ttu-id="1d7ec-167">Ridimensionare l'app Web</span><span class="sxs-lookup"><span data-stu-id="1d7ec-167">Scale the web app</span></span>
<span data-ttu-id="1d7ec-168">Nel servizio app di Azure, per ottimizzare le prestazioni e la velocità effettiva è possibile modificare la scalabilità in cui è in esecuzione l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1d7ec-168">In Azure App Service, for increased performance and throughput,  you can adjust the scale at which you are running your application.</span></span> <span data-ttu-id="1d7ec-169">Ridimensionare un'app Web di Azure implica due azioni correlate: passare a un piano tariffario superiore e configurare determinate impostazioni una volta adottato il nuovo piano.</span><span class="sxs-lookup"><span data-stu-id="1d7ec-169">Scaling up a web app involves two related actions: changing your App Service plan to a higher pricing tier, and configuring certain settings after you have switched to the higher pricing tier.</span></span>

<span data-ttu-id="1d7ec-170">Per altre informazioni sul ridimensionamento, vedere [Ridimensionare un'app Web nel servizio app di Azure](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="1d7ec-170">For more information on scaling, see [Scale a web app in Azure App Service](web-sites-scale.md).</span></span>

<span data-ttu-id="1d7ec-171">È anche possibile scegliere di eseguire l'applicazione in più di un'istanza.</span><span class="sxs-lookup"><span data-stu-id="1d7ec-171">Additionally, you can choose to run your application on more than one instance .</span></span> <span data-ttu-id="1d7ec-172">In questo modo, non solo si ottiene una maggiore capacità di elaborazione, ma si può usufruire della tolleranza di errore.</span><span class="sxs-lookup"><span data-stu-id="1d7ec-172">This not only provides you with more processing capability, but also gives you some amount of fault tolerance.</span></span> <span data-ttu-id="1d7ec-173">Se il processo si arresta in un'istanza, l'altra istanza continuerà a gestire le richieste.</span><span class="sxs-lookup"><span data-stu-id="1d7ec-173">If the process goes down on one instance, the other instance will still continue serving requests.</span></span>

<span data-ttu-id="1d7ec-174">È possibile impostare il ridimensionamento manuale o automatico.</span><span class="sxs-lookup"><span data-stu-id="1d7ec-174">You can set the scaling to be Manual or Automatic.</span></span>

#### <a name="use-autoheal"></a><span data-ttu-id="1d7ec-175">Usare la funzionalità AutoHeal</span><span class="sxs-lookup"><span data-stu-id="1d7ec-175">Use AutoHeal</span></span>
<span data-ttu-id="1d7ec-176">La funzionalità AutoHeal consente di riciclare il processo di lavoro per l'app in base alle impostazioni specificate, ad esempio modifiche di configurazione, richieste, limiti basati sulla memoria o il tempo necessario per l'esecuzione di una richiesta.</span><span class="sxs-lookup"><span data-stu-id="1d7ec-176">AutoHeal recycles the worker process for your app based on settings you choose (like configuration changes, requests, memory-based limits, or the time needed to execute a request).</span></span> <span data-ttu-id="1d7ec-177">Nella maggior parte dei casi, riciclare il processo costituisce il modo più veloce per risolvere un problema.</span><span class="sxs-lookup"><span data-stu-id="1d7ec-177">Most of the time, recycle the process is the fastest way to recover from a problem.</span></span> <span data-ttu-id="1d7ec-178">Anche se è possibile riavviare l'app Web direttamente dall'interno del portale di Azure, la funzionalità AutoHeal eseguirà questa operazione automaticamente.</span><span class="sxs-lookup"><span data-stu-id="1d7ec-178">Though you can always restart the web app from directly within the Azure Portal, AutoHeal will do it automatically for you.</span></span> <span data-ttu-id="1d7ec-179">È sufficiente aggiungere alcuni trigger nel file web.config radice per l'app Web.</span><span class="sxs-lookup"><span data-stu-id="1d7ec-179">All you need to do is add some triggers in the root web.config for your web app.</span></span> <span data-ttu-id="1d7ec-180">Si noti che queste impostazioni funzionano allo stesso modo anche per le applicazioni non .NET.</span><span class="sxs-lookup"><span data-stu-id="1d7ec-180">Note that these settings would work in the same way even if your application is not a .Net one.</span></span>

<span data-ttu-id="1d7ec-181">Per altre informazioni, vedere il post di blog relativo alla [correzione automatica di Siti Web di Azure](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).</span><span class="sxs-lookup"><span data-stu-id="1d7ec-181">For more information, see [Auto-Healing Azure Web Sites](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).</span></span>

#### <a name="restart-the-web-app"></a><span data-ttu-id="1d7ec-182">Riavviare l'app Web</span><span class="sxs-lookup"><span data-stu-id="1d7ec-182">Restart the web app</span></span>
<span data-ttu-id="1d7ec-183">Questo è spesso il modo più semplice per risolvere problemi occasionali.</span><span class="sxs-lookup"><span data-stu-id="1d7ec-183">This is often the simplest way to recover from one-time issues.</span></span> <span data-ttu-id="1d7ec-184">Nel pannello dell'app Web del [portale di Azure](https://portal.azure.com/)sono disponibili le opzioni per arrestare o riavviare l'app.</span><span class="sxs-lookup"><span data-stu-id="1d7ec-184">On the [Azure Portal](https://portal.azure.com/), on your web app’s blade, you have the options to stop or restart your app.</span></span>

 ![riavviare l'app per risolvere gli errori HTTP "502 - Gateway non valido" e "503 - Servizio non disponibile"](./media/app-service-web-troubleshoot-HTTP-502-503/2-restart.png)

<span data-ttu-id="1d7ec-186">È anche possibile gestire l'app Web usando Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1d7ec-186">You can also manage your web app using Azure Powershell.</span></span> <span data-ttu-id="1d7ec-187">Per altre informazioni, vedere [Uso di Azure PowerShell con Gestione risorse di Azure](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="1d7ec-187">For more information, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

