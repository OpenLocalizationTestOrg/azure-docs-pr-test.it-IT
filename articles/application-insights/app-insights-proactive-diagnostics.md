---
title: Rilevamento intelligente in Azure Application Insights | Microsoft Docs
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
ms.openlocfilehash: f203b2a532ea721d9797c67a4750896e3ab2b9f7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="smart-detection-in-application-insights"></a><span data-ttu-id="03052-103">Rilevamento intelligente in Application Insights</span><span class="sxs-lookup"><span data-stu-id="03052-103">Smart Detection in Application Insights</span></span>
 <span data-ttu-id="03052-104">Il rilevamento intelligente segnala automaticamente i potenziali problemi di prestazioni nell'applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="03052-104">Smart Detection automatically warns you of potential performance problems in your web application.</span></span> <span data-ttu-id="03052-105">Esegue l'analisi proattiva dei dati di telemetria che l'app invia ad [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="03052-105">It performs proactive analysis of the telemetry that your app sends to [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="03052-106">Se si verifica un improvviso aumento della percentuale di errori o in caso di modelli anomali delle prestazioni di client o server, viene generato un avviso.</span><span class="sxs-lookup"><span data-stu-id="03052-106">If there is a sudden rise in failure rates, or abnormal patterns in client or server performance, you get an alert.</span></span> <span data-ttu-id="03052-107">Questa funzionalità non richiede alcuna configurazione.</span><span class="sxs-lookup"><span data-stu-id="03052-107">This feature needs no configuration.</span></span> <span data-ttu-id="03052-108">Funziona se l'applicazione invia dati di telemetria sufficienti.</span><span class="sxs-lookup"><span data-stu-id="03052-108">It operates if your application sends enough telemetry.</span></span>

<span data-ttu-id="03052-109">È possibile accedere agli avvisi della funzionalità di rilevamento intelligente dai messaggi di posta elettronica ricevuti e dal pannello Smart Detection (Rilevamento intelligente).</span><span class="sxs-lookup"><span data-stu-id="03052-109">You can access Smart Detection alerts both from the emails you receive, and from the Smart Detection blade.</span></span>

## <a name="review-your-smart-detections"></a><span data-ttu-id="03052-110">Esaminare i rilevamenti intelligenti</span><span class="sxs-lookup"><span data-stu-id="03052-110">Review your Smart Detections</span></span>
<span data-ttu-id="03052-111">È possibile individuare i rilevamenti in due modi:</span><span class="sxs-lookup"><span data-stu-id="03052-111">You can discover detections in two ways:</span></span>

* <span data-ttu-id="03052-112">**Viene visualizzato un messaggio di posta elettronica** da Application Insights.</span><span class="sxs-lookup"><span data-stu-id="03052-112">**You receive an email** from Application Insights.</span></span> <span data-ttu-id="03052-113">Ecco un esempio tipico:</span><span class="sxs-lookup"><span data-stu-id="03052-113">Here's a typical example:</span></span>
  
    ![Avviso di posta elettronica](./media/app-insights-proactive-diagnostics/03.png)
  
    <span data-ttu-id="03052-115">Fare clic sul pulsante grande per visualizzare altri dettagli nel portale.</span><span class="sxs-lookup"><span data-stu-id="03052-115">Click the big button to open more detail in the portal.</span></span>
* <span data-ttu-id="03052-116">Il **riquadro Smart Detection (Rilevamento intelligente)** nel pannello della panoramica dell'app visualizza il numero di avvisi recenti.</span><span class="sxs-lookup"><span data-stu-id="03052-116">**The Smart Detection tile** on your app's overview blade shows a count of recent alerts.</span></span> <span data-ttu-id="03052-117">Fare clic sul riquadro per visualizzare un elenco degli avvisi recenti.</span><span class="sxs-lookup"><span data-stu-id="03052-117">Click the tile to see a list of recent alerts.</span></span>

![Visualizzare rilevamenti recenti](./media/app-insights-proactive-diagnostics/04.png)

<span data-ttu-id="03052-119">Selezionare un avviso per visualizzarne i dettagli.</span><span class="sxs-lookup"><span data-stu-id="03052-119">Select an alert to see its details.</span></span>

## <a name="what-problems-are-detected"></a><span data-ttu-id="03052-120">Tipi di problemi rilevati</span><span class="sxs-lookup"><span data-stu-id="03052-120">What problems are detected?</span></span>
<span data-ttu-id="03052-121">Esistono tre tipologie di rilevamento:</span><span class="sxs-lookup"><span data-stu-id="03052-121">There are three kinds of detection:</span></span>

* <span data-ttu-id="03052-122">[Rilevamento intelligente: anomalie negli errori](app-insights-proactive-failure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="03052-122">[Smart detection - Failure Anomalies](app-insights-proactive-failure-diagnostics.md).</span></span> <span data-ttu-id="03052-123">Si usa Machine Learning per impostare la frequenza prevista delle richieste non riuscite per l'app, in correlazione con il carico e altri fattori.</span><span class="sxs-lookup"><span data-stu-id="03052-123">We use machine learning to set the expected rate of failed requests for your app, correlating with load and other factors.</span></span> <span data-ttu-id="03052-124">Se la percentuale di errori supera la prevista, viene inviato un avviso.</span><span class="sxs-lookup"><span data-stu-id="03052-124">If the failure rate goes outside the expected envelope, we send an alert.</span></span>
* <span data-ttu-id="03052-125">[Rilevamento intelligente: anomalie nelle prestazioni](app-insights-proactive-performance-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="03052-125">[Smart detection - Performance Anomalies](app-insights-proactive-performance-diagnostics.md).</span></span> <span data-ttu-id="03052-126">Vengono inviate notifiche se il tempo di risposta di un'operazione o la durata delle dipendenze sta rallentando rispetto alla baseline cronologica o se viene identificato un modello anomalo nel tempo di risposta o di caricamento pagina.</span><span class="sxs-lookup"><span data-stu-id="03052-126">You get notifications if response time of an operation or dependency duration is slowing down compared to historical baseline or if we identify an anomalous pattern in response time or page load time.</span></span>   
* <span data-ttu-id="03052-127">[Rilevamento intelligente: problemi del servizio cloud di Azure](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/).</span><span class="sxs-lookup"><span data-stu-id="03052-127">[Smart detection - Azure Cloud Service issues](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/).</span></span> <span data-ttu-id="03052-128">Vengono inviati avvisi all'utente se l'app è ospitata in Servizi cloud di Azure e un'istanza del ruolo presenta errori di avvio, ricicli frequenti o arresti anomali del sistema in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="03052-128">You get alerts if your app is hosted in Azure Cloud Services and a role instance has startup failures, frequent recycling, or runtime crashes.</span></span>

<span data-ttu-id="03052-129">I collegamenti della Guida in ogni notifica consentono di vedere gli articoli pertinenti.</span><span class="sxs-lookup"><span data-stu-id="03052-129">(The help links in each notification take you to the relevant articles.)</span></span>

## <a name="video"></a><span data-ttu-id="03052-130">Video</span><span class="sxs-lookup"><span data-stu-id="03052-130">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="03052-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="03052-131">Next steps</span></span>
<span data-ttu-id="03052-132">Gli strumenti di diagnostica seguenti consentono di controllare la telemetria dall'app:</span><span class="sxs-lookup"><span data-stu-id="03052-132">These diagnostic tools help you inspect the telemetry from your app:</span></span>

* [<span data-ttu-id="03052-133">Esplora metriche</span><span class="sxs-lookup"><span data-stu-id="03052-133">Metric explorer</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="03052-134">Esplora ricerche</span><span class="sxs-lookup"><span data-stu-id="03052-134">Search explorer</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="03052-135">Linguaggio avanzato di query di Analisi</span><span class="sxs-lookup"><span data-stu-id="03052-135">Analytics - powerful query language</span></span>](app-insights-analytics-tour.md)

<span data-ttu-id="03052-136">Il rilevamento intelligente è completamente automatico,</span><span class="sxs-lookup"><span data-stu-id="03052-136">Smart Detection is completely automatic.</span></span> <span data-ttu-id="03052-137">tuttavia è possibile configurare avvisi aggiuntivi, se necessario.</span><span class="sxs-lookup"><span data-stu-id="03052-137">But maybe you'd like to set up some more alerts?</span></span>

* [<span data-ttu-id="03052-138">Configurare manualmente gli avvisi relativi alle metriche</span><span class="sxs-lookup"><span data-stu-id="03052-138">Manually configured metric alerts</span></span>](app-insights-alerts.md)
* [<span data-ttu-id="03052-139">Test Web di disponibilità</span><span class="sxs-lookup"><span data-stu-id="03052-139">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md) 

