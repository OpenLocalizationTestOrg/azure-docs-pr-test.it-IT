---
title: utilizzo di tooenable contesto utente aaaSending esperienze disponibili in Azure Application Insights | Documenti Microsoft
description: Tenere traccia degli spostamenti degli utenti nel servizio dopo aver assegnato a ognuno una stringa ID univoca e persistente in Application Insights.
services: application-insights
documentationcenter: 
author: abgreg
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: csharp
ms.topic: article
ms.date: 08/02/2017
ms.author: bwren
ms.openlocfilehash: 0e6c2348f53a3ea970060334179b0dd070925e82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
#  <a name="sending-user-context-tooenable-usage-experiences-in-azure-application-insights"></a>Si verifica l'invio di utilizzo tooenable contesto utente in Azure Application Insights

## <a name="tracking-users"></a>Monitorare gli utenti

Application Insights consente di toomonitor e tenere traccia degli utenti tramite un set di strumenti di gestione del prodotto: 
* [Utenti, sessioni ed eventi](https://docs.microsoft.com/azure/application-insights/app-insights-usage-segmentation)
* [Grafici a imbuto](https://docs.microsoft.com/azure/application-insights/usage-funnels)
* [Conservazione](https://docs.microsoft.com/azure/application-insights/app-insights-usage-retention)
* Coorte
* [Cartelle di lavoro](https://docs.microsoft.com/azure/application-insights/app-insights-usage-workbooks)

In ordine tootrack quali un utente esegue nel tempo, Application Insights è necessario un ID per ogni utente o sessione. Includere questi ID in ogni evento o visualizzazione pagina personalizzati.
- Utenti, grafici a imbuto, conservazione e coorti: includere l'ID utente.
- Sessioni: includere l'ID di sessione.

Se l'app è integrato con hello [JavaScript SDK](https://docs.microsoft.com/azure/application-insights/app-insights-javascript#set-up-application-insights-for-your-web-page), viene tenuta automaticamente traccia ID utente.

## <a name="choosing-user-ids"></a>Scelta degli ID utente

Gli ID utente devono essere rese persistenti tra tootrack sessioni utente come gli utenti si comportano nel tempo. Esistono diversi approcci per salvare in modo permanente ID hello
- Una definizione di un utente già presente nel servizio.
- Se il servizio di hello dispone accedere tooa browser, può passare browser hello un cookie con un ID in essa contenuti. ID Hello verranno mantenute per come cookie hello rimane nel browser dell'utente hello.
- Se necessario, è possibile utilizzare un nuovo ID di ogni sessione, ma saranno limitati risultati hello sugli utenti. Ad esempio, non sarà in grado di toosee come comportamento di un utente cambia nel tempo.

Hello ID deve essere un Guid o un'altra stringa tooidentify sufficientemente complessa ogni utente in modo univoco. Potrebbe essere, ad esempio, un numero lungo casuale.

Se ID hello contiene informazioni personali sull'utente hello, non è tooApplication di toosend Insights un valore appropriato come un ID utente. È possibile inviare tale ID come un [ID utente autenticato](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#authenticated-users), ma non soddisfa il requisito di ID utente di hello per scenari di utilizzo.

## <a name="aspnet-apps-set-user-context-in-an-itelemetryinitializer"></a>App ASP.NET: impostare il contesto utente in un ITelemetryInitializer

Creare un inizializzatore di telemetria, come descritto in dettaglio [qui](https://docs.microsoft.com/azure/application-insights/app-insights-api-filtering-sampling#add-properties-itelemetryinitializer)e impostare hello Context.User.Id e hello Context.Session.Id.

In questo esempio la identificatore hello utente ID tooan che scade dopo hello sessione. Se possibile, usare un ID utente che persiste tra le sessioni.

*C#*

```C#

    using System;
    using System.Web;
    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.Extensibility;

    namespace MvcWebRole.Telemetry
    {
      /*
       * Custom TelemetryInitializer that sets hello user ID.
       *
       */
      public class MyTelemetryInitializer : ITelemetryInitializer
      {
        public void Initialize(ITelemetry telemetry)
        {
            // For a full experience, track each user across sessions. For an incomplete view of user 
            // behavior within a session, store user ID on hello HttpContext Session.
            // Set hello user ID if we haven't done so yet.
            if (HttpContext.Current.Session["UserId"] == null)
            {
                HttpContext.Current.Session["UserId"] = Guid.NewGuid();
            }

            // Set hello user id on hello Application Insights telemetry item.
            telemetry.Context.User.Id = (string)HttpContext.Current.Session["UserId"];

            // Set hello session id on hello Application Insights telemetry item.
            telemetry.Context.Session.Id = HttpContext.Current.Session.SessionID;
        }
      }
    }
```

## <a name="next-steps"></a>Passaggi successivi
- utilizzo di tooenable esperienze, avviare l'invio [eventi personalizzati](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) o [visualizzazioni pagina](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).
- Se si invia già hello utilizzo strumenti toolearn di esplorare gli eventi personalizzati o le visualizzazioni di pagina, come gli utenti di usare il servizio.
    * [Panoramica sull'uso](app-insights-usage-overview.md)
    * [Utenti, Sessioni ed Eventi](app-insights-usage-segmentation.md)
    * [Grafici a imbuto](usage-funnels.md)
    * [Conservazione](app-insights-usage-retention.md)
    * [Cartelle di lavoro](app-insights-usage-workbooks.md)
