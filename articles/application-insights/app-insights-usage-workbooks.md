---
title: Analizzare e condividere i dati di utilizzo con cartelle di lavoro interattive in Azure Application Insights | Microsoft docs
description: Analisi demografica degli utenti dell'app Web.
services: application-insights
documentationcenter: 
author: numberbycolors
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 06/12/2017
ms.author: bwren
ms.openlocfilehash: 75028b4fbda43d90f56690a33c7eb624fce049c8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="investigate-and-share-usage-data-with-interactive-workbooks-in-application-insights"></a><span data-ttu-id="36638-103">Analizzare e condividere i dati di utilizzo con cartelle di lavoro interattive in Application Insights</span><span class="sxs-lookup"><span data-stu-id="36638-103">Investigate and share usage data with interactive workbooks in Application Insights</span></span>

<span data-ttu-id="36638-104">Le cartelle di lavoro combinano le visualizzazioni dei dati di [Azure Application Insights](app-insights-overview.md), le [query di Analisi](app-insights-analytics.md) e il testo in documenti interattivi.</span><span class="sxs-lookup"><span data-stu-id="36638-104">Workbooks combine [Azure Application Insights](app-insights-overview.md) data visualizations, [Analytics queries](app-insights-analytics.md), and text into interactive documents.</span></span> <span data-ttu-id="36638-105">Le cartelle di lavoro possono essere modificate da altri membri del team con accesso alla stessa risorsa di Azure.</span><span class="sxs-lookup"><span data-stu-id="36638-105">Workbooks are editable by other team members with access to the same Azure resource.</span></span> <span data-ttu-id="36638-106">Ciò significa che le query e i controlli usati per creare una cartella di lavoro sono disponibili ad altri utenti che leggono la cartella di lavoro semplificandone l'esplorazione, l'estensione e la ricerca di errori.</span><span class="sxs-lookup"><span data-stu-id="36638-106">This means the queries and controls used to create a workbook are available to other people reading the workbook, making them easy to explore, extend, and check for mistakes.</span></span>

<span data-ttu-id="36638-107">Le cartelle di lavoro sono utili per scenari simili ai seguenti:</span><span class="sxs-lookup"><span data-stu-id="36638-107">Workbooks are helpful for scenarios like:</span></span>

* <span data-ttu-id="36638-108">Esplorazione dell'utilizzo dell'app quando non si conoscono le metriche di interesse in anticipo, ovvero il numero di utenti, i tassi di fidelizzazione, i tassi di conversione e così via. A differenza di altri strumenti di analisi dell'utilizzo di Application Insights, le cartelle di lavoro consentono di combinare più tipi di visualizzazioni e analisi risultando ideali per questo tipo di esplorazione in formato libero.</span><span class="sxs-lookup"><span data-stu-id="36638-108">Exploring the usage of your app when you don't know the metrics of interest in advance: numbers of users, retention rates, conversion rates, etc. Unlike other usage analytics tools in Application Insights, workbooks let you combine multiple kinds of visualizations and analyses, making them great for this kind of free-form exploration.</span></span>
* <span data-ttu-id="36638-109">Descrizione al proprio team delle prestazioni di una nuova funzionalità rilasciata visualizzando i conteggi degli utenti per le interazioni chiave e altre metriche.</span><span class="sxs-lookup"><span data-stu-id="36638-109">Explaining to your team how a newly released feature is performing, by showing user counts for key interactions and other metrics.</span></span>
* <span data-ttu-id="36638-110">Condivisione dei risultati di un esperimento A/B nell'app con altri membri del team.</span><span class="sxs-lookup"><span data-stu-id="36638-110">Sharing the results of an A/B experiment in your app with other members of your team.</span></span> <span data-ttu-id="36638-111">È possibile descrivere gli obiettivi dell'esperimento usando testo e visualizzare ogni metrica di utilizzo e query di Analisi usate per valutare l'esperimento con callout chiari che indicano se la singola metrica è al di sopra o al di sotto del target.</span><span class="sxs-lookup"><span data-stu-id="36638-111">You can explain the goals for the experiment with text, then show each usage metric and Analytics query used to evaluate the experiment, along with clear call-outs for whether each metric was above- or below-target.</span></span>
* <span data-ttu-id="36638-112">Segnalazione dell'impatto di un'interruzione nell'utilizzo dell'app, combinazione dei dati, spiegazione del testo e descrizione dei passaggi successivi per impedire interruzioni future.</span><span class="sxs-lookup"><span data-stu-id="36638-112">Reporting the impact of an outage on the usage of your app, combining data, text explanation, and a discussion of next steps to prevent outages in the future.</span></span>

> [!NOTE]
> <span data-ttu-id="36638-113">La risorsa di Application Insights deve contenere visualizzazioni di pagina o eventi personalizzati per usare le cartelle di lavoro.</span><span class="sxs-lookup"><span data-stu-id="36638-113">Your Application Insights resource must contain page views or custom events to use workbooks.</span></span> <span data-ttu-id="36638-114">Vedere le [informazioni su come configurare l'app per la raccolta automatica delle visualizzazioni di pagina con Application Insights JavaScript SDK](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="36638-114">[Learn how to set up your app to collect page views automatically with the Application Insights JavaScript SDK](app-insights-javascript.md).</span></span>
> 
> 

## <a name="editing-rearranging-cloning-and-deleting-workbook-sections"></a><span data-ttu-id="36638-115">Modifica, ridisposizione, clonazione ed eliminazione di sezioni delle cartelle di lavoro</span><span class="sxs-lookup"><span data-stu-id="36638-115">Editing, rearranging, cloning, and deleting workbook sections</span></span>

<span data-ttu-id="36638-116">Una cartella di lavoro è costituita da sezioni: visualizzazioni dell'utilizzo modificabili separatamente, grafici, tabelle, testo o risultati delle query di Analisi.</span><span class="sxs-lookup"><span data-stu-id="36638-116">A workbook is a made of sections: independently editable usage visualizations, charts, tables, text, or Analytics query results.</span></span>

<span data-ttu-id="36638-117">Per modificare il contenuto di una sezione di una cartella di lavoro, fare clic sul pulsante **Modifica** sotto e a destra della sezione.</span><span class="sxs-lookup"><span data-stu-id="36638-117">To edit the contents of a workbook section, click the **Edit** button below and to the right of the workbook section.</span></span>

![Controlli di modifica delle sezioni delle cartelle di controllo di Application Insights](./media/app-insights-usage-workbooks/editing-controls.png)

1. <span data-ttu-id="36638-119">Dopo aver modificato una sezione, fare clic su **Modifica completata** nell'angolo inferiore sinistro della sezione.</span><span class="sxs-lookup"><span data-stu-id="36638-119">When you're done editing a section, click **Done Editing** in the bottom left corner of the section.</span></span>

2. <span data-ttu-id="36638-120">Per creare un duplicato di una sezione, fare clic sull'icona **Clona questa sezione**.</span><span class="sxs-lookup"><span data-stu-id="36638-120">To create a duplicate of a section, click the **Clone this section** icon.</span></span> <span data-ttu-id="36638-121">La creazione di sezioni duplicate è un ottimo modo per eseguire l'iterazione in una query senza perdere le iterazioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="36638-121">Creating duplicate sections is a great to way to iterate on a query without losing previous iterations.</span></span>

3. <span data-ttu-id="36638-122">Per spostare una sezione verso l'alto in una cartella di lavoro, fare clic sull'icona **Sposta in alto** o **Sposta giù**.</span><span class="sxs-lookup"><span data-stu-id="36638-122">To move up a section in a workbook, click the **Move up** or **Move down** icon.</span></span>

4. <span data-ttu-id="36638-123">Per rimuovere una sezione in modo permanente, fare clic sull'icona **Rimuovi**.</span><span class="sxs-lookup"><span data-stu-id="36638-123">To remove a section permanently, click the **Remove** icon.</span></span>

## <a name="adding-usage-data-visualization-sections"></a><span data-ttu-id="36638-124">Aggiunta di sezioni di visualizzazioni dei dati di utilizzo</span><span class="sxs-lookup"><span data-stu-id="36638-124">Adding usage data visualization sections</span></span>

<span data-ttu-id="36638-125">Le cartelle di lavoro offrono quattro tipi di visualizzazioni di analisi di utilizzo predefiniti.</span><span class="sxs-lookup"><span data-stu-id="36638-125">Workbooks offer four types of built-in usage analytics visualizations.</span></span> <span data-ttu-id="36638-126">Ogni tipo risponde a una domanda comune sull'utilizzo dell'app.</span><span class="sxs-lookup"><span data-stu-id="36638-126">Each answers a common question about the usage of your app.</span></span> <span data-ttu-id="36638-127">Per aggiungere tabelle e grafici diversi da queste quattro sezioni, aggiungere sezioni di query di Analisi (vedere sotto).</span><span class="sxs-lookup"><span data-stu-id="36638-127">To add tables and charts other than these four sections, add Analytics query sections (see below).</span></span>

<span data-ttu-id="36638-128">Per aggiungere una sezione Utenti, Sessioni, Eventi o Conservazione alla cartella di lavoro, usare il pulsante **Aggiungi utenti** o un pulsante corrispondente nella parte inferiore della cartella di lavoro o di una sezione.</span><span class="sxs-lookup"><span data-stu-id="36638-128">To add a Users, Sessions, Events, or Retention section to your workbook, use the **Add Users** or other corresponding button at the bottom of the workbook, or at the bottom of any section.</span></span>

![Sezione Utenti nelle cartelle di lavoro](./media/app-insights-usage-workbooks/users-section.png)

<span data-ttu-id="36638-130">Le sezioni **Utenti** rispondono alla domanda "Quanti utenti hanno visualizzato una pagina o usato una funzionalità del sito?"</span><span class="sxs-lookup"><span data-stu-id="36638-130">**Users** sections answer "How many users viewed some page or used some feature of my site?"</span></span>

<span data-ttu-id="36638-131">Le sezioni **Sessioni** rispondono alla domanda "Per quante sessioni gli utenti hanno visualizzato una pagina o usato una funzionalità del sito?"</span><span class="sxs-lookup"><span data-stu-id="36638-131">**Sessions** sections answer "How many sessions did users spend viewing some page or using some feature of my site?"</span></span>

<span data-ttu-id="36638-132">Le sezioni **Eventi** rispondono alla domanda "Quante volte gli utenti hanno visualizzato una pagina o usato una funzionalità del sito?"</span><span class="sxs-lookup"><span data-stu-id="36638-132">**Events** sections answer "How many times did users view some page or use some feature of my site?"</span></span>

<span data-ttu-id="36638-133">Ognuno di questi tre tipi di sezione include gli stessi insiemi di controlli e visualizzazioni:</span><span class="sxs-lookup"><span data-stu-id="36638-133">Each of these three section types offers the same sets of controls and visualizations:</span></span>

* <span data-ttu-id="36638-134">Vedere le [informazioni sulla modifica delle sezioni Utenti, Sessioni ed Eventi](app-insights-usage-segmentation.md)</span><span class="sxs-lookup"><span data-stu-id="36638-134">[Learn more about editing Users, Sessions, and Events sections](app-insights-usage-segmentation.md)</span></span>
* <span data-ttu-id="36638-135">Attivare o disattivare il grafico principale, le griglie degli istogrammi, le informazioni dettagliate automatiche e le visualizzazioni utenti di esempio usando le caselle di controllo **Mostra grafico**, **Mostra griglia**, **Mostra i dettagli** e **Esempio di questi utenti** nella parte superiore di ogni sezione.</span><span class="sxs-lookup"><span data-stu-id="36638-135">Toggle the main chart, histogram grids, automatic insights, and sample users visualizations using the **Show Chart**, **Show Grid**, **Show Insights**, and **Sample of These Users** checkboxes at the top of each section.</span></span>

![Sezione Conservazione nelle cartelle di lavoro](./media/app-insights-usage-workbooks/retention-section.png)

<span data-ttu-id="36638-137">Le sezioni **Conservazione** rispondono alla domanda "Degli utenti che hanno visualizzato una pagina o usato una funzionalità in un determinato giorno o settimana quanti sono tornati un giorno o una settimana successiva?"</span><span class="sxs-lookup"><span data-stu-id="36638-137">**Retention** sections answer "Of people who viewed some page or used some feature on one day or week, how many came back in a subsequent day or week?"</span></span>

* <span data-ttu-id="36638-138">Vedere le [informazioni sulla modifica delle sezioni Conservazione](app-insights-usage-retention.md)</span><span class="sxs-lookup"><span data-stu-id="36638-138">[Learn more about editing Retention sections](app-insights-usage-retention.md)</span></span>
* <span data-ttu-id="36638-139">Attivare o disattivare il grafico Totale conservazione facoltativo usando la casella di controllo **Mostra il grafico generale della conservazione** nella parte superiore della sezione.</span><span class="sxs-lookup"><span data-stu-id="36638-139">Toggle the optional Overall Retention chart using the **Show overall retention chart** checkbox at the top of the section.</span></span>

## <a name="adding-application-insights-analytics-sections"></a><span data-ttu-id="36638-140">Aggiunta di sezioni di analisi di Application Insights</span><span class="sxs-lookup"><span data-stu-id="36638-140">Adding Application Insights Analytics sections</span></span>

![Sezione di analisi nelle cartelle di lavoro](./media/app-insights-usage-workbooks/analytics-section.png)

<span data-ttu-id="36638-142">Per aggiungere una sezione di query di Analisi di Application Insights alla cartella di lavoro, usare il pulsante **Aggiungi query di analisi** nella parte inferiore della cartella di lavoro o nella parte inferiore di una sezione.</span><span class="sxs-lookup"><span data-stu-id="36638-142">To add an Application Insights Analytics query section to your workbook, use the **Add Analytics query** button at the bottom of the workbook, or at the bottom of any section.</span></span>

<span data-ttu-id="36638-143">Le sezioni delle query di Analisi consentono di aggiungere query arbitrarie nei dati di Application Insights nelle cartelle di lavoro.</span><span class="sxs-lookup"><span data-stu-id="36638-143">Analytics query sections let you add arbitrary queries over your Application Insights data into workbooks.</span></span> <span data-ttu-id="36638-144">Questa flessibilità consente di usare le sezioni di query di Analisi per rispondere a qualsiasi domanda sul sito diversa dalle quattro domande indicate in precedenza per le sezioni Utenti, Sessioni, Eventi e Conservazione, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="36638-144">This flexibility means Analytics query sections should be your go-to for answering any questions about your site other than the four listed above for Users, Sessions, Events, and Retention, like:</span></span>

* <span data-ttu-id="36638-145">Quante eccezioni ha generato il sito nello stesso periodo di tempo come riduzione dell'utilizzo?</span><span class="sxs-lookup"><span data-stu-id="36638-145">How many exceptions did your site throw during the same time period as a decline in usage?</span></span>
* <span data-ttu-id="36638-146">Qual è stata la distribuzione dei tempi di caricamento della pagina per gli utenti che visualizzano una pagina?</span><span class="sxs-lookup"><span data-stu-id="36638-146">What was the distribution of page load times for users viewing some page?</span></span>
* <span data-ttu-id="36638-147">Quanti utenti hanno visualizzato un insieme di pagine nel sito ma non un altro insieme di pagine?</span><span class="sxs-lookup"><span data-stu-id="36638-147">How many users viewed some set of pages on your site, but not some other set of pages?</span></span> <span data-ttu-id="36638-148">Queste informazioni possono essere utili per comprendere se sono presenti cluster di utenti che usano sottoinsiemi diversi di funzionalità del sito (usare l'operatore `join` con il modificatore `kind=leftanti` nel linguaggio di query di Log Analytics).</span><span class="sxs-lookup"><span data-stu-id="36638-148">This can be useful to understand if you have clusters of users who use different subsets of your site's functionality (use the `join` operator with the `kind=leftanti` modifier in the Log Analytics query language).</span></span>

<span data-ttu-id="36638-149">Usare le [informazioni di riferimento sul linguaggio di query di Log Analytics](https://docs.loganalytics.io/) per altre informazioni sulla scrittura di query.</span><span class="sxs-lookup"><span data-stu-id="36638-149">Use the [Log Analytics query language reference](https://docs.loganalytics.io/) to learn more about writing queries.</span></span>

## <a name="adding-text-and-markdown-sections"></a><span data-ttu-id="36638-150">Aggiunta di sezioni di testo e Markdown</span><span class="sxs-lookup"><span data-stu-id="36638-150">Adding text and Markdown sections</span></span>

<span data-ttu-id="36638-151">L'aggiunta di intestazioni, spiegazioni e commenti nelle cartelle di lavoro consente di trasformare un insieme di tabelle e grafici in un resoconto.</span><span class="sxs-lookup"><span data-stu-id="36638-151">Adding headings, explanations, and commentary to your workbooks helps turn a set of tables and charts into a narrative.</span></span> <span data-ttu-id="36638-152">Le sezioni di testo nelle cartelle di lavoro supportano la [sintassi Markdown](https://daringfireball.net/projects/markdown/) per la formattazione del testo, ad esempio intestazioni, grassetto, corsivo ed elenchi puntati.</span><span class="sxs-lookup"><span data-stu-id="36638-152">Text sections in workbooks support the [Markdown syntax](https://daringfireball.net/projects/markdown/) for text formatting, like headings, bold, italics, and bulleted lists.</span></span>

<span data-ttu-id="36638-153">Per aggiungere una sezione di testo alla cartella di lavoro, usare il pulsante **Aggiungi testo** nella parte inferiore della cartella di lavoro o nella parte inferiore di una sezione.</span><span class="sxs-lookup"><span data-stu-id="36638-153">To add a text section to your workbook, use the **Add text** button at the bottom of the workbook, or at the bottom of any section.</span></span>

## <a name="saving-and-sharing-workbooks-with-your-team"></a><span data-ttu-id="36638-154">Salvataggio e condivisione delle cartelle di lavoro con il team</span><span class="sxs-lookup"><span data-stu-id="36638-154">Saving and sharing workbooks with your team</span></span>

<span data-ttu-id="36638-155">Le cartelle di lavoro vengono salvate all'interno di una risorsa di Application Insights, ovvero nella sezione **Report personali** privata o nella sezione **Report condivisi** accessibile a tutti gli utenti che hanno accesso alla risorsa di Application Insights.</span><span class="sxs-lookup"><span data-stu-id="36638-155">Workbooks are saved within an Application Insights resource, either in the **My Reports** section that's private to you or in the **Shared Reports** section that's accessible to everyone with access to the Application Insights resource.</span></span> <span data-ttu-id="36638-156">Per visualizzare tutte le cartelle di lavoro della risorsa, fare clic sul pulsante **Apri** nella barra delle azioni.</span><span class="sxs-lookup"><span data-stu-id="36638-156">To view all the workbooks in the resource, click the **Open** button in the action bar.</span></span>

<span data-ttu-id="36638-157">Per condividere una cartella di lavoro che è attualmente in **Report personali**:</span><span class="sxs-lookup"><span data-stu-id="36638-157">To share a workbook that's currently in **My Reports**:</span></span>

1. <span data-ttu-id="36638-158">Fare clic su **Apri** nella barra delle azioni</span><span class="sxs-lookup"><span data-stu-id="36638-158">Click **Open** in the action bar</span></span>
2. <span data-ttu-id="36638-159">Fare clic sul pulsante "…" accanto alla cartella di lavoro da condividere</span><span class="sxs-lookup"><span data-stu-id="36638-159">Click the "..." button beside the workbook you want to share</span></span>
3. <span data-ttu-id="36638-160">Fare clic su **Sposta in Report condivisi**.</span><span class="sxs-lookup"><span data-stu-id="36638-160">Click **Move to Shared Reports**.</span></span>

<span data-ttu-id="36638-161">Per condividere una cartella di lavoro con un collegamento o tramite posta elettronica, fare clic su **Condividi** nella barra delle azioni.</span><span class="sxs-lookup"><span data-stu-id="36638-161">To share a workbook with a link or via email, click **Share** in the action bar.</span></span> <span data-ttu-id="36638-162">Tenere presente che i destinatari del collegamento necessitano dell'accesso alla risorsa nel portale di Azure per visualizzare la cartella di lavoro.</span><span class="sxs-lookup"><span data-stu-id="36638-162">Keep in mind that recipients of the link need access to this resource in the Azure portal to view the workbook.</span></span> <span data-ttu-id="36638-163">Per apportare modifiche, i destinatari devono avere almeno le autorizzazioni di collaboratori per la risorsa.</span><span class="sxs-lookup"><span data-stu-id="36638-163">To make edits, recipients need at least Contributor permissions for the resource.</span></span>

<span data-ttu-id="36638-164">Per aggiungere un collegamento in una cartella di lavoro in un dashboard di Azure:</span><span class="sxs-lookup"><span data-stu-id="36638-164">To pin a link to a workbook to an Azure Dashboard:</span></span>

1. <span data-ttu-id="36638-165">Fare clic su **Apri** nella barra delle azioni</span><span class="sxs-lookup"><span data-stu-id="36638-165">Click **Open** in the action bar</span></span>
2. <span data-ttu-id="36638-166">Fare clic sul pulsante "…" accanto alla cartella di lavoro da aggiungere</span><span class="sxs-lookup"><span data-stu-id="36638-166">Click the "..." button beside the workbook you want to pin</span></span>
3. <span data-ttu-id="36638-167">Fare clic su **Aggiungi al dashboard**.</span><span class="sxs-lookup"><span data-stu-id="36638-167">Click **Pin to dashboard**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36638-168">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="36638-168">Next steps</span></span>

## <a name="next-steps"></a><span data-ttu-id="36638-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="36638-169">Next steps</span></span>
- <span data-ttu-id="36638-170">Per abilitare le esperienze di utilizzo, iniziare a inviare [eventi personalizzati](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) o [visualizzazioni pagina](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="36638-170">To enable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="36638-171">Se si inviano già eventi personalizzati o visualizzazioni pagina, è possibile esplorare gli strumenti relativi all'uso per scoprire come gli utenti usano il servizio.</span><span class="sxs-lookup"><span data-stu-id="36638-171">If you already send custom events or page views, explore the Usage tools to learn how users use your service.</span></span>
    - [<span data-ttu-id="36638-172">Utenti, sessioni ed eventi</span><span class="sxs-lookup"><span data-stu-id="36638-172">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
    - [<span data-ttu-id="36638-173">Grafici a imbuto</span><span class="sxs-lookup"><span data-stu-id="36638-173">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="36638-174">Conservazione</span><span class="sxs-lookup"><span data-stu-id="36638-174">Retention</span></span>](app-insights-usage-retention.md)
    - [<span data-ttu-id="36638-175">Flussi degli utenti</span><span class="sxs-lookup"><span data-stu-id="36638-175">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="36638-176">Aggiungere il contesto utente</span><span class="sxs-lookup"><span data-stu-id="36638-176">Add user context</span></span>](app-insights-usage-send-user-context.md)
    
