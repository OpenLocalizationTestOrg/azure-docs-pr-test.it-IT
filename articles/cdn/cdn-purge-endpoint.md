---
title: Ripulire un endpoint della rete CDN di Azure | Microsoft Docs
description: Informazioni su come ripulire tutto il contenuto memorizzato nella cache da un endpoint della rete CDN di Azure.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 0b50230b-fe82-4740-90aa-95d4dde8bd4f
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: b035c232bb58d653960190d4974cc3789d55a51d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="purge-an-azure-cdn-endpoint"></a><span data-ttu-id="820c3-103">Ripulire un endpoint della rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="820c3-103">Purge an Azure CDN endpoint</span></span>
## <a name="overview"></a><span data-ttu-id="820c3-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="820c3-104">Overview</span></span>
<span data-ttu-id="820c3-105">I nodi perimetrali della rete CDN di Azure memorizzeranno nella cache gli asset fino alla scadenza della durata TTL dell'asset.</span><span class="sxs-lookup"><span data-stu-id="820c3-105">Azure CDN edge nodes will cache assets until the asset's time-to-live (TTL) expires.</span></span>  <span data-ttu-id="820c3-106">Dopo la scadenza della durata TTL dell'asset, quando un client richiede l'asset dal nodo periodico, questo recupera una nuova copia aggiornata dell'asset per soddisfare la richiesta del client e aggiornare la cache.</span><span class="sxs-lookup"><span data-stu-id="820c3-106">After the asset's TTL expires, when a client requests the asset from the edge node, the edge node will retrieve a new updated copy of the asset to serve the client request and store refresh the cache.</span></span>

<span data-ttu-id="820c3-107">La procedura consigliata per assicurarsi che gli utenti ottengano sempre la copia più recente degli asset consiste nel versioning di questi ultimi per ogni aggiornamento e nella relativa pubblicazione come nuovi URL.</span><span class="sxs-lookup"><span data-stu-id="820c3-107">The best practice to make sure your users always obtain the latest copy of your assets is to version your assets for each update and publish them as new URLs.</span></span>  <span data-ttu-id="820c3-108">La rete CDN recupera immediatamente i nuovi asset per le richieste client successive.</span><span class="sxs-lookup"><span data-stu-id="820c3-108">CDN will immediately retrieve the new assets for the next client requests.</span></span>  <span data-ttu-id="820c3-109">A volte si desidera ripulire il contenuto memorizzato nella cache da tutti i nodi periodici e forzare il recupero dei nuovi asset aggiornati.</span><span class="sxs-lookup"><span data-stu-id="820c3-109">Sometimes you may wish to purge cached content from all edge nodes and force them all to retrieve new updated assets.</span></span>  <span data-ttu-id="820c3-110">Ciò potrebbe essere dovuto agli aggiornamenti all'applicazione Web o a un aggiornamento rapido di asset che contengono informazioni non corrette.</span><span class="sxs-lookup"><span data-stu-id="820c3-110">This might be due to updates to your web application, or to quickly update assets that contain incorrect information.</span></span>

> [!TIP]
> <span data-ttu-id="820c3-111">Solo la cancellazione svuota il contenuto della cache sui server perimetrali della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="820c3-111">Note that purging only clears the cached content on the CDN edge servers.</span></span>  <span data-ttu-id="820c3-112">Tutte le cache downstream, ad esempio le cache dei server proxy e del browser locale, possono comunque mantenere una copia del file nella cache.</span><span class="sxs-lookup"><span data-stu-id="820c3-112">Any downstream caches, such as proxy servers and local browser caches, may still hold a cached copy of the file.</span></span>  <span data-ttu-id="820c3-113">È importante tenerlo presente quando si imposta la durata di un file.</span><span class="sxs-lookup"><span data-stu-id="820c3-113">It's important to remember this when you set a file's time-to-live.</span></span>  <span data-ttu-id="820c3-114">È possibile forzare un client downstream per richiedere la versione più recente del file assegnandogli un nome univoco ogni volta che viene aggiornato o sfruttando la [memorizzazione nella cache delle stringhe di query](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="820c3-114">You can force a downstream client to request the latest version of your file by giving it a unique name every time you update it, or by taking advantage of [query string caching](cdn-query-string.md).</span></span>  
> 
> 

<span data-ttu-id="820c3-115">Questa esercitazione illustra l'eliminazione dagli asset di tutti i nodi periodici di un endpoint.</span><span class="sxs-lookup"><span data-stu-id="820c3-115">This tutorial walks you through purging assets from all edge nodes of an endpoint.</span></span>

## <a name="walkthrough"></a><span data-ttu-id="820c3-116">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="820c3-116">Walkthrough</span></span>
1. <span data-ttu-id="820c3-117">Nel [portale di Azure](https://portal.azure.com)passare al profilo di rete CDN contenente l'endpoint che si desidera ripulire.</span><span class="sxs-lookup"><span data-stu-id="820c3-117">In the [Azure Portal](https://portal.azure.com), browse to the CDN profile containing the endpoint you wish to purge.</span></span>
2. <span data-ttu-id="820c3-118">Nel pannello relativo al profilo di rete CDN fare clic sul pulsante di eliminazione.</span><span class="sxs-lookup"><span data-stu-id="820c3-118">From the CDN profile blade, click the purge button.</span></span>
   
    ![Pannello del profilo di rete CDN](./media/cdn-purge-endpoint/cdn-profile-blade.png)
   
    <span data-ttu-id="820c3-120">Viene visualizzato il pannello di eliminazione.</span><span class="sxs-lookup"><span data-stu-id="820c3-120">The Purge blade opens.</span></span>
   
    ![Pannello di eliminazione della rete CDN](./media/cdn-purge-endpoint/cdn-purge-blade.png)
3. <span data-ttu-id="820c3-122">Nel pannello di eliminazione selezionare l'indirizzo del servizio che si desidera ripulire dall'elenco a discesa degli URL.</span><span class="sxs-lookup"><span data-stu-id="820c3-122">On the Purge blade, select the service address you wish to purge from the URL dropdown.</span></span>
   
    ![Maschera di eliminazione](./media/cdn-purge-endpoint/cdn-purge-form.png)
   
   > [!NOTE]
   > <span data-ttu-id="820c3-124">È possibile visualizzare il pannello di eliminazione anche facendo clic sul pulsante **Elimina** nel pannello dell'endpoint della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="820c3-124">You can also get to the Purge blade by clicking the **Purge** button on the CDN endpoint blade.</span></span>  <span data-ttu-id="820c3-125">In tal caso, il campo **URL** sarà prepopolato con l'indirizzo del servizio dell'endpoint specifico.</span><span class="sxs-lookup"><span data-stu-id="820c3-125">In that case, the **URL** field will be pre-populated with the service address of that specific endpoint.</span></span>
   > 
   > 
4. <span data-ttu-id="820c3-126">Selezionare gli asset che si desidera ripulire dai nodi periferici.</span><span class="sxs-lookup"><span data-stu-id="820c3-126">Select what assets you wish to purge from the edge nodes.</span></span>  <span data-ttu-id="820c3-127">Se si desidera ripulire tutti gli asset, fare clic sulla casella di controllo **Elimina tutto** .</span><span class="sxs-lookup"><span data-stu-id="820c3-127">If you wish to clear all assets, click the **Purge all** checkbox.</span></span>  <span data-ttu-id="820c3-128">In alternativa digitare il percorso di ogni asset che si vuole eliminare nella casella di testo **Percorso**.</span><span class="sxs-lookup"><span data-stu-id="820c3-128">Otherwise, type the path of each asset you wish to purge in the **Path** textbox.</span></span> <span data-ttu-id="820c3-129">I formati seguenti sono supportati nel percorso.</span><span class="sxs-lookup"><span data-stu-id="820c3-129">Below formats are supported in the path.</span></span>
    1. <span data-ttu-id="820c3-130">**Single URL purge**: (Eliminazione di un URL singolo) eliminazione di un singolo asset specificando l'URL completo, con o senza l'estensione di file, ad esempio `/pictures/strasbourg.png`; `/pictures/strasbourg`</span><span class="sxs-lookup"><span data-stu-id="820c3-130">**Single URL purge**: Purge individual asset by specifying the full URL, with or without the file extension, e.g.,`/pictures/strasbourg.png`; `/pictures/strasbourg`</span></span>
    2. <span data-ttu-id="820c3-131">**Wildcard purge**: (Eliminazione dei caratteri jolly) l'asterisco (\*) può essere usato come carattere jolly.</span><span class="sxs-lookup"><span data-stu-id="820c3-131">**Wildcard purge**: Asterisk (\*) may be used as a wildcard.</span></span> <span data-ttu-id="820c3-132">Consente di eliminare tutte le cartelle, le sottocartelle e i file in un endpoint inserendo `/*` nel percorso o di eliminare tutte le sottocartelle e i file in una determinata cartella specificando la cartella seguita da `/*`, ad esempio `/pictures/*`.</span><span class="sxs-lookup"><span data-stu-id="820c3-132">Purge all folders, sub-folders and files under an endpoint with `/*` in the path or purge all sub-folders and files under a specific folder by specifying the folder followed by `/*`, e.g.,`/pictures/*`.</span></span>  <span data-ttu-id="820c3-133">Si noti che l'eliminazione dei caratteri jolly non è attualmente supportata dalla rete CDN di Azure fornita da Akamai.</span><span class="sxs-lookup"><span data-stu-id="820c3-133">Note that wildcard purge is not supported by Azure CDN from Akamai currently.</span></span> 
    3. <span data-ttu-id="820c3-134">**Root domain purge**: (Eliminazione del dominio radice) consente di eliminare la radice dell'endpoint inserendo "/" nel percorso.</span><span class="sxs-lookup"><span data-stu-id="820c3-134">**Root domain purge**: Purge the root of the endpoint with "/" in the path.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="820c3-135">Per l'eliminazione, è necessario che i percorsi vengano specificati e che siano un URL relativo che soddisfi l'[espressione regolare](https://msdn.microsoft.com/library/az24scfc.aspx) seguente.</span><span class="sxs-lookup"><span data-stu-id="820c3-135">Paths must be specified for purge and must be a relative URL that fit the following [regular expression](https://msdn.microsoft.com/library/az24scfc.aspx).</span></span> <span data-ttu-id="820c3-136">Le funzioni **Elimina tutti** e **Wildcard purge** (Eliminazione dei caratteri jolly) non sono attualmente supportate con la **rete CDN di Azure fornita da Akamai**.</span><span class="sxs-lookup"><span data-stu-id="820c3-136">**Purge all** and **Wildcard purge** not supported by **Azure CDN from Akamai** currently.</span></span>
   > > <span data-ttu-id="820c3-137">Single URL purge (Eliminazione di un URL singolo) `@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`</span><span class="sxs-lookup"><span data-stu-id="820c3-137">Single URL purge `@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`</span></span>  
   > > <span data-ttu-id="820c3-138">Stringa di query `@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`</span><span class="sxs-lookup"><span data-stu-id="820c3-138">Query string `@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`</span></span>  
   > > <span data-ttu-id="820c3-139">Wildcard purge (Eliminazione dei caratteri jolly) `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`.</span><span class="sxs-lookup"><span data-stu-id="820c3-139">Wildcard purge `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`.</span></span> 
   > 
   > <span data-ttu-id="820c3-140">Dopo l'immissione di testo verranno visualizzate altre caselle di testo **Percorso** che consentono di compilare un elenco di più asset.</span><span class="sxs-lookup"><span data-stu-id="820c3-140">More **Path** textboxes will appear after you enter text to allow you to build a list of multiple assets.</span></span>  <span data-ttu-id="820c3-141">È possibile eliminare gli asset dall'elenco facendo clic sul pulsante con i puntini di sospensione (...).</span><span class="sxs-lookup"><span data-stu-id="820c3-141">You can delete assets from the list by clicking the ellipsis (...) button.</span></span>
   > 
5. <span data-ttu-id="820c3-142">Fare clic sul pulsante **Elimina** .</span><span class="sxs-lookup"><span data-stu-id="820c3-142">Click the **Purge** button.</span></span>
   
    ![Pulsante di eliminazione](./media/cdn-purge-endpoint/cdn-purge-button.png)

> [!IMPORTANT]
> <span data-ttu-id="820c3-144">L'elaborazione delle richieste di eliminazione dura circa 2-3 minuti per l'elaborazione con la **rete CDN di Azure fornita da Verizon** (Standard e Premium) e circa 7 minuti con la **rete CDN di Azure fornita da Akamai**.</span><span class="sxs-lookup"><span data-stu-id="820c3-144">Purge requests take approximately 2-3 minutes to process with **Azure CDN from Verizon** (Standard and Premium), and approximately 7 minutes with **Azure CDN from Akamai**.</span></span>  <span data-ttu-id="820c3-145">La rete CDN di Azure ha un limite di 50 richieste di eliminazione simultanee in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="820c3-145">Azure CDN has a limit of 50 concurrent purge requests at any given time.</span></span> 
> 
> 

## <a name="see-also"></a><span data-ttu-id="820c3-146">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="820c3-146">See also</span></span>
* [<span data-ttu-id="820c3-147">Precaricamento di risorse in un endpoint della rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="820c3-147">Pre-load assets on an Azure CDN endpoint</span></span>](cdn-preload-endpoint.md)
* [<span data-ttu-id="820c3-148">Riferimento API REST della rete CDN di Azure - Ripulire o precaricare un endpoint</span><span class="sxs-lookup"><span data-stu-id="820c3-148">Azure CDN REST API reference - Purge or Pre-Load an Endpoint</span></span>](https://msdn.microsoft.com/library/mt634451.aspx)

