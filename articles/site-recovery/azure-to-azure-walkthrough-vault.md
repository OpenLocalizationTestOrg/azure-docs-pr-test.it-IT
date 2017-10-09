---
title: aaaSet di un insieme di credenziali per la macchina virtuale di Azure repliction tra aree con Azure Site Recovery | Documenti Microsoft
description: "Vengono riepilogati i passaggi di hello tooset di un insieme di credenziali è necessario per la replica tra aree di Azure usando Azure Site Recovery di Azure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: 40472189-3d80-4963-b175-8bddcbc2f61f
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: 9959c59c7ea57114763f13bf060404ddd267ba80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-set-up-a-vault-for-azure-tooazure-replication"></a><span data-ttu-id="c48c3-103">Passaggio 4: Configurare un insieme di credenziali per la replica di Azure tooAzure</span><span class="sxs-lookup"><span data-stu-id="c48c3-103">Step 4: Set up a vault for Azure tooAzure replication</span></span>

<span data-ttu-id="c48c3-104">Dopo aver [pianificazione delle reti](azure-to-azure-walkthrough-network.md), utilizzare questo tooset articolo backup di un insieme di credenziali per Azure le macchine virtuali (VM) replica tooanother area di Azure utilizzando hello [Azure Site Recovery](site-recovery-overview.md) di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c48c3-104">After [planning networks](azure-to-azure-walkthrough-network.md), use this article tooset up a vault, for Azure virtual machines (VMs) replicating tooanother Azure region, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

- <span data-ttu-id="c48c3-105">Dopo aver articolo hello, è necessario impostato un archivio di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="c48c3-105">When you finish hello article, you should have a Recovery Services vault set up.</span></span>
- <span data-ttu-id="c48c3-106">Inviare eventuali commenti nella parte inferiore di hello di questo articolo, o porre domande in hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="c48c3-106">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



>[!NOTE]
>
> <span data-ttu-id="c48c3-107">La replica di macchine virtuali di Azure è attualmente in anteprima.</span><span class="sxs-lookup"><span data-stu-id="c48c3-107">Azure VM replication is currently in preview.</span></span>




## <a name="create-a-vault"></a><span data-ttu-id="c48c3-108">Creare un insieme di credenziali</span><span class="sxs-lookup"><span data-stu-id="c48c3-108">Create a vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> <span data-ttu-id="c48c3-109">Si consiglia di creare credenziali di servizi di ripristino hello in hello percorso in cui tooreplicate le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="c48c3-109">We recommend that you create hello Recovery Services vault in hello location where you want your VMs tooreplicate.</span></span> <span data-ttu-id="c48c3-110">Ad esempio, se il percorso di destinazione è hello central US, creare un archivio di hello in **centrale Usa**.</span><span class="sxs-lookup"><span data-stu-id="c48c3-110">For example, if your target location is hello central US, create hello vault in **Central US**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c48c3-111">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c48c3-111">Next steps</span></span>

<span data-ttu-id="c48c3-112">Andare troppo[passaggio 5: abilitare la replica](azure-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="c48c3-112">Go too[Step 5: Enable replication](azure-to-azure-walkthrough-enable-replication.md)</span></span>
