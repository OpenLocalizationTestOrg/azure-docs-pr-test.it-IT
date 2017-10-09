---
title: "avvisi di integrità aaaResolve endpoint protection in Centro sicurezza di Azure | Documenti Microsoft"
description: "Questo documento viene illustrato come tooimplement hello raccomandazione Centro sicurezza di Azure * * risolvere Endpoint Protection integrità avvisi * *."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 4050f453-98fc-4314-8438-d476469757fb
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/01/2016
ms.author: terrylan
ms.openlocfilehash: 9631d15aa1dfa9003d56332363ae7911061ed0b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-endpoint-protection-health-alerts-in-azure-security-center"></a><span data-ttu-id="f6628-103">Risolvere gli avvisi sull'integrità della protezione degli endpoint nel Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="f6628-103">Resolve endpoint protection health alerts in Azure Security Center</span></span>
<span data-ttu-id="f6628-104">Il Centro sicurezza di Azure consiglia di risolvere gli avvisi sull'integrità della protezione degli endpoint rilevati.</span><span class="sxs-lookup"><span data-stu-id="f6628-104">Azure Security Center will recommend that you resolve detected endpoint protection health alerts.</span></span>  <span data-ttu-id="f6628-105">Centro sicurezza PC consente toosee quali macchine virtuali (VM) sono errori di endpoint protection e il numero di errori.</span><span class="sxs-lookup"><span data-stu-id="f6628-105">Security Center enables you toosee which virtual machines (VMs) have endpoint protection failures and how many failures.</span></span>

> [!NOTE]
> <span data-ttu-id="f6628-106">Questo documento introduce servizio hello utilizzando un esempio di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="f6628-106">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="f6628-107">Questa non è una guida dettagliata.</span><span class="sxs-lookup"><span data-stu-id="f6628-107">This is not a step-by-step guide.</span></span>
> 
> 

## <a name="implement-hello-recommendation"></a><span data-ttu-id="f6628-108">Implementare la raccomandazione hello</span><span class="sxs-lookup"><span data-stu-id="f6628-108">Implement hello recommendation</span></span>
1. <span data-ttu-id="f6628-109">In hello **pannello indicazioni**selezionare **gli avvisi di integrità di Endpoint Protection risolvere**.</span><span class="sxs-lookup"><span data-stu-id="f6628-109">In hello **Recommendations blade**, select **Resolve Endpoint Protection health alerts**.</span></span>
   <span data-ttu-id="f6628-110">![Risolvere gli avvisi sull'integrità della protezione degli endpoint][1]</span><span class="sxs-lookup"><span data-stu-id="f6628-110">![Resolve endpoint protection health alerts][1]</span></span>
2. <span data-ttu-id="f6628-111">Verrà aperto il pannello hello **errore di Endpoint Protection** in cui sono elencate le macchine virtuali con gli errori e il numero di hello di errori per ogni macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f6628-111">This opens hello blade **Endpoint Protection failure** which lists VMs with failures and hello number of failures for each VM.</span></span> <span data-ttu-id="f6628-112">Selezionare una macchina virtuale dall'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="f6628-112">Select a VM from hello list.</span></span>
   <span data-ttu-id="f6628-113">![Endpoint protection failure][2]</span><span class="sxs-lookup"><span data-stu-id="f6628-113">![Endpoint protection failure][2]</span></span>
3. <span data-ttu-id="f6628-114">Oggetto **elenco errori** pannello apre per hello selezionato VM, che visualizza un elenco di errori.</span><span class="sxs-lookup"><span data-stu-id="f6628-114">A **Failures List** blade opens for hello selected VM, displaying a list of failures.</span></span> <span data-ttu-id="f6628-115">Selezionare un errore hello elenco toolearn altre.</span><span class="sxs-lookup"><span data-stu-id="f6628-115">Select a failure from hello list toolearn more.</span></span> <span data-ttu-id="f6628-116">Verrà aperto un pannello con informazioni sull'errore hello selezionato.</span><span class="sxs-lookup"><span data-stu-id="f6628-116">This opens a blade with information about hello selected failure.</span></span>
   <span data-ttu-id="f6628-117">![Elenco degli errori][3]
   ![Evento di errore][4]</span><span class="sxs-lookup"><span data-stu-id="f6628-117">![Failures list][3]
![Failure event][4]</span></span>

## <a name="see-also"></a><span data-ttu-id="f6628-118">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f6628-118">See also</span></span>
<span data-ttu-id="f6628-119">toolearn ulteriori informazioni su Centro di sicurezza, vedere l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="f6628-119">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="f6628-120">[L'impostazione di criteri di sicurezza nel Centro protezione Azure](security-center-policies.md)-informazioni su come tooconfigure i criteri di sicurezza per le sottoscrizioni di Azure e i gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="f6628-120">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="f6628-121">[Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](security-center-recommendations.md): informazioni sul modo in cui le raccomandazioni semplificano la protezione delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="f6628-121">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="f6628-122">[Il monitoraggio dello stato di sicurezza nel Centro protezione Azure](security-center-monitoring.md)-informazioni su come toomonitor hello integrità delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="f6628-122">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="f6628-123">[La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md)-informazioni su come avvisi toosecurity toomanage e rispondere.</span><span class="sxs-lookup"><span data-stu-id="f6628-123">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="f6628-124">[Monitoraggio di soluzioni dei partner con Centro sicurezza di Azure](security-center-partner-solutions.md) -informazioni su come toomonitor hello lo stato di integrità delle soluzioni di partner.</span><span class="sxs-lookup"><span data-stu-id="f6628-124">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="f6628-125">[Domande frequenti su Centro sicurezza di Azure](security-center-faq.md)-domande frequenti sull'utilizzo di hello servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="f6628-125">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="f6628-126">[Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/)-ottenere informazioni e notizie sicurezza di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="f6628-126">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-resolve-endpoint-protection/resolve-endpoint-protection.png
[2]: ./media/security-center-resolve-endpoint-protection/endpoint-protection-failure.png
[3]: ./media/security-center-resolve-endpoint-protection/failure-list.png
[4]: ./media/security-center-resolve-endpoint-protection/failure-event.png
