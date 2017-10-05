---
title: 'Controllare il comportamento di memorizzazione nella cache della rete CDN di Azure con stringhe di query: Premium | Documentazione Microsoft'
description: La memorizzazione nella cache della stringa di query della rete CDN controlla in che modo i file devono essere memorizzati nella cache quando contengono stringhe di query.
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
ms.openlocfilehash: 145067c2ce50b41c4783f4de4052c0e7cb529fc7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings---premium"></a><span data-ttu-id="12b6f-103">Controllare il comportamento di memorizzazione nella cache della rete CDN di Azure con stringhe di query: Premium</span><span class="sxs-lookup"><span data-stu-id="12b6f-103">Control Azure CDN caching behavior with query strings - Premium</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="12b6f-104">Standard</span><span class="sxs-lookup"><span data-stu-id="12b6f-104">Standard</span></span>](cdn-query-string.md)
> * [<span data-ttu-id="12b6f-105">Rete CDN Premium di Azure fornita da Verizon</span><span class="sxs-lookup"><span data-stu-id="12b6f-105">Azure CDN Premium from Verizon</span></span>](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="12b6f-106">Panoramica</span><span class="sxs-lookup"><span data-stu-id="12b6f-106">Overview</span></span>
<span data-ttu-id="12b6f-107">La memorizzazione nella cache della stringa di query controlla come i file devono essere memorizzati nella cache quando contengono stringhe di query.</span><span class="sxs-lookup"><span data-stu-id="12b6f-107">Query string caching controls how files are to be cached when they contain query strings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="12b6f-108">I prodotti della rete CDN Standard e Premium forniscono la stessa funzionalità di memorizzazione nella cache delle stringhe di query, ma l'interfaccia utente è diversa.</span><span class="sxs-lookup"><span data-stu-id="12b6f-108">The Standard and Premium CDN products provide the same query string caching functionality, but the user interface differs.</span></span>  <span data-ttu-id="12b6f-109">Questo documento descrive l'interfaccia della **rete CDN Premium di Azure fornita da Verizon**.</span><span class="sxs-lookup"><span data-stu-id="12b6f-109">This document describes the interface for **Azure CDN Premium from Verizon**.</span></span>  <span data-ttu-id="12b6f-110">Per informazioni sulla memorizzazione nella cache di stringhe di query con la **rete CDN Standard di Azure fornita da Akamai** e la **rete CDN Standard di Azure fornita da Verizon**, vedere l'articolo [Controllo del comportamento di memorizzazione nella cache delle richieste della rete CDN con le stringhe di query](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="12b6f-110">For query string caching with **Azure CDN Standard from Akamai** and **Azure CDN Standard from Verizon**, see [Controlling caching behavior of CDN requests with query strings](cdn-query-string.md).</span></span>
> 
> 

<span data-ttu-id="12b6f-111">Sono disponibili tre modalità:</span><span class="sxs-lookup"><span data-stu-id="12b6f-111">Three modes are available:</span></span>

* <span data-ttu-id="12b6f-112">**standard-cache**: si tratta della modalità predefinita.</span><span class="sxs-lookup"><span data-stu-id="12b6f-112">**standard-cache**:  This is the default mode.</span></span>  <span data-ttu-id="12b6f-113">Il nodo edge della rete CDN passerà la stringa di query dal richiedente all’origine alla prima richiesta ed eseguirà la memorizzazione nella cache dell’asset.</span><span class="sxs-lookup"><span data-stu-id="12b6f-113">The CDN edge node will pass the query string from the requestor to the origin on the first request and cache the asset.</span></span>  <span data-ttu-id="12b6f-114">Tutte le richieste successive per quell’asset che vengono presentate dal nodo edge ignoreranno la stringa di query fino a quando l’asset memorizzato nella cache non sarà scaduto.</span><span class="sxs-lookup"><span data-stu-id="12b6f-114">All subsequent requests for that asset that are served from the edge node will ignore the query string until the cached asset expires.</span></span>
* <span data-ttu-id="12b6f-115">**no-cache**: in questa modalità, le richieste con stringhe di query non vengono memorizzate nella cache in corrispondenza del nodo edge della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="12b6f-115">**no-cache**:  In this mode, requests with query strings are not cached at the CDN edge node.</span></span>  <span data-ttu-id="12b6f-116">Il nodo edge recupera l'asset direttamente dall'origine e lo passa al richiedente ad ogni richiesta.</span><span class="sxs-lookup"><span data-stu-id="12b6f-116">The edge node retrieves the asset directly from the origin and passes it to the requestor with each request.</span></span>
* <span data-ttu-id="12b6f-117">**unique-cache**: questa modalità considera ogni richiesta con una stringa di query come un asset univoco con la propria memorizzazione nella cache.</span><span class="sxs-lookup"><span data-stu-id="12b6f-117">**unique-cache**:  This mode treats each request with a query string as a unique asset with its own cache.</span></span>  <span data-ttu-id="12b6f-118">Ad esempio, la risposta dall'origine per una richiesta di *foo.ashx?q=bar* verrebbe memorizzata nella cache in corrispondenza del nodo edge e restituita per le successive memorizzazione nella cache con quella stessa stringa di query.</span><span class="sxs-lookup"><span data-stu-id="12b6f-118">For example, the response from the origin for a request for *foo.ashx?q=bar* would be cached at the edge node and returned for subsequent caches with that same query string.</span></span>  <span data-ttu-id="12b6f-119">Una richiesta di *foo.ashx?q=somethingelse* verrebbe memorizzata nella cache come asset separato con il proprio time to live.</span><span class="sxs-lookup"><span data-stu-id="12b6f-119">A request for *foo.ashx?q=somethingelse* would be cached as a separate asset with its own time to live.</span></span>

## <a name="changing-query-string-caching-settings-for-premium-cdn-profiles"></a><span data-ttu-id="12b6f-120">Modifica delle impostazioni di memorizzazione nella cache della stringa di query per i profili premium della rete CDN</span><span class="sxs-lookup"><span data-stu-id="12b6f-120">Changing query string caching settings for premium CDN profiles</span></span>
1. <span data-ttu-id="12b6f-121">Dal pannello del profilo della rete CDN fare clic sul pulsante **Gestisci** .</span><span class="sxs-lookup"><span data-stu-id="12b6f-121">From the CDN profile blade, click the **Manage** button.</span></span>
   
    ![Pulsante Gestisci pannello del profilo di rete CDN](./media/cdn-query-string-premium/cdn-manage-btn.png)
   
    <span data-ttu-id="12b6f-123">Si aprirà il portale di gestione della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="12b6f-123">The CDN management portal opens.</span></span>
2. <span data-ttu-id="12b6f-124">Passare il puntatore sulla scheda **HTTP Grande**, quindi passare il puntatore sul riquadro a comparsa **Impostazioni della memorizzazione nella cache**.</span><span class="sxs-lookup"><span data-stu-id="12b6f-124">Hover over the **HTTP Large** tab, then hover over the **Cache Settings** flyout.</span></span>  <span data-ttu-id="12b6f-125">Fare clic su **Memorizzazione nella cache della stringa di Query**.</span><span class="sxs-lookup"><span data-stu-id="12b6f-125">Click on **Query-String Caching**.</span></span>
   
    <span data-ttu-id="12b6f-126">Vengono visualizzate le opzioni di memorizzazione nella cache della stringa di query.</span><span class="sxs-lookup"><span data-stu-id="12b6f-126">Query string caching options are displayed.</span></span>
   
    ![Opzioni della memorizzazione nella cache della stringa di query della rete CDN](./media/cdn-query-string-premium/cdn-query-string.png)
3. <span data-ttu-id="12b6f-128">Una volta effettuate le selezioni, fare clic sul pulsante **Aggiorna** .</span><span class="sxs-lookup"><span data-stu-id="12b6f-128">After making your selection, click the **Update** button.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="12b6f-129">Le modifiche delle impostazioni non sono immediatamente visibili, perché la propagazione della registrazione nella rete CDN richiede tempo.</span><span class="sxs-lookup"><span data-stu-id="12b6f-129">The settings changes may not be immediately visible, as it takes time for the registration to propagate through the CDN.</span></span>  <span data-ttu-id="12b6f-130">Per i profili della <b>rete CDN di Azure fornita da Verizon</b>, la propagazione in genere viene completata entro 90 minuti, ma in alcuni casi può richiedere più tempo.</span><span class="sxs-lookup"><span data-stu-id="12b6f-130">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
> 
> 

