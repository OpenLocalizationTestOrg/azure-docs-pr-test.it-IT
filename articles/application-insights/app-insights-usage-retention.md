---
title: analisi di conservazione aaaUser per le applicazioni web con Azure Application Insights | Documenti Microsoft
description: Il numero di utenti restituiti tooyour app?
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
ms.openlocfilehash: 8bcee5f1611afbd69016ec3eef27832c304762a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="user-retention-analysis-for-web-applications-with-application-insights"></a><span data-ttu-id="78ad2-103">Analisi della conservazione degli utenti per applicazioni Web con Application Insights</span><span class="sxs-lookup"><span data-stu-id="78ad2-103">User retention analysis for web applications with Application Insights</span></span>

<span data-ttu-id="78ad2-104">funzionalità di memorizzazione Hello [Azure Application Insights](app-insights-overview.md) si analizza il numero di utenti consente di restituiscono tooyour app e la frequenza con cui eseguire attività specifiche o a scopi.</span><span class="sxs-lookup"><span data-stu-id="78ad2-104">hello retention feature in [Azure Application Insights](app-insights-overview.md) helps you analyze how many users return tooyour app, and how often they perform particular tasks or achieve goals.</span></span> <span data-ttu-id="78ad2-105">Ad esempio, se si esegue un sito di gioco, è possibile confrontare un numero di utenti che restituiscono toohello sito dopo la perdita di un gioco con numero di hello che restituiscono dopo dominante hello.</span><span class="sxs-lookup"><span data-stu-id="78ad2-105">For example, if you run a game site, you could compare hello numbers of users who return toohello site after losing a game with hello number who return after winning.</span></span> <span data-ttu-id="78ad2-106">Queste informazioni consentono di migliorare sia l'esperienza per l'utente che la strategia aziendale.</span><span class="sxs-lookup"><span data-stu-id="78ad2-106">This knowledge can help you improve both your user experience and your business strategy.</span></span>

## <a name="get-started"></a><span data-ttu-id="78ad2-107">Attività iniziali</span><span class="sxs-lookup"><span data-stu-id="78ad2-107">Get started</span></span>

<span data-ttu-id="78ad2-108">Se non viene visualizzato ancora dati strumento memorizzazione hello nel portale Application Insights hello [informazioni su come tooget iniziare con strumenti di gestione di hello](app-insights-usage-overview.md).</span><span class="sxs-lookup"><span data-stu-id="78ad2-108">If you don't yet see data in hello retention tool in hello Application Insights portal, [learn how tooget started with hello usage tools](app-insights-usage-overview.md).</span></span>

## <a name="hello-retention-tool"></a><span data-ttu-id="78ad2-109">strumento di conservazione Hello</span><span class="sxs-lookup"><span data-stu-id="78ad2-109">hello Retention tool</span></span>

![Strumento Conservazione](./media/app-insights-usage-retention/retention.png)

1. <span data-ttu-id="78ad2-111">barra degli strumenti Hello consente agli utenti i nuovi report conservazione toocreate, aprire i report esistenti di memorizzazione, salvare i report di memorizzazione corrente o Salva con nome, annullare le modifiche apportate toosaved report, aggiornare i dati nel report hello, condivisione di report tramite posta elettronica o un collegamento diretto e hello accesso pagina della documentazione.</span><span class="sxs-lookup"><span data-stu-id="78ad2-111">hello toolbar allows users toocreate new retention reports, open existing retention reports, save current retention report or save as, revert changes made toosaved reports, refresh data on hello report, share report via email or direct link, and access hello documentation page.</span></span> 
2. <span data-ttu-id="78ad2-112">Per impostazione predefinita, il report di conservazione mostra tutti gli utenti che non hanno fatto alcuna operazione, poi sono tornati e non hanno fatto altro per un periodo.</span><span class="sxs-lookup"><span data-stu-id="78ad2-112">By default, retention shows all users who did anything then came back and did anything else over a period.</span></span> <span data-ttu-id="78ad2-113">È possibile selezionare una diversa combinazione di eventi toonarrow hello riguardano le attività dell'utente specifico.</span><span class="sxs-lookup"><span data-stu-id="78ad2-113">You can select different combination of events toonarrow hello focus on specific user activities.</span></span>
3. <span data-ttu-id="78ad2-114">Aggiungere uno o più filtri alle proprietà.</span><span class="sxs-lookup"><span data-stu-id="78ad2-114">Add one or more filters on properties.</span></span> <span data-ttu-id="78ad2-115">Ad esempio, è possibile concentrarsi sugli utenti di un determinato paese o area.</span><span class="sxs-lookup"><span data-stu-id="78ad2-115">For example, you can focus on users in a particular country or region.</span></span> <span data-ttu-id="78ad2-116">Fare clic su **aggiornamento** dopo l'impostazione di filtri hello.</span><span class="sxs-lookup"><span data-stu-id="78ad2-116">Click **Update** after setting hello filters.</span></span> 
4. <span data-ttu-id="78ad2-117">Hello complessivo memorizzazione grafico mostra un riepilogo del mantenimento dei dati utente tra hello periodo di tempo selezionato.</span><span class="sxs-lookup"><span data-stu-id="78ad2-117">hello overall retention chart shows a summary of user retention across hello selected time period.</span></span> 
5. <span data-ttu-id="78ad2-118">griglia Hello Mostra hello numero di utenti di conservazione generatore delle query toohello secondo in #2.</span><span class="sxs-lookup"><span data-stu-id="78ad2-118">hello grid shows hello number of users retained according toohello query builder in #2.</span></span> <span data-ttu-id="78ad2-119">Ogni riga rappresenta una coorte nel programma di utenti che hanno eseguito qualsiasi evento nel tempo hello periodo indicato.</span><span class="sxs-lookup"><span data-stu-id="78ad2-119">Each row represents a cohort of users who performed any event in hello time period shown.</span></span> <span data-ttu-id="78ad2-120">Ogni cella della riga hello viene restituito il numero di tale coorte almeno una volta in un periodo successivo.</span><span class="sxs-lookup"><span data-stu-id="78ad2-120">Each cell in hello row shows how many of that cohort returned at least once in a later period.</span></span> <span data-ttu-id="78ad2-121">Alcuni utenti potrebbero ritornare in periodi diversi.</span><span class="sxs-lookup"><span data-stu-id="78ad2-121">Some users may return in more than one period.</span></span> 
6. <span data-ttu-id="78ad2-122">schede di approfondimenti Hello mostrano i primi cinque eventi di origine e prime cinque restituito utenti toogive eventi una migliore comprensione del loro report di conservazione.</span><span class="sxs-lookup"><span data-stu-id="78ad2-122">hello insights cards show top five initiating events, and top five returned events toogive users a better understanding of their retention report.</span></span> 

![Passaggio del mouse sullo strumento Conservazione](./media/app-insights-usage-retention/hover.png)

<span data-ttu-id="78ad2-124">Gli utenti è possono passare il mouse sulle celle sul pulsante di hello memorizzazione strumento tooaccess hello analitica e descrizioni comandi che spiega quali cella hello significa.</span><span class="sxs-lookup"><span data-stu-id="78ad2-124">Users can hover over cells on hello retention tool tooaccess hello analytics button and tool tips explaining what hello cell means.</span></span> <span data-ttu-id="78ad2-125">pulsante Analitica Hello accetta strumento Analitica toohello di utenti con gli utenti toogenerate una query già popolati dalla cella hello.</span><span class="sxs-lookup"><span data-stu-id="78ad2-125">hello Analytics button takes users toohello Analytics tool with a pre-populated query toogenerate users from hello cell.</span></span> 

## <a name="use-business-events-tootrack-retention"></a><span data-ttu-id="78ad2-126">Utilizzare la memorizzazione dei tootrack gli eventi di business</span><span class="sxs-lookup"><span data-stu-id="78ad2-126">Use business events tootrack retention</span></span>

<span data-ttu-id="78ad2-127">tooget hello utili memorizzazione analysis, gli eventi di misure che rappresentano le attività di business significativo.</span><span class="sxs-lookup"><span data-stu-id="78ad2-127">tooget hello most useful retention analysis, measure events that represent significant business activities.</span></span> 

<span data-ttu-id="78ad2-128">Ad esempio, molti utenti potrebbero aprire una pagina nell'app senza hello gioco che vengono visualizzati.</span><span class="sxs-lookup"><span data-stu-id="78ad2-128">For example, many users might open a page in your app without playing hello game that it displays.</span></span> <span data-ttu-id="78ad2-129">Rilevamento solo visualizzazioni di pagina hello fornisce pertanto una stima imprecisa di quante persone hanno restituito tooplay gioco hello dopo a sfruttare in precedenza.</span><span class="sxs-lookup"><span data-stu-id="78ad2-129">Tracking just hello page views would therefore provide an inaccurate estimate of how many people return tooplay hello game after enjoying it previously.</span></span> <span data-ttu-id="78ad2-130">tooget un quadro preciso di restituzione dei lettori, l'app deve inviare un evento personalizzato quando un utente viene riprodotto.</span><span class="sxs-lookup"><span data-stu-id="78ad2-130">tooget a clear picture of returning players, your app should send a custom event when a user actually plays.</span></span>  

<span data-ttu-id="78ad2-131">È buona norma toocode eventi personalizzati che rappresentano azioni aziendali principali e utilizzano per l'analisi di memorizzazione.</span><span class="sxs-lookup"><span data-stu-id="78ad2-131">It's good practice toocode custom events that represent key business actions, and use these for your retention analysis.</span></span> <span data-ttu-id="78ad2-132">risultato di gioco hello toocapture, è necessario toowrite una riga di codice toosend tooApplication un evento personalizzato Insights.</span><span class="sxs-lookup"><span data-stu-id="78ad2-132">toocapture hello game outcome, you need toowrite a line of code toosend a custom event tooApplication Insights.</span></span> <span data-ttu-id="78ad2-133">Se si scrive il codice della pagina web hello o Node.JS, l'aspetto è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="78ad2-133">If you write it in hello web page code or in Node.JS, it looks like this:</span></span>

```JavaScript
    appinsights.trackEvent("won game");
```

<span data-ttu-id="78ad2-134">O nel codice server di ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="78ad2-134">Or in ASP.NET server code:</span></span>

```C#
   telemetry.TrackEvent("won game");
```

<span data-ttu-id="78ad2-135">[Altre informazioni sulla scrittura di eventi personalizzati](app-insights-api-custom-events-metrics.md#trackevent).</span><span class="sxs-lookup"><span data-stu-id="78ad2-135">[Learn more about writing custom events](app-insights-api-custom-events-metrics.md#trackevent).</span></span>


## <a name="next-steps"></a><span data-ttu-id="78ad2-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="78ad2-136">Next steps</span></span>
- <span data-ttu-id="78ad2-137">utilizzo di tooenable esperienze, avviare l'invio [eventi personalizzati](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) o [visualizzazioni pagina](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="78ad2-137">tooenable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="78ad2-138">Se si invia già hello utilizzo strumenti toolearn di esplorare gli eventi personalizzati o le visualizzazioni di pagina, come gli utenti di usare il servizio.</span><span class="sxs-lookup"><span data-stu-id="78ad2-138">If you already send custom events or page views, explore hello Usage tools toolearn how users use your service.</span></span>
    - [<span data-ttu-id="78ad2-139">Utenti, sessioni ed eventi</span><span class="sxs-lookup"><span data-stu-id="78ad2-139">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
    - [<span data-ttu-id="78ad2-140">Grafici a imbuto</span><span class="sxs-lookup"><span data-stu-id="78ad2-140">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="78ad2-141">Flussi degli utenti</span><span class="sxs-lookup"><span data-stu-id="78ad2-141">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="78ad2-142">Cartelle di lavoro</span><span class="sxs-lookup"><span data-stu-id="78ad2-142">Workbooks</span></span>](app-insights-usage-workbooks.md)
    - [<span data-ttu-id="78ad2-143">Aggiungere il contesto utente</span><span class="sxs-lookup"><span data-stu-id="78ad2-143">Add user context</span></span>](app-insights-usage-send-user-context.md)


