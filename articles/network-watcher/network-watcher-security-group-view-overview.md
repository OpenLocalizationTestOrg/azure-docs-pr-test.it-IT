---
title: Introduzione alla visualizzazione dei gruppi di sicurezza in Azure Network Watcher | Microsoft Docs
description: "Questa pagina fornisce una panoramica della funzionalità di visualizzazione della sicurezza di Network Watcher"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: ad27ab85-9d84-4759-b2b9-e861ef8ea8d8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: 2c581a2d152a6d3f16de8f249e27a426aa9f844f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-network-security-group-view-in-azure-network-watcher"></a><span data-ttu-id="6cd4f-103">Introduzione alla visualizzazione dei gruppi di sicurezza di rete in Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="6cd4f-103">Introduction to network security group view in Azure Network Watcher</span></span>

<span data-ttu-id="6cd4f-104">I gruppi di sicurezza di rete sono associati a un livello di subnet o a un livello di scheda di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="6cd4f-104">Network Security groups are associated at a subnet level or at a NIC level.</span></span> <span data-ttu-id="6cd4f-105">Se associato a livello di subnet, si applica a tutte le istanze delle VM della subnet.</span><span class="sxs-lookup"><span data-stu-id="6cd4f-105">When associated at a subnet level, it applies to all the VM instances in the subnet.</span></span> <span data-ttu-id="6cd4f-106">La visualizzazione dei gruppi di sicurezza di rete restituisce tutti i gruppi di sicurezza di rete configurati e le regole associate a livello di scheda di interfaccia di rete e di subnet per una macchina virtuale, offrendo così informazioni approfondite sulla configurazione.</span><span class="sxs-lookup"><span data-stu-id="6cd4f-106">Network Security Group view returns all the configured NSGs and rules that are associated at a NIC and subnet level for a virtual machine providing insight into the configuration.</span></span> <span data-ttu-id="6cd4f-107">Vengono anche restituite le regole di sicurezza effettive per ogni scheda di interfaccia di rete in una VM.</span><span class="sxs-lookup"><span data-stu-id="6cd4f-107">In addition, the effective security rules are returned for each of the NICs in a VM.</span></span> <span data-ttu-id="6cd4f-108">Usando la visualizzazione dei gruppi di sicurezza di rete, è possibile valutare le vulnerabilità di rete di una VM, ad esempio le porte aperte.</span><span class="sxs-lookup"><span data-stu-id="6cd4f-108">Using Network Security Group view, you can assess a VM for network vulnerabilities such as open ports.</span></span> <span data-ttu-id="6cd4f-109">È anche possibile verificare se il gruppo di sicurezza di rete funziona come previsto [confrontando le regole di sicurezza configurate e quelle effettive](network-watcher-nsg-auditing-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="6cd4f-109">You can also validate if your Network Security Group is working as expected based on a [comparison between the configured and the effective security rules](network-watcher-nsg-auditing-powershell.md).</span></span>

<span data-ttu-id="6cd4f-110">Un caso d'uso più esteso include la conformità alla sicurezza e il controllo della sicurezza.</span><span class="sxs-lookup"><span data-stu-id="6cd4f-110">A more extended use case is in security compliance and auditing.</span></span> <span data-ttu-id="6cd4f-111">È possibile definire un set prescrittivo di regole di sicurezza come modello per la governance della sicurezza nell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="6cd4f-111">You can define a prescriptive set of security rules as a model for security governance in your organization.</span></span> <span data-ttu-id="6cd4f-112">Un controllo della conformità periodico può essere implementato in modo programmatico confrontando le regole prescrittive con le regole effettive per ogni VM della rete.</span><span class="sxs-lookup"><span data-stu-id="6cd4f-112">A periodic compliance audit can be implemented in a programmatic way by comparing the prescriptive rules with the effective rules for each of the VMs in your network.</span></span>

<span data-ttu-id="6cd4f-113">Nel portale le regolo sono divise in Valide, Subnet, Interfaccia di rete e Predefinite.</span><span class="sxs-lookup"><span data-stu-id="6cd4f-113">In the portal rules are divided by Effective, Subnet, Network Interface, and Default.</span></span> <span data-ttu-id="6cd4f-114">Si ottiene così una semplice visualizzazione delle regole applicate a una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6cd4f-114">This provides a simple view into the rules applied to a virtual machine.</span></span> <span data-ttu-id="6cd4f-115">È disponibile un pulsante per il download per scaricare facilmente tutte le regole di sicurezza indipendentemente dalla scheda in un file CSV.</span><span class="sxs-lookup"><span data-stu-id="6cd4f-115">A download button is provided to easily download all the security rules no matter the tab into a CSV file.</span></span>

![Visualizzazione di un gruppo di sicurezza][1]

<span data-ttu-id="6cd4f-117">Le regole possono essere selezionate e si apre un nuovo pannello che visualizza il gruppo di sicurezza di rete e i prefissi di origine e di destinazione.</span><span class="sxs-lookup"><span data-stu-id="6cd4f-117">Rules can be selected and a new blade opens up to show the Network Security Group and source and destination prefixes.</span></span> <span data-ttu-id="6cd4f-118">Da questo pannello è possibile passare direttamente alla risorsa del gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="6cd4f-118">From this blade you can navigate directly to the Network Security Group resource.</span></span>

![Drill-down][2]

### <a name="next-steps"></a><span data-ttu-id="6cd4f-120">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6cd4f-120">Next steps</span></span>

<span data-ttu-id="6cd4f-121">Per informazioni su come controllare le impostazioni del gruppo di sicurezza di rete, vedere [Audit Network Security Group settings with PowerShell](network-watcher-nsg-auditing-powershell.md) (Controllare le impostazioni di un gruppo di sicurezza di rete con PowerShell)</span><span class="sxs-lookup"><span data-stu-id="6cd4f-121">Learn how to audit your Network Security Group settings by visiting [Audit Network Security Group settings with PowerShell](network-watcher-nsg-auditing-powershell.md)</span></span>

[1]: ./media/network-watcher-security-group-view-overview/securitygroupview.png
[2]: ./media/network-watcher-security-group-view-overview/figure1.png









