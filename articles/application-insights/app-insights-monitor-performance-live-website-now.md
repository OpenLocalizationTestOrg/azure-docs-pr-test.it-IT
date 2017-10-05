---
title: Monitorare un'app Web ASP.NET live con Azure Application Insights | Microsoft Docs
description: "Monitorare le prestazioni di un sito Web senza ripetere la distribuzione. Questa funzionalità può essere usata con app Web ASP.NET ospitate in locale, in macchine virtuali o in Azure."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 769a5ea4-a8c6-4c18-b46c-657e864e24de
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: d07a0c81f89100c378456bbea8dca1c009cc8d77
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="instrument-web-apps-at-runtime-with-application-insights"></a><span data-ttu-id="7d3a0-104">Instrumentare app Web in fase di esecuzione con Application Insights</span><span class="sxs-lookup"><span data-stu-id="7d3a0-104">Instrument web apps at runtime with Application Insights</span></span>


<span data-ttu-id="7d3a0-105">È possibile instrumentare un'app Web attiva con Azure Application Insights senza dover modificare o ridistribuire il codice.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-105">You can instrument a live web app with Azure Application Insights, without having to modify or redeploy your code.</span></span> <span data-ttu-id="7d3a0-106">Se le applicazioni sono ospitate da un server IIS locale, installare Status Monitor.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-106">If your apps are hosted by an on-premises IIS server, install Status Monitor.</span></span> <span data-ttu-id="7d3a0-107">Se si tratta di app Web di Azure o vengono eseguite in una macchina virtuale di Azure, è possibile attivare il monitoraggio di Application Insights dal pannello di controllo di Azure.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-107">If they're Azure web apps or run in an Azure VM, you can switch on Application Insights monitoring from the Azure control panel.</span></span> <span data-ttu-id="7d3a0-108">Sono disponibili anche articoli separati sulla strumentazione di [app Web J2EE live](app-insights-java-live.md) e [Servizi cloud di Azure](app-insights-cloudservices.md). È necessaria una sottoscrizione di [Microsoft Azure](http://azure.com) .</span><span class="sxs-lookup"><span data-stu-id="7d3a0-108">(There are also separate articles about instrumenting [live J2EE web apps](app-insights-java-live.md) and [Azure Cloud Services](app-insights-cloudservices.md).) You need a [Microsoft Azure](http://azure.com) subscription.</span></span>

![grafici di esempio](./media/app-insights-monitor-performance-live-website-now/10-intro.png)

<span data-ttu-id="7d3a0-110">È possibile scegliere di applicare Application Insights alle applicazioni Web .NET in tre modi:</span><span class="sxs-lookup"><span data-stu-id="7d3a0-110">You have a choice of three routes to apply Application Insights to your .NET web applications:</span></span>

* <span data-ttu-id="7d3a0-111">**Fase di compilazione:** [aggiungere Application Insights SDK][greenbrown] al codice dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-111">**Build time:** [Add the Application Insights SDK][greenbrown] to your web app code.</span></span>
* <span data-ttu-id="7d3a0-112">**Fase di esecuzione:** instrumentare l'app Web sul server, come descritto di seguito, senza ricompilare e ridistribuire il codice.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-112">**Run time:** Instrument your web app on the server, as described below, without rebuilding and redeploying the code.</span></span>
* <span data-ttu-id="7d3a0-113">**Entrambe le opzioni:** compilare l'SDK nel codice dell'app Web e applicare anche le estensioni della fase di esecuzione,</span><span class="sxs-lookup"><span data-stu-id="7d3a0-113">**Both:** Build the SDK into your web app code, and also apply the run-time extensions.</span></span> <span data-ttu-id="7d3a0-114">sfruttando il meglio delle due opzioni.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-114">Get the best of both options.</span></span>

<span data-ttu-id="7d3a0-115">Ecco un riepilogo di ciò che offrono i singoli modi:</span><span class="sxs-lookup"><span data-stu-id="7d3a0-115">Here's a summary of what you get by each route:</span></span>

|  | <span data-ttu-id="7d3a0-116">Fase di compilazione</span><span class="sxs-lookup"><span data-stu-id="7d3a0-116">Build time</span></span> | <span data-ttu-id="7d3a0-117">Fase di esecuzione</span><span class="sxs-lookup"><span data-stu-id="7d3a0-117">Run time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7d3a0-118">Richieste ed eccezioni</span><span class="sxs-lookup"><span data-stu-id="7d3a0-118">Requests & exceptions</span></span> |<span data-ttu-id="7d3a0-119">Sì</span><span class="sxs-lookup"><span data-stu-id="7d3a0-119">Yes</span></span> |<span data-ttu-id="7d3a0-120">Sì</span><span class="sxs-lookup"><span data-stu-id="7d3a0-120">Yes</span></span> |
| [<span data-ttu-id="7d3a0-121">Eccezioni più dettagliate</span><span class="sxs-lookup"><span data-stu-id="7d3a0-121">More detailed exceptions</span></span>](app-insights-asp-net-exceptions.md) | |<span data-ttu-id="7d3a0-122">Sì</span><span class="sxs-lookup"><span data-stu-id="7d3a0-122">Yes</span></span> |
| [<span data-ttu-id="7d3a0-123">Diagnostica delle dipendenze</span><span class="sxs-lookup"><span data-stu-id="7d3a0-123">Dependency diagnostics</span></span>](app-insights-asp-net-dependencies.md) |<span data-ttu-id="7d3a0-124">In .NET 4.6 e versioni successive, ma meno dettagli</span><span class="sxs-lookup"><span data-stu-id="7d3a0-124">On .NET 4.6+, but less detail</span></span> |<span data-ttu-id="7d3a0-125">Sì, dettagli completi: codici risultato, testo del comando SQL, verbo HTTP</span><span class="sxs-lookup"><span data-stu-id="7d3a0-125">Yes, full detail: result codes, SQL command text, HTTP verb</span></span>|
| [<span data-ttu-id="7d3a0-126">Contatori delle prestazioni di sistema</span><span class="sxs-lookup"><span data-stu-id="7d3a0-126">System performance counters</span></span>](app-insights-performance-counters.md) |<span data-ttu-id="7d3a0-127">Sì</span><span class="sxs-lookup"><span data-stu-id="7d3a0-127">Yes</span></span> |<span data-ttu-id="7d3a0-128">Sì</span><span class="sxs-lookup"><span data-stu-id="7d3a0-128">Yes</span></span> |
| <span data-ttu-id="7d3a0-129">[API per telemetria personalizzata][api]</span><span class="sxs-lookup"><span data-stu-id="7d3a0-129">[API for custom telemetry][api]</span></span> |<span data-ttu-id="7d3a0-130">Sì</span><span class="sxs-lookup"><span data-stu-id="7d3a0-130">Yes</span></span> |<span data-ttu-id="7d3a0-131">No</span><span class="sxs-lookup"><span data-stu-id="7d3a0-131">No</span></span> |
| [<span data-ttu-id="7d3a0-132">Integrazione log di traccia</span><span class="sxs-lookup"><span data-stu-id="7d3a0-132">Trace log integration</span></span>](app-insights-asp-net-trace-logs.md) |<span data-ttu-id="7d3a0-133">Sì</span><span class="sxs-lookup"><span data-stu-id="7d3a0-133">Yes</span></span> |<span data-ttu-id="7d3a0-134">No</span><span class="sxs-lookup"><span data-stu-id="7d3a0-134">No</span></span> |
| [<span data-ttu-id="7d3a0-135">Visualizzazione pagina e dati utente</span><span class="sxs-lookup"><span data-stu-id="7d3a0-135">Page view & user data</span></span>](app-insights-javascript.md) |<span data-ttu-id="7d3a0-136">Sì</span><span class="sxs-lookup"><span data-stu-id="7d3a0-136">Yes</span></span> |<span data-ttu-id="7d3a0-137">No</span><span class="sxs-lookup"><span data-stu-id="7d3a0-137">No</span></span> |
| <span data-ttu-id="7d3a0-138">Ricompilazione del codice necessaria</span><span class="sxs-lookup"><span data-stu-id="7d3a0-138">Need to rebuild code</span></span> |<span data-ttu-id="7d3a0-139">Sì</span><span class="sxs-lookup"><span data-stu-id="7d3a0-139">Yes</span></span> | <span data-ttu-id="7d3a0-140">No</span><span class="sxs-lookup"><span data-stu-id="7d3a0-140">No</span></span> |


## <a name="monitor-a-live-azure-web-app"></a><span data-ttu-id="7d3a0-141">Monitorare un'app Web live di Azure</span><span class="sxs-lookup"><span data-stu-id="7d3a0-141">Monitor a live Azure web app</span></span>

<span data-ttu-id="7d3a0-142">Se l'applicazione è in esecuzione come servizio Web di Azure, ecco come attivare il monitoraggio:</span><span class="sxs-lookup"><span data-stu-id="7d3a0-142">If your application is running as an Azure web service, here's how to switch on monitoring:</span></span>

* <span data-ttu-id="7d3a0-143">Selezionare Application Insights nel pannello di controllo dell'app in Azure.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-143">Select Application Insights on the app's control panel in Azure.</span></span>

    ![Configurare Application Insights per un'app Web di Azure](./media/app-insights-monitor-performance-live-website-now/azure-web-setup.png)
* <span data-ttu-id="7d3a0-145">Quando viene visualizzata la pagina di riepilogo di Application Insights, fare clic sul collegamento nella parte inferiore per aprire la risorsa completa di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-145">When the Application Insights summary page opens, click the link at the bottom to open the full Application Insights resource.</span></span>

    ![Fare clic sulle opzioni disponibili fino ad Application Insights](./media/app-insights-monitor-performance-live-website-now/azure-web-view-more.png)

<span data-ttu-id="7d3a0-147">[Monitoraggio di app cloud e VM](app-insights-azure.md).</span><span class="sxs-lookup"><span data-stu-id="7d3a0-147">[Monitoring Cloud and VM apps](app-insights-azure.md).</span></span>

### <a name="enable-client-side-monitoring-in-azure"></a><span data-ttu-id="7d3a0-148">Abilitare il monitoraggio lato client in Azure</span><span class="sxs-lookup"><span data-stu-id="7d3a0-148">Enable client-side monitoring in Azure</span></span>

<span data-ttu-id="7d3a0-149">Se è stato abilitato Application Insights in Azure, è possibile aggiungere la visualizzazione delle pagine e la telemetria utente.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-149">If you have enabled Application Insights in Azure, you can add page view and user telemetry.</span></span>

1. <span data-ttu-id="7d3a0-150">Selezionare Impostazioni > Impostazioni applicazione</span><span class="sxs-lookup"><span data-stu-id="7d3a0-150">Select Settings > Application Settings</span></span>
2.  <span data-ttu-id="7d3a0-151">In Impostazioni app aggiungere una nuova coppia chiave-valore:</span><span class="sxs-lookup"><span data-stu-id="7d3a0-151">Under App Settings, add a new key value pair:</span></span> 
   
    <span data-ttu-id="7d3a0-152">Chiave: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span><span class="sxs-lookup"><span data-stu-id="7d3a0-152">Key: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span></span> 
    
    <span data-ttu-id="7d3a0-153">Valore: `true`</span><span class="sxs-lookup"><span data-stu-id="7d3a0-153">Value: `true`</span></span>
3. <span data-ttu-id="7d3a0-154">Salvare le impostazioni scegliendo **Salva** e quindi fare clic su **Riavvia** per riavviare l'app.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-154">**Save** the settings and **Restart** your app.</span></span>

<span data-ttu-id="7d3a0-155">Application Insights JavaScript SDK è ora incluso in ogni pagina Web.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-155">The Application Insights JavaScript SDK is now injected into each web page.</span></span>

## <a name="monitor-a-live-iis-web-app"></a><span data-ttu-id="7d3a0-156">Monitorare un'app Web live di IIS</span><span class="sxs-lookup"><span data-stu-id="7d3a0-156">Monitor a live IIS web app</span></span>

<span data-ttu-id="7d3a0-157">Se l'app è ospitata in un server IIS, abilitare Application Insights usando Status Monitor.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-157">If your app is hosted on an IIS server, enable Application Insights by using Status Monitor.</span></span>

1. <span data-ttu-id="7d3a0-158">Nel server Web IIS accedere con le credenziali di amministratore.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-158">On your IIS web server, sign in with administrator credentials.</span></span>
2. <span data-ttu-id="7d3a0-159">Se Application Insights Status Monitor non è già installato, scaricare ed eseguire il [programma di installazione di Status Monitor](http://go.microsoft.com/fwlink/?LinkId=506648) oppure eseguire l'[Installazione guidata piattaforma Web](https://www.microsoft.com/web/downloads/platform.aspx) e cercarvi Application Insights Status Monitor.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-159">If Application Insights Status Monitor is not already installed, download and run the [Status Monitor installer](http://go.microsoft.com/fwlink/?LinkId=506648) (or run [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) and search in it for Application Insights Status Monitor).</span></span>
3. <span data-ttu-id="7d3a0-160">In Status Monitor selezionare l'applicazione Web installata o il sito Web da monitorare.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-160">In Status Monitor, select the installed web application or website that you want to monitor.</span></span> <span data-ttu-id="7d3a0-161">Accedere con le credenziali di Azure.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-161">Sign in with your Azure credentials.</span></span>

    <span data-ttu-id="7d3a0-162">Configurare la risorsa in cui si vogliono visualizzare i risultati nel portale di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-162">Configure the resource where you want to see the results in the Application Insights portal.</span></span> <span data-ttu-id="7d3a0-163">È in genere consigliabile creare una nuova risorsa.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-163">(Normally, it's best to create a new resource.</span></span> <span data-ttu-id="7d3a0-164">Selezionare una risorsa esistente se sono già disponibili [test Web][availability] o il [monitoraggio del client][client] per questa app.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-164">Select an existing resource if you already have [web tests][availability] or [client monitoring][client] for this app.)</span></span> 

    ![Scegliere un'applicazione e una risorsa.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-configAIC.png)

4. <span data-ttu-id="7d3a0-166">Riavviare IIS.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-166">Restart IIS.</span></span>

    ![Scegliere Riavvia nella parte superiore della finestra di dialogo.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-restart.png)

    <span data-ttu-id="7d3a0-168">Il servizio Web viene interrotto per un breve periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-168">Your web service is interrupted for a short while.</span></span>

## <a name="customize-monitoring-options"></a><span data-ttu-id="7d3a0-169">Personalizzare le opzioni di monitoraggio</span><span class="sxs-lookup"><span data-stu-id="7d3a0-169">Customize monitoring options</span></span>

<span data-ttu-id="7d3a0-170">L'abilitazione di Application Insights aggiunge DLL e il file ApplicationInsights.config all'app Web.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-170">Enabling Application Insights adds DLLs and ApplicationInsights.config to your web app.</span></span> <span data-ttu-id="7d3a0-171">È possibile [modificare il file con estensione config](app-insights-configuration-with-applicationinsights-config.md) per modificare alcune opzioni.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-171">You can [edit the .config file](app-insights-configuration-with-applicationinsights-config.md) to change some of the options.</span></span>

## <a name="when-you-re-publish-your-app-re-enable-application-insights"></a><span data-ttu-id="7d3a0-172">Quando si ripubblica l'app, riabilitare Application Insights</span><span class="sxs-lookup"><span data-stu-id="7d3a0-172">When you re-publish your app, re-enable Application Insights</span></span>

<span data-ttu-id="7d3a0-173">Prima di ripubblicare l'app, prendere in considerazione l'[aggiunta di Application Insights al codice in Visual Studio][greenbrown].</span><span class="sxs-lookup"><span data-stu-id="7d3a0-173">Before you re-publish your app, consider [adding Application Insights to the code in Visual Studio][greenbrown].</span></span> <span data-ttu-id="7d3a0-174">Questo approccio consente di ottenere dati di telemetria più dettagliati e di scrivere dati di telemetria personalizzati.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-174">You'll get more detailed telemetry and the ability to write custom telemetry.</span></span>

<span data-ttu-id="7d3a0-175">Per ripetere la pubblicazione senza aggiungere Application Insights al codice, si noti che il processo di distribuzione potrebbe eliminare i file DLL e il file ApplicationInsights.config dal sito Web pubblicato.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-175">If you want to re-publish without adding Application Insights to the code, be aware that the deployment process may delete the DLLs and ApplicationInsights.config from the published web site.</span></span> <span data-ttu-id="7d3a0-176">Di conseguenza:</span><span class="sxs-lookup"><span data-stu-id="7d3a0-176">Therefore:</span></span>

1. <span data-ttu-id="7d3a0-177">Se sono state apportate modifiche al file ApplicationInsights.config, copiarlo prima di ripubblicare l'app.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-177">If you edited ApplicationInsights.config, take a copy of it before you re-publish your app.</span></span>
2. <span data-ttu-id="7d3a0-178">Pubblicare di nuovo l'app.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-178">Republish your app.</span></span>
3. <span data-ttu-id="7d3a0-179">Abilitare di nuovo il monitoraggio di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-179">Re-enable Application Insights monitoring.</span></span> <span data-ttu-id="7d3a0-180">Usare il metodo appropriato, ovvero il pannello di controllo dell'app Web di Azure o Status Monitor in un host IIS.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-180">(Use the appropriate method: either the Azure web app control panel, or the Status Monitor on an IIS host.)</span></span>
4. <span data-ttu-id="7d3a0-181">Ripristinare eventuali modifiche apportate al file con estensione config.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-181">Reinstate any edits you performed on the .config file.</span></span>


## <a name="troubleshooting-runtime-configuration-of-application-insights"></a><span data-ttu-id="7d3a0-182">Risoluzione dei problemi della configurazione del runtime di Application Insights</span><span class="sxs-lookup"><span data-stu-id="7d3a0-182">Troubleshooting runtime configuration of Application Insights</span></span>

### <a name="cant-connect-no-telemetry"></a><span data-ttu-id="7d3a0-183">Nessuna connessione?</span><span class="sxs-lookup"><span data-stu-id="7d3a0-183">Can't connect?</span></span> <span data-ttu-id="7d3a0-184">Nessun dato di telemetria?</span><span class="sxs-lookup"><span data-stu-id="7d3a0-184">No telemetry?</span></span>

* <span data-ttu-id="7d3a0-185">Per consentire il funzionamento di Status Monitor, aprire le [porte in uscita necessarie](app-insights-ip-addresses.md#outgoing-ports) nel firewall del server.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-185">Open [the necessary outgoing ports](app-insights-ip-addresses.md#outgoing-ports) in your server's firewall to allow Status Monitor to work.</span></span>

* <span data-ttu-id="7d3a0-186">Aprire Status Monitor e selezionare la propria applicazione nel pannello a sinistra.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-186">Open Status Monitor and select your application on left pane.</span></span> <span data-ttu-id="7d3a0-187">Verificare se sono presenti messaggi di diagnostica per l'applicazione nella sezione "Configuration notifications":</span><span class="sxs-lookup"><span data-stu-id="7d3a0-187">Check if there are any diagnostics messages for this application in the "Configuration notifications" section:</span></span>

  ![Aprire il pannello delle prestazioni per visualizzare una richiesta, il tempo di risposta, le dipendenze e altri dati](./media/app-insights-monitor-performance-live-website-now/appinsights-status-monitor-diagnostics-message.png)
* <span data-ttu-id="7d3a0-189">Se sul server viene visualizzato un messaggio relativo alle autorizzazioni insufficienti, provare a seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="7d3a0-189">On the server, if you see a message about "insufficient permissions", try the following:</span></span>
  * <span data-ttu-id="7d3a0-190">In Gestione IIS selezionare il pool di applicazioni, aprire **Impostazioni avanzate** e prendere nota dell'identità in **Modello di processo**.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-190">In IIS Manager, select your application pool, open **Advanced Settings**, and under **Process Model** note the identity.</span></span>
  * <span data-ttu-id="7d3a0-191">Nel pannello di controllo Gestione computer, aggiungere questa identità al gruppo Utenti di Performance Monitor.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-191">In Computer management control panel, add this identity to the Performance Monitor Users group.</span></span>
* <span data-ttu-id="7d3a0-192">Se nel server è installato MMA/SCOM (System Center Operations Manager), alcune versioni potrebbero entrare in conflitto.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-192">If you have MMA/SCOM (Systems Center Operations Manager) installed on your server, some versions can conflict.</span></span> <span data-ttu-id="7d3a0-193">Disinstallare SCOM e Status Monitor e reinstallare le versioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-193">Uninstall both SCOM and Status Monitor, and re-install the latest versions.</span></span>
* <span data-ttu-id="7d3a0-194">Vedere [Risoluzione dei problemi][qna].</span><span class="sxs-lookup"><span data-stu-id="7d3a0-194">See [Troubleshooting][qna].</span></span>

## <a name="system-requirements"></a><span data-ttu-id="7d3a0-195">Requisiti di sistema</span><span class="sxs-lookup"><span data-stu-id="7d3a0-195">System Requirements</span></span>
<span data-ttu-id="7d3a0-196">Supporto del sistema operativo per Application Insights Status Monitor sul server</span><span class="sxs-lookup"><span data-stu-id="7d3a0-196">OS support for Application Insights Status Monitor on Server:</span></span>

* <span data-ttu-id="7d3a0-197">Windows Server 2008</span><span class="sxs-lookup"><span data-stu-id="7d3a0-197">Windows Server 2008</span></span>
* <span data-ttu-id="7d3a0-198">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="7d3a0-198">Windows Server 2008 R2</span></span>
* <span data-ttu-id="7d3a0-199">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="7d3a0-199">Windows Server 2012</span></span>
* <span data-ttu-id="7d3a0-200">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="7d3a0-200">Windows server 2012 R2</span></span>
* <span data-ttu-id="7d3a0-201">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="7d3a0-201">Windows Server 2016</span></span>

<span data-ttu-id="7d3a0-202">con SP più recente e .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="7d3a0-202">with latest SP and .NET Framework 4.5</span></span>

<span data-ttu-id="7d3a0-203">Sul lato client: Windows 7, 8, 8.1 e 10, con .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="7d3a0-203">On the client side: Windows 7, 8, 8.1 and 10, again with .NET Framework 4.5</span></span>

<span data-ttu-id="7d3a0-204">Il supporto IIS è: IIS 7, 7.5, 8, 8.5 (IIS è obbligatorio)</span><span class="sxs-lookup"><span data-stu-id="7d3a0-204">IIS support is: IIS 7, 7.5, 8, 8.5 (IIS is required)</span></span>

## <a name="automation-with-powershell"></a><span data-ttu-id="7d3a0-205">Automazione con PowerShell</span><span class="sxs-lookup"><span data-stu-id="7d3a0-205">Automation with PowerShell</span></span>
<span data-ttu-id="7d3a0-206">È possibile usare PowerShell nel server IIS per avviare e arrestare il monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-206">You can start and stop monitoring by using PowerShell on your IIS server.</span></span>

<span data-ttu-id="7d3a0-207">Importare prima di tutto il modulo di Application Insights:</span><span class="sxs-lookup"><span data-stu-id="7d3a0-207">First import the Application Insights module:</span></span>

`Import-Module 'C:\Program Files\Microsoft Application Insights\Status Monitor\PowerShell\Microsoft.Diagnostics.Agent.StatusMonitor.PowerShell.dll'`

<span data-ttu-id="7d3a0-208">Individuare le applicazioni sottoposte a monitoraggio:</span><span class="sxs-lookup"><span data-stu-id="7d3a0-208">Find out which apps are being monitored:</span></span>

`Get-ApplicationInsightsMonitoringStatus [-Name appName]`

* <span data-ttu-id="7d3a0-209">`-Name` (facoltativo): nome di un'app Web.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-209">`-Name` (Optional) The name of a web app.</span></span>
* <span data-ttu-id="7d3a0-210">Visualizza lo stato del monitoraggio di Application Insights per ogni app Web o per l'app denominata nel server IIS.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-210">Displays the Application Insights monitoring status for each web app (or the named app) in this IIS server.</span></span>
* <span data-ttu-id="7d3a0-211">Restituisce `ApplicationInsightsApplication` per ogni app.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-211">Returns `ApplicationInsightsApplication` for each app:</span></span>

  * <span data-ttu-id="7d3a0-212">`SdkState==EnabledAfterDeployment`: l'app viene monitorata ed è stata instrumentata in fase di esecuzione dallo strumento Status Monitor oppure da `Start-ApplicationInsightsMonitoring`.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-212">`SdkState==EnabledAfterDeployment`: App is being monitored, and was instrumented at run time, either by the Status Monitor tool, or by `Start-ApplicationInsightsMonitoring`.</span></span>
  * <span data-ttu-id="7d3a0-213">`SdkState==Disabled`: l'app non è instrumentata per Application Insights.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-213">`SdkState==Disabled`: The app is not instrumented for Application Insights.</span></span> <span data-ttu-id="7d3a0-214">Non è mai stata instrumentata oppure il monitoraggio in fase di esecuzione è stato disabilitato con lo strumento Status Monitor o con `Stop-ApplicationInsightsMonitoring`.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-214">Either it was never instrumented, or run-time monitoring was disabled with the Status Monitor tool or with `Stop-ApplicationInsightsMonitoring`.</span></span>
  * <span data-ttu-id="7d3a0-215">`SdkState==EnabledByCodeInstrumentation`: l'app è stata instrumentata aggiungendo l'SDK al codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-215">`SdkState==EnabledByCodeInstrumentation`: The app was instrumented by adding the SDK to the source code.</span></span> <span data-ttu-id="7d3a0-216">Il relativo SDK non può essere aggiornato o arrestato.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-216">Its SDK cannot be updated or stopped.</span></span>
  * <span data-ttu-id="7d3a0-217">`SdkVersion` : mostra la versione usata per il monitoraggio dell'app.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-217">`SdkVersion` shows the version in use for monitoring this app.</span></span>
  * <span data-ttu-id="7d3a0-218">`LatestAvailableSdkVersion`: mostra la versione attualmente disponibile nella raccolta NuGet.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-218">`LatestAvailableSdkVersion`shows the version currently available on the NuGet gallery.</span></span> <span data-ttu-id="7d3a0-219">Per aggiornare l'app a questa versione, usare `Update-ApplicationInsightsMonitoring`.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-219">To upgrade the app to this version, use `Update-ApplicationInsightsMonitoring`.</span></span>

`Start-ApplicationInsightsMonitoring -Name appName -InstrumentationKey 00000000-000-000-000-0000000`

* <span data-ttu-id="7d3a0-220">`-Name` : nome dell'app in IIS.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-220">`-Name` The name of the app in IIS</span></span>
* <span data-ttu-id="7d3a0-221">`-InstrumentationKey` : valore ikey della risorsa di Application Insights in cui visualizzare i risultati.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-221">`-InstrumentationKey` The ikey of the Application Insights resource where you want the results to be displayed.</span></span>
* <span data-ttu-id="7d3a0-222">Questo cmdlet influisce solo sulle app che non sono già instrumentate, ovvero SdkState==NotInstrumented.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-222">This cmdlet only affects apps that are not already instrumented - that is, SdkState==NotInstrumented.</span></span>

    <span data-ttu-id="7d3a0-223">Il cmdlet non influisce sulle app già instrumentate,</span><span class="sxs-lookup"><span data-stu-id="7d3a0-223">The cmdlet does not affect an app that is already instrumented.</span></span> <span data-ttu-id="7d3a0-224">sia che siano state instrumentate in fase di compilazione, aggiungendo l'SDK al codice, o in fase di esecuzione da un uso precedente di questo cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-224">It does not matter whether the app was instrumented at build time by adding the SDK to the code, or at run time by a previous use of this cmdlet.</span></span>

    <span data-ttu-id="7d3a0-225">La versione SDK usata per instrumentare l'app è la versione scaricata più di recente nel server.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-225">The SDK version used to instrument the app is the version that was most recently downloaded to this server.</span></span>

    <span data-ttu-id="7d3a0-226">Per scaricare l'ultima versione, usare Update-ApplicationInsightsVersion.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-226">To download the latest version, use Update-ApplicationInsightsVersion.</span></span>
* <span data-ttu-id="7d3a0-227">Se l'esito è positivo, restituisce `ApplicationInsightsApplication` .</span><span class="sxs-lookup"><span data-stu-id="7d3a0-227">Returns `ApplicationInsightsApplication` on success.</span></span> <span data-ttu-id="7d3a0-228">Se l'esito è negativo, registra una traccia in stderr.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-228">If it fails, it logs a trace to stderr.</span></span>

          Name                      : Default Web Site/WebApp1
          InstrumentationKey        : 00000000-0000-0000-0000-000000000000
          ProfilerState             : ApplicationInsights
          SdkState                  : EnabledAfterDeployment
          SdkVersion                : 1.2.1
          LatestAvailableSdkVersion : 1.2.3

`Stop-ApplicationInsightsMonitoring [-Name appName | -All]`

* <span data-ttu-id="7d3a0-229">`-Name` : nome di un'app in IIS.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-229">`-Name` The name of an app in IIS</span></span>
* <span data-ttu-id="7d3a0-230">`-All`: arresta il monitoraggio di tutte le app nel server IIS per cui `SdkState==EnabledAfterDeployment`</span><span class="sxs-lookup"><span data-stu-id="7d3a0-230">`-All` Stops monitoring all apps in this IIS server for which `SdkState==EnabledAfterDeployment`</span></span>
* <span data-ttu-id="7d3a0-231">Arresta il monitoraggio delle app specificate e rimuove la strumentazione.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-231">Stops monitoring the specified apps and removes instrumentation.</span></span> <span data-ttu-id="7d3a0-232">Funziona solo per le app instrumentate in fase di esecuzione usando lo strumento Status Monitor o Start-ApplicationInsightsApplication.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-232">It only works for apps that have been instrumented at run-time using the Status Monitoring tool or Start-ApplicationInsightsApplication.</span></span> <span data-ttu-id="7d3a0-233">(`SdkState==EnabledAfterDeployment`)</span><span class="sxs-lookup"><span data-stu-id="7d3a0-233">(`SdkState==EnabledAfterDeployment`)</span></span>
* <span data-ttu-id="7d3a0-234">Restituisce ApplicationInsightsApplication.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-234">Returns ApplicationInsightsApplication.</span></span>

<span data-ttu-id="7d3a0-235">`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]</span><span class="sxs-lookup"><span data-stu-id="7d3a0-235">`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]</span></span>

* <span data-ttu-id="7d3a0-236">`-Name`: nome di un'app Web in IIS.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-236">`-Name`: The name of a web app in IIS.</span></span>
* <span data-ttu-id="7d3a0-237">`-InstrumentationKey` (facoltativo): consente di modificare la risorsa a cui vengono inviati i dati di telemetria dell'app.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-237">`-InstrumentationKey` (Optional.) Use this to change the resource to which the app's telemetry is sent.</span></span>
* <span data-ttu-id="7d3a0-238">Questo cmdlet:</span><span class="sxs-lookup"><span data-stu-id="7d3a0-238">This cmdlet:</span></span>
  * <span data-ttu-id="7d3a0-239">Aggiorna l'app denominata alla versione dell'SDK scaricata più di recente nel computer.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-239">Upgrades the named app to the version of the SDK most recently downloaded to this machine.</span></span> <span data-ttu-id="7d3a0-240">Funziona solo se `SdkState==EnabledAfterDeployment`.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-240">(Only works if `SdkState==EnabledAfterDeployment`)</span></span>
  * <span data-ttu-id="7d3a0-241">Se si specifica una chiave di strumentazione, l'app denominata viene riconfigurata per l'invio di dati di telemetria alla risorsa con tale chiave.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-241">If you provide an instrumentation key, the named app is reconfigured to send telemetry to the resource with that key.</span></span> <span data-ttu-id="7d3a0-242">Funziona se `SdkState != Disabled`.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-242">(Works if `SdkState != Disabled`)</span></span>

`Update-ApplicationInsightsVersion`

* <span data-ttu-id="7d3a0-243">Scarica l'ultima versione di Application Insights SDK nel server.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-243">Downloads the latest Application Insights SDK to the server.</span></span>

## <span data-ttu-id="7d3a0-244"><a name="questions"></a>Domande su Status Monitor</span><span class="sxs-lookup"><span data-stu-id="7d3a0-244"><a name="questions"></a>Questions about Status Monitor</span></span>

### <a name="what-is-status-monitor"></a><span data-ttu-id="7d3a0-245">Che cos'è Status Monitor?</span><span class="sxs-lookup"><span data-stu-id="7d3a0-245">What is Status Monitor?</span></span>

<span data-ttu-id="7d3a0-246">Un'applicazione desktop che viene installata nel server Web IIS</span><span class="sxs-lookup"><span data-stu-id="7d3a0-246">A desktop application that you install in your IIS web server.</span></span> <span data-ttu-id="7d3a0-247">e consente di instrumentare e configurare le app Web.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-247">It helps you instrument and configure web apps.</span></span> 

### <a name="when-do-i-use-status-monitor"></a><span data-ttu-id="7d3a0-248">Quando si usa Status Monitor?</span><span class="sxs-lookup"><span data-stu-id="7d3a0-248">When do I use Status Monitor?</span></span>

* <span data-ttu-id="7d3a0-249">Per instrumentare qualsiasi app Web eseguita nel server IIS, anche se è già in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-249">To instrument any web app that is running on your IIS server - even if it is already running.</span></span>
* <span data-ttu-id="7d3a0-250">Per abilitare altri dati di telemetria per le app Web [compilate con Application Insights SDK](app-insights-asp-net.md) in fase di compilazione.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-250">To enable additional telemetry for web apps that have been [built with the Application Insights SDK](app-insights-asp-net.md) at compile time.</span></span> 

### <a name="can-i-close-it-after-it-runs"></a><span data-ttu-id="7d3a0-251">È possibile chiudere Status Monitor dopo l'esecuzione?</span><span class="sxs-lookup"><span data-stu-id="7d3a0-251">Can I close it after it runs?</span></span>

<span data-ttu-id="7d3a0-252">Sì.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-252">Yes.</span></span> <span data-ttu-id="7d3a0-253">Dopo aver instrumentato i siti Web selezionati, è possibile chiuderlo.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-253">After it has instrumented the websites you select, you can close it.</span></span>

<span data-ttu-id="7d3a0-254">Status Monitor non raccoglie i dati di telemetria,</span><span class="sxs-lookup"><span data-stu-id="7d3a0-254">It doesn't collect telemetry by itself.</span></span> <span data-ttu-id="7d3a0-255">ma si limita a configurare le app Web e impostare alcune autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-255">It just configures the web apps and sets some permissions.</span></span>

### <a name="what-does-status-monitor-do"></a><span data-ttu-id="7d3a0-256">Che cosa fa Status Monitor?</span><span class="sxs-lookup"><span data-stu-id="7d3a0-256">What does Status Monitor do?</span></span>

<span data-ttu-id="7d3a0-257">Quando si seleziona un'app Web per l'instrumentazione da parte di Status Monitor:</span><span class="sxs-lookup"><span data-stu-id="7d3a0-257">When you select a web app for Status Monitor to instrument:</span></span>

* <span data-ttu-id="7d3a0-258">Scarica e inserisce gli assembly di Application Insights e il file config nella cartella dei file binari dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-258">Downloads and places the Application Insights assemblies and .config file in the web app's binaries folder.</span></span>
* <span data-ttu-id="7d3a0-259">Modifica `web.config` per aggiungere il modulo di rilevamento HTTP di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-259">Modifies `web.config` to add the Application Insights HTTP tracking module.</span></span>
* <span data-ttu-id="7d3a0-260">Abilita la profilatura CLR per raccogliere le chiamate alle dipendenze.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-260">Enables CLR profiling to collect dependency calls.</span></span>

### <a name="do-i-need-to-run-status-monitor-whenever-i-update-the-app"></a><span data-ttu-id="7d3a0-261">È necessario eseguire Status Monitor ogni volta che si aggiorna l'app?</span><span class="sxs-lookup"><span data-stu-id="7d3a0-261">Do I need to run Status Monitor whenever I update the app?</span></span>

<span data-ttu-id="7d3a0-262">Se si esegue la ridistribuzione in modo incrementale, non è necessario.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-262">Not if you redeploy incrementally.</span></span> 

<span data-ttu-id="7d3a0-263">Se si seleziona l'opzione "Elimina file esistenti" nel processo di pubblicazione, è necessario eseguire nuovamente Status Monitor per configurare Application Insights.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-263">If you select the 'delete existing files' option in the publish process, you would need to re-run Status Monitor to configure Application Insights.</span></span>

### <a name="what-telemetry-is-collected"></a><span data-ttu-id="7d3a0-264">Quali dati di telemetria vengono raccolti?</span><span class="sxs-lookup"><span data-stu-id="7d3a0-264">What telemetry is collected?</span></span>

<span data-ttu-id="7d3a0-265">Per le applicazioni che vengono instrumentate solo in fase di esecuzione tramite Status Monitor:</span><span class="sxs-lookup"><span data-stu-id="7d3a0-265">For applications that you instrument only at run-time by using Status Monitor:</span></span>

* <span data-ttu-id="7d3a0-266">Richieste HTTP</span><span class="sxs-lookup"><span data-stu-id="7d3a0-266">HTTP requests</span></span>
* <span data-ttu-id="7d3a0-267">Chiamate alle dipendenze</span><span class="sxs-lookup"><span data-stu-id="7d3a0-267">Calls to dependencies</span></span>
* <span data-ttu-id="7d3a0-268">Eccezioni</span><span class="sxs-lookup"><span data-stu-id="7d3a0-268">Exceptions</span></span>
* <span data-ttu-id="7d3a0-269">Contatori delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="7d3a0-269">Performance counters</span></span>

<span data-ttu-id="7d3a0-270">Per le applicazioni già instrumentate in fase di compilazione:</span><span class="sxs-lookup"><span data-stu-id="7d3a0-270">For applications already instrumented at compile time:</span></span>

 * <span data-ttu-id="7d3a0-271">Contatori dei processi</span><span class="sxs-lookup"><span data-stu-id="7d3a0-271">Process counters.</span></span>
 * <span data-ttu-id="7d3a0-272">Chiamate alle dipendenze (.NET 4.5) e valori restituiti nelle chiamate alle dipendenze (.NET 4.6)</span><span class="sxs-lookup"><span data-stu-id="7d3a0-272">Dependency calls (.NET 4.5); return values in dependency calls (.NET 4.6).</span></span>
 * <span data-ttu-id="7d3a0-273">Valori di analisi dello stack delle eccezioni</span><span class="sxs-lookup"><span data-stu-id="7d3a0-273">Exception stack trace values.</span></span>

[<span data-ttu-id="7d3a0-274">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="7d3a0-274">Learn more</span></span>](http://apmtips.com/blog/2016/11/18/how-application-insights-status-monitor-not-monitors-dependencies/)

## <a name="video"></a><span data-ttu-id="7d3a0-275">Video</span><span class="sxs-lookup"><span data-stu-id="7d3a0-275">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <span data-ttu-id="7d3a0-276"><a name="next"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7d3a0-276"><a name="next"></a>Next steps</span></span>

<span data-ttu-id="7d3a0-277">Visualizzare i dati di telemetria:</span><span class="sxs-lookup"><span data-stu-id="7d3a0-277">View your telemetry:</span></span>

* <span data-ttu-id="7d3a0-278">[Esaminare le metriche](app-insights-metrics-explorer.md) per monitorare le prestazioni e l'utilizzo</span><span class="sxs-lookup"><span data-stu-id="7d3a0-278">[Explore metrics](app-insights-metrics-explorer.md) to monitor performance and usage</span></span>
* <span data-ttu-id="7d3a0-279">Per diagnosticare i problemi, vedere [Eventi e log di ricerca][diagnostic]</span><span class="sxs-lookup"><span data-stu-id="7d3a0-279">[Search events and logs][diagnostic] to diagnose problems</span></span>
* <span data-ttu-id="7d3a0-280">Per informazioni sulle query più avanzate, vedere [Analytics](app-insights-analytics.md)</span><span class="sxs-lookup"><span data-stu-id="7d3a0-280">[Analytics](app-insights-analytics.md) for more advanced queries</span></span>
* [<span data-ttu-id="7d3a0-281">Creare i dashboard</span><span class="sxs-lookup"><span data-stu-id="7d3a0-281">Create dashboards</span></span>](app-insights-dashboards.md)

<span data-ttu-id="7d3a0-282">Aggiungere altri dati di telemetria:</span><span class="sxs-lookup"><span data-stu-id="7d3a0-282">Add more telemetry:</span></span>

* <span data-ttu-id="7d3a0-283">[Creare test Web][availability] per assicurarsi che il sito rimanga attivo.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-283">[Create web tests][availability] to make sure your site stays live.</span></span>
* <span data-ttu-id="7d3a0-284">[Aggiungere dati di telemetria del client Web][usage] per visualizzare le eccezioni dal codice della pagina Web e consentire di inserire le chiamate di traccia.</span><span class="sxs-lookup"><span data-stu-id="7d3a0-284">[Add web client telemetry][usage] to see exceptions from web page code and to let you insert trace calls.</span></span>
* <span data-ttu-id="7d3a0-285">[Aggiungere Application Insights SDK al codice][greenbrown] per poter inserire chiamate di traccia e log nel codice del server</span><span class="sxs-lookup"><span data-stu-id="7d3a0-285">[Add Application Insights SDK to your code][greenbrown] so that you can insert trace and log calls</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[roles]: app-insights-resources-roles-access-control.md
[usage]: app-insights-javascript.md
