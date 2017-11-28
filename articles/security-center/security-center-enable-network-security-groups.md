---
title: Gruppi di sicurezza di rete nel Centro protezione Azure aaaEnable | Documenti Microsoft
description: Questo documento viene illustrato come tooimplement hello raccomandazione Centro sicurezza di Azure * * abilitare rete sicurezza gruppi * *.
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
ms.openlocfilehash: 2f70fe432aa452f833a5c322d13102ebbd6dbb69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-network-security-groups-in-azure-security-center"></a><span data-ttu-id="23c0d-103">Abilitare i gruppi di sicurezza di rete nel Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="23c0d-103">Enable Network Security Groups in Azure Security Center</span></span>
<span data-ttu-id="23c0d-104">Se non è già disponibile, il Centro sicurezza di Azure consiglia l'abilitazione di un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="23c0d-104">Azure Security Center recommends that you enable a network security group (NSG) if one is not already enabled.</span></span> <span data-ttu-id="23c0d-105">NSGs contiene un elenco di regole di elenco di controllo di accesso (ACL) che consentono o negano il traffico di rete tooyour istanze di macchina virtuale in una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="23c0d-105">NSGs contain a list of Access Control List (ACL) rules that allow or deny network traffic tooyour VM instances in a Virtual Network.</span></span> <span data-ttu-id="23c0d-106">I gruppi di sicurezza di rete possono essere associati a subnet o singole istanze VM in una subnet.</span><span class="sxs-lookup"><span data-stu-id="23c0d-106">NSGs can be associated with either subnets or individual VM instances within that subnet.</span></span> <span data-ttu-id="23c0d-107">Quando un gruppo è associata a una subnet, regole ACL hello si applicano le istanze VM hello tooall nella subnet.</span><span class="sxs-lookup"><span data-stu-id="23c0d-107">When an NSG is associated with a subnet, hello ACL rules apply tooall hello VM instances in that subnet.</span></span> <span data-ttu-id="23c0d-108">Inoltre, il traffico tooan singole macchine Virtuali è possibile limitare ulteriormente l'associazione di un gruppo direttamente toothat macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="23c0d-108">In addition, traffic tooan individual VM can be restricted further by associating an NSG directly toothat VM.</span></span> <span data-ttu-id="23c0d-109">vedere più toolearn [che cos'è un gruppo di sicurezza di rete (gruppo)?](../virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="23c0d-109">toolearn more see [What is a Network Security Group (NSG)?](../virtual-network/virtual-networks-nsg.md)</span></span>

<span data-ttu-id="23c0d-110">Se non si dispone di NSGs abilitata, il Centro sicurezza PC presenta due indicazioni tooyou: abilitare dei gruppi di sicurezza di rete su subnet e attivare dei gruppi di sicurezza di rete nelle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="23c0d-110">If you do not have NSGs enabled, Security Center presents two recommendations tooyou: Enable Network Security Groups on subnets and Enable Network Security Groups on virtual machines.</span></span> <span data-ttu-id="23c0d-111">Si sceglie il livello, subnet o macchina virtuale, tooapply NSGs.</span><span class="sxs-lookup"><span data-stu-id="23c0d-111">You choose which level, subnet or VM, tooapply NSGs.</span></span>

> [!NOTE]
> <span data-ttu-id="23c0d-112">Questo documento introduce servizio hello utilizzando un esempio di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="23c0d-112">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="23c0d-113">Questa non è una guida dettagliata.</span><span class="sxs-lookup"><span data-stu-id="23c0d-113">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="23c0d-114">Implementare la raccomandazione hello</span><span class="sxs-lookup"><span data-stu-id="23c0d-114">Implement hello recommendation</span></span>
1. <span data-ttu-id="23c0d-115">In hello **indicazioni** pannello seleziona **abilitare gruppi di sicurezza di rete** in subnet o su macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="23c0d-115">In hello **Recommendations** blade, select **Enable Network Security Groups** on subnets or on virtual machines.</span></span>
   <span data-ttu-id="23c0d-116">![Abilitare i gruppi di sicurezza di rete][1]</span><span class="sxs-lookup"><span data-stu-id="23c0d-116">![Enable Network Security Groups][1]</span></span>
2. <span data-ttu-id="23c0d-117">Verrà aperto il pannello hello **configurare gruppi di sicurezza rete mancante** per le subnet o per le macchine virtuali, a seconda della raccomandazione hello selezionato.</span><span class="sxs-lookup"><span data-stu-id="23c0d-117">This opens hello blade **Configure Missing Network Security Groups** for subnets or for virtual machines, depending on hello recommendation that you selected.</span></span> <span data-ttu-id="23c0d-118">Selezionare una subnet o tooconfigure una macchina virtuale un gruppo in.</span><span class="sxs-lookup"><span data-stu-id="23c0d-118">Select a subnet or a virtual machine tooconfigure an NSG on.</span></span>

   ![Configurare i gruppi di sicurezza di rete per la subnet][2]

   ![Configurare i gruppi di sicurezza di rete per le macchine virtuali][3]
3. <span data-ttu-id="23c0d-121">In hello **scegliere gruppo di sicurezza di rete** pannello selezionare un gruppo esistente oppure **Crea nuovo** toocreate un gruppo.</span><span class="sxs-lookup"><span data-stu-id="23c0d-121">On hello **Choose network security group** blade, select an existing NSG or select **Create new** toocreate an NSG.</span></span>

   ![Scegli un gruppo di sicurezza di rete][4]

<span data-ttu-id="23c0d-123">Se si crea un gruppo, seguire i passaggi di hello in [come NSGs toomanage utilizzando hello Azure portal](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) toocreate un gruppo e impostare le regole di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="23c0d-123">If you create an NSG, follow hello steps in [How toomanage NSGs using hello Azure portal](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) toocreate an NSG and set security rules.</span></span>

## <a name="see-also"></a><span data-ttu-id="23c0d-124">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="23c0d-124">See also</span></span>
<span data-ttu-id="23c0d-125">In questo articolo ha illustrato come tooimplement hello Centro sicurezza PC indicazione "abilitare gruppi di sicurezza rete" per le macchine virtuali o subnet.</span><span class="sxs-lookup"><span data-stu-id="23c0d-125">This article showed you how tooimplement hello Security Center recommendation "Enable Network Security Groups" for subnets or virtual machines.</span></span> <span data-ttu-id="23c0d-126">toolearn ulteriori informazioni su attivazione NSGs, vedere l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="23c0d-126">toolearn more about enabling NSGs, see hello following:</span></span>

* [<span data-ttu-id="23c0d-127">Che cos'è un gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="23c0d-127">What is a Network Security Group (NSG)?</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="23c0d-128">Come NSGs toomanage utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="23c0d-128">How toomanage NSGs using hello Azure portal</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

<span data-ttu-id="23c0d-129">toolearn ulteriori informazioni su Centro di sicurezza, vedere l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="23c0d-129">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="23c0d-130">[L'impostazione di criteri di sicurezza nel Centro protezione Azure](security-center-policies.md) -informazioni su come tooconfigure i criteri di sicurezza per le sottoscrizioni di Azure e i gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="23c0d-130">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="23c0d-131">[Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](security-center-recommendations.md) : informazioni sul modo in cui le raccomandazioni semplificano la protezione delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="23c0d-131">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="23c0d-132">[Il monitoraggio dello stato di sicurezza nel Centro protezione Azure](security-center-monitoring.md) -informazioni su come toomonitor hello integrità delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="23c0d-132">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="23c0d-133">[La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) -informazioni su come avvisi toosecurity toomanage e rispondere.</span><span class="sxs-lookup"><span data-stu-id="23c0d-133">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="23c0d-134">[Monitoraggio di soluzioni dei partner con Centro sicurezza di Azure](security-center-partner-solutions.md) -informazioni su come toomonitor hello lo stato di integrità delle soluzioni di partner.</span><span class="sxs-lookup"><span data-stu-id="23c0d-134">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="23c0d-135">[Domande frequenti su Centro sicurezza di Azure](security-center-faq.md) -domande frequenti sull'utilizzo di hello servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="23c0d-135">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="23c0d-136">[Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/) -ottenere informazioni e notizie sicurezza di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="23c0d-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-nsg/enable-nsg.png
[2]:./media/security-center-enable-nsg/configure-nsg-for-subnet.png
[3]: ./media/security-center-enable-nsg/configure-nsg-for-vm.png
[4]: ./media/security-center-enable-nsg/choose-nsg.png
