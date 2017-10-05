---
title: Abilitare i gruppi di sicurezza di rete nel Centro sicurezza di Azure | Microsoft Docs
description: Questo documento illustra come implementare la raccomandazione **Abilita i gruppi di sicurezza di rete** del Centro sicurezza di Azure.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: f53ed853-ffaf-4530-a019-1906ba6f341b
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 1e034d59d8847f237fa0d4c772344d45cd618576
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="enable-network-security-groups-in-azure-security-center"></a><span data-ttu-id="798fa-103">Abilitare i gruppi di sicurezza di rete nel Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="798fa-103">Enable Network Security Groups in Azure Security Center</span></span>
<span data-ttu-id="798fa-104">Se non è già disponibile, il Centro sicurezza di Azure consiglia l'abilitazione di un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="798fa-104">Azure Security Center recommends that you enable a network security group (NSG) if one is not already enabled.</span></span> <span data-ttu-id="798fa-105">I gruppi di sicurezza di rete contengono un elenco di regole dell'elenco di controllo di accesso (ACL) che consentono o rifiutano il traffico di rete alle istanze VM in una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="798fa-105">NSGs contain a list of Access Control List (ACL) rules that allow or deny network traffic to your VM instances in a Virtual Network.</span></span> <span data-ttu-id="798fa-106">I gruppi di sicurezza di rete possono essere associati a subnet o singole istanze VM in una subnet.</span><span class="sxs-lookup"><span data-stu-id="798fa-106">NSGs can be associated with either subnets or individual VM instances within that subnet.</span></span> <span data-ttu-id="798fa-107">Quando un gruppo di sicurezza di rete viene associato a una subnet, le regole ACL si applicano a tutte le istanze di VM in tale subnet.</span><span class="sxs-lookup"><span data-stu-id="798fa-107">When an NSG is associated with a subnet, the ACL rules apply to all the VM instances in that subnet.</span></span> <span data-ttu-id="798fa-108">Il traffico verso una singola VM può essere inoltre ulteriormente limitato associando un gruppo di sicurezza di rete direttamente a tale VM.</span><span class="sxs-lookup"><span data-stu-id="798fa-108">In addition, traffic to an individual VM can be restricted further by associating an NSG directly to that VM.</span></span> <span data-ttu-id="798fa-109">Per altre informazioni, vedere [Che cos'è un gruppo di sicurezza di rete](../virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="798fa-109">To learn more see [What is a Network Security Group (NSG)?](../virtual-network/virtual-networks-nsg.md)</span></span>

<span data-ttu-id="798fa-110">Se i gruppi di sicurezza di rete non sono stati abilitati, il Centro sicurezza presenta all'utente due indicazioni, ovvero Abilita i gruppi di sicurezza di rete nelle subnet e Abilita i gruppi di sicurezza di rete sulle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="798fa-110">If you do not have NSGs enabled, Security Center presents two recommendations to you: Enable Network Security Groups on subnets and Enable Network Security Groups on virtual machines.</span></span> <span data-ttu-id="798fa-111">È possibile scegliere il livello a cui applicare i gruppi di sicurezza di rete, ovvero subnet o VM.</span><span class="sxs-lookup"><span data-stu-id="798fa-111">You choose which level, subnet or VM, to apply NSGs.</span></span>

> [!NOTE]
> <span data-ttu-id="798fa-112">Il documento introduce il servizio usando una distribuzione di esempio.</span><span class="sxs-lookup"><span data-stu-id="798fa-112">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="798fa-113">Questa non è una guida dettagliata.</span><span class="sxs-lookup"><span data-stu-id="798fa-113">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="798fa-114">Implementare la raccomandazione</span><span class="sxs-lookup"><span data-stu-id="798fa-114">Implement the recommendation</span></span>
1. <span data-ttu-id="798fa-115">Nel pannello **Raccomandazioni** selezionare **Abilita i gruppi di sicurezza di rete** nelle subnet o sulle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="798fa-115">In the **Recommendations** blade, select **Enable Network Security Groups** on subnets or on virtual machines.</span></span>
   <span data-ttu-id="798fa-116">![Abilitare i gruppi di sicurezza di rete][1]</span><span class="sxs-lookup"><span data-stu-id="798fa-116">![Enable Network Security Groups][1]</span></span>
2. <span data-ttu-id="798fa-117">Verrà visualizzato il pannello **Configura i gruppi di sicurezza di rete mancanti** per le subnet o le macchine virtuali, in base alla raccomandazione selezionata.</span><span class="sxs-lookup"><span data-stu-id="798fa-117">This opens the blade **Configure Missing Network Security Groups** for subnets or for virtual machines, depending on the recommendation that you selected.</span></span> <span data-ttu-id="798fa-118">Selezionare una subnet o una macchina virtuale su cui configurare un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="798fa-118">Select a subnet or a virtual machine to configure an NSG on.</span></span>

   ![Configurare i gruppi di sicurezza di rete per la subnet][2]

   ![Configurare i gruppi di sicurezza di rete per le macchine virtuali][3]
3. <span data-ttu-id="798fa-121">Nel pannello **Scegli un gruppo di sicurezza di rete** selezionare un gruppo di sicurezza di rete esistente o selezionare **Crea nuovo** per crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="798fa-121">On the **Choose network security group** blade, select an existing NSG or select **Create new** to create an NSG.</span></span>

   ![Scegli un gruppo di sicurezza di rete][4]

<span data-ttu-id="798fa-123">Se si crea un gruppo di sicurezza di rete, seguire la procedura illustrata in [Come gestire gruppi di sicurezza di rete tramite il portale di Azure](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) per creare un gruppo di sicurezza di rete e configurare le regole di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="798fa-123">If you create an NSG, follow the steps in [How to manage NSGs using the Azure portal](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) to create an NSG and set security rules.</span></span>

## <a name="see-also"></a><span data-ttu-id="798fa-124">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="798fa-124">See also</span></span>
<span data-ttu-id="798fa-125">Questo articolo ha illustrato come implementare la raccomandazione "Abilita i gruppi di sicurezza di rete" per subnet o macchine virtuali nel Centro sicurezza.</span><span class="sxs-lookup"><span data-stu-id="798fa-125">This article showed you how to implement the Security Center recommendation "Enable Network Security Groups" for subnets or virtual machines.</span></span> <span data-ttu-id="798fa-126">Per altre informazioni sull'abilitazione dei gruppi di sicurezza di rete, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="798fa-126">To learn more about enabling NSGs, see the following:</span></span>

* [<span data-ttu-id="798fa-127">Che cos'è un gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="798fa-127">What is a Network Security Group (NSG)?</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="798fa-128">Come gestire gruppi di sicurezza di rete tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="798fa-128">How to manage NSGs using the Azure portal</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

<span data-ttu-id="798fa-129">Per altre informazioni sul Centro sicurezza, vedere gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="798fa-129">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="798fa-130">[Impostazione dei criteri di sicurezza nel Centro sicurezza di Azure](security-center-policies.md) : informazioni su come configurare i criteri di sicurezza per le sottoscrizioni e i gruppi di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="798fa-130">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="798fa-131">[Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](security-center-recommendations.md) : informazioni sul modo in cui le raccomandazioni semplificano la protezione delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="798fa-131">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="798fa-132">[Monitoraggio dell'integrità della sicurezza nel Centro sicurezza di Azure](security-center-monitoring.md) : informazioni su come monitorare l'integrità delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="798fa-132">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="798fa-133">[Gestione e risposta agli avvisi di sicurezza nel Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) : informazioni su come gestire e rispondere agli avvisi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="798fa-133">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="798fa-134">[Monitoraggio delle soluzioni dei partner con il Centro sicurezza di Azure](security-center-partner-solutions.md) : informazioni su come monitorare lo stato integrità delle soluzioni dei partner.</span><span class="sxs-lookup"><span data-stu-id="798fa-134">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="798fa-135">[Domande frequenti sul Centro sicurezza di Azure](security-center-faq.md) : domande frequenti sull'uso del servizio.</span><span class="sxs-lookup"><span data-stu-id="798fa-135">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="798fa-136">[Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/) : informazioni e notizie aggiornate sulla sicurezza di Azure.</span><span class="sxs-lookup"><span data-stu-id="798fa-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-nsg/enable-nsg.png
[2]:./media/security-center-enable-nsg/configure-nsg-for-subnet.png
[3]: ./media/security-center-enable-nsg/configure-nsg-for-vm.png
[4]: ./media/security-center-enable-nsg/choose-nsg.png
