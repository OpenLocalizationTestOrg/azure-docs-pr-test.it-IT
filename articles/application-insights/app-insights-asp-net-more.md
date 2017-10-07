---
title: aaaGet meglio Azure Application Insights | Documenti Microsoft
description: "Dopo l'introduzione ad Application Insights, ecco un riepilogo delle funzionalità di hello che è possibile esplorare."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 7ec10a2d-c669-448d-8d45-b486ee32c8db
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: bwren
ms.openlocfilehash: 2023728afcf5aa5ecab8b957c8517d4872668765
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="more-telemetry-from-application-insights"></a>Altri dati di telemetria da Application Insights
Dopo aver [aggiunto codice ASP.NET di Application Insights tooyour](app-insights-asp-net.md), esistono alcune operazioni che è possibile eseguire tooget anche ulteriori dati di telemetria. 

| Azione | Risultato finale|
|---|---|
|(Server IIS) [Installare Status Monitor](http://go.microsoft.com/fwlink/?LinkId=506648) in ogni computer server.<br/>(App web di azure) Nel Pannello di controllo Azure hello per app web hello, aprire il pannello di Application Insights hello.| [**Contatori delle prestazioni**](app-insights-performance-counters.md)<br/>[**Eccezioni**](app-insights-asp-net-exceptions.md): analisi dello stack dettagliate<br/>[**Dipendenze**](app-insights-asp-net-dependencies.md)|
|[Aggiungere le pagine web hello JavaScript frammento tooyour](app-insights-javascript.md)|[Prestazioni delle pagine](app-insights-web-track-usage.md), eccezioni del browser, prestazioni AJAX. Telemetria personalizzata sul lato client.|
|[Creare test Web di disponibilità](app-insights-monitor-web-app-availability.md)|Ricevere avvisi se il sito diventa non disponibile|
|[Assicurarsi che buildinfo.config](https://msdn.microsoft.com/library/dn449058.aspx) sia generato da MSBuild|[Creare annotazioni nei grafici di metriche](https://blogs.msdn.microsoft.com/visualstudioalm/2013/11/14/implementing-deployment-markers-in-application-insights/)
|[Scrivere eventi e metriche personalizzati](app-insights-api-custom-events-metrics.md)|Conteggiare eventi aziendali e metriche, tenere traccia dell'uso dettagliato e altro ancora.|
|[Profilatura del sito live](https://aka.ms/AIProfilerPreview)|Intervalli di funzione dettagliati dall'app Web live|






