---
title: Abilitare l'agente di macchine virtuali nel Centro sicurezza di Azure | Microsoft Docs
description: Questo documento illustra come implementare la raccomandazione **Abilita l'agente di macchine virtuali** del Centro sicurezza di Azure.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 5b431c25-4241-45b7-9556-cf2a1956f3da
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 337a7adfd93c76882a749685702bea6d1524c96a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="enable-vm-agent-in-azure-security-center"></a><span data-ttu-id="6fc13-103">Abilita l'agente di macchine virtuali nel Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="6fc13-103">Enable VM Agent in Azure Security Center</span></span>
<span data-ttu-id="6fc13-104">Per [abilitare la raccolta dati](security-center-enable-data-collection.md), l'agente di macchine virtuali deve essere installato sulle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="6fc13-104">The VM Agent must be installed on virtual machines (VMs) in order to [enable data collection](security-center-enable-data-collection.md).</span></span>  <span data-ttu-id="6fc13-105">Il Centro sicurezza di Azure consente di visualizzare le VM che richiedono l'agente di macchine virtuali e consiglia di abilitare l'agente di macchine virtuali su queste VM.</span><span class="sxs-lookup"><span data-stu-id="6fc13-105">Azure Security Center enables you to see which VMs require the VM Agent and will recommend that you enable the VM Agent on those VMs.</span></span>

<span data-ttu-id="6fc13-106">Per impostazione predefinita, l'agente di macchine virtuali è installato nelle macchine virtuali distribuite da Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6fc13-106">The VM Agent is installed by default for VMs that are deployed from the Azure Marketplace.</span></span> <span data-ttu-id="6fc13-107">L'articolo relativo all' [agente di macchine virtuali e relative estensioni, parte 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) fornisce informazioni su come installare l'agente di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="6fc13-107">The article [VM Agent and Extensions – Part 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) provides information on how to install the VM Agent.</span></span>

> [!NOTE]
> <span data-ttu-id="6fc13-108">Il documento introduce il servizio usando una distribuzione di esempio.</span><span class="sxs-lookup"><span data-stu-id="6fc13-108">This document introduces the service by using an example deployment.</span></span> <span data-ttu-id="6fc13-109">Questa non è una guida dettagliata.</span><span class="sxs-lookup"><span data-stu-id="6fc13-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="6fc13-110">Implementare la raccomandazione</span><span class="sxs-lookup"><span data-stu-id="6fc13-110">Implement the recommendation</span></span>
1. <span data-ttu-id="6fc13-111">Nel pannello **Indicazioni** selezionare **Abilita l'agente di macchine virtuali**.</span><span class="sxs-lookup"><span data-stu-id="6fc13-111">In the **Recommendations blade**, select **Enable VM Agent**.</span></span>
   <span data-ttu-id="6fc13-112">![Abilita l'agente di macchine virtuali][1]</span><span class="sxs-lookup"><span data-stu-id="6fc13-112">![Enable VM Agent][1]</span></span>
2. <span data-ttu-id="6fc13-113">Verrà aperto il pannello **L'agente di macchine virtuali non è presente o non risponde**.</span><span class="sxs-lookup"><span data-stu-id="6fc13-113">This opens the blade **VM Agent Is Missing Or Not Responding**.</span></span> <span data-ttu-id="6fc13-114">Questo pannello elenca le VM che richiedono l'agente di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="6fc13-114">This blade lists the VMs that require the VM Agent.</span></span> <span data-ttu-id="6fc13-115">Seguire le istruzioni nel pannello per installare l'agente.</span><span class="sxs-lookup"><span data-stu-id="6fc13-115">Follow the instructions on the blade to install the VM agent.</span></span>
   <span data-ttu-id="6fc13-116">![L'agente di macchine virtuali non è present][2]</span><span class="sxs-lookup"><span data-stu-id="6fc13-116">![VM Agent is missing][2]</span></span>

## <a name="see-also"></a><span data-ttu-id="6fc13-117">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="6fc13-117">See also</span></span>
<span data-ttu-id="6fc13-118">Per altre informazioni sul Centro sicurezza, vedere gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="6fc13-118">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="6fc13-119">[Impostazione dei criteri di sicurezza nel Centro sicurezza di Azure](security-center-policies.md): informazioni su come configurare i criteri di sicurezza per le sottoscrizioni e i gruppi di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="6fc13-119">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="6fc13-120">[Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](security-center-recommendations.md): informazioni sul modo in cui le raccomandazioni semplificano la protezione delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="6fc13-120">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="6fc13-121">[Monitoraggio dell'integrità della sicurezza nel Centro sicurezza di Azure](security-center-monitoring.md): informazioni su come monitorare l'integrità delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="6fc13-121">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="6fc13-122">[Gestione e risposta agli avvisi di sicurezza nel Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md): informazioni su come gestire e rispondere agli avvisi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="6fc13-122">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="6fc13-123">[Monitoraggio delle soluzioni dei partner con il Centro sicurezza di Azure](security-center-partner-solutions.md) : informazioni su come monitorare lo stato integrità delle soluzioni dei partner.</span><span class="sxs-lookup"><span data-stu-id="6fc13-123">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="6fc13-124">[Domande frequenti sul Centro sicurezza di Azure](security-center-faq.md): domande frequenti sull'uso del servizio.</span><span class="sxs-lookup"><span data-stu-id="6fc13-124">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="6fc13-125">[Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/): informazioni e notizie aggiornate sulla sicurezza di Azure.</span><span class="sxs-lookup"><span data-stu-id="6fc13-125">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-vm-agent/enable-vm-agent.png
[2]: ./media/security-center-enable-vm-agent/vm-agent-is-missing.png
