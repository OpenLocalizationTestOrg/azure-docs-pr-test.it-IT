---
title: accesso aaaRestrict tramite gli endpoint con connessione Internet nel Centro sicurezza di Azure | Documenti Microsoft
description: "Questo documento viene illustrato come tooimplement hello raccomandazione Centro sicurezza di Azure * * limitare l'accesso tramite endpoint * * è connessa a Internet."
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
ms.openlocfilehash: ee72497088618d4db29b5ae4183f4fe77b498423
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="restrict-access-through-internet-facing-endpoints-in-azure-security-center"></a><span data-ttu-id="de3e0-103">Limitare l'accesso tramite endpoint con connessione Internet in Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="de3e0-103">Restrict access through Internet-facing endpoints in Azure Security Center</span></span>
<span data-ttu-id="de3e0-104">Il Centro sicurezza di Azure consiglia di limitare l'accesso tramite endpoint con connessione Internet se uno dei gruppi di sicurezza di rete contiene una o più regole in ingresso che consentono l'accesso da "qualsiasi" indirizzo IP di origine.</span><span class="sxs-lookup"><span data-stu-id="de3e0-104">Azure Security Center will recommend that you restrict access through Internet-facing endpoints if any of your Network Security Groups (NSGs) has one or more inbound rules that allow access from “any” source IP address.</span></span> <span data-ttu-id="de3e0-105">Apertura accesso troppo "any" può attivare gli utenti malintenzionati tooaccess le risorse.</span><span class="sxs-lookup"><span data-stu-id="de3e0-105">Opening access too“any” may enable attackers tooaccess your resources.</span></span> <span data-ttu-id="de3e0-106">Centro sicurezza PC verrà consiglia di modificare queste regole in entrata toorestrict accesso toosource indirizzi IP che effettivamente richiedono l'accesso.</span><span class="sxs-lookup"><span data-stu-id="de3e0-106">Security Center will recommend that you edit these inbound rules toorestrict access toosource IP addresses that actually need access.</span></span>

<span data-ttu-id="de3e0-107">Questa raccomandazione viene generata per qualsiasi porta Web con "any" come origine.</span><span class="sxs-lookup"><span data-stu-id="de3e0-107">This recommendation is generated for any non-web port that has "any" as source.</span></span>

> [!NOTE]
> <span data-ttu-id="de3e0-108">Questo documento introduce servizio hello utilizzando un esempio di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="de3e0-108">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="de3e0-109">Questa non è una guida dettagliata.</span><span class="sxs-lookup"><span data-stu-id="de3e0-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="de3e0-110">Implementare la raccomandazione hello</span><span class="sxs-lookup"><span data-stu-id="de3e0-110">Implement hello recommendation</span></span>
1. <span data-ttu-id="de3e0-111">In hello **pannello indicazioni**selezionare **limitare l'accesso tramite endpoint per Internet**.</span><span class="sxs-lookup"><span data-stu-id="de3e0-111">In hello **Recommendations blade**, select **Restrict access through Internet facing endpoint**.</span></span>

   ![Restrict access through Internet facing endpoint (Limita accesso tramite endpoint con connessione Internet)][1]
2. <span data-ttu-id="de3e0-113">Verrà aperto il pannello hello **limitare l'accesso tramite endpoint per Internet**.</span><span class="sxs-lookup"><span data-stu-id="de3e0-113">This opens hello blade **Restrict access through Internet facing endpoint**.</span></span> <span data-ttu-id="de3e0-114">Questo pannello elenca hello le macchine virtuali (VM) con le regole in entrata che creano un potenziale problema di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="de3e0-114">This blade lists hello virtual machines (VMs) with inbound rules that create a potential security issue.</span></span> <span data-ttu-id="de3e0-115">Selezionare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="de3e0-115">Select a VM.</span></span>

   ![Selezionare una macchina virtuale][2]
3. <span data-ttu-id="de3e0-117">Hello **NSG** pannello Visualizza le informazioni di gruppo di sicurezza di rete, le regole in entrata correlate, e hello associati macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="de3e0-117">hello **NSG** blade displays Network Security Group information, related inbound rules, and hello associated VM.</span></span> <span data-ttu-id="de3e0-118">Selezionare **modificare le regole in entrata** tooproceed con la modifica di una regola in ingresso.</span><span class="sxs-lookup"><span data-stu-id="de3e0-118">Select **Edit inbound rules** tooproceed with editing an inbound rule.</span></span>

   ![Pannello Gruppo di sicurezza di rete][3]
4. <span data-ttu-id="de3e0-120">In hello **sicurezza regole connessioni in entrata** pannello selezionare hello tooedit regola in ingresso.</span><span class="sxs-lookup"><span data-stu-id="de3e0-120">On hello **Inbound security rules** blade select hello inbound rule tooedit.</span></span> <span data-ttu-id="de3e0-121">In questo esempio selezioniamo **Consenti Web**.</span><span class="sxs-lookup"><span data-stu-id="de3e0-121">In this example, let’s select **AllowWeb**.</span></span>

   ![Regole di sicurezza in ingresso][4]

   <span data-ttu-id="de3e0-123">Si noti che è anche possibile selezionare **regole predefinite** set hello toosee di regole predefinite contenute NSGs tutti.</span><span class="sxs-lookup"><span data-stu-id="de3e0-123">Note, you can also select **Default rules** toosee hello set of default rules contained by all NSGs.</span></span> <span data-ttu-id="de3e0-124">non è possibile eliminare le regole predefinite di Hello ma, poiché vengono assegnati una priorità più bassa, possono essere sostituite dalle regole di hello creati.</span><span class="sxs-lookup"><span data-stu-id="de3e0-124">hello default rules cannot be deleted but, because they are assigned a lower priority, they can be overridden by hello rules that you create.</span></span> <span data-ttu-id="de3e0-125">Altre informazioni sulle [regole predefinite](../virtual-network/virtual-networks-nsg.md#default-rules).</span><span class="sxs-lookup"><span data-stu-id="de3e0-125">Learn more about [default rules](../virtual-network/virtual-networks-nsg.md#default-rules).</span></span>

   ![Regole predefinite][5]
5. <span data-ttu-id="de3e0-127">In hello **AllowWeb** pannello hello di modificare le proprietà della regola in ingresso di hello in modo che hello **origine** è un indirizzo IP o un blocco di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="de3e0-127">On hello **AllowWeb** blade, edit hello properties of hello inbound rule so that hello **Source** is an IP address or block of IP addresses.</span></span> <span data-ttu-id="de3e0-128">vedere toolearn più sulle proprietà hello della regola in ingresso di hello [regole NSG](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span><span class="sxs-lookup"><span data-stu-id="de3e0-128">toolearn more about hello properties of hello inbound rule, see [NSG rules](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span></span>

   ![Modificare la regola in ingresso][6]

## <a name="see-also"></a><span data-ttu-id="de3e0-130">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="de3e0-130">See also</span></span>
<span data-ttu-id="de3e0-131">In questo articolo ha illustrato come tooimplement hello Centro sicurezza PC indicazione "limitare l'accesso tramite endpoint per Internet."</span><span class="sxs-lookup"><span data-stu-id="de3e0-131">This article showed you how tooimplement hello Security Center recommendation "Restrict access through Internet facing endpoint.”</span></span> <span data-ttu-id="de3e0-132">toolearn ulteriori informazioni su attivazione NSGs e regole, vedere l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="de3e0-132">toolearn more about enabling NSGs and rules, see hello following:</span></span>

* [<span data-ttu-id="de3e0-133">Che cos'è un gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="de3e0-133">What is a Network Security Group (NSG)?</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="de3e0-134">Come NSGs toomanage utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="de3e0-134">How toomanage NSGs using hello Azure portal</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

<span data-ttu-id="de3e0-135">toolearn ulteriori informazioni su Centro di sicurezza, vedere l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="de3e0-135">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="de3e0-136">[L'impostazione di criteri di sicurezza nel Centro protezione Azure](security-center-policies.md)-informazioni su come tooconfigure i criteri di sicurezza per le sottoscrizioni di Azure e i gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="de3e0-136">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="de3e0-137">[Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](security-center-recommendations.md): informazioni sul modo in cui le raccomandazioni semplificano la protezione delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="de3e0-137">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="de3e0-138">[Il monitoraggio dello stato di sicurezza nel Centro protezione Azure](security-center-monitoring.md)-informazioni su come toomonitor hello integrità delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="de3e0-138">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="de3e0-139">[La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md)-informazioni su come avvisi toosecurity toomanage e rispondere.</span><span class="sxs-lookup"><span data-stu-id="de3e0-139">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="de3e0-140">[Monitoraggio di soluzioni dei partner con Centro sicurezza di Azure](security-center-partner-solutions.md) -informazioni su come toomonitor hello lo stato di integrità delle soluzioni di partner.</span><span class="sxs-lookup"><span data-stu-id="de3e0-140">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="de3e0-141">[Domande frequenti su Centro sicurezza di Azure](security-center-faq.md)-domande frequenti sull'utilizzo di hello servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="de3e0-141">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="de3e0-142">[Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/)-ottenere informazioni e notizie sicurezza di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="de3e0-142">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/restrict-access-thru-internet-facing-endpoint.png
[2]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/select-a-vm.png
[3]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/network-security-group-blade.png
[4]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/inbound-security-rules.png
[5]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/default-rules.png
[6]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/edit-inbound-rule.png
