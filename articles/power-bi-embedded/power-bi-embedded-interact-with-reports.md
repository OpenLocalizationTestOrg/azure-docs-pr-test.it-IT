---
title: Interagire con i report usando l'API JavaScript | Microsoft Docs
description: Power BI Embedded, interagire con i report usando l'API JavaScript
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
ms.openlocfilehash: 500462ac835674d80650c02aa7fc629b4a975857
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="interact-with-power-bi-reports-using-the-javascript-api"></a><span data-ttu-id="08f9c-103">Interagire con i report di Power BI usando l'API JavaScript</span><span class="sxs-lookup"><span data-stu-id="08f9c-103">Interact with Power BI reports using the JavaScript API</span></span>
<span data-ttu-id="08f9c-104">L'API JavaScript per Power BI consente di incorporare facilmente i report di Power BI nelle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="08f9c-104">The Power BI JavaScript API enables you to easily embed Power BI reports into your applications.</span></span> <span data-ttu-id="08f9c-105">Con l'API, le applicazioni possono interagire a livello di codice con elementi diversi dei report, ad esempio pagine e filtri.</span><span class="sxs-lookup"><span data-stu-id="08f9c-105">With the API, your applications can programmatically interact with different report elements like pages and filters.</span></span> <span data-ttu-id="08f9c-106">Grazie a questa interattività i report di Power BI si integrano ancora meglio nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="08f9c-106">This interactivity makes Power BI reports a more integrated part of your application.</span></span>

<span data-ttu-id="08f9c-107">Per incorporare un report di Power BI nell'applicazione, usare un iframe ospitato nell'ambito dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="08f9c-107">You embed a Power BI report in your application by using an iframe that is hosted as part of the application.</span></span> <span data-ttu-id="08f9c-108">L'iframe viene usato come limite tra l'applicazione e il report, come si può osservare nell'immagine seguente.</span><span class="sxs-lookup"><span data-stu-id="08f9c-108">The iframe acts as a boundary between your application and the report, as you can see in the following image.</span></span> 

![Iframe di Power BI Embedded senza l'API Javascript](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-1.png)

<span data-ttu-id="08f9c-110">L'iframe facilita considerevolmente il processo di incorporamento, ma senza l'API JavaScript il report e l'applicazione non possono interagire.</span><span class="sxs-lookup"><span data-stu-id="08f9c-110">The iframe makes the embedding process a lot easier, but without the JavaScript API the report and your application can't interact with each other.</span></span> <span data-ttu-id="08f9c-111">Questa mancanza di interazione può far credere che il report non faccia effettivamente parte dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="08f9c-111">This lack of interaction can make it feel like the report is not really part of the application.</span></span> <span data-ttu-id="08f9c-112">Il report e l'applicazione devono effettivamente comunicare in entrambe le direzioni, come nell'immagine seguente.</span><span class="sxs-lookup"><span data-stu-id="08f9c-112">The report and application really need to communicate back and forth, as in the following image.</span></span>

![Iframe di Power BI Embedded con l'API Javascript](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-2.png)

<span data-ttu-id="08f9c-114">L'API JavaScript per Power BI consente di scrivere codice che può passare in modo sicuro attraverso il limite dell'iframe.</span><span class="sxs-lookup"><span data-stu-id="08f9c-114">The Power BI JavaScript API enables you to write code that can securely pass through the iframe boundary.</span></span> <span data-ttu-id="08f9c-115">Ciò consente all'applicazione di eseguire a livello di codice un'azione in un report e di essere in ascolto degli eventi generati dalle azioni eseguite dagli utenti nel report.</span><span class="sxs-lookup"><span data-stu-id="08f9c-115">This enables your application to programmatically perform an action in a report, and to listen for events from actions that users make within the report.</span></span>

## <a name="what-can-you-do-with-the-power-bi-javascript-api"></a><span data-ttu-id="08f9c-116">Che cosa si può fare con l'API JavaScript per Power BI?</span><span class="sxs-lookup"><span data-stu-id="08f9c-116">What can you do with the Power BI JavaScript API?</span></span>
<span data-ttu-id="08f9c-117">Con l'API JavaScript è possibile gestire i report, accedere alle pagine di un report, filtrare un report e gestire l'incorporamento degli eventi.</span><span class="sxs-lookup"><span data-stu-id="08f9c-117">With the JavaScript API you can manage reports, navigate to pages in a report, filter a report, and handle embedding events.</span></span> <span data-ttu-id="08f9c-118">Il diagramma seguente mostra la struttura dell'API.</span><span class="sxs-lookup"><span data-stu-id="08f9c-118">The following diagram shows the structure of the API.</span></span>

![Diagramma dell'API JavaScript per Power BI](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-3.png)

### <a name="manage-reports"></a><span data-ttu-id="08f9c-120">Gestire i report</span><span class="sxs-lookup"><span data-stu-id="08f9c-120">Manage reports</span></span>
<span data-ttu-id="08f9c-121">L'API Javascript consente di gestire il comportamento a livello di pagina e di report:</span><span class="sxs-lookup"><span data-stu-id="08f9c-121">The Javascript API enables you to manage behavior at the report and page level:</span></span>

* <span data-ttu-id="08f9c-122">Incorporare un report di Power BI specifico in modo sicuro nell'applicazione: provare l' [applicazione demo di incorporamento](http://azure-samples.github.io/powerbi-angular-client/#/scenario1)</span><span class="sxs-lookup"><span data-stu-id="08f9c-122">Embed a specific Power BI Report securely in your application - try the [embed demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario1)</span></span>
  * <span data-ttu-id="08f9c-123">Impostare il token di accesso</span><span class="sxs-lookup"><span data-stu-id="08f9c-123">Set access token</span></span>
* <span data-ttu-id="08f9c-124">Configurare il report</span><span class="sxs-lookup"><span data-stu-id="08f9c-124">Configure the report</span></span>
  * <span data-ttu-id="08f9c-125">Abilitare e disabilitare il riquadro del filtro e il riquadro di spostamento della pagina: provare l' [applicazione demo di aggiornamento delle impostazioni](http://azure-samples.github.io/powerbi-angular-client/#/scenario6)</span><span class="sxs-lookup"><span data-stu-id="08f9c-125">Enable and disable the filter pane and page navigation pane - try the [update settings demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario6)</span></span>
  * <span data-ttu-id="08f9c-126">Impostare i valori predefiniti per le pagine e i filtri: provare la [demo di impostazione dei valori predefiniti](http://azure-samples.github.io/powerbi-angular-client/#/scenario5)</span><span class="sxs-lookup"><span data-stu-id="08f9c-126">Set defaults for pages and filters - try the [set defaults demo](http://azure-samples.github.io/powerbi-angular-client/#/scenario5)</span></span>
* <span data-ttu-id="08f9c-127">Entrare e uscire dalla modalità schermo intero</span><span class="sxs-lookup"><span data-stu-id="08f9c-127">Enter and exit full screen mode</span></span>

[<span data-ttu-id="08f9c-128">Altre informazioni sull'incorporamento di un report</span><span class="sxs-lookup"><span data-stu-id="08f9c-128">Learn more about embedding a report</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embedding-Basics)

### <a name="navigate-to-pages-in-a-report"></a><span data-ttu-id="08f9c-129">Passare alle pagine in un report</span><span class="sxs-lookup"><span data-stu-id="08f9c-129">Navigate to pages in a report</span></span>
<span data-ttu-id="08f9c-130">L'API JavaScript consente di trovare tutte le pagine di un report e di impostare la pagina corrente.</span><span class="sxs-lookup"><span data-stu-id="08f9c-130">The JavaScript API enbales you to discover all pages in a report and to set the current page.</span></span> <span data-ttu-id="08f9c-131">Provare l' [applicazione demo di spostamento](http://azure-samples.github.io/powerbi-angular-client/#/scenario3).</span><span class="sxs-lookup"><span data-stu-id="08f9c-131">Try the [navigation demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario3).</span></span>

[<span data-ttu-id="08f9c-132">Altre informazioni sullo spostamento tra le pagine</span><span class="sxs-lookup"><span data-stu-id="08f9c-132">Learn more about page navigation</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Page-Navigation)

### <a name="filter-a-report"></a><span data-ttu-id="08f9c-133">Filtrare un report</span><span class="sxs-lookup"><span data-stu-id="08f9c-133">Filter a report</span></span>
<span data-ttu-id="08f9c-134">L'API JavaScript fornisce funzionalità di filtro di base e avanzate per le pagine di report e i report incorporati.</span><span class="sxs-lookup"><span data-stu-id="08f9c-134">The JavaScript API provides basic and advanced filtering capabilities for embedded reports and report pages.</span></span> <span data-ttu-id="08f9c-135">Provare l' [applicazione demo di filtro](http://azure-samples.github.io/powerbi-angular-client/#/scenario4)ed esaminare un codice introduttivo qui.</span><span class="sxs-lookup"><span data-stu-id="08f9c-135">Try the [filtering demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario4), and review some introductory code here.</span></span>  

#### <a name="basic-filters"></a><span data-ttu-id="08f9c-136">Filtri di base</span><span class="sxs-lookup"><span data-stu-id="08f9c-136">Basic filters</span></span>
<span data-ttu-id="08f9c-137">Un filtro di base viene applicato a livello di colonna o di gerarchia e contiene un elenco di valori da includere o escludere.</span><span class="sxs-lookup"><span data-stu-id="08f9c-137">A basic filter is placed on a column or hierarchy level and contains a list of values to include or exclude.</span></span>

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


#### <a name="advanced-filters"></a><span data-ttu-id="08f9c-138">Filtri avanzati</span><span class="sxs-lookup"><span data-stu-id="08f9c-138">Advanced filters</span></span>
<span data-ttu-id="08f9c-139">I filtri avanzati usano l'operatore logico AND o OR e accettano una o due condizioni, ognuna con il proprio operatore e valore.</span><span class="sxs-lookup"><span data-stu-id="08f9c-139">Advanced filters use the logical operator AND or OR, and accept one or two conditions, each with their own operator and value.</span></span> <span data-ttu-id="08f9c-140">Le condizioni supportate sono:</span><span class="sxs-lookup"><span data-stu-id="08f9c-140">Supported conditions are:</span></span>

* <span data-ttu-id="08f9c-141">None</span><span class="sxs-lookup"><span data-stu-id="08f9c-141">None</span></span>
* <span data-ttu-id="08f9c-142">LessThan</span><span class="sxs-lookup"><span data-stu-id="08f9c-142">LessThan</span></span>
* <span data-ttu-id="08f9c-143">LessThanOrEqual</span><span class="sxs-lookup"><span data-stu-id="08f9c-143">LessThanOrEqual</span></span>
* <span data-ttu-id="08f9c-144">GreaterThan</span><span class="sxs-lookup"><span data-stu-id="08f9c-144">GreaterThan</span></span>
* <span data-ttu-id="08f9c-145">GreaterThanOrEqual</span><span class="sxs-lookup"><span data-stu-id="08f9c-145">GreaterThanOrEqual</span></span>
* <span data-ttu-id="08f9c-146">Contiene</span><span class="sxs-lookup"><span data-stu-id="08f9c-146">Contains</span></span>
* <span data-ttu-id="08f9c-147">DoesNotContain</span><span class="sxs-lookup"><span data-stu-id="08f9c-147">DoesNotContain</span></span>
* <span data-ttu-id="08f9c-148">StartsWith</span><span class="sxs-lookup"><span data-stu-id="08f9c-148">StartsWith</span></span>
* <span data-ttu-id="08f9c-149">DoesNotStartWith</span><span class="sxs-lookup"><span data-stu-id="08f9c-149">DoesNotStartWith</span></span>
* <span data-ttu-id="08f9c-150">Is</span><span class="sxs-lookup"><span data-stu-id="08f9c-150">Is</span></span>
* <span data-ttu-id="08f9c-151">IsNot</span><span class="sxs-lookup"><span data-stu-id="08f9c-151">IsNot</span></span>
* <span data-ttu-id="08f9c-152">IsBlank</span><span class="sxs-lookup"><span data-stu-id="08f9c-152">IsBlank</span></span>
* <span data-ttu-id="08f9c-153">IsNotBlank</span><span class="sxs-lookup"><span data-stu-id="08f9c-153">IsNotBlank</span></span>

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
[<span data-ttu-id="08f9c-154">Altre informazioni sui filtri</span><span class="sxs-lookup"><span data-stu-id="08f9c-154">Learn more about filtering</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Filters)

### <a name="handling-events"></a><span data-ttu-id="08f9c-155">Gestione degli eventi</span><span class="sxs-lookup"><span data-stu-id="08f9c-155">Handling events</span></span>
<span data-ttu-id="08f9c-156">Oltre a inviare informazioni all'iframe, l'applicazione può anche ricevere informazioni sugli eventi seguenti provenienti dall'iframe:</span><span class="sxs-lookup"><span data-stu-id="08f9c-156">In addition to sending information into the iframe, your application can also receive information on the following events coming from the iframe:</span></span>

* <span data-ttu-id="08f9c-157">Embed</span><span class="sxs-lookup"><span data-stu-id="08f9c-157">Embed</span></span>
  * <span data-ttu-id="08f9c-158">loaded</span><span class="sxs-lookup"><span data-stu-id="08f9c-158">loaded</span></span>
  * <span data-ttu-id="08f9c-159">error</span><span class="sxs-lookup"><span data-stu-id="08f9c-159">error</span></span>
* <span data-ttu-id="08f9c-160">Report</span><span class="sxs-lookup"><span data-stu-id="08f9c-160">Reports</span></span>
  * <span data-ttu-id="08f9c-161">pageChanged</span><span class="sxs-lookup"><span data-stu-id="08f9c-161">pageChanged</span></span>
  * <span data-ttu-id="08f9c-162">dataSelected (presto disponibile)</span><span class="sxs-lookup"><span data-stu-id="08f9c-162">dataSelected (coming soon)</span></span>

[<span data-ttu-id="08f9c-163">Altre informazioni sulla gestione degli eventi</span><span class="sxs-lookup"><span data-stu-id="08f9c-163">Learn more about handling events</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Handling-Events)

## <a name="next-steps"></a><span data-ttu-id="08f9c-164">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="08f9c-164">Next steps</span></span>
<span data-ttu-id="08f9c-165">Per altre informazioni sull'API JavaScript per Power BI, vedere i collegamenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="08f9c-165">For more information about the Power BI JavaScript API, check out the following links:</span></span>

* [<span data-ttu-id="08f9c-166">JavaScript API Wiki (Wiki sull'API JavaScript)</span><span class="sxs-lookup"><span data-stu-id="08f9c-166">JavaScript API Wiki</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki)
* [<span data-ttu-id="08f9c-167">Object model reference (Informazioni di riferimento sul modello a oggetti)</span><span class="sxs-lookup"><span data-stu-id="08f9c-167">Object model reference</span></span>](https://microsoft.github.io/powerbi-models/modules/_models_.html)
* <span data-ttu-id="08f9c-168">Esempi</span><span class="sxs-lookup"><span data-stu-id="08f9c-168">Samples</span></span>
  * [<span data-ttu-id="08f9c-169">Angular</span><span class="sxs-lookup"><span data-stu-id="08f9c-169">Angular</span></span>](http://azure-samples.github.io/powerbi-angular-client)
  * [<span data-ttu-id="08f9c-170">Ember</span><span class="sxs-lookup"><span data-stu-id="08f9c-170">Ember</span></span>](https://github.com/Microsoft/powerbi-ember)
* [<span data-ttu-id="08f9c-171">Live demo (Demo live)</span><span class="sxs-lookup"><span data-stu-id="08f9c-171">Live demo</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)

