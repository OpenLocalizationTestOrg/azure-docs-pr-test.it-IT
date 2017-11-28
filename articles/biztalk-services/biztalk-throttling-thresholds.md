---
title: Informazioni sulla limitazione in Servizi BizTalk | Microsoft Docs
description: "Informazioni sulle soglie di limitazione delle richieste e sui relativi comportamenti di runtime per Servizi BizTalk. La limitazione delle richieste è basata sull'utilizzo della memoria e sul numero di messaggi. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: f6663cf2-cda4-4bac-855e-27d2ad5c4fa4
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 145e7470bbc01c676a1fb5856c0f9a8726e667fc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="biztalk-services-throttling"></a><span data-ttu-id="33f7c-105">Servizi BizTalk: limitazione</span><span class="sxs-lookup"><span data-stu-id="33f7c-105">BizTalk Services: Throttling</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="33f7c-106">Servizi BizTalk di Azure implementa la limitazione del servizio sulla base di due condizioni: l'utilizzo della memoria e il numero di messaggi simultanei elaborati.</span><span class="sxs-lookup"><span data-stu-id="33f7c-106">Azure BizTalk Services implements service throttling based on two conditions: memory usage and the number of simultaneous messages processing.</span></span> <span data-ttu-id="33f7c-107">In questo argomento sono elencate le soglie di limitazione e viene descritto il comportamento in fase di esecuzione quando si verifica una condizione di limitazione.</span><span class="sxs-lookup"><span data-stu-id="33f7c-107">This topic lists the throttling thresholds and describes the Runtime behavior when a throttling condition occurs.</span></span>

## <a name="throttling-thresholds"></a><span data-ttu-id="33f7c-108">Soglie di limitazione</span><span class="sxs-lookup"><span data-stu-id="33f7c-108">Throttling Thresholds</span></span>
<span data-ttu-id="33f7c-109">Nella tabella seguente sono elencate le origini e le soglie di limitazione:</span><span class="sxs-lookup"><span data-stu-id="33f7c-109">The following table lists the throttling source and thresholds:</span></span>

|  | <span data-ttu-id="33f7c-110">Descrizione</span><span class="sxs-lookup"><span data-stu-id="33f7c-110">Description</span></span> | <span data-ttu-id="33f7c-111">Soglia inferiore</span><span class="sxs-lookup"><span data-stu-id="33f7c-111">Low Threshold</span></span> | <span data-ttu-id="33f7c-112">Soglia superiore</span><span class="sxs-lookup"><span data-stu-id="33f7c-112">High Threshold</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="33f7c-113">Memoria</span><span class="sxs-lookup"><span data-stu-id="33f7c-113">Memory</span></span> |<span data-ttu-id="33f7c-114">Percentuale di memoria totale del sistema disponibile/byte file di paging.</span><span class="sxs-lookup"><span data-stu-id="33f7c-114">% of total system memory available/PageFileBytes.</span></span> <p><p><span data-ttu-id="33f7c-115">I byte totali disponibili del file di paging sono il doppio della RAM del sistema.</span><span class="sxs-lookup"><span data-stu-id="33f7c-115">Total available PageFileBytes is approximately 2 times the RAM of the system.</span></span> |<span data-ttu-id="33f7c-116">60%</span><span class="sxs-lookup"><span data-stu-id="33f7c-116">60%</span></span> |<span data-ttu-id="33f7c-117">70%</span><span class="sxs-lookup"><span data-stu-id="33f7c-117">70%</span></span> |
| <span data-ttu-id="33f7c-118">Elaborazione di messaggi</span><span class="sxs-lookup"><span data-stu-id="33f7c-118">Message Processing</span></span> |<span data-ttu-id="33f7c-119">Numero di messaggi elaborati simultaneamente</span><span class="sxs-lookup"><span data-stu-id="33f7c-119">Number of messages processing simultaneously</span></span> |<span data-ttu-id="33f7c-120">40 * numero di memorie centrali</span><span class="sxs-lookup"><span data-stu-id="33f7c-120">40 * number of cores</span></span> |<span data-ttu-id="33f7c-121">100 * numero di memorie centrali</span><span class="sxs-lookup"><span data-stu-id="33f7c-121">100 * number of cores</span></span> |

<span data-ttu-id="33f7c-122">Quando viene raggiunta una soglia superiore, Servizi BizTalk di Azure inizia la limitazione.</span><span class="sxs-lookup"><span data-stu-id="33f7c-122">When a high threshold is reached, Azure BizTalk Services starts to throttle.</span></span> <span data-ttu-id="33f7c-123">La limitazione viene interrotta quando viene raggiunta la soglia inferiore.</span><span class="sxs-lookup"><span data-stu-id="33f7c-123">Throttling stops when the low threshold is reached.</span></span> <span data-ttu-id="33f7c-124">Se ad esempio il servizio utilizza il 65% della memoria di sistema,</span><span class="sxs-lookup"><span data-stu-id="33f7c-124">For example, your service is using 65% system memory.</span></span> <span data-ttu-id="33f7c-125">non viene applicata la limitazione.</span><span class="sxs-lookup"><span data-stu-id="33f7c-125">In this situation, the service does not throttle.</span></span> <span data-ttu-id="33f7c-126">Se invece il servizio inizia a utilizzare il 70% della memoria di sistema,</span><span class="sxs-lookup"><span data-stu-id="33f7c-126">Your service starts using 70% system memory.</span></span> <span data-ttu-id="33f7c-127">viene applicata la limitazione, che continua fino a quando il servizio non utilizzerà il 60% (soglia inferiore) della memoria di sistema.</span><span class="sxs-lookup"><span data-stu-id="33f7c-127">In this situation, the service throttles and continues to throttle until the service uses 60% (low threshold) system memory.</span></span>

<span data-ttu-id="33f7c-128">Servizi BizTalk di Azure registra lo stato di limitazione (normale o limitato) e la durata della limitazione.</span><span class="sxs-lookup"><span data-stu-id="33f7c-128">Azure BizTalk Services tracks the throttling status (normal state vs. throttled state) and the throttling duration.</span></span>

## <a name="runtime-behavior"></a><span data-ttu-id="33f7c-129">Comportamento in fase di esecuzione</span><span class="sxs-lookup"><span data-stu-id="33f7c-129">Runtime Behavior</span></span>
<span data-ttu-id="33f7c-130">Quando Servizi BizTalk di Azure entra nello stato di limitazione, si verifica quanto segue:</span><span class="sxs-lookup"><span data-stu-id="33f7c-130">When Azure BizTalk Services enters a throttling state, the following occurs:</span></span>

* <span data-ttu-id="33f7c-131">La limitazione viene applicata a ogni istanza del ruolo,</span><span class="sxs-lookup"><span data-stu-id="33f7c-131">Throttling is per role instance.</span></span> <span data-ttu-id="33f7c-132">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="33f7c-132">For example:</span></span><br/>
  <span data-ttu-id="33f7c-133">IstanzaRuoloA è limitata.</span><span class="sxs-lookup"><span data-stu-id="33f7c-133">RoleInstanceA is throttling.</span></span> <span data-ttu-id="33f7c-134">IstanzaRuoloB non è limitata.</span><span class="sxs-lookup"><span data-stu-id="33f7c-134">RoleInstanceB is not throttling.</span></span> <span data-ttu-id="33f7c-135">In questa situazione, i messaggi in IstanzaRuoloB vengono elaborati come previsto.</span><span class="sxs-lookup"><span data-stu-id="33f7c-135">In this situation, messages in RoleInstanceB are processed as expected.</span></span> <span data-ttu-id="33f7c-136">I messaggi in IstanzaRuoloA vengono rimossi e non vengono eseguiti con l'errore seguente:</span><span class="sxs-lookup"><span data-stu-id="33f7c-136">Messages in RoleInstanceA are discarded and fail with the following error:</span></span><br/><br/><span data-ttu-id="33f7c-137">
  **Il server è occupato. Riprovare più tardi.**</span><span class="sxs-lookup"><span data-stu-id="33f7c-137">
**Server is busy. Please try again.**</span></span><br/><br/>
* <span data-ttu-id="33f7c-138">Nessuna origine di pull esegue il polling o scarica un messaggio,</span><span class="sxs-lookup"><span data-stu-id="33f7c-138">Any pull sources do not poll or download a message.</span></span> <span data-ttu-id="33f7c-139">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="33f7c-139">For example:</span></span><br/>
  <span data-ttu-id="33f7c-140">Una pipeline effettua il pull dei messaggi da un'origine FTP esterna.</span><span class="sxs-lookup"><span data-stu-id="33f7c-140">A pipeline pulls messages from an external FTP source.</span></span> <span data-ttu-id="33f7c-141">L'istanza del ruolo che effettua il pull entra in stato limitato.</span><span class="sxs-lookup"><span data-stu-id="33f7c-141">The role instance doing the pull gets into a throttling state.</span></span> <span data-ttu-id="33f7c-142">In questa situazione, la pipeline interrompe il download di altri messaggi fino a quando l'istanza del ruolo non interrompe la limitazione.</span><span class="sxs-lookup"><span data-stu-id="33f7c-142">In this situation, the pipeline stops downloading additional messages until the role instance stops throttling.</span></span>
* <span data-ttu-id="33f7c-143">Al client viene inviata una risposta in modo che possa inviare di nuovo il messaggio.</span><span class="sxs-lookup"><span data-stu-id="33f7c-143">A response is sent to the client so the client can resubmit the message.</span></span>
* <span data-ttu-id="33f7c-144">È necessario attendere che la limitazione sia risolta.</span><span class="sxs-lookup"><span data-stu-id="33f7c-144">You must wait until the throttling is resolved.</span></span> <span data-ttu-id="33f7c-145">In particolare, occorre attendere che venga raggiunta la soglia inferiore.</span><span class="sxs-lookup"><span data-stu-id="33f7c-145">Specifically, you must wait until the low threshold is reached.</span></span>

## <a name="important-notes"></a><span data-ttu-id="33f7c-146">Note importanti</span><span class="sxs-lookup"><span data-stu-id="33f7c-146">Important notes</span></span>
* <span data-ttu-id="33f7c-147">Non è possibile disabilitare la limitazione.</span><span class="sxs-lookup"><span data-stu-id="33f7c-147">Throttling cannot be disabled.</span></span>
* <span data-ttu-id="33f7c-148">Non è possibile modificare le soglie di limitazione.</span><span class="sxs-lookup"><span data-stu-id="33f7c-148">Throttling thresholds cannot be modified.</span></span>
* <span data-ttu-id="33f7c-149">La limitazione viene implementata nell'intero sistema.</span><span class="sxs-lookup"><span data-stu-id="33f7c-149">Throttling is implemented system-wide.</span></span>
* <span data-ttu-id="33f7c-150">Anche il server di database SQL di Azure ha la funzionalità di limitazione incorporata.</span><span class="sxs-lookup"><span data-stu-id="33f7c-150">The Azure SQL Database Server also has built-in throttling.</span></span>

## <a name="additional-azure-biztalk-services-topics"></a><span data-ttu-id="33f7c-151">Argomenti aggiuntivi su Servizi BizTalk di Azure</span><span class="sxs-lookup"><span data-stu-id="33f7c-151">Additional Azure BizTalk Services topics</span></span>
* [<span data-ttu-id="33f7c-152">Installare Azure BizTalk Services SDK</span><span class="sxs-lookup"><span data-stu-id="33f7c-152">Installing the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [<span data-ttu-id="33f7c-153">Servizi BizTalk: Esercitazioni ed esempi</span><span class="sxs-lookup"><span data-stu-id="33f7c-153">Tutorials: Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [<span data-ttu-id="33f7c-154">Come iniziare a usare l'SDK di Servizi BizTalk di Azure</span><span class="sxs-lookup"><span data-stu-id="33f7c-154">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="33f7c-155">Servizi BizTalk di Azure</span><span class="sxs-lookup"><span data-stu-id="33f7c-155">Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a><span data-ttu-id="33f7c-156">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="33f7c-156">See Also</span></span>
* [<span data-ttu-id="33f7c-157">Servizi BizTalk: Grafico edizioni Developer, Basic, Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="33f7c-157">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [<span data-ttu-id="33f7c-158">Servizi BizTalk: effettuare il provisioning di un servizio BizTalk mediante il portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="33f7c-158">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [<span data-ttu-id="33f7c-159">Servizi BizTalk: Tabella degli stati del servizio</span><span class="sxs-lookup"><span data-stu-id="33f7c-159">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [<span data-ttu-id="33f7c-160">Servizi BizTalk: Schede Dashboard, Monitoraggio, Scalabilità</span><span class="sxs-lookup"><span data-stu-id="33f7c-160">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [<span data-ttu-id="33f7c-161">Servizi BizTalk: backup e ripristino</span><span class="sxs-lookup"><span data-stu-id="33f7c-161">BizTalk Services: Backup and Restore</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [<span data-ttu-id="33f7c-162">Servizi BizTalk: nome e chiave dell'autorità emittente</span><span class="sxs-lookup"><span data-stu-id="33f7c-162">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)<br/>

