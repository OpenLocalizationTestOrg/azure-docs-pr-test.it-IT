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
redirect_document_id: True
ms.openlocfilehash: 4c5f0eee4aa04ce823321d52985374c52850f0d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-recommendations---javascript-integration"></a><span data-ttu-id="7a001-103">Raccomandazioni di Azure Machine Learning - Integrazione con JavaScript</span><span class="sxs-lookup"><span data-stu-id="7a001-103">Azure Machine Learning Recommendations - JavaScript Integration</span></span>
> [!NOTE]
> <span data-ttu-id="7a001-104">È consigliabile iniziare utilizzando hello indicazioni API cognitivi servizio invece di questa versione.</span><span class="sxs-lookup"><span data-stu-id="7a001-104">You should start using hello Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="7a001-105">Hello servizio cognitivi indicazioni andrà a sostituire questo servizio e tutte le nuove funzionalità hello verranno sviluppate non esiste.</span><span class="sxs-lookup"><span data-stu-id="7a001-105">hello Recommendations Cognitive Service will be replacing this service, and all hello new features will be developed there.</span></span> <span data-ttu-id="7a001-106">Il servizio include nuove funzionalità come il supporto in batch, una migliore funzione di Esplora API, una superficie API più pulita, un'esperienza più coerente in termini di iscrizione e fatturazione e così via.</span><span class="sxs-lookup"><span data-stu-id="7a001-106">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="7a001-107">Altre informazioni, vedere [toohello migrazione nuovo servizio cognitivi](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="7a001-107">Learn more about [Migrating toohello new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="7a001-108">Questo documento illustrano come toointegrate del sito utilizzando JavaScript.</span><span class="sxs-lookup"><span data-stu-id="7a001-108">This document depict how toointegrate your site using JavaScript.</span></span> <span data-ttu-id="7a001-109">Hello JavaScript consente toosend gli eventi di acquisizione dei dati e indicazioni tooconsume dopo aver creato un modello di raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="7a001-109">hello JavaScript enables you toosend Data Acquisition events and tooconsume recommendations once you build a recommendation model.</span></span> <span data-ttu-id="7a001-110">Tutte le operazioni eseguite tramite JS possono essere eseguite anche dal lato server.</span><span class="sxs-lookup"><span data-stu-id="7a001-110">All operations done via JS can be also done from server side.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a><span data-ttu-id="7a001-111">1. Panoramica generale</span><span class="sxs-lookup"><span data-stu-id="7a001-111">1. General Overview</span></span>
<span data-ttu-id="7a001-112">L'integrazione del sito con Azure ML Recommendations si articola in 2 fasi:</span><span class="sxs-lookup"><span data-stu-id="7a001-112">Integrating your site with Azure ML Recommendations consist on 2 Phases:</span></span>

1. <span data-ttu-id="7a001-113">Invio di eventi ad Azure ML Recommendations.</span><span class="sxs-lookup"><span data-stu-id="7a001-113">Send Events into Azure ML Recommendations.</span></span> <span data-ttu-id="7a001-114">In questo modo toobuild un modello di raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="7a001-114">This will enable toobuild a recommendation model.</span></span>
2. <span data-ttu-id="7a001-115">Utilizzare indicazioni hello.</span><span class="sxs-lookup"><span data-stu-id="7a001-115">Consume hello recommendations.</span></span> <span data-ttu-id="7a001-116">Una volta creato il modello di hello è possibile utilizzare indicazioni hello.</span><span class="sxs-lookup"><span data-stu-id="7a001-116">After hello model is built you can consume hello recommendations.</span></span> <span data-ttu-id="7a001-117">(Questo documento vengono descritte le modalità toobuild un modello, leggere hello tooget Guida introduttiva ulteriori informazioni su come).</span><span class="sxs-lookup"><span data-stu-id="7a001-117">(This document does not explain how toobuild a model, read hello quick start guide tooget more information on how).</span></span>

<span data-ttu-id="7a001-118"><ins>Fase I</ins></span><span class="sxs-lookup"><span data-stu-id="7a001-118"><ins>Phase I</ins></span></span>

<span data-ttu-id="7a001-119">In hello prima fase di che nelle pagine html si inserisce una piccola libreria JavaScript che consente hello eventi toosend pagina che si verificano nella pagina html hello nei server di Azure ML raccomandazioni (tramite Data Market):</span><span class="sxs-lookup"><span data-stu-id="7a001-119">In hello first phase you insert into your html pages a small JavaScript library that enables hello page toosend events as they occur on hello html page into Azure ML Recommendations servers (via Data Market):</span></span>

![Drawing1][1]

<span data-ttu-id="7a001-121"><ins>Fase II</ins></span><span class="sxs-lookup"><span data-stu-id="7a001-121"><ins>Phase II</ins></span></span>

<span data-ttu-id="7a001-122">In hello seconda fase, quando si desidera consigli hello tooshow pagina hello selezionare una delle seguenti opzioni hello:</span><span class="sxs-lookup"><span data-stu-id="7a001-122">In hello second phase when you want tooshow hello recommendations on hello page you select one of hello following options:</span></span>

<span data-ttu-id="7a001-123">1. il server (in fase di hello del rendering della pagina) chiama indicazioni tooget Azure ML indicazioni Server (tramite Data Market).</span><span class="sxs-lookup"><span data-stu-id="7a001-123">1.Your server (on hello phase of page rendering) calls Azure ML Recommendations Server (via Data Market) tooget recommendations.</span></span> <span data-ttu-id="7a001-124">risultati di Hello includono un elenco di id degli elementi. Il server deve risultati hello tooenrich con gli elementi di hello metadati (ad esempio immagini, descrizione) e inviare hello creato pagina toohello browser.</span><span class="sxs-lookup"><span data-stu-id="7a001-124">hello results include a list of items id. Your server needs tooenrich hello results with hello items Meta data (e.g. images, description) and send hello created page toohello browser.</span></span>

![Drawing2][2]

<span data-ttu-id="7a001-126">2. hello è toouse hello JavaScript file di piccole dimensioni da una tooget fase un semplice elenco di elementi consigliati.</span><span class="sxs-lookup"><span data-stu-id="7a001-126">2.hello other option is toouse hello small JavaScript file from phase one tooget a simple list of recommended items.</span></span> <span data-ttu-id="7a001-127">dati Hello qui ricevuti sono più snelli di hello prima opzione hello.</span><span class="sxs-lookup"><span data-stu-id="7a001-127">hello data received here is leaner than hello one in hello first option.</span></span>

![Drawing3][3]

## <a name="2-prerequisites"></a><span data-ttu-id="7a001-129">2. Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7a001-129">2. Prerequisites</span></span>
1. <span data-ttu-id="7a001-130">Creare un nuovo modello utilizzando le API di hello.</span><span class="sxs-lookup"><span data-stu-id="7a001-130">Create a new model using hello APIs.</span></span> <span data-ttu-id="7a001-131">Vedere la Guida introduttiva di hello sul toodo è.</span><span class="sxs-lookup"><span data-stu-id="7a001-131">See hello Quick start guide on how toodo it.</span></span>
2. <span data-ttu-id="7a001-132">Codificare &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; con codifica base64.</span><span class="sxs-lookup"><span data-stu-id="7a001-132">Encode your &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; with base64.</span></span> <span data-ttu-id="7a001-133">(Questo verrà utilizzato per hello l'autenticazione di base tooenable hello JS codice toocall hello API).</span><span class="sxs-lookup"><span data-stu-id="7a001-133">(This will be used for hello basic authentication tooenable hello JS code toocall hello APIs).</span></span>

## <a name="3-send-data-acquisition-events-using-javascript"></a><span data-ttu-id="7a001-134">3. Inviare eventi di acquisizione dei dati tramite JavaScript</span><span class="sxs-lookup"><span data-stu-id="7a001-134">3. Send Data Acquisition events using JavaScript</span></span>
<span data-ttu-id="7a001-135">Hello passaggi facilitare l'invio di eventi:</span><span class="sxs-lookup"><span data-stu-id="7a001-135">hello following steps facilitate sending events:</span></span>

1. <span data-ttu-id="7a001-136">Includere la libreria JQuery nel codice.</span><span class="sxs-lookup"><span data-stu-id="7a001-136">Include JQuery library in your code.</span></span> <span data-ttu-id="7a001-137">È possibile scaricarlo da nuget in hello URL seguente.</span><span class="sxs-lookup"><span data-stu-id="7a001-137">You can download it from nuget in hello following URL.</span></span>
   
     <span data-ttu-id="7a001-138">http://www.nuget.org/packages/jQuery/1.8.2</span><span class="sxs-lookup"><span data-stu-id="7a001-138">http://www.nuget.org/packages/jQuery/1.8.2</span></span>
2. <span data-ttu-id="7a001-139">Libreria Script Java indicazioni hello dal seguente URL hello includono: http://aka.ms/RecoJSLib1</span><span class="sxs-lookup"><span data-stu-id="7a001-139">Include hello Recommendations Java Script library from hello following URL: http://aka.ms/RecoJSLib1</span></span>
3. <span data-ttu-id="7a001-140">Inizializzare la libreria di Azure ML indicazioni con i parametri appropriati hello.</span><span class="sxs-lookup"><span data-stu-id="7a001-140">Initialize Azure ML Recommendations library with hello appropriate parameters.</span></span>
   
     <span data-ttu-id="7a001-141"><script>AzureMLRecommendationsStart ("<base64encoding of username:key>", "< model_id >"); </script> 
4. Eventi di trasmissione hello appropriato.</span><span class="sxs-lookup"><span data-stu-id="7a001-141"><script> AzureMLRecommendationsStart("<base64encoding of username:key>", "<model_id>"); </script>
4. Send hello appropriate event.</span></span> <span data-ttu-id="7a001-142">Vedere la sezione dettagliata di seguito in merito a tutti i tipi di eventi, esempio di evento Click, <script> se (typeof AzureMLRecommendationsEvent = = "undefined") {</span><span class="sxs-lookup"><span data-stu-id="7a001-142">See detailed section below on all type of events (example of click event)  <script> if (typeof AzureMLRecommendationsEvent=="undefined") {</span></span>         
                     <span data-ttu-id="7a001-143">AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({ event: "click", item: "18321116" }); </script></span><span class="sxs-lookup"><span data-stu-id="7a001-143">AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({ event: "click", item: "18321116" }); </script></span></span>

### <a name="31----limitations-and-browser-support"></a><span data-ttu-id="7a001-144">3.1.</span><span class="sxs-lookup"><span data-stu-id="7a001-144">3.1.</span></span>    <span data-ttu-id="7a001-145">Limitazioni e supporto browser</span><span class="sxs-lookup"><span data-stu-id="7a001-145">Limitations and Browser Support</span></span>
<span data-ttu-id="7a001-146">Di seguito viene fornita un'implementazione di riferimento così com'è.</span><span class="sxs-lookup"><span data-stu-id="7a001-146">This is a reference implementation and it is given as is.</span></span> <span data-ttu-id="7a001-147">Tutti i principali browser dovrebbero essere supportati.</span><span class="sxs-lookup"><span data-stu-id="7a001-147">It should support all major browsers.</span></span>

### <a name="32----type-of-events"></a><span data-ttu-id="7a001-148">3.2.</span><span class="sxs-lookup"><span data-stu-id="7a001-148">3.2.</span></span>    <span data-ttu-id="7a001-149">Tipi di eventi</span><span class="sxs-lookup"><span data-stu-id="7a001-149">Type of Events</span></span>
<span data-ttu-id="7a001-150">Sono disponibili 5 tipi di evento che supporta la libreria di hello: fare clic su, fare clic su indicazione, aggiungere tooShop carrello, rimuovere dal reparto carrello e l'acquisto.</span><span class="sxs-lookup"><span data-stu-id="7a001-150">There are 5 types of event that hello library supports: Click, Recommendation Click, Add tooShop Cart, Remove from Shop Cart and Purchase.</span></span> <span data-ttu-id="7a001-151">È un evento aggiuntivo che è usato tooset hello utente contesto denominato account di accesso.</span><span class="sxs-lookup"><span data-stu-id="7a001-151">There is an additional event that is used tooset hello user context called Login.</span></span>

#### <a name="321-click-event"></a><span data-ttu-id="7a001-152">3.2.1.</span><span class="sxs-lookup"><span data-stu-id="7a001-152">3.2.1.</span></span> <span data-ttu-id="7a001-153">Evento Click</span><span class="sxs-lookup"><span data-stu-id="7a001-153">Click Event</span></span>
<span data-ttu-id="7a001-154">Questo evento deve essere usato ogni volta che un utente fa clic su un elemento.</span><span class="sxs-lookup"><span data-stu-id="7a001-154">This event should be used any time a user clicked on an item.</span></span> <span data-ttu-id="7a001-155">In genere quando l'utente fa clic su un elemento di una nuova pagina viene aperto con i dettagli dell'elemento hello; in questa pagina, questo evento dovrebbe essere attivato.</span><span class="sxs-lookup"><span data-stu-id="7a001-155">Usually when user clicks on an item a new page is opened with hello item details; in this page this event should be triggered.</span></span>

<span data-ttu-id="7a001-156">Parametri</span><span class="sxs-lookup"><span data-stu-id="7a001-156">Parameters:</span></span>

* <span data-ttu-id="7a001-157">event (stringa, obbligatorio) - "click"</span><span class="sxs-lookup"><span data-stu-id="7a001-157">event (string, mandatory) - “click”</span></span>
* <span data-ttu-id="7a001-158">elemento (string, obbligatorio) - identificatore univoco dell'elemento hello</span><span class="sxs-lookup"><span data-stu-id="7a001-158">item (string, mandatory) - Unique identifier of hello item</span></span>
* <span data-ttu-id="7a001-159">itemName (stringa, facoltativo) nome hello dell'elemento di hello</span><span class="sxs-lookup"><span data-stu-id="7a001-159">itemName (string, optional) - hello name of hello item</span></span>
* <span data-ttu-id="7a001-160">Descrizione articolo (stringa, facoltativo) - Descrizione hello dell'elemento di hello</span><span class="sxs-lookup"><span data-stu-id="7a001-160">itemDescription (string, optional) - hello description of hello item</span></span>
* <span data-ttu-id="7a001-161">itemCategory (stringa, facoltativo) categoria hello dell'elemento hello</span><span class="sxs-lookup"><span data-stu-id="7a001-161">itemCategory (string, optional) - hello category of hello item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "click", item: "3111718" });
        </script>

<span data-ttu-id="7a001-162">In alternativa, con dati facoltativi:</span><span class="sxs-lookup"><span data-stu-id="7a001-162">Or with optional data:</span></span>

        <script>
            if (typeof AzureMLRecommendationsEvent === "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "click", item: "3111718", itemName: "Plane", itemDescription: "It is a big plane", itemCategory: "Aviation"});
        </script>


#### <a name="322-recommendation-click-event"></a><span data-ttu-id="7a001-163">3.2.2.</span><span class="sxs-lookup"><span data-stu-id="7a001-163">3.2.2.</span></span> <span data-ttu-id="7a001-164">Evento Recommendation Click</span><span class="sxs-lookup"><span data-stu-id="7a001-164">Recommendation Click Event</span></span>
<span data-ttu-id="7a001-165">Questo evento deve essere usato ogni volta che un utente fa clic su un elemento ricevuto da Azure ML Recommendations come elemento raccomandato.</span><span class="sxs-lookup"><span data-stu-id="7a001-165">This event should be used any time a user clicked on an item that was received from Azure ML Recommendations as a recommended item.</span></span> <span data-ttu-id="7a001-166">In genere quando l'utente fa clic su un elemento di una nuova pagina viene aperto con i dettagli dell'elemento hello; in questa pagina, questo evento dovrebbe essere attivato.</span><span class="sxs-lookup"><span data-stu-id="7a001-166">Usually when user clicks on an item a new page is opened with hello item details; in this page this event should be triggered.</span></span>

<span data-ttu-id="7a001-167">Parametri</span><span class="sxs-lookup"><span data-stu-id="7a001-167">Parameters:</span></span>

* <span data-ttu-id="7a001-168">event (stringa, obbligatorio) - "recommendationclick"</span><span class="sxs-lookup"><span data-stu-id="7a001-168">event (string, mandatory) - “recommendationclick”</span></span>
* <span data-ttu-id="7a001-169">elemento (string, obbligatorio) - identificatore univoco dell'elemento hello</span><span class="sxs-lookup"><span data-stu-id="7a001-169">item (string, mandatory) - Unique identifier of hello item</span></span>
* <span data-ttu-id="7a001-170">itemName (stringa, facoltativo) nome hello dell'elemento di hello</span><span class="sxs-lookup"><span data-stu-id="7a001-170">itemName (string, optional) - hello name of hello item</span></span>
* <span data-ttu-id="7a001-171">Descrizione articolo (stringa, facoltativo) - Descrizione hello dell'elemento di hello</span><span class="sxs-lookup"><span data-stu-id="7a001-171">itemDescription (string, optional) - hello description of hello item</span></span>
* <span data-ttu-id="7a001-172">itemCategory (stringa, facoltativo) categoria hello dell'elemento hello</span><span class="sxs-lookup"><span data-stu-id="7a001-172">itemCategory (string, optional) - hello category of hello item</span></span>
* <span data-ttu-id="7a001-173">i valori di inizializzazione (matrice di stringhe, facoltativo) - hello i valori di inizializzazione che ha generato query raccomandazione hello.</span><span class="sxs-lookup"><span data-stu-id="7a001-173">seeds (string array, optional) - hello seeds that generated hello recommendation query.</span></span>
* <span data-ttu-id="7a001-174">recoList (matrice di stringhe, facoltativo) - hello risultato della richiesta di indicazione hello che ha generato l'elemento hello che è stato fatto clic.</span><span class="sxs-lookup"><span data-stu-id="7a001-174">recoList (string array, optional) - hello result of hello recommendation request that generated hello item that was clicked.</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "recommendationclick", item: "18899918" });
        </script>

<span data-ttu-id="7a001-175">In alternativa, con dati facoltativi:</span><span class="sxs-lookup"><span data-stu-id="7a001-175">Or with optional data:</span></span>

        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: eventName, item: "198", itemName: "Plane2", itemDescription: "It is a big plane2", itemCategory: "Default2", seeds: ["Seed1", "Seed2"], recoList: ["199", "198", "197"]                 });
        </script>


#### <a name="323-add-shopping-cart-event"></a><span data-ttu-id="7a001-176">3.2.3.</span><span class="sxs-lookup"><span data-stu-id="7a001-176">3.2.3.</span></span> <span data-ttu-id="7a001-177">Evento Add Shopping Cart</span><span class="sxs-lookup"><span data-stu-id="7a001-177">Add Shopping Cart Event</span></span>
<span data-ttu-id="7a001-178">Questo evento deve essere utilizzato quando l'utente di hello aggiungere un elemento di toohello carrello degli acquisti.</span><span class="sxs-lookup"><span data-stu-id="7a001-178">This event should be used when hello user add an item toohello shopping cart.</span></span>
<span data-ttu-id="7a001-179">Parametri</span><span class="sxs-lookup"><span data-stu-id="7a001-179">Parameters:</span></span>

* <span data-ttu-id="7a001-180">event (stringa, obbligatorio) - "addshopcart"</span><span class="sxs-lookup"><span data-stu-id="7a001-180">event (string, mandatory) - “addshopcart”</span></span>
* <span data-ttu-id="7a001-181">elemento (string, obbligatorio) - identificatore univoco dell'elemento hello</span><span class="sxs-lookup"><span data-stu-id="7a001-181">item (string, mandatory) - Unique identifier of hello item</span></span>
* <span data-ttu-id="7a001-182">itemName (stringa, facoltativo) nome hello dell'elemento di hello</span><span class="sxs-lookup"><span data-stu-id="7a001-182">itemName (string, optional) - hello name of hello item</span></span>
* <span data-ttu-id="7a001-183">Descrizione articolo (stringa, facoltativo) - Descrizione hello dell'elemento di hello</span><span class="sxs-lookup"><span data-stu-id="7a001-183">itemDescription (string, optional) - hello description of hello item</span></span>
* <span data-ttu-id="7a001-184">itemCategory (stringa, facoltativo) categoria hello dell'elemento hello</span><span class="sxs-lookup"><span data-stu-id="7a001-184">itemCategory (string, optional) - hello category of hello item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "addshopcart", item: "13221118" });
        </script>

#### <a name="324-remove-shopping-cart-event"></a><span data-ttu-id="7a001-185">3.2.4.</span><span class="sxs-lookup"><span data-stu-id="7a001-185">3.2.4.</span></span> <span data-ttu-id="7a001-186">Evento Remove Shopping Cart</span><span class="sxs-lookup"><span data-stu-id="7a001-186">Remove Shopping Cart Event</span></span>
<span data-ttu-id="7a001-187">Questo evento deve essere utilizzato quando l'utente hello rimuove un elemento toohello carrello acquisti.</span><span class="sxs-lookup"><span data-stu-id="7a001-187">This event should be used when hello user removes an item toohello shopping cart.</span></span>

<span data-ttu-id="7a001-188">Parametri</span><span class="sxs-lookup"><span data-stu-id="7a001-188">Parameters:</span></span>

* <span data-ttu-id="7a001-189">event (stringa, obbligatorio) - "removeshopcart"</span><span class="sxs-lookup"><span data-stu-id="7a001-189">event (string, mandatory) - “removeshopcart”</span></span>
* <span data-ttu-id="7a001-190">elemento (string, obbligatorio) - identificatore univoco dell'elemento hello</span><span class="sxs-lookup"><span data-stu-id="7a001-190">item (string, mandatory) - Unique identifier of hello item</span></span>
* <span data-ttu-id="7a001-191">itemName (stringa, facoltativo) nome hello dell'elemento di hello</span><span class="sxs-lookup"><span data-stu-id="7a001-191">itemName (string, optional) - hello name of hello item</span></span>
* <span data-ttu-id="7a001-192">Descrizione articolo (stringa, facoltativo) - Descrizione hello dell'elemento di hello</span><span class="sxs-lookup"><span data-stu-id="7a001-192">itemDescription (string, optional) - hello description of hello item</span></span>
* <span data-ttu-id="7a001-193">itemCategory (stringa, facoltativo) categoria hello dell'elemento hello</span><span class="sxs-lookup"><span data-stu-id="7a001-193">itemCategory (string, optional) - hello category of hello item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "removeshopcart", item: "111118" });
        </script>

#### <a name="325-purchase-event"></a><span data-ttu-id="7a001-194">3.2.5.</span><span class="sxs-lookup"><span data-stu-id="7a001-194">3.2.5.</span></span> <span data-ttu-id="7a001-195">Evento Purchase</span><span class="sxs-lookup"><span data-stu-id="7a001-195">Purchase Event</span></span>
<span data-ttu-id="7a001-196">Questo evento deve essere utilizzato quando l'utente hello ha acquistato il carrello acquisti.</span><span class="sxs-lookup"><span data-stu-id="7a001-196">This event should be used when hello user purchased his shopping cart.</span></span>

<span data-ttu-id="7a001-197">Parametri</span><span class="sxs-lookup"><span data-stu-id="7a001-197">Parameters:</span></span>

* <span data-ttu-id="7a001-198">event (stringa) - "purchase"</span><span class="sxs-lookup"><span data-stu-id="7a001-198">event (string) - “purchase”</span></span>
* <span data-ttu-id="7a001-199">items (acquistati) - matrice contenente una voce per ogni elemento acquistato</span><span class="sxs-lookup"><span data-stu-id="7a001-199">items ( Purchased[] ) - Array holding an entry for each item purchased.</span></span><br><br>
  <span data-ttu-id="7a001-200">Formato elementi acquistati:</span><span class="sxs-lookup"><span data-stu-id="7a001-200">Purchased format:</span></span>
  * <span data-ttu-id="7a001-201">elemento (string) - identificatore univoco dell'elemento hello.</span><span class="sxs-lookup"><span data-stu-id="7a001-201">item (string) - Unique identifier of hello item.</span></span>
  * <span data-ttu-id="7a001-202">count (numero intero o stringa) - numero di elementi che sono stati acquistati</span><span class="sxs-lookup"><span data-stu-id="7a001-202">count (int or string) - number of items that were purchased.</span></span>
  * <span data-ttu-id="7a001-203">prezzo (float o string) - campo facoltativo - hello prezzo dell'articolo hello.</span><span class="sxs-lookup"><span data-stu-id="7a001-203">price (float or string) - optional field - hello price of hello item.</span></span>

<span data-ttu-id="7a001-204">esempio di Hello seguente mostra l'acquisto di 3 elementi (33, 34, 35), due con tutti i campi popolati (elemento, count, prezzo) e uno (elemento 34) senza un prezzo.</span><span class="sxs-lookup"><span data-stu-id="7a001-204">hello example below shows purchase of 3 items (33, 34, 35), two with all fields populated (item, count, price) and one (item 34) without a price.</span></span>

        <script>
            if ( typeof AzureMLRecommendationsEvent == "undefined"){ AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "purchase", items: [{ item: "33", count: "1", price: "10" }, { item: "34", count: "2" }, { item: "35", count: "1", price: "210" }] });
        </script>

#### <a name="326-user-login-event"></a><span data-ttu-id="7a001-205">3.2.6.</span><span class="sxs-lookup"><span data-stu-id="7a001-205">3.2.6.</span></span> <span data-ttu-id="7a001-206">Evento User Login</span><span class="sxs-lookup"><span data-stu-id="7a001-206">User Login Event</span></span>
<span data-ttu-id="7a001-207">Azure ML indicazioni evento libreria consente di creare e utilizzare un cookie negli eventi tooidentify ordine da cui proviene hello browser stesso.</span><span class="sxs-lookup"><span data-stu-id="7a001-207">Azure ML Recommendations Event library creates and use a cookie in order tooidentify events that came from hello same browser.</span></span> <span data-ttu-id="7a001-208">Nel modello di ordine tooimprove hello risultati Azure ML indicazioni consente tooset un'identificazione univoca di utente che eseguirà l'override dell'utilizzo di cookie hello.</span><span class="sxs-lookup"><span data-stu-id="7a001-208">In order tooimprove hello model results Azure ML Recommendations enables tooset a user unique identification that will override hello cookie usage.</span></span>

<span data-ttu-id="7a001-209">Questo evento deve essere utilizzato dopo sito tooyour account di accesso utente di hello.</span><span class="sxs-lookup"><span data-stu-id="7a001-209">This event should be used after hello user login tooyour site.</span></span>

<span data-ttu-id="7a001-210">Parametri</span><span class="sxs-lookup"><span data-stu-id="7a001-210">Parameters:</span></span>

* <span data-ttu-id="7a001-211">event (stringa) - "userlogin"</span><span class="sxs-lookup"><span data-stu-id="7a001-211">event (string) - “userlogin”</span></span>
* <span data-ttu-id="7a001-212">utente (string) - identificazione univoca dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="7a001-212">user (string) - unique identification of hello user.</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "userlogin", user: “ABCD10AA” });
        </script>

## <a name="4-consume-recommendations-via-javascript"></a><span data-ttu-id="7a001-213">4. Utilizzare le raccomandazioni tramite JavaScript</span><span class="sxs-lookup"><span data-stu-id="7a001-213">4. Consume Recommendations via JavaScript</span></span>
<span data-ttu-id="7a001-214">codice Hello che utilizza la raccomandazione hello viene attivato da un evento JavaScript dalla pagina Web del client hello.</span><span class="sxs-lookup"><span data-stu-id="7a001-214">hello code that consumes hello recommendation is triggered by some JavaScript event by hello client’s webpage.</span></span> <span data-ttu-id="7a001-215">risposta di raccomandazione Hello include hello gli ID degli elementi, i relativi nomi e le classificazioni consigliati.</span><span class="sxs-lookup"><span data-stu-id="7a001-215">hello recommendation response includes hello recommended items Ids, their names and their ratings.</span></span> <span data-ttu-id="7a001-216">È toouse migliore, è necessario eseguire questa opzione solo per visualizzare un elenco di elementi - più complessi la gestione (ad esempio l'aggiunta di metadati dell'elemento hello) consigliato hello sull'integrazione di lato server hello.</span><span class="sxs-lookup"><span data-stu-id="7a001-216">It’s best toouse this option only for a list display of hello recommended items - more complex handling (such as adding hello item’s metadata) should be done on hello server side integration.</span></span>

### <a name="41-consume-recommendations"></a><span data-ttu-id="7a001-217">4.1 Utilizzare le raccomandazioni</span><span class="sxs-lookup"><span data-stu-id="7a001-217">4.1 Consume Recommendations</span></span>
<span data-ttu-id="7a001-218">le raccomandazioni tooconsume che necessarie tooinclude hello necessarie librerie JavaScript nella pagina e toocall AzureMLRecommendationsStart.</span><span class="sxs-lookup"><span data-stu-id="7a001-218">tooconsume recommendations you need tooinclude hello required JavaScript libraries in your page and toocall AzureMLRecommendationsStart.</span></span> <span data-ttu-id="7a001-219">Vedere la sezione 2.</span><span class="sxs-lookup"><span data-stu-id="7a001-219">See section 2.</span></span>

<span data-ttu-id="7a001-220">indicazioni tooconsume per uno o più elementi, è necessario toocall chiamato un metodo: AzureMLRecommendationsGetI2IRecommendation.</span><span class="sxs-lookup"><span data-stu-id="7a001-220">tooconsume recommendations for one or more items you need toocall a method called: AzureMLRecommendationsGetI2IRecommendation.</span></span>

<span data-ttu-id="7a001-221">Parametri</span><span class="sxs-lookup"><span data-stu-id="7a001-221">Parameters:</span></span>

* <span data-ttu-id="7a001-222">gli elementi (matrice di stringhe): uno o più elementi tooget consigli.</span><span class="sxs-lookup"><span data-stu-id="7a001-222">items (array of strings) - One or more items tooget recommendations for.</span></span> <span data-ttu-id="7a001-223">Se si usa una build Fbt, qui sarà possibile impostare un solo elemento.</span><span class="sxs-lookup"><span data-stu-id="7a001-223">If you consume an Fbt build then you can set here only one item.</span></span>
* <span data-ttu-id="7a001-224">numberOfResults (numero intero) - numero dei risultati richiesti</span><span class="sxs-lookup"><span data-stu-id="7a001-224">numberOfResults (int) - number of required results.</span></span>
* <span data-ttu-id="7a001-225">includeMetadata (valore booleano, facoltativo) - se impostato too'true' indica il campo di metadati hello deve essere popolato nel risultato hello.</span><span class="sxs-lookup"><span data-stu-id="7a001-225">includeMetadata (boolean, optional) - if set too‘true’ indicates that hello metadata field must be populated in hello result.</span></span>
* <span data-ttu-id="7a001-226">L'elaborazione di funzione, una funzione che gestirà indicazioni hello restituito.</span><span class="sxs-lookup"><span data-stu-id="7a001-226">Processing function - a function that will handle hello recommendations returned.</span></span> <span data-ttu-id="7a001-227">Hello dati vengono restituiti come matrice di:</span><span class="sxs-lookup"><span data-stu-id="7a001-227">hello data is returned as an array of:</span></span>
  * <span data-ttu-id="7a001-228">Item - ID univoco dell'elemento</span><span class="sxs-lookup"><span data-stu-id="7a001-228">Item - item unique id</span></span>
  * <span data-ttu-id="7a001-229">name - nome dell'elemento (se esiste nel catalogo)</span><span class="sxs-lookup"><span data-stu-id="7a001-229">name - item name (if exist in catalog)</span></span>
  * <span data-ttu-id="7a001-230">rating - valutazione della raccomandazione</span><span class="sxs-lookup"><span data-stu-id="7a001-230">rating - recommendation rating</span></span>
  * <span data-ttu-id="7a001-231">metadati - stringa che rappresenta i metadati di hello dell'elemento hello</span><span class="sxs-lookup"><span data-stu-id="7a001-231">metadata - a string that represents hello metadata of hello item</span></span>

<span data-ttu-id="7a001-232">Esempio: le richieste di hello seguente codice 8 indicazioni per l'elemento "64f6eb0d-947a-4c18-a16c-888da9e228ba" (e non specificando includeMetadata - implicitamente dichiara che i metadati non sono necessario), quindi concatenare i risultati di hello in un buffer.</span><span class="sxs-lookup"><span data-stu-id="7a001-232">Example: hello following code requests 8 recommendations for item "64f6eb0d-947a-4c18-a16c-888da9e228ba" (and by not specifying includeMetadata - it implicitly says that no metadata is required), it then concatenate hello results into a buffer.</span></span>

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
