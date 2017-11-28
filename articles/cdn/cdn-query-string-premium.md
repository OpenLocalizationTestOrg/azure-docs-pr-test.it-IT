---
title: comportamento di memorizzazione nella cache della rete CDN di Azure con le stringhe di query - Premium aaaControl | Documenti Microsoft
description: Stringa di query della rete CDN Azure controlli come i file vengono memorizzati nella cache quando contengono stringhe di query toobe di memorizzazione nella cache.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 99db4a85-4f5f-431f-ac3a-69e05518c997
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 5c97cf0230ae13fd378bfce49481f3135a5ef101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings---premium"></a><span data-ttu-id="2ff3c-103">Controllare il comportamento di memorizzazione nella cache della rete CDN di Azure con stringhe di query: Premium</span><span class="sxs-lookup"><span data-stu-id="2ff3c-103">Control Azure CDN caching behavior with query strings - Premium</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2ff3c-104">Standard</span><span class="sxs-lookup"><span data-stu-id="2ff3c-104">Standard</span></span>](cdn-query-string.md)
> * [<span data-ttu-id="2ff3c-105">Rete CDN Premium di Azure fornita da Verizon</span><span class="sxs-lookup"><span data-stu-id="2ff3c-105">Azure CDN Premium from Verizon</span></span>](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="2ff3c-106">Panoramica</span><span class="sxs-lookup"><span data-stu-id="2ff3c-106">Overview</span></span>
<span data-ttu-id="2ff3c-107">La memorizzazione nella cache i controlli come i file vengono memorizzati nella cache quando contengono stringhe di query toobe stringa di query.</span><span class="sxs-lookup"><span data-stu-id="2ff3c-107">Query string caching controls how files are toobe cached when they contain query strings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2ff3c-108">prodotti Standard e Premium CDN Hello forniscono hello stessa funzionalità di memorizzazione nella cache di stringhe di query, ma l'interfaccia utente di hello diversa.</span><span class="sxs-lookup"><span data-stu-id="2ff3c-108">hello Standard and Premium CDN products provide hello same query string caching functionality, but hello user interface differs.</span></span>  <span data-ttu-id="2ff3c-109">Questo documento descrive l'interfaccia di hello per **Premium rete CDN di Azure da Verizon**.</span><span class="sxs-lookup"><span data-stu-id="2ff3c-109">This document describes hello interface for **Azure CDN Premium from Verizon**.</span></span>  <span data-ttu-id="2ff3c-110">Per informazioni sulla memorizzazione nella cache di stringhe di query con la **rete CDN Standard di Azure fornita da Akamai** e la **rete CDN Standard di Azure fornita da Verizon**, vedere l'articolo [Controllo del comportamento di memorizzazione nella cache delle richieste della rete CDN con le stringhe di query](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="2ff3c-110">For query string caching with **Azure CDN Standard from Akamai** and **Azure CDN Standard from Verizon**, see [Controlling caching behavior of CDN requests with query strings](cdn-query-string.md).</span></span>
> 
> 

<span data-ttu-id="2ff3c-111">Sono disponibili tre modalità:</span><span class="sxs-lookup"><span data-stu-id="2ff3c-111">Three modes are available:</span></span>

* <span data-ttu-id="2ff3c-112">**standard cache**: si tratta di modalità predefinita di hello.</span><span class="sxs-lookup"><span data-stu-id="2ff3c-112">**standard-cache**:  This is hello default mode.</span></span>  <span data-ttu-id="2ff3c-113">nodo perimetrale della rete CDN di Hello passa la stringa di query hello dall'origine toohello richiedente di hello nella prima richiesta hello e asset hello cache.</span><span class="sxs-lookup"><span data-stu-id="2ff3c-113">hello CDN edge node will pass hello query string from hello requestor toohello origin on hello first request and cache hello asset.</span></span>  <span data-ttu-id="2ff3c-114">Tutte le richieste successive per tale asset resi disponibili dal nodo edge hello ignorerà la stringa di query hello fino alla scadenza di asset memorizzati nella cache di hello.</span><span class="sxs-lookup"><span data-stu-id="2ff3c-114">All subsequent requests for that asset that are served from hello edge node will ignore hello query string until hello cached asset expires.</span></span>
* <span data-ttu-id="2ff3c-115">**no-cache**: In questa modalità, le richieste con stringhe di query non vengono memorizzate nel nodo perimetrale della rete CDN di hello.</span><span class="sxs-lookup"><span data-stu-id="2ff3c-115">**no-cache**:  In this mode, requests with query strings are not cached at hello CDN edge node.</span></span>  <span data-ttu-id="2ff3c-116">nodo edge Hello recupera asset hello direttamente dall'origine hello e passa il richiedente toohello con ogni richiesta.</span><span class="sxs-lookup"><span data-stu-id="2ff3c-116">hello edge node retrieves hello asset directly from hello origin and passes it toohello requestor with each request.</span></span>
* <span data-ttu-id="2ff3c-117">**unique-cache**: questa modalità considera ogni richiesta con una stringa di query come un asset univoco con la propria memorizzazione nella cache.</span><span class="sxs-lookup"><span data-stu-id="2ff3c-117">**unique-cache**:  This mode treats each request with a query string as a unique asset with its own cache.</span></span>  <span data-ttu-id="2ff3c-118">Ad esempio, hello risposta dall'origine hello per una richiesta di *foo.ashx?q=bar* vengono memorizzati nella cache al nodo del bordo hello e restituiti per le successive cache con la stessa stringa di query.</span><span class="sxs-lookup"><span data-stu-id="2ff3c-118">For example, hello response from hello origin for a request for *foo.ashx?q=bar* would be cached at hello edge node and returned for subsequent caches with that same query string.</span></span>  <span data-ttu-id="2ff3c-119">Una richiesta per *foo.ashx?q=somethingelse* verrà memorizzata nella cache come una risorsa con il proprio tempo toolive separata.</span><span class="sxs-lookup"><span data-stu-id="2ff3c-119">A request for *foo.ashx?q=somethingelse* would be cached as a separate asset with its own time toolive.</span></span>

## <a name="changing-query-string-caching-settings-for-premium-cdn-profiles"></a><span data-ttu-id="2ff3c-120">Modifica delle impostazioni di memorizzazione nella cache della stringa di query per i profili premium della rete CDN</span><span class="sxs-lookup"><span data-stu-id="2ff3c-120">Changing query string caching settings for premium CDN profiles</span></span>
1. <span data-ttu-id="2ff3c-121">Dal Pannello di profilo CDN hello, fare clic su hello **Gestisci** pulsante.</span><span class="sxs-lookup"><span data-stu-id="2ff3c-121">From hello CDN profile blade, click hello **Manage** button.</span></span>
   
    ![Pulsante Gestisci pannello del profilo di rete CDN](./media/cdn-query-string-premium/cdn-manage-btn.png)
   
    <span data-ttu-id="2ff3c-123">viene visualizzato il portale di gestione della rete CDN Hello.</span><span class="sxs-lookup"><span data-stu-id="2ff3c-123">hello CDN management portal opens.</span></span>
2. <span data-ttu-id="2ff3c-124">Passare il mouse su hello **HTTP grandi** scheda, quindi passare il mouse su hello **le impostazioni della Cache** riquadro a comparsa.</span><span class="sxs-lookup"><span data-stu-id="2ff3c-124">Hover over hello **HTTP Large** tab, then hover over hello **Cache Settings** flyout.</span></span>  <span data-ttu-id="2ff3c-125">Fare clic su **Memorizzazione nella cache della stringa di Query**.</span><span class="sxs-lookup"><span data-stu-id="2ff3c-125">Click on **Query-String Caching**.</span></span>
   
    <span data-ttu-id="2ff3c-126">Vengono visualizzate le opzioni di memorizzazione nella cache della stringa di query.</span><span class="sxs-lookup"><span data-stu-id="2ff3c-126">Query string caching options are displayed.</span></span>
   
    ![Opzioni della memorizzazione nella cache della stringa di query della rete CDN](./media/cdn-query-string-premium/cdn-query-string.png)
3. <span data-ttu-id="2ff3c-128">Dopo aver effettuato la selezione, fare clic su hello **aggiornamento** pulsante.</span><span class="sxs-lookup"><span data-stu-id="2ff3c-128">After making your selection, click hello **Update** button.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2ff3c-129">modifiche alle impostazioni di Hello potrebbe non essere immediatamente visibile, come il tempo per hello registrazione toopropagate tramite hello CDN.</span><span class="sxs-lookup"><span data-stu-id="2ff3c-129">hello settings changes may not be immediately visible, as it takes time for hello registration toopropagate through hello CDN.</span></span>  <span data-ttu-id="2ff3c-130">Per i profili della <b>rete CDN di Azure fornita da Verizon</b>, la propagazione in genere viene completata entro 90 minuti, ma in alcuni casi può richiedere più tempo.</span><span class="sxs-lookup"><span data-stu-id="2ff3c-130">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
> 
> 

