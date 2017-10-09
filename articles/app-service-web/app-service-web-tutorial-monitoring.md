---
title: un'App Web aaaMonitor | Documenti Microsoft
description: Informazioni su come tooset di monitoraggio nell'App Web
services: App-Service
keywords: 
author: btardif
ms.author: byvinyal
ms.date: 04/04/2017
ms.topic: article
ms.service: app-service-web
ms.openlocfilehash: c2f5e9842c732a804f1caee5d67e53dad24e190a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-app-service"></a><span data-ttu-id="32b14-103">Monitorare il servizio app</span><span class="sxs-lookup"><span data-stu-id="32b14-103">Monitor App Service</span></span>
<span data-ttu-id="32b14-104">In questa esercitazione illustra il monitoraggio dell'applicazione e l'utilizzo di problemi di toosolve hello piattaforma incorporata strumenti quando si verificano.</span><span class="sxs-lookup"><span data-stu-id="32b14-104">This tutorial walks you through monitoring your app and using hello built-in platform tools toosolve problems when they occur.</span></span>

<span data-ttu-id="32b14-105">Ogni sezione di questo documento illustra una funzionalità specifica.</span><span class="sxs-lookup"><span data-stu-id="32b14-105">Each section of this document goes over a specific feature.</span></span> <span data-ttu-id="32b14-106">Uso combinato hello funzionalità consentono di:</span><span class="sxs-lookup"><span data-stu-id="32b14-106">Using hello features together let you:</span></span>
- <span data-ttu-id="32b14-107">Identificare un problema nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="32b14-107">Identifying an issue in your app.</span></span>
- <span data-ttu-id="32b14-108">Determinare quando hello è causato dalla piattaforma hello o codice.</span><span class="sxs-lookup"><span data-stu-id="32b14-108">Determining when hello issue is caused by your code or hello platform.</span></span>
- <span data-ttu-id="32b14-109">Restringere causa hello hello problema nel codice.</span><span class="sxs-lookup"><span data-stu-id="32b14-109">Narrow down hello source of hello problem in your code.</span></span>
- <span data-ttu-id="32b14-110">Debug e risoluzione problema hello.</span><span class="sxs-lookup"><span data-stu-id="32b14-110">Debugging and fixing hello issue.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="32b14-111">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="32b14-111">Before you begin</span></span>
- <span data-ttu-id="32b14-112">È necessario un toomonitor App Web e seguire hello descritti passaggi.</span><span class="sxs-lookup"><span data-stu-id="32b14-112">You need a Web App toomonitor and follow hello outlined steps.</span></span>
    - <span data-ttu-id="32b14-113">È possibile creare un'applicazione hello passaggi descritti in hello [creare un'applicazione ASP.NET in Azure con il Database SQL](app-service-web-tutorial-dotnet-sqldatabase.md) esercitazione.</span><span class="sxs-lookup"><span data-stu-id="32b14-113">You can create an application following hello steps described in hello [Create an ASP.NET app in Azure with SQL Database](app-service-web-tutorial-dotnet-sqldatabase.md) tutorial.</span></span>

- <span data-ttu-id="32b14-114">Se si desidera tootry out **il debug remoto** dell'applicazione, è necessario Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="32b14-114">If you want tootry out **Remote Debugging** of your application, you need Visual Studio.</span></span>
    - <span data-ttu-id="32b14-115">Se si dispone già di Visual Studio 2017, che installata, è possibile scaricare e utilizzare hello libero [2017 di Visual Studio Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="32b14-115">If you don’t already have Visual Studio 2017 installed, you can download and use hello free [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span>
    - <span data-ttu-id="32b14-116">Assicurarsi di abilitare **lo sviluppo di Azure** durante l'installazione di Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="32b14-116">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

## <span data-ttu-id="32b14-117"><a name="metrics"></a>Passaggio 1: visualizzare le metriche</span><span class="sxs-lookup"><span data-stu-id="32b14-117"><a name="metrics"></a> Step 1 - View metrics</span></span>
<span data-ttu-id="32b14-118">**Metriche** toounderstand utili sono:</span><span class="sxs-lookup"><span data-stu-id="32b14-118">**Metrics** are useful toounderstand:</span></span>
- <span data-ttu-id="32b14-119">Integrità dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="32b14-119">Application health</span></span>
- <span data-ttu-id="32b14-120">Prestazioni dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="32b14-120">App performance</span></span>
- <span data-ttu-id="32b14-121">Utilizzo di risorse</span><span class="sxs-lookup"><span data-stu-id="32b14-121">Resource consumption</span></span>

<span data-ttu-id="32b14-122">Quando si analizzano i problemi di un'applicazione, esaminare le metriche è toostart un buon punto.</span><span class="sxs-lookup"><span data-stu-id="32b14-122">When investigating an application issue, reviewing metrics is a good place toostart.</span></span> <span data-ttu-id="32b14-123">Portale di Azure è toovisually un modo rapido controllare metriche di hello dell'app utilizzando **Monitor Azure**.</span><span class="sxs-lookup"><span data-stu-id="32b14-123">Azure portal has a quick way toovisually inspect hello metrics of your app using **Azure Monitor**.</span></span>

<span data-ttu-id="32b14-124">Le metriche forniscono una visualizzazione cronologica in numerose aggregazioni chiave per l'app.</span><span class="sxs-lookup"><span data-stu-id="32b14-124">Metrics provide a historical view across several key aggregations for your app.</span></span> <span data-ttu-id="32b14-125">Per qualsiasi applicazione ospitata nel servizio app, è necessario monitorare hello App Web sia hello piano di servizio App.</span><span class="sxs-lookup"><span data-stu-id="32b14-125">For any app hosted in app service, you should monitor both hello Web App and hello App Service plan.</span></span>

> [!NOTE]
> <span data-ttu-id="32b14-126">Un piano di servizio App rappresenta raccolta hello di risorse fisiche utilizzate toohost app.</span><span class="sxs-lookup"><span data-stu-id="32b14-126">An App Service plan represents hello collection of physical resources used toohost your apps.</span></span> <span data-ttu-id="32b14-127">Tutte le applicazioni assegnate tooan risorse hello condivisione piano di servizio App da essa consentendo toosave costo quando più applicazioni di hosting definite.</span><span class="sxs-lookup"><span data-stu-id="32b14-127">All applications assigned tooan App Service plan share hello resources defined by it allowing you toosave cost when hosting multiple apps.</span></span>
>
> <span data-ttu-id="32b14-128">I piani di servizio app definiscono:</span><span class="sxs-lookup"><span data-stu-id="32b14-128">App Service plans define:</span></span>
> * <span data-ttu-id="32b14-129">Area: Europa settentrionale, Stati Uniti orientali, Asia sud-orientale e così via.</span><span class="sxs-lookup"><span data-stu-id="32b14-129">Region: North Europe, East US, Southeast Asia, etc.</span></span>
> * <span data-ttu-id="32b14-130">Dimensione dell'istanza: Small, Medium, Large e così via.</span><span class="sxs-lookup"><span data-stu-id="32b14-130">Instance Size: Small, Medium, Large, etc.</span></span>
> * <span data-ttu-id="32b14-131">Numero di scala: una, due o tre istanze e così via.</span><span class="sxs-lookup"><span data-stu-id="32b14-131">Scale Count: one, two, or three instances, etc.</span></span>
> * <span data-ttu-id="32b14-132">SKU: Free, Shared, Basic, Standard, Premium e così via.</span><span class="sxs-lookup"><span data-stu-id="32b14-132">SKU: Free, Shared, Basic, Standard, Premium, etc.</span></span>

<span data-ttu-id="32b14-133">metriche tooreview per l'App Web, visita toohello **Panoramica** pannello App hello desiderato toomonitor.</span><span class="sxs-lookup"><span data-stu-id="32b14-133">tooreview metrics for your Web App, go toohello **Overview** blade of hello app you want toomonitor.</span></span> <span data-ttu-id="32b14-134">A questo punto, è possibile visualizzare un grafico per le metriche dell'app come un **riquadro Monitoraggio**.</span><span class="sxs-lookup"><span data-stu-id="32b14-134">From here, you can view a chart for your app's metrics as a **Monitoring tile**.</span></span> <span data-ttu-id="32b14-135">Fare clic su tooedit riquadro hello e configurare quali tooview metriche e hello toodisplay intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="32b14-135">Click hello tile tooedit and configure what metrics tooview and hello time range toodisplay.</span></span>

<span data-ttu-id="32b14-136">Dal pannello della risorsa predefinita hello fornisce una visualizzazione per le richieste dell'applicazione hello e gli errori per hello ultima ora.</span><span class="sxs-lookup"><span data-stu-id="32b14-136">By default hello resource blade provides a view for hello Application Requests and errors for hello last hour.</span></span>
<span data-ttu-id="32b14-137">![Monitorare un'app](media/app-service-web-tutorial-monitoring/app-service-monitor.png)</span><span class="sxs-lookup"><span data-stu-id="32b14-137">![Monitor App](media/app-service-web-tutorial-monitoring/app-service-monitor.png)</span></span>

<span data-ttu-id="32b14-138">Come si può notare nell'esempio hello, disporre di un'applicazione che genera molti **errori Server HTTP**.</span><span class="sxs-lookup"><span data-stu-id="32b14-138">As you can see in hello example, we have an application that is generating many **HTTP Server Errors**.</span></span> <span data-ttu-id="32b14-139">numero elevato di errori Hello è prima indicazione hello dobbiamo tooinvestigate questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="32b14-139">hello high volume of errors is hello first indication we need tooinvestigate this application.</span></span>

> [!TIP]
> <span data-ttu-id="32b14-140">Ulteriori informazioni sul monitoraggio di Azure con hello seguenti collegamenti:</span><span class="sxs-lookup"><span data-stu-id="32b14-140">Learn more about Azure Monitor with hello following links:</span></span>
> - [<span data-ttu-id="32b14-141">Introduzione al monitoraggio di Azure</span><span class="sxs-lookup"><span data-stu-id="32b14-141">Get started with Azure Monitor</span></span>](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [<span data-ttu-id="32b14-142">Metriche di Azure</span><span class="sxs-lookup"><span data-stu-id="32b14-142">Azure Metrics</span></span>](..\monitoring-and-diagnostics\monitoring-overview-metrics.md)
> - [<span data-ttu-id="32b14-143">Metriche supportate con il monitoraggio di Azure</span><span class="sxs-lookup"><span data-stu-id="32b14-143">Supported metrics with Azure Monitor</span></span>](..\monitoring-and-diagnostics\monitoring-supported-metrics.md)
> - [<span data-ttu-id="32b14-144">Dashboard di Azure</span><span class="sxs-lookup"><span data-stu-id="32b14-144">Azure Dashboards</span></span>](..\azure-portal\azure-portal-dashboards.md)

## <span data-ttu-id="32b14-145"><a name="alerts"></a> Passaggio 2: configurare gli avvisi</span><span class="sxs-lookup"><span data-stu-id="32b14-145"><a name="alerts"></a> Step 2 - Configure Alerts</span></span>
<span data-ttu-id="32b14-146">**Avvisi** può essere configurato tootrigger condizioni specifiche per l'app.</span><span class="sxs-lookup"><span data-stu-id="32b14-146">**Alerts** can be configured tootrigger on specific conditions for your app.</span></span>

<span data-ttu-id="32b14-147">In [passaggio 1 - metriche vista](#metrics), abbiamo visto che un'applicazione hello ha un numero elevato di errori.</span><span class="sxs-lookup"><span data-stu-id="32b14-147">In [Step 1 - View metrics](#metrics), we saw that hello application had a high number of errors.</span></span>

<span data-ttu-id="32b14-148">Consente di configurare un avviso tooautomatically ricevere notifiche quando si verificano errori.</span><span class="sxs-lookup"><span data-stu-id="32b14-148">Lets configure an alert tooautomatically get notified when errors occur.</span></span> <span data-ttu-id="32b14-149">In questo caso, si desidera toosend avviso hello e di posta elettronica ogni volta che il numero di hello di errori HTTP 50 X supera una determinata soglia.</span><span class="sxs-lookup"><span data-stu-id="32b14-149">In this case, we want hello alert toosend and e-mail every time hello number of HTTP 50X errors goes over a certain threshold.</span></span>

<span data-ttu-id="32b14-150">toocreate un avviso, passare troppo**monitoraggio** > **avvisi** e fare clic su **[+] Aggiungi avviso**.</span><span class="sxs-lookup"><span data-stu-id="32b14-150">toocreate an alert, navigate too**Monitoring** > **Alerts** and click **[+] Add Alert**.</span></span>

![Avvisi](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts.png)

<span data-ttu-id="32b14-152">Fornire valori per la configurazione di avviso hello:</span><span class="sxs-lookup"><span data-stu-id="32b14-152">Provide values for hello Alert configuration:</span></span>
- <span data-ttu-id="32b14-153">**Risorse:** hello toomonitor sito con avviso hello.</span><span class="sxs-lookup"><span data-stu-id="32b14-153">**Resource:** hello site toomonitor with hello alert.</span></span>
- <span data-ttu-id="32b14-154">**Nome:** un nome per l'avviso, in questo caso: *Troppi HTTP 50X*.</span><span class="sxs-lookup"><span data-stu-id="32b14-154">**Name:** A name for your alert, in this case: *High HTTP 50X*.</span></span>
- <span data-ttu-id="32b14-155">**Descrizione:** spiegazione in formato testo normale di cosa sta monitorando questo avviso.</span><span class="sxs-lookup"><span data-stu-id="32b14-155">**Description:** Plain text explanation of what this alert is looking at.</span></span>
- <span data-ttu-id="32b14-156">**Avviso per:** gli avvisi possono monitorare Metriche o Eventi, in questo esempio monitoreremo le metriche.</span><span class="sxs-lookup"><span data-stu-id="32b14-156">**Alert on:** Alerts can look at Metrics or Events, for this example we are looking at metrics.</span></span>
- <span data-ttu-id="32b14-157">**Metrica:** quali toomonitor metrica, in questo caso: *errori Server HTTP*.</span><span class="sxs-lookup"><span data-stu-id="32b14-157">**Metric:** What metric toomonitor, in this case: *HTTP Server Errors*.</span></span>
- <span data-ttu-id="32b14-158">**Condizione:** quando tooalert, in questo caso selezionare hello *maggiore* opzione.</span><span class="sxs-lookup"><span data-stu-id="32b14-158">**Condition:** When tooalert, in this case select hello *greater than* option.</span></span>
- <span data-ttu-id="32b14-159">**Soglia:** novità toolook valore, in questo caso: *400*.</span><span class="sxs-lookup"><span data-stu-id="32b14-159">**Threshold:** What is value toolook for, in this case: *400*.</span></span>
- <span data-ttu-id="32b14-160">**Periodo:** gli avvisi di operare su valore medio di hello di una metrica.</span><span class="sxs-lookup"><span data-stu-id="32b14-160">**Period:** Alerts operate over hello average value of a metric.</span></span> <span data-ttu-id="32b14-161">Per i periodi di tempo più ristretti, gli avvisi sensibili vengono sospesi.</span><span class="sxs-lookup"><span data-stu-id="32b14-161">Smaller periods of time yield more sensitive alerts.</span></span> <span data-ttu-id="32b14-162">In questo caso, consideriamo *5 minuti*.</span><span class="sxs-lookup"><span data-stu-id="32b14-162">in this case we are looking at *5 Minutes*.</span></span>
- <span data-ttu-id="32b14-163">**Invia messaggio di posta elettronica a proprietari e collaboratori:** in questo caso *Abilitato*.</span><span class="sxs-lookup"><span data-stu-id="32b14-163">**Email Owners and contributors:** in this case: *Enabled*.</span></span>

<span data-ttu-id="32b14-164">Dopo aver creato hello avviso tramite posta elettronica viene inviato ogni volta che hello app supera la soglia configurata di hello.</span><span class="sxs-lookup"><span data-stu-id="32b14-164">Now that hello alert is created an email is sent every time hello app goes over hello configured threshold.</span></span> <span data-ttu-id="32b14-165">Gli avvisi attivi possono anche essere rivista in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="32b14-165">Active alerts can also be reviewed in hello Azure portal.</span></span>

![Avvisi attivati](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts-triggered.png)


> [!TIP]
> <span data-ttu-id="32b14-167">Altre informazioni sugli avvisi di Azure con hello seguenti collegamenti:</span><span class="sxs-lookup"><span data-stu-id="32b14-167">Learn more about Azure Alerts with hello following links:</span></span>
> - [<span data-ttu-id="32b14-168">Cosa sono gli avvisi in Microsoft Azure?</span><span class="sxs-lookup"><span data-stu-id="32b14-168">What are alerts in Microsoft Azure</span></span>](..\monitoring-and-diagnostics\monitoring-overview-alerts.md)
> - [<span data-ttu-id="32b14-169">Eseguire operazioni sulle metriche</span><span class="sxs-lookup"><span data-stu-id="32b14-169">Take Action On Metrics</span></span>](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [<span data-ttu-id="32b14-170">Creare avvisi delle metriche</span><span class="sxs-lookup"><span data-stu-id="32b14-170">Create metric alerts</span></span>](..\monitoring-and-diagnostics\insights-alerts-portal.md)

## <span data-ttu-id="32b14-171"><a name="companion"></a> Passaggio 3: App Service Companion</span><span class="sxs-lookup"><span data-stu-id="32b14-171"><a name="companion"></a> Step 3 - App Service Companion</span></span>
<span data-ttu-id="32b14-172">**Complementare di servizio app** offre un modo pratico di toomonitor dell'app con un'esperienza nativa nel dispositivo mobile (iOS e Android).</span><span class="sxs-lookup"><span data-stu-id="32b14-172">**App Service companion** offers a convenient way toomonitor your app with a native experience in your mobile device (iOS or Android).</span></span>

<span data-ttu-id="32b14-173">Usare App Service Companion per:</span><span class="sxs-lookup"><span data-stu-id="32b14-173">Use App Service Companion to:</span></span>
- <span data-ttu-id="32b14-174">Rivedere le metriche dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="32b14-174">Review application metrics</span></span>
- <span data-ttu-id="32b14-175">Rivedere ed eseguire azioni su avvisi e suggerimenti dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="32b14-175">Review and act on application alerts and recommendations</span></span>
- <span data-ttu-id="32b14-176">Base per la risoluzione (Sfoglia, start, stop, riavvio hello app)</span><span class="sxs-lookup"><span data-stu-id="32b14-176">Perform basic troubleshooting (browse, start, stop, restart hello app)</span></span>
- <span data-ttu-id="32b14-177">Ottenere notifiche push per gli eventi critici.</span><span class="sxs-lookup"><span data-stu-id="32b14-177">Get push notifications for critical events.</span></span>

![App Service Companion](media/app-service-web-tutorial-monitoring/app-service-companion.png)

<span data-ttu-id="32b14-179">[![App Service Companion in App Store](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![App Service Companion in Google Play](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span><span class="sxs-lookup"><span data-stu-id="32b14-179">[![App Service Companion App Store](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![App Service Companion Google Play](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span></span>

<span data-ttu-id="32b14-180">È possibile installare complementare di servizio App hello [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) o [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span><span class="sxs-lookup"><span data-stu-id="32b14-180">You can install App Service companion from hello [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) or [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span></span>

## <span data-ttu-id="32b14-181"><a name="diagnose"></a> Passaggio 4: diagnostica e risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="32b14-181"><a name="diagnose"></a> Step 4 - Diagnose and solve problems</span></span>
<span data-ttu-id="32b14-182">La **diagnostica e risoluzione dei problemi** consente di separare i problemi legati all'app da quelli legati alla piattaforma.</span><span class="sxs-lookup"><span data-stu-id="32b14-182">**Diagnose and solve problems** helps you separate application issues form platform issues.</span></span> <span data-ttu-id="32b14-183">Può inoltre indicare soluzioni correttive possibili tooget toohealthy di back-l'App Web.</span><span class="sxs-lookup"><span data-stu-id="32b14-183">It can also suggest possible mitigations tooget your Web App back toohealthy.</span></span>

![Diagnostica e risoluzione dei problemi](media/app-service-web-tutorial-monitoring/app-service-monitor-diagnosis.png)

<span data-ttu-id="32b14-185">Continuare con i passaggi precedenti form di esempio hello, possiamo vedere che un'applicazione hello è stata problemi di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="32b14-185">Continuing with hello example form previous steps, we can see that hello application has been having availably issues.</span></span> <span data-ttu-id="32b14-186">Al contrario, la disponibilità di hello piattaforma non è stato spostato dal 100%.</span><span class="sxs-lookup"><span data-stu-id="32b14-186">In contrast, hello platform availability has not moved from 100%.</span></span>

<span data-ttu-id="32b14-187">Quando l'app hello in caso di problema e hello rimane piattaforma backup, è una chiara indicazione che si sta gestiscono i problemi di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="32b14-187">When hello app is having issue and hello platform stays up, it's a clear indication that we are dealing with an application issue.</span></span>

## <span data-ttu-id="32b14-188"><a name="logging"></a> Passaggio 5: registrazione</span><span class="sxs-lookup"><span data-stu-id="32b14-188"><a name="logging"></a> Step 5 - Logging</span></span>
<span data-ttu-id="32b14-189">Ora che è stato limitato, problema di hello errori tooan dell'applicazione, è possibile esaminare in tooget di registri applicazioni e server hello ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="32b14-189">Now that we have narrowed down hello failures tooan application issue, we can look at hello application and server logs tooget more information.</span></span>

<span data-ttu-id="32b14-190">La registrazione consente toocollect entrambi **Application Diagnostics** e **diagnostica del Server Web** log per l'App Web.</span><span class="sxs-lookup"><span data-stu-id="32b14-190">Logging allows you toocollect both **Application Diagnostics** and **Web Server Diagnostics** logs for your Web App.</span></span>

### <a name="application-diagnostics"></a><span data-ttu-id="32b14-191">Diagnostica applicazioni</span><span class="sxs-lookup"><span data-stu-id="32b14-191">Application Diagnostics</span></span>
<span data-ttu-id="32b14-192">Diagnostica delle applicazioni consente si toocapture le tracce prodotte da un'applicazione hello in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="32b14-192">Application diagnostics allows you toocapture traces produced by hello application at runtime.</span></span>

<span data-ttu-id="32b14-193">Aggiunta di funzionalità di traccia tooyour applicazione migliora notevolmente il possibilità toodebug e problemi di punto di blocco.</span><span class="sxs-lookup"><span data-stu-id="32b14-193">Adding tracing tooyour application greatly improves your ability toodebug and pin-point issues.</span></span>

<span data-ttu-id="32b14-194">In ASP.NET, è possibile registrare le tracce di applicazione utilizzando [classe Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) eventi toogenerate acquisite dall'infrastruttura di log hello.</span><span class="sxs-lookup"><span data-stu-id="32b14-194">In ASP.NET, you can log application traces using [System.Diagnostics.Trace class](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) toogenerate events that are captured by hello log infrastructure.</span></span> <span data-ttu-id="32b14-195">È inoltre possibile specificare la gravità hello di traccia hello per il filtro più semplice.</span><span class="sxs-lookup"><span data-stu-id="32b14-195">You can also specify hello severity of hello trace for easier filtering.</span></span>

```csharp
public ActionResult Delete(Guid? id)
{
    System.Diagnostics.Trace.TraceInformation("GET /Todos/Delete/" + id);
    if (id == null)
    {
        System.Diagnostics.Trace.TraceError("/Todos/Delete/ failed, ID is null");
        return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
    }
    Todo todo = db.Todoes.Find(id);
    if (todo == null)
    {
        System.Diagnostics.Trace.TraceWarning("/Todos/Delete/ failed, ID: " + id + " could not be found");
        return HttpNotFound();
    }
    System.Diagnostics.Trace.TraceInformation("GET /Todos/Delete/" + id + "completed successfully");
    return View(todo);
}
```
<span data-ttu-id="32b14-196">registrazione applicazioni tooenable andare troppo**monitoraggio** > **i log di diagnostica** e abilitare la registrazione delle applicazioni utilizzando gli elementi Toggle hello.</span><span class="sxs-lookup"><span data-stu-id="32b14-196">tooenable Application logging Go too**Monitoring** > **Diagnostic Logs** and Enable Application Logging using hello toggles.</span></span>

![Monitorare un'app](media/app-service-web-tutorial-monitoring/app-service-monitor-applogs.png)

<span data-ttu-id="32b14-198">Log applicazioni possono essere il sistema di file dell'App Web tooyour stored o distribuirli tooblob archiviazione.</span><span class="sxs-lookup"><span data-stu-id="32b14-198">Application logs can be stored tooyour Web App's file system or pushed out tooblob storage.</span></span> <span data-ttu-id="32b14-199">Per gli scenari di produzione, è consigliato toouse nell'archiviazione blob.</span><span class="sxs-lookup"><span data-stu-id="32b14-199">For production scenarios, it's recommended toouse blob storage.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="32b14-200">L'abilitazione della registrazione ha effetto sulle prestazioni dell'applicazione e l'uso delle risorse.</span><span class="sxs-lookup"><span data-stu-id="32b14-200">Enabling logging has an impact on your application performance and resource utilization.</span></span> <span data-ttu-id="32b14-201">Per gli scenari di produzione è consigliabile usare i log degli errori.</span><span class="sxs-lookup"><span data-stu-id="32b14-201">For production scenarios, error logs are recommended.</span></span> <span data-ttu-id="32b14-202">Abilitare una registrazione più dettagliata solo durante l'analisi dei problemi.</span><span class="sxs-lookup"><span data-stu-id="32b14-202">Only enable more verbose logging when investigating issues.</span></span>

 ### <a name="web-server-diagnostics"></a><span data-ttu-id="32b14-203">Diagnostica del server Web</span><span class="sxs-lookup"><span data-stu-id="32b14-203">Web Server Diagnostics</span></span>
<span data-ttu-id="32b14-204">I log del server Web vengono generati anche se l'app non è instrumentata.</span><span class="sxs-lookup"><span data-stu-id="32b14-204">Web Server logs are generated even if your app is not instrumented.</span></span> <span data-ttu-id="32b14-205">Il servizio app consente di raccogliere tre tipi diversi di log del server:</span><span class="sxs-lookup"><span data-stu-id="32b14-205">App Service can collect three different types of server logs:</span></span>

- <span data-ttu-id="32b14-206">**Registrazione del server Web**</span><span class="sxs-lookup"><span data-stu-id="32b14-206">**Web Server Logging**</span></span>
    - <span data-ttu-id="32b14-207">Informazioni sulle transazioni HTTP tramite hello [formato di file registro esteso W3C](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span><span class="sxs-lookup"><span data-stu-id="32b14-207">Information about HTTP transactions using hello [W3C extended log file format](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span></span>
    - <span data-ttu-id="32b14-208">È utile quando si determinano le metriche di generale del sito, ad esempio il numero di hello di richieste gestite o il numero di richieste provengono da un indirizzo IP specifico.</span><span class="sxs-lookup"><span data-stu-id="32b14-208">Useful when determining overall site metrics such as hello number of requests handled or how many requests are from a specific IP address.</span></span>
- <span data-ttu-id="32b14-209">**Registrazione degli errori dettagliata**</span><span class="sxs-lookup"><span data-stu-id="32b14-209">**Detailed Error Logging**</span></span>
    - <span data-ttu-id="32b14-210">Informazioni dettagliate sugli errori relativi ai codici di stato HTTP che indicano un'operazione non riuscita (codice di stato 400 o superiore).</span><span class="sxs-lookup"><span data-stu-id="32b14-210">Detailed error information for HTTP status codes that indicate a failure (status code 400 or greater).</span></span>
    - [<span data-ttu-id="32b14-211">Altre informazioni sulla registrazione degli errori dettagliata</span><span class="sxs-lookup"><span data-stu-id="32b14-211">Learn more about detailed error logging</span></span>](https://www.iis.net/learn/troubleshoot/diagnosing-http-errors/how-to-use-http-detailed-errors-in-iis)
- <span data-ttu-id="32b14-212">**Traccia delle richieste non riuscite**</span><span class="sxs-lookup"><span data-stu-id="32b14-212">**Failed Request Tracing**</span></span>
    - <span data-ttu-id="32b14-213">Informazioni dettagliate sulle richieste non riuscite, inclusa un'analisi dei componenti IIS hello utilizzato tooprocess hello richiesta e hello tempo impiegato in ogni componente.</span><span class="sxs-lookup"><span data-stu-id="32b14-213">Detailed information on failed requests, including a trace of hello IIS components used tooprocess hello request and hello time taken in each component.</span></span>
    - <span data-ttu-id="32b14-214">Registri richieste non riuscite sono utili quando si tenta di tooisolate causa un errore HTTP specifico.</span><span class="sxs-lookup"><span data-stu-id="32b14-214">Failed request logs are useful when trying tooisolate what is causing a specific HTTP error.</span></span>
    - [<span data-ttu-id="32b14-215">Altre informazioni sulla traccia delle richieste non riuscite</span><span class="sxs-lookup"><span data-stu-id="32b14-215">Learn more about failed request tracing</span></span>](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis)

<span data-ttu-id="32b14-216">registrazione del Server tooenable:</span><span class="sxs-lookup"><span data-stu-id="32b14-216">tooenable Server logging:</span></span>
- <span data-ttu-id="32b14-217">andare troppo**monitoraggio** > **i log di diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="32b14-217">go too**Monitoring** > **Diagnostic Logs**.</span></span>
- <span data-ttu-id="32b14-218">Abilitare tipi diversi di hello di diagnostica del Server Web utilizzando gli elementi Toggle hello.</span><span class="sxs-lookup"><span data-stu-id="32b14-218">Enable hello different types of Web Server Diagnostics using hello toggles.</span></span>

![Monitorare un'app](media/app-service-web-tutorial-monitoring/app-service-monitor-serverlogs.png)

> [!IMPORTANT]
> <span data-ttu-id="32b14-220">L'abilitazione della registrazione ha effetto sulle prestazioni dell'applicazione e l'uso delle risorse.</span><span class="sxs-lookup"><span data-stu-id="32b14-220">Enabling logging has an impact on your application performance and resource utilization.</span></span> <span data-ttu-id="32b14-221">Per gli scenari di produzione è consigliabile usare i log degli errori. Abilitare una registrazione più dettagliata solo durante l'analisi dei problemi.</span><span class="sxs-lookup"><span data-stu-id="32b14-221">For Production Scenarios, Error logs are recommended, Only Enable more verbose logging when investigating issues.</span></span>

### <a name="accessing-logs"></a><span data-ttu-id="32b14-222">Accesso ai log</span><span class="sxs-lookup"><span data-stu-id="32b14-222">Accessing Logs</span></span>
<span data-ttu-id="32b14-223">I log memorizzati nell'archiviazione BLOB sono accessibili tramite Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="32b14-223">Logs stored in blob storage are accessed using Azure Storage Explorer.</span></span> <span data-ttu-id="32b14-224">Registri archiviati nel file System dell'App Web hello sono accessibili tramite FTP in hello seguenti percorsi:</span><span class="sxs-lookup"><span data-stu-id="32b14-224">Logs stored in hello Web App's filesystem are accessed through FTP under hello following paths:</span></span>

- <span data-ttu-id="32b14-225">**Log applicazioni** - `%HOME%/LogFiles/Application/`.</span><span class="sxs-lookup"><span data-stu-id="32b14-225">**Application logs** - `%HOME%/LogFiles/Application/`.</span></span>
    - <span data-ttu-id="32b14-226">In questa cartella sono presenti uno o più file di testo contenenti le informazioni generate dalla registrazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="32b14-226">This folder contains one or more text files containing information produced by application logging.</span></span>
- <span data-ttu-id="32b14-227">**Traccia delle richieste non riuscite** - `%HOME%/LogFiles/W3SVC#########/`.</span><span class="sxs-lookup"><span data-stu-id="32b14-227">**Failed Request Traces** - `%HOME%/LogFiles/W3SVC#########/`.</span></span>
    - <span data-ttu-id="32b14-228">Questa cartella contiene un file XSL e uno o più file XML.</span><span class="sxs-lookup"><span data-stu-id="32b14-228">This folder contains an XSL file and one or more XML files.</span></span>
- <span data-ttu-id="32b14-229">**Registrazione degli errori dettagliata** - `%HOME%/LogFiles/DetailedErrors/`.</span><span class="sxs-lookup"><span data-stu-id="32b14-229">**Detailed Error Logs** - `%HOME%/LogFiles/DetailedErrors/`.</span></span>
    - <span data-ttu-id="32b14-230">Questa cartella contiene uno o più file con estensione htm con informazioni dettagliate sugli errori HTTP generati dall'app.</span><span class="sxs-lookup"><span data-stu-id="32b14-230">This folder contains one or more .htm files with extensive information on HTTP errors generated by your app.</span></span>
- <span data-ttu-id="32b14-231">**Log del server Web** - `%HOME%/LogFiles/http/RawLogs`.</span><span class="sxs-lookup"><span data-stu-id="32b14-231">**Web Server Logs** - `%HOME%/LogFiles/http/RawLogs`.</span></span>
    - <span data-ttu-id="32b14-232">Questa cartella contiene uno o più file di testo formattati con formato del file registro esteso W3C hello.</span><span class="sxs-lookup"><span data-stu-id="32b14-232">This folder contains one or more text files formatted using hello W3C extended log file format.</span></span>

## <span data-ttu-id="32b14-233"><a name="streaming"></a> Passaggio 6: streaming dei log</span><span class="sxs-lookup"><span data-stu-id="32b14-233"><a name="streaming"></a> Step 6 - Log Streaming</span></span>
<span data-ttu-id="32b14-234">I log di streaming sono particolarmente utili quando il debug di un'applicazione, poiché consente di risparmiare tempo confrontato troppo[accesso ai registri hello](#Accessing-Logs) tramite FTP.</span><span class="sxs-lookup"><span data-stu-id="32b14-234">Streaming logs are convenient when debugging an application since it saves time compared too[accessing hello logs](#Accessing-Logs) through FTP.</span></span>

<span data-ttu-id="32b14-235">Il servizio app può eseguire lo streaming dei **Log applicazione** e dei **Log del server Web** generati.</span><span class="sxs-lookup"><span data-stu-id="32b14-235">App Service can stream **Application Logs** and **Web Server Logs** as they are generated.</span></span>

> [!TIP]
> <span data-ttu-id="32b14-236">Prima di tentare di registri toostream, assicurarsi che è stata attivata la raccolta dei registri, come descritto in hello [registrazione](#logging) sezione.</span><span class="sxs-lookup"><span data-stu-id="32b14-236">Before trying toostream logs, make sure you have enabled collecting logs as described in hello [Logging](#logging) section.</span></span>

<span data-ttu-id="32b14-237">log toostream, andare troppo**monitoraggio**> **flusso del Log**.</span><span class="sxs-lookup"><span data-stu-id="32b14-237">toostream logs, go too**Monitoring**> **Log Stream**.</span></span> <span data-ttu-id="32b14-238">Selezionare **Log applicazione** o **Log del server Web**, a seconda delle informazioni desiderate.</span><span class="sxs-lookup"><span data-stu-id="32b14-238">Select **Application Logs** or **Web server logs** depending what information you are looking for.</span></span> <span data-ttu-id="32b14-239">Da qui, è anche possibile sospendere, riavviare e cancellare il buffer di hello.</span><span class="sxs-lookup"><span data-stu-id="32b14-239">From here, you can also pause, restart, and clear hello buffer.</span></span>

![Log in streaming](media/app-service-web-tutorial-monitoring/app-service-monitor-logstream.png)

> [!TIP]
> <span data-ttu-id="32b14-241">I log vengono generati solo quando il traffico è hello App, è anche possibile aumentare il livello di dettaglio hello di registri tooget più eventi o informazioni.</span><span class="sxs-lookup"><span data-stu-id="32b14-241">Logs are only generated when there is traffic on hello app, you can also increase hello verbosity of logs tooget more events or information.</span></span>

## <span data-ttu-id="32b14-242"><a name="remote"></a> Passaggio 7 - Debug remoto</span><span class="sxs-lookup"><span data-stu-id="32b14-242"><a name="remote"></a> Step 7 - Remote Debugging</span></span>
<span data-ttu-id="32b14-243">Dopo avere origine a cui punta pin hello dei problemi di applicazioni di hello, utilizzare **il debug remoto** toowalk tramite codice hello.</span><span class="sxs-lookup"><span data-stu-id="32b14-243">Once you have pin-pointed hello source of hello applications problems, use **Remote Debugging** toowalk through hello code.</span></span>

<span data-ttu-id="32b14-244">Consente di debug remoto si collega un tooyour debugger App Web in esecuzione nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="32b14-244">Remote debugging lets you attach a debugger tooyour Web App running in hello cloud.</span></span> <span data-ttu-id="32b14-245">È possibile impostare i punti di interruzione, modificare direttamente memoria, esaminare il codice e cambiare anche percorso di codice hello come se si trattasse di un'app in esecuzione in locale.</span><span class="sxs-lookup"><span data-stu-id="32b14-245">You can set breakpoints, manipulate memory directly, step through code, and even change hello code path just like you do for an app running locally.</span></span>

<span data-ttu-id="32b14-246">tooattach hello debugger tooyour app in esecuzione nel cloud hello:</span><span class="sxs-lookup"><span data-stu-id="32b14-246">tooattach hello debugger tooyour app running in hello cloud:</span></span>

- <span data-ttu-id="32b14-247">Utilizzando Visual Studio 2017, soluzione hello aperto per l'applicazione hello desiderato toodebug</span><span class="sxs-lookup"><span data-stu-id="32b14-247">Using Visual Studio 2017, open hello solution for hello app you want toodebug</span></span>
- <span data-ttu-id="32b14-248">Impostare alcuni punti di interruzione esattamente come si farebbe per lo sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="32b14-248">Set some brake points just like you would for local development.</span></span>
- <span data-ttu-id="32b14-249">Aprire **Cloud Explorer** (CTRL+/, CTRL+X).</span><span class="sxs-lookup"><span data-stu-id="32b14-249">Open **cloud explorer** (ctr + /, ctrl + x).</span></span>
- <span data-ttu-id="32b14-250">Accedere con le credenziali di Azure.</span><span class="sxs-lookup"><span data-stu-id="32b14-250">Log in with your azure credentials as needed.</span></span>
- <span data-ttu-id="32b14-251">Trova hello app da toodebug</span><span class="sxs-lookup"><span data-stu-id="32b14-251">Find hello app you want toodebug</span></span>
- <span data-ttu-id="32b14-252">Selezionare **collega Debugger** hello modulo **azioni** riquadro.</span><span class="sxs-lookup"><span data-stu-id="32b14-252">Select **Attach Debugger** form hello **Actions** pane.</span></span>

![Debug remoto](media/app-service-web-tutorial-monitoring/app-service-monitor-vsdebug.png)

<span data-ttu-id="32b14-254">Visual Studio consente di configurare l'applicazione per il debug remoto e viene avviata una finestra del browser che consente di passare tooyour app.</span><span class="sxs-lookup"><span data-stu-id="32b14-254">Visual Studio configures your application for remote debugging and launches a browser window that navigates tooyour app.</span></span> <span data-ttu-id="32b14-255">Sfogliare i punti di interruzione tootrigger app e avanzare nel codice hello.</span><span class="sxs-lookup"><span data-stu-id="32b14-255">Browse through your app tootrigger break points and step through hello code.</span></span>

> [!WARNING]
> <span data-ttu-id="32b14-256">L'esecuzione in modalità debug in produzione non è una scelta consigliata.</span><span class="sxs-lookup"><span data-stu-id="32b14-256">Running in debug mode in production is not recommended.</span></span> <span data-ttu-id="32b14-257">Se l'applicazione di produzione non è scalare orizzontalmente toomultiple istanze del server, il debug di evitare hello del server web da richieste tooother risponde.</span><span class="sxs-lookup"><span data-stu-id="32b14-257">If your production app is not scaled out toomultiple server instances, debugging prevent hello web server from responding tooother requests.</span></span> <span data-ttu-id="32b14-258">Per risolvere i problemi di produzione, la risorsa migliore è troppo[configurare la registrazione](#logging) e [Application Insights](#insights).</span><span class="sxs-lookup"><span data-stu-id="32b14-258">For troubleshooting production problems, your best resource is too[configure logging](#logging) and [Application Insights](#insights).</span></span>



## <span data-ttu-id="32b14-259"><a name="explorer"></a> Passaggio 8: esplora processi</span><span class="sxs-lookup"><span data-stu-id="32b14-259"><a name="explorer"></a> Step 8 - Process Explorer</span></span>
<span data-ttu-id="32b14-260">Quando l'applicazione viene ampliato toomore più di un'istanza, **Esplora processi** consente di identificare i problemi specifici di istanza.</span><span class="sxs-lookup"><span data-stu-id="32b14-260">When your application is scaled out toomore than one instance, **process explorer** can help you identify instance specific problems.</span></span>

<span data-ttu-id="32b14-261">Usare **Esplora processi** per:</span><span class="sxs-lookup"><span data-stu-id="32b14-261">Use **Process Explorer** to:</span></span>

- <span data-ttu-id="32b14-262">Consente di enumerare tutti i processi di hello tra istanze diverse del piano di servizio App.</span><span class="sxs-lookup"><span data-stu-id="32b14-262">Enumerate all hello processes across different instances of your App Service plan.</span></span>
- <span data-ttu-id="32b14-263">Drill-down e visualizzare gli handle di hello e moduli associati a ogni processo.</span><span class="sxs-lookup"><span data-stu-id="32b14-263">Drill down and view hello handles and modules associated with each process.</span></span>
- <span data-ttu-id="32b14-264">Il numero di CPU di visualizzazione, Working Set e Thread a hello elaborare toohelp livello è identificare i processi per tale tipo</span><span class="sxs-lookup"><span data-stu-id="32b14-264">View CPU, Working Set, and Thread count at hello process level toohelp you identify runaway processes</span></span>
- <span data-ttu-id="32b14-265">Trovare gli handle di file aperti e terminare l'istanza di un processo specifico.</span><span class="sxs-lookup"><span data-stu-id="32b14-265">Find open file handles, and even kill a specific process instance.</span></span>

<span data-ttu-id="32b14-266">Esplora processi è disponibile in **Monitoraggio** > **Esplora processi**.</span><span class="sxs-lookup"><span data-stu-id="32b14-266">Process Explorer can be found under **Monitoring** > **Process Explorer**.</span></span>

![Esplora processi](media/app-service-web-tutorial-monitoring/app-service-monitor-processexplorer.png)


## <span data-ttu-id="32b14-268"><a name="insights"></a> Passaggio 9: Application Insights</span><span class="sxs-lookup"><span data-stu-id="32b14-268"><a name="insights"></a> Step 9 - Application Insights</span></span>
<span data-ttu-id="32b14-269">**Application Insights** offre funzionalità avanzate di profilatura e monitoraggio dell'app.</span><span class="sxs-lookup"><span data-stu-id="32b14-269">**Application Insights** provides application profiling and advanced monitoring capabilities for your app.</span></span>

<span data-ttu-id="32b14-270">Usare Application Insights toodetect e diagnosticare le eccezioni e i problemi di prestazioni nell'App Web.</span><span class="sxs-lookup"><span data-stu-id="32b14-270">Use Application Insights toodetect and diagnose exceptions and performance issues in your Web App.</span></span>

<span data-ttu-id="32b14-271">È possibile abilitare Application Insights per l'app Web in **Monitoraggio** > **Application Insights**</span><span class="sxs-lookup"><span data-stu-id="32b14-271">You can enable Application Insights for your Web App under **Monitoring** > **Application Insights**</span></span>

> [!NOTE]
> <span data-ttu-id="32b14-272">Application Insights potrebbe richiedere toostart tooinstall hello Application Insights sito estensione con la raccolta dei dati.</span><span class="sxs-lookup"><span data-stu-id="32b14-272">Application Insights might prompt you tooinstall hello Application Insights site extension toostart collecting data.</span></span> <span data-ttu-id="32b14-273">L'installazione dell'estensione del sito hello comporta il riavvio dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="32b14-273">Installing hello site extension causes an application restart.</span></span>

![Application Insights](media/app-service-web-tutorial-monitoring/app-service-monitor-appinsights.png)

<span data-ttu-id="32b14-275">Application Insights è una funzionalità avanzata, impostare toolearn, più collegamenti hello incluso in hello [passaggi successivi](#next) sezione.</span><span class="sxs-lookup"><span data-stu-id="32b14-275">Application Insights has a rich feature set, toolearn more, follow hello links included in hello [Next Steps](#next) section.</span></span>

## <span data-ttu-id="32b14-276"><a name="next"></a> Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="32b14-276"><a name="next"></a> Next steps</span></span>

 - [<span data-ttu-id="32b14-277">Informazioni su Azure Application Insights</span><span class="sxs-lookup"><span data-stu-id="32b14-277">What is Application Insights</span></span>](..\application-insights\app-insights-overview.md)
 - [<span data-ttu-id="32b14-278">Monitoraggio delle prestazioni dell'applicazione web di Azure</span><span class="sxs-lookup"><span data-stu-id="32b14-278">Monitor Azure web app performance with Application Insights</span></span>](..\application-insights\app-insights-azure-web-apps.md)
 - [<span data-ttu-id="32b14-279">Monitorare la disponibilità e la velocità di risposta dei siti Web</span><span class="sxs-lookup"><span data-stu-id="32b14-279">Monitor availability and responsiveness of any web site with Application Insights</span></span>](..\application-insights\app-insights-monitor-web-app-availability.md)
