---
title: aaaFix 502 gateway non valido, 503 Servizio non disponibili errori | Documenti Microsoft
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
ms.openlocfilehash: d9d8dcddaac930967a2e8d2bfd8cad09e6824c17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-http-errors-of-502-bad-gateway-and-503-service-unavailable-in-your-azure-web-apps"></a><span data-ttu-id="16bc2-104">Risolvere gli errori HTTP "502 - Gateway non valido" e "503 - Servizio non disponibile" nelle App Web di Azure</span><span class="sxs-lookup"><span data-stu-id="16bc2-104">Troubleshoot HTTP errors of "502 bad gateway" and "503 service unavailable" in your Azure web apps</span></span>
<span data-ttu-id="16bc2-105">Gli errori "502 - Gateway non valido" e "503 - Servizio non disponibile" sono comuni nelle applicazioni Web ospitate in un [Servizio app di Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="16bc2-105">"502 bad gateway" and "503 service unavailable" are common errors in your web app hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="16bc2-106">Questo articolo fornisce informazioni utili per la risoluzione di questi errori.</span><span class="sxs-lookup"><span data-stu-id="16bc2-106">This article helps you troubleshoot these errors.</span></span>

<span data-ttu-id="16bc2-107">Se è necessario ulteriore assistenza in qualsiasi punto in questo articolo, è possibile contattare hello Azure esperti in [hello MSDN di Azure e forum di Overflow dello Stack di hello](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="16bc2-107">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and hello Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="16bc2-108">In alternativa, è anche possibile archiviare un evento imprevisto di supporto tecnico di Azure.</span><span class="sxs-lookup"><span data-stu-id="16bc2-108">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="16bc2-109">Passare toohello [sito del supporto tecnico di Azure](https://azure.microsoft.com/support/options/) e fare clic su **supporto**.</span><span class="sxs-lookup"><span data-stu-id="16bc2-109">Go toohello [Azure Support site](https://azure.microsoft.com/support/options/) and click on **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="16bc2-110">Sintomo</span><span class="sxs-lookup"><span data-stu-id="16bc2-110">Symptom</span></span>
<span data-ttu-id="16bc2-111">Quando si passa toohello web app, viene restituito un HTTP un HTTP o errore "502 Gateway non valido" errore "503 Servizio non disponibile".</span><span class="sxs-lookup"><span data-stu-id="16bc2-111">When you browse toohello web app, it returns a HTTP "502 Bad Gateway" error or a HTTP "503 Service Unavailable" error.</span></span>

## <a name="cause"></a><span data-ttu-id="16bc2-112">Causa</span><span class="sxs-lookup"><span data-stu-id="16bc2-112">Cause</span></span>
<span data-ttu-id="16bc2-113">Spesso la causa dell'errore deriva da problemi a livello dell'applicazione, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="16bc2-113">This problem is often caused by application level issues, such as:</span></span>

* <span data-ttu-id="16bc2-114">le richieste impiegano troppo tempo</span><span class="sxs-lookup"><span data-stu-id="16bc2-114">requests taking a long time</span></span>
* <span data-ttu-id="16bc2-115">utilizzo elevato di memoria/CPU da parte dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="16bc2-115">application using high memory/CPU</span></span>
* <span data-ttu-id="16bc2-116">applicazione di un arresto anomalo a causa di eccezione tooan.</span><span class="sxs-lookup"><span data-stu-id="16bc2-116">application crashing due tooan exception.</span></span>

## <a name="troubleshooting-steps-toosolve-502-bad-gateway-and-503-service-unavailable-errors"></a><span data-ttu-id="16bc2-117">Risoluzione dei problemi relativi a operazioni toosolve "502 gateway non valido" e gli errori di "503 Servizio non disponibile"</span><span class="sxs-lookup"><span data-stu-id="16bc2-117">Troubleshooting steps toosolve "502 bad gateway" and "503 service unavailable" errors</span></span>
<span data-ttu-id="16bc2-118">La risoluzione dei problemi prevede tre attività distinte, in ordine sequenziale:</span><span class="sxs-lookup"><span data-stu-id="16bc2-118">Troubleshooting can be divided into three distinct tasks, in sequential order:</span></span>

1. [<span data-ttu-id="16bc2-119">Osservare e monitorare il comportamento dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="16bc2-119">Observe and monitor application behavior</span></span>](#observe)
2. [<span data-ttu-id="16bc2-120">Raccogliere i dati</span><span class="sxs-lookup"><span data-stu-id="16bc2-120">Collect data</span></span>](#collect)
3. [<span data-ttu-id="16bc2-121">Limitare i problemi di hello</span><span class="sxs-lookup"><span data-stu-id="16bc2-121">Mitigate hello issue</span></span>](#mitigate)

<span data-ttu-id="16bc2-122">[app Web del servizio app](/services/app-service/web/) vengono presentate diverse opzioni per ogni passaggio.</span><span class="sxs-lookup"><span data-stu-id="16bc2-122">[App Service Web Apps](/services/app-service/web/) gives you various options at each step.</span></span>

<a name="observe" />

### <a name="1-observe-and-monitor-application-behavior"></a><span data-ttu-id="16bc2-123">1. Osservare e monitorare il comportamento dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="16bc2-123">1. Observe and monitor application behavior</span></span>
#### <a name="track-service-health"></a><span data-ttu-id="16bc2-124">Tenere traccia dell'integrità del servizio</span><span class="sxs-lookup"><span data-stu-id="16bc2-124">Track Service health</span></span>
<span data-ttu-id="16bc2-125">Microsoft Azure pubblica un annuncio ogni volta che si verifica un'interruzione del servizio o una riduzione delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="16bc2-125">Microsoft Azure publicizes each time there is a service interruption or performance degradation.</span></span> <span data-ttu-id="16bc2-126">È possibile tenere traccia dello stato di hello del servizio hello in hello [portale Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="16bc2-126">You can track hello health of hello service on hello [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="16bc2-127">Per altre informazioni, vedere [Tenere traccia dell’integrità del servizio](../monitoring-and-diagnostics/insights-service-health.md).</span><span class="sxs-lookup"><span data-stu-id="16bc2-127">For more information, see [Track service health](../monitoring-and-diagnostics/insights-service-health.md).</span></span>

#### <a name="monitor-your-web-app"></a><span data-ttu-id="16bc2-128">Monitorare l'app Web</span><span class="sxs-lookup"><span data-stu-id="16bc2-128">Monitor your web app</span></span>
<span data-ttu-id="16bc2-129">Questa opzione consente toofind out dell'applicazione in caso di eventuali problemi.</span><span class="sxs-lookup"><span data-stu-id="16bc2-129">This option enables you toofind out if your application is having any issues.</span></span> <span data-ttu-id="16bc2-130">Nel pannello dell'app web, fare clic su hello **richieste ed errori** riquadro.</span><span class="sxs-lookup"><span data-stu-id="16bc2-130">In your web app’s blade, click hello **Requests and errors** tile.</span></span> <span data-ttu-id="16bc2-131">Hello **metrica** pannello è visualizzate tutte le metriche di hello è possibile aggiungere.</span><span class="sxs-lookup"><span data-stu-id="16bc2-131">hello **Metric** blade will show you all hello metrics you can add.</span></span>

<span data-ttu-id="16bc2-132">Sono riportate alcune delle metriche hello che potrebbe essere toomonitor per l'app web</span><span class="sxs-lookup"><span data-stu-id="16bc2-132">Some of hello metrics that you might want toomonitor for your web app are</span></span>

* <span data-ttu-id="16bc2-133">Working set della memoria medio</span><span class="sxs-lookup"><span data-stu-id="16bc2-133">Average memory working set</span></span>
* <span data-ttu-id="16bc2-134">Tempo di risposta medio</span><span class="sxs-lookup"><span data-stu-id="16bc2-134">Average response time</span></span>
* <span data-ttu-id="16bc2-135">Tempo CPU</span><span class="sxs-lookup"><span data-stu-id="16bc2-135">CPU time</span></span>
* <span data-ttu-id="16bc2-136">Working set della memoria</span><span class="sxs-lookup"><span data-stu-id="16bc2-136">Memory working set</span></span>
* <span data-ttu-id="16bc2-137">Richieste</span><span class="sxs-lookup"><span data-stu-id="16bc2-137">Requests</span></span>

![monitorare le app Web per risolvere gli errori HTTP "502 - Gateway non valido" e "503 - Servizio non disponibile"](./media/app-service-web-troubleshoot-HTTP-502-503/1-monitor-metrics.png)

<span data-ttu-id="16bc2-139">Per altre informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="16bc2-139">For more information, see:</span></span>

* [<span data-ttu-id="16bc2-140">Eseguire il monitoraggio delle app Web nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="16bc2-140">Monitor Web Apps in Azure App Service</span></span>](web-sites-monitor.md)
* [<span data-ttu-id="16bc2-141">Ricevere notifiche di avviso</span><span class="sxs-lookup"><span data-stu-id="16bc2-141">Receive alert notifications</span></span>](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

<a name="collect" />

### <a name="2-collect-data"></a><span data-ttu-id="16bc2-142">2. Raccogliere i dati</span><span class="sxs-lookup"><span data-stu-id="16bc2-142">2. Collect data</span></span>
#### <a name="use-hello-azure-app-service-support-portal"></a><span data-ttu-id="16bc2-143">Utilizzare hello portale di supporto del servizio App di Azure</span><span class="sxs-lookup"><span data-stu-id="16bc2-143">Use hello Azure App Service Support Portal</span></span>
<span data-ttu-id="16bc2-144">App Web fornisce hello possibilità tootroubleshoot problemi correlati tooyour web app esaminando HTTP log, i registri eventi, i dump del processo e altro.</span><span class="sxs-lookup"><span data-stu-id="16bc2-144">Web Apps provides you with hello ability tootroubleshoot issues related tooyour web app by looking at HTTP logs, event logs, process dumps, and more.</span></span> <span data-ttu-id="16bc2-145">È possibile accedere a tutte queste informazioni tramite il portale di supporto disponibile all'indirizzo **http://&lt;nome app>.scm.azurewebsites.net/Support**</span><span class="sxs-lookup"><span data-stu-id="16bc2-145">You can access all this information using our Support portal at **http://&lt;your app name>.scm.azurewebsites.net/Support**</span></span>

<span data-ttu-id="16bc2-146">portale di Azure App Service supportano Hello offre tre schede separate toosupport hello tre passaggi di uno scenario di risoluzione dei problemi più comune:</span><span class="sxs-lookup"><span data-stu-id="16bc2-146">hello Azure App Service Support portal provides you with three separate tabs toosupport hello three steps of a common troubleshooting scenario:</span></span>

1. <span data-ttu-id="16bc2-147">Osservare il comportamento corrente</span><span class="sxs-lookup"><span data-stu-id="16bc2-147">Observe current behavior</span></span>
2. <span data-ttu-id="16bc2-148">Analizzare la raccolta di informazioni di diagnostica ed eseguendo hello analizzatori incorporati</span><span class="sxs-lookup"><span data-stu-id="16bc2-148">Analyze by collecting diagnostics information and running hello built-in analyzers</span></span>
3. <span data-ttu-id="16bc2-149">Attenuare il problema</span><span class="sxs-lookup"><span data-stu-id="16bc2-149">Mitigate</span></span>

<span data-ttu-id="16bc2-150">Se il problema di hello è in corso al momento, fare clic su **Analizza** > **diagnostica** > **diagnosticare ora** toocreate una sessione di diagnostica, che verranno raccolti HTTP registra, Visualizzatore eventi, memoria dump, log degli errori PHP e PHP report viene elaborato.</span><span class="sxs-lookup"><span data-stu-id="16bc2-150">If hello issue is happening right now, click **Analyze** > **Diagnostics** > **Diagnose Now** toocreate a diagnostic session for you, which will collect HTTP logs, event viewer logs, memory dumps, PHP error logs and PHP process report.</span></span>

<span data-ttu-id="16bc2-151">Una volta raccolti i dati di hello, inoltre, verranno eseguire un'analisi sui dati hello e fornire un rapporto HTML.</span><span class="sxs-lookup"><span data-stu-id="16bc2-151">Once hello data is collected, it will also run an analysis on hello data and provide you with an HTML report.</span></span>

<span data-ttu-id="16bc2-152">Nel caso in cui si desiderano i dati di hello toodownload, per impostazione predefinita, potrebbe essere archiviato nella cartella D:\home\data\DaaS hello.</span><span class="sxs-lookup"><span data-stu-id="16bc2-152">In case you want toodownload hello data, by default, it would be stored in hello D:\home\data\DaaS folder.</span></span>

<span data-ttu-id="16bc2-153">Per ulteriori informazioni sul portale di Azure App Service supportano hello, vedere [tooSupport nuovi aggiornamenti estensione del sito per siti Web di Azure](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).</span><span class="sxs-lookup"><span data-stu-id="16bc2-153">For more information on hello Azure App Service Support portal, see [New Updates tooSupport Site Extension for Azure Websites](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).</span></span>

#### <a name="use-hello-kudu-debug-console"></a><span data-ttu-id="16bc2-154">Utilizzare hello Kudu Console di Debug</span><span class="sxs-lookup"><span data-stu-id="16bc2-154">Use hello Kudu Debug Console</span></span>
<span data-ttu-id="16bc2-155">Il servizio App Web include una console di debug che è possibile usare per il debug, l'esplorazione e il caricamento di file, nonché endpoint JSON per ottenere informazioni sull'ambiente in uso.</span><span class="sxs-lookup"><span data-stu-id="16bc2-155">Web Apps comes with a debug console that you can use for debugging, exploring, uploading files, as well as JSON endpoints for getting information about your environment.</span></span> <span data-ttu-id="16bc2-156">Si tratta di hello *Kudu Console* o hello *Dashboard SCM* per l'app web.</span><span class="sxs-lookup"><span data-stu-id="16bc2-156">This is called hello *Kudu Console* or hello *SCM Dashboard* for your web app.</span></span>

<span data-ttu-id="16bc2-157">È possibile accedere a questo dashboard per passare toohello collegamento **https://&lt;nome dell'app >.scm.azurewebsites.net/**.</span><span class="sxs-lookup"><span data-stu-id="16bc2-157">You can access this dashboard by going toohello link **https://&lt;Your app name>.scm.azurewebsites.net/**.</span></span>

<span data-ttu-id="16bc2-158">Sono riportate alcune delle operazioni hello Kudu offre:</span><span class="sxs-lookup"><span data-stu-id="16bc2-158">Some of hello things that Kudu provides are:</span></span>

* <span data-ttu-id="16bc2-159">impostazioni di ambiente per l'applicazione</span><span class="sxs-lookup"><span data-stu-id="16bc2-159">environment settings for your application</span></span>
* <span data-ttu-id="16bc2-160">log in streaming</span><span class="sxs-lookup"><span data-stu-id="16bc2-160">log stream</span></span>
* <span data-ttu-id="16bc2-161">dump di diagnostica</span><span class="sxs-lookup"><span data-stu-id="16bc2-161">diagnostic dump</span></span>
* <span data-ttu-id="16bc2-162">console di debug in cui è possibile eseguire cmdlet di PowerShell e comandi DOS di base.</span><span class="sxs-lookup"><span data-stu-id="16bc2-162">debug console in which you can run Powershell cmdlets and basic DOS commands.</span></span>

<span data-ttu-id="16bc2-163">Un'altra caratteristica utile di Kudu è che, nel caso in cui l'applicazione è la generazione di eccezioni first-chance, è possibile utilizzare Kudu e dump della memoria di hello SysInternals strumento Procdump toocreate.</span><span class="sxs-lookup"><span data-stu-id="16bc2-163">Another useful feature of Kudu is that, in case your application is throwing first-chance exceptions, you can use Kudu and hello SysInternals tool Procdump toocreate memory dumps.</span></span> <span data-ttu-id="16bc2-164">Le immagini della memoria sono snapshot dei processo hello e spesso consentono di risolvere i problemi più complessi con l'app web.</span><span class="sxs-lookup"><span data-stu-id="16bc2-164">These memory dumps are snapshots of hello process and can often help you troubleshoot more complicated issues with your web app.</span></span>

<span data-ttu-id="16bc2-165">Per altre informazioni sulle funzionalità disponibili in Kudu, vedere il post di blog relativo agli [strumenti online di Siti Web di Azure che è opportuno conoscere](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).</span><span class="sxs-lookup"><span data-stu-id="16bc2-165">For more information on features available in Kudu, see [Azure Websites online tools you should know about](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).</span></span>

<a name="mitigate" />

### <a name="3-mitigate-hello-issue"></a><span data-ttu-id="16bc2-166">3. Limitare i problemi di hello</span><span class="sxs-lookup"><span data-stu-id="16bc2-166">3. Mitigate hello issue</span></span>
#### <a name="scale-hello-web-app"></a><span data-ttu-id="16bc2-167">Scala hello web app</span><span class="sxs-lookup"><span data-stu-id="16bc2-167">Scale hello web app</span></span>
<span data-ttu-id="16bc2-168">In Azure App Service, per migliorare le prestazioni e velocità effettiva, è possibile modificare la scala hello in corrispondenza del quale si esegue l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="16bc2-168">In Azure App Service, for increased performance and throughput,  you can adjust hello scale at which you are running your application.</span></span> <span data-ttu-id="16bc2-169">La scalabilità verticale un'app web prevede due azioni correlate: modifica il maggiore livello di prezzo e la configurazione di determinate impostazioni dopo avere impostato toohello maggiore livello di prezzo tooa di piano di servizio App.</span><span class="sxs-lookup"><span data-stu-id="16bc2-169">Scaling up a web app involves two related actions: changing your App Service plan tooa higher pricing tier, and configuring certain settings after you have switched toohello higher pricing tier.</span></span>

<span data-ttu-id="16bc2-170">Per altre informazioni sul ridimensionamento, vedere [Ridimensionare un'app Web nel servizio app di Azure](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="16bc2-170">For more information on scaling, see [Scale a web app in Azure App Service](web-sites-scale.md).</span></span>

<span data-ttu-id="16bc2-171">Inoltre, è possibile scegliere toorun l'applicazione in più di un'istanza.</span><span class="sxs-lookup"><span data-stu-id="16bc2-171">Additionally, you can choose toorun your application on more than one instance .</span></span> <span data-ttu-id="16bc2-172">In questo modo, non solo si ottiene una maggiore capacità di elaborazione, ma si può usufruire della tolleranza di errore.</span><span class="sxs-lookup"><span data-stu-id="16bc2-172">This not only provides you with more processing capability, but also gives you some amount of fault tolerance.</span></span> <span data-ttu-id="16bc2-173">Se hello processo diventa inattivo in un'istanza, hello altra istanza verrà comunque continuare risposta alle richieste.</span><span class="sxs-lookup"><span data-stu-id="16bc2-173">If hello process goes down on one instance, hello other instance will still continue serving requests.</span></span>

<span data-ttu-id="16bc2-174">È possibile impostare hello scalabilità toobe manuale o automatico.</span><span class="sxs-lookup"><span data-stu-id="16bc2-174">You can set hello scaling toobe Manual or Automatic.</span></span>

#### <a name="use-autoheal"></a><span data-ttu-id="16bc2-175">Usare la funzionalità AutoHeal</span><span class="sxs-lookup"><span data-stu-id="16bc2-175">Use AutoHeal</span></span>
<span data-ttu-id="16bc2-176">AutoHeal Ricicla il processo di lavoro hello per l'app in base alle impostazioni selezionate (ad esempio, è necessario tooexecute una richiesta di modifiche alla configurazione, le richieste, basata sulla memoria limiti o il tempo di hello).</span><span class="sxs-lookup"><span data-stu-id="16bc2-176">AutoHeal recycles hello worker process for your app based on settings you choose (like configuration changes, requests, memory-based limits, or hello time needed tooexecute a request).</span></span> <span data-ttu-id="16bc2-177">La maggior parte dei casi hello Ricicla i processi di hello sono toorecover modo più veloce di hello da un problema.</span><span class="sxs-lookup"><span data-stu-id="16bc2-177">Most of hello time, recycle hello process is hello fastest way toorecover from a problem.</span></span> <span data-ttu-id="16bc2-178">Anche se è sempre possibile riavviare un'app web hello da direttamente in hello portale di Azure, AutoHeal per l'esecuzione automatica per l'utente.</span><span class="sxs-lookup"><span data-stu-id="16bc2-178">Though you can always restart hello web app from directly within hello Azure Portal, AutoHeal will do it automatically for you.</span></span> <span data-ttu-id="16bc2-179">È sufficiente toodo aggiungere alcuni trigger in Web. config radice hello per le app web.</span><span class="sxs-lookup"><span data-stu-id="16bc2-179">All you need toodo is add some triggers in hello root web.config for your web app.</span></span> <span data-ttu-id="16bc2-180">Si noti che queste impostazioni funzionerà in hello stesso modo, anche se l'applicazione non è di tipo .net uno.</span><span class="sxs-lookup"><span data-stu-id="16bc2-180">Note that these settings would work in hello same way even if your application is not a .Net one.</span></span>

<span data-ttu-id="16bc2-181">Per altre informazioni, vedere il post di blog relativo alla [correzione automatica di Siti Web di Azure](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).</span><span class="sxs-lookup"><span data-stu-id="16bc2-181">For more information, see [Auto-Healing Azure Web Sites](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).</span></span>

#### <a name="restart-hello-web-app"></a><span data-ttu-id="16bc2-182">Riavviare l'app web hello</span><span class="sxs-lookup"><span data-stu-id="16bc2-182">Restart hello web app</span></span>
<span data-ttu-id="16bc2-183">Questo è spesso toorecover modo più semplice di hello da problemi occasionali.</span><span class="sxs-lookup"><span data-stu-id="16bc2-183">This is often hello simplest way toorecover from one-time issues.</span></span> <span data-ttu-id="16bc2-184">In hello [portale Azure](https://portal.azure.com/), nel pannello dell'app web, si dispone di hello opzioni toostop o riavviare l'app.</span><span class="sxs-lookup"><span data-stu-id="16bc2-184">On hello [Azure Portal](https://portal.azure.com/), on your web app’s blade, you have hello options toostop or restart your app.</span></span>

 ![riavviare gli errori di app toosolve HTTP 502 gateway non valido e 503 Servizio non disponibile](./media/app-service-web-troubleshoot-HTTP-502-503/2-restart.png)

<span data-ttu-id="16bc2-186">È anche possibile gestire l'app Web usando Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="16bc2-186">You can also manage your web app using Azure Powershell.</span></span> <span data-ttu-id="16bc2-187">Per altre informazioni, vedere [Uso di Azure PowerShell con Gestione risorse di Azure](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="16bc2-187">For more information, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

