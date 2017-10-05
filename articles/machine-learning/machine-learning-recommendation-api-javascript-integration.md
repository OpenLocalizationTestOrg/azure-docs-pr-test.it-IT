---
title: 'Raccomandazioni di Machine Learning: integrazione con JavaScript | Documentazione Microsoft'
description: Raccomandazioni di Azure Machine Learning - Integrazione con JavaScript - Documentazione
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: bbbb5bb6-489d-4a62-a2ae-f36237e9e2e1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: TRUE
ms.openlocfilehash: 8f27962d097bffc2a03de80244ae41d6573a4bf3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-machine-learning-recommendations---javascript-integration"></a><span data-ttu-id="d18fc-103">Raccomandazioni di Azure Machine Learning - Integrazione con JavaScript</span><span class="sxs-lookup"><span data-stu-id="d18fc-103">Azure Machine Learning Recommendations - JavaScript Integration</span></span>
> [!NOTE]
> <span data-ttu-id="d18fc-104">È consigliabile iniziare usando l'API Recommendations di Servizi cognitivi invece di questa versione.</span><span class="sxs-lookup"><span data-stu-id="d18fc-104">You should start using the Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="d18fc-105">Il Servizio cognitivo di Recommendations sostituirà questo servizio e verranno sviluppate nuove funzionalità.</span><span class="sxs-lookup"><span data-stu-id="d18fc-105">The Recommendations Cognitive Service will be replacing this service, and all the new features will be developed there.</span></span> <span data-ttu-id="d18fc-106">Il servizio include nuove funzionalità come il supporto in batch, una migliore funzione di Esplora API, una superficie API più pulita, un'esperienza più coerente in termini di iscrizione e fatturazione e così via.</span><span class="sxs-lookup"><span data-stu-id="d18fc-106">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="d18fc-107">Per altre informazioni, vedere [Migrating to the new Cognitive Service](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="d18fc-107">Learn more about [Migrating to the new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="d18fc-108">Questo documento illustra come integrare il sito usando JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d18fc-108">This document depict how to integrate your site using JavaScript.</span></span> <span data-ttu-id="d18fc-109">JavaScript consente di inviare eventi di acquisizione dei dati e utilizzare raccomandazioni dopo aver creato un modello di raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="d18fc-109">The JavaScript enables you to send Data Acquisition events and to consume recommendations once you build a recommendation model.</span></span> <span data-ttu-id="d18fc-110">Tutte le operazioni eseguite tramite JS possono essere eseguite anche dal lato server.</span><span class="sxs-lookup"><span data-stu-id="d18fc-110">All operations done via JS can be also done from server side.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a><span data-ttu-id="d18fc-111">1. Panoramica generale</span><span class="sxs-lookup"><span data-stu-id="d18fc-111">1. General Overview</span></span>
<span data-ttu-id="d18fc-112">L'integrazione del sito con Azure ML Recommendations si articola in 2 fasi:</span><span class="sxs-lookup"><span data-stu-id="d18fc-112">Integrating your site with Azure ML Recommendations consist on 2 Phases:</span></span>

1. <span data-ttu-id="d18fc-113">Invio di eventi ad Azure ML Recommendations.</span><span class="sxs-lookup"><span data-stu-id="d18fc-113">Send Events into Azure ML Recommendations.</span></span> <span data-ttu-id="d18fc-114">In tal modo verrà creato un modello di raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="d18fc-114">This will enable to build a recommendation model.</span></span>
2. <span data-ttu-id="d18fc-115">Utilizzo delle raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="d18fc-115">Consume the recommendations.</span></span> <span data-ttu-id="d18fc-116">Dopo aver creato il modello, è possibile utilizzare le raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="d18fc-116">After the model is built you can consume the recommendations.</span></span> <span data-ttu-id="d18fc-117">Questo documento non spiega come creare un modello. Per altre informazioni a riguardo, leggere la guida introduttiva.</span><span class="sxs-lookup"><span data-stu-id="d18fc-117">(This document does not explain how to build a model, read the quick start guide to get more information on how).</span></span>

<span data-ttu-id="d18fc-118"><ins>Fase I</ins></span><span class="sxs-lookup"><span data-stu-id="d18fc-118"><ins>Phase I</ins></span></span>

<span data-ttu-id="d18fc-119">Nella prima fase si inserisce nelle pagine HTML una piccola libreria JavaScript che consente l'invio di eventi nel momento in cui si verificano nella pagina HTML ai server di Azure ML Recommendations (tramite DataMarket):</span><span class="sxs-lookup"><span data-stu-id="d18fc-119">In the first phase you insert into your html pages a small JavaScript library that enables the page to send events as they occur on the html page into Azure ML Recommendations servers (via Data Market):</span></span>

![Drawing1][1]

<span data-ttu-id="d18fc-121"><ins>Fase II</ins></span><span class="sxs-lookup"><span data-stu-id="d18fc-121"><ins>Phase II</ins></span></span>

<span data-ttu-id="d18fc-122">Nella seconda fase, per visualizzare le raccomandazioni nella pagina si seleziona una delle opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="d18fc-122">In the second phase when you want to show the recommendations on the page you select one of the following options:</span></span>

<span data-ttu-id="d18fc-123">1. Il server (in fase di rendering della pagina) chiama il server di Azure ML Recommendations (tramite DataMarket) per ottenere le raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="d18fc-123">1.Your server (on the phase of page rendering) calls Azure ML Recommendations Server (via Data Market) to get recommendations.</span></span> <span data-ttu-id="d18fc-124">I risultati includono un elenco di ID di elementi.</span><span class="sxs-lookup"><span data-stu-id="d18fc-124">The results include a list of items id.</span></span> <span data-ttu-id="d18fc-125">Il server deve arricchire i risultati con i metadati degli elementi, ad esempio immagini e descrizione, e inviare la pagina creata al browser.</span><span class="sxs-lookup"><span data-stu-id="d18fc-125">Your server needs to enrich the results with the items Meta data (e.g. images, description) and send the created page to the browser.</span></span>

![Drawing2][2]

<span data-ttu-id="d18fc-127">2. L'altra opzione prevede di usare il piccolo file JavaScript della fase I per ottenere un semplice elenco degli elementi raccomandati.</span><span class="sxs-lookup"><span data-stu-id="d18fc-127">2.The other option is to use the small JavaScript file from phase one to get a simple list of recommended items.</span></span> <span data-ttu-id="d18fc-128">I dati ricevuti in questo caso sono più snelli rispetto a quelli che si ricevono utilizzando la prima opzione.</span><span class="sxs-lookup"><span data-stu-id="d18fc-128">The data received here is leaner than the one in the first option.</span></span>

![Drawing3][3]

## <a name="2-prerequisites"></a><span data-ttu-id="d18fc-130">2. Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d18fc-130">2. Prerequisites</span></span>
1. <span data-ttu-id="d18fc-131">Creare un nuovo modello usando le API.</span><span class="sxs-lookup"><span data-stu-id="d18fc-131">Create a new model using the APIs.</span></span> <span data-ttu-id="d18fc-132">Per istruzioni su come eseguire questa operazione, vedere la guida introduttiva.</span><span class="sxs-lookup"><span data-stu-id="d18fc-132">See the Quick start guide on how to do it.</span></span>
2. <span data-ttu-id="d18fc-133">Codificare &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; con codifica base64.</span><span class="sxs-lookup"><span data-stu-id="d18fc-133">Encode your &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; with base64.</span></span> <span data-ttu-id="d18fc-134">Questi dati verranno usati per l'autenticazione di base che consente al codice JS di chiamare le API.</span><span class="sxs-lookup"><span data-stu-id="d18fc-134">(This will be used for the basic authentication to enable the JS code to call the APIs).</span></span>

## <a name="3-send-data-acquisition-events-using-javascript"></a><span data-ttu-id="d18fc-135">3. Inviare eventi di acquisizione dei dati tramite JavaScript</span><span class="sxs-lookup"><span data-stu-id="d18fc-135">3. Send Data Acquisition events using JavaScript</span></span>
<span data-ttu-id="d18fc-136">Per inviare eventi in modo semplice, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="d18fc-136">The following steps facilitate sending events:</span></span>

1. <span data-ttu-id="d18fc-137">Includere la libreria JQuery nel codice.</span><span class="sxs-lookup"><span data-stu-id="d18fc-137">Include JQuery library in your code.</span></span> <span data-ttu-id="d18fc-138">È possibile scaricarla da nuget all'URL seguente.</span><span class="sxs-lookup"><span data-stu-id="d18fc-138">You can download it from nuget in the following URL.</span></span>
   
     <span data-ttu-id="d18fc-139">http://www.nuget.org/packages/jQuery/1.8.2</span><span class="sxs-lookup"><span data-stu-id="d18fc-139">http://www.nuget.org/packages/jQuery/1.8.2</span></span>
2. <span data-ttu-id="d18fc-140">Includere la libreria JavaScript di Recommendations disponibile all'URL seguente: http://aka.ms/RecoJSLib1</span><span class="sxs-lookup"><span data-stu-id="d18fc-140">Include the Recommendations Java Script library from the following URL: http://aka.ms/RecoJSLib1</span></span>
3. <span data-ttu-id="d18fc-141">Inizializzare la libreria di Azure ML Recommendations con i parametri appropriati.</span><span class="sxs-lookup"><span data-stu-id="d18fc-141">Initialize Azure ML Recommendations library with the appropriate parameters.</span></span>
   
     <span data-ttu-id="d18fc-142"><script> AzureMLRecommendationsStart("<base64encoding of username:key>", "<model_id>"); </script>
4. Inviare l'evento appropriato.</span><span class="sxs-lookup"><span data-stu-id="d18fc-142"><script> AzureMLRecommendationsStart("<base64encoding of username:key>", "<model_id>"); </script>
4. Send the appropriate event.</span></span> <span data-ttu-id="d18fc-143">Vedere la sezione dettagliata di seguito in merito a tutti i tipi di eventi, esempio di evento Click, <script> se (typeof AzureMLRecommendationsEvent = = "undefined") {</span><span class="sxs-lookup"><span data-stu-id="d18fc-143">See detailed section below on all type of events (example of click event)  <script> if (typeof AzureMLRecommendationsEvent=="undefined") {</span></span>         
                     <span data-ttu-id="d18fc-144">AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({ event: "click", item: "18321116" }); </script></span><span class="sxs-lookup"><span data-stu-id="d18fc-144">AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({ event: "click", item: "18321116" }); </script></span></span>

### <a name="31----limitations-and-browser-support"></a><span data-ttu-id="d18fc-145">3.1.</span><span class="sxs-lookup"><span data-stu-id="d18fc-145">3.1.</span></span>    <span data-ttu-id="d18fc-146">Limitazioni e supporto browser</span><span class="sxs-lookup"><span data-stu-id="d18fc-146">Limitations and Browser Support</span></span>
<span data-ttu-id="d18fc-147">Di seguito viene fornita un'implementazione di riferimento così com'è.</span><span class="sxs-lookup"><span data-stu-id="d18fc-147">This is a reference implementation and it is given as is.</span></span> <span data-ttu-id="d18fc-148">Tutti i principali browser dovrebbero essere supportati.</span><span class="sxs-lookup"><span data-stu-id="d18fc-148">It should support all major browsers.</span></span>

### <a name="32----type-of-events"></a><span data-ttu-id="d18fc-149">3.2.</span><span class="sxs-lookup"><span data-stu-id="d18fc-149">3.2.</span></span>    <span data-ttu-id="d18fc-150">Tipi di eventi</span><span class="sxs-lookup"><span data-stu-id="d18fc-150">Type of Events</span></span>
<span data-ttu-id="d18fc-151">La libreria supporta 5 tipi di eventi: Click, Recommendation Click, Add to Shop Cart, Remove from Shop Cart e Purchase.</span><span class="sxs-lookup"><span data-stu-id="d18fc-151">There are 5 types of event that the library supports: Click, Recommendation Click, Add to Shop Cart, Remove from Shop Cart and Purchase.</span></span> <span data-ttu-id="d18fc-152">Esiste un evento aggiuntivo, denominato Login, che viene usato per impostare il contesto dell'utente.</span><span class="sxs-lookup"><span data-stu-id="d18fc-152">There is an additional event that is used to set the user context called Login.</span></span>

#### <a name="321-click-event"></a><span data-ttu-id="d18fc-153">3.2.1.</span><span class="sxs-lookup"><span data-stu-id="d18fc-153">3.2.1.</span></span> <span data-ttu-id="d18fc-154">Evento Click</span><span class="sxs-lookup"><span data-stu-id="d18fc-154">Click Event</span></span>
<span data-ttu-id="d18fc-155">Questo evento deve essere usato ogni volta che un utente fa clic su un elemento.</span><span class="sxs-lookup"><span data-stu-id="d18fc-155">This event should be used any time a user clicked on an item.</span></span> <span data-ttu-id="d18fc-156">In genere, quando un utente fa clic su un elemento, si apre una nuova pagina contenente i dettagli dell'elemento dove l'evento deve essere attivato.</span><span class="sxs-lookup"><span data-stu-id="d18fc-156">Usually when user clicks on an item a new page is opened with the item details; in this page this event should be triggered.</span></span>

<span data-ttu-id="d18fc-157">Parametri</span><span class="sxs-lookup"><span data-stu-id="d18fc-157">Parameters:</span></span>

* <span data-ttu-id="d18fc-158">event (stringa, obbligatorio) - "click"</span><span class="sxs-lookup"><span data-stu-id="d18fc-158">event (string, mandatory) - “click”</span></span>
* <span data-ttu-id="d18fc-159">item (stringa, obbligatorio) - identificatore univoco dell'elemento</span><span class="sxs-lookup"><span data-stu-id="d18fc-159">item (string, mandatory) - Unique identifier of the item</span></span>
* <span data-ttu-id="d18fc-160">itemName (stringa, facoltativo) - nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="d18fc-160">itemName (string, optional) - the name of the item</span></span>
* <span data-ttu-id="d18fc-161">itemDescription (stringa, facoltativo) - descrizione dell'elemento</span><span class="sxs-lookup"><span data-stu-id="d18fc-161">itemDescription (string, optional) - the description of the item</span></span>
* <span data-ttu-id="d18fc-162">itemCategory (stringa, facoltativo) - categoria dell'elemento</span><span class="sxs-lookup"><span data-stu-id="d18fc-162">itemCategory (string, optional) - the category of the item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "click", item: "3111718" });
        </script>

<span data-ttu-id="d18fc-163">In alternativa, con dati facoltativi:</span><span class="sxs-lookup"><span data-stu-id="d18fc-163">Or with optional data:</span></span>

        <script>
            if (typeof AzureMLRecommendationsEvent === "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "click", item: "3111718", itemName: "Plane", itemDescription: "It is a big plane", itemCategory: "Aviation"});
        </script>


#### <a name="322-recommendation-click-event"></a><span data-ttu-id="d18fc-164">3.2.2.</span><span class="sxs-lookup"><span data-stu-id="d18fc-164">3.2.2.</span></span> <span data-ttu-id="d18fc-165">Evento Recommendation Click</span><span class="sxs-lookup"><span data-stu-id="d18fc-165">Recommendation Click Event</span></span>
<span data-ttu-id="d18fc-166">Questo evento deve essere usato ogni volta che un utente fa clic su un elemento ricevuto da Azure ML Recommendations come elemento raccomandato.</span><span class="sxs-lookup"><span data-stu-id="d18fc-166">This event should be used any time a user clicked on an item that was received from Azure ML Recommendations as a recommended item.</span></span> <span data-ttu-id="d18fc-167">In genere, quando un utente fa clic su un elemento, si apre una nuova pagina contenente i dettagli dell'elemento dove l'evento deve essere attivato.</span><span class="sxs-lookup"><span data-stu-id="d18fc-167">Usually when user clicks on an item a new page is opened with the item details; in this page this event should be triggered.</span></span>

<span data-ttu-id="d18fc-168">Parametri</span><span class="sxs-lookup"><span data-stu-id="d18fc-168">Parameters:</span></span>

* <span data-ttu-id="d18fc-169">event (stringa, obbligatorio) - "recommendationclick"</span><span class="sxs-lookup"><span data-stu-id="d18fc-169">event (string, mandatory) - “recommendationclick”</span></span>
* <span data-ttu-id="d18fc-170">item (stringa, obbligatorio) - identificatore univoco dell'elemento</span><span class="sxs-lookup"><span data-stu-id="d18fc-170">item (string, mandatory) - Unique identifier of the item</span></span>
* <span data-ttu-id="d18fc-171">itemName (stringa, facoltativo) - nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="d18fc-171">itemName (string, optional) - the name of the item</span></span>
* <span data-ttu-id="d18fc-172">itemDescription (stringa, facoltativo) - descrizione dell'elemento</span><span class="sxs-lookup"><span data-stu-id="d18fc-172">itemDescription (string, optional) - the description of the item</span></span>
* <span data-ttu-id="d18fc-173">itemCategory (stringa, facoltativo) - categoria dell'elemento</span><span class="sxs-lookup"><span data-stu-id="d18fc-173">itemCategory (string, optional) - the category of the item</span></span>
* <span data-ttu-id="d18fc-174">seeds (matrice di stringhe, facoltativo) - semi che hanno generato la query di raccomandazione</span><span class="sxs-lookup"><span data-stu-id="d18fc-174">seeds (string array, optional) - the seeds that generated the recommendation query.</span></span>
* <span data-ttu-id="d18fc-175">recoList (matrice di stringhe, facoltativo) - il risultato della richiesta di raccomandazione che ha generato l'elemento selezionato</span><span class="sxs-lookup"><span data-stu-id="d18fc-175">recoList (string array, optional) - the result of the recommendation request that generated the item that was clicked.</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "recommendationclick", item: "18899918" });
        </script>

<span data-ttu-id="d18fc-176">In alternativa, con dati facoltativi:</span><span class="sxs-lookup"><span data-stu-id="d18fc-176">Or with optional data:</span></span>

        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: eventName, item: "198", itemName: "Plane2", itemDescription: "It is a big plane2", itemCategory: "Default2", seeds: ["Seed1", "Seed2"], recoList: ["199", "198", "197"]                 });
        </script>


#### <a name="323-add-shopping-cart-event"></a><span data-ttu-id="d18fc-177">3.2.3.</span><span class="sxs-lookup"><span data-stu-id="d18fc-177">3.2.3.</span></span> <span data-ttu-id="d18fc-178">Evento Add Shopping Cart</span><span class="sxs-lookup"><span data-stu-id="d18fc-178">Add Shopping Cart Event</span></span>
<span data-ttu-id="d18fc-179">Questo evento deve essere usato quando l'utente aggiunge un elemento al carrello acquisti.</span><span class="sxs-lookup"><span data-stu-id="d18fc-179">This event should be used when the user add an item to the shopping cart.</span></span>
<span data-ttu-id="d18fc-180">Parametri</span><span class="sxs-lookup"><span data-stu-id="d18fc-180">Parameters:</span></span>

* <span data-ttu-id="d18fc-181">event (stringa, obbligatorio) - "addshopcart"</span><span class="sxs-lookup"><span data-stu-id="d18fc-181">event (string, mandatory) - “addshopcart”</span></span>
* <span data-ttu-id="d18fc-182">item (stringa, obbligatorio) - identificatore univoco dell'elemento</span><span class="sxs-lookup"><span data-stu-id="d18fc-182">item (string, mandatory) - Unique identifier of the item</span></span>
* <span data-ttu-id="d18fc-183">itemName (stringa, facoltativo) - nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="d18fc-183">itemName (string, optional) - the name of the item</span></span>
* <span data-ttu-id="d18fc-184">itemDescription (stringa, facoltativo) - descrizione dell'elemento</span><span class="sxs-lookup"><span data-stu-id="d18fc-184">itemDescription (string, optional) - the description of the item</span></span>
* <span data-ttu-id="d18fc-185">itemCategory (stringa, facoltativo) - categoria dell'elemento</span><span class="sxs-lookup"><span data-stu-id="d18fc-185">itemCategory (string, optional) - the category of the item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "addshopcart", item: "13221118" });
        </script>

#### <a name="324-remove-shopping-cart-event"></a><span data-ttu-id="d18fc-186">3.2.4.</span><span class="sxs-lookup"><span data-stu-id="d18fc-186">3.2.4.</span></span> <span data-ttu-id="d18fc-187">Evento Remove Shopping Cart</span><span class="sxs-lookup"><span data-stu-id="d18fc-187">Remove Shopping Cart Event</span></span>
<span data-ttu-id="d18fc-188">Questo evento deve essere usato quando l'utente rimuove un elemento dal carrello acquisti.</span><span class="sxs-lookup"><span data-stu-id="d18fc-188">This event should be used when the user removes an item to the shopping cart.</span></span>

<span data-ttu-id="d18fc-189">Parametri</span><span class="sxs-lookup"><span data-stu-id="d18fc-189">Parameters:</span></span>

* <span data-ttu-id="d18fc-190">event (stringa, obbligatorio) - "removeshopcart"</span><span class="sxs-lookup"><span data-stu-id="d18fc-190">event (string, mandatory) - “removeshopcart”</span></span>
* <span data-ttu-id="d18fc-191">item (stringa, obbligatorio) - identificatore univoco dell'elemento</span><span class="sxs-lookup"><span data-stu-id="d18fc-191">item (string, mandatory) - Unique identifier of the item</span></span>
* <span data-ttu-id="d18fc-192">itemName (stringa, facoltativo) - nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="d18fc-192">itemName (string, optional) - the name of the item</span></span>
* <span data-ttu-id="d18fc-193">itemDescription (stringa, facoltativo) - descrizione dell'elemento</span><span class="sxs-lookup"><span data-stu-id="d18fc-193">itemDescription (string, optional) - the description of the item</span></span>
* <span data-ttu-id="d18fc-194">itemCategory (stringa, facoltativo) - categoria dell'elemento</span><span class="sxs-lookup"><span data-stu-id="d18fc-194">itemCategory (string, optional) - the category of the item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "removeshopcart", item: "111118" });
        </script>

#### <a name="325-purchase-event"></a><span data-ttu-id="d18fc-195">3.2.5.</span><span class="sxs-lookup"><span data-stu-id="d18fc-195">3.2.5.</span></span> <span data-ttu-id="d18fc-196">Evento Purchase</span><span class="sxs-lookup"><span data-stu-id="d18fc-196">Purchase Event</span></span>
<span data-ttu-id="d18fc-197">Questo evento deve essere usato quando l'utente ha acquistato gli elementi nel carrello.</span><span class="sxs-lookup"><span data-stu-id="d18fc-197">This event should be used when the user purchased his shopping cart.</span></span>

<span data-ttu-id="d18fc-198">Parametri</span><span class="sxs-lookup"><span data-stu-id="d18fc-198">Parameters:</span></span>

* <span data-ttu-id="d18fc-199">event (stringa) - "purchase"</span><span class="sxs-lookup"><span data-stu-id="d18fc-199">event (string) - “purchase”</span></span>
* <span data-ttu-id="d18fc-200">items (acquistati) - matrice contenente una voce per ogni elemento acquistato</span><span class="sxs-lookup"><span data-stu-id="d18fc-200">items ( Purchased[] ) - Array holding an entry for each item purchased.</span></span><br><br>
  <span data-ttu-id="d18fc-201">Formato elementi acquistati:</span><span class="sxs-lookup"><span data-stu-id="d18fc-201">Purchased format:</span></span>
  * <span data-ttu-id="d18fc-202">item (stringa) - identificatore univoco dell'elemento.</span><span class="sxs-lookup"><span data-stu-id="d18fc-202">item (string) - Unique identifier of the item.</span></span>
  * <span data-ttu-id="d18fc-203">count (numero intero o stringa) - numero di elementi che sono stati acquistati</span><span class="sxs-lookup"><span data-stu-id="d18fc-203">count (int or string) - number of items that were purchased.</span></span>
  * <span data-ttu-id="d18fc-204">price (float o stringa) - campo facoltativo - prezzo dell'elemento</span><span class="sxs-lookup"><span data-stu-id="d18fc-204">price (float or string) - optional field - the price of the item.</span></span>

<span data-ttu-id="d18fc-205">L'esempio seguente illustra l'acquisto di 3 elementi (33, 34, 35), di cui due con tutti i campi popolati (item, count, price) e uno (item 34) privo di prezzo.</span><span class="sxs-lookup"><span data-stu-id="d18fc-205">The example below shows purchase of 3 items (33, 34, 35), two with all fields populated (item, count, price) and one (item 34) without a price.</span></span>

        <script>
            if ( typeof AzureMLRecommendationsEvent == "undefined"){ AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "purchase", items: [{ item: "33", count: "1", price: "10" }, { item: "34", count: "2" }, { item: "35", count: "1", price: "210" }] });
        </script>

#### <a name="326-user-login-event"></a><span data-ttu-id="d18fc-206">3.2.6.</span><span class="sxs-lookup"><span data-stu-id="d18fc-206">3.2.6.</span></span> <span data-ttu-id="d18fc-207">Evento User Login</span><span class="sxs-lookup"><span data-stu-id="d18fc-207">User Login Event</span></span>
<span data-ttu-id="d18fc-208">La libreria degli eventi di Azure ML Recommendations crea e usa un cookie per identificare gli eventi che provengono dallo stesso browser.</span><span class="sxs-lookup"><span data-stu-id="d18fc-208">Azure ML Recommendations Event library creates and use a cookie in order to identify events that came from the same browser.</span></span> <span data-ttu-id="d18fc-209">Per migliorare i risultati del modello, Azure ML Recommendations consente di impostare un'identificazione univoca dell'utente che sostituirà l'utilizzo del cookie.</span><span class="sxs-lookup"><span data-stu-id="d18fc-209">In order to improve the model results Azure ML Recommendations enables to set a user unique identification that will override the cookie usage.</span></span>

<span data-ttu-id="d18fc-210">Questo evento deve essere usato dopo l'accesso dell'utente al sito.</span><span class="sxs-lookup"><span data-stu-id="d18fc-210">This event should be used after the user login to your site.</span></span>

<span data-ttu-id="d18fc-211">Parametri</span><span class="sxs-lookup"><span data-stu-id="d18fc-211">Parameters:</span></span>

* <span data-ttu-id="d18fc-212">event (stringa) - "userlogin"</span><span class="sxs-lookup"><span data-stu-id="d18fc-212">event (string) - “userlogin”</span></span>
* <span data-ttu-id="d18fc-213">user (stringa) - identificazione univoca dell'utente</span><span class="sxs-lookup"><span data-stu-id="d18fc-213">user (string) - unique identification of the user.</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "userlogin", user: “ABCD10AA” });
        </script>

## <a name="4-consume-recommendations-via-javascript"></a><span data-ttu-id="d18fc-214">4. Utilizzare le raccomandazioni tramite JavaScript</span><span class="sxs-lookup"><span data-stu-id="d18fc-214">4. Consume Recommendations via JavaScript</span></span>
<span data-ttu-id="d18fc-215">Il codice che utilizza la raccomandazione viene attivato da alcuni eventi JavaScript nella pagina Web del client.</span><span class="sxs-lookup"><span data-stu-id="d18fc-215">The code that consumes the recommendation is triggered by some JavaScript event by the client’s webpage.</span></span> <span data-ttu-id="d18fc-216">Le risposta alla raccomandazione include gli ID degli elementi raccomandati con i relativi nomi e valutazioni.</span><span class="sxs-lookup"><span data-stu-id="d18fc-216">The recommendation response includes the recommended items Ids, their names and their ratings.</span></span> <span data-ttu-id="d18fc-217">È preferibile usare questa opzione solo per la visualizzazione di un elenco degli elementi consigliati. Le attività di gestione più complesse, ad esempio l'aggiunta dei metadati dell'elemento, devono essere eseguite sull'integrazione lato server.</span><span class="sxs-lookup"><span data-stu-id="d18fc-217">It’s best to use this option only for a list display of the recommended items - more complex handling (such as adding the item’s metadata) should be done on the server side integration.</span></span>

### <a name="41-consume-recommendations"></a><span data-ttu-id="d18fc-218">4.1 Utilizzare le raccomandazioni</span><span class="sxs-lookup"><span data-stu-id="d18fc-218">4.1 Consume Recommendations</span></span>
<span data-ttu-id="d18fc-219">Per utilizzare le raccomandazioni, è necessario includere nella pagina le librerie JavaScript obbligatorie e chiamare AzureMLRecommendationsStart.</span><span class="sxs-lookup"><span data-stu-id="d18fc-219">To consume recommendations you need to include the required JavaScript libraries in your page and to call AzureMLRecommendationsStart.</span></span> <span data-ttu-id="d18fc-220">Vedere la sezione 2.</span><span class="sxs-lookup"><span data-stu-id="d18fc-220">See section 2.</span></span>

<span data-ttu-id="d18fc-221">Per utilizzare le raccomandazioni per uno o più elementi, è necessario chiamare un metodo denominato AzureMLRecommendationsGetI2IRecommendation.</span><span class="sxs-lookup"><span data-stu-id="d18fc-221">To consume recommendations for one or more items you need to call a method called: AzureMLRecommendationsGetI2IRecommendation.</span></span>

<span data-ttu-id="d18fc-222">Parametri</span><span class="sxs-lookup"><span data-stu-id="d18fc-222">Parameters:</span></span>

* <span data-ttu-id="d18fc-223">items (matrice di stringhe) - uno o più elementi per i quali ottenere le raccomandazioni</span><span class="sxs-lookup"><span data-stu-id="d18fc-223">items (array of strings) - One or more items to get recommendations for.</span></span> <span data-ttu-id="d18fc-224">Se si usa una build Fbt, qui sarà possibile impostare un solo elemento.</span><span class="sxs-lookup"><span data-stu-id="d18fc-224">If you consume an Fbt build then you can set here only one item.</span></span>
* <span data-ttu-id="d18fc-225">numberOfResults (numero intero) - numero dei risultati richiesti</span><span class="sxs-lookup"><span data-stu-id="d18fc-225">numberOfResults (int) - number of required results.</span></span>
* <span data-ttu-id="d18fc-226">includeMetadata (booleano, facoltativo) - se impostato su 'true' indica che il campo di metadati deve essere popolato nel risultato</span><span class="sxs-lookup"><span data-stu-id="d18fc-226">includeMetadata (boolean, optional) - if set to ‘true’ indicates that the metadata field must be populated in the result.</span></span>
* <span data-ttu-id="d18fc-227">Funzione di elaborazione - una funzione che gestirà le raccomandazioni restituite</span><span class="sxs-lookup"><span data-stu-id="d18fc-227">Processing function - a function that will handle the recommendations returned.</span></span> <span data-ttu-id="d18fc-228">I dati vengono restituiti come matrice di:</span><span class="sxs-lookup"><span data-stu-id="d18fc-228">The data is returned as an array of:</span></span>
  * <span data-ttu-id="d18fc-229">Item - ID univoco dell'elemento</span><span class="sxs-lookup"><span data-stu-id="d18fc-229">Item - item unique id</span></span>
  * <span data-ttu-id="d18fc-230">name - nome dell'elemento (se esiste nel catalogo)</span><span class="sxs-lookup"><span data-stu-id="d18fc-230">name - item name (if exist in catalog)</span></span>
  * <span data-ttu-id="d18fc-231">rating - valutazione della raccomandazione</span><span class="sxs-lookup"><span data-stu-id="d18fc-231">rating - recommendation rating</span></span>
  * <span data-ttu-id="d18fc-232">metadata - stringa che rappresenta i metadati dell'elemento</span><span class="sxs-lookup"><span data-stu-id="d18fc-232">metadata - a string that represents the metadata of the item</span></span>

<span data-ttu-id="d18fc-233">Esempio: il codice seguente richiede 8 raccomandazioni per l'elemento "64f6eb0d-947a-4c18-a16c-888da9e228ba" e, poiché il parametro includeMetadata non è specificato, è implicito che i metadati non sono obbligatori. I risultati vengono quindi concatenati in un buffer.</span><span class="sxs-lookup"><span data-stu-id="d18fc-233">Example: The following code requests 8 recommendations for item "64f6eb0d-947a-4c18-a16c-888da9e228ba" (and by not specifying includeMetadata - it implicitly says that no metadata is required), it then concatenate the results into a buffer.</span></span>

        <script>
             var reco = AzureMLRecommendationsGetI2IRecommendation(["64f6eb0d-947a-4c18-a16c-888da9e228ba"], 8, false, function (reco) {
                 var buff = "";
                 for (var ii = 0; ii < reco.length; ii++) {
                       buff += reco[ii].item + "," + reco[ii].name + "," + reco[ii].rating + "\n";
                 }
                 alert(buff);
            });
        </script>


[1]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing1.png
[2]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing2.png
[3]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing3.png
