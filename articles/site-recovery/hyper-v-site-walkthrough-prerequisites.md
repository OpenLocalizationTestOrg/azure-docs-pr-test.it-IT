---
title: Esaminare i prerequisiti per la replica Hyper-V in Azure (senza System Center VMM) usando Azure Site Recovery | Microsoft Docs
description: Vengono descritti i prerequisiti per la configurazione di replica, failover e ripristino di VM Hyper-V locali in Azure con Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 7ef3fb46-52f5-4c8a-b1a1-658c2305762a
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: cbb5d3598ef91512991d7d1e9f854eb12980752b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="step-2-review-the-prerequisites-for-hyper-v-without-vmm-to-azure-replication"></a><span data-ttu-id="68b2f-103">Passaggio 2: Esaminare i prerequisiti per la replica Hyper-V (senza VMM) in Azure</span><span class="sxs-lookup"><span data-stu-id="68b2f-103">Step 2: Review the prerequisites for Hyper-V (without VMM) to Azure replication</span></span>

<span data-ttu-id="68b2f-104">I prerequisiti sono riepilogati nella tabella.</span><span class="sxs-lookup"><span data-stu-id="68b2f-104">The prerequisites are summarized in the table.</span></span>


<span data-ttu-id="68b2f-105">**Prerequisito**</span><span class="sxs-lookup"><span data-stu-id="68b2f-105">**Prerequisite**</span></span> | <span data-ttu-id="68b2f-106">**Dettagli**</span><span class="sxs-lookup"><span data-stu-id="68b2f-106">**Details**</span></span> 
--- | --- 
<span data-ttu-id="68b2f-107">**Azure**</span><span class="sxs-lookup"><span data-stu-id="68b2f-107">**Azure**</span></span> | <span data-ttu-id="68b2f-108">Vedere i [requisiti di Azure](site-recovery-prereq.md#azure-requirements).</span><span class="sxs-lookup"><span data-stu-id="68b2f-108">Learn about [Azure requirements](site-recovery-prereq.md#azure-requirements).</span></span>
<span data-ttu-id="68b2f-109">**Server locali**</span><span class="sxs-lookup"><span data-stu-id="68b2f-109">**On-premises servers**</span></span> | <span data-ttu-id="68b2f-110">Leggere altre informazioni sui requisiti per gli host Hyper-V locali [qui](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm).</span><span class="sxs-lookup"><span data-stu-id="68b2f-110">[Learn more](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm) about requirements for the on-premises Hyper-V hosts.</span></span>
<span data-ttu-id="68b2f-111">**VM Hyper-V locali**</span><span class="sxs-lookup"><span data-stu-id="68b2f-111">**On-premises Hyper-V VMs**</span></span> | <span data-ttu-id="68b2f-112">Le VM da replicare devono eseguire un [sistema operativo supportato](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions) ed essere conformi ai [prerequisiti di Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="68b2f-112">VMs you want to replicate should be running a [supported operating system](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions), and conform with [Azure prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
<span data-ttu-id="68b2f-113">**URL di Azure**</span><span class="sxs-lookup"><span data-stu-id="68b2f-113">**Azure URLs**</span></span> | <span data-ttu-id="68b2f-114">Gli host Hyper-V devono accedere agli URL seguenti:</span><span class="sxs-lookup"><span data-stu-id="68b2f-114">Hyper-V hosts need access to these URLs:</span></span><br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> <span data-ttu-id="68b2f-115">Se sono presenti regole del firewall basate sull'indirizzo IP, verificare che consentano la comunicazione con Azure.</span><span class="sxs-lookup"><span data-stu-id="68b2f-115">If you have IP address-based firewall rules, ensure they allow communication to Azure.</span></span><br/></br> <span data-ttu-id="68b2f-116">Consentire gli [intervalli IP del data center di Azure ](https://www.microsoft.com/download/confirmation.aspx?id=41653) e la porta HTTPS (443).</span><span class="sxs-lookup"><span data-stu-id="68b2f-116">Allow the [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and the HTTPS (443) port.</span></span><br/></br> <span data-ttu-id="68b2f-117">Consentire gli intervalli di indirizzi IP per l'area di Azure della sottoscrizione e per gli Stati Uniti occidentali (usati per il controllo di accesso e la gestione delle identità).</span><span class="sxs-lookup"><span data-stu-id="68b2f-117">Allow IP address ranges for the Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>



## <a name="next-steps"></a><span data-ttu-id="68b2f-118">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="68b2f-118">Next steps</span></span>

- <span data-ttu-id="68b2f-119">Se si sta eseguendo una distribuzione completa, andare a [Passaggio 3: Pianificare la capacità](hyper-v-site-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="68b2f-119">If you're doing a full deployment, go to [Step 3: Plan capacity](hyper-v-site-walkthrough-capacity.md)</span></span>
- <span data-ttu-id="68b2f-120">Se si sta eseguendo una distribuzione di test semplice, andare a [Passaggio 4: Pianificare la rete](hyper-v-site-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="68b2f-120">If you're doing a simple test deployment, go to [Step 4: Plan networking](hyper-v-site-walkthrough-network.md).</span></span>
