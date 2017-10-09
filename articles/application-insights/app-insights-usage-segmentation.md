---
title: analisi aaaUser, sessione ed eventi in Application Insights di Azure | Documenti Microsoft
description: Analisi demografica degli utenti dell'app Web.
services: application-insights
documentationcenter: 
author: botatoes
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/03/2017
ms.author: bwren
ms.openlocfilehash: 152ab90e9a25c03087d3ebbde1263ec72acb227e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="users-sessions-and-events-analysis-in-application-insights"></a><span data-ttu-id="d8692-103">Analisi di utenti, sessioni ed eventi in Application Insights</span><span class="sxs-lookup"><span data-stu-id="d8692-103">Users, sessions, and events analysis in Application Insights</span></span>

<span data-ttu-id="d8692-104">Scoprire quando le persone usano l'app Web, a quali pagine sono più interessati, dove si trovano, quali browser e sistemi operativi usano.</span><span class="sxs-lookup"><span data-stu-id="d8692-104">Find out when people use your web app, what pages they're most interested in, where your users are located, what browsers and operating systems they use.</span></span> <span data-ttu-id="d8692-105">Analizzare i dati di telemetria sull'utilizzo e sull'azienda con [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d8692-105">Analyze business and usage telemetry by using [Azure Application Insights](app-insights-overview.md).</span></span>

## <a name="get-started"></a><span data-ttu-id="d8692-106">Attività iniziali</span><span class="sxs-lookup"><span data-stu-id="d8692-106">Get started</span></span>

<span data-ttu-id="d8692-107">Se non viene visualizzato ancora dati hello utenti, sessioni o blade eventi nel portale Application Insights hello [informazioni su come tooget iniziare con strumenti di gestione di hello](app-insights-usage-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d8692-107">If you don't yet see data in hello users, sessions, or events blades in hello Application Insights portal, [learn how tooget started with hello usage tools](app-insights-usage-overview.md).</span></span>

## <a name="hello-users-sessions-and-events-segmentation-tool"></a><span data-ttu-id="d8692-108">strumento di segmentazione Hello utenti, sessioni e gli eventi</span><span class="sxs-lookup"><span data-stu-id="d8692-108">hello Users, Sessions, and Events segmentation tool</span></span>

<span data-ttu-id="d8692-109">Tre di utilizzo di hello pannelli utilizzano hello stesso strumento tooslice e il dicing dei dati di telemetria dall'app web da tre diverse prospettive.</span><span class="sxs-lookup"><span data-stu-id="d8692-109">Three of hello usage blades use hello same tool tooslice and dice telemetry from your web app from three perspectives.</span></span> <span data-ttu-id="d8692-110">Applicazione di filtri e suddividere i dati di hello, consente di individuare informazioni dettagliate sull'utilizzo del relativo hello di pagine e funzionalità diverse.</span><span class="sxs-lookup"><span data-stu-id="d8692-110">By filtering and splitting hello data, you can uncover insights about hello relative usage of different pages and features.</span></span>

* <span data-ttu-id="d8692-111">**Strumento Utenti**: numero di persone che hanno usato l'app e le relative funzionalità.</span><span class="sxs-lookup"><span data-stu-id="d8692-111">**Users tool**: How many people used your app and its features.</span></span>  <span data-ttu-id="d8692-112">Gli utenti vengono conteggiati tramite ID anonimi memorizzati nei cookie del browser.</span><span class="sxs-lookup"><span data-stu-id="d8692-112">Users are counted by using anonymous IDs stored in browser cookies.</span></span> <span data-ttu-id="d8692-113">Una singola persona che usa browser o computer diversi verrà conteggiata più di una volta.</span><span class="sxs-lookup"><span data-stu-id="d8692-113">A single person using different browsers or machines will be counted as more than one user.</span></span>
* <span data-ttu-id="d8692-114">**Strumento Sessioni**: il numero di sessioni delle attività dell'utente che include determinate pagine e funzionalità dell'app.</span><span class="sxs-lookup"><span data-stu-id="d8692-114">**Sessions tool**: How many sessions of user activity have included certain pages and features of your app.</span></span> <span data-ttu-id="d8692-115">Una sessione viene conteggiata dopo mezz'ora di inattività dell'utente o in seguito a un uso continuo di 24 ore.</span><span class="sxs-lookup"><span data-stu-id="d8692-115">A session is counted after half an hour of user inactivity, or after continuous 24h of use.</span></span>
* <span data-ttu-id="d8692-116">**Strumento Eventi**: la frequenza con cui vengono usate alcune pagine e funzionalità dell'app.</span><span class="sxs-lookup"><span data-stu-id="d8692-116">**Events tool**: How often certain pages and features of your app are used.</span></span> <span data-ttu-id="d8692-117">La visualizzazione di una pagina viene conteggiata quando un browser carica la pagina dell'app, purché sia stata [instrumentata](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="d8692-117">A page view is counted when a browser loads a page from your app, provided you have [instrumented it](app-insights-javascript.md).</span></span> 

    <span data-ttu-id="d8692-118">Un evento personalizzato rappresenta un'occorrenza di un problema verificatosi nell'app, spesso un'interazione dell'utente fare clic su un pulsante o hello completamento di alcune delle attività.</span><span class="sxs-lookup"><span data-stu-id="d8692-118">A custom event represents one occurrence of something happening in your app, often a user interaction like a button click or hello completion of some task.</span></span> <span data-ttu-id="d8692-119">Inserire codice nell'app troppo[generare eventi personalizzati](app-insights-api-custom-events-metrics.md#trackevent).</span><span class="sxs-lookup"><span data-stu-id="d8692-119">You insert code in your app too[generate custom events](app-insights-api-custom-events-metrics.md#trackevent).</span></span>

![Strumento Uso](./media/app-insights-usage-segmentation/users.png)

## <a name="querying-for-certain-users"></a><span data-ttu-id="d8692-121">Esecuzione di query per determinati utenti</span><span class="sxs-lookup"><span data-stu-id="d8692-121">Querying for Certain Users</span></span> 

<span data-ttu-id="d8692-122">Esplorare i diversi gruppi di utenti modificando le opzioni di query hello nella parte superiore di hello dello strumento di hello utenti:</span><span class="sxs-lookup"><span data-stu-id="d8692-122">Explore different groups of users by adjusting hello query options at hello top of hello Users tool:</span></span> 

* <span data-ttu-id="d8692-123">Who used (Usato da): scegliere gli eventi personalizzati e le visualizzazioni di pagina.</span><span class="sxs-lookup"><span data-stu-id="d8692-123">Who used: Choose custom events and page views.</span></span> 
* <span data-ttu-id="d8692-124">Durante: scegliere un intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="d8692-124">During: Choose a time range.</span></span> 
* <span data-ttu-id="d8692-125">Da: Scegliere come toobucket hello dati, per un periodo di tempo o da un'altra proprietà, ad esempio browser o una città.</span><span class="sxs-lookup"><span data-stu-id="d8692-125">By: Choose how toobucket hello data, either by a period of time or by another property such as browser or city.</span></span> 
* <span data-ttu-id="d8692-126">Divisione: Scegliere una proprietà per i dati di hello toosplit o segmento.</span><span class="sxs-lookup"><span data-stu-id="d8692-126">Split By: Choose a property by which toosplit or segment hello data.</span></span> 
* <span data-ttu-id="d8692-127">Aggiungere filtri: Limitare hello query toocertain utenti, sessioni o gli eventi in base alle relative proprietà, ad esempio browser o una città.</span><span class="sxs-lookup"><span data-stu-id="d8692-127">Add Filters: Limit hello query toocertain users, sessions, or events based on their properties, such as browser or city.</span></span> 
 
## <a name="saving-and-sharing-reports"></a><span data-ttu-id="d8692-128">Salvataggio e condivisione di report</span><span class="sxs-lookup"><span data-stu-id="d8692-128">Saving and sharing reports</span></span> 
<span data-ttu-id="d8692-129">È possibile salvare i report agli utenti, entrambi tooyou privata solo nella sezione report personali hello o condivisi con tutti gli utenti con accesso toothis risorsa di Application Insights hello sezione report condiviso.</span><span class="sxs-lookup"><span data-stu-id="d8692-129">You can save Users reports, either private just tooyou in hello My Reports section, or shared with everyone else with access toothis Application Insights resource in hello Shared Reports section.</span></span>  
 
<span data-ttu-id="d8692-130">Durante il salvataggio di un report o la modifica delle proprietà, scegliere "Intervallo di tempo relativo corrente" toosave che un report verrà continuamente l'aggiornamento dati, se si torna indietro certa quantità di tempo fisso.</span><span class="sxs-lookup"><span data-stu-id="d8692-130">While saving a report or editing its properties, choose "Current Relative Time Range" toosave a report will continuously refreshed data, going back some fixed amount of time.</span></span>  
 
<span data-ttu-id="d8692-131">Scegliere "Intervallo di tempo assoluto corrente" toosave un report con un set di dati predefinito.</span><span class="sxs-lookup"><span data-stu-id="d8692-131">Choose "Current Absolute Time Range" toosave a report with a fixed set of data.</span></span> <span data-ttu-id="d8692-132">Tenere presente che i dati in Application Insights viene archiviati solo per 90 giorni, pertanto se sono trascorsi più di 90 giorni da un report con un intervallo di tempo assoluto è stato salvato, report hello apparirà vuoto.</span><span class="sxs-lookup"><span data-stu-id="d8692-132">Keep in mind that data in Application Insights is only stored for 90 days, so if more than 90 days have passed since a report with an absolute time range was saved, hello report will appear empty.</span></span> 
 
## <a name="example-instances"></a><span data-ttu-id="d8692-133">Istanze di esempio</span><span class="sxs-lookup"><span data-stu-id="d8692-133">Example instances</span></span>

<span data-ttu-id="d8692-134">sezione di esempio istanze Hello Mostra informazioni su un numero limitato di singoli utenti, sessioni o gli eventi corrispondenti a query corrente hello.</span><span class="sxs-lookup"><span data-stu-id="d8692-134">hello Example instances section shows information about a handful of individual users, sessions, or events that are matched by hello current query.</span></span> <span data-ttu-id="d8692-135">Prendere in considerazione ed esplorare i comportamenti di hello dei singoli utenti, in aggiunta tooaggregates, forniscono informazioni dettagliate sul modo le persone usano effettivamente l'app.</span><span class="sxs-lookup"><span data-stu-id="d8692-135">Considering and exploring hello behaviors of individuals, in addition tooaggregates, can provide insights about how people actually use your app.</span></span> 
 
## <a name="insights"></a><span data-ttu-id="d8692-136">Informazioni dettagliate</span><span class="sxs-lookup"><span data-stu-id="d8692-136">Insights</span></span> 

<span data-ttu-id="d8692-137">intestazione laterale approfondimenti Hello Mostra cluster di grandi dimensioni di utenti che condividono le proprietà comuni.</span><span class="sxs-lookup"><span data-stu-id="d8692-137">hello Insights sidebar shows large clusters of users that share common properties.</span></span> <span data-ttu-id="d8692-138">Questi cluster consentono di individuare andamenti sorprendenti sulle modalità di uso dell'app.</span><span class="sxs-lookup"><span data-stu-id="d8692-138">These clusters can uncover surprising trends in how people use your app.</span></span> <span data-ttu-id="d8692-139">Se ad esempio 40% di utilizzo di hello dell'app tutti provengono da utenti che utilizzano una singola funzionalità.</span><span class="sxs-lookup"><span data-stu-id="d8692-139">For example, if 40% of all of hello usage of your app comes from people using a single feature.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="d8692-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d8692-140">Next steps</span></span>
- <span data-ttu-id="d8692-141">utilizzo di tooenable esperienze, avviare l'invio [eventi personalizzati](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) o [visualizzazioni pagina](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="d8692-141">tooenable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="d8692-142">Se si invia già hello utilizzo strumenti toolearn di esplorare gli eventi personalizzati o le visualizzazioni di pagina, come gli utenti di usare il servizio.</span><span class="sxs-lookup"><span data-stu-id="d8692-142">If you already send custom events or page views, explore hello Usage tools toolearn how users use your service.</span></span>
    - [<span data-ttu-id="d8692-143">Grafici a imbuto</span><span class="sxs-lookup"><span data-stu-id="d8692-143">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="d8692-144">Conservazione</span><span class="sxs-lookup"><span data-stu-id="d8692-144">Retention</span></span>](app-insights-usage-retention.md)
    - [<span data-ttu-id="d8692-145">Flussi degli utenti</span><span class="sxs-lookup"><span data-stu-id="d8692-145">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="d8692-146">Cartelle di lavoro</span><span class="sxs-lookup"><span data-stu-id="d8692-146">Workbooks</span></span>](app-insights-usage-workbooks.md)
    - [<span data-ttu-id="d8692-147">Aggiungere il contesto utente</span><span class="sxs-lookup"><span data-stu-id="d8692-147">Add user context</span></span>](app-insights-usage-send-user-context.md)

