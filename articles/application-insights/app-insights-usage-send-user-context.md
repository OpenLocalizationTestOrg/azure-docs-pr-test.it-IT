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
#  <a name="sending-user-context-tooenable-usage-experiences-in-azure-application-insights"></a><span data-ttu-id="6420c-103">Si verifica l'invio di utilizzo tooenable contesto utente in Azure Application Insights</span><span class="sxs-lookup"><span data-stu-id="6420c-103">Sending user context tooenable usage experiences in Azure Application Insights</span></span>

## <a name="tracking-users"></a><span data-ttu-id="6420c-104">Monitorare gli utenti</span><span class="sxs-lookup"><span data-stu-id="6420c-104">Tracking users</span></span>

<span data-ttu-id="6420c-105">Application Insights consente di toomonitor e tenere traccia degli utenti tramite un set di strumenti di gestione del prodotto:</span><span class="sxs-lookup"><span data-stu-id="6420c-105">Application Insights enables you toomonitor and track your users through a set of product usage tools:</span></span> 
* [<span data-ttu-id="6420c-106">Utenti, sessioni ed eventi</span><span class="sxs-lookup"><span data-stu-id="6420c-106">Users, Sessions, Events</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-segmentation)
* [<span data-ttu-id="6420c-107">Grafici a imbuto</span><span class="sxs-lookup"><span data-stu-id="6420c-107">Funnels</span></span>](https://docs.microsoft.com/azure/application-insights/usage-funnels)
* [<span data-ttu-id="6420c-108">Conservazione</span><span class="sxs-lookup"><span data-stu-id="6420c-108">Retention</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-retention)
* <span data-ttu-id="6420c-109">Coorte</span><span class="sxs-lookup"><span data-stu-id="6420c-109">Cohorts</span></span>
* [<span data-ttu-id="6420c-110">Cartelle di lavoro</span><span class="sxs-lookup"><span data-stu-id="6420c-110">Workbooks</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-workbooks)

<span data-ttu-id="6420c-111">In ordine tootrack quali un utente esegue nel tempo, Application Insights è necessario un ID per ogni utente o sessione.</span><span class="sxs-lookup"><span data-stu-id="6420c-111">In order tootrack what a user does over time, Application Insights needs an ID for each user or session.</span></span> <span data-ttu-id="6420c-112">Includere questi ID in ogni evento o visualizzazione pagina personalizzati.</span><span class="sxs-lookup"><span data-stu-id="6420c-112">Include these IDs in every custom event or page view.</span></span>
- <span data-ttu-id="6420c-113">Utenti, grafici a imbuto, conservazione e coorti: includere l'ID utente.</span><span class="sxs-lookup"><span data-stu-id="6420c-113">Users, Funnels, Retention, and Cohorts: Include user ID.</span></span>
- <span data-ttu-id="6420c-114">Sessioni: includere l'ID di sessione.</span><span class="sxs-lookup"><span data-stu-id="6420c-114">Sessions: Include session ID.</span></span>

<span data-ttu-id="6420c-115">Se l'app è integrato con hello [JavaScript SDK](https://docs.microsoft.com/azure/application-insights/app-insights-javascript#set-up-application-insights-for-your-web-page), viene tenuta automaticamente traccia ID utente.</span><span class="sxs-lookup"><span data-stu-id="6420c-115">If your app is integrated with hello [JavaScript SDK](https://docs.microsoft.com/azure/application-insights/app-insights-javascript#set-up-application-insights-for-your-web-page), user ID is tracked automatically.</span></span>

## <a name="choosing-user-ids"></a><span data-ttu-id="6420c-116">Scelta degli ID utente</span><span class="sxs-lookup"><span data-stu-id="6420c-116">Choosing user IDs</span></span>

<span data-ttu-id="6420c-117">Gli ID utente devono essere rese persistenti tra tootrack sessioni utente come gli utenti si comportano nel tempo.</span><span class="sxs-lookup"><span data-stu-id="6420c-117">User IDs should persist across user sessions tootrack how users behave over time.</span></span> <span data-ttu-id="6420c-118">Esistono diversi approcci per salvare in modo permanente ID hello</span><span class="sxs-lookup"><span data-stu-id="6420c-118">There are various approaches for persisting hello ID.</span></span>
- <span data-ttu-id="6420c-119">Una definizione di un utente già presente nel servizio.</span><span class="sxs-lookup"><span data-stu-id="6420c-119">A definition of a user that you already have in your service.</span></span>
- <span data-ttu-id="6420c-120">Se il servizio di hello dispone accedere tooa browser, può passare browser hello un cookie con un ID in essa contenuti.</span><span class="sxs-lookup"><span data-stu-id="6420c-120">If hello service has access tooa browser, it can pass hello browser a cookie with an ID in it.</span></span> <span data-ttu-id="6420c-121">ID Hello verranno mantenute per come cookie hello rimane nel browser dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="6420c-121">hello ID will persist for as long as hello cookie remains in hello user's browser.</span></span>
- <span data-ttu-id="6420c-122">Se necessario, è possibile utilizzare un nuovo ID di ogni sessione, ma saranno limitati risultati hello sugli utenti.</span><span class="sxs-lookup"><span data-stu-id="6420c-122">If necessary, you can use a new ID each session, but hello results about users will be limited.</span></span> <span data-ttu-id="6420c-123">Ad esempio, non sarà in grado di toosee come comportamento di un utente cambia nel tempo.</span><span class="sxs-lookup"><span data-stu-id="6420c-123">For example, you won't be able toosee how a user's behavior changes over time.</span></span>

<span data-ttu-id="6420c-124">Hello ID deve essere un Guid o un'altra stringa tooidentify sufficientemente complessa ogni utente in modo univoco.</span><span class="sxs-lookup"><span data-stu-id="6420c-124">hello ID should be a Guid or another string complex enough tooidentify each user uniquely.</span></span> <span data-ttu-id="6420c-125">Potrebbe essere, ad esempio, un numero lungo casuale.</span><span class="sxs-lookup"><span data-stu-id="6420c-125">For example, it could be a long random number.</span></span>

<span data-ttu-id="6420c-126">Se ID hello contiene informazioni personali sull'utente hello, non è tooApplication di toosend Insights un valore appropriato come un ID utente.</span><span class="sxs-lookup"><span data-stu-id="6420c-126">If hello ID contains personally identifying information about hello user, it is not an appropriate value toosend tooApplication Insights as a user ID.</span></span> <span data-ttu-id="6420c-127">È possibile inviare tale ID come un [ID utente autenticato](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#authenticated-users), ma non soddisfa il requisito di ID utente di hello per scenari di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="6420c-127">You can send such an ID as an [authenticated user ID](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#authenticated-users), but it does not fulfill hello user ID requirement for usage scenarios.</span></span>

## <a name="aspnet-apps-set-user-context-in-an-itelemetryinitializer"></a><span data-ttu-id="6420c-128">App ASP.NET: impostare il contesto utente in un ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="6420c-128">ASP.NET Apps: Set user context in an ITelemetryInitializer</span></span>

<span data-ttu-id="6420c-129">Creare un inizializzatore di telemetria, come descritto in dettaglio [qui](https://docs.microsoft.com/azure/application-insights/app-insights-api-filtering-sampling#add-properties-itelemetryinitializer)e impostare hello Context.User.Id e hello Context.Session.Id.</span><span class="sxs-lookup"><span data-stu-id="6420c-129">Create a telemetry initializer, as described in detail [here](https://docs.microsoft.com/azure/application-insights/app-insights-api-filtering-sampling#add-properties-itelemetryinitializer), and set hello Context.User.Id and hello Context.Session.Id.</span></span>

<span data-ttu-id="6420c-130">In questo esempio la identificatore hello utente ID tooan che scade dopo hello sessione.</span><span class="sxs-lookup"><span data-stu-id="6420c-130">This example sets hello user ID tooan identifier that expires after hello session.</span></span> <span data-ttu-id="6420c-131">Se possibile, usare un ID utente che persiste tra le sessioni.</span><span class="sxs-lookup"><span data-stu-id="6420c-131">If possible, use a user ID that persists across sessions.</span></span>

<span data-ttu-id="6420c-132">*C#*</span><span class="sxs-lookup"><span data-stu-id="6420c-132">*C#*</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="6420c-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6420c-133">Next steps</span></span>
- <span data-ttu-id="6420c-134">utilizzo di tooenable esperienze, avviare l'invio [eventi personalizzati](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) o [visualizzazioni pagina](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="6420c-134">tooenable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="6420c-135">Se si invia già hello utilizzo strumenti toolearn di esplorare gli eventi personalizzati o le visualizzazioni di pagina, come gli utenti di usare il servizio.</span><span class="sxs-lookup"><span data-stu-id="6420c-135">If you already send custom events or page views, explore hello Usage tools toolearn how users use your service.</span></span>
    * [<span data-ttu-id="6420c-136">Panoramica sull'uso</span><span class="sxs-lookup"><span data-stu-id="6420c-136">Usage overview</span></span>](app-insights-usage-overview.md)
    * [<span data-ttu-id="6420c-137">Utenti, Sessioni ed Eventi</span><span class="sxs-lookup"><span data-stu-id="6420c-137">Users, Sessions, and Events</span></span>](app-insights-usage-segmentation.md)
    * [<span data-ttu-id="6420c-138">Grafici a imbuto</span><span class="sxs-lookup"><span data-stu-id="6420c-138">Funnels</span></span>](usage-funnels.md)
    * [<span data-ttu-id="6420c-139">Conservazione</span><span class="sxs-lookup"><span data-stu-id="6420c-139">Retention</span></span>](app-insights-usage-retention.md)
    * [<span data-ttu-id="6420c-140">Cartelle di lavoro</span><span class="sxs-lookup"><span data-stu-id="6420c-140">Workbooks</span></span>](app-insights-usage-workbooks.md)
