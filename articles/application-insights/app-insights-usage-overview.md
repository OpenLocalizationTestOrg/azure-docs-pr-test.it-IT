---
title: analisi aaaUsage per le applicazioni web con Azure Application Insights | Documenti Microsoft
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
ms.openlocfilehash: f7f9173cf411fa0d2dfb3b5ba99134a02bbc0e89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="usage-analysis-for-web-applications-with-application-insights"></a><span data-ttu-id="29ac6-103">Analisi dell'utilizzo per applicazioni Web con Application Insights</span><span class="sxs-lookup"><span data-stu-id="29ac6-103">Usage analysis for web applications with Application Insights</span></span>

<span data-ttu-id="29ac6-104">Quali sono le funzionalità dell'app Web più comuni?</span><span class="sxs-lookup"><span data-stu-id="29ac6-104">Which features of your web app are most popular?</span></span> <span data-ttu-id="29ac6-105">Gli utenti raggiungono i propri obiettivi con l'app?</span><span class="sxs-lookup"><span data-stu-id="29ac6-105">Do your users achieve their goals with your app?</span></span> <span data-ttu-id="29ac6-106">Escono in particolari punti e riaccedono in un secondo momento?</span><span class="sxs-lookup"><span data-stu-id="29ac6-106">Do they drop out at particular points, and do they return later?</span></span>  <span data-ttu-id="29ac6-107">[Application Insights di Azure](app-insights-overview.md) consente di ottenere importanti informazioni approfondite sull'uso dell'app Web da parte degli utenti.</span><span class="sxs-lookup"><span data-stu-id="29ac6-107">[Azure Application Insights](app-insights-overview.md) helps you gain powerful insights into how people use your web app.</span></span> <span data-ttu-id="29ac6-108">Ogni volta che si aggiorna l'app, è possibile valutarne il funzionamento per gli utenti.</span><span class="sxs-lookup"><span data-stu-id="29ac6-108">Every time you update your app, you can assess how well it works for users.</span></span> <span data-ttu-id="29ac6-109">Con queste informazioni è possibile prendere decisioni in base ai dati sui cicli di sviluppo successivi.</span><span class="sxs-lookup"><span data-stu-id="29ac6-109">With this knowledge, you can make data driven decisions about your next development cycles.</span></span>

## <a name="send-telemetry-from-your-app"></a><span data-ttu-id="29ac6-110">Inviare dati di telemetria dall'app</span><span class="sxs-lookup"><span data-stu-id="29ac6-110">Send telemetry from your app</span></span>

<span data-ttu-id="29ac6-111">migliore esperienza Hello viene ottenuta mediante l'installazione di Application Insights nel codice server dell'app e nelle pagine web.</span><span class="sxs-lookup"><span data-stu-id="29ac6-111">hello best experience is obtained by installing Application Insights both in your app server code, and in your web pages.</span></span> <span data-ttu-id="29ac6-112">componenti client e server di Hello dell'app inviano toohello indietro telemetria portale di Azure per l'analisi.</span><span class="sxs-lookup"><span data-stu-id="29ac6-112">hello client and server components of your app send telemetry back toohello Azure portal for analysis.</span></span>

1. <span data-ttu-id="29ac6-113">**Il codice lato server:** modulo appropriato hello di installazione per il [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), o [altri](app-insights-platforms.md) app.</span><span class="sxs-lookup"><span data-stu-id="29ac6-113">**Server code:** Install hello appropriate module for your [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), or [other](app-insights-platforms.md) app.</span></span>

    * <span data-ttu-id="29ac6-114">*Evitare di dover codice server tooinstall? [Creare una risorsa di Azure Application Insights](app-insights-create-new-resource.md).*</span><span class="sxs-lookup"><span data-stu-id="29ac6-114">*Don't want tooinstall server code? Just [create an Azure Application Insights resource](app-insights-create-new-resource.md).*</span></span>

2. <span data-ttu-id="29ac6-115">**Codice della pagina Web:** hello aprire [portale di Azure](https://portal.azure.com), aprire la risorsa di Application Insights hello per l'app e quindi aprire **introduzione > monitoraggio e diagnosi lato Client**.</span><span class="sxs-lookup"><span data-stu-id="29ac6-115">**Web page code:** Open hello [Azure portal](https://portal.azure.com), open hello Application Insights resource for your app, and then open **Getting Started > Monitor and Diagnose Client-Side**.</span></span> 

    ![Copiare script hello in head hello della pagina master web.](./media/app-insights-usage-overview/02-monitor-web-page.png)


3. <span data-ttu-id="29ac6-117">**Ottenere dati di telemetria:** eseguire il progetto in modalità di debug per alcuni minuti e quindi cercare i risultati nel pannello della panoramica hello in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="29ac6-117">**Get telemetry:** Run your project in debug mode for a few minutes, and then look for results in hello Overview blade in Application Insights.</span></span>

    <span data-ttu-id="29ac6-118">Pubblicare l'app toomonitor le prestazioni dell'app e scoprire operazioni con l'app agli utenti.</span><span class="sxs-lookup"><span data-stu-id="29ac6-118">Publish your app toomonitor your app's performance and find out what your users are doing with your app.</span></span>

## <a name="include-user-and-session-id-in-your-telemetry"></a><span data-ttu-id="29ac6-119">Includere l'ID di utente e sessione nei dati di telemetria</span><span class="sxs-lookup"><span data-stu-id="29ac6-119">Include user and session ID in your telemetry</span></span>
<span data-ttu-id="29ac6-120">tootrack gli utenti nel tempo, Application Insights è necessario un modo tooidentify li.</span><span class="sxs-lookup"><span data-stu-id="29ac6-120">tootrack users over time, Application Insights requires a way tooidentify them.</span></span> <span data-ttu-id="29ac6-121">gli eventi di Hello strumento hello solo strumento in uso non richiede un ID utente o un ID sessione.</span><span class="sxs-lookup"><span data-stu-id="29ac6-121">hello Events tool is hello only Usage tool that does not require a user ID or a session ID.</span></span>

<span data-ttu-id="29ac6-122">Per iniziare a inviare questi ID, vedere [qui](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).</span><span class="sxs-lookup"><span data-stu-id="29ac6-122">Start sending these IDs [here](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).</span></span>

## <a name="explore-usage-demographics-and-statistics"></a><span data-ttu-id="29ac6-123">Esplorare le statistiche e i dati demografici di uso</span><span class="sxs-lookup"><span data-stu-id="29ac6-123">Explore usage demographics and statistics</span></span>
<span data-ttu-id="29ac6-124">Scoprire quando le persone usano l'app, a quali pagine sono più interessati, dove si trovano, quali browser e sistemi operativi usano.</span><span class="sxs-lookup"><span data-stu-id="29ac6-124">Find out when people use your app, what pages they're most interested in, where your users are located, what browsers and operating systems they use.</span></span> 

<span data-ttu-id="29ac6-125">report di utenti e sessioni Hello filtrare i dati nelle pagine o eventi personalizzati e li segmento da proprietà quali posizione, l'ambiente e pagina.</span><span class="sxs-lookup"><span data-stu-id="29ac6-125">hello Users and Sessions reports filter your data by pages or custom events, and segment them by properties such as location, environment, and page.</span></span> <span data-ttu-id="29ac6-126">È anche possibile aggiungere filtri personalizzati.</span><span class="sxs-lookup"><span data-stu-id="29ac6-126">You can also add your own filters.</span></span>

![Utenti](./media/app-insights-usage-overview/users.png)  

<span data-ttu-id="29ac6-128">Informazioni dettagliate sui hello destro specificare schemi interessanti nei set di hello di dati.</span><span class="sxs-lookup"><span data-stu-id="29ac6-128">Insights on hello right point out interesting patterns in hello set of data.</span></span>  

* <span data-ttu-id="29ac6-129">Hello **utenti** report conta il numero di hello di utenti univoci che accedere alle pagine durante i periodi di tempo scelto.</span><span class="sxs-lookup"><span data-stu-id="29ac6-129">hello **Users** report counts hello numbers of unique users that access your pages within your chosen time periods.</span></span> <span data-ttu-id="29ac6-130">Gli utenti vengono conteggiati usando i cookie.</span><span class="sxs-lookup"><span data-stu-id="29ac6-130">(Users are counted by using cookies.</span></span> <span data-ttu-id="29ac6-131">Se un utente accede al sito con browser o computer client diversi o cancella i cookie, verrà conteggiato più volte.</span><span class="sxs-lookup"><span data-stu-id="29ac6-131">If someone accesses your site with different browsers or client machines, or clears their cookies, then they will be counted more than once.)</span></span>
* <span data-ttu-id="29ac6-132">Hello **sessioni** report conta il numero di hello delle sessioni che accedono al sito.</span><span class="sxs-lookup"><span data-stu-id="29ac6-132">hello **Sessions** report counts hello number of user sessions that access your site.</span></span> <span data-ttu-id="29ac6-133">Una sessione è un periodo di attività dell'utente, che termina quando si verifica un periodo di inattività di più di mezz'ora.</span><span class="sxs-lookup"><span data-stu-id="29ac6-133">A session is a period of activity by a user, terminated by a period of inactivity of more than half an hour.</span></span>

[<span data-ttu-id="29ac6-134">Informazioni sugli strumenti di utenti, sessioni e gli eventi di hello</span><span class="sxs-lookup"><span data-stu-id="29ac6-134">More about hello Users, Sessions, and Events tools</span></span>](app-insights-usage-segmentation.md)  

## <a name="page-views"></a><span data-ttu-id="29ac6-135">Visualizzazioni pagina</span><span class="sxs-lookup"><span data-stu-id="29ac6-135">Page views</span></span>

<span data-ttu-id="29ac6-136">Dal Pannello di utilizzo di hello, fare clic sulle hello visualizzazioni pagina riquadro tooget una suddivisione delle pagine più diffusi:</span><span class="sxs-lookup"><span data-stu-id="29ac6-136">From hello Usage blade, click through hello Page Views tile tooget a breakdown of your most popular pages:</span></span>

![Dal pannello della panoramica hello, fare clic su hello grafico visualizzazioni pagina](./media/app-insights-usage-overview/05-games.png)

<span data-ttu-id="29ac6-138">esempio Hello sopra si trova in un sito web di giochi.</span><span class="sxs-lookup"><span data-stu-id="29ac6-138">hello example above is from a games web site.</span></span> <span data-ttu-id="29ac6-139">Da grafici hello, è possibile vedere immediatamente:</span><span class="sxs-lookup"><span data-stu-id="29ac6-139">From hello charts, we can instantly see:</span></span>

* <span data-ttu-id="29ac6-140">Utilizzo non è stata migliorata in hello settimana precedente.</span><span class="sxs-lookup"><span data-stu-id="29ac6-140">Usage hasn't improved in hello past week.</span></span> <span data-ttu-id="29ac6-141">Potrebbe essere utile ottimizzare il motore di ricerca.</span><span class="sxs-lookup"><span data-stu-id="29ac6-141">Maybe we should think about search engine optimization?</span></span>
* <span data-ttu-id="29ac6-142">Tennis è la pagina di gioco più diffuso di hello.</span><span class="sxs-lookup"><span data-stu-id="29ac6-142">Tennis is hello most popular game page.</span></span> <span data-ttu-id="29ac6-143">Concentriamoci pagina ulteriori miglioramenti toothis.</span><span class="sxs-lookup"><span data-stu-id="29ac6-143">Let's focus on further improvements toothis page.</span></span>
* <span data-ttu-id="29ac6-144">In Media, gli utenti visitano pagina Tennis hello circa tre volte per ogni settimana.</span><span class="sxs-lookup"><span data-stu-id="29ac6-144">On average, users visit hello Tennis page about three times per week.</span></span> <span data-ttu-id="29ac6-145">Il numero delle sessioni è tre volte superiore al numero di utenti.</span><span class="sxs-lookup"><span data-stu-id="29ac6-145">(There are about three times more sessions than users.)</span></span>
* <span data-ttu-id="29ac6-146">La maggior parte degli utenti sito hello durante la settimana lavorativa di hello Stati Uniti e in orario di lavoro.</span><span class="sxs-lookup"><span data-stu-id="29ac6-146">Most users visit hello site during hello U.S. working week, and in working hours.</span></span> <span data-ttu-id="29ac6-147">Forse dovremmo offriamo un pulsante "Nascondi rapido" nella pagina web hello.</span><span class="sxs-lookup"><span data-stu-id="29ac6-147">Perhaps we should provide a "quick hide" button on hello web page.</span></span>
* <span data-ttu-id="29ac6-148">Hello [annotazioni](app-insights-annotations.md) sul grafico hello vengono visualizzati quando le nuove versioni del sito Web di hello distribuite.</span><span class="sxs-lookup"><span data-stu-id="29ac6-148">hello [annotations](app-insights-annotations.md) on hello chart show when new versions of hello website were deployed.</span></span> <span data-ttu-id="29ac6-149">Nessuna delle distribuzioni recenti hello aveva un impatto negativo sulle utilizzo.</span><span class="sxs-lookup"><span data-stu-id="29ac6-149">None of hello recent deployments had a noticeable effect on usage.</span></span>

<span data-ttu-id="29ac6-150">Cosa accade se si desidera tooinvestigate sito tooyour il traffico di hello in modo più dettagliato, ad esempio suddivisione di una proprietà personalizzata che del sito invia nei relativi dati di telemetria di visualizzazione pagina?</span><span class="sxs-lookup"><span data-stu-id="29ac6-150">What if you want tooinvestigate hello traffic tooyour site in more detail, like splitting by a custom property your site sends in its page view telemetry?</span></span>

1. <span data-ttu-id="29ac6-151">Aprire hello **eventi** strumento nel menu di risorsa di Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="29ac6-151">Open hello **Events** tool in hello Application Insights resource menu.</span></span> <span data-ttu-id="29ac6-152">Questo strumento consente di analizzare il numero di visualizzazioni della pagina ed eventi personalizzati inviati dall'app, in base a diverse opzioni di filtro, coorte e segmentazione.</span><span class="sxs-lookup"><span data-stu-id="29ac6-152">This tool lets you analyze how many page views and custom events were sent from your app, based on a variety of filtering, cohorting, and segmentation options.</span></span>
2. <span data-ttu-id="29ac6-153">Nell'elenco a discesa delle "Chi ha utilizzato" hello, selezionare "Qualsiasi visualizzazione pagina".</span><span class="sxs-lookup"><span data-stu-id="29ac6-153">In hello "Who used" dropdown, select "Any Page View".</span></span>
3. <span data-ttu-id="29ac6-154">Nell'elenco a discesa "Divisione" hello, selezionare una proprietà da cui toosplit pagina consente di visualizzare dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="29ac6-154">In hello "Split by" dropdown, select a property by which toosplit your page view telemetry.</span></span>

## <a name="retention---how-many-users-come-back"></a><span data-ttu-id="29ac6-155">Conservazione: numero di utenti che ritornano</span><span class="sxs-lookup"><span data-stu-id="29ac6-155">Retention - how many users come back?</span></span>

<span data-ttu-id="29ac6-156">Conservazione consente di comprendere la frequenza con cui gli utenti restituiscono toouse la propria applicazione, in base a coorti di utenti di eseguire un'azione di business durante un determinato intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="29ac6-156">Retention helps you understand how often your users return toouse their app, based on cohorts of users that performed some business action during a certain time bucket.</span></span> 

- <span data-ttu-id="29ac6-157">Comprendere quali funzionalità specifiche causare la back toocome più rispetto ad altri utenti</span><span class="sxs-lookup"><span data-stu-id="29ac6-157">Understand what specific features cause users toocome back more than others</span></span> 
- <span data-ttu-id="29ac6-158">Fare ipotesi in base a dati utente reali</span><span class="sxs-lookup"><span data-stu-id="29ac6-158">Form hypotheses based on real user data</span></span> 
- <span data-ttu-id="29ac6-159">Determinare se la conservazione è un problema per il prodotto</span><span class="sxs-lookup"><span data-stu-id="29ac6-159">Determine whether retention is a problem in your product</span></span> 

![Conservazione](./media/app-insights-usage-overview/retention.png) 

<span data-ttu-id="29ac6-161">i controlli di conservazione Hello nella parte superiore consentono si toodefine eventi specifici e conservazione toocalculate intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="29ac6-161">hello retention controls on top allow you toodefine specific events and time range toocalculate retention.</span></span> <span data-ttu-id="29ac6-162">grafico centro hello Hello fornisce una rappresentazione visiva di hello percentuale complessiva di conservazione per hello intervallo di tempo specificato.</span><span class="sxs-lookup"><span data-stu-id="29ac6-162">hello graph in hello middle gives a visual representation of hello overall retention percentage by hello time range specified.</span></span> <span data-ttu-id="29ac6-163">grafico Hello nella parte inferiore di hello rappresenta memorizzazione singola in un determinato periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="29ac6-163">hello graph on hello bottom represents individual retention in a given time period.</span></span> <span data-ttu-id="29ac6-164">Questo livello di dettaglio consente toounderstand quali gli utenti eseguono e cosa possono influire degli utenti in una granularità più dettagliata.</span><span class="sxs-lookup"><span data-stu-id="29ac6-164">This level of detail allows you toounderstand what your users are doing and what might affect returning users on a more detailed granularity.</span></span>  

[<span data-ttu-id="29ac6-165">Informazioni sullo strumento di conservazione hello</span><span class="sxs-lookup"><span data-stu-id="29ac6-165">More about hello Retention tool</span></span>](app-insights-usage-retention.md)

## <a name="custom-business-events"></a><span data-ttu-id="29ac6-166">Eventi aziendali personalizzati</span><span class="sxs-lookup"><span data-stu-id="29ac6-166">Custom business events</span></span>

<span data-ttu-id="29ac6-167">tooget una chiara comprensione di ciò che gli utenti di eseguire l'App web, è utile tooinsert righe degli eventi personalizzati toolog di codice.</span><span class="sxs-lookup"><span data-stu-id="29ac6-167">tooget a clear understanding of what users do with your web app, it's useful tooinsert lines of code toolog custom events.</span></span> <span data-ttu-id="29ac6-168">Questi eventi possono tenere traccia nulla da azioni dell'utente dettagliato, ad esempio facendo clic sui pulsanti specifici, eventi di business significativo toomore come effettuare l'acquisto o vincente un gioco.</span><span class="sxs-lookup"><span data-stu-id="29ac6-168">These events can track anything from detailed user actions such as clicking specific buttons, toomore significant business events such as making a purchase or winning a game.</span></span> 

<span data-ttu-id="29ac6-169">Sebbene in alcuni casi, le visualizzazioni della pagina possano rappresentare eventi utili, questo non è vero in generale.</span><span class="sxs-lookup"><span data-stu-id="29ac6-169">Although in some cases, page views can represent useful events, it isn't true in general.</span></span> <span data-ttu-id="29ac6-170">Un utente può aprire una pagina di prodotto senza dover acquistare il prodotto hello.</span><span class="sxs-lookup"><span data-stu-id="29ac6-170">A user can open a product page without buying hello product.</span></span> 

<span data-ttu-id="29ac6-171">Con eventi aziendali specifici, è possibile rappresentare in un grafico lo stato di avanzamento degli utenti all'interno del sito.</span><span class="sxs-lookup"><span data-stu-id="29ac6-171">With specific business events, you can chart your users' progress through your site.</span></span> <span data-ttu-id="29ac6-172">È possibile scoprirne le preferenze per le diverse opzioni e i punti in cui abbandonano il sito o hanno difficoltà.</span><span class="sxs-lookup"><span data-stu-id="29ac6-172">You can find out their preferences for different options, and where they drop out or have difficulties.</span></span> <span data-ttu-id="29ac6-173">Con queste informazioni, è possibile prendere decisioni informate sulla priorità hello nel backlog di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="29ac6-173">With this knowledge, you can make informed decisions about hello priorities in your development backlog.</span></span>

<span data-ttu-id="29ac6-174">Gli eventi possono essere registrati nella pagina web hello:</span><span class="sxs-lookup"><span data-stu-id="29ac6-174">Events can be logged in hello web page:</span></span>

```JavaScript

    appInsights.trackEvent("ExpandDetailTab", {DetailTab: tabName});
```

<span data-ttu-id="29ac6-175">O sul lato server hello dell'app web hello:</span><span class="sxs-lookup"><span data-stu-id="29ac6-175">Or in hello server side of hello web app:</span></span>

```C#
    var tc = new Microsoft.ApplicationInsights.TelemetryClient();
    tc.TrackEvent("CreatedAccount", new Dictionary<string,string> {"AccountType":account.Type}, null);
    ...
    tc.TrackEvent("AddedItemToCart", new Dictionary<string,string> {"Item":item.Name}, null);
    ...
    tc.TrackEvent("CompletedPurchase");
```

<span data-ttu-id="29ac6-176">È possibile collegare eventi toothese valori di proprietà, in modo che è possibile filtrare o suddividere gli eventi di hello quando si verifica nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="29ac6-176">You can attach property values toothese events, so that you can filter or split hello events when you inspect them in hello portal.</span></span> <span data-ttu-id="29ac6-177">Inoltre, un set standard di proprietà è associata tooeach evento, ad esempio ID utente anonimo, consentendo la sequenza di hello tootrace delle attività di un singolo utente.</span><span class="sxs-lookup"><span data-stu-id="29ac6-177">In addition, a standard set of properties is attached tooeach event, such as anonymous user ID, which allows you tootrace hello sequence of activities of an individual user.</span></span>

<span data-ttu-id="29ac6-178">Altre informazioni sugli [eventi personalizzati](app-insights-api-custom-events-metrics.md#trackevent) e le [proprietà](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="29ac6-178">Learn more about [custom events](app-insights-api-custom-events-metrics.md#trackevent) and [properties](app-insights-api-custom-events-metrics.md#properties).</span></span>

### <a name="slice-and-dice-events"></a><span data-ttu-id="29ac6-179">Analisi approfondita degli eventi</span><span class="sxs-lookup"><span data-stu-id="29ac6-179">Slice and dice events</span></span>

<span data-ttu-id="29ac6-180">In strumenti di utenti, sessioni e gli eventi hello, è possibile sezionare e ripartiscono eventi personalizzati dall'utente, nome dell'evento e le proprietà.</span><span class="sxs-lookup"><span data-stu-id="29ac6-180">In hello Users, Sessions, and Events tools, you can slice and dice custom events by user, event name, and properties.</span></span>
<span data-ttu-id="29ac6-181">![Utenti](./media/app-insights-usage-overview/users.png)</span><span class="sxs-lookup"><span data-stu-id="29ac6-181">![Users](./media/app-insights-usage-overview/users.png)</span></span>  
  
## <a name="design-hello-telemetry-with-hello-app"></a><span data-ttu-id="29ac6-182">Dati di telemetria di progettazione hello con app hello</span><span class="sxs-lookup"><span data-stu-id="29ac6-182">Design hello telemetry with hello app</span></span>

<span data-ttu-id="29ac6-183">Quando si progetta ogni funzionalità dell'app, considerare come verrà toomeasure il suo successo con gli utenti.</span><span class="sxs-lookup"><span data-stu-id="29ac6-183">When you are designing each feature of your app, consider how you are going toomeasure its success with your users.</span></span> <span data-ttu-id="29ac6-184">Decidere quali avviare gli eventi di business è necessario toorecord e codice hello chiamate per gli eventi di rilevamento nell'app da hello.</span><span class="sxs-lookup"><span data-stu-id="29ac6-184">Decide what business events you need toorecord, and code hello tracking calls for those events into your app from hello start.</span></span>

## <a name="a--b-testing"></a><span data-ttu-id="29ac6-185">Test A | B</span><span class="sxs-lookup"><span data-stu-id="29ac6-185">A | B Testing</span></span>
<span data-ttu-id="29ac6-186">Se non si conosce variante di una funzionalità sarà più efficace, rilasciare entrambe, rendere gli utenti di ogni toodifferent accessibile.</span><span class="sxs-lookup"><span data-stu-id="29ac6-186">If you don't know which variant of a feature will be more successful, release both of them, making each accessible toodifferent users.</span></span> <span data-ttu-id="29ac6-187">Misurare il successo di hello di ogni e quindi spostare tooa unificata versione.</span><span class="sxs-lookup"><span data-stu-id="29ac6-187">Measure hello success of each, and then move tooa unified version.</span></span>

<span data-ttu-id="29ac6-188">Questa tecnica, si collega la telemetria proprietà distinti valori tooall hello inviato da ogni versione dell'app.</span><span class="sxs-lookup"><span data-stu-id="29ac6-188">For this technique, you attach distinct property values tooall hello telemetry that is sent by each version of your app.</span></span> <span data-ttu-id="29ac6-189">È possibile farlo mediante la definizione di proprietà in hello TelemetryContext attivo.</span><span class="sxs-lookup"><span data-stu-id="29ac6-189">You can do that by defining properties in hello active TelemetryContext.</span></span> <span data-ttu-id="29ac6-190">Queste proprietà predefinite vengono aggiunte Invia messaggio di dati di telemetria tooevery applicazione hello - non solo i messaggi personalizzati, ma anche telemetria standard hello.</span><span class="sxs-lookup"><span data-stu-id="29ac6-190">These default properties are added tooevery telemetry message that hello application sends - not just your custom messages, but hello standard telemetry as well.</span></span>

<span data-ttu-id="29ac6-191">Nel portale Application Insights hello, filtrare e dividere i dati per valori di proprietà hello, in modo da versioni diverse di toocompare hello.</span><span class="sxs-lookup"><span data-stu-id="29ac6-191">In hello Application Insights portal, filter and split your data on hello property values, so as toocompare hello different versions.</span></span>

<span data-ttu-id="29ac6-192">toodo, [impostare un inizializzatore di telemetria](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):</span><span class="sxs-lookup"><span data-stu-id="29ac6-192">toodo this, [set up a telemetry initializer](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):</span></span>

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

<span data-ttu-id="29ac6-193">Nell'inizializzatore di app web hello, ad esempio Global.asax.cs:</span><span class="sxs-lookup"><span data-stu-id="29ac6-193">In hello web app initializer such as Global.asax.cs:</span></span>

```C#

    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```

<span data-ttu-id="29ac6-194">TelemetryClients di nuovo tutti aggiunge automaticamente il valore di proprietà hello specificato.</span><span class="sxs-lookup"><span data-stu-id="29ac6-194">All new TelemetryClients automatically add hello property value you specify.</span></span> <span data-ttu-id="29ac6-195">Gli eventi di telemetria singoli possono eseguire l'override di valori predefiniti di hello.</span><span class="sxs-lookup"><span data-stu-id="29ac6-195">Individual telemetry events can override hello default values.</span></span>

## <a name="next-steps"></a><span data-ttu-id="29ac6-196">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="29ac6-196">Next steps</span></span>
   - [<span data-ttu-id="29ac6-197">Utenti, sessioni ed eventi</span><span class="sxs-lookup"><span data-stu-id="29ac6-197">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
   - [<span data-ttu-id="29ac6-198">Grafici a imbuto</span><span class="sxs-lookup"><span data-stu-id="29ac6-198">Funnels</span></span>](usage-funnels.md)
   - [<span data-ttu-id="29ac6-199">Conservazione</span><span class="sxs-lookup"><span data-stu-id="29ac6-199">Retention</span></span>](app-insights-usage-retention.md)
   - [<span data-ttu-id="29ac6-200">Flussi degli utenti</span><span class="sxs-lookup"><span data-stu-id="29ac6-200">User Flows</span></span>](app-insights-usage-flows.md)
   - [<span data-ttu-id="29ac6-201">Cartelle di lavoro</span><span class="sxs-lookup"><span data-stu-id="29ac6-201">Workbooks</span></span>](app-insights-usage-workbooks.md)
   - [<span data-ttu-id="29ac6-202">Aggiungere il contesto utente</span><span class="sxs-lookup"><span data-stu-id="29ac6-202">Add user context</span></span>](app-insights-usage-send-user-context.md)
