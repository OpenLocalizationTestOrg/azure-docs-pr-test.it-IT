---
title: aaaPurge un endpoint rete CDN di Azure | Documenti Microsoft
description: Informazioni su come toopurge tutti memorizzato nella cache contenuto da un endpoint rete CDN di Azure.
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
ms.openlocfilehash: a09f4a49aa1e2d7655ecae44b5126c11c28fd599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="purge-an-azure-cdn-endpoint"></a><span data-ttu-id="7f08c-103">Ripulire un endpoint della rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="7f08c-103">Purge an Azure CDN endpoint</span></span>
## <a name="overview"></a><span data-ttu-id="7f08c-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="7f08c-104">Overview</span></span>
<span data-ttu-id="7f08c-105">Nodi di bordo della rete CDN Azure vengono memorizzati nella cache di asset fino alla scadenza time-to-live (TTL) dell'asset hello.</span><span class="sxs-lookup"><span data-stu-id="7f08c-105">Azure CDN edge nodes will cache assets until hello asset's time-to-live (TTL) expires.</span></span>  <span data-ttu-id="7f08c-106">Alla scadenza durata (TTL) dell'asset hello, quando un client richiede asset hello dal nodo edge hello, nodo edge hello recupererà una nuova copia aggiornata della richiesta client di hello asset tooserve hello e archiviare l'aggiornamento della cache di hello.</span><span class="sxs-lookup"><span data-stu-id="7f08c-106">After hello asset's TTL expires, when a client requests hello asset from hello edge node, hello edge node will retrieve a new updated copy of hello asset tooserve hello client request and store refresh hello cache.</span></span>

<span data-ttu-id="7f08c-107">Hello best practice toomake che gli utenti ottengono sempre una copia più recente di hello delle risorse è tooversion le risorse per ogni aggiornamento e pubblicano come nuovi URL.</span><span class="sxs-lookup"><span data-stu-id="7f08c-107">hello best practice toomake sure your users always obtain hello latest copy of your assets is tooversion your assets for each update and publish them as new URLs.</span></span>  <span data-ttu-id="7f08c-108">Rete CDN recupera immediatamente nuove risorse di hello per le richieste client successive hello.</span><span class="sxs-lookup"><span data-stu-id="7f08c-108">CDN will immediately retrieve hello new assets for hello next client requests.</span></span>  <span data-ttu-id="7f08c-109">In alcuni casi è preferibile toopurge memorizzati nella cache il contenuto di tutti i nodi del bordo e forzarne tutte le risorse aggiornate nuovo tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="7f08c-109">Sometimes you may wish toopurge cached content from all edge nodes and force them all tooretrieve new updated assets.</span></span>  <span data-ttu-id="7f08c-110">Potrebbe trattarsi di scadenza dell'applicazione web di tooupdates tooyour o tooquickly aggiornamento asset che contenga informazioni non corrette.</span><span class="sxs-lookup"><span data-stu-id="7f08c-110">This might be due tooupdates tooyour web application, or tooquickly update assets that contain incorrect information.</span></span>

> [!TIP]
> <span data-ttu-id="7f08c-111">Si noti che solo eliminazione Cancella hello memorizzati nella cache contenuto nel server perimetrale della rete CDN di hello.</span><span class="sxs-lookup"><span data-stu-id="7f08c-111">Note that purging only clears hello cached content on hello CDN edge servers.</span></span>  <span data-ttu-id="7f08c-112">Tutte le cache downstream, ad esempio i server proxy e cache locale del browser, possono comunque contenere una copia memorizzata nella cache del file hello.</span><span class="sxs-lookup"><span data-stu-id="7f08c-112">Any downstream caches, such as proxy servers and local browser caches, may still hold a cached copy of hello file.</span></span>  <span data-ttu-id="7f08c-113">È importante tooremember questo quando si imposta un file time-to-live.</span><span class="sxs-lookup"><span data-stu-id="7f08c-113">It's important tooremember this when you set a file's time-to-live.</span></span>  <span data-ttu-id="7f08c-114">È possibile forzare una versione più recente di hello toorequest client downstream del file, assegnargli un nome univoco che ogni volta che si aggiornarlo o sfruttando [la memorizzazione nella cache di stringa di query](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="7f08c-114">You can force a downstream client toorequest hello latest version of your file by giving it a unique name every time you update it, or by taking advantage of [query string caching](cdn-query-string.md).</span></span>  
> 
> 

<span data-ttu-id="7f08c-115">Questa esercitazione illustra l'eliminazione dagli asset di tutti i nodi periodici di un endpoint.</span><span class="sxs-lookup"><span data-stu-id="7f08c-115">This tutorial walks you through purging assets from all edge nodes of an endpoint.</span></span>

## <a name="walkthrough"></a><span data-ttu-id="7f08c-116">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="7f08c-116">Walkthrough</span></span>
1. <span data-ttu-id="7f08c-117">In hello [portale Azure](https://portal.azure.com), selezionare il profilo CDN toohello contenente hello endpoint desiderato toopurge.</span><span class="sxs-lookup"><span data-stu-id="7f08c-117">In hello [Azure Portal](https://portal.azure.com), browse toohello CDN profile containing hello endpoint you wish toopurge.</span></span>
2. <span data-ttu-id="7f08c-118">Dal Pannello di profilo CDN hello, fare clic sul pulsante di eliminazione hello di seguito.</span><span class="sxs-lookup"><span data-stu-id="7f08c-118">From hello CDN profile blade, click hello purge button.</span></span>
   
    ![Pannello del profilo di rete CDN](./media/cdn-purge-endpoint/cdn-profile-blade.png)
   
    <span data-ttu-id="7f08c-120">verrà visualizzata la finestra di blade Purge Hello.</span><span class="sxs-lookup"><span data-stu-id="7f08c-120">hello Purge blade opens.</span></span>
   
    ![Pannello di eliminazione della rete CDN](./media/cdn-purge-endpoint/cdn-purge-blade.png)
3. <span data-ttu-id="7f08c-122">In hello ripulire pannello, selezionare l'indirizzo del servizio hello desiderato toopurge dall'elenco a discesa URL hello.</span><span class="sxs-lookup"><span data-stu-id="7f08c-122">On hello Purge blade, select hello service address you wish toopurge from hello URL dropdown.</span></span>
   
    ![Maschera di eliminazione](./media/cdn-purge-endpoint/cdn-purge-form.png)
   
   > [!NOTE]
   > <span data-ttu-id="7f08c-124">È inoltre possibile ottenere toohello eliminazione pannello facendo hello **ripulire** pulsante sul pannello endpoint rete CDN di hello.</span><span class="sxs-lookup"><span data-stu-id="7f08c-124">You can also get toohello Purge blade by clicking hello **Purge** button on hello CDN endpoint blade.</span></span>  <span data-ttu-id="7f08c-125">In tal caso, hello **URL** campo sarà già popolato con l'indirizzo del servizio hello di quell'endpoint specifico.</span><span class="sxs-lookup"><span data-stu-id="7f08c-125">In that case, hello **URL** field will be pre-populated with hello service address of that specific endpoint.</span></span>
   > 
   > 
4. <span data-ttu-id="7f08c-126">Selezionare le risorse desiderate toopurge da hello nodi periferici.</span><span class="sxs-lookup"><span data-stu-id="7f08c-126">Select what assets you wish toopurge from hello edge nodes.</span></span>  <span data-ttu-id="7f08c-127">Se si desiderano tooclear tutte le risorse, fare clic su hello **Ripulisci** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="7f08c-127">If you wish tooclear all assets, click hello **Purge all** checkbox.</span></span>  <span data-ttu-id="7f08c-128">In caso contrario, tipo hello percorso di ogni asset da cui toopurge in hello **percorso** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="7f08c-128">Otherwise, type hello path of each asset you wish toopurge in hello **Path** textbox.</span></span> <span data-ttu-id="7f08c-129">Formati di seguito sono supportate nel percorso di hello.</span><span class="sxs-lookup"><span data-stu-id="7f08c-129">Below formats are supported in hello path.</span></span>
    1. <span data-ttu-id="7f08c-130">**Eliminazione di URL singolo**: Elimina una singola risorsa specificando l'URL completo di hello, con o senza estensione file hello, ad esempio,`/pictures/strasbourg.png`;`/pictures/strasbourg`</span><span class="sxs-lookup"><span data-stu-id="7f08c-130">**Single URL purge**: Purge individual asset by specifying hello full URL, with or without hello file extension, e.g.,`/pictures/strasbourg.png`; `/pictures/strasbourg`</span></span>
    2. <span data-ttu-id="7f08c-131">**Wildcard purge**: (Eliminazione dei caratteri jolly) l'asterisco (\*) può essere usato come carattere jolly.</span><span class="sxs-lookup"><span data-stu-id="7f08c-131">**Wildcard purge**: Asterisk (\*) may be used as a wildcard.</span></span> <span data-ttu-id="7f08c-132">Eliminare tutte le cartelle, sottocartelle e file in un endpoint con `/*` hello percorso oppure eliminare tutte le sottocartelle e file in una cartella specifica specificando cartella hello seguita da `/*`, ad esempio,`/pictures/*`.</span><span class="sxs-lookup"><span data-stu-id="7f08c-132">Purge all folders, sub-folders and files under an endpoint with `/*` in hello path or purge all sub-folders and files under a specific folder by specifying hello folder followed by `/*`, e.g.,`/pictures/*`.</span></span>  <span data-ttu-id="7f08c-133">Si noti che l'eliminazione dei caratteri jolly non è attualmente supportata dalla rete CDN di Azure fornita da Akamai.</span><span class="sxs-lookup"><span data-stu-id="7f08c-133">Note that wildcard purge is not supported by Azure CDN from Akamai currently.</span></span> 
    3. <span data-ttu-id="7f08c-134">**Eliminazione di dominio radice**: radice hello di eliminazione dell'endpoint hello con "/" nel percorso di hello.</span><span class="sxs-lookup"><span data-stu-id="7f08c-134">**Root domain purge**: Purge hello root of hello endpoint with "/" in hello path.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="7f08c-135">I percorsi devono essere specificati per l'eliminazione e deve essere un URL relativo che rientrano seguente hello [espressione regolare](https://msdn.microsoft.com/library/az24scfc.aspx).</span><span class="sxs-lookup"><span data-stu-id="7f08c-135">Paths must be specified for purge and must be a relative URL that fit hello following [regular expression](https://msdn.microsoft.com/library/az24scfc.aspx).</span></span> <span data-ttu-id="7f08c-136">Le funzioni **Elimina tutti** e **Wildcard purge** (Eliminazione dei caratteri jolly) non sono attualmente supportate con la **rete CDN di Azure fornita da Akamai**.</span><span class="sxs-lookup"><span data-stu-id="7f08c-136">**Purge all** and **Wildcard purge** not supported by **Azure CDN from Akamai** currently.</span></span>
   > > <span data-ttu-id="7f08c-137">Single URL purge (Eliminazione di un URL singolo) `@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`</span><span class="sxs-lookup"><span data-stu-id="7f08c-137">Single URL purge `@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`</span></span>  
   > > <span data-ttu-id="7f08c-138">Stringa di query `@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`</span><span class="sxs-lookup"><span data-stu-id="7f08c-138">Query string `@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`</span></span>  
   > > <span data-ttu-id="7f08c-139">Wildcard purge (Eliminazione dei caratteri jolly) `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`.</span><span class="sxs-lookup"><span data-stu-id="7f08c-139">Wildcard purge `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`.</span></span> 
   > 
   > <span data-ttu-id="7f08c-140">Ulteriori **percorso** nelle caselle di testo verrà visualizzato dopo l'immissione di testo tooallow si toobuild un elenco di più risorse.</span><span class="sxs-lookup"><span data-stu-id="7f08c-140">More **Path** textboxes will appear after you enter text tooallow you toobuild a list of multiple assets.</span></span>  <span data-ttu-id="7f08c-141">È possibile eliminare l'asset dall'elenco hello facendo clic sul pulsante con puntini di sospensione (…) hello.</span><span class="sxs-lookup"><span data-stu-id="7f08c-141">You can delete assets from hello list by clicking hello ellipsis (...) button.</span></span>
   > 
5. <span data-ttu-id="7f08c-142">Fare clic su hello **ripulire** pulsante.</span><span class="sxs-lookup"><span data-stu-id="7f08c-142">Click hello **Purge** button.</span></span>
   
    ![Pulsante di eliminazione](./media/cdn-purge-endpoint/cdn-purge-button.png)

> [!IMPORTANT]
> <span data-ttu-id="7f08c-144">Eliminare le richieste richiedere circa 2-3 minuti tooprocess con **rete CDN di Azure da Verizon** (Standard e Premium) e circa 7 minuti con **rete CDN di Azure da Akamai**.</span><span class="sxs-lookup"><span data-stu-id="7f08c-144">Purge requests take approximately 2-3 minutes tooprocess with **Azure CDN from Verizon** (Standard and Premium), and approximately 7 minutes with **Azure CDN from Akamai**.</span></span>  <span data-ttu-id="7f08c-145">La rete CDN di Azure ha un limite di 50 richieste di eliminazione simultanee in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="7f08c-145">Azure CDN has a limit of 50 concurrent purge requests at any given time.</span></span> 
> 
> 

## <a name="see-also"></a><span data-ttu-id="7f08c-146">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="7f08c-146">See also</span></span>
* [<span data-ttu-id="7f08c-147">Precaricamento di risorse in un endpoint della rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="7f08c-147">Pre-load assets on an Azure CDN endpoint</span></span>](cdn-preload-endpoint.md)
* [<span data-ttu-id="7f08c-148">Riferimento API REST della rete CDN di Azure - Ripulire o precaricare un endpoint</span><span class="sxs-lookup"><span data-stu-id="7f08c-148">Azure CDN REST API reference - Purge or Pre-Load an Endpoint</span></span>](https://msdn.microsoft.com/library/mt634451.aspx)

