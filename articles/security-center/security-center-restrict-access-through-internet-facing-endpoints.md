---
title: Limitare l'accesso tramite endpoint con connessione Internet in Centro sicurezza di Azure | Documentazione Microsoft
description: Questo documento illustra come implementare la raccomandazione **Restrict access through Internet facing endpoint** (Limita accesso tramite endpoint con connessione Internet) del Centro sicurezza di Azure.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 727d88c9-163b-4ea0-a4ce-3be43686599f
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: f7309c617f1705205e2c9f1b1b48d141391d45da
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="restrict-access-through-internet-facing-endpoints-in-azure-security-center"></a><span data-ttu-id="29a58-103">Limitare l'accesso tramite endpoint con connessione Internet in Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="29a58-103">Restrict access through Internet-facing endpoints in Azure Security Center</span></span>
<span data-ttu-id="29a58-104">Il Centro sicurezza di Azure consiglia di limitare l'accesso tramite endpoint con connessione Internet se uno dei gruppi di sicurezza di rete contiene una o più regole in ingresso che consentono l'accesso da "qualsiasi" indirizzo IP di origine.</span><span class="sxs-lookup"><span data-stu-id="29a58-104">Azure Security Center will recommend that you restrict access through Internet-facing endpoints if any of your Network Security Groups (NSGs) has one or more inbound rules that allow access from “any” source IP address.</span></span> <span data-ttu-id="29a58-105">L'accesso su "qualsiasi" origine potrebbe abilitare utenti malintenzionati ad accedere alle risorse.</span><span class="sxs-lookup"><span data-stu-id="29a58-105">Opening access to “any” may enable attackers to access your resources.</span></span> <span data-ttu-id="29a58-106">Il Centro sicurezza consiglierà di modificare queste regole in ingresso per limitare l'accesso agli indirizzi IP di origine che necessitano effettivamente dell'accesso.</span><span class="sxs-lookup"><span data-stu-id="29a58-106">Security Center will recommend that you edit these inbound rules to restrict access to source IP addresses that actually need access.</span></span>

<span data-ttu-id="29a58-107">Questa raccomandazione viene generata per qualsiasi porta Web con "any" come origine.</span><span class="sxs-lookup"><span data-stu-id="29a58-107">This recommendation is generated for any non-web port that has "any" as source.</span></span>

> [!NOTE]
> <span data-ttu-id="29a58-108">Il documento introduce il servizio usando una distribuzione di esempio.</span><span class="sxs-lookup"><span data-stu-id="29a58-108">This document introduces the service by using an example deployment.</span></span> <span data-ttu-id="29a58-109">Questa non è una guida dettagliata.</span><span class="sxs-lookup"><span data-stu-id="29a58-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="29a58-110">Implementare la raccomandazione</span><span class="sxs-lookup"><span data-stu-id="29a58-110">Implement the recommendation</span></span>
1. <span data-ttu-id="29a58-111">Nel pannello **Indicazioni** selezionare **Limita l'accesso tramite un endpoint con connessione Internet**.</span><span class="sxs-lookup"><span data-stu-id="29a58-111">In the **Recommendations blade**, select **Restrict access through Internet facing endpoint**.</span></span>

   ![Restrict access through Internet facing endpoint (Limita accesso tramite endpoint con connessione Internet)][1]
2. <span data-ttu-id="29a58-113">Verrà visualizzato il pannello **Limita l'accesso tramite un endpoint con connessione Internet**.</span><span class="sxs-lookup"><span data-stu-id="29a58-113">This opens the blade **Restrict access through Internet facing endpoint**.</span></span> <span data-ttu-id="29a58-114">Questo pannello elenca le macchine virtuali (VM) con regole in ingresso che creano un potenziale problema di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="29a58-114">This blade lists the virtual machines (VMs) with inbound rules that create a potential security issue.</span></span> <span data-ttu-id="29a58-115">Selezionare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="29a58-115">Select a VM.</span></span>

   ![Selezionare una macchina virtuale][2]
3. <span data-ttu-id="29a58-117">Il pannello **Gruppo di sicurezza di rete** visualizza le informazioni sul gruppo di sicurezza di rete, le regole in ingresso correlate e la VM associata.</span><span class="sxs-lookup"><span data-stu-id="29a58-117">The **NSG** blade displays Network Security Group information, related inbound rules, and the associated VM.</span></span> <span data-ttu-id="29a58-118">Selezionare **Modifica le regole in ingresso** per procedere con la modifica di una regola in ingresso.</span><span class="sxs-lookup"><span data-stu-id="29a58-118">Select **Edit inbound rules** to proceed with editing an inbound rule.</span></span>

   ![Pannello Gruppo di sicurezza di rete][3]
4. <span data-ttu-id="29a58-120">Nel pannello **Regole di sicurezza in ingresso** selezionare la regola in ingresso da modificare.</span><span class="sxs-lookup"><span data-stu-id="29a58-120">On the **Inbound security rules** blade select the inbound rule to edit.</span></span> <span data-ttu-id="29a58-121">In questo esempio selezioniamo **Consenti Web**.</span><span class="sxs-lookup"><span data-stu-id="29a58-121">In this example, let’s select **AllowWeb**.</span></span>

   ![Regole di sicurezza in ingresso][4]

   <span data-ttu-id="29a58-123">Si noti che è possibile anche selezionare **Regole predefinite** per visualizzare il set di regole predefinite contenute in tutti i gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="29a58-123">Note, you can also select **Default rules** to see the set of default rules contained by all NSGs.</span></span> <span data-ttu-id="29a58-124">Le regole predefinite non possono essere eliminate, ma poiché hanno la priorità più bassa, è possibile eseguirne l'override con le regole create dall'utente.</span><span class="sxs-lookup"><span data-stu-id="29a58-124">The default rules cannot be deleted but, because they are assigned a lower priority, they can be overridden by the rules that you create.</span></span> <span data-ttu-id="29a58-125">Altre informazioni sulle [regole predefinite](../virtual-network/virtual-networks-nsg.md#default-rules).</span><span class="sxs-lookup"><span data-stu-id="29a58-125">Learn more about [default rules](../virtual-network/virtual-networks-nsg.md#default-rules).</span></span>

   ![Regole predefinite][5]
5. <span data-ttu-id="29a58-127">Nel pannello **AllowWeb** (Consenti Web) modificare le proprietà della regola in ingresso in modo che **Origine** sia un indirizzo IP o un blocco di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="29a58-127">On the **AllowWeb** blade, edit the properties of the inbound rule so that the **Source** is an IP address or block of IP addresses.</span></span> <span data-ttu-id="29a58-128">Per altre informazioni sulle proprietà della regola in ingresso, vedere [Regole NSG](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span><span class="sxs-lookup"><span data-stu-id="29a58-128">To learn more about the properties of the inbound rule, see [NSG rules](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span></span>

   ![Modificare la regola in ingresso][6]

## <a name="see-also"></a><span data-ttu-id="29a58-130">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="29a58-130">See also</span></span>
<span data-ttu-id="29a58-131">Questo articolo illustra come implementare la raccomandazione "Restrict access through Internet facing endpoint" (Limita accesso tramite endpoint con connessione Internet) del Centro sicurezza.</span><span class="sxs-lookup"><span data-stu-id="29a58-131">This article showed you how to implement the Security Center recommendation "Restrict access through Internet facing endpoint.”</span></span> <span data-ttu-id="29a58-132">Per altre informazioni sull'abilitazione dei gruppi di sicurezza di rete e delle regole, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="29a58-132">To learn more about enabling NSGs and rules, see the following:</span></span>

* [<span data-ttu-id="29a58-133">Che cos'è un gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="29a58-133">What is a Network Security Group (NSG)?</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="29a58-134">Come gestire gruppi di sicurezza di rete tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="29a58-134">How to manage NSGs using the Azure portal</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

<span data-ttu-id="29a58-135">Per altre informazioni sul Centro sicurezza, vedere gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="29a58-135">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="29a58-136">[Impostazione dei criteri di sicurezza nel Centro sicurezza di Azure](security-center-policies.md): informazioni su come configurare i criteri di sicurezza per le sottoscrizioni e i gruppi di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="29a58-136">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="29a58-137">[Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](security-center-recommendations.md): informazioni sul modo in cui le raccomandazioni semplificano la protezione delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="29a58-137">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="29a58-138">[Monitoraggio dell'integrità della sicurezza nel Centro sicurezza di Azure](security-center-monitoring.md): informazioni su come monitorare l'integrità delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="29a58-138">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="29a58-139">[Gestione e risposta agli avvisi di sicurezza nel Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md): informazioni su come gestire e rispondere agli avvisi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="29a58-139">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="29a58-140">[Monitoraggio delle soluzioni dei partner con il Centro sicurezza di Azure](security-center-partner-solutions.md) : informazioni su come monitorare lo stato integrità delle soluzioni dei partner.</span><span class="sxs-lookup"><span data-stu-id="29a58-140">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="29a58-141">[Domande frequenti sul Centro sicurezza di Azure](security-center-faq.md): domande frequenti sull'uso del servizio.</span><span class="sxs-lookup"><span data-stu-id="29a58-141">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="29a58-142">[Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/): informazioni e notizie aggiornate sulla sicurezza di Azure.</span><span class="sxs-lookup"><span data-stu-id="29a58-142">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/restrict-access-thru-internet-facing-endpoint.png
[2]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/select-a-vm.png
[3]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/network-security-group-blade.png
[4]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/inbound-security-rules.png
[5]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/default-rules.png
[6]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/edit-inbound-rule.png
