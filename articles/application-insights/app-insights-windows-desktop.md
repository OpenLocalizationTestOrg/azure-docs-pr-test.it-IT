---
title: utilizzo di aaaMonitoring e le prestazioni per le app desktop di Windows
description: Analizzare l'utilizzo e le prestazioni dell'applicazione desktop di Windows con HockeyApp e Application Insights.
services: application-insights
documentationcenter: windows
author: CFreemanwa
manager: carmonm
ms.assetid: 19040746-3315-47e7-8c60-4b3000d2ddc4
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/26/2016
ms.author: bwren
ms.openlocfilehash: 73806885a6f0ed3896c0e43308c90ba087007887
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-usage-and-performance-in-windows-desktop-apps"></a>Monitoraggio dell'utilizzo e delle prestazioni nelle applicazioni desktop di Windows


[Application Insights di Azure](app-insights-overview.md) e [HockeyApp](https://hockeyapp.net) consentono di monitorare l'utilizzo e le prestazioni dell'applicazione distribuita.

> [!IMPORTANT]
> È consigliabile [HockeyApp](https://hockeyapp.net) toodistribute e monitorare le app desktop e dispositivi. Con HockeyApp è possibile gestire la distribuzione, i test live e i commenti degli utenti, oltre a monitorare i report di utilizzo e di arresto anomalo. È anche possibile [esportare ed eseguire una query sui dati di telemetria con Analisi](app-insights-hockeyapp-bridge-app.md).
> 
> Anche se i dati di telemetria possono essere inviati tooApplication Insights da un'applicazione desktop, si tratta principalmente utile ai fini di debug e sperimentale.
> 
> 

## <a name="toosend-telemetry-tooapplication-insights-from-a-windows-application"></a>toosend telemetria tooApplication Insights da un'applicazione Windows
1. In hello [portale di Azure](https://portal.azure.com), [creare una risorsa di Application Insights](app-insights-create-new-resource.md). Scegliere l'app ASP.NET per il tipo di applicazione.
2. Eseguire una copia della chiave di strumentazione hello. Trovare la chiave di hello in hello Essentials elenco a discesa della nuova risorsa hello che appena creato. 
3. In Visual Studio, modificare i pacchetti NuGet hello del progetto dell'app e aggiungere Microsoft.ApplicationInsights.WindowsServer. In alternativa, scegliere Microsoft. applicationinsights, se si desidera hello API bare, senza i moduli di raccolta dati di telemetria standard hello.
4. Impostare la chiave di strumentazione hello nel codice:
   
    `TelemetryConfiguration.Active.InstrumentationKey = "`*nome della chiave*`";` 
   
    o in Applicationinsights (se è installato uno dei pacchetti di dati di telemetria standard hello):
   
    `<InstrumentationKey>`*chiave*`</InstrumentationKey>` 
   
    Se si utilizza Applicationinsights, assicurarsi che le relative proprietà in Esplora soluzioni vengono impostate troppo**Build Action = il contenuto, copia tooOutput Directory = copia**.
5. [Utilizzare l'API di hello](app-insights-api-custom-events-metrics.md) toosend telemetria.
6. Eseguire l'app e visualizzare i dati di telemetria hello nella risorsa hello creato nel portale di Azure hello.

## <a name="telemetry"></a>Codice di esempio
```C#

    public partial class Form1 : Form
    {
        private TelemetryClient tc = new TelemetryClient();
        ...
        private void Form1_Load(object sender, EventArgs e)
        {
            // Alternative toosetting ikey in config file:
            tc.InstrumentationKey = "key copied from portal";

            // Set session data:
            tc.Context.User.Id = Environment.UserName;
            tc.Context.Session.Id = Guid.NewGuid().ToString();
            tc.Context.Device.OperatingSystem = Environment.OSVersion.ToString();

            // Log a page view:
            tc.TrackPageView("Form1");
            ...
        }

        protected override void OnClosing(CancelEventArgs e)
        {
            stop = true;
            if (tc != null)
            {
                tc.Flush(); // only for desktop apps

                // Allow time for flushing:
                System.Threading.Thread.Sleep(1000);
            }
            base.OnClosing(e);
        }

```

## <a name="next-steps"></a>Passaggi successivi
* [Creare un dashboard](app-insights-dashboards.md)
* [Ricerca diagnostica](app-insights-diagnostic-search.md)
* [Esplorare le metriche](app-insights-metrics-explorer.md)
* [Scrivere query di Analisi](app-insights-analytics.md)

