---
title: prerequisiti di hello aaaReview per Hyper-V tooAzure della replica (senza System Center VMM) usando Azure Site Recovery | Documenti Microsoft
description: Vengono descritti i prerequisiti hello per la configurazione di replica, il failover e il ripristino di tooAzure di macchine virtuali Hyper-V locale con Azure Site Recovery
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
ms.openlocfilehash: 3eefc3b7e3982ec6c413c1db7f7784863f9c701d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-for-hyper-v-without-vmm-tooazure-replication"></a><span data-ttu-id="ee89c-103">Passaggio 2: Esaminare i prerequisiti di hello per la replica Hyper-V (senza VMM) tooAzure</span><span class="sxs-lookup"><span data-stu-id="ee89c-103">Step 2: Review hello prerequisites for Hyper-V (without VMM) tooAzure replication</span></span>

<span data-ttu-id="ee89c-104">prerequisiti di Hello sono riepilogati nella tabella di hello.</span><span class="sxs-lookup"><span data-stu-id="ee89c-104">hello prerequisites are summarized in hello table.</span></span>


<span data-ttu-id="ee89c-105">**Prerequisito**</span><span class="sxs-lookup"><span data-stu-id="ee89c-105">**Prerequisite**</span></span> | <span data-ttu-id="ee89c-106">**Dettagli**</span><span class="sxs-lookup"><span data-stu-id="ee89c-106">**Details**</span></span> 
--- | --- 
<span data-ttu-id="ee89c-107">**Azure**</span><span class="sxs-lookup"><span data-stu-id="ee89c-107">**Azure**</span></span> | <span data-ttu-id="ee89c-108">Vedere i [requisiti di Azure](site-recovery-prereq.md#azure-requirements).</span><span class="sxs-lookup"><span data-stu-id="ee89c-108">Learn about [Azure requirements](site-recovery-prereq.md#azure-requirements).</span></span>
<span data-ttu-id="ee89c-109">**Server locali**</span><span class="sxs-lookup"><span data-stu-id="ee89c-109">**On-premises servers**</span></span> | <span data-ttu-id="ee89c-110">[Altre informazioni](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm) sui requisiti per gli host Hyper-V locale di hello.</span><span class="sxs-lookup"><span data-stu-id="ee89c-110">[Learn more](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm) about requirements for hello on-premises Hyper-V hosts.</span></span>
<span data-ttu-id="ee89c-111">**VM Hyper-V locali**</span><span class="sxs-lookup"><span data-stu-id="ee89c-111">**On-premises Hyper-V VMs**</span></span> | <span data-ttu-id="ee89c-112">Macchine virtuali che si desidera tooreplicate deve essere in esecuzione un [sistema operativo supportato](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)e devono essere conformi con [Azure prerequisiti](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="ee89c-112">VMs you want tooreplicate should be running a [supported operating system](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions), and conform with [Azure prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
<span data-ttu-id="ee89c-113">**URL di Azure**</span><span class="sxs-lookup"><span data-stu-id="ee89c-113">**Azure URLs**</span></span> | <span data-ttu-id="ee89c-114">Host Hyper-V è necessario accedere toothese URL:</span><span class="sxs-lookup"><span data-stu-id="ee89c-114">Hyper-V hosts need access toothese URLs:</span></span><br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> <span data-ttu-id="ee89c-115">Se si dispone di regole del firewall basato su indirizzi IP, assicurarsi che consentano la comunicazione tooAzure.</span><span class="sxs-lookup"><span data-stu-id="ee89c-115">If you have IP address-based firewall rules, ensure they allow communication tooAzure.</span></span><br/></br> <span data-ttu-id="ee89c-116">Consenti hello [intervalli IP dei Data Center Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)e hello porta HTTPS (443).</span><span class="sxs-lookup"><span data-stu-id="ee89c-116">Allow hello [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and hello HTTPS (443) port.</span></span><br/></br> <span data-ttu-id="ee89c-117">Consenti gli intervalli di indirizzi IP per hello area della sottoscrizione di Azure e per Stati Uniti occidentali (utilizzato per il controllo di accesso e gestione delle identità).</span><span class="sxs-lookup"><span data-stu-id="ee89c-117">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>



## <a name="next-steps"></a><span data-ttu-id="ee89c-118">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ee89c-118">Next steps</span></span>

- <span data-ttu-id="ee89c-119">Se si sta eseguendo una distribuzione completa, andare troppo[passaggio 3: pianificare la capacità](hyper-v-site-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="ee89c-119">If you're doing a full deployment, go too[Step 3: Plan capacity](hyper-v-site-walkthrough-capacity.md)</span></span>
- <span data-ttu-id="ee89c-120">Se si sta eseguendo una distribuzione di test semplice, andare troppo[passaggio 4: pianificare la rete](hyper-v-site-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="ee89c-120">If you're doing a simple test deployment, go too[Step 4: Plan networking](hyper-v-site-walkthrough-network.md).</span></span>
