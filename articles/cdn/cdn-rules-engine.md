---
title: Eseguire l'override del comportamento HTTP con il motore regole della rete CDN di Azure | Documentazione Microsoft
description: "Il motore regole consente di personalizzare la modalità con cui vengono gestite le richieste HTTP nella rete CDN di Azure, ad esempio la distribuzione di determinati tipi di contenuto, la definizione di criteri di memorizzazione nella cache e la modifica delle intestazioni HTTP."
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
ms.openlocfilehash: abfe283476206b181018d187675b47112dc5ad2f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="override-http-behavior-using-the-azure-cdn-rules-engine"></a><span data-ttu-id="9f020-103">Eseguire l'override del comportamento HTTP con il motore regole della rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="9f020-103">Override HTTP behavior using the Azure CDN rules engine</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="9f020-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="9f020-104">Overview</span></span>
<span data-ttu-id="9f020-105">Il motore regole consente di personalizzare la modalità con cui vengono gestite le richieste HTTP, come ad esempio il blocco della distribuzione di determinati tipi di contenuto, la definizione di un criterio di memorizzazione nella cache e la modifica della intestazioni HTTP.</span><span class="sxs-lookup"><span data-stu-id="9f020-105">The rules engine allows you to customize how HTTP requests are handled, such as blocking the delivery of certain types of content, defining a caching policy, and modifying HTTP headers.</span></span>  <span data-ttu-id="9f020-106">Questa esercitazione illustra la creazione di una regola che modifica il comportamento di memorizzazione nella cache degli asset della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="9f020-106">This tutorial will demonstrate creating a rule that will change the caching behavior of CDN assets.</span></span>  <span data-ttu-id="9f020-107">Nella sezione "[Vedere anche](#see-also)" sono disponibili anche contenuti video.</span><span class="sxs-lookup"><span data-stu-id="9f020-107">There's also video content available in the "[See also](#see-also)" section.</span></span>

   > [!TIP] 
   > <span data-ttu-id="9f020-108">Per informazioni dettagliate sulla sintassi, vedere le [informazioni di riferimento sul motore regole](cdn-rules-engine-reference.md).</span><span class="sxs-lookup"><span data-stu-id="9f020-108">For a reference to the syntax in detail, see [Rules Engine Reference](cdn-rules-engine-reference.md).</span></span>
   > 


## <a name="tutorial"></a><span data-ttu-id="9f020-109">Esercitazione</span><span class="sxs-lookup"><span data-stu-id="9f020-109">Tutorial</span></span>
1. <span data-ttu-id="9f020-110">Dal pannello del profilo della rete CDN fare clic sul pulsante **Gestisci** .</span><span class="sxs-lookup"><span data-stu-id="9f020-110">From the CDN profile blade, click the **Manage** button.</span></span>
   
    ![Pulsante Gestisci pannello del profilo di rete CDN](./media/cdn-rules-engine/cdn-manage-btn.png)
   
    <span data-ttu-id="9f020-112">Si aprirà il portale di gestione della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="9f020-112">The CDN management portal opens.</span></span>
2. <span data-ttu-id="9f020-113">Fare clic sulla scheda **HTTP Large** (HTTP esteso) e quindi su **Motore regole**.</span><span class="sxs-lookup"><span data-stu-id="9f020-113">Click on the **HTTP Large** tab, followed by **Rules Engine**.</span></span>
   
    <span data-ttu-id="9f020-114">Vengono visualizzate le opzioni per una nuova regola.</span><span class="sxs-lookup"><span data-stu-id="9f020-114">Options for a new rule are displayed.</span></span>
   
    ![Opzioni delle regole della nuova rete CDN](./media/cdn-rules-engine/cdn-new-rule.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="9f020-116">L'ordine in cui sono elencate più regole influisce sulla modalità di gestione.</span><span class="sxs-lookup"><span data-stu-id="9f020-116">The order in which multiple rules are listed affects how they are handled.</span></span> <span data-ttu-id="9f020-117">Una regola successiva potrebbe seguire l’override delle azioni specificate da una regola precedente.</span><span class="sxs-lookup"><span data-stu-id="9f020-117">A subsequent rule may override the actions specified by a previous rule.</span></span>
   > 
   > 
3. <span data-ttu-id="9f020-118">Inserire un nome per la casella di testo **Nome / Descrizione** .</span><span class="sxs-lookup"><span data-stu-id="9f020-118">Enter a name in the **Name / Description** textbox.</span></span>
4. <span data-ttu-id="9f020-119">Identificare il tipo di richieste che a cui verrà applicata la regola.</span><span class="sxs-lookup"><span data-stu-id="9f020-119">Identify the type of requests the rule will apply to.</span></span>  <span data-ttu-id="9f020-120">Per impostazione predefinita, viene selezionata la condizione corrispondente **Sempre** .</span><span class="sxs-lookup"><span data-stu-id="9f020-120">By default, the **Always** match condition is selected.</span></span>  <span data-ttu-id="9f020-121">Si utilizzerà **Sempre** per questa esercitazione, quindi lasciarla selezionata.</span><span class="sxs-lookup"><span data-stu-id="9f020-121">You'll use **Always** for this tutorial, so leave that selected.</span></span>
   
   ![Condizione di corrispondenza della rete CDN](./media/cdn-rules-engine/cdn-request-type.png)
   
   > [!TIP]
   > <span data-ttu-id="9f020-123">Vi sono molti tipi di condizioni di corrispondenza disponibili nell'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="9f020-123">There are many types of match conditions available in the dropdown.</span></span>  <span data-ttu-id="9f020-124">Facendo clic sull'icona blu delle informazioni a sinistra della condizione di corrispondenza viene illustrata la condizione selezionata in modo dettagliato.</span><span class="sxs-lookup"><span data-stu-id="9f020-124">Clicking on the blue informational icon to the left of the match condition will explain the currently selected condition in detail.</span></span>
   > 
   >  <span data-ttu-id="9f020-125">Per l'elenco completo e dettagliato delle espressioni condizionali, vedere l'articolo relativo alle [espressioni condizionali del motore regole](cdn-rules-engine-reference-match-conditions.md).</span><span class="sxs-lookup"><span data-stu-id="9f020-125">For the full list of conditional expressions in detail, see [Rules Engine Conditional Expressions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   >  
   > <span data-ttu-id="9f020-126">Per l'elenco completo e dettagliato delle condizioni di corrispondenza, vedere l'articolo relativo alle [condizioni di corrispondenza del motore regole](cdn-rules-engine-reference-match-conditions.md).</span><span class="sxs-lookup"><span data-stu-id="9f020-126">For the full list of match conditions in detail, see [Rules Engine Match Conditions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   > 
   > 
5. <span data-ttu-id="9f020-127">Fare clic sul pulsante **+** accanto a **Funzionalità** per aggiungere una nuova funzionalità.</span><span class="sxs-lookup"><span data-stu-id="9f020-127">Click the **+** button next to **Features** to add a new feature.</span></span>  <span data-ttu-id="9f020-128">Nell'elenco a discesa a sinistra, selezionare **Forza interna Max-Age**.</span><span class="sxs-lookup"><span data-stu-id="9f020-128">In the dropdown on the left, select **Force Internal Max-Age**.</span></span>  <span data-ttu-id="9f020-129">Nella casella di testo che viene visualizzata, inserire **300**.</span><span class="sxs-lookup"><span data-stu-id="9f020-129">In the textbox that appears, enter **300**.</span></span>  <span data-ttu-id="9f020-130">Lasciare i valori predefiniti restanti.</span><span class="sxs-lookup"><span data-stu-id="9f020-130">Leave the remaining default values.</span></span>
   
   ![Funzionalità della rete CDN](./media/cdn-rules-engine/cdn-new-feature.png)
   
   > [!NOTE]
   > <span data-ttu-id="9f020-132">Come con le condizioni di corrispondenza, fare clic sull'icona blu delle informazioni a sinistra della nuova funzionalità per visualizzare i dettagli su questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="9f020-132">As with match conditions, clicking the blue informational icon to the left of the new feature will display details about this feature.</span></span>  <span data-ttu-id="9f020-133">Nel caso di **Force Internal Max-Age** (Forza validità massima interna), viene eseguito l'override delle intestazioni **Cache-Control** ed **Expires** dell'asset per controllare quando il nodo perimetrale della rete CDN aggiornerà l'asset dall'origine.</span><span class="sxs-lookup"><span data-stu-id="9f020-133">In the case of **Force Internal Max-Age**, we are overriding the asset's **Cache-Control** and **Expires** headers to control when the CDN edge node will refresh the asset from the origin.</span></span>  <span data-ttu-id="9f020-134">L’esempio di 300 secondi indica che il nodo edge della rete CDN memorizza l’asset nella cache per 5 minuti prima di aggiornare la risorsa dall'origine.</span><span class="sxs-lookup"><span data-stu-id="9f020-134">Our example of 300 seconds means the CDN edge node will cache the asset for 5 minutes before refreshing the asset from its origin.</span></span>
   > 
   > <span data-ttu-id="9f020-135">Per l'elenco completo e dettagliato delle funzionalità, vedere l'articolo contenente [informazioni dettagliate sulle funzionalità del motore regole](cdn-rules-engine-reference-features.md).</span><span class="sxs-lookup"><span data-stu-id="9f020-135">For the full list of features in detail, see [Rules Engine Feature Details](cdn-rules-engine-reference-features.md).</span></span>
   > 
   > 
6. <span data-ttu-id="9f020-136">Fare clic sul pulsante **Aggiungi** per salvare la nuova regola.</span><span class="sxs-lookup"><span data-stu-id="9f020-136">Click the **Add** button to save the new rule.</span></span>  <span data-ttu-id="9f020-137">La nuova regola ora è in attesa di approvazione.</span><span class="sxs-lookup"><span data-stu-id="9f020-137">The new rule is now awaiting approval.</span></span> <span data-ttu-id="9f020-138">Dopo l'approvazione, lo stato viene modificato da **Pending XML** (XML in sospeso) a **Active XML** (XML attivo).</span><span class="sxs-lookup"><span data-stu-id="9f020-138">Once it has been approved, the status will change from **Pending XML** to **Active XML**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="9f020-139">La propagazione delle modifiche delle regole in tutta la rete CDN può durare fino a 90 minuti.</span><span class="sxs-lookup"><span data-stu-id="9f020-139">Rules changes may take up to 90 minutes to propagate through the CDN.</span></span>
   > 
   > 

## <a name="see-also"></a><span data-ttu-id="9f020-140">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="9f020-140">See also</span></span>
* [<span data-ttu-id="9f020-141">Panoramica della rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="9f020-141">Azure CDN Overview</span></span>](cdn-overview.md)
* [<span data-ttu-id="9f020-142">Informazioni di riferimento sul motore regole</span><span class="sxs-lookup"><span data-stu-id="9f020-142">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="9f020-143">Condizioni di corrispondenza del motore regole</span><span class="sxs-lookup"><span data-stu-id="9f020-143">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="9f020-144">Espressioni condizionali del motore regole</span><span class="sxs-lookup"><span data-stu-id="9f020-144">Rules Engine Conditional Expressions</span></span>](cdn-rules-engine-reference-conditional-expressions.md)
* [<span data-ttu-id="9f020-145">Funzionalità del motore regole</span><span class="sxs-lookup"><span data-stu-id="9f020-145">Rules Engine Features</span></span>](cdn-rules-engine-reference-features.md)
* [<span data-ttu-id="9f020-146">Override del comportamento HTTP predefinito mediante il motore di regole</span><span class="sxs-lookup"><span data-stu-id="9f020-146">Overriding default HTTP behavior using the rules engine</span></span>](cdn-rules-engine.md)
* <span data-ttu-id="9f020-147">[Vedere il video relativo alle nuove potenti funzionalità Premium della rete CDN di Azure](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/)</span><span class="sxs-lookup"><span data-stu-id="9f020-147">[Azure Fridays: Azure CDN's powerful new Premium Features](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (video)</span></span>