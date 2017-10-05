---
title: Analisi della conservazione degli utenti per applicazioni Web con Azure Application Insights | Microsoft Docs
description: Quanti utenti tornano all'app?
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
ms.openlocfilehash: 7f7ca19ab171278bbd82f68e3822bc650b25373d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="user-retention-analysis-for-web-applications-with-application-insights"></a><span data-ttu-id="c7ca5-103">Analisi della conservazione degli utenti per applicazioni Web con Application Insights</span><span class="sxs-lookup"><span data-stu-id="c7ca5-103">User retention analysis for web applications with Application Insights</span></span>

<span data-ttu-id="c7ca5-104">La funzionalità di conservazione in [Azure Application Insights](app-insights-overview.md) consente di analizzare il numero di utenti che tornano all'app e la frequenza con cui si eseguono attività specifiche o si raggiungono determinati obiettivi.</span><span class="sxs-lookup"><span data-stu-id="c7ca5-104">The retention feature in [Azure Application Insights](app-insights-overview.md) helps you analyze how many users return to your app, and how often they perform particular tasks or achieve goals.</span></span> <span data-ttu-id="c7ca5-105">Ad esempio, se si esegue un sito di giochi, è possibile confrontare il numero di utenti che ritornano sul sito dopo aver perso una partita con il numero di utenti che ritornano dopo averla vinta.</span><span class="sxs-lookup"><span data-stu-id="c7ca5-105">For example, if you run a game site, you could compare the numbers of users who return to the site after losing a game with the number who return after winning.</span></span> <span data-ttu-id="c7ca5-106">Queste informazioni consentono di migliorare sia l'esperienza per l'utente che la strategia aziendale.</span><span class="sxs-lookup"><span data-stu-id="c7ca5-106">This knowledge can help you improve both your user experience and your business strategy.</span></span>

## <a name="get-started"></a><span data-ttu-id="c7ca5-107">Attività iniziali</span><span class="sxs-lookup"><span data-stu-id="c7ca5-107">Get started</span></span>

<span data-ttu-id="c7ca5-108">Se nello strumento Conservazione nel portale di Application Insights non vengono ancora visualizzati i dati, leggere le [informazioni su come iniziare a usare gli strumenti di utilizzo](app-insights-usage-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c7ca5-108">If you don't yet see data in the retention tool in the Application Insights portal, [learn how to get started with the usage tools](app-insights-usage-overview.md).</span></span>

## <a name="the-retention-tool"></a><span data-ttu-id="c7ca5-109">Strumento Conservazione</span><span class="sxs-lookup"><span data-stu-id="c7ca5-109">The Retention tool</span></span>

![Strumento Conservazione](./media/app-insights-usage-retention/retention.png)

1. <span data-ttu-id="c7ca5-111">La barra degli strumenti consente agli utenti di creare nuovi report di conservazione, aprire i report di conservazione esistenti, salvare il report di conservazione corrente o salvarlo con un altro nome, ripristinare le modifiche apportate al report salvati, aggiornare i dati del report, condividere un report tramite posta elettronica o un collegamento diretto e accedere alla pagina della documentazione.</span><span class="sxs-lookup"><span data-stu-id="c7ca5-111">The toolbar allows users to create new retention reports, open existing retention reports, save current retention report or save as, revert changes made to saved reports, refresh data on the report, share report via email or direct link, and access the documentation page.</span></span> 
2. <span data-ttu-id="c7ca5-112">Per impostazione predefinita, il report di conservazione mostra tutti gli utenti che non hanno fatto alcuna operazione, poi sono tornati e non hanno fatto altro per un periodo.</span><span class="sxs-lookup"><span data-stu-id="c7ca5-112">By default, retention shows all users who did anything then came back and did anything else over a period.</span></span> <span data-ttu-id="c7ca5-113">È possibile selezionare una diversa combinazione di eventi per restringere l'ambito ad attività specifiche degli utenti.</span><span class="sxs-lookup"><span data-stu-id="c7ca5-113">You can select different combination of events to narrow the focus on specific user activities.</span></span>
3. <span data-ttu-id="c7ca5-114">Aggiungere uno o più filtri alle proprietà.</span><span class="sxs-lookup"><span data-stu-id="c7ca5-114">Add one or more filters on properties.</span></span> <span data-ttu-id="c7ca5-115">Ad esempio, è possibile concentrarsi sugli utenti di un determinato paese o area.</span><span class="sxs-lookup"><span data-stu-id="c7ca5-115">For example, you can focus on users in a particular country or region.</span></span> <span data-ttu-id="c7ca5-116">Fare clic su **Aggiorna** sopo aver impostato i filtri.</span><span class="sxs-lookup"><span data-stu-id="c7ca5-116">Click **Update** after setting the filters.</span></span> 
4. <span data-ttu-id="c7ca5-117">Il grafico generale della conservazione mostra un riepilogo degli utenti conservati per il periodo di tempo selezionato.</span><span class="sxs-lookup"><span data-stu-id="c7ca5-117">The overall retention chart shows a summary of user retention across the selected time period.</span></span> 
5. <span data-ttu-id="c7ca5-118">Nella griglia viene visualizzato il numero di utenti conservati secondo il generatore di query al numero 2.</span><span class="sxs-lookup"><span data-stu-id="c7ca5-118">The grid shows the number of users retained according to the query builder in #2.</span></span> <span data-ttu-id="c7ca5-119">Ogni riga rappresenta una coorte di utenti che hanno eseguito qualsiasi evento nel periodo di tempo indicato.</span><span class="sxs-lookup"><span data-stu-id="c7ca5-119">Each row represents a cohort of users who performed any event in the time period shown.</span></span> <span data-ttu-id="c7ca5-120">Ogni cella nella riga mostra il numero di utenti della coorte che sono ritornati almeno una volta nel periodo successivo.</span><span class="sxs-lookup"><span data-stu-id="c7ca5-120">Each cell in the row shows how many of that cohort returned at least once in a later period.</span></span> <span data-ttu-id="c7ca5-121">Alcuni utenti potrebbero ritornare in periodi diversi.</span><span class="sxs-lookup"><span data-stu-id="c7ca5-121">Some users may return in more than one period.</span></span> 
6. <span data-ttu-id="c7ca5-122">Le schede dei dettagli mostrano i primi 5 eventi di avvio e i primi 5 eventi restituiti per consentire agli utenti una migliore comprensione del report di conservazione.</span><span class="sxs-lookup"><span data-stu-id="c7ca5-122">The insights cards show top five initiating events, and top five returned events to give users a better understanding of their retention report.</span></span> 

![Passaggio del mouse sullo strumento Conservazione](./media/app-insights-usage-retention/hover.png)

<span data-ttu-id="c7ca5-124">Gli utenti possono passare il mouse sulle celle dello strumento Conservazione per accedere al pulsante di analisi e alle descrizioni dei comandi che spiegano il significato di ogni cella.</span><span class="sxs-lookup"><span data-stu-id="c7ca5-124">Users can hover over cells on the retention tool to access the analytics button and tool tips explaining what the cell means.</span></span> <span data-ttu-id="c7ca5-125">Usando il pulsante di analisi, gli utenti accedono allo strumento di analisi con una query pre-popolata per la generazione di utenti dalla cella.</span><span class="sxs-lookup"><span data-stu-id="c7ca5-125">The Analytics button takes users to the Analytics tool with a pre-populated query to generate users from the cell.</span></span> 

## <a name="use-business-events-to-track-retention"></a><span data-ttu-id="c7ca5-126">Usare gli eventi aziendali per tenere traccia della conservazione</span><span class="sxs-lookup"><span data-stu-id="c7ca5-126">Use business events to track retention</span></span>

<span data-ttu-id="c7ca5-127">Per ottenere un'analisi di conservazione più utile, misurare gli eventi che rappresentano attività aziendali significativi.</span><span class="sxs-lookup"><span data-stu-id="c7ca5-127">To get the most useful retention analysis, measure events that represent significant business activities.</span></span> 

<span data-ttu-id="c7ca5-128">Ad esempio, molti utenti potrebbero aprire una pagina nell'app senza giocare al gioco visualizzato.</span><span class="sxs-lookup"><span data-stu-id="c7ca5-128">For example, many users might open a page in your app without playing the game that it displays.</span></span> <span data-ttu-id="c7ca5-129">Il rilevamento delle sole visualizzazioni di pagina offrirebbe pertanto una stima imprecisa del numero di persone che torna per giocare in seguito al primo accesso.</span><span class="sxs-lookup"><span data-stu-id="c7ca5-129">Tracking just the page views would therefore provide an inaccurate estimate of how many people return to play the game after enjoying it previously.</span></span> <span data-ttu-id="c7ca5-130">Per ottenere un quadro chiaro dei giocatori che ritornano, l'app deve inviare un evento personalizzato quando un utente gioca realmente.</span><span class="sxs-lookup"><span data-stu-id="c7ca5-130">To get a clear picture of returning players, your app should send a custom event when a user actually plays.</span></span>  

<span data-ttu-id="c7ca5-131">È buona norma codificare gli eventi personalizzati che rappresentano la azioni chiave aziendali e usarle per l'analisi di conservazione.</span><span class="sxs-lookup"><span data-stu-id="c7ca5-131">It's good practice to code custom events that represent key business actions, and use these for your retention analysis.</span></span> <span data-ttu-id="c7ca5-132">Per acquisire il risultato di gioco, è necessario scrivere una riga di codice che invii un evento personalizzato ad Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c7ca5-132">To capture the game outcome, you need to write a line of code to send a custom event to Application Insights.</span></span> <span data-ttu-id="c7ca5-133">Se la si scrive nella pagina Web o in Node.js, questa ha un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="c7ca5-133">If you write it in the web page code or in Node.JS, it looks like this:</span></span>

```JavaScript
    appinsights.trackEvent("won game");
```

<span data-ttu-id="c7ca5-134">O nel codice server di ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="c7ca5-134">Or in ASP.NET server code:</span></span>

```C#
   telemetry.TrackEvent("won game");
```

<span data-ttu-id="c7ca5-135">[Altre informazioni sulla scrittura di eventi personalizzati](app-insights-api-custom-events-metrics.md#trackevent).</span><span class="sxs-lookup"><span data-stu-id="c7ca5-135">[Learn more about writing custom events](app-insights-api-custom-events-metrics.md#trackevent).</span></span>


## <a name="next-steps"></a><span data-ttu-id="c7ca5-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c7ca5-136">Next steps</span></span>
- <span data-ttu-id="c7ca5-137">Per abilitare le esperienze di utilizzo, iniziare a inviare [eventi personalizzati](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) o [visualizzazioni pagina](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="c7ca5-137">To enable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="c7ca5-138">Se si inviano già eventi personalizzati o visualizzazioni pagina, è possibile esplorare gli strumenti relativi all'uso per scoprire come gli utenti usano il servizio.</span><span class="sxs-lookup"><span data-stu-id="c7ca5-138">If you already send custom events or page views, explore the Usage tools to learn how users use your service.</span></span>
    - [<span data-ttu-id="c7ca5-139">Utenti, sessioni ed eventi</span><span class="sxs-lookup"><span data-stu-id="c7ca5-139">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
    - [<span data-ttu-id="c7ca5-140">Grafici a imbuto</span><span class="sxs-lookup"><span data-stu-id="c7ca5-140">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="c7ca5-141">Flussi degli utenti</span><span class="sxs-lookup"><span data-stu-id="c7ca5-141">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="c7ca5-142">Cartelle di lavoro</span><span class="sxs-lookup"><span data-stu-id="c7ca5-142">Workbooks</span></span>](app-insights-usage-workbooks.md)
    - [<span data-ttu-id="c7ca5-143">Aggiungere il contesto utente</span><span class="sxs-lookup"><span data-stu-id="c7ca5-143">Add user context</span></span>](app-insights-usage-send-user-context.md)


