---
title: Precaricare asset in un endpoint della rete CDN di Azure | Documentazione Microsoft
description: Informazioni su come precaricare il contenuto memorizzato nella cache in un endpoint della rete CDN di Azure.
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 5ea3eba5-1335-413e-9af3-3918ce608a83
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 1f2dcd9a91bb6e883cbef06373c1acd98bf8d45f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="pre-load-assets-on-an-azure-cdn-endpoint"></a><span data-ttu-id="73415-103">Precaricamento di risorse in un endpoint della rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="73415-103">Pre-load assets on an Azure CDN endpoint</span></span>
[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="73415-104">Per impostazione predefinita, gli asset vengono prima di tutto memorizzati nella cache quando vengono richiesti.</span><span class="sxs-lookup"><span data-stu-id="73415-104">By default, assets are first cached as they are requested.</span></span> <span data-ttu-id="73415-105">Questo significa che la prima richiesta da ogni area potrebbe richiedere più tempo, poiché i server perimetrali non avranno il contenuto memorizzato nella cache e la richiesta dovrà essere inoltrata al server di origine.</span><span class="sxs-lookup"><span data-stu-id="73415-105">This means that the first request from each region may take longer, since the edge servers will not have the content cached and will need to forward the request to the origin server.</span></span> <span data-ttu-id="73415-106">Il precaricamento del contenuto consente di evitare questa latenza della prima richiesta.</span><span class="sxs-lookup"><span data-stu-id="73415-106">Pre-loading content avoids this first hit latency.</span></span>

<span data-ttu-id="73415-107">Oltre a fornire una migliore esperienza utente, il precaricamento di asset memorizzati nella cache può inoltre ridurre il traffico di rete sul server di origine.</span><span class="sxs-lookup"><span data-stu-id="73415-107">In addition to providing a better customer experience, pre-loading your cached assets can also reduce network traffic on the origin server.</span></span>

> [!NOTE]
> <span data-ttu-id="73415-108">Il precaricamento degli asset è utile per eventi di grandi dimensioni o contenuto che diventa disponibile contemporaneamente per un numero elevato di utenti, come ad esempio la nuova versione di un filmato o un aggiornamento software.</span><span class="sxs-lookup"><span data-stu-id="73415-108">Pre-loading assets is useful for  large events or content that becomes simultaneously available to a large number of users, such as a new movie release or a software update.</span></span>
> 
> 

<span data-ttu-id="73415-109">Questa esercitazione illustra in modo dettagliato il precaricamento di contenuto memorizzato nella cache in tutti i nodi perimetrali della rete CDN di Azure.</span><span class="sxs-lookup"><span data-stu-id="73415-109">This tutorial walks you through pre-loading cached content on all Azure CDN edge nodes.</span></span>

## <a name="walkthrough"></a><span data-ttu-id="73415-110">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="73415-110">Walkthrough</span></span>
1. <span data-ttu-id="73415-111">Nel [portale di Azure](https://portal.azure.com)passare al profilo di rete CDN contenente l'endpoint che si vuole precaricare.</span><span class="sxs-lookup"><span data-stu-id="73415-111">In the [Azure Portal](https://portal.azure.com), browse to the CDN profile containing the endpoint you wish to pre-load.</span></span>  <span data-ttu-id="73415-112">Viene visualizzato il pannello del profilo.</span><span class="sxs-lookup"><span data-stu-id="73415-112">The profile blade opens.</span></span>
2. <span data-ttu-id="73415-113">Fare clic sull'endpoint nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="73415-113">Click the endpoint in the list.</span></span>  <span data-ttu-id="73415-114">Viene visualizzato il pannello dell'endpoint.</span><span class="sxs-lookup"><span data-stu-id="73415-114">The endpoint blade opens.</span></span>
3. <span data-ttu-id="73415-115">Nel pannello dell'endpoint della rete CDN fare clic sul pulsante Carica.</span><span class="sxs-lookup"><span data-stu-id="73415-115">From the CDN endpoint blade, click the load button.</span></span>
   
    ![Pannello dell'endpoint della rete CDN](./media/cdn-preload-endpoint/cdn-endpoint-blade.png)
   
    <span data-ttu-id="73415-117">Viene visualizzato il pannello Carica.</span><span class="sxs-lookup"><span data-stu-id="73415-117">The Load blade opens.</span></span>
   
    ![Pannello di caricamento della rete CDN](./media/cdn-preload-endpoint/cdn-load-blade.png)
4. <span data-ttu-id="73415-119">Immettere il percorso completo di ogni asset da caricare, ad esempio `/pictures/kitten.png`, nella casella di testo **Percorso** .</span><span class="sxs-lookup"><span data-stu-id="73415-119">Enter the full path of each asset you wish to load (e.g., `/pictures/kitten.png`) in the **Path** textbox.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="73415-120">Dopo l'immissione di testo verranno visualizzate altre caselle di testo **Percorso** che consentono di compilare un elenco di più asset.</span><span class="sxs-lookup"><span data-stu-id="73415-120">More **Path** textboxes will appear after you enter text to allow you to build a list of multiple assets.</span></span>  <span data-ttu-id="73415-121">È possibile eliminare gli asset dall'elenco facendo clic sul pulsante con i puntini di sospensione (...).</span><span class="sxs-lookup"><span data-stu-id="73415-121">You can delete assets from the list by clicking the ellipsis (...) button.</span></span>
   > 
   > <span data-ttu-id="73415-122">I percorsi devono essere URL relativi che soddisfino l'[espressione regolare](https://msdn.microsoft.com/library/az24scfc.aspx) seguente:</span><span class="sxs-lookup"><span data-stu-id="73415-122">Paths must be a relative URL that fits the following [regular expression](https://msdn.microsoft.com/library/az24scfc.aspx):</span></span>  
   > ><span data-ttu-id="73415-123">Caricare un singolo percorso di file `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;</span><span class="sxs-lookup"><span data-stu-id="73415-123">Load a single file path `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;</span></span>  
   > ><span data-ttu-id="73415-124">Caricare un singolo file con stringa di query `@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`</span><span class="sxs-lookup"><span data-stu-id="73415-124">Load a single file with query string `@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`</span></span>  
   > 
   > <span data-ttu-id="73415-125">Ogni asset deve avere il proprio percorso.</span><span class="sxs-lookup"><span data-stu-id="73415-125">Each asset must have its own path.</span></span>  <span data-ttu-id="73415-126">Non esiste alcuna funzionalità con caratteri jolly per il pre-caricamento degli asset.</span><span class="sxs-lookup"><span data-stu-id="73415-126">There is no wildcard functionality for pre-loading assets.</span></span>
   > 
   > 
   
    ![Pulsante Carica](./media/cdn-preload-endpoint/cdn-load-paths.png)
5. <span data-ttu-id="73415-128">Fare clic sul pulsante **Carica** .</span><span class="sxs-lookup"><span data-stu-id="73415-128">Click the **Load** button.</span></span>
   
    ![Pulsante Carica](./media/cdn-preload-endpoint/cdn-load-button.png)

> [!NOTE]
> <span data-ttu-id="73415-130">Le richieste di caricamento sono limitate a un massimo di 10 al minuto per ogni profilo di rete CDN.</span><span class="sxs-lookup"><span data-stu-id="73415-130">There is a limitation of 10 load requests per minute per CDN profile.</span></span> <span data-ttu-id="73415-131">Sono consentiti 50 percorsi per richiesta.</span><span class="sxs-lookup"><span data-stu-id="73415-131">50 paths are allowed per request.</span></span> <span data-ttu-id="73415-132">Ogni percorso ha un limite di lunghezza di 1024 caratteri.</span><span class="sxs-lookup"><span data-stu-id="73415-132">Each path has a path-length limit of 1024 characters.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="73415-133">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="73415-133">See also</span></span>
* [<span data-ttu-id="73415-134">Ripulire un endpoint della rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="73415-134">Purge an Azure CDN endpoint</span></span>](cdn-purge-endpoint.md)
* [<span data-ttu-id="73415-135">Riferimento API REST della rete CDN di Azure - Ripulire o precaricare un endpoint</span><span class="sxs-lookup"><span data-stu-id="73415-135">Azure CDN REST API reference - Purge or Pre-Load an Endpoint</span></span>](https://msdn.microsoft.com/library/mt634451.aspx)

