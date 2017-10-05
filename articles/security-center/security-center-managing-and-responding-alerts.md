---
title: Gestire gli avvisi di sicurezza nel Centro sicurezza di Azure | Documentazione Microsoft
description: "Questo documento illustra come usare le funzionalità del Centro sicurezza di Azure per gestire e rispondere agli avvisi di sicurezza."
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
ms.openlocfilehash: 56fcfbfdbe15749132ba6a27861142fd564063c3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="managing-and-responding-to-security-alerts-in-azure-security-center"></a><span data-ttu-id="33eab-103">Gestione e risposta agli avvisi di sicurezza nel Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="33eab-103">Managing and responding to security alerts in Azure Security Center</span></span>
<span data-ttu-id="33eab-104">Questo documento illustra come usare il Centro sicurezza di Azure per gestire e rispondere agli avvisi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="33eab-104">This document helps you use Azure Security Center to manage and respond to security alerts.</span></span>

> [!NOTE]
> <span data-ttu-id="33eab-105">Per abilitare le funzionalità di rilevamento avanzato, eseguire l'aggiornamento al livello Standard del Centro sicurezza di Azure.</span><span class="sxs-lookup"><span data-stu-id="33eab-105">To enable advanced detections, upgrade to Azure Security Center Standard.</span></span> <span data-ttu-id="33eab-106">È disponibile una versione di valutazione gratuita di 60 giorni.</span><span class="sxs-lookup"><span data-stu-id="33eab-106">A free 60-day trial is available.</span></span> <span data-ttu-id="33eab-107">Per eseguire l'aggiornamento, selezionare il piano tariffario nei [criteri di sicurezza](security-center-policies.md).</span><span class="sxs-lookup"><span data-stu-id="33eab-107">To upgrade, select Pricing Tier in the [Security Policy](security-center-policies.md).</span></span> <span data-ttu-id="33eab-108">Per altre informazioni, vedere [Prezzi del Centro sicurezza di Azure](security-center-pricing.md).</span><span class="sxs-lookup"><span data-stu-id="33eab-108">See [Azure Security Center pricing](security-center-pricing.md) to learn more.</span></span>
>
>

## <a name="what-are-security-alerts"></a><span data-ttu-id="33eab-109">Informazioni sugli avvisi di sicurezza</span><span class="sxs-lookup"><span data-stu-id="33eab-109">What are security alerts?</span></span>
<span data-ttu-id="33eab-110">Il Centro sicurezza raccoglie, analizza e integra automaticamente i dati di log delle risorse di Azure, della rete e delle soluzioni dei partner connesse, come soluzioni di protezione endpoint e firewall, per rilevare le minacce reali e ridurre i falsi positivi.</span><span class="sxs-lookup"><span data-stu-id="33eab-110">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, the network, and connected partner solutions, like firewall and endpoint protection solutions, to detect real threats and reduce false positives.</span></span> <span data-ttu-id="33eab-111">Il Centro sicurezza visualizza un elenco degli avvisi di sicurezza in ordine di priorità, nonché le informazioni necessarie per analizzare rapidamente il problema e indicazioni per risolvere un attacco.</span><span class="sxs-lookup"><span data-stu-id="33eab-111">A list of prioritized security alerts is shown in Security Center along with the information you need to quickly investigate the problem and recommendations for how to remediate an attack.</span></span>


> [!NOTE]
> <span data-ttu-id="33eab-112">Per altre informazioni sulle funzionalità di rilevamento del Centro sicurezza, vedere [Funzionalità di rilevamento del Centro sicurezza di Azure](security-center-detection-capabilities.md).</span><span class="sxs-lookup"><span data-stu-id="33eab-112">For more information about how Security Center detection capabilities work, read [Azure Security Center Detection Capabilities](security-center-detection-capabilities.md).</span></span>
>
>

## <a name="managing-security-alerts"></a><span data-ttu-id="33eab-113">Gestire gli avvisi di sicurezza</span><span class="sxs-lookup"><span data-stu-id="33eab-113">Managing security alerts</span></span>
<span data-ttu-id="33eab-114">È possibile esaminare gli avvisi correnti visualizzando il riquadro **Avvisi di sicurezza** .</span><span class="sxs-lookup"><span data-stu-id="33eab-114">You can review your current alerts by looking at the **Security alerts** tile.</span></span> <span data-ttu-id="33eab-115">Aprire il portale di Azure e seguire questa procedura per visualizzare altri dettagli su ogni avviso:</span><span class="sxs-lookup"><span data-stu-id="33eab-115">Open Azure Portal and follow the steps below to see more details about each alert:</span></span>

1. <span data-ttu-id="33eab-116">Nel dashboard del Centro sicurezza è disponibile il riquadro **Avvisi di sicurezza** .</span><span class="sxs-lookup"><span data-stu-id="33eab-116">On the Security Center dashboard, you will see the **Security alerts** tile.</span></span>

    ![Riquadro Avvisi di sicurezza nel Centro sicurezza di Azure](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig1-ga.png)

2. <span data-ttu-id="33eab-118">Fare clic sul riquadro per aprire il pannello **Avvisi di sicurezza** contenente altri dettagli sugli avvisi, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="33eab-118">Click the tile to open the **Security alerts** blade that contains more details about the alerts as shown below.</span></span>

   ![Pannello Avvisi di sicurezza nel Centro sicurezza](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig2-ga.png)

<span data-ttu-id="33eab-120">Nella parte inferiore del pannello sono riportati i dettagli relativi ad ogni avviso.</span><span class="sxs-lookup"><span data-stu-id="33eab-120">In the bottom part of this blade are the details for each alert.</span></span> <span data-ttu-id="33eab-121">Per ordinarli, fare clic sulla colonna in base alle quale si vuole ordinare.</span><span class="sxs-lookup"><span data-stu-id="33eab-121">To sort, click the column that you want to sort by.</span></span> <span data-ttu-id="33eab-122">Di seguito è riportata una definizione per ogni colonna:</span><span class="sxs-lookup"><span data-stu-id="33eab-122">The definition for each column is given below:</span></span>

* <span data-ttu-id="33eab-123">**Descrizione**: breve spiegazione dell'avviso.</span><span class="sxs-lookup"><span data-stu-id="33eab-123">**Description**: A brief explanation of the alert.</span></span>
* <span data-ttu-id="33eab-124">**Conteggio**: elenco di tutti gli avvisi di questo tipo rilevati in un giorno specifico.</span><span class="sxs-lookup"><span data-stu-id="33eab-124">**Count**: A list of all alerts of this specific type that were detected on a specific day.</span></span>
* <span data-ttu-id="33eab-125">**Rilevato da**: servizio responsabile dell'attivazione dell'avviso.</span><span class="sxs-lookup"><span data-stu-id="33eab-125">**Detected by**: The service that was responsible for triggering the alert.</span></span>
* <span data-ttu-id="33eab-126">**Data**: data in cui si è verificato l'evento.</span><span class="sxs-lookup"><span data-stu-id="33eab-126">**Date**: The date that the event occurred.</span></span>
* <span data-ttu-id="33eab-127">**Stato**: stato corrente dell'avviso.</span><span class="sxs-lookup"><span data-stu-id="33eab-127">**State**: The current state for that alert.</span></span> <span data-ttu-id="33eab-128">Esistono due tipi di stato:</span><span class="sxs-lookup"><span data-stu-id="33eab-128">There are two types of states:</span></span>
  * <span data-ttu-id="33eab-129">**Attivo**: l'avviso di sicurezza è stato rilevato.</span><span class="sxs-lookup"><span data-stu-id="33eab-129">**Active**: The security alert has been detected.</span></span>
* <span data-ttu-id="33eab-130">**Gravità**: livello di gravità, che può essere alto, medio o basso.</span><span class="sxs-lookup"><span data-stu-id="33eab-130">**Severity**: The severity level, which can be high, medium or low.</span></span>

### <a name="filtering-alerts"></a><span data-ttu-id="33eab-131">Filtro degli avvisi</span><span class="sxs-lookup"><span data-stu-id="33eab-131">Filtering alerts</span></span>
<span data-ttu-id="33eab-132">È possibile filtrare gli avvisi in base a data, stato e gravità.</span><span class="sxs-lookup"><span data-stu-id="33eab-132">You can filter alerts based on date, state, and severity.</span></span> <span data-ttu-id="33eab-133">Il filtro degli avvisi può risultare utile per scenari in cui è necessario limitare l'ambito degli avvisi di sicurezza da visualizzare.</span><span class="sxs-lookup"><span data-stu-id="33eab-133">Filtering alerts can be useful for scenarios where you need to narrow the scope of security alerts show.</span></span> <span data-ttu-id="33eab-134">Ad esempio, potrebbe essere necessario gestire gli avvisi di sicurezza che si sono verificati nelle ultime 24 ore, perché si sta esaminando una potenziale violazione del sistema.</span><span class="sxs-lookup"><span data-stu-id="33eab-134">For example, you might you want to address security alerts that occurred in the last 24 hours because you are investigating a potential breach in the system.</span></span>

1. <span data-ttu-id="33eab-135">Fare clic su **Filtro** nel pannello **Avvisi di sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="33eab-135">Click **Filter** on the **Security Alerts** blade.</span></span> <span data-ttu-id="33eab-136">Verrà visualizzato il pannello **Filtro** in cui è possibile selezionare i valori di data, stato e gravità da visualizzare.</span><span class="sxs-lookup"><span data-stu-id="33eab-136">The **Filter** blade opens and you select the date, state, and severity values you wish to see.</span></span>

    ![Filtro degli avvisi nel Centro sicurezza](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig3-2017.png)

### <a name="respond-to-security-alerts"></a><span data-ttu-id="33eab-138">Rispondere agli avvisi di sicurezza</span><span class="sxs-lookup"><span data-stu-id="33eab-138">Respond to security alerts</span></span>
<span data-ttu-id="33eab-139">Selezionare un avviso di sicurezza per altre informazioni sugli eventi che hanno attivato l'avviso e, se presenti, i passaggi da eseguire per correggere un attacco.</span><span class="sxs-lookup"><span data-stu-id="33eab-139">Select a security alert to learn more about the event(s) that triggered the alert and what, if any, steps you need to take to remediate an attack.</span></span> <span data-ttu-id="33eab-140">Gli avvisi di sicurezza sono raggruppati per tipo e data.</span><span class="sxs-lookup"><span data-stu-id="33eab-140">Security alerts are grouped by type and date.</span></span> <span data-ttu-id="33eab-141">Se si fa clic su un avviso di sicurezza, viene aperto un pannello contenente un elenco degli avvisi raggruppati.</span><span class="sxs-lookup"><span data-stu-id="33eab-141">Clicking a security alert will open a blade containing a list of the grouped alerts.</span></span>

![Rispondere agli avvisi di sicurezza nel Centro sicurezza di Azure](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig5-ga.png)

<span data-ttu-id="33eab-143">In questo caso, gli avvisi attivati fanno riferimento a un'attività RDP (Remote Desktop Protocol) sospetta.</span><span class="sxs-lookup"><span data-stu-id="33eab-143">In this case, the alerts that were triggered refer to suspicious Remote Desktop Protocol (RDP) activity.</span></span> <span data-ttu-id="33eab-144">La prima colonna indica le risorse che sono state attaccate, la seconda quante volte la risorsa è stata attaccata, la terza l'ora dell'attacco, la quarta lo stato dell'avviso e la quinta il livello di gravità dell'attacco.</span><span class="sxs-lookup"><span data-stu-id="33eab-144">The first column shows which resources were attacked; the second shows how many times the resource was attacked; the third shows the time of the attack; the fourth shows state of the alert; and the fifth shows the severity of the attack.</span></span> <span data-ttu-id="33eab-145">Dopo aver esaminato queste informazioni, fare clic sulla risorsa che ha subito attacchi. Verrà visualizzato un nuovo pannello.</span><span class="sxs-lookup"><span data-stu-id="33eab-145">After reviewing this information, click the resource that was attacked and a new blade will open.</span></span>

![Suggerimenti sulle operazioni da eseguire in presenza di avvisi di sicurezza nel Centro sicurezza di Azure](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig6-ga.png)

<span data-ttu-id="33eab-147">Nel campo **Descrizione** di questo pannello sono disponibili altri dettagli sull'evento.</span><span class="sxs-lookup"><span data-stu-id="33eab-147">In the **Description** field of this blade you will find more details about this event.</span></span> <span data-ttu-id="33eab-148">Tali dettagli aggiuntivi forniscono informazioni sull'azione che ha attivato l'avviso di sicurezza, la risorsa di destinazione, l'indirizzo IP di origine quando applicabile e raccomandazioni su come risolvere.</span><span class="sxs-lookup"><span data-stu-id="33eab-148">These additional details offer insight into what triggered the security alert, the target resource, when applicable the source IP address, and recommendations about how to remediate.</span></span>  <span data-ttu-id="33eab-149">In alcuni casi, l'indirizzo IP di origine sarà vuoto (non disponibile), perché non tutti i registri eventi di sicurezza di Windows includono l'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="33eab-149">In some instances, the source IP address will be empty (not available) because not all Windows security events logs include the IP address.</span></span>

<span data-ttu-id="33eab-150">Le correzioni suggerite dal Centro sicurezza variano in base all'avviso di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="33eab-150">The remediation suggested by Security Center will vary according to the security alert.</span></span> <span data-ttu-id="33eab-151">In alcuni casi, può essere necessario usare altre funzionalità di Azure per implementare la correzione consigliata.</span><span class="sxs-lookup"><span data-stu-id="33eab-151">In some cases, you may have to use other Azure capabilities to implement the recommended remediation.</span></span> <span data-ttu-id="33eab-152">La correzione consigliata per questo tipo di attacco, ad esempio, consiste nell'aggiungere alla blacklist l'indirizzo IP che genera l'attacco usando un [ACL di rete](../virtual-network/virtual-networks-acl.md) o una regola del [gruppo di sicurezza di rete](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="33eab-152">For example, the remediation for this attack is to blacklist the IP address that is generating this attack by using a [network ACL](../virtual-network/virtual-networks-acl.md) or a [network security group](../virtual-network/virtual-networks-nsg.md) rule.</span></span>

> [!NOTE]
> <span data-ttu-id="33eab-153">Per altre informazioni sui diversi tipi di avvisi, vedere [Avvisi di sicurezza per tipo nel Centro sicurezza di Azure](security-center-alerts-type.md).</span><span class="sxs-lookup"><span data-stu-id="33eab-153">For more information on the different types of alerts, read [Security Alerts by Type in Azure Security Center](security-center-alerts-type.md).</span></span>
>
>

## <a name="see-also"></a><span data-ttu-id="33eab-154">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="33eab-154">See also</span></span>
<span data-ttu-id="33eab-155">In questo documento si è appreso come configurare i criteri di sicurezza nel Centro sicurezza.</span><span class="sxs-lookup"><span data-stu-id="33eab-155">In this document, you learned how to configure security policies in Security Center.</span></span> <span data-ttu-id="33eab-156">Per altre informazioni sul Centro sicurezza, vedere gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="33eab-156">To learn more about Security Center, see the following:</span></span>

* [<span data-ttu-id="33eab-157">Gestione degli eventi imprevisti della sicurezza nel Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="33eab-157">Handling Security Incident in Azure Security Center</span></span>](security-center-incident.md)
* [<span data-ttu-id="33eab-158">Funzionalità di rilevamento del Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="33eab-158">Azure Security Center Detection Capabilities</span></span>](security-center-detection-capabilities.md)
* [<span data-ttu-id="33eab-159">Guida alla pianificazione e alla gestione del Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="33eab-159">Azure Security Center Planning and Operations Guide</span></span>](security-center-planning-and-operations-guide.md)
* <span data-ttu-id="33eab-160">[Domande frequenti sul Centro sicurezza di Azure](security-center-faq.md) : domande frequenti sull'uso del servizio.</span><span class="sxs-lookup"><span data-stu-id="33eab-160">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="33eab-161">[Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/) : post di blog sulla sicurezza e sulla conformità di Azure.</span><span class="sxs-lookup"><span data-stu-id="33eab-161">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Find blog posts about Azure security and compliance.</span></span>
