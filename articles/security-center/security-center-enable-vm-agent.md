---
title: aaaEnable agente della macchina virtuale in Centro sicurezza di Azure | Documenti Microsoft
description: Questo documento viene illustrato come tooimplement hello raccomandazione Centro sicurezza di Azure * * abilitare VM agente * *.
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
ms.openlocfilehash: 9bd71e638b020780537da25fd4cf7baf34d3e11a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-vm-agent-in-azure-security-center"></a><span data-ttu-id="453d4-103">Abilita l'agente di macchine virtuali nel Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="453d4-103">Enable VM Agent in Azure Security Center</span></span>
<span data-ttu-id="453d4-104">Hello agente della macchina virtuale deve essere installato nelle macchine virtuali (VM) in ordine troppo[Abilita raccolta dati](security-center-enable-data-collection.md).</span><span class="sxs-lookup"><span data-stu-id="453d4-104">hello VM Agent must be installed on virtual machines (VMs) in order too[enable data collection](security-center-enable-data-collection.md).</span></span>  <span data-ttu-id="453d4-105">Abilita il Centro sicurezza di Azure è toosee che richiedono che le macchine virtuali hello agente VM e consiglia di abilitare hello agente VM su tali macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="453d4-105">Azure Security Center enables you toosee which VMs require hello VM Agent and will recommend that you enable hello VM Agent on those VMs.</span></span>

<span data-ttu-id="453d4-106">Hello agente VM viene installato per impostazione predefinita per le macchine virtuali distribuite da hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="453d4-106">hello VM Agent is installed by default for VMs that are deployed from hello Azure Marketplace.</span></span> <span data-ttu-id="453d4-107">articolo Hello [agente VM ed estensioni-parte 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) vengono fornite informazioni su come tooinstall hello agente della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="453d4-107">hello article [VM Agent and Extensions – Part 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) provides information on how tooinstall hello VM Agent.</span></span>

> [!NOTE]
> <span data-ttu-id="453d4-108">Questo documento introduce servizio hello utilizzando un esempio di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="453d4-108">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="453d4-109">Questa non è una guida dettagliata.</span><span class="sxs-lookup"><span data-stu-id="453d4-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="453d4-110">Implementare la raccomandazione hello</span><span class="sxs-lookup"><span data-stu-id="453d4-110">Implement hello recommendation</span></span>
1. <span data-ttu-id="453d4-111">In hello **pannello indicazioni**selezionare **abilitare agente VM**.</span><span class="sxs-lookup"><span data-stu-id="453d4-111">In hello **Recommendations blade**, select **Enable VM Agent**.</span></span>
   <span data-ttu-id="453d4-112">![Abilita l'agente di macchine virtuali][1]</span><span class="sxs-lookup"><span data-stu-id="453d4-112">![Enable VM Agent][1]</span></span>
2. <span data-ttu-id="453d4-113">Verrà aperto il pannello hello **VM agente mancante o non risponde**.</span><span class="sxs-lookup"><span data-stu-id="453d4-113">This opens hello blade **VM Agent Is Missing Or Not Responding**.</span></span> <span data-ttu-id="453d4-114">Questo pannello sono elencate le macchine virtuali hello che richiedono hello agente della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="453d4-114">This blade lists hello VMs that require hello VM Agent.</span></span> <span data-ttu-id="453d4-115">Istruzioni hello sull'agente VM di hello pannello tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="453d4-115">Follow hello instructions on hello blade tooinstall hello VM agent.</span></span>
   <span data-ttu-id="453d4-116">![L'agente di macchine virtuali non è present][2]</span><span class="sxs-lookup"><span data-stu-id="453d4-116">![VM Agent is missing][2]</span></span>

## <a name="see-also"></a><span data-ttu-id="453d4-117">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="453d4-117">See also</span></span>
<span data-ttu-id="453d4-118">toolearn ulteriori informazioni su Centro di sicurezza, vedere l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="453d4-118">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="453d4-119">[L'impostazione di criteri di sicurezza nel Centro protezione Azure](security-center-policies.md)-informazioni su come tooconfigure i criteri di sicurezza per le sottoscrizioni di Azure e i gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="453d4-119">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="453d4-120">[Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](security-center-recommendations.md): informazioni sul modo in cui le raccomandazioni semplificano la protezione delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="453d4-120">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="453d4-121">[Il monitoraggio dello stato di sicurezza nel Centro protezione Azure](security-center-monitoring.md)-informazioni su come toomonitor hello integrità delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="453d4-121">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="453d4-122">[La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md)-informazioni su come avvisi toosecurity toomanage e rispondere.</span><span class="sxs-lookup"><span data-stu-id="453d4-122">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="453d4-123">[Monitoraggio di soluzioni dei partner con Centro sicurezza di Azure](security-center-partner-solutions.md) -informazioni su come toomonitor hello lo stato di integrità delle soluzioni di partner.</span><span class="sxs-lookup"><span data-stu-id="453d4-123">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="453d4-124">[Domande frequenti su Centro sicurezza di Azure](security-center-faq.md)-domande frequenti sull'utilizzo di hello servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="453d4-124">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="453d4-125">[Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/)-ottenere informazioni e notizie sicurezza di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="453d4-125">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-vm-agent/enable-vm-agent.png
[2]: ./media/security-center-enable-vm-agent/vm-agent-is-missing.png
