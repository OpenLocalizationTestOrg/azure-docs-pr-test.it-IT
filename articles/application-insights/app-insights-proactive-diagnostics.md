---
title: Rilevamento in Azure Application Insights aaaSmart | Documenti Microsoft
description: Application Insights esegue automaticamente un'analisi approfondita dei dati di telemetria dell'app e segnala potenziali problemi.
services: application-insights
documentationcenter: windows
author: rakefetj
manager: carmonm
ms.assetid: 2eeb4a35-c7a1-49f7-9b68-4f4b860938b2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: bwren
ms.openlocfilehash: f794476088fc69154eda2077b7a5cdc769fab3a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="smart-detection-in-application-insights"></a><span data-ttu-id="b6a4f-103">Rilevamento intelligente in Application Insights</span><span class="sxs-lookup"><span data-stu-id="b6a4f-103">Smart Detection in Application Insights</span></span>
 <span data-ttu-id="b6a4f-104">Il rilevamento intelligente segnala automaticamente i potenziali problemi di prestazioni nell'applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="b6a4f-104">Smart Detection automatically warns you of potential performance problems in your web application.</span></span> <span data-ttu-id="b6a4f-105">Esegue l'analisi proattiva dei dati di telemetria hello che l'app invia troppo[Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b6a4f-105">It performs proactive analysis of hello telemetry that your app sends too[Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="b6a4f-106">Se si verifica un improvviso aumento della percentuale di errori o in caso di modelli anomali delle prestazioni di client o server, viene generato un avviso.</span><span class="sxs-lookup"><span data-stu-id="b6a4f-106">If there is a sudden rise in failure rates, or abnormal patterns in client or server performance, you get an alert.</span></span> <span data-ttu-id="b6a4f-107">Questa funzionalità non richiede alcuna configurazione.</span><span class="sxs-lookup"><span data-stu-id="b6a4f-107">This feature needs no configuration.</span></span> <span data-ttu-id="b6a4f-108">Funziona se l'applicazione invia dati di telemetria sufficienti.</span><span class="sxs-lookup"><span data-stu-id="b6a4f-108">It operates if your application sends enough telemetry.</span></span>

<span data-ttu-id="b6a4f-109">È possibile accedere gli avvisi di rilevamento intelligente da messaggi di posta elettronica hello che viene visualizzato sia dal pannello Smart rilevamento hello.</span><span class="sxs-lookup"><span data-stu-id="b6a4f-109">You can access Smart Detection alerts both from hello emails you receive, and from hello Smart Detection blade.</span></span>

## <a name="review-your-smart-detections"></a><span data-ttu-id="b6a4f-110">Esaminare i rilevamenti intelligenti</span><span class="sxs-lookup"><span data-stu-id="b6a4f-110">Review your Smart Detections</span></span>
<span data-ttu-id="b6a4f-111">È possibile individuare i rilevamenti in due modi:</span><span class="sxs-lookup"><span data-stu-id="b6a4f-111">You can discover detections in two ways:</span></span>

* <span data-ttu-id="b6a4f-112">**Viene visualizzato un messaggio di posta elettronica** da Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b6a4f-112">**You receive an email** from Application Insights.</span></span> <span data-ttu-id="b6a4f-113">Ecco un esempio tipico:</span><span class="sxs-lookup"><span data-stu-id="b6a4f-113">Here's a typical example:</span></span>
  
    ![Avviso di posta elettronica](./media/app-insights-proactive-diagnostics/03.png)
  
    <span data-ttu-id="b6a4f-115">Fare clic su hello pulsante grande tooopen più dettagliatamente nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="b6a4f-115">Click hello big button tooopen more detail in hello portal.</span></span>
* <span data-ttu-id="b6a4f-116">**riquadro rilevamento intelligente Hello** panoramica dell'app pannello Visualizza il numero di avvisi recenti.</span><span class="sxs-lookup"><span data-stu-id="b6a4f-116">**hello Smart Detection tile** on your app's overview blade shows a count of recent alerts.</span></span> <span data-ttu-id="b6a4f-117">Fare clic su hello riquadro toosee un elenco degli avvisi recenti.</span><span class="sxs-lookup"><span data-stu-id="b6a4f-117">Click hello tile toosee a list of recent alerts.</span></span>

![Visualizzare rilevamenti recenti](./media/app-insights-proactive-diagnostics/04.png)

<span data-ttu-id="b6a4f-119">Selezionare un avviso toosee i dettagli.</span><span class="sxs-lookup"><span data-stu-id="b6a4f-119">Select an alert toosee its details.</span></span>

## <a name="what-problems-are-detected"></a><span data-ttu-id="b6a4f-120">Tipi di problemi rilevati</span><span class="sxs-lookup"><span data-stu-id="b6a4f-120">What problems are detected?</span></span>
<span data-ttu-id="b6a4f-121">Esistono tre tipologie di rilevamento:</span><span class="sxs-lookup"><span data-stu-id="b6a4f-121">There are three kinds of detection:</span></span>

* <span data-ttu-id="b6a4f-122">[Rilevamento intelligente: anomalie negli errori](app-insights-proactive-failure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="b6a4f-122">[Smart detection - Failure Anomalies](app-insights-proactive-failure-diagnostics.md).</span></span> <span data-ttu-id="b6a4f-123">Si usa machine learning frequenza hello previsto tooset delle richieste non riuscite per l'app, correlazione con carico e di altri fattori.</span><span class="sxs-lookup"><span data-stu-id="b6a4f-123">We use machine learning tooset hello expected rate of failed requests for your app, correlating with load and other factors.</span></span> <span data-ttu-id="b6a4f-124">Se la percentuale di errori hello passa all'esterno di busta previsto hello, si invia un avviso.</span><span class="sxs-lookup"><span data-stu-id="b6a4f-124">If hello failure rate goes outside hello expected envelope, we send an alert.</span></span>
* <span data-ttu-id="b6a4f-125">[Rilevamento intelligente: anomalie nelle prestazioni](app-insights-proactive-performance-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="b6a4f-125">[Smart detection - Performance Anomalies](app-insights-proactive-performance-diagnostics.md).</span></span> <span data-ttu-id="b6a4f-126">Ricevere le notifiche se il tempo di risposta di un'operazione o la dipendenza di durata rallentamento toohistorical confrontati della linea di base o se si stabilisce un modello anomalo in fase di caricamento pagina o di tempi di risposta.</span><span class="sxs-lookup"><span data-stu-id="b6a4f-126">You get notifications if response time of an operation or dependency duration is slowing down compared toohistorical baseline or if we identify an anomalous pattern in response time or page load time.</span></span>   
* <span data-ttu-id="b6a4f-127">[Rilevamento intelligente: problemi del servizio cloud di Azure](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/).</span><span class="sxs-lookup"><span data-stu-id="b6a4f-127">[Smart detection - Azure Cloud Service issues](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/).</span></span> <span data-ttu-id="b6a4f-128">Vengono inviati avvisi all'utente se l'app è ospitata in Servizi cloud di Azure e un'istanza del ruolo presenta errori di avvio, ricicli frequenti o arresti anomali del sistema in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="b6a4f-128">You get alerts if your app is hosted in Azure Cloud Services and a role instance has startup failures, frequent recycling, or runtime crashes.</span></span>

<span data-ttu-id="b6a4f-129">(i collegamenti della Guida hello in ogni notifica visualizzano articoli pertinenti toohello.)</span><span class="sxs-lookup"><span data-stu-id="b6a4f-129">(hello help links in each notification take you toohello relevant articles.)</span></span>

## <a name="video"></a><span data-ttu-id="b6a4f-130">Video</span><span class="sxs-lookup"><span data-stu-id="b6a4f-130">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="b6a4f-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b6a4f-131">Next steps</span></span>
<span data-ttu-id="b6a4f-132">Questi strumenti di diagnostica consentono di controllare la telemetria hello dall'app:</span><span class="sxs-lookup"><span data-stu-id="b6a4f-132">These diagnostic tools help you inspect hello telemetry from your app:</span></span>

* [<span data-ttu-id="b6a4f-133">Esplora metriche</span><span class="sxs-lookup"><span data-stu-id="b6a4f-133">Metric explorer</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="b6a4f-134">Esplora ricerche</span><span class="sxs-lookup"><span data-stu-id="b6a4f-134">Search explorer</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="b6a4f-135">Linguaggio avanzato di query di Analisi</span><span class="sxs-lookup"><span data-stu-id="b6a4f-135">Analytics - powerful query language</span></span>](app-insights-analytics-tour.md)

<span data-ttu-id="b6a4f-136">Il rilevamento intelligente è completamente automatico,</span><span class="sxs-lookup"><span data-stu-id="b6a4f-136">Smart Detection is completely automatic.</span></span> <span data-ttu-id="b6a4f-137">Ma forse si vogliono tooset di alcune ulteriori avvisi?</span><span class="sxs-lookup"><span data-stu-id="b6a4f-137">But maybe you'd like tooset up some more alerts?</span></span>

* [<span data-ttu-id="b6a4f-138">Configurare manualmente gli avvisi relativi alle metriche</span><span class="sxs-lookup"><span data-stu-id="b6a4f-138">Manually configured metric alerts</span></span>](app-insights-alerts.md)
* [<span data-ttu-id="b6a4f-139">Test Web di disponibilità</span><span class="sxs-lookup"><span data-stu-id="b6a4f-139">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md) 

