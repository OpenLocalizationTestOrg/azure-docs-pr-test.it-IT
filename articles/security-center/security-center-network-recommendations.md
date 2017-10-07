---
title: aaaProtecting la rete in Centro sicurezza di Azure | Documenti Microsoft
description: "Questo documento illustra le raccomandazioni presenti nel Centro sicurezza di Azure che facilitano la protezione della rete di Azure e garantiscano la conformità ai criteri di sicurezza."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 96c55a02-afd6-478b-9c1f-039528f3dea0
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/16/2016
ms.author: terrylan
ms.openlocfilehash: 053738da432edf13b40172fb44d2044702dd8211
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-your-network-in-azure-security-center"></a><span data-ttu-id="487d2-103">Protezione della rete nel Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="487d2-103">Protecting your network in Azure Security Center</span></span>
<span data-ttu-id="487d2-104">Centro sicurezza di Azure consente di analizzare lo stato di sicurezza hello delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="487d2-104">Azure Security Center analyzes hello security state of your Azure resources.</span></span> <span data-ttu-id="487d2-105">Quando il Centro sicurezza PC identifica potenziali vulnerabilità di sicurezza, viene creato indicazioni che consentono di eseguire il processo di hello di configurazione dei controlli di hello necessita.</span><span class="sxs-lookup"><span data-stu-id="487d2-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through hello process of configuring hello needed controls.</span></span>  <span data-ttu-id="487d2-106">Consigli si applicano a tipi di risorse tooAzure: macchine virtuali (VM), rete, SQL e le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="487d2-106">Recommendations apply tooAzure resource types: virtual machines (VMs), networking, SQL, and applications.</span></span>

<span data-ttu-id="487d2-107">Questo articolo illustra indicazioni applicabili tooyour rete.</span><span class="sxs-lookup"><span data-stu-id="487d2-107">This article addresses recommendations that apply tooyour network.</span></span>  <span data-ttu-id="487d2-108">Le raccomandazioni per le risorse di rete sono incentrate sui firewall di nuova generazione, sui gruppi di sicurezza di rete, sulla configurazione delle regole di traffico in ingresso e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="487d2-108">Network recommendations center around next generation firewalls, Network Security Groups, configuring inbound traffic rules, and more.</span></span>  <span data-ttu-id="487d2-109">Tabella di hello utilizzare riportata di seguito come un riferimento di toohelp comprendere indicazioni di rete disponibile hello e ciascuna di esse cosa se lo si applica.</span><span class="sxs-lookup"><span data-stu-id="487d2-109">Use hello table below as a reference toohelp you understand hello available network recommendations and what each one does if you apply it.</span></span>

## <a name="available-network-recommendations"></a><span data-ttu-id="487d2-110">Indicazioni disponibili per la rete</span><span class="sxs-lookup"><span data-stu-id="487d2-110">Available network recommendations</span></span>
| <span data-ttu-id="487d2-111">Raccomandazione</span><span class="sxs-lookup"><span data-stu-id="487d2-111">Recommendation</span></span> | <span data-ttu-id="487d2-112">Descrizione</span><span class="sxs-lookup"><span data-stu-id="487d2-112">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="487d2-113">Aggiungi un firewall di nuova generazione</span><span class="sxs-lookup"><span data-stu-id="487d2-113">Add a Next Generation Firewall</span></span>](security-center-add-next-generation-firewall.md) |<span data-ttu-id="487d2-114">Consiglia di aggiungere un Firewall di generazione successiva (NGFW) da un tooincrease partner Microsoft i meccanismi di protezione.</span><span class="sxs-lookup"><span data-stu-id="487d2-114">Recommends that you add a Next Generation Firewall (NGFW) from a Microsoft partner tooincrease your security protections.</span></span> |
| [<span data-ttu-id="487d2-115">Indirizza il traffico solo tramite il firewall di nuova generazione</span><span class="sxs-lookup"><span data-stu-id="487d2-115">Route traffic through NGFW only</span></span>](security-center-add-next-generation-firewall.md#route-traffic-through-ngfw-only) |<span data-ttu-id="487d2-116">Consiglia di configurare regole di gruppo () sicurezza di rete che impongono il traffico in entrata tooyour VM tramite il NGFW.</span><span class="sxs-lookup"><span data-stu-id="487d2-116">Recommends that you configure network security group (NSG) rules that force inbound traffic tooyour VM through your NGFW.</span></span> |
| [<span data-ttu-id="487d2-117">Abilita i gruppi di sicurezza di rete sulle subnet o sulle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="487d2-117">Enable Network Security Groups on subnets or virtual machines</span></span>](security-center-enable-network-security-groups.md) |<span data-ttu-id="487d2-118">Consiglia di attivare i gruppo di sicurezza di rete sulle subnet o sulle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="487d2-118">Recommends that you enable NSGs on subnets or VMs.</span></span> |
| [<span data-ttu-id="487d2-119">Limita l'accesso tramite un endpoint con connessione Internet</span><span class="sxs-lookup"><span data-stu-id="487d2-119">Restrict access through Internet facing endpoint</span></span>](security-center-restrict-access-through-internet-facing-endpoints.md) |<span data-ttu-id="487d2-120">Consiglia di configurare le regole del traffico in ingresso per i gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="487d2-120">Recommends that you configure inbound traffic rules for NSGs.</span></span> |

## <a name="see-also"></a><span data-ttu-id="487d2-121">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="487d2-121">See also</span></span>
<span data-ttu-id="487d2-122">toolearn ulteriori informazioni sui suggerimenti che si applicano tooother tipi di risorse di Azure, vedere l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="487d2-122">toolearn more about recommendations that apply tooother Azure resource types, see hello following:</span></span>

* [<span data-ttu-id="487d2-123">Protezione delle macchine virtuali nel Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="487d2-123">Protecting your virtual machines in Azure Security Center</span></span>](security-center-virtual-machine-recommendations.md)
* [<span data-ttu-id="487d2-124">Protecting your applications in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="487d2-124">Protecting your applications in Azure Security Center</span></span>](security-center-application-recommendations.md)
* [<span data-ttu-id="487d2-125">Protezione del servizio SQL di Azure nel Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="487d2-125">Protecting your Azure SQL service in Azure Security Center</span></span>](security-center-sql-service-recommendations.md)

<span data-ttu-id="487d2-126">toolearn ulteriori informazioni su Centro di sicurezza, vedere l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="487d2-126">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="487d2-127">[L'impostazione di criteri di sicurezza nel Centro protezione Azure](security-center-policies.md) -informazioni su come tooconfigure i criteri di sicurezza per le sottoscrizioni di Azure e i gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="487d2-127">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="487d2-128">[La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) -informazioni su come avvisi toosecurity toomanage e rispondere.</span><span class="sxs-lookup"><span data-stu-id="487d2-128">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="487d2-129">[Domande frequenti su Centro sicurezza di Azure](security-center-faq.md) -domande frequenti sull'utilizzo di hello servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="487d2-129">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
