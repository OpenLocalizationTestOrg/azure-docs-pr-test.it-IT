---
title: Aggiornare la versione del sistema operativo nel Centro sicurezza di Azure | Documentazione Microsoft
description: Questo documento illustra come implementare la raccomandazione **Aggiorna la versione del sistema operativo** del Centro sicurezza di Azure.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: aa372492-ecdb-4368-8fdd-d8ed31e216ee
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/01/2016
ms.author: terrylan
ms.openlocfilehash: ce0d178914907750e5da59f223a4b1e04b9bb6fb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="update-os-version-in-azure-security-center"></a><span data-ttu-id="b07db-103">Aggiornare la versione del sistema operativo nel Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="b07db-103">Update OS version in Azure Security Center</span></span>
<span data-ttu-id="b07db-104">Per le macchine virtuali nei servizi cloud il Centro sicurezza di Azure consiglierà l'aggiornamento del sistema operativo se è disponibile una versione più recente.</span><span class="sxs-lookup"><span data-stu-id="b07db-104">For virtual machines (VMs) in cloud services, Azure Security Center will recommend that the operating system (OS) be updated if there is a more recent version available.</span></span>  <span data-ttu-id="b07db-105">Vengono monitorati solo i ruoli Web e di lavoro dei servizi cloud in esecuzione negli slot di produzione.</span><span class="sxs-lookup"><span data-stu-id="b07db-105">Only cloud services web and worker roles running in production slots are monitored.</span></span>

> [!NOTE]
> <span data-ttu-id="b07db-106">Il documento introduce il servizio usando una distribuzione di esempio.</span><span class="sxs-lookup"><span data-stu-id="b07db-106">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="b07db-107">Questa non è una guida dettagliata.</span><span class="sxs-lookup"><span data-stu-id="b07db-107">This is not a step-by-step guide.</span></span>
> 
> 

## <a name="implement-the-recommendation"></a><span data-ttu-id="b07db-108">Implementare la raccomandazione</span><span class="sxs-lookup"><span data-stu-id="b07db-108">Implement the recommendation</span></span>
1. <span data-ttu-id="b07db-109">Nel pannello **Raccomandazioni** selezionare **Aggiorna la versione del sistema operativo**.</span><span class="sxs-lookup"><span data-stu-id="b07db-109">In the **Recommendations** blade, select **Update OS version**.</span></span>
   <span data-ttu-id="b07db-110">![Aggiornare la versione sistema operativo][1]</span><span class="sxs-lookup"><span data-stu-id="b07db-110">![Update OS version][1]</span></span>
2. <span data-ttu-id="b07db-111">Viene visualizzato il pannello **Aggiorna la versione del sistema operativo**.</span><span class="sxs-lookup"><span data-stu-id="b07db-111">This opens the blade **Update OS version**.</span></span> <span data-ttu-id="b07db-112">Seguire i passaggi in questo pannello per aggiornare la versione del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="b07db-112">Follow the steps in this blade to update the OS version.</span></span>

## <a name="see-also"></a><span data-ttu-id="b07db-113">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="b07db-113">See also</span></span>
<span data-ttu-id="b07db-114">Questo documento illustra come implementare la raccomandazione "Aggiorna la versione del sistema operativo" del Centro sicurezza.</span><span class="sxs-lookup"><span data-stu-id="b07db-114">This article showed you how to implement the Security Center recommendation "Update OS version."</span></span> <span data-ttu-id="b07db-115">Per altre informazioni sui servizi cloud e sull'aggiornamento della versione del sistema operativo per un servizio cloud, vedere:</span><span class="sxs-lookup"><span data-stu-id="b07db-115">To learn more about cloud services and updating the OS version for a cloud service, see:</span></span>

* [<span data-ttu-id="b07db-116">Perché scegliere Servizi cloud</span><span class="sxs-lookup"><span data-stu-id="b07db-116">Cloud Services overview</span></span>](../cloud-services/cloud-services-choose-me.md)
* [<span data-ttu-id="b07db-117">Come aggiornare un servizio cloud</span><span class="sxs-lookup"><span data-stu-id="b07db-117">How to update a cloud service</span></span>](../cloud-services/cloud-services-update-azure-service.md)
* [<span data-ttu-id="b07db-118">Come configurare i servizi cloud</span><span class="sxs-lookup"><span data-stu-id="b07db-118">How to Configure Cloud Services</span></span>](../cloud-services/cloud-services-how-to-configure-portal.md)

<span data-ttu-id="b07db-119">Per altre informazioni sul Centro sicurezza, vedere gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="b07db-119">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="b07db-120">[Impostazione dei criteri di sicurezza nel Centro sicurezza di Azure](security-center-policies.md) : informazioni su come configurare i criteri di sicurezza per le sottoscrizioni e i gruppi di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="b07db-120">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="b07db-121">[Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](security-center-recommendations.md) : informazioni sul modo in cui le raccomandazioni semplificano la protezione delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="b07db-121">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="b07db-122">[Monitoraggio dell'integrità della sicurezza nel Centro sicurezza di Azure](security-center-monitoring.md) : informazioni su come monitorare l'integrità delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="b07db-122">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="b07db-123">[Gestione e risposta agli avvisi di sicurezza nel Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) : informazioni su come gestire e rispondere agli avvisi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="b07db-123">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="b07db-124">[Monitoraggio delle soluzioni dei partner con il Centro sicurezza di Azure](security-center-partner-solutions.md) : informazioni su come monitorare lo stato integrità delle soluzioni dei partner.</span><span class="sxs-lookup"><span data-stu-id="b07db-124">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="b07db-125">[Domande frequenti sul Centro sicurezza di Azure](security-center-faq.md) : domande frequenti sull'uso del servizio.</span><span class="sxs-lookup"><span data-stu-id="b07db-125">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="b07db-126">[Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/) : informazioni e notizie aggiornate sulla sicurezza di Azure.</span><span class="sxs-lookup"><span data-stu-id="b07db-126">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-update-os-version/update-os-version.png
