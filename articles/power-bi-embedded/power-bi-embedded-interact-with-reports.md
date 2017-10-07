---
title: aaaInteract con i report utilizzando l'API JavaScript hello | Documenti Microsoft
description: Power BI incorporato, interagire con i report utilizzando hello API JavaScript
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: bdd885d3-1b00-4dcf-bdff-531eb1f97bfb
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: 657e4d5cee031bdda173ab3f451cc19b93ddb17b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="interact-with-power-bi-reports-using-hello-javascript-api"></a><span data-ttu-id="21d8f-103">Interagire con i report di Power BI usando hello API JavaScript</span><span class="sxs-lookup"><span data-stu-id="21d8f-103">Interact with Power BI reports using hello JavaScript API</span></span>
<span data-ttu-id="21d8f-104">Consente di API di Power BI JavaScript Hello è tooeasily incorporare i report di Power BI nelle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="21d8f-104">hello Power BI JavaScript API enables you tooeasily embed Power BI reports into your applications.</span></span> <span data-ttu-id="21d8f-105">Con hello API, le applicazioni a livello di codice possono interagire con gli elementi di report diverso come pagine e filtri.</span><span class="sxs-lookup"><span data-stu-id="21d8f-105">With hello API, your applications can programmatically interact with different report elements like pages and filters.</span></span> <span data-ttu-id="21d8f-106">Grazie a questa interattività i report di Power BI si integrano ancora meglio nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="21d8f-106">This interactivity makes Power BI reports a more integrated part of your application.</span></span>

<span data-ttu-id="21d8f-107">Incorporare un report di Power BI nell'applicazione usando un iframe ospitato come parte di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="21d8f-107">You embed a Power BI report in your application by using an iframe that is hosted as part of hello application.</span></span> <span data-ttu-id="21d8f-108">Hello iframe funge da confine tra l'applicazione e i report di hello, come può vedere nella seguente immagine hello.</span><span class="sxs-lookup"><span data-stu-id="21d8f-108">hello iframe acts as a boundary between your application and hello report, as you can see in hello following image.</span></span> 

![Iframe di Power BI Embedded senza l'API Javascript](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-1.png)

<span data-ttu-id="21d8f-110">Hello iframe rende hello incorporamento processo molto più semplice, ma senza hello API JavaScript hello report e l'applicazione non può interagire tra loro.</span><span class="sxs-lookup"><span data-stu-id="21d8f-110">hello iframe makes hello embedding process a lot easier, but without hello JavaScript API hello report and your application can't interact with each other.</span></span> <span data-ttu-id="21d8f-111">La mancanza di interazione può rendere ha l'impressione hello report non è effettivamente parte di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="21d8f-111">This lack of interaction can make it feel like hello report is not really part of hello application.</span></span> <span data-ttu-id="21d8f-112">applicazione e i report di hello è davvero necessario toocommunicate avanti e indietro, come illustrato di seguito immagine hello.</span><span class="sxs-lookup"><span data-stu-id="21d8f-112">hello report and application really need toocommunicate back and forth, as in hello following image.</span></span>

![Iframe di Power BI Embedded con l'API Javascript](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-2.png)

<span data-ttu-id="21d8f-114">API di Power BI JavaScript Hello consente codice toowrite in modo sicuro può passare attraverso il limite di iframe hello.</span><span class="sxs-lookup"><span data-stu-id="21d8f-114">hello Power BI JavaScript API enables you toowrite code that can securely pass through hello iframe boundary.</span></span> <span data-ttu-id="21d8f-115">In questo modo l'applicazione tooprogrammatically eseguire un'azione in un report e toolisten per gli eventi da azioni che gli utenti all'interno di report hello.</span><span class="sxs-lookup"><span data-stu-id="21d8f-115">This enables your application tooprogrammatically perform an action in a report, and toolisten for events from actions that users make within hello report.</span></span>

## <a name="what-can-you-do-with-hello-power-bi-javascript-api"></a><span data-ttu-id="21d8f-116">Cosa si può fare con l'API di Power BI JavaScript hello?</span><span class="sxs-lookup"><span data-stu-id="21d8f-116">What can you do with hello Power BI JavaScript API?</span></span>
<span data-ttu-id="21d8f-117">Con hello API JavaScript è possibile gestire i report, esplorare toopages in un report, filtrare un report e gestire gli eventi di incorporamento.</span><span class="sxs-lookup"><span data-stu-id="21d8f-117">With hello JavaScript API you can manage reports, navigate toopages in a report, filter a report, and handle embedding events.</span></span> <span data-ttu-id="21d8f-118">Hello diagramma seguente mostra la struttura hello di hello API.</span><span class="sxs-lookup"><span data-stu-id="21d8f-118">hello following diagram shows hello structure of hello API.</span></span>

![Diagramma dell'API JavaScript per Power BI](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-3.png)

### <a name="manage-reports"></a><span data-ttu-id="21d8f-120">Gestire i report</span><span class="sxs-lookup"><span data-stu-id="21d8f-120">Manage reports</span></span>
<span data-ttu-id="21d8f-121">Hello API Javascript consente toomanage comportamento a livello di pagina e report hello:</span><span class="sxs-lookup"><span data-stu-id="21d8f-121">hello Javascript API enables you toomanage behavior at hello report and page level:</span></span>

* <span data-ttu-id="21d8f-122">Incorporare in modo sicuro un determinato Report di Power BI in un'applicazione - provare a hello [incorporare applicazione demo](http://azure-samples.github.io/powerbi-angular-client/#/scenario1)</span><span class="sxs-lookup"><span data-stu-id="21d8f-122">Embed a specific Power BI Report securely in your application - try hello [embed demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario1)</span></span>
  * <span data-ttu-id="21d8f-123">Impostare il token di accesso</span><span class="sxs-lookup"><span data-stu-id="21d8f-123">Set access token</span></span>
* <span data-ttu-id="21d8f-124">Configurare i report di hello</span><span class="sxs-lookup"><span data-stu-id="21d8f-124">Configure hello report</span></span>
  * <span data-ttu-id="21d8f-125">Abilitare e disabilitare il riquadro filtro hello e riquadro di spostamento - provare a hello [applicazione demo di impostazioni di aggiornamento](http://azure-samples.github.io/powerbi-angular-client/#/scenario6)</span><span class="sxs-lookup"><span data-stu-id="21d8f-125">Enable and disable hello filter pane and page navigation pane - try hello [update settings demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario6)</span></span>
  * <span data-ttu-id="21d8f-126">Impostare i valori predefiniti per le pagine e filtri - provare a hello [demo di set di impostazioni predefinite](http://azure-samples.github.io/powerbi-angular-client/#/scenario5)</span><span class="sxs-lookup"><span data-stu-id="21d8f-126">Set defaults for pages and filters - try hello [set defaults demo](http://azure-samples.github.io/powerbi-angular-client/#/scenario5)</span></span>
* <span data-ttu-id="21d8f-127">Entrare e uscire dalla modalità schermo intero</span><span class="sxs-lookup"><span data-stu-id="21d8f-127">Enter and exit full screen mode</span></span>

[<span data-ttu-id="21d8f-128">Altre informazioni sull'incorporamento di un report</span><span class="sxs-lookup"><span data-stu-id="21d8f-128">Learn more about embedding a report</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embedding-Basics)

### <a name="navigate-toopages-in-a-report"></a><span data-ttu-id="21d8f-129">Passare toopages in un report</span><span class="sxs-lookup"><span data-stu-id="21d8f-129">Navigate toopages in a report</span></span>
<span data-ttu-id="21d8f-130">Hello API JavaScript enbales toodiscover per tutte le pagine nel report e tooset hello pagina corrente.</span><span class="sxs-lookup"><span data-stu-id="21d8f-130">hello JavaScript API enbales you toodiscover all pages in a report and tooset hello current page.</span></span> <span data-ttu-id="21d8f-131">Provare a hello [applicazione demo navigazione](http://azure-samples.github.io/powerbi-angular-client/#/scenario3).</span><span class="sxs-lookup"><span data-stu-id="21d8f-131">Try hello [navigation demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario3).</span></span>

[<span data-ttu-id="21d8f-132">Altre informazioni sullo spostamento tra le pagine</span><span class="sxs-lookup"><span data-stu-id="21d8f-132">Learn more about page navigation</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Page-Navigation)

### <a name="filter-a-report"></a><span data-ttu-id="21d8f-133">Filtrare un report</span><span class="sxs-lookup"><span data-stu-id="21d8f-133">Filter a report</span></span>
<span data-ttu-id="21d8f-134">Hello API JavaScript fornisce una base e avanzate di filtraggio dei report incorporati e le pagine del report.</span><span class="sxs-lookup"><span data-stu-id="21d8f-134">hello JavaScript API provides basic and advanced filtering capabilities for embedded reports and report pages.</span></span> <span data-ttu-id="21d8f-135">Provare a hello [filtro applicazione demo](http://azure-samples.github.io/powerbi-angular-client/#/scenario4)ed esaminare alcuni introduttivo qui il codice.</span><span class="sxs-lookup"><span data-stu-id="21d8f-135">Try hello [filtering demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario4), and review some introductory code here.</span></span>  

#### <a name="basic-filters"></a><span data-ttu-id="21d8f-136">Filtri di base</span><span class="sxs-lookup"><span data-stu-id="21d8f-136">Basic filters</span></span>
<span data-ttu-id="21d8f-137">Un filtro di base si trova in un livello di colonna o una gerarchia e contiene un elenco di valori tooinclude o exclude.</span><span class="sxs-lookup"><span data-stu-id="21d8f-137">A basic filter is placed on a column or hierarchy level and contains a list of values tooinclude or exclude.</span></span>

```
const basicFilter: pbi.models.IBasicFilter = {
  $schema: "http://powerbi.com/product/schema#basic",
  target: {
    table: "Store",
    column: "Count"
  },
  operator: "In",
  values: [1,2,3,4]
}
```


#### <a name="advanced-filters"></a><span data-ttu-id="21d8f-138">Filtri avanzati</span><span class="sxs-lookup"><span data-stu-id="21d8f-138">Advanced filters</span></span>
<span data-ttu-id="21d8f-139">Filtri avanzati utilizzano l'operatore logico hello e o OR e accettare le condizioni di uno o due, ognuna con i propri operatore e il valore.</span><span class="sxs-lookup"><span data-stu-id="21d8f-139">Advanced filters use hello logical operator AND or OR, and accept one or two conditions, each with their own operator and value.</span></span> <span data-ttu-id="21d8f-140">Le condizioni supportate sono:</span><span class="sxs-lookup"><span data-stu-id="21d8f-140">Supported conditions are:</span></span>

* <span data-ttu-id="21d8f-141">None</span><span class="sxs-lookup"><span data-stu-id="21d8f-141">None</span></span>
* <span data-ttu-id="21d8f-142">LessThan</span><span class="sxs-lookup"><span data-stu-id="21d8f-142">LessThan</span></span>
* <span data-ttu-id="21d8f-143">LessThanOrEqual</span><span class="sxs-lookup"><span data-stu-id="21d8f-143">LessThanOrEqual</span></span>
* <span data-ttu-id="21d8f-144">GreaterThan</span><span class="sxs-lookup"><span data-stu-id="21d8f-144">GreaterThan</span></span>
* <span data-ttu-id="21d8f-145">GreaterThanOrEqual</span><span class="sxs-lookup"><span data-stu-id="21d8f-145">GreaterThanOrEqual</span></span>
* <span data-ttu-id="21d8f-146">Contiene</span><span class="sxs-lookup"><span data-stu-id="21d8f-146">Contains</span></span>
* <span data-ttu-id="21d8f-147">DoesNotContain</span><span class="sxs-lookup"><span data-stu-id="21d8f-147">DoesNotContain</span></span>
* <span data-ttu-id="21d8f-148">StartsWith</span><span class="sxs-lookup"><span data-stu-id="21d8f-148">StartsWith</span></span>
* <span data-ttu-id="21d8f-149">DoesNotStartWith</span><span class="sxs-lookup"><span data-stu-id="21d8f-149">DoesNotStartWith</span></span>
* <span data-ttu-id="21d8f-150">Is</span><span class="sxs-lookup"><span data-stu-id="21d8f-150">Is</span></span>
* <span data-ttu-id="21d8f-151">IsNot</span><span class="sxs-lookup"><span data-stu-id="21d8f-151">IsNot</span></span>
* <span data-ttu-id="21d8f-152">IsBlank</span><span class="sxs-lookup"><span data-stu-id="21d8f-152">IsBlank</span></span>
* <span data-ttu-id="21d8f-153">IsNotBlank</span><span class="sxs-lookup"><span data-stu-id="21d8f-153">IsNotBlank</span></span>

```
const advancedFilter: pbi.models.IAdvancedFilter = {
  $schema: "http://powerbi.com/product/schema#advanced",
  target: {
    table: "Store",
    column: "Name"
  },
  logicalOperator: "Or",
  conditions: [
    {
      operator: "Contains",
      value: "Wash"
    },
    {
      operator: "Contains",
      value: "Park"
    }
  ]
}
```
[<span data-ttu-id="21d8f-154">Altre informazioni sui filtri</span><span class="sxs-lookup"><span data-stu-id="21d8f-154">Learn more about filtering</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Filters)

### <a name="handling-events"></a><span data-ttu-id="21d8f-155">Gestione degli eventi</span><span class="sxs-lookup"><span data-stu-id="21d8f-155">Handling events</span></span>
<span data-ttu-id="21d8f-156">Inoltre informazioni toosending in iframe hello, l'applicazione può anche ricevere informazioni su hello dopo gli eventi generati dalle hello iframe:</span><span class="sxs-lookup"><span data-stu-id="21d8f-156">In addition toosending information into hello iframe, your application can also receive information on hello following events coming from hello iframe:</span></span>

* <span data-ttu-id="21d8f-157">Embed</span><span class="sxs-lookup"><span data-stu-id="21d8f-157">Embed</span></span>
  * <span data-ttu-id="21d8f-158">loaded</span><span class="sxs-lookup"><span data-stu-id="21d8f-158">loaded</span></span>
  * <span data-ttu-id="21d8f-159">error</span><span class="sxs-lookup"><span data-stu-id="21d8f-159">error</span></span>
* <span data-ttu-id="21d8f-160">Report</span><span class="sxs-lookup"><span data-stu-id="21d8f-160">Reports</span></span>
  * <span data-ttu-id="21d8f-161">pageChanged</span><span class="sxs-lookup"><span data-stu-id="21d8f-161">pageChanged</span></span>
  * <span data-ttu-id="21d8f-162">dataSelected (presto disponibile)</span><span class="sxs-lookup"><span data-stu-id="21d8f-162">dataSelected (coming soon)</span></span>

[<span data-ttu-id="21d8f-163">Altre informazioni sulla gestione degli eventi</span><span class="sxs-lookup"><span data-stu-id="21d8f-163">Learn more about handling events</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Handling-Events)

## <a name="next-steps"></a><span data-ttu-id="21d8f-164">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="21d8f-164">Next steps</span></span>
<span data-ttu-id="21d8f-165">Per ulteriori informazioni su hello API JavaScript di Power BI, vedere hello seguenti collegamenti:</span><span class="sxs-lookup"><span data-stu-id="21d8f-165">For more information about hello Power BI JavaScript API, check out hello following links:</span></span>

* [<span data-ttu-id="21d8f-166">JavaScript API Wiki (Wiki sull'API JavaScript)</span><span class="sxs-lookup"><span data-stu-id="21d8f-166">JavaScript API Wiki</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki)
* [<span data-ttu-id="21d8f-167">Object model reference (Informazioni di riferimento sul modello a oggetti)</span><span class="sxs-lookup"><span data-stu-id="21d8f-167">Object model reference</span></span>](https://microsoft.github.io/powerbi-models/modules/_models_.html)
* <span data-ttu-id="21d8f-168">Esempi</span><span class="sxs-lookup"><span data-stu-id="21d8f-168">Samples</span></span>
  * [<span data-ttu-id="21d8f-169">Angular</span><span class="sxs-lookup"><span data-stu-id="21d8f-169">Angular</span></span>](http://azure-samples.github.io/powerbi-angular-client)
  * [<span data-ttu-id="21d8f-170">Ember</span><span class="sxs-lookup"><span data-stu-id="21d8f-170">Ember</span></span>](https://github.com/Microsoft/powerbi-ember)
* [<span data-ttu-id="21d8f-171">Live demo (Demo live)</span><span class="sxs-lookup"><span data-stu-id="21d8f-171">Live demo</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)

