---
title: aaaMonitor un live ASP.NET web app con Azure Application Insights | Documenti Microsoft
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
ms.openlocfilehash: 0d53f0a59974f40767fae681bafc4f358d1283a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="instrument-web-apps-at-runtime-with-application-insights"></a><span data-ttu-id="02239-104">Instrumentare app Web in fase di esecuzione con Application Insights</span><span class="sxs-lookup"><span data-stu-id="02239-104">Instrument web apps at runtime with Application Insights</span></span>


<span data-ttu-id="02239-105">È possibile instrumentare un'applicazione web in tempo reale con Azure Application Insights, senza dovere toomodify o ridistribuire il codice.</span><span class="sxs-lookup"><span data-stu-id="02239-105">You can instrument a live web app with Azure Application Insights, without having toomodify or redeploy your code.</span></span> <span data-ttu-id="02239-106">Se le applicazioni sono ospitate da un server IIS locale, installare Status Monitor.</span><span class="sxs-lookup"><span data-stu-id="02239-106">If your apps are hosted by an on-premises IIS server, install Status Monitor.</span></span> <span data-ttu-id="02239-107">Se stai App web di Azure o eseguire in una macchina virtuale di Azure, è possibile attivare il monitoraggio di Application Insights hello Azure nel Pannello di controllo.</span><span class="sxs-lookup"><span data-stu-id="02239-107">If they're Azure web apps or run in an Azure VM, you can switch on Application Insights monitoring from hello Azure control panel.</span></span> <span data-ttu-id="02239-108">Sono disponibili anche articoli separati sulla strumentazione di [app Web J2EE live](app-insights-java-live.md) e [Servizi cloud di Azure](app-insights-cloudservices.md). È necessaria una sottoscrizione di [Microsoft Azure](http://azure.com) .</span><span class="sxs-lookup"><span data-stu-id="02239-108">(There are also separate articles about instrumenting [live J2EE web apps](app-insights-java-live.md) and [Azure Cloud Services](app-insights-cloudservices.md).) You need a [Microsoft Azure](http://azure.com) subscription.</span></span>

![grafici di esempio](./media/app-insights-monitor-performance-live-website-now/10-intro.png)

<span data-ttu-id="02239-110">È possibile scegliere di tre route tooapply Application Insights tooyour applicazioni web .NET:</span><span class="sxs-lookup"><span data-stu-id="02239-110">You have a choice of three routes tooapply Application Insights tooyour .NET web applications:</span></span>

* <span data-ttu-id="02239-111">**Fase di compilazione:** [hello Aggiungi Application Insights SDK] [ greenbrown] tooyour codice dell'applicazione web.</span><span class="sxs-lookup"><span data-stu-id="02239-111">**Build time:** [Add hello Application Insights SDK][greenbrown] tooyour web app code.</span></span>
* <span data-ttu-id="02239-112">**Fase di esecuzione:** instrumentare l'app web nel server di hello, come descritto di seguito, senza dover ricompilare e ridistribuire codice hello.</span><span class="sxs-lookup"><span data-stu-id="02239-112">**Run time:** Instrument your web app on hello server, as described below, without rebuilding and redeploying hello code.</span></span>
* <span data-ttu-id="02239-113">**Both:** compilare hello SDK nel codice dell'app web e si applicano anche le estensioni di hello in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="02239-113">**Both:** Build hello SDK into your web app code, and also apply hello run-time extensions.</span></span> <span data-ttu-id="02239-114">Ottenere hello migliori di entrambe le opzioni.</span><span class="sxs-lookup"><span data-stu-id="02239-114">Get hello best of both options.</span></span>

<span data-ttu-id="02239-115">Ecco un riepilogo di ciò che offrono i singoli modi:</span><span class="sxs-lookup"><span data-stu-id="02239-115">Here's a summary of what you get by each route:</span></span>

|  | <span data-ttu-id="02239-116">Fase di compilazione</span><span class="sxs-lookup"><span data-stu-id="02239-116">Build time</span></span> | <span data-ttu-id="02239-117">Fase di esecuzione</span><span class="sxs-lookup"><span data-stu-id="02239-117">Run time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="02239-118">Richieste ed eccezioni</span><span class="sxs-lookup"><span data-stu-id="02239-118">Requests & exceptions</span></span> |<span data-ttu-id="02239-119">Sì</span><span class="sxs-lookup"><span data-stu-id="02239-119">Yes</span></span> |<span data-ttu-id="02239-120">Sì</span><span class="sxs-lookup"><span data-stu-id="02239-120">Yes</span></span> |
| [<span data-ttu-id="02239-121">Eccezioni più dettagliate</span><span class="sxs-lookup"><span data-stu-id="02239-121">More detailed exceptions</span></span>](app-insights-asp-net-exceptions.md) | |<span data-ttu-id="02239-122">Sì</span><span class="sxs-lookup"><span data-stu-id="02239-122">Yes</span></span> |
| [<span data-ttu-id="02239-123">Diagnostica delle dipendenze</span><span class="sxs-lookup"><span data-stu-id="02239-123">Dependency diagnostics</span></span>](app-insights-asp-net-dependencies.md) |<span data-ttu-id="02239-124">In .NET 4.6 e versioni successive, ma meno dettagli</span><span class="sxs-lookup"><span data-stu-id="02239-124">On .NET 4.6+, but less detail</span></span> |<span data-ttu-id="02239-125">Sì, dettagli completi: codici risultato, testo del comando SQL, verbo HTTP</span><span class="sxs-lookup"><span data-stu-id="02239-125">Yes, full detail: result codes, SQL command text, HTTP verb</span></span>|
| [<span data-ttu-id="02239-126">Contatori delle prestazioni di sistema</span><span class="sxs-lookup"><span data-stu-id="02239-126">System performance counters</span></span>](app-insights-performance-counters.md) |<span data-ttu-id="02239-127">Sì</span><span class="sxs-lookup"><span data-stu-id="02239-127">Yes</span></span> |<span data-ttu-id="02239-128">Sì</span><span class="sxs-lookup"><span data-stu-id="02239-128">Yes</span></span> |
| <span data-ttu-id="02239-129">[API per telemetria personalizzata][api]</span><span class="sxs-lookup"><span data-stu-id="02239-129">[API for custom telemetry][api]</span></span> |<span data-ttu-id="02239-130">Sì</span><span class="sxs-lookup"><span data-stu-id="02239-130">Yes</span></span> |<span data-ttu-id="02239-131">No</span><span class="sxs-lookup"><span data-stu-id="02239-131">No</span></span> |
| [<span data-ttu-id="02239-132">Integrazione log di traccia</span><span class="sxs-lookup"><span data-stu-id="02239-132">Trace log integration</span></span>](app-insights-asp-net-trace-logs.md) |<span data-ttu-id="02239-133">Sì</span><span class="sxs-lookup"><span data-stu-id="02239-133">Yes</span></span> |<span data-ttu-id="02239-134">No</span><span class="sxs-lookup"><span data-stu-id="02239-134">No</span></span> |
| [<span data-ttu-id="02239-135">Visualizzazione pagina e dati utente</span><span class="sxs-lookup"><span data-stu-id="02239-135">Page view & user data</span></span>](app-insights-javascript.md) |<span data-ttu-id="02239-136">Sì</span><span class="sxs-lookup"><span data-stu-id="02239-136">Yes</span></span> |<span data-ttu-id="02239-137">No</span><span class="sxs-lookup"><span data-stu-id="02239-137">No</span></span> |
| <span data-ttu-id="02239-138">È necessario codice toorebuild</span><span class="sxs-lookup"><span data-stu-id="02239-138">Need toorebuild code</span></span> |<span data-ttu-id="02239-139">Sì</span><span class="sxs-lookup"><span data-stu-id="02239-139">Yes</span></span> | <span data-ttu-id="02239-140">No</span><span class="sxs-lookup"><span data-stu-id="02239-140">No</span></span> |


## <a name="monitor-a-live-azure-web-app"></a><span data-ttu-id="02239-141">Monitorare un'app Web live di Azure</span><span class="sxs-lookup"><span data-stu-id="02239-141">Monitor a live Azure web app</span></span>

<span data-ttu-id="02239-142">Se l'applicazione è in esecuzione come servizio web di Azure, modalità tooswitch sul monitoraggio:</span><span class="sxs-lookup"><span data-stu-id="02239-142">If your application is running as an Azure web service, here's how tooswitch on monitoring:</span></span>

* <span data-ttu-id="02239-143">Selezionare Application Insights nel Pannello di controllo dell'applicazione hello in Azure.</span><span class="sxs-lookup"><span data-stu-id="02239-143">Select Application Insights on hello app's control panel in Azure.</span></span>

    ![Configurare Application Insights per un'app Web di Azure](./media/app-insights-monitor-performance-live-website-now/azure-web-setup.png)
* <span data-ttu-id="02239-145">Quando verrà visualizzata la pagina di riepilogo di hello Application Insights, fare clic sul collegamento hello in hello inferiore tooopen hello completa risorsa di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="02239-145">When hello Application Insights summary page opens, click hello link at hello bottom tooopen hello full Application Insights resource.</span></span>

    ![Fare clic sulle tooApplication Insights](./media/app-insights-monitor-performance-live-website-now/azure-web-view-more.png)

<span data-ttu-id="02239-147">[Monitoraggio di app cloud e VM](app-insights-azure.md).</span><span class="sxs-lookup"><span data-stu-id="02239-147">[Monitoring Cloud and VM apps](app-insights-azure.md).</span></span>

### <a name="enable-client-side-monitoring-in-azure"></a><span data-ttu-id="02239-148">Abilitare il monitoraggio lato client in Azure</span><span class="sxs-lookup"><span data-stu-id="02239-148">Enable client-side monitoring in Azure</span></span>

<span data-ttu-id="02239-149">Se è stato abilitato Application Insights in Azure, è possibile aggiungere la visualizzazione delle pagine e la telemetria utente.</span><span class="sxs-lookup"><span data-stu-id="02239-149">If you have enabled Application Insights in Azure, you can add page view and user telemetry.</span></span>

1. <span data-ttu-id="02239-150">Selezionare Impostazioni > Impostazioni applicazione</span><span class="sxs-lookup"><span data-stu-id="02239-150">Select Settings > Application Settings</span></span>
2.  <span data-ttu-id="02239-151">In Impostazioni app aggiungere una nuova coppia chiave-valore:</span><span class="sxs-lookup"><span data-stu-id="02239-151">Under App Settings, add a new key value pair:</span></span> 
   
    <span data-ttu-id="02239-152">Chiave: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span><span class="sxs-lookup"><span data-stu-id="02239-152">Key: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span></span> 
    
    <span data-ttu-id="02239-153">Valore: `true`</span><span class="sxs-lookup"><span data-stu-id="02239-153">Value: `true`</span></span>
3. <span data-ttu-id="02239-154">**Salvare** hello impostazioni e **riavviare** l'app.</span><span class="sxs-lookup"><span data-stu-id="02239-154">**Save** hello settings and **Restart** your app.</span></span>

<span data-ttu-id="02239-155">Hello Application Insights JavaScript SDK ora viene inserito in ogni pagina web.</span><span class="sxs-lookup"><span data-stu-id="02239-155">hello Application Insights JavaScript SDK is now injected into each web page.</span></span>

## <a name="monitor-a-live-iis-web-app"></a><span data-ttu-id="02239-156">Monitorare un'app Web live di IIS</span><span class="sxs-lookup"><span data-stu-id="02239-156">Monitor a live IIS web app</span></span>

<span data-ttu-id="02239-157">Se l'app è ospitata in un server IIS, abilitare Application Insights usando Status Monitor.</span><span class="sxs-lookup"><span data-stu-id="02239-157">If your app is hosted on an IIS server, enable Application Insights by using Status Monitor.</span></span>

1. <span data-ttu-id="02239-158">Nel server Web IIS accedere con le credenziali di amministratore.</span><span class="sxs-lookup"><span data-stu-id="02239-158">On your IIS web server, sign in with administrator credentials.</span></span>
2. <span data-ttu-id="02239-159">Se Application Insights Status Monitor non è già installato, scaricare ed eseguire hello [installer Status Monitor](http://go.microsoft.com/fwlink/?LinkId=506648) (o eseguire [installazione guidata piattaforma Web](https://www.microsoft.com/web/downloads/platform.aspx) e cercare in essa contenuti lo stato di Application Insights Monitoraggio).</span><span class="sxs-lookup"><span data-stu-id="02239-159">If Application Insights Status Monitor is not already installed, download and run hello [Status Monitor installer](http://go.microsoft.com/fwlink/?LinkId=506648) (or run [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) and search in it for Application Insights Status Monitor).</span></span>
3. <span data-ttu-id="02239-160">In Monitoraggio di stato, selezionare un'applicazione web hello installato o un sito Web che si desidera toomonitor.</span><span class="sxs-lookup"><span data-stu-id="02239-160">In Status Monitor, select hello installed web application or website that you want toomonitor.</span></span> <span data-ttu-id="02239-161">Accedere con le credenziali di Azure.</span><span class="sxs-lookup"><span data-stu-id="02239-161">Sign in with your Azure credentials.</span></span>

    <span data-ttu-id="02239-162">Configurare hello risorsa in cui si desidera risultati hello toosee portale Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="02239-162">Configure hello resource where you want toosee hello results in hello Application Insights portal.</span></span> <span data-ttu-id="02239-163">(In genere, è migliore toocreate una nuova risorsa.</span><span class="sxs-lookup"><span data-stu-id="02239-163">(Normally, it's best toocreate a new resource.</span></span> <span data-ttu-id="02239-164">Selezionare una risorsa esistente se sono già disponibili [test Web][availability] o il [monitoraggio del client][client] per questa app.</span><span class="sxs-lookup"><span data-stu-id="02239-164">Select an existing resource if you already have [web tests][availability] or [client monitoring][client] for this app.)</span></span> 

    ![Scegliere un'applicazione e una risorsa.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-configAIC.png)

4. <span data-ttu-id="02239-166">Riavviare IIS.</span><span class="sxs-lookup"><span data-stu-id="02239-166">Restart IIS.</span></span>

    ![Scegliere Riavvia nella parte superiore di hello della finestra di dialogo hello.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-restart.png)

    <span data-ttu-id="02239-168">Il servizio Web viene interrotto per un breve periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="02239-168">Your web service is interrupted for a short while.</span></span>

## <a name="customize-monitoring-options"></a><span data-ttu-id="02239-169">Personalizzare le opzioni di monitoraggio</span><span class="sxs-lookup"><span data-stu-id="02239-169">Customize monitoring options</span></span>

<span data-ttu-id="02239-170">L'abilitazione di Application Insights aggiunge DLL e Applicationinsights tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="02239-170">Enabling Application Insights adds DLLs and ApplicationInsights.config tooyour web app.</span></span> <span data-ttu-id="02239-171">È possibile [modificare i file con estensione config hello](app-insights-configuration-with-applicationinsights-config.md) toochange alcune delle opzioni di hello.</span><span class="sxs-lookup"><span data-stu-id="02239-171">You can [edit hello .config file](app-insights-configuration-with-applicationinsights-config.md) toochange some of hello options.</span></span>

## <a name="when-you-re-publish-your-app-re-enable-application-insights"></a><span data-ttu-id="02239-172">Quando si ripubblica l'app, riabilitare Application Insights</span><span class="sxs-lookup"><span data-stu-id="02239-172">When you re-publish your app, re-enable Application Insights</span></span>

<span data-ttu-id="02239-173">Prima di pubblicare nuovamente l'app, prendere in considerazione [aggiungendo codice toohello Application Insights in Visual Studio][greenbrown].</span><span class="sxs-lookup"><span data-stu-id="02239-173">Before you re-publish your app, consider [adding Application Insights toohello code in Visual Studio][greenbrown].</span></span> <span data-ttu-id="02239-174">Si otterrà telemetria più dettagliata e dati di telemetria personalizzati hello possibilità toowrite.</span><span class="sxs-lookup"><span data-stu-id="02239-174">You'll get more detailed telemetry and hello ability toowrite custom telemetry.</span></span>

<span data-ttu-id="02239-175">Se si desidera toore-pubblicare senza aggiungere codice toohello Application Insights, tenere presente che il processo di distribuzione hello può eliminare le DLL hello e Applicationinsights da hello pubblicazione sito web.</span><span class="sxs-lookup"><span data-stu-id="02239-175">If you want toore-publish without adding Application Insights toohello code, be aware that hello deployment process may delete hello DLLs and ApplicationInsights.config from hello published web site.</span></span> <span data-ttu-id="02239-176">Di conseguenza:</span><span class="sxs-lookup"><span data-stu-id="02239-176">Therefore:</span></span>

1. <span data-ttu-id="02239-177">Se sono state apportate modifiche al file ApplicationInsights.config, copiarlo prima di ripubblicare l'app.</span><span class="sxs-lookup"><span data-stu-id="02239-177">If you edited ApplicationInsights.config, take a copy of it before you re-publish your app.</span></span>
2. <span data-ttu-id="02239-178">Pubblicare di nuovo l'app.</span><span class="sxs-lookup"><span data-stu-id="02239-178">Republish your app.</span></span>
3. <span data-ttu-id="02239-179">Abilitare di nuovo il monitoraggio di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="02239-179">Re-enable Application Insights monitoring.</span></span> <span data-ttu-id="02239-180">(Utilizzare il metodo appropriato di hello: pannello di controllo di hello Azure web app o hello Status Monitor in un host IIS.)</span><span class="sxs-lookup"><span data-stu-id="02239-180">(Use hello appropriate method: either hello Azure web app control panel, or hello Status Monitor on an IIS host.)</span></span>
4. <span data-ttu-id="02239-181">Ripristinare le modifiche apportate al file con estensione config hello.</span><span class="sxs-lookup"><span data-stu-id="02239-181">Reinstate any edits you performed on hello .config file.</span></span>


## <a name="troubleshooting-runtime-configuration-of-application-insights"></a><span data-ttu-id="02239-182">Risoluzione dei problemi della configurazione del runtime di Application Insights</span><span class="sxs-lookup"><span data-stu-id="02239-182">Troubleshooting runtime configuration of Application Insights</span></span>

### <a name="cant-connect-no-telemetry"></a><span data-ttu-id="02239-183">Nessuna connessione?</span><span class="sxs-lookup"><span data-stu-id="02239-183">Can't connect?</span></span> <span data-ttu-id="02239-184">Nessun dato di telemetria?</span><span class="sxs-lookup"><span data-stu-id="02239-184">No telemetry?</span></span>

* <span data-ttu-id="02239-185">Aprire [hello porte in uscita necessarie](app-insights-ip-addresses.md#outgoing-ports) in toowork di monitoraggio stato tooallow firewall del server.</span><span class="sxs-lookup"><span data-stu-id="02239-185">Open [hello necessary outgoing ports](app-insights-ip-addresses.md#outgoing-ports) in your server's firewall tooallow Status Monitor toowork.</span></span>

* <span data-ttu-id="02239-186">Aprire Status Monitor e selezionare la propria applicazione nel pannello a sinistra.</span><span class="sxs-lookup"><span data-stu-id="02239-186">Open Status Monitor and select your application on left pane.</span></span> <span data-ttu-id="02239-187">Verificare se sono presenti eventuali messaggi di diagnostica per questa applicazione nella sezione "Configurazione notifiche" hello:</span><span class="sxs-lookup"><span data-stu-id="02239-187">Check if there are any diagnostics messages for this application in hello "Configuration notifications" section:</span></span>

  ![Aprire una richiesta di hello prestazioni pannello toosee, tempo di risposta, dipendenze e altri dati](./media/app-insights-monitor-performance-live-website-now/appinsights-status-monitor-diagnostics-message.png)
* <span data-ttu-id="02239-189">Nel server di hello, se viene visualizzato un messaggio relativo ad autorizzazioni"insufficienti", provare a seguente hello:</span><span class="sxs-lookup"><span data-stu-id="02239-189">On hello server, if you see a message about "insufficient permissions", try hello following:</span></span>
  * <span data-ttu-id="02239-190">In Gestione IIS, selezionare il pool di applicazioni, aprire **impostazioni avanzate**e in **modello di processo** nota identità hello.</span><span class="sxs-lookup"><span data-stu-id="02239-190">In IIS Manager, select your application pool, open **Advanced Settings**, and under **Process Model** note hello identity.</span></span>
  * <span data-ttu-id="02239-191">Nel Pannello di controllo di gestione Computer, aggiungere questo gruppo Performance Monitor Users toohello di identità.</span><span class="sxs-lookup"><span data-stu-id="02239-191">In Computer management control panel, add this identity toohello Performance Monitor Users group.</span></span>
* <span data-ttu-id="02239-192">Se nel server è installato MMA/SCOM (System Center Operations Manager), alcune versioni potrebbero entrare in conflitto.</span><span class="sxs-lookup"><span data-stu-id="02239-192">If you have MMA/SCOM (Systems Center Operations Manager) installed on your server, some versions can conflict.</span></span> <span data-ttu-id="02239-193">Disinstallare SCOM e monitoraggio dello stato e reinstallare la versione più recente di hello.</span><span class="sxs-lookup"><span data-stu-id="02239-193">Uninstall both SCOM and Status Monitor, and re-install hello latest versions.</span></span>
* <span data-ttu-id="02239-194">Vedere [Risoluzione dei problemi][qna].</span><span class="sxs-lookup"><span data-stu-id="02239-194">See [Troubleshooting][qna].</span></span>

## <a name="system-requirements"></a><span data-ttu-id="02239-195">Requisiti di sistema</span><span class="sxs-lookup"><span data-stu-id="02239-195">System Requirements</span></span>
<span data-ttu-id="02239-196">Supporto del sistema operativo per Application Insights Status Monitor sul server</span><span class="sxs-lookup"><span data-stu-id="02239-196">OS support for Application Insights Status Monitor on Server:</span></span>

* <span data-ttu-id="02239-197">Windows Server 2008</span><span class="sxs-lookup"><span data-stu-id="02239-197">Windows Server 2008</span></span>
* <span data-ttu-id="02239-198">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="02239-198">Windows Server 2008 R2</span></span>
* <span data-ttu-id="02239-199">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="02239-199">Windows Server 2012</span></span>
* <span data-ttu-id="02239-200">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="02239-200">Windows server 2012 R2</span></span>
* <span data-ttu-id="02239-201">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="02239-201">Windows Server 2016</span></span>

<span data-ttu-id="02239-202">con SP più recente e .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="02239-202">with latest SP and .NET Framework 4.5</span></span>

<span data-ttu-id="02239-203">Sul lato client hello: Windows 7, 8, 8.1 e 10, con .NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="02239-203">On hello client side: Windows 7, 8, 8.1 and 10, again with .NET Framework 4.5</span></span>

<span data-ttu-id="02239-204">Il supporto IIS è: IIS 7, 7.5, 8, 8.5 (IIS è obbligatorio)</span><span class="sxs-lookup"><span data-stu-id="02239-204">IIS support is: IIS 7, 7.5, 8, 8.5 (IIS is required)</span></span>

## <a name="automation-with-powershell"></a><span data-ttu-id="02239-205">Automazione con PowerShell</span><span class="sxs-lookup"><span data-stu-id="02239-205">Automation with PowerShell</span></span>
<span data-ttu-id="02239-206">È possibile usare PowerShell nel server IIS per avviare e arrestare il monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="02239-206">You can start and stop monitoring by using PowerShell on your IIS server.</span></span>

<span data-ttu-id="02239-207">È innanzitutto necessario importare il modulo di Application Insights hello:</span><span class="sxs-lookup"><span data-stu-id="02239-207">First import hello Application Insights module:</span></span>

`Import-Module 'C:\Program Files\Microsoft Application Insights\Status Monitor\PowerShell\Microsoft.Diagnostics.Agent.StatusMonitor.PowerShell.dll'`

<span data-ttu-id="02239-208">Individuare le applicazioni sottoposte a monitoraggio:</span><span class="sxs-lookup"><span data-stu-id="02239-208">Find out which apps are being monitored:</span></span>

`Get-ApplicationInsightsMonitoringStatus [-Name appName]`

* <span data-ttu-id="02239-209">`-Name`Nome hello (facoltativo) di un'app web.</span><span class="sxs-lookup"><span data-stu-id="02239-209">`-Name` (Optional) hello name of a web app.</span></span>
* <span data-ttu-id="02239-210">Consente di visualizzare hello lo stato di monitoraggio di Application Insights per ogni app web (o hello denominato app) nel server IIS.</span><span class="sxs-lookup"><span data-stu-id="02239-210">Displays hello Application Insights monitoring status for each web app (or hello named app) in this IIS server.</span></span>
* <span data-ttu-id="02239-211">Restituisce `ApplicationInsightsApplication` per ogni app.</span><span class="sxs-lookup"><span data-stu-id="02239-211">Returns `ApplicationInsightsApplication` for each app:</span></span>

  * <span data-ttu-id="02239-212">`SdkState==EnabledAfterDeployment`: L'app viene monitorato ed è stato instrumentato in fase di esecuzione per lo strumento di monitoraggio dello stato di hello o per `Start-ApplicationInsightsMonitoring`.</span><span class="sxs-lookup"><span data-stu-id="02239-212">`SdkState==EnabledAfterDeployment`: App is being monitored, and was instrumented at run time, either by hello Status Monitor tool, or by `Start-ApplicationInsightsMonitoring`.</span></span>
  * <span data-ttu-id="02239-213">`SdkState==Disabled`: hello app non è instrumentato per Application Insights.</span><span class="sxs-lookup"><span data-stu-id="02239-213">`SdkState==Disabled`: hello app is not instrumented for Application Insights.</span></span> <span data-ttu-id="02239-214">È non stato mai instrumentato o monitoraggio in fase di esecuzione è stato disabilitato con lo strumento di monitoraggio dello stato di hello o `Stop-ApplicationInsightsMonitoring`.</span><span class="sxs-lookup"><span data-stu-id="02239-214">Either it was never instrumented, or run-time monitoring was disabled with hello Status Monitor tool or with `Stop-ApplicationInsightsMonitoring`.</span></span>
  * <span data-ttu-id="02239-215">`SdkState==EnabledByCodeInstrumentation`: è stato instrumentato app hello mediante l'aggiunta di codice sorgente di hello SDK toohello.</span><span class="sxs-lookup"><span data-stu-id="02239-215">`SdkState==EnabledByCodeInstrumentation`: hello app was instrumented by adding hello SDK toohello source code.</span></span> <span data-ttu-id="02239-216">Il relativo SDK non può essere aggiornato o arrestato.</span><span class="sxs-lookup"><span data-stu-id="02239-216">Its SDK cannot be updated or stopped.</span></span>
  * <span data-ttu-id="02239-217">`SdkVersion`Mostra una versione di hello in uso per il monitoraggio di questa app.</span><span class="sxs-lookup"><span data-stu-id="02239-217">`SdkVersion` shows hello version in use for monitoring this app.</span></span>
  * <span data-ttu-id="02239-218">`LatestAvailableSdkVersion`Mostra hello versione attualmente disponibile nella raccolta NuGet hello.</span><span class="sxs-lookup"><span data-stu-id="02239-218">`LatestAvailableSdkVersion`shows hello version currently available on hello NuGet gallery.</span></span> <span data-ttu-id="02239-219">versione del toothis app hello tooupgrade, utilizzare `Update-ApplicationInsightsMonitoring`.</span><span class="sxs-lookup"><span data-stu-id="02239-219">tooupgrade hello app toothis version, use `Update-ApplicationInsightsMonitoring`.</span></span>

`Start-ApplicationInsightsMonitoring -Name appName -InstrumentationKey 00000000-000-000-000-0000000`

* <span data-ttu-id="02239-220">`-Name`nome Hello dell'applicazione hello in IIS</span><span class="sxs-lookup"><span data-stu-id="02239-220">`-Name` hello name of hello app in IIS</span></span>
* <span data-ttu-id="02239-221">`-InstrumentationKey`Hello ikey di hello risorsa di Application Insights in cui si desidera toobe risultati hello visualizzato.</span><span class="sxs-lookup"><span data-stu-id="02239-221">`-InstrumentationKey` hello ikey of hello Application Insights resource where you want hello results toobe displayed.</span></span>
* <span data-ttu-id="02239-222">Questo cmdlet influisce solo sulle app che non sono già instrumentate, ovvero SdkState==NotInstrumented.</span><span class="sxs-lookup"><span data-stu-id="02239-222">This cmdlet only affects apps that are not already instrumented - that is, SdkState==NotInstrumented.</span></span>

    <span data-ttu-id="02239-223">Hello non influisce invece un'applicazione che è già stata instrumentata.</span><span class="sxs-lookup"><span data-stu-id="02239-223">hello cmdlet does not affect an app that is already instrumented.</span></span> <span data-ttu-id="02239-224">Non è rilevante se è stato instrumentato app hello in fase di compilazione aggiungendo hello SDK toohello codice, né in fase di esecuzione da una precedente, utilizzare questo cmdlet.</span><span class="sxs-lookup"><span data-stu-id="02239-224">It does not matter whether hello app was instrumented at build time by adding hello SDK toohello code, or at run time by a previous use of this cmdlet.</span></span>

    <span data-ttu-id="02239-225">app hello tooinstrument di Hello SDK versione utilizzata è la versione di hello ultimo scaricata toothis server.</span><span class="sxs-lookup"><span data-stu-id="02239-225">hello SDK version used tooinstrument hello app is hello version that was most recently downloaded toothis server.</span></span>

    <span data-ttu-id="02239-226">versione più recente di hello toodownload, utilizzare ApplicationInsightsVersion di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="02239-226">toodownload hello latest version, use Update-ApplicationInsightsVersion.</span></span>
* <span data-ttu-id="02239-227">Se l'esito è positivo, restituisce `ApplicationInsightsApplication` .</span><span class="sxs-lookup"><span data-stu-id="02239-227">Returns `ApplicationInsightsApplication` on success.</span></span> <span data-ttu-id="02239-228">In caso contrario, viene registrato un toostderr di traccia.</span><span class="sxs-lookup"><span data-stu-id="02239-228">If it fails, it logs a trace toostderr.</span></span>

          Name                      : Default Web Site/WebApp1
          InstrumentationKey        : 00000000-0000-0000-0000-000000000000
          ProfilerState             : ApplicationInsights
          SdkState                  : EnabledAfterDeployment
          SdkVersion                : 1.2.1
          LatestAvailableSdkVersion : 1.2.3

`Stop-ApplicationInsightsMonitoring [-Name appName | -All]`

* <span data-ttu-id="02239-229">`-Name`nome Hello di un'applicazione in IIS</span><span class="sxs-lookup"><span data-stu-id="02239-229">`-Name` hello name of an app in IIS</span></span>
* <span data-ttu-id="02239-230">`-All`: arresta il monitoraggio di tutte le app nel server IIS per cui `SdkState==EnabledAfterDeployment`</span><span class="sxs-lookup"><span data-stu-id="02239-230">`-All` Stops monitoring all apps in this IIS server for which `SdkState==EnabledAfterDeployment`</span></span>
* <span data-ttu-id="02239-231">Arresta il monitoraggio hello le app specificate e rimuove strumentazione.</span><span class="sxs-lookup"><span data-stu-id="02239-231">Stops monitoring hello specified apps and removes instrumentation.</span></span> <span data-ttu-id="02239-232">Funziona solo per le applicazioni che sono stata modificate in fase di esecuzione usando hello dello strumento di monitoraggio dello stato o ApplicationInsightsApplication di inizio.</span><span class="sxs-lookup"><span data-stu-id="02239-232">It only works for apps that have been instrumented at run-time using hello Status Monitoring tool or Start-ApplicationInsightsApplication.</span></span> <span data-ttu-id="02239-233">(`SdkState==EnabledAfterDeployment`)</span><span class="sxs-lookup"><span data-stu-id="02239-233">(`SdkState==EnabledAfterDeployment`)</span></span>
* <span data-ttu-id="02239-234">Restituisce ApplicationInsightsApplication.</span><span class="sxs-lookup"><span data-stu-id="02239-234">Returns ApplicationInsightsApplication.</span></span>

<span data-ttu-id="02239-235">`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]</span><span class="sxs-lookup"><span data-stu-id="02239-235">`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]</span></span>

* <span data-ttu-id="02239-236">`-Name`: nome hello di un'app web in IIS.</span><span class="sxs-lookup"><span data-stu-id="02239-236">`-Name`: hello name of a web app in IIS.</span></span>
* <span data-ttu-id="02239-237">`-InstrumentationKey` (facoltativo): Utilizzo di che dati di telemetria toochange hello risorsa toowhich hello dell'app viene inviato.</span><span class="sxs-lookup"><span data-stu-id="02239-237">`-InstrumentationKey` (Optional.) Use this toochange hello resource toowhich hello app's telemetry is sent.</span></span>
* <span data-ttu-id="02239-238">Questo cmdlet:</span><span class="sxs-lookup"><span data-stu-id="02239-238">This cmdlet:</span></span>
  * <span data-ttu-id="02239-239">Hello aggiornamenti denominato hello SDK versione toohello app scaricate più di recente toothis macchina.</span><span class="sxs-lookup"><span data-stu-id="02239-239">Upgrades hello named app toohello version of hello SDK most recently downloaded toothis machine.</span></span> <span data-ttu-id="02239-240">Funziona solo se `SdkState==EnabledAfterDeployment`.</span><span class="sxs-lookup"><span data-stu-id="02239-240">(Only works if `SdkState==EnabledAfterDeployment`)</span></span>
  * <span data-ttu-id="02239-241">Se si specifica una chiave di strumentazione, hello denominato app viene riconfigurato toosend telemetria toohello risorsa con tale chiave.</span><span class="sxs-lookup"><span data-stu-id="02239-241">If you provide an instrumentation key, hello named app is reconfigured toosend telemetry toohello resource with that key.</span></span> <span data-ttu-id="02239-242">Funziona se `SdkState != Disabled`.</span><span class="sxs-lookup"><span data-stu-id="02239-242">(Works if `SdkState != Disabled`)</span></span>

`Update-ApplicationInsightsVersion`

* <span data-ttu-id="02239-243">Scarica server toohello Application Insights SDK più recente di hello.</span><span class="sxs-lookup"><span data-stu-id="02239-243">Downloads hello latest Application Insights SDK toohello server.</span></span>

## <span data-ttu-id="02239-244"><a name="questions"></a>Domande su Status Monitor</span><span class="sxs-lookup"><span data-stu-id="02239-244"><a name="questions"></a>Questions about Status Monitor</span></span>

### <a name="what-is-status-monitor"></a><span data-ttu-id="02239-245">Che cos'è Status Monitor?</span><span class="sxs-lookup"><span data-stu-id="02239-245">What is Status Monitor?</span></span>

<span data-ttu-id="02239-246">Un'applicazione desktop che viene installata nel server Web IIS</span><span class="sxs-lookup"><span data-stu-id="02239-246">A desktop application that you install in your IIS web server.</span></span> <span data-ttu-id="02239-247">e consente di instrumentare e configurare le app Web.</span><span class="sxs-lookup"><span data-stu-id="02239-247">It helps you instrument and configure web apps.</span></span> 

### <a name="when-do-i-use-status-monitor"></a><span data-ttu-id="02239-248">Quando si usa Status Monitor?</span><span class="sxs-lookup"><span data-stu-id="02239-248">When do I use Status Monitor?</span></span>

* <span data-ttu-id="02239-249">tooinstrument qualsiasi web app è in esecuzione sul server IIS, anche se è già in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="02239-249">tooinstrument any web app that is running on your IIS server - even if it is already running.</span></span>
* <span data-ttu-id="02239-250">tooenable telemetria aggiuntive per le applicazioni web che sono stati [compilati con Application Insights SDK hello](app-insights-asp-net.md) in fase di compilazione.</span><span class="sxs-lookup"><span data-stu-id="02239-250">tooenable additional telemetry for web apps that have been [built with hello Application Insights SDK](app-insights-asp-net.md) at compile time.</span></span> 

### <a name="can-i-close-it-after-it-runs"></a><span data-ttu-id="02239-251">È possibile chiudere Status Monitor dopo l'esecuzione?</span><span class="sxs-lookup"><span data-stu-id="02239-251">Can I close it after it runs?</span></span>

<span data-ttu-id="02239-252">Sì.</span><span class="sxs-lookup"><span data-stu-id="02239-252">Yes.</span></span> <span data-ttu-id="02239-253">Dopo che è instrumentato siti Web di hello che si seleziona, è possibile chiuderlo.</span><span class="sxs-lookup"><span data-stu-id="02239-253">After it has instrumented hello websites you select, you can close it.</span></span>

<span data-ttu-id="02239-254">Status Monitor non raccoglie i dati di telemetria,</span><span class="sxs-lookup"><span data-stu-id="02239-254">It doesn't collect telemetry by itself.</span></span> <span data-ttu-id="02239-255">Sufficiente Configura App web hello e imposta alcune autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="02239-255">It just configures hello web apps and sets some permissions.</span></span>

### <a name="what-does-status-monitor-do"></a><span data-ttu-id="02239-256">Che cosa fa Status Monitor?</span><span class="sxs-lookup"><span data-stu-id="02239-256">What does Status Monitor do?</span></span>

<span data-ttu-id="02239-257">Quando si seleziona un'app web per monitoraggio stato tooinstrument:</span><span class="sxs-lookup"><span data-stu-id="02239-257">When you select a web app for Status Monitor tooinstrument:</span></span>

* <span data-ttu-id="02239-258">Scarica e inserisce gli assembly di Application Insights hello e file. config nella cartella dei file binari dell'applicazione web hello.</span><span class="sxs-lookup"><span data-stu-id="02239-258">Downloads and places hello Application Insights assemblies and .config file in hello web app's binaries folder.</span></span>
* <span data-ttu-id="02239-259">Modifica `web.config` modulo di rilevamento tooadd hello Application Insights HTTP.</span><span class="sxs-lookup"><span data-stu-id="02239-259">Modifies `web.config` tooadd hello Application Insights HTTP tracking module.</span></span>
* <span data-ttu-id="02239-260">Abilita analisi toocollect chiamate a dipendenze di CLR.</span><span class="sxs-lookup"><span data-stu-id="02239-260">Enables CLR profiling toocollect dependency calls.</span></span>

### <a name="do-i-need-toorun-status-monitor-whenever-i-update-hello-app"></a><span data-ttu-id="02239-261">È necessario toorun monitoraggio stato quando si aggiorna l'applicazione hello?</span><span class="sxs-lookup"><span data-stu-id="02239-261">Do I need toorun Status Monitor whenever I update hello app?</span></span>

<span data-ttu-id="02239-262">Se si esegue la ridistribuzione in modo incrementale, non è necessario.</span><span class="sxs-lookup"><span data-stu-id="02239-262">Not if you redeploy incrementally.</span></span> 

<span data-ttu-id="02239-263">Se si seleziona l'opzione 'eliminare i file esistenti' hello in hello processo di pubblicazione, è necessario eseguire toore Status Monitor tooconfigure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="02239-263">If you select hello 'delete existing files' option in hello publish process, you would need toore-run Status Monitor tooconfigure Application Insights.</span></span>

### <a name="what-telemetry-is-collected"></a><span data-ttu-id="02239-264">Quali dati di telemetria vengono raccolti?</span><span class="sxs-lookup"><span data-stu-id="02239-264">What telemetry is collected?</span></span>

<span data-ttu-id="02239-265">Per le applicazioni che vengono instrumentate solo in fase di esecuzione tramite Status Monitor:</span><span class="sxs-lookup"><span data-stu-id="02239-265">For applications that you instrument only at run-time by using Status Monitor:</span></span>

* <span data-ttu-id="02239-266">Richieste HTTP</span><span class="sxs-lookup"><span data-stu-id="02239-266">HTTP requests</span></span>
* <span data-ttu-id="02239-267">Chiama toodependencies</span><span class="sxs-lookup"><span data-stu-id="02239-267">Calls toodependencies</span></span>
* <span data-ttu-id="02239-268">Eccezioni</span><span class="sxs-lookup"><span data-stu-id="02239-268">Exceptions</span></span>
* <span data-ttu-id="02239-269">Contatori delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="02239-269">Performance counters</span></span>

<span data-ttu-id="02239-270">Per le applicazioni già instrumentate in fase di compilazione:</span><span class="sxs-lookup"><span data-stu-id="02239-270">For applications already instrumented at compile time:</span></span>

 * <span data-ttu-id="02239-271">Contatori dei processi</span><span class="sxs-lookup"><span data-stu-id="02239-271">Process counters.</span></span>
 * <span data-ttu-id="02239-272">Chiamate alle dipendenze (.NET 4.5) e valori restituiti nelle chiamate alle dipendenze (.NET 4.6)</span><span class="sxs-lookup"><span data-stu-id="02239-272">Dependency calls (.NET 4.5); return values in dependency calls (.NET 4.6).</span></span>
 * <span data-ttu-id="02239-273">Valori di analisi dello stack delle eccezioni</span><span class="sxs-lookup"><span data-stu-id="02239-273">Exception stack trace values.</span></span>

[<span data-ttu-id="02239-274">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="02239-274">Learn more</span></span>](http://apmtips.com/blog/2016/11/18/how-application-insights-status-monitor-not-monitors-dependencies/)

## <a name="video"></a><span data-ttu-id="02239-275">Video</span><span class="sxs-lookup"><span data-stu-id="02239-275">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <span data-ttu-id="02239-276"><a name="next"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="02239-276"><a name="next"></a>Next steps</span></span>

<span data-ttu-id="02239-277">Visualizzare i dati di telemetria:</span><span class="sxs-lookup"><span data-stu-id="02239-277">View your telemetry:</span></span>

* <span data-ttu-id="02239-278">[Esplorare le metriche](app-insights-metrics-explorer.md) toomonitor delle prestazioni e utilizzo</span><span class="sxs-lookup"><span data-stu-id="02239-278">[Explore metrics](app-insights-metrics-explorer.md) toomonitor performance and usage</span></span>
* <span data-ttu-id="02239-279">[Ricerca di eventi e log] [ diagnostic] toodiagnose problemi</span><span class="sxs-lookup"><span data-stu-id="02239-279">[Search events and logs][diagnostic] toodiagnose problems</span></span>
* <span data-ttu-id="02239-280">Per informazioni sulle query più avanzate, vedere [Analytics](app-insights-analytics.md)</span><span class="sxs-lookup"><span data-stu-id="02239-280">[Analytics](app-insights-analytics.md) for more advanced queries</span></span>
* [<span data-ttu-id="02239-281">Creare i dashboard</span><span class="sxs-lookup"><span data-stu-id="02239-281">Create dashboards</span></span>](app-insights-dashboards.md)

<span data-ttu-id="02239-282">Aggiungere altri dati di telemetria:</span><span class="sxs-lookup"><span data-stu-id="02239-282">Add more telemetry:</span></span>

* <span data-ttu-id="02239-283">[Creare test web] [ availability] toomake che il sito rimane in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="02239-283">[Create web tests][availability] toomake sure your site stays live.</span></span>
* <span data-ttu-id="02239-284">[Aggiungi telemetria di client web] [ usage] toosee eccezioni dal codice della pagina web e si inserisce toolet tenere traccia delle chiamate.</span><span class="sxs-lookup"><span data-stu-id="02239-284">[Add web client telemetry][usage] toosee exceptions from web page code and toolet you insert trace calls.</span></span>
* <span data-ttu-id="02239-285">[Aggiungere il codice di Application Insights SDK tooyour] [ greenbrown] in modo che sia possibile inserire una traccia e registrare le chiamate</span><span class="sxs-lookup"><span data-stu-id="02239-285">[Add Application Insights SDK tooyour code][greenbrown] so that you can insert trace and log calls</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[roles]: app-insights-resources-roles-access-control.md
[usage]: app-insights-javascript.md
