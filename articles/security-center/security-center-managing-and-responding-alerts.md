---
title: avvisi di sicurezza aaaManage nel Centro protezione di Azure | Documenti Microsoft
description: "Questo documento consente si toouse Centro sicurezza di Azure funzionalità toomanage e risposta toosecurity avvisi."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: b88a8df7-6979-479b-8039-04da1b8737a7
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: yurid
ms.openlocfilehash: f1cb7e4770776827b75ed15893914678c1f44216
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-and-responding-toosecurity-alerts-in-azure-security-center"></a><span data-ttu-id="64db7-103">La gestione e risponde avvisi toosecurity nel Centro protezione di Azure</span><span class="sxs-lookup"><span data-stu-id="64db7-103">Managing and responding toosecurity alerts in Azure Security Center</span></span>
<span data-ttu-id="64db7-104">Questo documento consente di utilizzare toomanage Centro sicurezza di Azure e rispondere toosecurity avvisi.</span><span class="sxs-lookup"><span data-stu-id="64db7-104">This document helps you use Azure Security Center toomanage and respond toosecurity alerts.</span></span>

> [!NOTE]
> <span data-ttu-id="64db7-105">rilevamenti tooenable avanzate, aggiornamento tooAzure Security Center Standard.</span><span class="sxs-lookup"><span data-stu-id="64db7-105">tooenable advanced detections, upgrade tooAzure Security Center Standard.</span></span> <span data-ttu-id="64db7-106">È disponibile una versione di valutazione gratuita di 60 giorni.</span><span class="sxs-lookup"><span data-stu-id="64db7-106">A free 60-day trial is available.</span></span> <span data-ttu-id="64db7-107">tooupgrade, tariffario selezionare in hello [criteri di sicurezza](security-center-policies.md).</span><span class="sxs-lookup"><span data-stu-id="64db7-107">tooupgrade, select Pricing Tier in hello [Security Policy](security-center-policies.md).</span></span> <span data-ttu-id="64db7-108">Vedere [Centro sicurezza di Azure prezzi](security-center-pricing.md) toolearn altre.</span><span class="sxs-lookup"><span data-stu-id="64db7-108">See [Azure Security Center pricing](security-center-pricing.md) toolearn more.</span></span>
>
>

## <a name="what-are-security-alerts"></a><span data-ttu-id="64db7-109">Informazioni sugli avvisi di sicurezza</span><span class="sxs-lookup"><span data-stu-id="64db7-109">What are security alerts?</span></span>
<span data-ttu-id="64db7-110">Centro sicurezza PC automaticamente raccoglie, analizza, integra i dati del log dalle risorse di Azure, rete hello e soluzioni partner, ad esempio soluzioni di protezione firewall ed endpoint, minacce reali toodetect connesse e ridurre i falsi positivi.</span><span class="sxs-lookup"><span data-stu-id="64db7-110">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, hello network, and connected partner solutions, like firewall and endpoint protection solutions, toodetect real threats and reduce false positives.</span></span> <span data-ttu-id="64db7-111">Viene visualizzato un elenco di avvisi di sicurezza in ordine di priorità del Centro sicurezza PC insieme hello informazioni necessarie tooquickly analizzare problema hello e indicazioni sul tooremediate un attacco.</span><span class="sxs-lookup"><span data-stu-id="64db7-111">A list of prioritized security alerts is shown in Security Center along with hello information you need tooquickly investigate hello problem and recommendations for how tooremediate an attack.</span></span>


> [!NOTE]
> <span data-ttu-id="64db7-112">Per altre informazioni sulle funzionalità di rilevamento del Centro sicurezza, vedere [Funzionalità di rilevamento del Centro sicurezza di Azure](security-center-detection-capabilities.md).</span><span class="sxs-lookup"><span data-stu-id="64db7-112">For more information about how Security Center detection capabilities work, read [Azure Security Center Detection Capabilities](security-center-detection-capabilities.md).</span></span>
>
>

## <a name="managing-security-alerts"></a><span data-ttu-id="64db7-113">Gestire gli avvisi di sicurezza</span><span class="sxs-lookup"><span data-stu-id="64db7-113">Managing security alerts</span></span>
<span data-ttu-id="64db7-114">È possibile esaminare gli avvisi correnti esaminando hello **degli avvisi di sicurezza** riquadro.</span><span class="sxs-lookup"><span data-stu-id="64db7-114">You can review your current alerts by looking at hello **Security alerts** tile.</span></span> <span data-ttu-id="64db7-115">Aprire il portale di Azure e seguire i passaggi di hello sotto toosee ulteriori dettagli su ogni avviso:</span><span class="sxs-lookup"><span data-stu-id="64db7-115">Open Azure Portal and follow hello steps below toosee more details about each alert:</span></span>

1. <span data-ttu-id="64db7-116">Nel dashboard del Centro sicurezza PC hello, verrà visualizzato hello **degli avvisi di sicurezza** riquadro.</span><span class="sxs-lookup"><span data-stu-id="64db7-116">On hello Security Center dashboard, you will see hello **Security alerts** tile.</span></span>

    ![Riquadro Avvisi di sicurezza nel Centro sicurezza di Azure](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig1-ga.png)

2. <span data-ttu-id="64db7-118">Fare clic su hello di hello riquadro tooopen **degli avvisi di sicurezza** pannello che contiene ulteriori dettagli sulle hello gli avvisi come mostrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="64db7-118">Click hello tile tooopen hello **Security alerts** blade that contains more details about hello alerts as shown below.</span></span>

   ![Pannello di avvisi di sicurezza Hello in Centro sicurezza PC](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig2-ga.png)

<span data-ttu-id="64db7-120">Nella parte inferiore di hello di questo pannello sono dettagli hello per ogni avviso.</span><span class="sxs-lookup"><span data-stu-id="64db7-120">In hello bottom part of this blade are hello details for each alert.</span></span> <span data-ttu-id="64db7-121">toosort, fare clic sulla colonna hello che si desidera toosort da.</span><span class="sxs-lookup"><span data-stu-id="64db7-121">toosort, click hello column that you want toosort by.</span></span> <span data-ttu-id="64db7-122">definizione di Hello per ogni colonna è indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="64db7-122">hello definition for each column is given below:</span></span>

* <span data-ttu-id="64db7-123">**Descrizione**: una breve descrizione dell'avviso hello.</span><span class="sxs-lookup"><span data-stu-id="64db7-123">**Description**: A brief explanation of hello alert.</span></span>
* <span data-ttu-id="64db7-124">**Conteggio**: elenco di tutti gli avvisi di questo tipo rilevati in un giorno specifico.</span><span class="sxs-lookup"><span data-stu-id="64db7-124">**Count**: A list of all alerts of this specific type that were detected on a specific day.</span></span>
* <span data-ttu-id="64db7-125">**Viene rilevata da**: hello servizio che è responsabile per l'attivazione dell'avviso hello.</span><span class="sxs-lookup"><span data-stu-id="64db7-125">**Detected by**: hello service that was responsible for triggering hello alert.</span></span>
* <span data-ttu-id="64db7-126">**Data**: hello data che l'evento hello si è verificato.</span><span class="sxs-lookup"><span data-stu-id="64db7-126">**Date**: hello date that hello event occurred.</span></span>
* <span data-ttu-id="64db7-127">**Stato**: hello stato corrente per tale avviso.</span><span class="sxs-lookup"><span data-stu-id="64db7-127">**State**: hello current state for that alert.</span></span> <span data-ttu-id="64db7-128">Esistono due tipi di stato:</span><span class="sxs-lookup"><span data-stu-id="64db7-128">There are two types of states:</span></span>
  * <span data-ttu-id="64db7-129">**Attiva**: avviso di sicurezza hello è stata rilevata.</span><span class="sxs-lookup"><span data-stu-id="64db7-129">**Active**: hello security alert has been detected.</span></span>
* <span data-ttu-id="64db7-130">**Gravità**: livello di gravità hello, che può essere alta, Media o bassa.</span><span class="sxs-lookup"><span data-stu-id="64db7-130">**Severity**: hello severity level, which can be high, medium or low.</span></span>

### <a name="filtering-alerts"></a><span data-ttu-id="64db7-131">Filtro degli avvisi</span><span class="sxs-lookup"><span data-stu-id="64db7-131">Filtering alerts</span></span>
<span data-ttu-id="64db7-132">È possibile filtrare gli avvisi in base a data, stato e gravità.</span><span class="sxs-lookup"><span data-stu-id="64db7-132">You can filter alerts based on date, state, and severity.</span></span> <span data-ttu-id="64db7-133">Filtraggio degli avvisi può essere utile per scenari in cui è necessario ambito hello toonarrow di visualizzare gli avvisi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="64db7-133">Filtering alerts can be useful for scenarios where you need toonarrow hello scope of security alerts show.</span></span> <span data-ttu-id="64db7-134">Ad esempio, si potrebbe si desidera che gli avvisi di sicurezza tooaddress che si è verificato in hello ultime 24 ore perché si sta analizzando una potenziale violazione nel sistema hello.</span><span class="sxs-lookup"><span data-stu-id="64db7-134">For example, you might you want tooaddress security alerts that occurred in hello last 24 hours because you are investigating a potential breach in hello system.</span></span>

1. <span data-ttu-id="64db7-135">Fare clic su **filtro** su hello **degli avvisi di sicurezza** blade.</span><span class="sxs-lookup"><span data-stu-id="64db7-135">Click **Filter** on hello **Security Alerts** blade.</span></span> <span data-ttu-id="64db7-136">Hello **filtro** pannello apre e si selezionano i valori di data, stato e gravità hello desiderato toosee.</span><span class="sxs-lookup"><span data-stu-id="64db7-136">hello **Filter** blade opens and you select hello date, state, and severity values you wish toosee.</span></span>

    ![Filtro degli avvisi nel Centro sicurezza](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig3-2017.png)

### <a name="respond-toosecurity-alerts"></a><span data-ttu-id="64db7-138">Rispondere toosecurity avvisi</span><span class="sxs-lookup"><span data-stu-id="64db7-138">Respond toosecurity alerts</span></span>
<span data-ttu-id="64db7-139">Selezionare un toolearn avviso di sicurezza ulteriori informazioni su eventi hello che ha attivato avviso hello e cosa, se presente, i passaggi necessari per necessario tootake tooremediate un attacco.</span><span class="sxs-lookup"><span data-stu-id="64db7-139">Select a security alert toolearn more about hello event(s) that triggered hello alert and what, if any, steps you need tootake tooremediate an attack.</span></span> <span data-ttu-id="64db7-140">Gli avvisi di sicurezza sono raggruppati per tipo e data.</span><span class="sxs-lookup"><span data-stu-id="64db7-140">Security alerts are grouped by type and date.</span></span> <span data-ttu-id="64db7-141">Fare clic su un avviso di sicurezza verrà aperto un pannello contenente un elenco di avvisi hello raggruppato.</span><span class="sxs-lookup"><span data-stu-id="64db7-141">Clicking a security alert will open a blade containing a list of hello grouped alerts.</span></span>

![Rispondere avvisi toosecurity nel Centro protezione di Azure](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig5-ga.png)

<span data-ttu-id="64db7-143">In questo caso, sono stati generati gli avvisi hello consultare toosuspicious attività Remote Desktop Protocol (RDP).</span><span class="sxs-lookup"><span data-stu-id="64db7-143">In this case, hello alerts that were triggered refer toosuspicious Remote Desktop Protocol (RDP) activity.</span></span> <span data-ttu-id="64db7-144">Hello prima colonna indica quali risorse sono state attaccate; in secondo luogo, Hello Mostra quante volte è stata attaccata risorse hello; Hello terzo Mostra ora hello dell'attacco hello. Hello quarto Mostra lo stato di avviso hello. e hello Mostra quinto gravità hello di attacco hello.</span><span class="sxs-lookup"><span data-stu-id="64db7-144">hello first column shows which resources were attacked; hello second shows how many times hello resource was attacked; hello third shows hello time of hello attack; hello fourth shows state of hello alert; and hello fifth shows hello severity of hello attack.</span></span> <span data-ttu-id="64db7-145">Dopo aver esaminato queste informazioni, fare clic sulla risorsa hello che è stato attaccato e verrà aperto un nuovo pannello.</span><span class="sxs-lookup"><span data-stu-id="64db7-145">After reviewing this information, click hello resource that was attacked and a new blade will open.</span></span>

![Suggerimenti per la quale toodo sulla sicurezza gli avvisi in Centro sicurezza di Azure](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig6-ga.png)

<span data-ttu-id="64db7-147">In hello **descrizione** campo di questo pannello sono disponibili ulteriori dettagli sull'evento.</span><span class="sxs-lookup"><span data-stu-id="64db7-147">In hello **Description** field of this blade you will find more details about this event.</span></span> <span data-ttu-id="64db7-148">Tali dettagli supplementari offrono approfondite quali hello attivata sicurezza avviso, hello risorsa di destinazione, quando applicabile hello origine indirizzo IP e indicazioni su come tooremediate.</span><span class="sxs-lookup"><span data-stu-id="64db7-148">These additional details offer insight into what triggered hello security alert, hello target resource, when applicable hello source IP address, and recommendations about how tooremediate.</span></span>  <span data-ttu-id="64db7-149">In alcuni casi, indirizzo IP di origine hello verrà essere svuotata (non disponibile) perché non tutti i registri di eventi di sicurezza di Windows includono l'indirizzo IP hello.</span><span class="sxs-lookup"><span data-stu-id="64db7-149">In some instances, hello source IP address will be empty (not available) because not all Windows security events logs include hello IP address.</span></span>

<span data-ttu-id="64db7-150">monitoraggio e aggiornamento Hello suggerita dal centro di sicurezza variano secondo avviso di sicurezza toohello.</span><span class="sxs-lookup"><span data-stu-id="64db7-150">hello remediation suggested by Security Center will vary according toohello security alert.</span></span> <span data-ttu-id="64db7-151">In alcuni casi, potrebbe essere toouse tooimplement altre funzionalità di Azure hello consigliato di monitoraggio e aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="64db7-151">In some cases, you may have toouse other Azure capabilities tooimplement hello recommended remediation.</span></span> <span data-ttu-id="64db7-152">Ad esempio, hello correzione per questo tipo di attacco è l'indirizzo IP di hello tooblacklist che genera questo attacco tramite un [ACL di rete](../virtual-network/virtual-networks-acl.md) o [il gruppo di sicurezza di rete](../virtual-network/virtual-networks-nsg.md) regola.</span><span class="sxs-lookup"><span data-stu-id="64db7-152">For example, hello remediation for this attack is tooblacklist hello IP address that is generating this attack by using a [network ACL](../virtual-network/virtual-networks-acl.md) or a [network security group](../virtual-network/virtual-networks-nsg.md) rule.</span></span>

> [!NOTE]
> <span data-ttu-id="64db7-153">Per altre informazioni sui diversi tipi di hello degli avvisi, vedere [degli avvisi di sicurezza dal tipo nel Centro protezione Azure](security-center-alerts-type.md).</span><span class="sxs-lookup"><span data-stu-id="64db7-153">For more information on hello different types of alerts, read [Security Alerts by Type in Azure Security Center](security-center-alerts-type.md).</span></span>
>
>

## <a name="see-also"></a><span data-ttu-id="64db7-154">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="64db7-154">See also</span></span>
<span data-ttu-id="64db7-155">In questo documento, si è appreso come criteri di sicurezza tooconfigure in Centro sicurezza PC.</span><span class="sxs-lookup"><span data-stu-id="64db7-155">In this document, you learned how tooconfigure security policies in Security Center.</span></span> <span data-ttu-id="64db7-156">toolearn ulteriori informazioni su Centro di sicurezza, vedere l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="64db7-156">toolearn more about Security Center, see hello following:</span></span>

* [<span data-ttu-id="64db7-157">Gestione degli eventi imprevisti della sicurezza nel Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="64db7-157">Handling Security Incident in Azure Security Center</span></span>](security-center-incident.md)
* [<span data-ttu-id="64db7-158">Funzionalità di rilevamento del Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="64db7-158">Azure Security Center Detection Capabilities</span></span>](security-center-detection-capabilities.md)
* [<span data-ttu-id="64db7-159">Guida alla pianificazione e alla gestione del Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="64db7-159">Azure Security Center Planning and Operations Guide</span></span>](security-center-planning-and-operations-guide.md)
* <span data-ttu-id="64db7-160">[Domande frequenti su Centro sicurezza di Azure](security-center-faq.md) : domande frequenti sull'utilizzo di hello servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="64db7-160">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="64db7-161">[Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/) : post di blog sulla sicurezza e sulla conformità di Azure.</span><span class="sxs-lookup"><span data-stu-id="64db7-161">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Find blog posts about Azure security and compliance.</span></span>
