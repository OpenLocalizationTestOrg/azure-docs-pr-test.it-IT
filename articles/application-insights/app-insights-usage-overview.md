---
title: Analisi dell'utilizzo per applicazioni Web con Azure Application Insights | Microsoft docs
description: Informazioni sugli utenti e le operazioni eseguite con l'app Web.
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
ms.openlocfilehash: 63b74399790b718e14a5b6e09bc009a336caf928
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="usage-analysis-for-web-applications-with-application-insights"></a><span data-ttu-id="bf765-103">Analisi dell'utilizzo per applicazioni Web con Application Insights</span><span class="sxs-lookup"><span data-stu-id="bf765-103">Usage analysis for web applications with Application Insights</span></span>

<span data-ttu-id="bf765-104">Quali sono le funzionalità dell'app Web più comuni?</span><span class="sxs-lookup"><span data-stu-id="bf765-104">Which features of your web app are most popular?</span></span> <span data-ttu-id="bf765-105">Gli utenti raggiungono i propri obiettivi con l'app?</span><span class="sxs-lookup"><span data-stu-id="bf765-105">Do your users achieve their goals with your app?</span></span> <span data-ttu-id="bf765-106">Escono in particolari punti e riaccedono in un secondo momento?</span><span class="sxs-lookup"><span data-stu-id="bf765-106">Do they drop out at particular points, and do they return later?</span></span>  <span data-ttu-id="bf765-107">[Application Insights di Azure](app-insights-overview.md) consente di ottenere importanti informazioni approfondite sull'uso dell'app Web da parte degli utenti.</span><span class="sxs-lookup"><span data-stu-id="bf765-107">[Azure Application Insights](app-insights-overview.md) helps you gain powerful insights into how people use your web app.</span></span> <span data-ttu-id="bf765-108">Ogni volta che si aggiorna l'app, è possibile valutarne il funzionamento per gli utenti.</span><span class="sxs-lookup"><span data-stu-id="bf765-108">Every time you update your app, you can assess how well it works for users.</span></span> <span data-ttu-id="bf765-109">Con queste informazioni è possibile prendere decisioni in base ai dati sui cicli di sviluppo successivi.</span><span class="sxs-lookup"><span data-stu-id="bf765-109">With this knowledge, you can make data driven decisions about your next development cycles.</span></span>

## <a name="send-telemetry-from-your-app"></a><span data-ttu-id="bf765-110">Inviare dati di telemetria dall'app</span><span class="sxs-lookup"><span data-stu-id="bf765-110">Send telemetry from your app</span></span>

<span data-ttu-id="bf765-111">La migliore esperienza viene ottenuta tramite l'installazione di Application Insights nel codice server dell'app e nelle pagine Web.</span><span class="sxs-lookup"><span data-stu-id="bf765-111">The best experience is obtained by installing Application Insights both in your app server code, and in your web pages.</span></span> <span data-ttu-id="bf765-112">I componenti client e server dell'app inviano dati di telemetria al portale di Azure per l'analisi.</span><span class="sxs-lookup"><span data-stu-id="bf765-112">The client and server components of your app send telemetry back to the Azure portal for analysis.</span></span>

1. <span data-ttu-id="bf765-113">**Codice server:** installare il modulo appropriato per l'app [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md) o per [altre](app-insights-platforms.md) app.</span><span class="sxs-lookup"><span data-stu-id="bf765-113">**Server code:** Install the appropriate module for your [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), or [other](app-insights-platforms.md) app.</span></span>

    * <span data-ttu-id="bf765-114">*Non si vuole installare il codice server? [Creare una risorsa di Azure Application Insights](app-insights-create-new-resource.md).*</span><span class="sxs-lookup"><span data-stu-id="bf765-114">*Don't want to install server code? Just [create an Azure Application Insights resource](app-insights-create-new-resource.md).*</span></span>

2. <span data-ttu-id="bf765-115">**Codice della pagina Web:** aprire il [Portale di Azure](https://portal.azure.com), aprire la risorsa di Application Insights per l'app e quindi aprire **Introduzione > Monitoraggio e diagnosi dell'applicazione lato client**.</span><span class="sxs-lookup"><span data-stu-id="bf765-115">**Web page code:** Open the [Azure portal](https://portal.azure.com), open the Application Insights resource for your app, and then open **Getting Started > Monitor and Diagnose Client-Side**.</span></span> 

    ![Copiare lo script nell'intestazione della pagina master web.](./media/app-insights-usage-overview/02-monitor-web-page.png)


3. <span data-ttu-id="bf765-117">**Ottenere dati di telemetria:** eseguire il progetto in modalità di debug per alcuni minuti e quindi cercare i risultati nel pannello Panoramica in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="bf765-117">**Get telemetry:** Run your project in debug mode for a few minutes, and then look for results in the Overview blade in Application Insights.</span></span>

    <span data-ttu-id="bf765-118">Pubblicare l'app per monitorare le prestazioni dell'app ed esaminare le operazioni eseguite dagli utenti con l'app.</span><span class="sxs-lookup"><span data-stu-id="bf765-118">Publish your app to monitor your app's performance and find out what your users are doing with your app.</span></span>

## <a name="include-user-and-session-id-in-your-telemetry"></a><span data-ttu-id="bf765-119">Includere l'ID di utente e sessione nei dati di telemetria</span><span class="sxs-lookup"><span data-stu-id="bf765-119">Include user and session ID in your telemetry</span></span>
<span data-ttu-id="bf765-120">Per tenere traccia degli utenti nel tempo, Application Insights richiede un modo per identificarli.</span><span class="sxs-lookup"><span data-stu-id="bf765-120">To track users over time, Application Insights requires a way to identify them.</span></span> <span data-ttu-id="bf765-121">Lo strumento Eventi è l'unico strumento relativo all'uso per cui non è richiesto un ID utente o un ID di sessione.</span><span class="sxs-lookup"><span data-stu-id="bf765-121">The Events tool is the only Usage tool that does not require a user ID or a session ID.</span></span>

<span data-ttu-id="bf765-122">Per iniziare a inviare questi ID, vedere [qui](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).</span><span class="sxs-lookup"><span data-stu-id="bf765-122">Start sending these IDs [here](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).</span></span>

## <a name="explore-usage-demographics-and-statistics"></a><span data-ttu-id="bf765-123">Esplorare le statistiche e i dati demografici di uso</span><span class="sxs-lookup"><span data-stu-id="bf765-123">Explore usage demographics and statistics</span></span>
<span data-ttu-id="bf765-124">Scoprire quando le persone usano l'app, a quali pagine sono più interessati, dove si trovano, quali browser e sistemi operativi usano.</span><span class="sxs-lookup"><span data-stu-id="bf765-124">Find out when people use your app, what pages they're most interested in, where your users are located, what browsers and operating systems they use.</span></span> 

<span data-ttu-id="bf765-125">I report sugli utenti e le sessioni filtrano i dati in base alle pagine o agli eventi personalizzati e li segmentano in base a proprietà quali posizione, ambiente e pagina.</span><span class="sxs-lookup"><span data-stu-id="bf765-125">The Users and Sessions reports filter your data by pages or custom events, and segment them by properties such as location, environment, and page.</span></span> <span data-ttu-id="bf765-126">È anche possibile aggiungere filtri personalizzati.</span><span class="sxs-lookup"><span data-stu-id="bf765-126">You can also add your own filters.</span></span>

![Utenti](./media/app-insights-usage-overview/users.png)  

<span data-ttu-id="bf765-128">Informazioni approfondite sui modelli di segnalazione corretti nel set di dati.</span><span class="sxs-lookup"><span data-stu-id="bf765-128">Insights on the right point out interesting patterns in the set of data.</span></span>  

* <span data-ttu-id="bf765-129">Il report sugli **utenti** conta il numero di utenti univoci che accedono alle pagine nei periodi di tempo scelti.</span><span class="sxs-lookup"><span data-stu-id="bf765-129">The **Users** report counts the numbers of unique users that access your pages within your chosen time periods.</span></span> <span data-ttu-id="bf765-130">Gli utenti vengono conteggiati usando i cookie.</span><span class="sxs-lookup"><span data-stu-id="bf765-130">(Users are counted by using cookies.</span></span> <span data-ttu-id="bf765-131">Se un utente accede al sito con browser o computer client diversi o cancella i cookie, verrà conteggiato più volte.</span><span class="sxs-lookup"><span data-stu-id="bf765-131">If someone accesses your site with different browsers or client machines, or clears their cookies, then they will be counted more than once.)</span></span>
* <span data-ttu-id="bf765-132">Il report sulle **sessioni** conteggia il numero di sessioni dell'utente che accedono al sito.</span><span class="sxs-lookup"><span data-stu-id="bf765-132">The **Sessions** report counts the number of user sessions that access your site.</span></span> <span data-ttu-id="bf765-133">Una sessione è un periodo di attività dell'utente, che termina quando si verifica un periodo di inattività di più di mezz'ora.</span><span class="sxs-lookup"><span data-stu-id="bf765-133">A session is a period of activity by a user, terminated by a period of inactivity of more than half an hour.</span></span>

[<span data-ttu-id="bf765-134">Altre informazioni sugli strumenti di Utenti, Sessioni ed Eventi</span><span class="sxs-lookup"><span data-stu-id="bf765-134">More about the Users, Sessions, and Events tools</span></span>](app-insights-usage-segmentation.md)  

## <a name="page-views"></a><span data-ttu-id="bf765-135">Visualizzazioni pagina</span><span class="sxs-lookup"><span data-stu-id="bf765-135">Page views</span></span>

<span data-ttu-id="bf765-136">Nel pannello Uso fare clic nel riquadro Visualizzazioni pagina per ottenere una suddivisione delle pagine più comuni:</span><span class="sxs-lookup"><span data-stu-id="bf765-136">From the Usage blade, click through the Page Views tile to get a breakdown of your most popular pages:</span></span>

![Nel pannello Panoramica fare clic sul grafico Visualizzazioni pagina.](./media/app-insights-usage-overview/05-games.png)

<span data-ttu-id="bf765-138">L'esempio precedente proviene da un sito Web di giochi.</span><span class="sxs-lookup"><span data-stu-id="bf765-138">The example above is from a games web site.</span></span> <span data-ttu-id="bf765-139">Dai grafici, è possibile immediatamente notare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="bf765-139">From the charts, we can instantly see:</span></span>

* <span data-ttu-id="bf765-140">L'utilizzo non è migliorato nell'ultima settimana.</span><span class="sxs-lookup"><span data-stu-id="bf765-140">Usage hasn't improved in the past week.</span></span> <span data-ttu-id="bf765-141">Potrebbe essere utile ottimizzare il motore di ricerca.</span><span class="sxs-lookup"><span data-stu-id="bf765-141">Maybe we should think about search engine optimization?</span></span>
* <span data-ttu-id="bf765-142">La pagina Tennis è la pagina del gioco più popolare.</span><span class="sxs-lookup"><span data-stu-id="bf765-142">Tennis is the most popular game page.</span></span> <span data-ttu-id="bf765-143">È opportuno quindi migliorare questa pagina.</span><span class="sxs-lookup"><span data-stu-id="bf765-143">Let's focus on further improvements to this page.</span></span>
* <span data-ttu-id="bf765-144">In media, gli utenti visitano la pagina Tennis circa tre volte alla settimana.</span><span class="sxs-lookup"><span data-stu-id="bf765-144">On average, users visit the Tennis page about three times per week.</span></span> <span data-ttu-id="bf765-145">Il numero delle sessioni è tre volte superiore al numero di utenti.</span><span class="sxs-lookup"><span data-stu-id="bf765-145">(There are about three times more sessions than users.)</span></span>
* <span data-ttu-id="bf765-146">La maggior parte degli utenti visita il sito durante la settimana lavorativa negli Stati Uniti e nell'orario di lavoro.</span><span class="sxs-lookup"><span data-stu-id="bf765-146">Most users visit the site during the U.S. working week, and in working hours.</span></span> <span data-ttu-id="bf765-147">Si dovrebbe forse aggiungere un pulsante "Nascondi rapidamente" nella pagina Web.</span><span class="sxs-lookup"><span data-stu-id="bf765-147">Perhaps we should provide a "quick hide" button on the web page.</span></span>
* <span data-ttu-id="bf765-148">Le [annotazioni](app-insights-annotations.md) nel grafico indicano quando sono state distribuite le nuove versioni del sito Web.</span><span class="sxs-lookup"><span data-stu-id="bf765-148">The [annotations](app-insights-annotations.md) on the chart show when new versions of the website were deployed.</span></span> <span data-ttu-id="bf765-149">Nessuna delle distribuzioni recenti ha avuto un effetto visibile sull'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="bf765-149">None of the recent deployments had a noticeable effect on usage.</span></span>

<span data-ttu-id="bf765-150">Cosa fare se si desidera analizzare il traffico del sito in modo più dettagliato, ad esempio suddividendolo in base a una proprietà personalizzata, mentre il sito invia i dati di telemetria di visualizzazioni della pagina?</span><span class="sxs-lookup"><span data-stu-id="bf765-150">What if you want to investigate the traffic to your site in more detail, like splitting by a custom property your site sends in its page view telemetry?</span></span>

1. <span data-ttu-id="bf765-151">Nel menu delle risorse di Application Insights aprire lo strumento **Eventi**.</span><span class="sxs-lookup"><span data-stu-id="bf765-151">Open the **Events** tool in the Application Insights resource menu.</span></span> <span data-ttu-id="bf765-152">Questo strumento consente di analizzare il numero di visualizzazioni della pagina ed eventi personalizzati inviati dall'app, in base a diverse opzioni di filtro, coorte e segmentazione.</span><span class="sxs-lookup"><span data-stu-id="bf765-152">This tool lets you analyze how many page views and custom events were sent from your app, based on a variety of filtering, cohorting, and segmentation options.</span></span>
2. <span data-ttu-id="bf765-153">Nell'elenco a discesa "Who used" (Usato da) selezionare "Any Page View" (Qualsiasi visualizzazione di pagina).</span><span class="sxs-lookup"><span data-stu-id="bf765-153">In the "Who used" dropdown, select "Any Page View".</span></span>
3. <span data-ttu-id="bf765-154">Nell'elenco a discesa "Split by" (Dividi per) selezionare una proprietà in base alla quale dividere i dati di telemetria di visualizzazione della pagina.</span><span class="sxs-lookup"><span data-stu-id="bf765-154">In the "Split by" dropdown, select a property by which to split your page view telemetry.</span></span>

## <a name="retention---how-many-users-come-back"></a><span data-ttu-id="bf765-155">Conservazione: numero di utenti che ritornano</span><span class="sxs-lookup"><span data-stu-id="bf765-155">Retention - how many users come back?</span></span>

<span data-ttu-id="bf765-156">La conservazione consente di comprendere la frequenza con cui gli utenti tornano a usare l'app, in base alle coorti di utenti che hanno eseguito un'azione aziendale in un determinato intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="bf765-156">Retention helps you understand how often your users return to use their app, based on cohorts of users that performed some business action during a certain time bucket.</span></span> 

- <span data-ttu-id="bf765-157">Comprendere le funzionalità specifiche per cui alcuni utenti ritornano di più rispetto ad altri</span><span class="sxs-lookup"><span data-stu-id="bf765-157">Understand what specific features cause users to come back more than others</span></span> 
- <span data-ttu-id="bf765-158">Fare ipotesi in base a dati utente reali</span><span class="sxs-lookup"><span data-stu-id="bf765-158">Form hypotheses based on real user data</span></span> 
- <span data-ttu-id="bf765-159">Determinare se la conservazione è un problema per il prodotto</span><span class="sxs-lookup"><span data-stu-id="bf765-159">Determine whether retention is a problem in your product</span></span> 

![Conservazione](./media/app-insights-usage-overview/retention.png) 

<span data-ttu-id="bf765-161">I controlli di conservazione nella parte superiore consentono di definire l'intervallo di tempo e gli eventi specifici per il calcolo della conservazione.</span><span class="sxs-lookup"><span data-stu-id="bf765-161">The retention controls on top allow you to define specific events and time range to calculate retention.</span></span> <span data-ttu-id="bf765-162">Il grafico nella parte centrale offre una rappresentazione visiva della percentuale della conservazione generale in base all'intervallo di tempo specificato.</span><span class="sxs-lookup"><span data-stu-id="bf765-162">The graph in the middle gives a visual representation of the overall retention percentage by the time range specified.</span></span> <span data-ttu-id="bf765-163">Il grafico nella parte inferiore rappresenta la singola conservazione in un determinato periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="bf765-163">The graph on the bottom represents individual retention in a given time period.</span></span> <span data-ttu-id="bf765-164">Questo livello di dettagli consente di capire le operazioni eseguite dagli utenti e le possibili motivazioni per cui un utente sceglie di ritornare con una granularità più dettagliata.</span><span class="sxs-lookup"><span data-stu-id="bf765-164">This level of detail allows you to understand what your users are doing and what might affect returning users on a more detailed granularity.</span></span>  

[<span data-ttu-id="bf765-165">Altre informazioni sullo strumento di conservazione</span><span class="sxs-lookup"><span data-stu-id="bf765-165">More about the Retention tool</span></span>](app-insights-usage-retention.md)

## <a name="custom-business-events"></a><span data-ttu-id="bf765-166">Eventi aziendali personalizzati</span><span class="sxs-lookup"><span data-stu-id="bf765-166">Custom business events</span></span>

<span data-ttu-id="bf765-167">Per ottenere una descrizione chiara delle operazioni che gli utenti eseguono con l'app Web, è utile inserire righe di codice per registrare eventi personalizzati.</span><span class="sxs-lookup"><span data-stu-id="bf765-167">To get a clear understanding of what users do with your web app, it's useful to insert lines of code to log custom events.</span></span> <span data-ttu-id="bf765-168">Questi eventi possono tenere traccia di qualsiasi operazione, da azioni dell'utente dettagliate, ad esempio fare clic su pulsanti specifici, agli eventi aziendali più importanti, ad esempio effettuare un acquisto o vincere a un gioco.</span><span class="sxs-lookup"><span data-stu-id="bf765-168">These events can track anything from detailed user actions such as clicking specific buttons, to more significant business events such as making a purchase or winning a game.</span></span> 

<span data-ttu-id="bf765-169">Sebbene in alcuni casi, le visualizzazioni della pagina possano rappresentare eventi utili, questo non è vero in generale.</span><span class="sxs-lookup"><span data-stu-id="bf765-169">Although in some cases, page views can represent useful events, it isn't true in general.</span></span> <span data-ttu-id="bf765-170">Un utente può aprire la pagina di un prodotto senza acquistarlo.</span><span class="sxs-lookup"><span data-stu-id="bf765-170">A user can open a product page without buying the product.</span></span> 

<span data-ttu-id="bf765-171">Con eventi aziendali specifici, è possibile rappresentare in un grafico lo stato di avanzamento degli utenti all'interno del sito.</span><span class="sxs-lookup"><span data-stu-id="bf765-171">With specific business events, you can chart your users' progress through your site.</span></span> <span data-ttu-id="bf765-172">È possibile scoprirne le preferenze per le diverse opzioni e i punti in cui abbandonano il sito o hanno difficoltà.</span><span class="sxs-lookup"><span data-stu-id="bf765-172">You can find out their preferences for different options, and where they drop out or have difficulties.</span></span> <span data-ttu-id="bf765-173">Con queste informazioni si possano prendere decisioni consapevoli sulle priorità nel backlog di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="bf765-173">With this knowledge, you can make informed decisions about the priorities in your development backlog.</span></span>

<span data-ttu-id="bf765-174">Gli eventi possono essere registrati nella pagina Web:</span><span class="sxs-lookup"><span data-stu-id="bf765-174">Events can be logged in the web page:</span></span>

```JavaScript

    appInsights.trackEvent("ExpandDetailTab", {DetailTab: tabName});
```

<span data-ttu-id="bf765-175">O sul lato server dell'app Web:</span><span class="sxs-lookup"><span data-stu-id="bf765-175">Or in the server side of the web app:</span></span>

```C#
    var tc = new Microsoft.ApplicationInsights.TelemetryClient();
    tc.TrackEvent("CreatedAccount", new Dictionary<string,string> {"AccountType":account.Type}, null);
    ...
    tc.TrackEvent("AddedItemToCart", new Dictionary<string,string> {"Item":item.Name}, null);
    ...
    tc.TrackEvent("CompletedPurchase");
```

<span data-ttu-id="bf765-176">È possibile collegare i valori delle proprietà a questi eventi, in modo da poter filtrare o suddividere gli eventi quando li si ispeziona nel portale.</span><span class="sxs-lookup"><span data-stu-id="bf765-176">You can attach property values to these events, so that you can filter or split the events when you inspect them in the portal.</span></span> <span data-ttu-id="bf765-177">A ogni evento viene anche associato un set standard di proprietà, ad esempio un'ID utente anonimo, che consente di analizzare la sequenza delle attività di un singolo utente.</span><span class="sxs-lookup"><span data-stu-id="bf765-177">In addition, a standard set of properties is attached to each event, such as anonymous user ID, which allows you to trace the sequence of activities of an individual user.</span></span>

<span data-ttu-id="bf765-178">Altre informazioni sugli [eventi personalizzati](app-insights-api-custom-events-metrics.md#trackevent) e le [proprietà](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="bf765-178">Learn more about [custom events](app-insights-api-custom-events-metrics.md#trackevent) and [properties](app-insights-api-custom-events-metrics.md#properties).</span></span>

### <a name="slice-and-dice-events"></a><span data-ttu-id="bf765-179">Analisi approfondita degli eventi</span><span class="sxs-lookup"><span data-stu-id="bf765-179">Slice and dice events</span></span>

<span data-ttu-id="bf765-180">Negli strumenti Utenti, Sessioni ed Eventi, è possibile eseguire un'analisi approfondita degli eventi personalizzati per utente, nome dell'evento e proprietà.</span><span class="sxs-lookup"><span data-stu-id="bf765-180">In the Users, Sessions, and Events tools, you can slice and dice custom events by user, event name, and properties.</span></span>
<span data-ttu-id="bf765-181">![Utenti](./media/app-insights-usage-overview/users.png)</span><span class="sxs-lookup"><span data-stu-id="bf765-181">![Users](./media/app-insights-usage-overview/users.png)</span></span>  
  
## <a name="design-the-telemetry-with-the-app"></a><span data-ttu-id="bf765-182">Progettare i dati di telemetria con l'app</span><span class="sxs-lookup"><span data-stu-id="bf765-182">Design the telemetry with the app</span></span>

<span data-ttu-id="bf765-183">Quando si progettano le funzionalità dell'app, prendere in considerazione le modalità in cui si desidera misurarne il successo con gli utenti.</span><span class="sxs-lookup"><span data-stu-id="bf765-183">When you are designing each feature of your app, consider how you are going to measure its success with your users.</span></span> <span data-ttu-id="bf765-184">Decidere quali eventi aziendali è necessario registrare e codificare il monitoraggio delle chiamate per questi eventi nell'app sin dall'inizio.</span><span class="sxs-lookup"><span data-stu-id="bf765-184">Decide what business events you need to record, and code the tracking calls for those events into your app from the start.</span></span>

## <a name="a--b-testing"></a><span data-ttu-id="bf765-185">Test A | B</span><span class="sxs-lookup"><span data-stu-id="bf765-185">A | B Testing</span></span>
<span data-ttu-id="bf765-186">Se non si sa quale variante di una funzionalità sarà più efficace, rilasciarle entrambe, rendendo ognuna accessibile a utenti diversi.</span><span class="sxs-lookup"><span data-stu-id="bf765-186">If you don't know which variant of a feature will be more successful, release both of them, making each accessible to different users.</span></span> <span data-ttu-id="bf765-187">Valutare la riuscita di ognuna e quindi passare a una versione unificata.</span><span class="sxs-lookup"><span data-stu-id="bf765-187">Measure the success of each, and then move to a unified version.</span></span>

<span data-ttu-id="bf765-188">Per questa tecnica è possibile collegare valori per le proprietà differenti per tutti i dati di telemetria inviati da ogni versione dell'app.</span><span class="sxs-lookup"><span data-stu-id="bf765-188">For this technique, you attach distinct property values to all the telemetry that is sent by each version of your app.</span></span> <span data-ttu-id="bf765-189">A questo scopo, definire le proprietà nel TelemetryContext attivo.</span><span class="sxs-lookup"><span data-stu-id="bf765-189">You can do that by defining properties in the active TelemetryContext.</span></span> <span data-ttu-id="bf765-190">Queste proprietà predefinite vengono aggiunte a ogni messaggio di telemetria inviato dall'applicazione, non solo ai messaggi personalizzati, ma anche ai dati di telemetria standard.</span><span class="sxs-lookup"><span data-stu-id="bf765-190">These default properties are added to every telemetry message that the application sends - not just your custom messages, but the standard telemetry as well.</span></span>

<span data-ttu-id="bf765-191">Nel portale Application Insights è possibile filtrare e dividere i dati sui valori delle proprietà, in modo da confrontare versioni diverse.</span><span class="sxs-lookup"><span data-stu-id="bf765-191">In the Application Insights portal, filter and split your data on the property values, so as to compare the different versions.</span></span>

<span data-ttu-id="bf765-192">A tale scopo, [configurare un inizializzatore di telemetria](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):</span><span class="sxs-lookup"><span data-stu-id="bf765-192">To do this, [set up a telemetry initializer](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):</span></span>

```C#


    // Telemetry initializer class
    public class MyTelemetryInitializer : ITelemetryInitializer
    {
        public void Initialize (ITelemetry telemetry)
        {
            telemetry.Properties["AppVersion"] = "v2.1";
        }
    }
```

<span data-ttu-id="bf765-193">Nell'inizializzatore dell'app Web, ad esempio Global.asax.cs:</span><span class="sxs-lookup"><span data-stu-id="bf765-193">In the web app initializer such as Global.asax.cs:</span></span>

```C#

    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```

<span data-ttu-id="bf765-194">Tutti i nuovi TelemetryClients aggiungono automaticamente il valore di proprietà specificato.</span><span class="sxs-lookup"><span data-stu-id="bf765-194">All new TelemetryClients automatically add the property value you specify.</span></span> <span data-ttu-id="bf765-195">I singoli eventi di telemetria possono eseguire la sostituzione dei valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="bf765-195">Individual telemetry events can override the default values.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bf765-196">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bf765-196">Next steps</span></span>
   - [<span data-ttu-id="bf765-197">Utenti, sessioni ed eventi</span><span class="sxs-lookup"><span data-stu-id="bf765-197">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
   - [<span data-ttu-id="bf765-198">Grafici a imbuto</span><span class="sxs-lookup"><span data-stu-id="bf765-198">Funnels</span></span>](usage-funnels.md)
   - [<span data-ttu-id="bf765-199">Conservazione</span><span class="sxs-lookup"><span data-stu-id="bf765-199">Retention</span></span>](app-insights-usage-retention.md)
   - [<span data-ttu-id="bf765-200">Flussi degli utenti</span><span class="sxs-lookup"><span data-stu-id="bf765-200">User Flows</span></span>](app-insights-usage-flows.md)
   - [<span data-ttu-id="bf765-201">Cartelle di lavoro</span><span class="sxs-lookup"><span data-stu-id="bf765-201">Workbooks</span></span>](app-insights-usage-workbooks.md)
   - [<span data-ttu-id="bf765-202">Aggiungere il contesto utente</span><span class="sxs-lookup"><span data-stu-id="bf765-202">Add user context</span></span>](app-insights-usage-send-user-context.md)
