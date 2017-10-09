---
title: aaaLearn sulla limitazione delle richieste nei servizi BizTalk | Documenti Microsoft
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
ms.openlocfilehash: 46c8806c3a1f4eeb793f721f849771e0ec155197
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-throttling"></a><span data-ttu-id="0dbe1-105">Servizi BizTalk: limitazione</span><span class="sxs-lookup"><span data-stu-id="0dbe1-105">BizTalk Services: Throttling</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="0dbe1-106">Servizi BizTalk di Azure implementa una limitazione del servizio in base alle due condizioni: numero di hello e utilizzo della memoria di elaborazione di messaggi simultanei.</span><span class="sxs-lookup"><span data-stu-id="0dbe1-106">Azure BizTalk Services implements service throttling based on two conditions: memory usage and hello number of simultaneous messages processing.</span></span> <span data-ttu-id="0dbe1-107">In questo argomento vengono elencate le soglie di limitazione hello e viene descritto il comportamento di Runtime hello quando si verifica una condizione di limitazione.</span><span class="sxs-lookup"><span data-stu-id="0dbe1-107">This topic lists hello throttling thresholds and describes hello Runtime behavior when a throttling condition occurs.</span></span>

## <a name="throttling-thresholds"></a><span data-ttu-id="0dbe1-108">Soglie di limitazione</span><span class="sxs-lookup"><span data-stu-id="0dbe1-108">Throttling Thresholds</span></span>
<span data-ttu-id="0dbe1-109">Nella seguente sono elencati nella tabella Hello hello origine limitazione delle richieste e le soglie:</span><span class="sxs-lookup"><span data-stu-id="0dbe1-109">hello following table lists hello throttling source and thresholds:</span></span>

|  | <span data-ttu-id="0dbe1-110">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0dbe1-110">Description</span></span> | <span data-ttu-id="0dbe1-111">Soglia inferiore</span><span class="sxs-lookup"><span data-stu-id="0dbe1-111">Low Threshold</span></span> | <span data-ttu-id="0dbe1-112">Soglia superiore</span><span class="sxs-lookup"><span data-stu-id="0dbe1-112">High Threshold</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0dbe1-113">Memoria</span><span class="sxs-lookup"><span data-stu-id="0dbe1-113">Memory</span></span> |<span data-ttu-id="0dbe1-114">Percentuale di memoria totale del sistema disponibile/byte file di paging.</span><span class="sxs-lookup"><span data-stu-id="0dbe1-114">% of total system memory available/PageFileBytes.</span></span> <p><p><span data-ttu-id="0dbe1-115">PageFileBytes disponibile totale è circa 2 volte hello RAM di sistema hello.</span><span class="sxs-lookup"><span data-stu-id="0dbe1-115">Total available PageFileBytes is approximately 2 times hello RAM of hello system.</span></span> |<span data-ttu-id="0dbe1-116">60%</span><span class="sxs-lookup"><span data-stu-id="0dbe1-116">60%</span></span> |<span data-ttu-id="0dbe1-117">70%</span><span class="sxs-lookup"><span data-stu-id="0dbe1-117">70%</span></span> |
| <span data-ttu-id="0dbe1-118">Elaborazione di messaggi</span><span class="sxs-lookup"><span data-stu-id="0dbe1-118">Message Processing</span></span> |<span data-ttu-id="0dbe1-119">Numero di messaggi elaborati simultaneamente</span><span class="sxs-lookup"><span data-stu-id="0dbe1-119">Number of messages processing simultaneously</span></span> |<span data-ttu-id="0dbe1-120">40 * numero di memorie centrali</span><span class="sxs-lookup"><span data-stu-id="0dbe1-120">40 * number of cores</span></span> |<span data-ttu-id="0dbe1-121">100 * numero di memorie centrali</span><span class="sxs-lookup"><span data-stu-id="0dbe1-121">100 * number of cores</span></span> |

<span data-ttu-id="0dbe1-122">Quando viene raggiunta una soglia elevata, i servizi BizTalk di Azure avvia toothrottle.</span><span class="sxs-lookup"><span data-stu-id="0dbe1-122">When a high threshold is reached, Azure BizTalk Services starts toothrottle.</span></span> <span data-ttu-id="0dbe1-123">Interrompe la limitazione delle richieste quando viene raggiunta la soglia inferiore hello.</span><span class="sxs-lookup"><span data-stu-id="0dbe1-123">Throttling stops when hello low threshold is reached.</span></span> <span data-ttu-id="0dbe1-124">Se ad esempio il servizio utilizza il 65% della memoria di sistema,</span><span class="sxs-lookup"><span data-stu-id="0dbe1-124">For example, your service is using 65% system memory.</span></span> <span data-ttu-id="0dbe1-125">In questo caso, il servizio di hello non rallenta.</span><span class="sxs-lookup"><span data-stu-id="0dbe1-125">In this situation, hello service does not throttle.</span></span> <span data-ttu-id="0dbe1-126">Se invece il servizio inizia a utilizzare il 70% della memoria di sistema,</span><span class="sxs-lookup"><span data-stu-id="0dbe1-126">Your service starts using 70% system memory.</span></span> <span data-ttu-id="0dbe1-127">In questo caso, il servizio di hello limita e continua toothrottle fino a quando il servizio di hello utilizza memoria di sistema di 60% (soglia inferiore).</span><span class="sxs-lookup"><span data-stu-id="0dbe1-127">In this situation, hello service throttles and continues toothrottle until hello service uses 60% (low threshold) system memory.</span></span>

<span data-ttu-id="0dbe1-128">Servizi BizTalk di Azure tiene traccia hello la limitazione delle richieste di stato (stato normale e lo stato di limitato) e la limitazione della durata hello.</span><span class="sxs-lookup"><span data-stu-id="0dbe1-128">Azure BizTalk Services tracks hello throttling status (normal state vs. throttled state) and hello throttling duration.</span></span>

## <a name="runtime-behavior"></a><span data-ttu-id="0dbe1-129">Comportamento in fase di esecuzione</span><span class="sxs-lookup"><span data-stu-id="0dbe1-129">Runtime Behavior</span></span>
<span data-ttu-id="0dbe1-130">Quando i servizi BizTalk di Azure passa allo stato di limitazione delle richieste, si verifica hello segue:</span><span class="sxs-lookup"><span data-stu-id="0dbe1-130">When Azure BizTalk Services enters a throttling state, hello following occurs:</span></span>

* <span data-ttu-id="0dbe1-131">La limitazione viene applicata a ogni istanza del ruolo,</span><span class="sxs-lookup"><span data-stu-id="0dbe1-131">Throttling is per role instance.</span></span> <span data-ttu-id="0dbe1-132">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="0dbe1-132">For example:</span></span><br/>
  <span data-ttu-id="0dbe1-133">IstanzaRuoloA è limitata.</span><span class="sxs-lookup"><span data-stu-id="0dbe1-133">RoleInstanceA is throttling.</span></span> <span data-ttu-id="0dbe1-134">IstanzaRuoloB non è limitata.</span><span class="sxs-lookup"><span data-stu-id="0dbe1-134">RoleInstanceB is not throttling.</span></span> <span data-ttu-id="0dbe1-135">In questa situazione, i messaggi in IstanzaRuoloB vengono elaborati come previsto.</span><span class="sxs-lookup"><span data-stu-id="0dbe1-135">In this situation, messages in RoleInstanceB are processed as expected.</span></span> <span data-ttu-id="0dbe1-136">I messaggi di RoleInstanceA vengono ignorati e non riuscire con hello errore seguente:</span><span class="sxs-lookup"><span data-stu-id="0dbe1-136">Messages in RoleInstanceA are discarded and fail with hello following error:</span></span><br/><br/><span data-ttu-id="0dbe1-137">
  **Il server è occupato. Riprovare più tardi.**</span><span class="sxs-lookup"><span data-stu-id="0dbe1-137">
**Server is busy. Please try again.**</span></span><br/><br/>
* <span data-ttu-id="0dbe1-138">Nessuna origine di pull esegue il polling o scarica un messaggio,</span><span class="sxs-lookup"><span data-stu-id="0dbe1-138">Any pull sources do not poll or download a message.</span></span> <span data-ttu-id="0dbe1-139">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="0dbe1-139">For example:</span></span><br/>
  <span data-ttu-id="0dbe1-140">Una pipeline effettua il pull dei messaggi da un'origine FTP esterna.</span><span class="sxs-lookup"><span data-stu-id="0dbe1-140">A pipeline pulls messages from an external FTP source.</span></span> <span data-ttu-id="0dbe1-141">istanza del ruolo Hello esegue il pull di hello ottiene in uno stato di limitazione delle richieste.</span><span class="sxs-lookup"><span data-stu-id="0dbe1-141">hello role instance doing hello pull gets into a throttling state.</span></span> <span data-ttu-id="0dbe1-142">In questo caso, la pipeline hello arresta download altri messaggi fino a quando l'istanza del ruolo hello arresta la limitazione delle richieste.</span><span class="sxs-lookup"><span data-stu-id="0dbe1-142">In this situation, hello pipeline stops downloading additional messages until hello role instance stops throttling.</span></span>
* <span data-ttu-id="0dbe1-143">Una risposta viene inviata toohello client in modo da client hello è possibile inviare di nuovo il messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="0dbe1-143">A response is sent toohello client so hello client can resubmit hello message.</span></span>
* <span data-ttu-id="0dbe1-144">È necessario attendere fino a quando la limitazione delle richieste di hello viene risolto.</span><span class="sxs-lookup"><span data-stu-id="0dbe1-144">You must wait until hello throttling is resolved.</span></span> <span data-ttu-id="0dbe1-145">In particolare, è necessario attendere fino a quando non viene raggiunta la soglia inferiore hello.</span><span class="sxs-lookup"><span data-stu-id="0dbe1-145">Specifically, you must wait until hello low threshold is reached.</span></span>

## <a name="important-notes"></a><span data-ttu-id="0dbe1-146">Note importanti</span><span class="sxs-lookup"><span data-stu-id="0dbe1-146">Important notes</span></span>
* <span data-ttu-id="0dbe1-147">Non è possibile disabilitare la limitazione.</span><span class="sxs-lookup"><span data-stu-id="0dbe1-147">Throttling cannot be disabled.</span></span>
* <span data-ttu-id="0dbe1-148">Non è possibile modificare le soglie di limitazione.</span><span class="sxs-lookup"><span data-stu-id="0dbe1-148">Throttling thresholds cannot be modified.</span></span>
* <span data-ttu-id="0dbe1-149">La limitazione viene implementata nell'intero sistema.</span><span class="sxs-lookup"><span data-stu-id="0dbe1-149">Throttling is implemented system-wide.</span></span>
* <span data-ttu-id="0dbe1-150">Hello Server di Database SQL di Azure dispone anche di limitazione incorporato.</span><span class="sxs-lookup"><span data-stu-id="0dbe1-150">hello Azure SQL Database Server also has built-in throttling.</span></span>

## <a name="additional-azure-biztalk-services-topics"></a><span data-ttu-id="0dbe1-151">Argomenti aggiuntivi su Servizi BizTalk di Azure</span><span class="sxs-lookup"><span data-stu-id="0dbe1-151">Additional Azure BizTalk Services topics</span></span>
* [<span data-ttu-id="0dbe1-152">L'installazione di hello Azure BizTalk Services SDK</span><span class="sxs-lookup"><span data-stu-id="0dbe1-152">Installing hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [<span data-ttu-id="0dbe1-153">Servizi BizTalk: Esercitazioni ed esempi</span><span class="sxs-lookup"><span data-stu-id="0dbe1-153">Tutorials: Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [<span data-ttu-id="0dbe1-154">Come è possibile utilizzare hello Azure BizTalk Services SDK</span><span class="sxs-lookup"><span data-stu-id="0dbe1-154">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="0dbe1-155">Servizi BizTalk di Azure</span><span class="sxs-lookup"><span data-stu-id="0dbe1-155">Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a><span data-ttu-id="0dbe1-156">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="0dbe1-156">See Also</span></span>
* [<span data-ttu-id="0dbe1-157">Servizi BizTalk: Grafico edizioni Developer, Basic, Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="0dbe1-157">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [<span data-ttu-id="0dbe1-158">Servizi BizTalk: effettuare il provisioning di un servizio BizTalk mediante il portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="0dbe1-158">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [<span data-ttu-id="0dbe1-159">Servizi BizTalk: Tabella degli stati del servizio</span><span class="sxs-lookup"><span data-stu-id="0dbe1-159">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [<span data-ttu-id="0dbe1-160">Servizi BizTalk: Schede Dashboard, Monitoraggio, Scalabilità</span><span class="sxs-lookup"><span data-stu-id="0dbe1-160">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [<span data-ttu-id="0dbe1-161">Servizi BizTalk: backup e ripristino</span><span class="sxs-lookup"><span data-stu-id="0dbe1-161">BizTalk Services: Backup and Restore</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [<span data-ttu-id="0dbe1-162">Servizi BizTalk: nome e chiave dell'autorità emittente</span><span class="sxs-lookup"><span data-stu-id="0dbe1-162">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)<br/>

