---
title: visualizzazione del gruppo toosecurity aaaIntroduction in Watcher di rete di Azure | Documenti Microsoft
description: "Questa pagina viene fornita una panoramica di hello funzionalità di visualizzazione sicurezza Watcher di rete"
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
ms.openlocfilehash: c2f6dbbffd0aedbb9db4b69d1758f2e66dd7abb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toonetwork-security-group-view-in-azure-network-watcher"></a><span data-ttu-id="1aa44-103">Visualizzazione del gruppo protezione toonetwork introduzione in Watcher di rete di Azure</span><span class="sxs-lookup"><span data-stu-id="1aa44-103">Introduction toonetwork security group view in Azure Network Watcher</span></span>

<span data-ttu-id="1aa44-104">I gruppi di sicurezza di rete sono associati a un livello di subnet o a un livello di scheda di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="1aa44-104">Network Security groups are associated at a subnet level or at a NIC level.</span></span> <span data-ttu-id="1aa44-105">Quando associato a un livello di subnet, si applica le istanze VM hello tooall nella subnet hello.</span><span class="sxs-lookup"><span data-stu-id="1aa44-105">When associated at a subnet level, it applies tooall hello VM instances in hello subnet.</span></span> <span data-ttu-id="1aa44-106">Visualizzazione del gruppo di sicurezza di rete restituisce tutti i NSGs hello configurata e le regole che sono associate a un livello di interfaccia di rete e subnet per una macchina virtuale per fornire informazioni sulle configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="1aa44-106">Network Security Group view returns all hello configured NSGs and rules that are associated at a NIC and subnet level for a virtual machine providing insight into hello configuration.</span></span> <span data-ttu-id="1aa44-107">Inoltre, le regole di sicurezza efficace hello vengono restituite per ognuna delle schede NIC hello in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1aa44-107">In addition, hello effective security rules are returned for each of hello NICs in a VM.</span></span> <span data-ttu-id="1aa44-108">Usando la visualizzazione dei gruppi di sicurezza di rete, è possibile valutare le vulnerabilità di rete di una VM, ad esempio le porte aperte.</span><span class="sxs-lookup"><span data-stu-id="1aa44-108">Using Network Security Group view, you can assess a VM for network vulnerabilities such as open ports.</span></span> <span data-ttu-id="1aa44-109">È anche possibile verificare se il gruppo di sicurezza di rete funzioni come previsto in base a un [confronto tra hello configurato e regole di sicurezza efficace hello](network-watcher-nsg-auditing-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="1aa44-109">You can also validate if your Network Security Group is working as expected based on a [comparison between hello configured and hello effective security rules](network-watcher-nsg-auditing-powershell.md).</span></span>

<span data-ttu-id="1aa44-110">Un caso d'uso più esteso include la conformità alla sicurezza e il controllo della sicurezza.</span><span class="sxs-lookup"><span data-stu-id="1aa44-110">A more extended use case is in security compliance and auditing.</span></span> <span data-ttu-id="1aa44-111">È possibile definire un set prescrittivo di regole di sicurezza come modello per la governance della sicurezza nell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="1aa44-111">You can define a prescriptive set of security rules as a model for security governance in your organization.</span></span> <span data-ttu-id="1aa44-112">Un controllo di conformità periodico può essere implementato in un modo programmatico confrontando le regole di normative hello con regole efficaci hello per ognuna delle macchine virtuali di hello nella rete.</span><span class="sxs-lookup"><span data-stu-id="1aa44-112">A periodic compliance audit can be implemented in a programmatic way by comparing hello prescriptive rules with hello effective rules for each of hello VMs in your network.</span></span>

<span data-ttu-id="1aa44-113">In hello regole portale siano divisi da effettivo, Subnet, l'interfaccia di rete e predefiniti.</span><span class="sxs-lookup"><span data-stu-id="1aa44-113">In hello portal rules are divided by Effective, Subnet, Network Interface, and Default.</span></span> <span data-ttu-id="1aa44-114">Ciò fornisce una visualizzazione semplice in macchina virtuale di hello regole applicate tooa.</span><span class="sxs-lookup"><span data-stu-id="1aa44-114">This provides a simple view into hello rules applied tooa virtual machine.</span></span> <span data-ttu-id="1aa44-115">Un pulsante di download viene fornito tooeasily scaricare tutte le regole di sicurezza hello indipendentemente dalla scheda hello in un file CSV.</span><span class="sxs-lookup"><span data-stu-id="1aa44-115">A download button is provided tooeasily download all hello security rules no matter hello tab into a CSV file.</span></span>

![Visualizzazione di un gruppo di sicurezza][1]

<span data-ttu-id="1aa44-117">È possibile selezionare le regole e i prefissi di gruppo di sicurezza di rete e di origine e di destinazione hello tooshow apre un nuovo pannello.</span><span class="sxs-lookup"><span data-stu-id="1aa44-117">Rules can be selected and a new blade opens up tooshow hello Network Security Group and source and destination prefixes.</span></span> <span data-ttu-id="1aa44-118">Questo pannello è possibile passare direttamente toohello risorsa del gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="1aa44-118">From this blade you can navigate directly toohello Network Security Group resource.</span></span>

![Drill-down][2]

### <a name="next-steps"></a><span data-ttu-id="1aa44-120">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1aa44-120">Next steps</span></span>

<span data-ttu-id="1aa44-121">Informazioni su come tooaudit la sicurezza della rete gruppo impostazioni visitando [delle impostazioni di controllo gruppo di sicurezza di rete con PowerShell](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="1aa44-121">Learn how tooaudit your Network Security Group settings by visiting [Audit Network Security Group settings with PowerShell](network-watcher-nsg-auditing-powershell.md)</span></span>

[1]: ./media/network-watcher-security-group-view-overview/securitygroupview.png
[2]: ./media/network-watcher-security-group-view-overview/figure1.png









