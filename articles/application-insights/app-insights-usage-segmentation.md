---
title: Analisi di utenti, sessioni ed eventi in Azure Application Insights | Microsoft Docs
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
ms.openlocfilehash: b154a01d1690bff4950ebc1ff5a5b89894d4d111
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="users-sessions-and-events-analysis-in-application-insights"></a><span data-ttu-id="6123e-103">Analisi di utenti, sessioni ed eventi in Application Insights</span><span class="sxs-lookup"><span data-stu-id="6123e-103">Users, sessions, and events analysis in Application Insights</span></span>

<span data-ttu-id="6123e-104">Scoprire quando le persone usano l'app Web, a quali pagine sono più interessati, dove si trovano, quali browser e sistemi operativi usano.</span><span class="sxs-lookup"><span data-stu-id="6123e-104">Find out when people use your web app, what pages they're most interested in, where your users are located, what browsers and operating systems they use.</span></span> <span data-ttu-id="6123e-105">Analizzare i dati di telemetria sull'utilizzo e sull'azienda con [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6123e-105">Analyze business and usage telemetry by using [Azure Application Insights](app-insights-overview.md).</span></span>

## <a name="get-started"></a><span data-ttu-id="6123e-106">Attività iniziali</span><span class="sxs-lookup"><span data-stu-id="6123e-106">Get started</span></span>

<span data-ttu-id="6123e-107">Se nei pannelli degli utenti, delle sessioni e degli eventi nel portale di Application Insights non vengono ancora visualizzati i dati, leggere le [informazioni su come iniziare a usare gli strumenti d'uso](app-insights-usage-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6123e-107">If you don't yet see data in the users, sessions, or events blades in the Application Insights portal, [learn how to get started with the usage tools](app-insights-usage-overview.md).</span></span>

## <a name="the-users-sessions-and-events-segmentation-tool"></a><span data-ttu-id="6123e-108">Strumenti di segmentazione di Utenti, Sessioni ed Eventi</span><span class="sxs-lookup"><span data-stu-id="6123e-108">The Users, Sessions, and Events segmentation tool</span></span>

<span data-ttu-id="6123e-109">Tre pannelli d'uso usano lo stesso strumento per effettuare un'analisi approfondita dei dati di telemetria dell'app Web da tre diverse prospettive.</span><span class="sxs-lookup"><span data-stu-id="6123e-109">Three of the usage blades use the same tool to slice and dice telemetry from your web app from three perspectives.</span></span> <span data-ttu-id="6123e-110">Applicando i filtri e dividendo i dati, si possono scoprire informazioni dettagliate sull'uso di pagine e funzionalità diverse.</span><span class="sxs-lookup"><span data-stu-id="6123e-110">By filtering and splitting the data, you can uncover insights about the relative usage of different pages and features.</span></span>

* <span data-ttu-id="6123e-111">**Strumento Utenti**: numero di persone che hanno usato l'app e le relative funzionalità.</span><span class="sxs-lookup"><span data-stu-id="6123e-111">**Users tool**: How many people used your app and its features.</span></span>  <span data-ttu-id="6123e-112">Gli utenti vengono conteggiati tramite ID anonimi memorizzati nei cookie del browser.</span><span class="sxs-lookup"><span data-stu-id="6123e-112">Users are counted by using anonymous IDs stored in browser cookies.</span></span> <span data-ttu-id="6123e-113">Una singola persona che usa browser o computer diversi verrà conteggiata più di una volta.</span><span class="sxs-lookup"><span data-stu-id="6123e-113">A single person using different browsers or machines will be counted as more than one user.</span></span>
* <span data-ttu-id="6123e-114">**Strumento Sessioni**: il numero di sessioni delle attività dell'utente che include determinate pagine e funzionalità dell'app.</span><span class="sxs-lookup"><span data-stu-id="6123e-114">**Sessions tool**: How many sessions of user activity have included certain pages and features of your app.</span></span> <span data-ttu-id="6123e-115">Una sessione viene conteggiata dopo mezz'ora di inattività dell'utente o in seguito a un uso continuo di 24 ore.</span><span class="sxs-lookup"><span data-stu-id="6123e-115">A session is counted after half an hour of user inactivity, or after continuous 24h of use.</span></span>
* <span data-ttu-id="6123e-116">**Strumento Eventi**: la frequenza con cui vengono usate alcune pagine e funzionalità dell'app.</span><span class="sxs-lookup"><span data-stu-id="6123e-116">**Events tool**: How often certain pages and features of your app are used.</span></span> <span data-ttu-id="6123e-117">La visualizzazione di una pagina viene conteggiata quando un browser carica la pagina dell'app, purché sia stata [instrumentata](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="6123e-117">A page view is counted when a browser loads a page from your app, provided you have [instrumented it](app-insights-javascript.md).</span></span> 

    <span data-ttu-id="6123e-118">Un evento personalizzato indica che nell'app si verifica un'operazione, spesso si tratta di un'interazione dell'utente ad esempio il clic su un pulsante o il completamento di alcune attività.</span><span class="sxs-lookup"><span data-stu-id="6123e-118">A custom event represents one occurrence of something happening in your app, often a user interaction like a button click or the completion of some task.</span></span> <span data-ttu-id="6123e-119">Inserire codice nell'app per [generare eventi personalizzati](app-insights-api-custom-events-metrics.md#trackevent).</span><span class="sxs-lookup"><span data-stu-id="6123e-119">You insert code in your app to [generate custom events](app-insights-api-custom-events-metrics.md#trackevent).</span></span>

![Strumento Uso](./media/app-insights-usage-segmentation/users.png)

## <a name="querying-for-certain-users"></a><span data-ttu-id="6123e-121">Esecuzione di query per determinati utenti</span><span class="sxs-lookup"><span data-stu-id="6123e-121">Querying for Certain Users</span></span> 

<span data-ttu-id="6123e-122">Modificando le opzioni di query nella parte superiore dello strumento Utenti, è possibile esaminare diversi gruppi di utenti:</span><span class="sxs-lookup"><span data-stu-id="6123e-122">Explore different groups of users by adjusting the query options at the top of the Users tool:</span></span> 

* <span data-ttu-id="6123e-123">Who used (Usato da): scegliere gli eventi personalizzati e le visualizzazioni di pagina.</span><span class="sxs-lookup"><span data-stu-id="6123e-123">Who used: Choose custom events and page views.</span></span> 
* <span data-ttu-id="6123e-124">Durante: scegliere un intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="6123e-124">During: Choose a time range.</span></span> 
* <span data-ttu-id="6123e-125">By (Da): scegliere la modalità di ordinazione dei dati in base un intervallo di tempo o a un'altra proprietà, ad esempio la città o il browser.</span><span class="sxs-lookup"><span data-stu-id="6123e-125">By: Choose how to bucket the data, either by a period of time or by another property such as browser or city.</span></span> 
* <span data-ttu-id="6123e-126">Split By (Dividi per): scegliere una proprietà in base alla quale dividere o segmentare i dati.</span><span class="sxs-lookup"><span data-stu-id="6123e-126">Split By: Choose a property by which to split or segment the data.</span></span> 
* <span data-ttu-id="6123e-127">Aggiungi filtri: limitare le query a determinati utenti, sessioni o eventi in base alle relative proprietà, ad esempio città o browser.</span><span class="sxs-lookup"><span data-stu-id="6123e-127">Add Filters: Limit the query to certain users, sessions, or events based on their properties, such as browser or city.</span></span> 
 
## <a name="saving-and-sharing-reports"></a><span data-ttu-id="6123e-128">Salvataggio e condivisione di report</span><span class="sxs-lookup"><span data-stu-id="6123e-128">Saving and sharing reports</span></span> 
<span data-ttu-id="6123e-129">È possibile salvare i report Utenti, mantenendoli privati nella sezione My Reports (Report personali) o condividendoli con tutti gli utenti con accesso a questa risorsa di Application Insights nella sezione Report condivisi.</span><span class="sxs-lookup"><span data-stu-id="6123e-129">You can save Users reports, either private just to you in the My Reports section, or shared with everyone else with access to this Application Insights resource in the Shared Reports section.</span></span>  
 
<span data-ttu-id="6123e-130">Durante il salvataggio di un report o la modifica delle proprietà, scegliere "Intervallo di tempo relativo corrente" per salvare un report che continuerà ad aggiornare i dati, per un determinato periodo di tempo stabilito.</span><span class="sxs-lookup"><span data-stu-id="6123e-130">While saving a report or editing its properties, choose "Current Relative Time Range" to save a report will continuously refreshed data, going back some fixed amount of time.</span></span>  
 
<span data-ttu-id="6123e-131">Scegliere "Intervallo di tempo assoluto corrente" per salvare un report con un set di dati fisso.</span><span class="sxs-lookup"><span data-stu-id="6123e-131">Choose "Current Absolute Time Range" to save a report with a fixed set of data.</span></span> <span data-ttu-id="6123e-132">Tenere presente che i dati in Application Insights vengono conservati solo per 90 giorni, pertanto se sono trascorsi più di 90 giorni dal salvataggio di un report con intervallo di tempo assoluto, il report visualizzato sarà vuoto.</span><span class="sxs-lookup"><span data-stu-id="6123e-132">Keep in mind that data in Application Insights is only stored for 90 days, so if more than 90 days have passed since a report with an absolute time range was saved, the report will appear empty.</span></span> 
 
## <a name="example-instances"></a><span data-ttu-id="6123e-133">Istanze di esempio</span><span class="sxs-lookup"><span data-stu-id="6123e-133">Example instances</span></span>

<span data-ttu-id="6123e-134">La sezione Example instances (Istanze di esempio) mostra informazioni relative ad alcuni singoli utenti, sessioni o eventi che corrispondono alla query corrente.</span><span class="sxs-lookup"><span data-stu-id="6123e-134">The Example instances section shows information about a handful of individual users, sessions, or events that are matched by the current query.</span></span> <span data-ttu-id="6123e-135">La valutazione e l'analisi dei comportamenti delle persone, oltre a creare aggregazioni, può offrire informazioni dettagliate sull'uso effettivo dell'app da parte degli utenti.</span><span class="sxs-lookup"><span data-stu-id="6123e-135">Considering and exploring the behaviors of individuals, in addition to aggregates, can provide insights about how people actually use your app.</span></span> 
 
## <a name="insights"></a><span data-ttu-id="6123e-136">Informazioni dettagliate</span><span class="sxs-lookup"><span data-stu-id="6123e-136">Insights</span></span> 

<span data-ttu-id="6123e-137">La barra laterale Informazioni dettagliate mostra cluster di grandi dimensioni di utenti che condividono proprietà comuni.</span><span class="sxs-lookup"><span data-stu-id="6123e-137">The Insights sidebar shows large clusters of users that share common properties.</span></span> <span data-ttu-id="6123e-138">Questi cluster consentono di individuare andamenti sorprendenti sulle modalità di uso dell'app.</span><span class="sxs-lookup"><span data-stu-id="6123e-138">These clusters can uncover surprising trends in how people use your app.</span></span> <span data-ttu-id="6123e-139">Ad esempio, se il 40% dell'uso dell'app deriva da utenti che usano una singola funzione.</span><span class="sxs-lookup"><span data-stu-id="6123e-139">For example, if 40% of all of the usage of your app comes from people using a single feature.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="6123e-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6123e-140">Next steps</span></span>
- <span data-ttu-id="6123e-141">Per abilitare le esperienze di utilizzo, iniziare a inviare [eventi personalizzati](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) o [visualizzazioni pagina](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="6123e-141">To enable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="6123e-142">Se si inviano già eventi personalizzati o visualizzazioni pagina, è possibile esplorare gli strumenti relativi all'uso per scoprire come gli utenti usano il servizio.</span><span class="sxs-lookup"><span data-stu-id="6123e-142">If you already send custom events or page views, explore the Usage tools to learn how users use your service.</span></span>
    - [<span data-ttu-id="6123e-143">Grafici a imbuto</span><span class="sxs-lookup"><span data-stu-id="6123e-143">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="6123e-144">Conservazione</span><span class="sxs-lookup"><span data-stu-id="6123e-144">Retention</span></span>](app-insights-usage-retention.md)
    - [<span data-ttu-id="6123e-145">Flussi degli utenti</span><span class="sxs-lookup"><span data-stu-id="6123e-145">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="6123e-146">Cartelle di lavoro</span><span class="sxs-lookup"><span data-stu-id="6123e-146">Workbooks</span></span>](app-insights-usage-workbooks.md)
    - [<span data-ttu-id="6123e-147">Aggiungere il contesto utente</span><span class="sxs-lookup"><span data-stu-id="6123e-147">Add user context</span></span>](app-insights-usage-send-user-context.md)

