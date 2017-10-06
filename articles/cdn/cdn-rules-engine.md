---
title: il comportamento di aaaOverride HTTP mediante motore regole di hello rete CDN di Azure | Documenti Microsoft
description: motore regole di Hello consente toocustomize come richieste HTTP vengono gestite dalla rete CDN di Azure, ad esempio il blocco di recapito hello di determinati tipi di contenuto, definire un criterio di memorizzazione nella cache e modificare le intestazioni HTTP.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 625a912b-91f2-485d-8991-128cc194ee71
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: dd7194be9dbda43180c64568d3e1f52c5c513a7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="override-http-behavior-using-hello-azure-cdn-rules-engine"></a><span data-ttu-id="8a9ea-103">Override del comportamento HTTP utilizzando motore regole di hello rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="8a9ea-103">Override HTTP behavior using hello Azure CDN rules engine</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="8a9ea-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="8a9ea-104">Overview</span></span>
<span data-ttu-id="8a9ea-105">il motore regole di Hello consente toocustomize come vengono gestite le richieste HTTP, ad esempio il blocco di recapito hello di determinati tipi di contenuto, definizione di criteri di memorizzazione nella cache e la modifica delle intestazioni HTTP.</span><span class="sxs-lookup"><span data-stu-id="8a9ea-105">hello rules engine allows you toocustomize how HTTP requests are handled, such as blocking hello delivery of certain types of content, defining a caching policy, and modifying HTTP headers.</span></span>  <span data-ttu-id="8a9ea-106">In questa esercitazione verrà illustrato la creazione di una regola che verrà modificato il comportamento delle risorse di rete CDN di memorizzazione nella cache di hello.</span><span class="sxs-lookup"><span data-stu-id="8a9ea-106">This tutorial will demonstrate creating a rule that will change hello caching behavior of CDN assets.</span></span>  <span data-ttu-id="8a9ea-107">È inoltre contenuto video disponibili in hello "[vedere anche](#see-also)" sezione.</span><span class="sxs-lookup"><span data-stu-id="8a9ea-107">There's also video content available in hello "[See also](#see-also)" section.</span></span>

   > [!TIP] 
   > <span data-ttu-id="8a9ea-108">Per un riferimento toohello in modo dettagliato, vedere [riferimento motore regole](cdn-rules-engine-reference.md).</span><span class="sxs-lookup"><span data-stu-id="8a9ea-108">For a reference toohello syntax in detail, see [Rules Engine Reference](cdn-rules-engine-reference.md).</span></span>
   > 


## <a name="tutorial"></a><span data-ttu-id="8a9ea-109">Esercitazione</span><span class="sxs-lookup"><span data-stu-id="8a9ea-109">Tutorial</span></span>
1. <span data-ttu-id="8a9ea-110">Dal Pannello di profilo CDN hello, fare clic su hello **Gestisci** pulsante.</span><span class="sxs-lookup"><span data-stu-id="8a9ea-110">From hello CDN profile blade, click hello **Manage** button.</span></span>
   
    ![Pulsante Gestisci pannello del profilo di rete CDN](./media/cdn-rules-engine/cdn-manage-btn.png)
   
    <span data-ttu-id="8a9ea-112">viene visualizzato il portale di gestione della rete CDN Hello.</span><span class="sxs-lookup"><span data-stu-id="8a9ea-112">hello CDN management portal opens.</span></span>
2. <span data-ttu-id="8a9ea-113">Fare clic su hello **HTTP grandi** scheda, seguita da **motore regole di business**.</span><span class="sxs-lookup"><span data-stu-id="8a9ea-113">Click on hello **HTTP Large** tab, followed by **Rules Engine**.</span></span>
   
    <span data-ttu-id="8a9ea-114">Vengono visualizzate le opzioni per una nuova regola.</span><span class="sxs-lookup"><span data-stu-id="8a9ea-114">Options for a new rule are displayed.</span></span>
   
    ![Opzioni delle regole della nuova rete CDN](./media/cdn-rules-engine/cdn-new-rule.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="8a9ea-116">ordine di Hello in cui sono elencate più regole influisce sulla modalità di gestione.</span><span class="sxs-lookup"><span data-stu-id="8a9ea-116">hello order in which multiple rules are listed affects how they are handled.</span></span> <span data-ttu-id="8a9ea-117">Una regola successive può eseguire l'override di azioni hello specificate da una regola precedente.</span><span class="sxs-lookup"><span data-stu-id="8a9ea-117">A subsequent rule may override hello actions specified by a previous rule.</span></span>
   > 
   > 
3. <span data-ttu-id="8a9ea-118">Immettere un nome in hello **nome / descrizione** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="8a9ea-118">Enter a name in hello **Name / Description** textbox.</span></span>
4. <span data-ttu-id="8a9ea-119">Identificare il tipo di hello di hello regola verrà applicata alle richieste.</span><span class="sxs-lookup"><span data-stu-id="8a9ea-119">Identify hello type of requests hello rule will apply to.</span></span>  <span data-ttu-id="8a9ea-120">Per impostazione predefinita, hello **sempre** condizione di corrispondenza è selezionata.</span><span class="sxs-lookup"><span data-stu-id="8a9ea-120">By default, hello **Always** match condition is selected.</span></span>  <span data-ttu-id="8a9ea-121">Si utilizzerà **Sempre** per questa esercitazione, quindi lasciarla selezionata.</span><span class="sxs-lookup"><span data-stu-id="8a9ea-121">You'll use **Always** for this tutorial, so leave that selected.</span></span>
   
   ![Condizione di corrispondenza della rete CDN](./media/cdn-rules-engine/cdn-request-type.png)
   
   > [!TIP]
   > <span data-ttu-id="8a9ea-123">Esistono molti tipi di corrispondenza condizioni disponibili nell'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="8a9ea-123">There are many types of match conditions available in hello dropdown.</span></span>  <span data-ttu-id="8a9ea-124">Facendo clic su toohello icona informativa blu hello sinistra della condizione di corrispondenza hello illustrerà condizione hello attualmente selezionato in modo dettagliato.</span><span class="sxs-lookup"><span data-stu-id="8a9ea-124">Clicking on hello blue informational icon toohello left of hello match condition will explain hello currently selected condition in detail.</span></span>
   > 
   >  <span data-ttu-id="8a9ea-125">Per hello l'elenco completo delle espressioni condizionali in modo dettagliato, vedere [espressioni condizionali di motore regole](cdn-rules-engine-reference-match-conditions.md).</span><span class="sxs-lookup"><span data-stu-id="8a9ea-125">For hello full list of conditional expressions in detail, see [Rules Engine Conditional Expressions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   >  
   > <span data-ttu-id="8a9ea-126">Per hello l'elenco completo delle condizioni di corrispondenza in modo dettagliato, vedere [le condizioni corrispondono del motore regole](cdn-rules-engine-reference-match-conditions.md).</span><span class="sxs-lookup"><span data-stu-id="8a9ea-126">For hello full list of match conditions in detail, see [Rules Engine Match Conditions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   > 
   > 
5. <span data-ttu-id="8a9ea-127">Fare clic su hello  **+**  accanto troppo**funzionalità** tooadd una nuova funzionalità.</span><span class="sxs-lookup"><span data-stu-id="8a9ea-127">Click hello **+** button next too**Features** tooadd a new feature.</span></span>  <span data-ttu-id="8a9ea-128">Nell'elenco a discesa hello hello sinistra, selezionare **Force interno Max-Age**.</span><span class="sxs-lookup"><span data-stu-id="8a9ea-128">In hello dropdown on hello left, select **Force Internal Max-Age**.</span></span>  <span data-ttu-id="8a9ea-129">Nella casella di testo hello che viene visualizzata, immettere **300**.</span><span class="sxs-lookup"><span data-stu-id="8a9ea-129">In hello textbox that appears, enter **300**.</span></span>  <span data-ttu-id="8a9ea-130">Lasciare hello rimanenti valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="8a9ea-130">Leave hello remaining default values.</span></span>
   
   ![Funzionalità della rete CDN](./media/cdn-rules-engine/cdn-new-feature.png)
   
   > [!NOTE]
   > <span data-ttu-id="8a9ea-132">Come con le condizioni di corrispondenza, fare clic su toohello icona informativa blu hello a sinistra della hello nuove funzionalità saranno visualizzati i dettagli su questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="8a9ea-132">As with match conditions, clicking hello blue informational icon toohello left of hello new feature will display details about this feature.</span></span>  <span data-ttu-id="8a9ea-133">Nel caso di hello di **Force interno Max-Age**, è stato eseguito l'override dell'asset hello **Cache-Control** e **Expires** toocontrol intestazioni quando il nodo del bordo della rete CDN di hello aggiornerà hello Asset dall'origine hello.</span><span class="sxs-lookup"><span data-stu-id="8a9ea-133">In hello case of **Force Internal Max-Age**, we are overriding hello asset's **Cache-Control** and **Expires** headers toocontrol when hello CDN edge node will refresh hello asset from hello origin.</span></span>  <span data-ttu-id="8a9ea-134">Esempio di 300 secondi significa nodo del bordo di hello CDN verrà memorizzati nella cache di asset hello per 5 minuti prima di aggiornare asset hello dall'origine.</span><span class="sxs-lookup"><span data-stu-id="8a9ea-134">Our example of 300 seconds means hello CDN edge node will cache hello asset for 5 minutes before refreshing hello asset from its origin.</span></span>
   > 
   > <span data-ttu-id="8a9ea-135">Per hello l'elenco completo di funzionalità in modo dettagliato, vedere [dettagli delle funzionalità del motore regole](cdn-rules-engine-reference-features.md).</span><span class="sxs-lookup"><span data-stu-id="8a9ea-135">For hello full list of features in detail, see [Rules Engine Feature Details](cdn-rules-engine-reference-features.md).</span></span>
   > 
   > 
6. <span data-ttu-id="8a9ea-136">Fare clic su hello **Aggiungi** nuova regola di pulsante toosave hello.</span><span class="sxs-lookup"><span data-stu-id="8a9ea-136">Click hello **Add** button toosave hello new rule.</span></span>  <span data-ttu-id="8a9ea-137">nuova regola Hello ora è in attesa di approvazione.</span><span class="sxs-lookup"><span data-stu-id="8a9ea-137">hello new rule is now awaiting approval.</span></span> <span data-ttu-id="8a9ea-138">Quando è stata approvata, hello stato cambia da **XML in sospeso** troppo**XML Active**.</span><span class="sxs-lookup"><span data-stu-id="8a9ea-138">Once it has been approved, hello status will change from **Pending XML** too**Active XML**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="8a9ea-139">Le modifiche delle regole potrebbero richiedere too90 minuti toopropagate tramite hello CDN.</span><span class="sxs-lookup"><span data-stu-id="8a9ea-139">Rules changes may take up too90 minutes toopropagate through hello CDN.</span></span>
   > 
   > 

## <a name="see-also"></a><span data-ttu-id="8a9ea-140">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="8a9ea-140">See also</span></span>
* [<span data-ttu-id="8a9ea-141">Panoramica della rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="8a9ea-141">Azure CDN Overview</span></span>](cdn-overview.md)
* [<span data-ttu-id="8a9ea-142">Informazioni di riferimento sul motore regole</span><span class="sxs-lookup"><span data-stu-id="8a9ea-142">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="8a9ea-143">Condizioni di corrispondenza del motore regole</span><span class="sxs-lookup"><span data-stu-id="8a9ea-143">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="8a9ea-144">Espressioni condizionali del motore regole</span><span class="sxs-lookup"><span data-stu-id="8a9ea-144">Rules Engine Conditional Expressions</span></span>](cdn-rules-engine-reference-conditional-expressions.md)
* [<span data-ttu-id="8a9ea-145">Funzionalità del motore regole</span><span class="sxs-lookup"><span data-stu-id="8a9ea-145">Rules Engine Features</span></span>](cdn-rules-engine-reference-features.md)
* [<span data-ttu-id="8a9ea-146">Override del comportamento HTTP predefinito utilizzando il motore regole di hello</span><span class="sxs-lookup"><span data-stu-id="8a9ea-146">Overriding default HTTP behavior using hello rules engine</span></span>](cdn-rules-engine.md)
* <span data-ttu-id="8a9ea-147">[Vedere il video relativo alle nuove potenti funzionalità Premium della rete CDN di Azure](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/)</span><span class="sxs-lookup"><span data-stu-id="8a9ea-147">[Azure Fridays: Azure CDN's powerful new Premium Features](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (video)</span></span>