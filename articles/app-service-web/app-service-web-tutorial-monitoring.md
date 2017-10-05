---
title: Monitorare un'app Web | Microsoft Docs
description: Informazioni su come configurare il monitoraggio nell'app Web
services: App-Service
keywords: 
author: btardif
ms.author: byvinyal
ms.date: 04/04/2017
ms.topic: article
ms.service: app-service-web
ms.openlocfilehash: 29df824062d00e01b786533033097948c008588f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-app-service"></a><span data-ttu-id="122f9-103">Monitorare il servizio app</span><span class="sxs-lookup"><span data-stu-id="122f9-103">Monitor App Service</span></span>
<span data-ttu-id="122f9-104">Questa esercitazione fornisce istruzioni dettagliate su come monitorare l'applicazione e usare gli strumenti della piattaforma predefinita per risolvere i problemi quando si verificano.</span><span class="sxs-lookup"><span data-stu-id="122f9-104">This tutorial walks you through monitoring your app and using the built-in platform tools to solve problems when they occur.</span></span>

<span data-ttu-id="122f9-105">Ogni sezione di questo documento illustra una funzionalità specifica.</span><span class="sxs-lookup"><span data-stu-id="122f9-105">Each section of this document goes over a specific feature.</span></span> <span data-ttu-id="122f9-106">Un utilizzo combinato delle funzionalità consente di:</span><span class="sxs-lookup"><span data-stu-id="122f9-106">Using the features together let you:</span></span>
- <span data-ttu-id="122f9-107">Identificare un problema nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="122f9-107">Identifying an issue in your app.</span></span>
- <span data-ttu-id="122f9-108">Determinare se il problema è causato dal codice o dalla piattaforma.</span><span class="sxs-lookup"><span data-stu-id="122f9-108">Determining when the issue is caused by your code or the platform.</span></span>
- <span data-ttu-id="122f9-109">Limitare l'origine del problema al codice.</span><span class="sxs-lookup"><span data-stu-id="122f9-109">Narrow down the source of the problem in your code.</span></span>
- <span data-ttu-id="122f9-110">Eseguire il debug e risolvere il problema.</span><span class="sxs-lookup"><span data-stu-id="122f9-110">Debugging and fixing the issue.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="122f9-111">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="122f9-111">Before you begin</span></span>
- <span data-ttu-id="122f9-112">Per monitorare e seguire la procedura descritta è necessaria un'app Web.</span><span class="sxs-lookup"><span data-stu-id="122f9-112">You need a Web App to monitor and follow the outlined steps.</span></span>
    - <span data-ttu-id="122f9-113">È possibile creare un'applicazione seguendo la procedura descritta nell'esercitazione [Creare un'app ASP.NET in Azure con un database SQL](app-service-web-tutorial-dotnet-sqldatabase.md).</span><span class="sxs-lookup"><span data-stu-id="122f9-113">You can create an application following the steps described in the [Create an ASP.NET app in Azure with SQL Database](app-service-web-tutorial-dotnet-sqldatabase.md) tutorial.</span></span>

- <span data-ttu-id="122f9-114">Se si vuole provare il **Debug remoto** dell'applicazione è necessario Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="122f9-114">If you want to try out **Remote Debugging** of your application, you need Visual Studio.</span></span>
    - <span data-ttu-id="122f9-115">Se Visual Studio 2017 non è ancora installato, è possibile scaricare e usare la versione gratuita [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="122f9-115">If you don’t already have Visual Studio 2017 installed, you can download and use the free [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span>
    - <span data-ttu-id="122f9-116">Durante l'installazione di Visual Studio abilitare **Sviluppo di Azure**.</span><span class="sxs-lookup"><span data-stu-id="122f9-116">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

## <span data-ttu-id="122f9-117"><a name="metrics"></a>Passaggio 1: visualizzare le metriche</span><span class="sxs-lookup"><span data-stu-id="122f9-117"><a name="metrics"></a> Step 1 - View metrics</span></span>
<span data-ttu-id="122f9-118">Le **metriche** sono utili per comprendere:</span><span class="sxs-lookup"><span data-stu-id="122f9-118">**Metrics** are useful to understand:</span></span>
- <span data-ttu-id="122f9-119">Integrità dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="122f9-119">Application health</span></span>
- <span data-ttu-id="122f9-120">Prestazioni dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="122f9-120">App performance</span></span>
- <span data-ttu-id="122f9-121">Utilizzo di risorse</span><span class="sxs-lookup"><span data-stu-id="122f9-121">Resource consumption</span></span>

<span data-ttu-id="122f9-122">Quando si analizza un problema dell'app, esaminare le metriche è un buon punto di partenza.</span><span class="sxs-lookup"><span data-stu-id="122f9-122">When investigating an application issue, reviewing metrics is a good place to start.</span></span> <span data-ttu-id="122f9-123">Il portale di Azure consente di esaminare visivamente in modo rapido le metriche dell'app usando **Monitoraggio di Azure**.</span><span class="sxs-lookup"><span data-stu-id="122f9-123">Azure portal has a quick way to visually inspect the metrics of your app using **Azure Monitor**.</span></span>

<span data-ttu-id="122f9-124">Le metriche forniscono una visualizzazione cronologica in numerose aggregazioni chiave per l'app.</span><span class="sxs-lookup"><span data-stu-id="122f9-124">Metrics provide a historical view across several key aggregations for your app.</span></span> <span data-ttu-id="122f9-125">Per tutte le app ospitate nel servizio app, si dovrebbero monitorare l'app Web e il piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="122f9-125">For any app hosted in app service, you should monitor both the Web App and the App Service plan.</span></span>

> [!NOTE]
> <span data-ttu-id="122f9-126">Un piano di servizio app rappresenta la raccolta delle risorse fisiche usate per ospitare le app.</span><span class="sxs-lookup"><span data-stu-id="122f9-126">An App Service plan represents the collection of physical resources used to host your apps.</span></span> <span data-ttu-id="122f9-127">Tutte le applicazioni assegnate a un piano di servizio app condividono le risorse definite dal piano, in modo da consentire un risparmio sui costi quando si ospitano più app.</span><span class="sxs-lookup"><span data-stu-id="122f9-127">All applications assigned to an App Service plan share the resources defined by it allowing you to save cost when hosting multiple apps.</span></span>
>
> <span data-ttu-id="122f9-128">I piani di servizio app definiscono:</span><span class="sxs-lookup"><span data-stu-id="122f9-128">App Service plans define:</span></span>
> * <span data-ttu-id="122f9-129">Area: Europa settentrionale, Stati Uniti orientali, Asia sud-orientale e così via.</span><span class="sxs-lookup"><span data-stu-id="122f9-129">Region: North Europe, East US, Southeast Asia, etc.</span></span>
> * <span data-ttu-id="122f9-130">Dimensione dell'istanza: Small, Medium, Large e così via.</span><span class="sxs-lookup"><span data-stu-id="122f9-130">Instance Size: Small, Medium, Large, etc.</span></span>
> * <span data-ttu-id="122f9-131">Numero di scala: una, due o tre istanze e così via.</span><span class="sxs-lookup"><span data-stu-id="122f9-131">Scale Count: one, two, or three instances, etc.</span></span>
> * <span data-ttu-id="122f9-132">SKU: Free, Shared, Basic, Standard, Premium e così via.</span><span class="sxs-lookup"><span data-stu-id="122f9-132">SKU: Free, Shared, Basic, Standard, Premium, etc.</span></span>

<span data-ttu-id="122f9-133">Per esaminare le metriche per l'app Web, passare al pannello **Panoramica** dell'app che si vuole monitorare.</span><span class="sxs-lookup"><span data-stu-id="122f9-133">To review metrics for your Web App, go to the **Overview** blade of the app you want to monitor.</span></span> <span data-ttu-id="122f9-134">A questo punto, è possibile visualizzare un grafico per le metriche dell'app come un **riquadro Monitoraggio**.</span><span class="sxs-lookup"><span data-stu-id="122f9-134">From here, you can view a chart for your app's metrics as a **Monitoring tile**.</span></span> <span data-ttu-id="122f9-135">Fare clic sul riquadro per modificare e configurare le metriche da visualizzare e l'intervallo di tempo di visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="122f9-135">Click the tile to edit and configure what metrics to view and the time range to display.</span></span>

<span data-ttu-id="122f9-136">Per impostazione predefinita, il pannello delle risorse fornisce una visualizzazione per le richieste dell'app e gli errori nell'ultima ora.</span><span class="sxs-lookup"><span data-stu-id="122f9-136">By default the resource blade provides a view for the Application Requests and errors for the last hour.</span></span>
<span data-ttu-id="122f9-137">![Monitorare un'app](media/app-service-web-tutorial-monitoring/app-service-monitor.png)</span><span class="sxs-lookup"><span data-stu-id="122f9-137">![Monitor App](media/app-service-web-tutorial-monitoring/app-service-monitor.png)</span></span>

<span data-ttu-id="122f9-138">Come è possibile notare nell'esempio, si dispone di un'app che genera molti **Errori server HTTP**.</span><span class="sxs-lookup"><span data-stu-id="122f9-138">As you can see in the example, we have an application that is generating many **HTTP Server Errors**.</span></span> <span data-ttu-id="122f9-139">Il volume elevato di errori è la prima indicazione, dobbiamo esaminare questa app.</span><span class="sxs-lookup"><span data-stu-id="122f9-139">The high volume of errors is the first indication we need to investigate this application.</span></span>

> [!TIP]
> <span data-ttu-id="122f9-140">Per informazioni sul monitoraggio di Azure usare i collegamenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="122f9-140">Learn more about Azure Monitor with the following links:</span></span>
> - [<span data-ttu-id="122f9-141">Introduzione al monitoraggio di Azure</span><span class="sxs-lookup"><span data-stu-id="122f9-141">Get started with Azure Monitor</span></span>](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [<span data-ttu-id="122f9-142">Metriche di Azure</span><span class="sxs-lookup"><span data-stu-id="122f9-142">Azure Metrics</span></span>](..\monitoring-and-diagnostics\monitoring-overview-metrics.md)
> - [<span data-ttu-id="122f9-143">Metriche supportate con il monitoraggio di Azure</span><span class="sxs-lookup"><span data-stu-id="122f9-143">Supported metrics with Azure Monitor</span></span>](..\monitoring-and-diagnostics\monitoring-supported-metrics.md)
> - [<span data-ttu-id="122f9-144">Dashboard di Azure</span><span class="sxs-lookup"><span data-stu-id="122f9-144">Azure Dashboards</span></span>](..\azure-portal\azure-portal-dashboards.md)

## <span data-ttu-id="122f9-145"><a name="alerts"></a> Passaggio 2: configurare gli avvisi</span><span class="sxs-lookup"><span data-stu-id="122f9-145"><a name="alerts"></a> Step 2 - Configure Alerts</span></span>
<span data-ttu-id="122f9-146">Gli **avvisi** possono essere configurati per attivare condizioni specifiche per l'app.</span><span class="sxs-lookup"><span data-stu-id="122f9-146">**Alerts** can be configured to trigger on specific conditions for your app.</span></span>

<span data-ttu-id="122f9-147">Nel [Passaggio 1: visualizzare le metriche](#metrics), abbiamo visto che l'app includeva un numero elevato di errori.</span><span class="sxs-lookup"><span data-stu-id="122f9-147">In [Step 1 - View metrics](#metrics), we saw that the application had a high number of errors.</span></span>

<span data-ttu-id="122f9-148">Configuriamo un avviso per ricevere notifiche automaticamente quando si verificano errori.</span><span class="sxs-lookup"><span data-stu-id="122f9-148">Lets configure an alert to automatically get notified when errors occur.</span></span> <span data-ttu-id="122f9-149">In questo caso vogliamo che l'avviso invii un messaggio di posta elettronica ogni qualvolta il numero di errori HTTP 50X supera una determinata soglia.</span><span class="sxs-lookup"><span data-stu-id="122f9-149">In this case, we want the alert to send and e-mail every time the number of HTTP 50X errors goes over a certain threshold.</span></span>

<span data-ttu-id="122f9-150">Per creare un avviso, passare a **Monitoraggio** > **Avvisi** e fare clic su **[+] Aggiungi avviso**.</span><span class="sxs-lookup"><span data-stu-id="122f9-150">To create an alert, navigate to **Monitoring** > **Alerts** and click **[+] Add Alert**.</span></span>

![Avvisi](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts.png)

<span data-ttu-id="122f9-152">Fornire valori per la configurazione degli avvisi:</span><span class="sxs-lookup"><span data-stu-id="122f9-152">Provide values for the Alert configuration:</span></span>
- <span data-ttu-id="122f9-153">**Risorsa:** il sito per il monitoraggio con l'avviso.</span><span class="sxs-lookup"><span data-stu-id="122f9-153">**Resource:** The site to monitor with the alert.</span></span>
- <span data-ttu-id="122f9-154">**Nome:** un nome per l'avviso, in questo caso: *Troppi HTTP 50X*.</span><span class="sxs-lookup"><span data-stu-id="122f9-154">**Name:** A name for your alert, in this case: *High HTTP 50X*.</span></span>
- <span data-ttu-id="122f9-155">**Descrizione:** spiegazione in formato testo normale di cosa sta monitorando questo avviso.</span><span class="sxs-lookup"><span data-stu-id="122f9-155">**Description:** Plain text explanation of what this alert is looking at.</span></span>
- <span data-ttu-id="122f9-156">**Avviso per:** gli avvisi possono monitorare Metriche o Eventi, in questo esempio monitoreremo le metriche.</span><span class="sxs-lookup"><span data-stu-id="122f9-156">**Alert on:** Alerts can look at Metrics or Events, for this example we are looking at metrics.</span></span>
- <span data-ttu-id="122f9-157">**Metrica:** la metrica da monitorare, in questo caso *Errori server HTTP*.</span><span class="sxs-lookup"><span data-stu-id="122f9-157">**Metric:** What metric to monitor, in this case: *HTTP Server Errors*.</span></span>
- <span data-ttu-id="122f9-158">**Condizione:** quando inviare l'avviso, in questo caso selezionare l'opzione *maggiore di*.</span><span class="sxs-lookup"><span data-stu-id="122f9-158">**Condition:** When to alert, in this case select the *greater than* option.</span></span>
- <span data-ttu-id="122f9-159">**Soglia:** valore da cercare, in questo caso *400*.</span><span class="sxs-lookup"><span data-stu-id="122f9-159">**Threshold:** What is value to look for, in this case: *400*.</span></span>
- <span data-ttu-id="122f9-160">**Periodo:** gli avvisi operano oltre il valore medio di una metrica.</span><span class="sxs-lookup"><span data-stu-id="122f9-160">**Period:** Alerts operate over the average value of a metric.</span></span> <span data-ttu-id="122f9-161">Per i periodi di tempo più ristretti, gli avvisi sensibili vengono sospesi.</span><span class="sxs-lookup"><span data-stu-id="122f9-161">Smaller periods of time yield more sensitive alerts.</span></span> <span data-ttu-id="122f9-162">In questo caso, consideriamo *5 minuti*.</span><span class="sxs-lookup"><span data-stu-id="122f9-162">in this case we are looking at *5 Minutes*.</span></span>
- <span data-ttu-id="122f9-163">**Invia messaggio di posta elettronica a proprietari e collaboratori:** in questo caso *Abilitato*.</span><span class="sxs-lookup"><span data-stu-id="122f9-163">**Email Owners and contributors:** in this case: *Enabled*.</span></span>

<span data-ttu-id="122f9-164">Ora che l'avviso è stato creato, viene inviato un messaggio di posta elettronica ogni volta che l'app supera la soglia configurata.</span><span class="sxs-lookup"><span data-stu-id="122f9-164">Now that the alert is created an email is sent every time the app goes over the configured threshold.</span></span> <span data-ttu-id="122f9-165">Gli avvisi attivi possono essere consultati anche nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="122f9-165">Active alerts can also be reviewed in the Azure portal.</span></span>

![Avvisi attivati](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts-triggered.png)


> [!TIP]
> <span data-ttu-id="122f9-167">Per informazioni sugli avvisi di Azure usare i collegamenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="122f9-167">Learn more about Azure Alerts with the following links:</span></span>
> - [<span data-ttu-id="122f9-168">Cosa sono gli avvisi in Microsoft Azure?</span><span class="sxs-lookup"><span data-stu-id="122f9-168">What are alerts in Microsoft Azure</span></span>](..\monitoring-and-diagnostics\monitoring-overview-alerts.md)
> - [<span data-ttu-id="122f9-169">Eseguire operazioni sulle metriche</span><span class="sxs-lookup"><span data-stu-id="122f9-169">Take Action On Metrics</span></span>](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [<span data-ttu-id="122f9-170">Creare avvisi delle metriche</span><span class="sxs-lookup"><span data-stu-id="122f9-170">Create metric alerts</span></span>](..\monitoring-and-diagnostics\insights-alerts-portal.md)

## <span data-ttu-id="122f9-171"><a name="companion"></a> Passaggio 3: App Service Companion</span><span class="sxs-lookup"><span data-stu-id="122f9-171"><a name="companion"></a> Step 3 - App Service Companion</span></span>
<span data-ttu-id="122f9-172">**App Service Companion** consente di monitorare l'app con un'esperienza nativa nel dispositivo mobile iOS o Android.</span><span class="sxs-lookup"><span data-stu-id="122f9-172">**App Service companion** offers a convenient way to monitor your app with a native experience in your mobile device (iOS or Android).</span></span>

<span data-ttu-id="122f9-173">Usare App Service Companion per:</span><span class="sxs-lookup"><span data-stu-id="122f9-173">Use App Service Companion to:</span></span>
- <span data-ttu-id="122f9-174">Rivedere le metriche dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="122f9-174">Review application metrics</span></span>
- <span data-ttu-id="122f9-175">Rivedere ed eseguire azioni su avvisi e suggerimenti dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="122f9-175">Review and act on application alerts and recommendations</span></span>
- <span data-ttu-id="122f9-176">Eseguire operazioni di base per la risoluzione dei problemi (esplorare, avviare, arrestare, riavviare l'app)</span><span class="sxs-lookup"><span data-stu-id="122f9-176">Perform basic troubleshooting (browse, start, stop, restart the app)</span></span>
- <span data-ttu-id="122f9-177">Ottenere notifiche push per gli eventi critici.</span><span class="sxs-lookup"><span data-stu-id="122f9-177">Get push notifications for critical events.</span></span>

![App Service Companion](media/app-service-web-tutorial-monitoring/app-service-companion.png)

<span data-ttu-id="122f9-179">[![App Service Companion in App Store](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![App Service Companion in Google Play](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span><span class="sxs-lookup"><span data-stu-id="122f9-179">[![App Service Companion App Store](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![App Service Companion Google Play](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span></span>

<span data-ttu-id="122f9-180">È possibile installare App Service Companion da [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) o [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span><span class="sxs-lookup"><span data-stu-id="122f9-180">You can install App Service companion from the [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) or [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span></span>

## <span data-ttu-id="122f9-181"><a name="diagnose"></a> Passaggio 4: diagnostica e risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="122f9-181"><a name="diagnose"></a> Step 4 - Diagnose and solve problems</span></span>
<span data-ttu-id="122f9-182">La **diagnostica e risoluzione dei problemi** consente di separare i problemi legati all'app da quelli legati alla piattaforma.</span><span class="sxs-lookup"><span data-stu-id="122f9-182">**Diagnose and solve problems** helps you separate application issues form platform issues.</span></span> <span data-ttu-id="122f9-183">Può inoltre suggerire possibili soluzioni per ripristinare l'integrità dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="122f9-183">It can also suggest possible mitigations to get your Web App back to healthy.</span></span>

![Diagnostica e risoluzione dei problemi](media/app-service-web-tutorial-monitoring/app-service-monitor-diagnosis.png)

<span data-ttu-id="122f9-185">Continuando con l'esempio dai passaggi precedenti, possiamo vedere che l'app presenta dei problemi di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="122f9-185">Continuing with the example form previous steps, we can see that the application has been having availably issues.</span></span> <span data-ttu-id="122f9-186">Dall'altro lato, però, la disponibilità della piattaforma non si è spostata dal 100%.</span><span class="sxs-lookup"><span data-stu-id="122f9-186">In contrast, the platform availability has not moved from 100%.</span></span>

<span data-ttu-id="122f9-187">Quando l'app, diversamente dalla piattaforma, presenta dei problemi, si tratta di un chiaro segno che i problemi sono legati esclusivamente all'app.</span><span class="sxs-lookup"><span data-stu-id="122f9-187">When the app is having issue and the platform stays up, it's a clear indication that we are dealing with an application issue.</span></span>

## <span data-ttu-id="122f9-188"><a name="logging"></a> Passaggio 5: registrazione</span><span class="sxs-lookup"><span data-stu-id="122f9-188"><a name="logging"></a> Step 5 - Logging</span></span>
<span data-ttu-id="122f9-189">Ora che gli errori sono stati circoscritti a un problema dell'app, per ottenere altre informazioni possiamo esaminare i log dell'app e del server.</span><span class="sxs-lookup"><span data-stu-id="122f9-189">Now that we have narrowed down the failures to an application issue, we can look at the application and server logs to get more information.</span></span>

<span data-ttu-id="122f9-190">La registrazione consente di raccogliere i log di **diagnostica dell'applicazione** e di **diagnostica del server Web** per l'app Web.</span><span class="sxs-lookup"><span data-stu-id="122f9-190">Logging allows you to collect both **Application Diagnostics** and **Web Server Diagnostics** logs for your Web App.</span></span>

### <a name="application-diagnostics"></a><span data-ttu-id="122f9-191">Diagnostica applicazioni</span><span class="sxs-lookup"><span data-stu-id="122f9-191">Application Diagnostics</span></span>
<span data-ttu-id="122f9-192">Diagnostica applicazioni consente di acquisire le tracce prodotte dall'applicazione durante il runtime.</span><span class="sxs-lookup"><span data-stu-id="122f9-192">Application diagnostics allows you to capture traces produced by the application at runtime.</span></span>

<span data-ttu-id="122f9-193">L'aggiunta della traccia all'app migliora notevolmente la capacità di eseguire il debug e di individuare con esattezza i problemi.</span><span class="sxs-lookup"><span data-stu-id="122f9-193">Adding tracing to your application greatly improves your ability to debug and pin-point issues.</span></span>

<span data-ttu-id="122f9-194">In ASP.NET è possibile registrare le tracce dell'applicazione usando la classe [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) per generare eventi che vengono acquisiti dall'infrastruttura dei log.</span><span class="sxs-lookup"><span data-stu-id="122f9-194">In ASP.NET, you can log application traces using [System.Diagnostics.Trace class](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) to generate events that are captured by the log infrastructure.</span></span> <span data-ttu-id="122f9-195">È anche possibile specificare la gravità della traccia per filtrare i risultati in modo più semplice.</span><span class="sxs-lookup"><span data-stu-id="122f9-195">You can also specify the severity of the trace for easier filtering.</span></span>

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
<span data-ttu-id="122f9-196">Per abilitare la registrazione dell'applicazione, andare al **Monitoraggio** > **Log di diagnostica** e abilitare la registrazione delle applicazioni usando i controlli.</span><span class="sxs-lookup"><span data-stu-id="122f9-196">To enable Application logging Go to **Monitoring** > **Diagnostic Logs** and Enable Application Logging using the toggles.</span></span>

![Monitorare un'app](media/app-service-web-tutorial-monitoring/app-service-monitor-applogs.png)

<span data-ttu-id="122f9-198">I log dell'applicazione possono essere archiviati nel file system dell'app Web o inseriti nell'archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="122f9-198">Application logs can be stored to your Web App's file system or pushed out to blob storage.</span></span> <span data-ttu-id="122f9-199">Per gli scenari di produzione è consigliabile usare l'archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="122f9-199">For production scenarios, it's recommended to use blob storage.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="122f9-200">L'abilitazione della registrazione ha effetto sulle prestazioni dell'applicazione e l'uso delle risorse.</span><span class="sxs-lookup"><span data-stu-id="122f9-200">Enabling logging has an impact on your application performance and resource utilization.</span></span> <span data-ttu-id="122f9-201">Per gli scenari di produzione è consigliabile usare i log degli errori.</span><span class="sxs-lookup"><span data-stu-id="122f9-201">For production scenarios, error logs are recommended.</span></span> <span data-ttu-id="122f9-202">Abilitare una registrazione più dettagliata solo durante l'analisi dei problemi.</span><span class="sxs-lookup"><span data-stu-id="122f9-202">Only enable more verbose logging when investigating issues.</span></span>

 ### <a name="web-server-diagnostics"></a><span data-ttu-id="122f9-203">Diagnostica del server Web</span><span class="sxs-lookup"><span data-stu-id="122f9-203">Web Server Diagnostics</span></span>
<span data-ttu-id="122f9-204">I log del server Web vengono generati anche se l'app non è instrumentata.</span><span class="sxs-lookup"><span data-stu-id="122f9-204">Web Server logs are generated even if your app is not instrumented.</span></span> <span data-ttu-id="122f9-205">Il servizio app consente di raccogliere tre tipi diversi di log del server:</span><span class="sxs-lookup"><span data-stu-id="122f9-205">App Service can collect three different types of server logs:</span></span>

- <span data-ttu-id="122f9-206">**Registrazione del server Web**</span><span class="sxs-lookup"><span data-stu-id="122f9-206">**Web Server Logging**</span></span>
    - <span data-ttu-id="122f9-207">Informazioni sulle transazioni HTTP che usano il [formato di file di log esteso W3C](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span><span class="sxs-lookup"><span data-stu-id="122f9-207">Information about HTTP transactions using the [W3C extended log file format](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span></span>
    - <span data-ttu-id="122f9-208">Consente di determinare le metriche generali del sito, ad esempio il numero di richieste gestite oppure il numero di richieste provenienti da un indirizzo IP specifico.</span><span class="sxs-lookup"><span data-stu-id="122f9-208">Useful when determining overall site metrics such as the number of requests handled or how many requests are from a specific IP address.</span></span>
- <span data-ttu-id="122f9-209">**Registrazione degli errori dettagliata**</span><span class="sxs-lookup"><span data-stu-id="122f9-209">**Detailed Error Logging**</span></span>
    - <span data-ttu-id="122f9-210">Informazioni dettagliate sugli errori relativi ai codici di stato HTTP che indicano un'operazione non riuscita (codice di stato 400 o superiore).</span><span class="sxs-lookup"><span data-stu-id="122f9-210">Detailed error information for HTTP status codes that indicate a failure (status code 400 or greater).</span></span>
    - [<span data-ttu-id="122f9-211">Altre informazioni sulla registrazione degli errori dettagliata</span><span class="sxs-lookup"><span data-stu-id="122f9-211">Learn more about detailed error logging</span></span>](https://www.iis.net/learn/troubleshoot/diagnosing-http-errors/how-to-use-http-detailed-errors-in-iis)
- <span data-ttu-id="122f9-212">**Traccia delle richieste non riuscite**</span><span class="sxs-lookup"><span data-stu-id="122f9-212">**Failed Request Tracing**</span></span>
    - <span data-ttu-id="122f9-213">Informazioni dettagliate sulle richieste non riuscite, inclusa una traccia dei componenti IIS usati per elaborare la richieste e il tempo impiegato in ogni componente.</span><span class="sxs-lookup"><span data-stu-id="122f9-213">Detailed information on failed requests, including a trace of the IIS components used to process the request and the time taken in each component.</span></span>
    - <span data-ttu-id="122f9-214">I log delle richieste non riuscite consentono di individuare la causa di un errore HTTP specifico.</span><span class="sxs-lookup"><span data-stu-id="122f9-214">Failed request logs are useful when trying to isolate what is causing a specific HTTP error.</span></span>
    - [<span data-ttu-id="122f9-215">Altre informazioni sulla traccia delle richieste non riuscite</span><span class="sxs-lookup"><span data-stu-id="122f9-215">Learn more about failed request tracing</span></span>](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis)

<span data-ttu-id="122f9-216">Per abilitare la registrazione del server:</span><span class="sxs-lookup"><span data-stu-id="122f9-216">To enable Server logging:</span></span>
- <span data-ttu-id="122f9-217">Passare a **Monitoraggio** > **Log di diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="122f9-217">go to **Monitoring** > **Diagnostic Logs**.</span></span>
- <span data-ttu-id="122f9-218">Abilitare i diversi tipi di diagnostica del server Web usando i controlli.</span><span class="sxs-lookup"><span data-stu-id="122f9-218">Enable the different types of Web Server Diagnostics using the toggles.</span></span>

![Monitorare un'app](media/app-service-web-tutorial-monitoring/app-service-monitor-serverlogs.png)

> [!IMPORTANT]
> <span data-ttu-id="122f9-220">L'abilitazione della registrazione ha effetto sulle prestazioni dell'applicazione e l'uso delle risorse.</span><span class="sxs-lookup"><span data-stu-id="122f9-220">Enabling logging has an impact on your application performance and resource utilization.</span></span> <span data-ttu-id="122f9-221">Per gli scenari di produzione è consigliabile usare i log degli errori. Abilitare una registrazione più dettagliata solo durante l'analisi dei problemi.</span><span class="sxs-lookup"><span data-stu-id="122f9-221">For Production Scenarios, Error logs are recommended, Only Enable more verbose logging when investigating issues.</span></span>

### <a name="accessing-logs"></a><span data-ttu-id="122f9-222">Accesso ai log</span><span class="sxs-lookup"><span data-stu-id="122f9-222">Accessing Logs</span></span>
<span data-ttu-id="122f9-223">I log memorizzati nell'archiviazione BLOB sono accessibili tramite Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="122f9-223">Logs stored in blob storage are accessed using Azure Storage Explorer.</span></span> <span data-ttu-id="122f9-224">I log archiviati nel file system dell'app Web sono accessibili tramite FTP nei percorsi seguenti:</span><span class="sxs-lookup"><span data-stu-id="122f9-224">Logs stored in the Web App's filesystem are accessed through FTP under the following paths:</span></span>

- <span data-ttu-id="122f9-225">**Log applicazioni** - `%HOME%/LogFiles/Application/`.</span><span class="sxs-lookup"><span data-stu-id="122f9-225">**Application logs** - `%HOME%/LogFiles/Application/`.</span></span>
    - <span data-ttu-id="122f9-226">In questa cartella sono presenti uno o più file di testo contenenti le informazioni generate dalla registrazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="122f9-226">This folder contains one or more text files containing information produced by application logging.</span></span>
- <span data-ttu-id="122f9-227">**Traccia delle richieste non riuscite** - `%HOME%/LogFiles/W3SVC#########/`.</span><span class="sxs-lookup"><span data-stu-id="122f9-227">**Failed Request Traces** - `%HOME%/LogFiles/W3SVC#########/`.</span></span>
    - <span data-ttu-id="122f9-228">Questa cartella contiene un file XSL e uno o più file XML.</span><span class="sxs-lookup"><span data-stu-id="122f9-228">This folder contains an XSL file and one or more XML files.</span></span>
- <span data-ttu-id="122f9-229">**Registrazione degli errori dettagliata** - `%HOME%/LogFiles/DetailedErrors/`.</span><span class="sxs-lookup"><span data-stu-id="122f9-229">**Detailed Error Logs** - `%HOME%/LogFiles/DetailedErrors/`.</span></span>
    - <span data-ttu-id="122f9-230">Questa cartella contiene uno o più file con estensione htm con informazioni dettagliate sugli errori HTTP generati dall'app.</span><span class="sxs-lookup"><span data-stu-id="122f9-230">This folder contains one or more .htm files with extensive information on HTTP errors generated by your app.</span></span>
- <span data-ttu-id="122f9-231">**Log del server Web** - `%HOME%/LogFiles/http/RawLogs`.</span><span class="sxs-lookup"><span data-stu-id="122f9-231">**Web Server Logs** - `%HOME%/LogFiles/http/RawLogs`.</span></span>
    - <span data-ttu-id="122f9-232">Questa cartella contiene uno o più file di testo formattati usando il formato di file di log esteso W3C.</span><span class="sxs-lookup"><span data-stu-id="122f9-232">This folder contains one or more text files formatted using the W3C extended log file format.</span></span>

## <span data-ttu-id="122f9-233"><a name="streaming"></a> Passaggio 6: streaming dei log</span><span class="sxs-lookup"><span data-stu-id="122f9-233"><a name="streaming"></a> Step 6 - Log Streaming</span></span>
<span data-ttu-id="122f9-234">I log in streaming sono utili durante il debug di un'applicazione poiché consentono di risparmiare tempo rispetto all'[accesso dei log](#Accessing-Logs) tramite FTP.</span><span class="sxs-lookup"><span data-stu-id="122f9-234">Streaming logs are convenient when debugging an application since it saves time compared to [accessing the logs](#Accessing-Logs) through FTP.</span></span>

<span data-ttu-id="122f9-235">Il servizio app può eseguire lo streaming dei **Log applicazione** e dei **Log del server Web** generati.</span><span class="sxs-lookup"><span data-stu-id="122f9-235">App Service can stream **Application Logs** and **Web Server Logs** as they are generated.</span></span>

> [!TIP]
> <span data-ttu-id="122f9-236">Prima di tentare di eseguire lo streaming dei log, assicurarsi di aver abilitato la raccolta dei log come descritto nella sezione [Registrazione](#logging).</span><span class="sxs-lookup"><span data-stu-id="122f9-236">Before trying to stream logs, make sure you have enabled collecting logs as described in the [Logging](#logging) section.</span></span>

<span data-ttu-id="122f9-237">Per eseguire lo streaming dei log, passare a **Monitoraggio**> **Flusso di registrazione**.</span><span class="sxs-lookup"><span data-stu-id="122f9-237">To stream logs, go to **Monitoring**> **Log Stream**.</span></span> <span data-ttu-id="122f9-238">Selezionare **Log applicazione** o **Log del server Web**, a seconda delle informazioni desiderate.</span><span class="sxs-lookup"><span data-stu-id="122f9-238">Select **Application Logs** or **Web server logs** depending what information you are looking for.</span></span> <span data-ttu-id="122f9-239">A questo punto, è anche possibile sospendere, riavviare e cancellare il buffer.</span><span class="sxs-lookup"><span data-stu-id="122f9-239">From here, you can also pause, restart, and clear the buffer.</span></span>

![Log in streaming](media/app-service-web-tutorial-monitoring/app-service-monitor-logstream.png)

> [!TIP]
> <span data-ttu-id="122f9-241">I log vengono generati soltanto quando è presente traffico nell'app. È anche possibile aumentare il livello di dettaglio dei log per ottenere più eventi o informazioni.</span><span class="sxs-lookup"><span data-stu-id="122f9-241">Logs are only generated when there is traffic on the app, you can also increase the verbosity of logs to get more events or information.</span></span>

## <span data-ttu-id="122f9-242"><a name="remote"></a> Passaggio 7 - Debug remoto</span><span class="sxs-lookup"><span data-stu-id="122f9-242"><a name="remote"></a> Step 7 - Remote Debugging</span></span>
<span data-ttu-id="122f9-243">Una volta individuata l'origine dei problemi dell'app, usare **Debug remoto** per esaminare il codice.</span><span class="sxs-lookup"><span data-stu-id="122f9-243">Once you have pin-pointed the source of the applications problems, use **Remote Debugging** to walk through the code.</span></span>

<span data-ttu-id="122f9-244">Il debug remoto consente di collegare un debugger all'app Web in esecuzione nel cloud.</span><span class="sxs-lookup"><span data-stu-id="122f9-244">Remote debugging lets you attach a debugger to your Web App running in the cloud.</span></span> <span data-ttu-id="122f9-245">È possibile impostare punti di interruzione, manipolare direttamente la memoria, esaminare il codice e cambiarne il percorso come in un'app eseguita in locale.</span><span class="sxs-lookup"><span data-stu-id="122f9-245">You can set breakpoints, manipulate memory directly, step through code, and even change the code path just like you do for an app running locally.</span></span>

<span data-ttu-id="122f9-246">Per collegare il debugger all'app in esecuzione nel cloud:</span><span class="sxs-lookup"><span data-stu-id="122f9-246">To attach the debugger to your app running in the cloud:</span></span>

- <span data-ttu-id="122f9-247">In Visual Studio 2017 aprire la soluzione per l'app di cui si vuole eseguire il debug</span><span class="sxs-lookup"><span data-stu-id="122f9-247">Using Visual Studio 2017, open the solution for the app you want to debug</span></span>
- <span data-ttu-id="122f9-248">Impostare alcuni punti di interruzione esattamente come si farebbe per lo sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="122f9-248">Set some brake points just like you would for local development.</span></span>
- <span data-ttu-id="122f9-249">Aprire **Cloud Explorer** (CTRL+/, CTRL+X).</span><span class="sxs-lookup"><span data-stu-id="122f9-249">Open **cloud explorer** (ctr + /, ctrl + x).</span></span>
- <span data-ttu-id="122f9-250">Accedere con le credenziali di Azure.</span><span class="sxs-lookup"><span data-stu-id="122f9-250">Log in with your azure credentials as needed.</span></span>
- <span data-ttu-id="122f9-251">Individuare l'app di cui si vuole eseguire il debug</span><span class="sxs-lookup"><span data-stu-id="122f9-251">Find the app you want to debug</span></span>
- <span data-ttu-id="122f9-252">Selezionare **Collega debugger** dal riquadro **Azioni**.</span><span class="sxs-lookup"><span data-stu-id="122f9-252">Select **Attach Debugger** form the **Actions** pane.</span></span>

![Debug remoto](media/app-service-web-tutorial-monitoring/app-service-monitor-vsdebug.png)

<span data-ttu-id="122f9-254">Visual Studio configura l'applicazione per il debug remoto e apre una finestra del browser che consente di passare all'app.</span><span class="sxs-lookup"><span data-stu-id="122f9-254">Visual Studio configures your application for remote debugging and launches a browser window that navigates to your app.</span></span> <span data-ttu-id="122f9-255">Esplorare l'app per attivare i punti di interruzione ed esaminare il codice.</span><span class="sxs-lookup"><span data-stu-id="122f9-255">Browse through your app to trigger break points and step through the code.</span></span>

> [!WARNING]
> <span data-ttu-id="122f9-256">L'esecuzione in modalità debug in produzione non è una scelta consigliata.</span><span class="sxs-lookup"><span data-stu-id="122f9-256">Running in debug mode in production is not recommended.</span></span> <span data-ttu-id="122f9-257">Se l'app in produzione non viene ampliata con più istanze del server, il debug impedisce al server Web di rispondere ad altre richieste.</span><span class="sxs-lookup"><span data-stu-id="122f9-257">If your production app is not scaled out to multiple server instances, debugging prevent the web server from responding to other requests.</span></span> <span data-ttu-id="122f9-258">Per la risoluzione dei problemi di produzione è consigliabile [configurare la registrazione](#logging) e usare [Application Insights](#insights).</span><span class="sxs-lookup"><span data-stu-id="122f9-258">For troubleshooting production problems, your best resource is to [configure logging](#logging) and [Application Insights](#insights).</span></span>



## <span data-ttu-id="122f9-259"><a name="explorer"></a> Passaggio 8: esplora processi</span><span class="sxs-lookup"><span data-stu-id="122f9-259"><a name="explorer"></a> Step 8 - Process Explorer</span></span>
<span data-ttu-id="122f9-260">Quando l'app viene scalata orizzontalmente a più di un'istanza, **Esplora processi** consente di identificare i problemi specifici delle istanze.</span><span class="sxs-lookup"><span data-stu-id="122f9-260">When your application is scaled out to more than one instance, **process explorer** can help you identify instance specific problems.</span></span>

<span data-ttu-id="122f9-261">Usare **Esplora processi** per:</span><span class="sxs-lookup"><span data-stu-id="122f9-261">Use **Process Explorer** to:</span></span>

- <span data-ttu-id="122f9-262">Enumerare tutti i processi nelle diverse istanze del piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="122f9-262">Enumerate all the processes across different instances of your App Service plan.</span></span>
- <span data-ttu-id="122f9-263">Eseguire il drill-down e visualizzare gli handle e i moduli associati a ogni processo.</span><span class="sxs-lookup"><span data-stu-id="122f9-263">Drill down and view the handles and modules associated with each process.</span></span>
- <span data-ttu-id="122f9-264">Visualizzare il numero di CPU, working set e thread a livello di processo per identificare i processi con eccessivo tempo di esecuzione</span><span class="sxs-lookup"><span data-stu-id="122f9-264">View CPU, Working Set, and Thread count at the process level to help you identify runaway processes</span></span>
- <span data-ttu-id="122f9-265">Trovare gli handle di file aperti e terminare l'istanza di un processo specifico.</span><span class="sxs-lookup"><span data-stu-id="122f9-265">Find open file handles, and even kill a specific process instance.</span></span>

<span data-ttu-id="122f9-266">Esplora processi è disponibile in **Monitoraggio** > **Esplora processi**.</span><span class="sxs-lookup"><span data-stu-id="122f9-266">Process Explorer can be found under **Monitoring** > **Process Explorer**.</span></span>

![Esplora processi](media/app-service-web-tutorial-monitoring/app-service-monitor-processexplorer.png)


## <span data-ttu-id="122f9-268"><a name="insights"></a> Passaggio 9: Application Insights</span><span class="sxs-lookup"><span data-stu-id="122f9-268"><a name="insights"></a> Step 9 - Application Insights</span></span>
<span data-ttu-id="122f9-269">**Application Insights** offre funzionalità avanzate di profilatura e monitoraggio dell'app.</span><span class="sxs-lookup"><span data-stu-id="122f9-269">**Application Insights** provides application profiling and advanced monitoring capabilities for your app.</span></span>

<span data-ttu-id="122f9-270">Usare Application Insights per rilevare e diagnosticare le eccezioni e i problemi di prestazioni nell'app Web.</span><span class="sxs-lookup"><span data-stu-id="122f9-270">Use Application Insights to detect and diagnose exceptions and performance issues in your Web App.</span></span>

<span data-ttu-id="122f9-271">È possibile abilitare Application Insights per l'app Web in **Monitoraggio** > **Application Insights**</span><span class="sxs-lookup"><span data-stu-id="122f9-271">You can enable Application Insights for your Web App under **Monitoring** > **Application Insights**</span></span>

> [!NOTE]
> <span data-ttu-id="122f9-272">Application Insights potrebbe richiedere l'installazione dell'estensione del sito Application Insights per avviare la raccolta dati.</span><span class="sxs-lookup"><span data-stu-id="122f9-272">Application Insights might prompt you to install the Application Insights site extension to start collecting data.</span></span> <span data-ttu-id="122f9-273">L'installazione dell'estensione del sito comporta il riavvio dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="122f9-273">Installing the site extension causes an application restart.</span></span>

![Application Insights](media/app-service-web-tutorial-monitoring/app-service-monitor-appinsights.png)

<span data-ttu-id="122f9-275">Application Insights include un'ampia gamma di funzionalità. Per altre informazioni, usare i collegamenti inclusi nella sezione [Passaggi successivi](#next).</span><span class="sxs-lookup"><span data-stu-id="122f9-275">Application Insights has a rich feature set, to learn more, follow the links included in the [Next Steps](#next) section.</span></span>

## <span data-ttu-id="122f9-276"><a name="next"></a> Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="122f9-276"><a name="next"></a> Next steps</span></span>

 - [<span data-ttu-id="122f9-277">Informazioni su Azure Application Insights</span><span class="sxs-lookup"><span data-stu-id="122f9-277">What is Application Insights</span></span>](..\application-insights\app-insights-overview.md)
 - [<span data-ttu-id="122f9-278">Monitoraggio delle prestazioni dell'applicazione web di Azure</span><span class="sxs-lookup"><span data-stu-id="122f9-278">Monitor Azure web app performance with Application Insights</span></span>](..\application-insights\app-insights-azure-web-apps.md)
 - [<span data-ttu-id="122f9-279">Monitorare la disponibilità e la velocità di risposta dei siti Web</span><span class="sxs-lookup"><span data-stu-id="122f9-279">Monitor availability and responsiveness of any web site with Application Insights</span></span>](..\application-insights\app-insights-monitor-web-app-availability.md)
