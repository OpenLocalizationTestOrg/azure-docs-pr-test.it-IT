---
title: Asset aaaPre carico su un endpoint rete CDN di Azure | Documenti Microsoft
description: Informazioni su come toopre carico memorizzato nella cache il contenuto di un endpoint rete CDN di Azure.
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
ms.openlocfilehash: 08ac4b834f1ac8ce59d22e65fa8adea11bafcf17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="pre-load-assets-on-an-azure-cdn-endpoint"></a><span data-ttu-id="ed97c-103">Precaricamento di risorse in un endpoint della rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="ed97c-103">Pre-load assets on an Azure CDN endpoint</span></span>
[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="ed97c-104">Per impostazione predefinita, gli asset vengono prima di tutto memorizzati nella cache quando vengono richiesti.</span><span class="sxs-lookup"><span data-stu-id="ed97c-104">By default, assets are first cached as they are requested.</span></span> <span data-ttu-id="ed97c-105">Ciò significa che prima richiesta di hello da ogni area può richiedere più tempo, poiché non dispone di server edge hello contenuto hello memorizzati nella cache e sarà necessario tooforward hello richiesta toohello origine server.</span><span class="sxs-lookup"><span data-stu-id="ed97c-105">This means that hello first request from each region may take longer, since hello edge servers will not have hello content cached and will need tooforward hello request toohello origin server.</span></span> <span data-ttu-id="ed97c-106">Il precaricamento del contenuto consente di evitare questa latenza della prima richiesta.</span><span class="sxs-lookup"><span data-stu-id="ed97c-106">Pre-loading content avoids this first hit latency.</span></span>

<span data-ttu-id="ed97c-107">Inoltre tooproviding soddisfazione del cliente, precaricamento risorse memorizzate nella cache può anche ridurre il traffico di rete sul server di origine hello.</span><span class="sxs-lookup"><span data-stu-id="ed97c-107">In addition tooproviding a better customer experience, pre-loading your cached assets can also reduce network traffic on hello origin server.</span></span>

> [!NOTE]
> <span data-ttu-id="ed97c-108">Precaricamento in corso asset è utile per eventi di grandi dimensioni o contenuto che diventa tooa contemporaneamente disponibili numerosi utenti, ad esempio una nuova versione di film o un aggiornamento software.</span><span class="sxs-lookup"><span data-stu-id="ed97c-108">Pre-loading assets is useful for  large events or content that becomes simultaneously available tooa large number of users, such as a new movie release or a software update.</span></span>
> 
> 

<span data-ttu-id="ed97c-109">Questa esercitazione illustra in modo dettagliato il precaricamento di contenuto memorizzato nella cache in tutti i nodi perimetrali della rete CDN di Azure.</span><span class="sxs-lookup"><span data-stu-id="ed97c-109">This tutorial walks you through pre-loading cached content on all Azure CDN edge nodes.</span></span>

## <a name="walkthrough"></a><span data-ttu-id="ed97c-110">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="ed97c-110">Walkthrough</span></span>
1. <span data-ttu-id="ed97c-111">In hello [portale Azure](https://portal.azure.com), selezionare il profilo CDN toohello contenente hello endpoint desiderato toopre carico.</span><span class="sxs-lookup"><span data-stu-id="ed97c-111">In hello [Azure Portal](https://portal.azure.com), browse toohello CDN profile containing hello endpoint you wish toopre-load.</span></span>  <span data-ttu-id="ed97c-112">Apre il pannello di profilo Hello.</span><span class="sxs-lookup"><span data-stu-id="ed97c-112">hello profile blade opens.</span></span>
2. <span data-ttu-id="ed97c-113">Fare clic sull'endpoint hello nell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="ed97c-113">Click hello endpoint in hello list.</span></span>  <span data-ttu-id="ed97c-114">Apre il pannello di endpoint Hello.</span><span class="sxs-lookup"><span data-stu-id="ed97c-114">hello endpoint blade opens.</span></span>
3. <span data-ttu-id="ed97c-115">Dal Pannello di endpoint rete CDN hello, fare clic sul pulsante Carica hello.</span><span class="sxs-lookup"><span data-stu-id="ed97c-115">From hello CDN endpoint blade, click hello load button.</span></span>
   
    ![Pannello dell'endpoint della rete CDN](./media/cdn-preload-endpoint/cdn-endpoint-blade.png)
   
    <span data-ttu-id="ed97c-117">Apre il pannello di carico Hello.</span><span class="sxs-lookup"><span data-stu-id="ed97c-117">hello Load blade opens.</span></span>
   
    ![Pannello di caricamento della rete CDN](./media/cdn-preload-endpoint/cdn-load-blade.png)
4. <span data-ttu-id="ed97c-119">Immettere il percorso completo di hello di ciascuna risorsa desiderato tooload (ad esempio, `/pictures/kitten.png`) in hello **percorso** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="ed97c-119">Enter hello full path of each asset you wish tooload (e.g., `/pictures/kitten.png`) in hello **Path** textbox.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="ed97c-120">Ulteriori **percorso** nelle caselle di testo verrà visualizzato dopo l'immissione di testo tooallow si toobuild un elenco di più risorse.</span><span class="sxs-lookup"><span data-stu-id="ed97c-120">More **Path** textboxes will appear after you enter text tooallow you toobuild a list of multiple assets.</span></span>  <span data-ttu-id="ed97c-121">È possibile eliminare l'asset dall'elenco hello facendo clic sul pulsante con puntini di sospensione (…) hello.</span><span class="sxs-lookup"><span data-stu-id="ed97c-121">You can delete assets from hello list by clicking hello ellipsis (...) button.</span></span>
   > 
   > <span data-ttu-id="ed97c-122">I percorsi devono contenere un URL relativo che si adatta a seguito di hello [espressione regolare](https://msdn.microsoft.com/library/az24scfc.aspx):</span><span class="sxs-lookup"><span data-stu-id="ed97c-122">Paths must be a relative URL that fits hello following [regular expression](https://msdn.microsoft.com/library/az24scfc.aspx):</span></span>  
   > ><span data-ttu-id="ed97c-123">Caricare un singolo percorso di file `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;</span><span class="sxs-lookup"><span data-stu-id="ed97c-123">Load a single file path `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;</span></span>  
   > ><span data-ttu-id="ed97c-124">Caricare un singolo file con stringa di query `@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`</span><span class="sxs-lookup"><span data-stu-id="ed97c-124">Load a single file with query string `@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`</span></span>  
   > 
   > <span data-ttu-id="ed97c-125">Ogni asset deve avere il proprio percorso.</span><span class="sxs-lookup"><span data-stu-id="ed97c-125">Each asset must have its own path.</span></span>  <span data-ttu-id="ed97c-126">Non esiste alcuna funzionalità con caratteri jolly per il pre-caricamento degli asset.</span><span class="sxs-lookup"><span data-stu-id="ed97c-126">There is no wildcard functionality for pre-loading assets.</span></span>
   > 
   > 
   
    ![Pulsante Carica](./media/cdn-preload-endpoint/cdn-load-paths.png)
5. <span data-ttu-id="ed97c-128">Fare clic su hello **carico** pulsante.</span><span class="sxs-lookup"><span data-stu-id="ed97c-128">Click hello **Load** button.</span></span>
   
    ![Pulsante Carica](./media/cdn-preload-endpoint/cdn-load-button.png)

> [!NOTE]
> <span data-ttu-id="ed97c-130">Le richieste di caricamento sono limitate a un massimo di 10 al minuto per ogni profilo di rete CDN.</span><span class="sxs-lookup"><span data-stu-id="ed97c-130">There is a limitation of 10 load requests per minute per CDN profile.</span></span> <span data-ttu-id="ed97c-131">Sono consentiti 50 percorsi per richiesta.</span><span class="sxs-lookup"><span data-stu-id="ed97c-131">50 paths are allowed per request.</span></span> <span data-ttu-id="ed97c-132">Ogni percorso ha un limite di lunghezza di 1024 caratteri.</span><span class="sxs-lookup"><span data-stu-id="ed97c-132">Each path has a path-length limit of 1024 characters.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="ed97c-133">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="ed97c-133">See also</span></span>
* [<span data-ttu-id="ed97c-134">Ripulire un endpoint della rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="ed97c-134">Purge an Azure CDN endpoint</span></span>](cdn-purge-endpoint.md)
* [<span data-ttu-id="ed97c-135">Riferimento API REST della rete CDN di Azure - Ripulire o precaricare un endpoint</span><span class="sxs-lookup"><span data-stu-id="ed97c-135">Azure CDN REST API reference - Purge or Pre-Load an Endpoint</span></span>](https://msdn.microsoft.com/library/mt634451.aspx)

