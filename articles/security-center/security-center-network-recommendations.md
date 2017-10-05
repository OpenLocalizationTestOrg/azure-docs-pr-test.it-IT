---
title: Protezione della rete nel Centro sicurezza di Azure | Documentazione Microsoft
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
ms.openlocfilehash: 00b715507a7c3a4d784b800e7bf0c700f6ea6ff1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="protecting-your-network-in-azure-security-center"></a><span data-ttu-id="f0bc3-103">Protezione della rete nel Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="f0bc3-103">Protecting your network in Azure Security Center</span></span>
<span data-ttu-id="f0bc3-104">Il Centro sicurezza di Azure analizza lo stato di sicurezza delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="f0bc3-104">Azure Security Center analyzes the security state of your Azure resources.</span></span> <span data-ttu-id="f0bc3-105">Quando il Centro sicurezza identifica potenziali vulnerabilità della sicurezza, crea raccomandazioni utili per definire il processo di configurazione dei controlli necessari.</span><span class="sxs-lookup"><span data-stu-id="f0bc3-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through the process of configuring the needed controls.</span></span>  <span data-ttu-id="f0bc3-106">Le raccomandazioni sono applicabili ai tipi di risorse di Azure, ovvero macchine virtuali, risorse di rete, SQL e applicazioni.</span><span class="sxs-lookup"><span data-stu-id="f0bc3-106">Recommendations apply to Azure resource types: virtual machines (VMs), networking, SQL, and applications.</span></span>

<span data-ttu-id="f0bc3-107">Questo articolo illustra le raccomandazioni applicabili alla rete.</span><span class="sxs-lookup"><span data-stu-id="f0bc3-107">This article addresses recommendations that apply to your network.</span></span>  <span data-ttu-id="f0bc3-108">Le raccomandazioni per le risorse di rete sono incentrate sui firewall di nuova generazione, sui gruppi di sicurezza di rete, sulla configurazione delle regole di traffico in ingresso e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="f0bc3-108">Network recommendations center around next generation firewalls, Network Security Groups, configuring inbound traffic rules, and more.</span></span>  <span data-ttu-id="f0bc3-109">Usare la tabella seguente come riferimento per conoscere le raccomandazioni disponibili per la rete e gli effetti che producono se si decide di metterle in pratica.</span><span class="sxs-lookup"><span data-stu-id="f0bc3-109">Use the table below as a reference to help you understand the available network recommendations and what each one does if you apply it.</span></span>

## <a name="available-network-recommendations"></a><span data-ttu-id="f0bc3-110">Indicazioni disponibili per la rete</span><span class="sxs-lookup"><span data-stu-id="f0bc3-110">Available network recommendations</span></span>
| <span data-ttu-id="f0bc3-111">Raccomandazione</span><span class="sxs-lookup"><span data-stu-id="f0bc3-111">Recommendation</span></span> | <span data-ttu-id="f0bc3-112">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f0bc3-112">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="f0bc3-113">Aggiungi un firewall di nuova generazione</span><span class="sxs-lookup"><span data-stu-id="f0bc3-113">Add a Next Generation Firewall</span></span>](security-center-add-next-generation-firewall.md) |<span data-ttu-id="f0bc3-114">Il Centro sicurezza di Azure consiglia di aggiungere un firewall di nuova generazione di un partner Microsoft per aumentare i meccanismi di protezione per la sicurezza.</span><span class="sxs-lookup"><span data-stu-id="f0bc3-114">Recommends that you add a Next Generation Firewall (NGFW) from a Microsoft partner to increase your security protections.</span></span> |
| [<span data-ttu-id="f0bc3-115">Indirizza il traffico solo tramite il firewall di nuova generazione</span><span class="sxs-lookup"><span data-stu-id="f0bc3-115">Route traffic through NGFW only</span></span>](security-center-add-next-generation-firewall.md#route-traffic-through-ngfw-only) |<span data-ttu-id="f0bc3-116">Consiglia di configurare le regole del gruppo di sicurezza di rete che forzano il traffico in ingresso alla VM tramite il firewall di nuova generazione.</span><span class="sxs-lookup"><span data-stu-id="f0bc3-116">Recommends that you configure network security group (NSG) rules that force inbound traffic to your VM through your NGFW.</span></span> |
| [<span data-ttu-id="f0bc3-117">Abilita i gruppi di sicurezza di rete sulle subnet o sulle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="f0bc3-117">Enable Network Security Groups on subnets or virtual machines</span></span>](security-center-enable-network-security-groups.md) |<span data-ttu-id="f0bc3-118">Consiglia di attivare i gruppo di sicurezza di rete sulle subnet o sulle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="f0bc3-118">Recommends that you enable NSGs on subnets or VMs.</span></span> |
| [<span data-ttu-id="f0bc3-119">Limita l'accesso tramite un endpoint con connessione Internet</span><span class="sxs-lookup"><span data-stu-id="f0bc3-119">Restrict access through Internet facing endpoint</span></span>](security-center-restrict-access-through-internet-facing-endpoints.md) |<span data-ttu-id="f0bc3-120">Consiglia di configurare le regole del traffico in ingresso per i gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="f0bc3-120">Recommends that you configure inbound traffic rules for NSGs.</span></span> |

## <a name="see-also"></a><span data-ttu-id="f0bc3-121">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f0bc3-121">See also</span></span>
<span data-ttu-id="f0bc3-122">Per altre informazioni sulle raccomandazioni applicabili ad altri tipi di risorse di Azure, vedere gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="f0bc3-122">To learn more about recommendations that apply to other Azure resource types, see the following:</span></span>

* [<span data-ttu-id="f0bc3-123">Protezione delle macchine virtuali nel Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="f0bc3-123">Protecting your virtual machines in Azure Security Center</span></span>](security-center-virtual-machine-recommendations.md)
* [<span data-ttu-id="f0bc3-124">Protecting your applications in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="f0bc3-124">Protecting your applications in Azure Security Center</span></span>](security-center-application-recommendations.md)
* [<span data-ttu-id="f0bc3-125">Protezione del servizio SQL di Azure nel Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="f0bc3-125">Protecting your Azure SQL service in Azure Security Center</span></span>](security-center-sql-service-recommendations.md)

<span data-ttu-id="f0bc3-126">Per altre informazioni sul Centro sicurezza, vedere gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="f0bc3-126">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="f0bc3-127">[Impostazione dei criteri di sicurezza nel Centro sicurezza di Azure](security-center-policies.md) : informazioni su come configurare i criteri di sicurezza per le sottoscrizioni e i gruppi di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="f0bc3-127">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="f0bc3-128">[Gestione e risposta agli avvisi di sicurezza nel Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) : informazioni su come gestire e rispondere agli avvisi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="f0bc3-128">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="f0bc3-129">[Domande frequenti sul Centro sicurezza di Azure](security-center-faq.md) : domande frequenti sull'uso del servizio.</span><span class="sxs-lookup"><span data-stu-id="f0bc3-129">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
