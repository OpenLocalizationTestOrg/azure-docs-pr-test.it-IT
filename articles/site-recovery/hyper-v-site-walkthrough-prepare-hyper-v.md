---
title: aaaPrepare Hyper-V ospita (senza System Center VMM) per la replica tooAzure | Documenti Microsoft
description: Viene descritto come tooprepare Hyper-V ospita per replica tooAzure usando Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 0f204e24-8d78-4076-95c5-8137d1be9c01
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 714b229d5efbd66a9844bd09e36ac3f69919a6bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-hyper-v-hosts-for-replication-tooazure"></a><span data-ttu-id="45a81-103">Passaggio 6: Preparare l'host Hyper-V per la replica tooAzure</span><span class="sxs-lookup"><span data-stu-id="45a81-103">Step 6: Prepare Hyper-V hosts for replication tooAzure</span></span>

<span data-ttu-id="45a81-104">Hello seguire le istruzioni riportate in questo articolo di tooprepare locale toointeract gli host Hyper-V con Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="45a81-104">Use hello instructions in this article tooprepare on-premises Hyper-V hosts toointeract with Azure Site Recovery.</span></span>

<span data-ttu-id="45a81-105">Dopo aver letto questo articolo, inviare eventuali commenti nella parte inferiore di hello o porre domande tecniche su hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="45a81-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="prepare-hosts"></a><span data-ttu-id="45a81-106">Preparare gli host</span><span class="sxs-lookup"><span data-stu-id="45a81-106">Prepare hosts</span></span>

- <span data-ttu-id="45a81-107">Verificare che gli host Hyper-V hello soddisfino hello [prerequisiti](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm).</span><span class="sxs-lookup"><span data-stu-id="45a81-107">Make sure that hello Hyper-V hosts meet hello [prerequisites](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm).</span></span>
- <span data-ttu-id="45a81-108">Assicurarsi che gli host hello possono accedere agli URL di hello necessarie:</span><span class="sxs-lookup"><span data-stu-id="45a81-108">Make sure that hello hosts can access hello required URLs:</span></span>

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- <span data-ttu-id="45a81-109">Se si dispone di regole del firewall basato su indirizzi IP, assicurarsi che consentano la comunicazione tooAzure.</span><span class="sxs-lookup"><span data-stu-id="45a81-109">If you have IP address-based firewall rules, ensure they allow communication tooAzure.</span></span>
- <span data-ttu-id="45a81-110">Consenti hello [intervalli IP dei Data Center Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)e hello porta HTTPS (443).</span><span class="sxs-lookup"><span data-stu-id="45a81-110">Allow hello [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and hello HTTPS (443) port.</span></span>
- <span data-ttu-id="45a81-111">Consenti gli intervalli di indirizzi IP per hello area della sottoscrizione di Azure e per Stati Uniti occidentali (utilizzato per il controllo di accesso e gestione delle identità).</span><span class="sxs-lookup"><span data-stu-id="45a81-111">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

<span data-ttu-id="45a81-112">Durante la distribuzione di Site Recovery, aggiungere gli host Hyper-V che contengono macchine virtuali che si desidera che il sito di Hyper-V tooa tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="45a81-112">During Site Recovery deployment, you add Hyper-V hosts that contain VMs you want tooreplicate tooa Hyper-V site.</span></span> <span data-ttu-id="45a81-113">Provider di Site Recovery Hello e dell'agente di servizi di ripristino vengono installati in ogni host.</span><span class="sxs-lookup"><span data-stu-id="45a81-113">hello Site Recovery Provider, and Recovery Services agent are installed on each host.</span></span> <span data-ttu-id="45a81-114">sito Hello Hyper-V è registrato nell'insieme di credenziali di servizi di ripristino hello.</span><span class="sxs-lookup"><span data-stu-id="45a81-114">hello Hyper-V site is registered in hello Recovery Services vault.</span></span>

## <a name="next-steps"></a><span data-ttu-id="45a81-115">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="45a81-115">Next steps</span></span>

<span data-ttu-id="45a81-116">Andare troppo[passaggio 7: creare un insieme di credenziali](hyper-v-site-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="45a81-116">Go too[Step 7: Create a vault](hyper-v-site-walkthrough-create-vault.md)</span></span>

