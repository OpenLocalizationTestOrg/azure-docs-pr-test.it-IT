---
title: un insieme di credenziali per il sito secondario con tooa di replica Hyper-V con Azure Site Recovery aaaCreate | Documenti Microsoft
description: Viene descritto come un insieme di credenziali per la replica delle macchine virtuali Hyper-V tooa toocreate sito secondario di System Center VMM con Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: ff65dbfb-cb26-410e-ab48-76971625db08
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 96ee09cbf2376a5089b9efa09dc7ab3fb7d472cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-create-a-vault-for-hyper-v-replication-tooa-secondary-site"></a><span data-ttu-id="a545c-103">Passaggio 5: Creare un insieme di credenziali per il sito secondario di Hyper-V replica tooa</span><span class="sxs-lookup"><span data-stu-id="a545c-103">Step 5: Create a vault for Hyper-V replication tooa secondary site</span></span>

<span data-ttu-id="a545c-104">Dopo la preparazione di on-premise [Server System Center Virtual Machine Manager (VMM) e gli host o cluster Hyper-V](vmm-to-vmm-walkthrough-vmm-hyper-v.md) per l'utilizzo del sito secondario di Hyper-V replica tooa [Azure Site Recovery](site-recovery-overview.md), è possibile creare un Archivio di servizi di ripristino e uno scenario di replica hello selezionare.</span><span class="sxs-lookup"><span data-stu-id="a545c-104">After preparing on-premises [System Center Virtual Machine Manager (VMM) servers and Hyper-V hosts/clusters](vmm-to-vmm-walkthrough-vmm-hyper-v.md) for Hyper-V replication tooa secondary site using [Azure Site Recovery](site-recovery-overview.md), you can create a Recovery Services vault, and select hello replication scenario.</span></span>

<span data-ttu-id="a545c-105">Dopo aver letto questo articolo, inviare eventuali commenti nella parte inferiore di hello o in hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="a545c-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="a545c-106">Creare un insieme di credenziali di Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="a545c-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]


## <a name="choose-a-protection-goal"></a><span data-ttu-id="a545c-107">Scegliere un obiettivo di protezione</span><span class="sxs-lookup"><span data-stu-id="a545c-107">Choose a protection goal</span></span>

<span data-ttu-id="a545c-108">Selezionare gli elementi si desidera tooreplicate e in cui si desidera tooreplicate per.</span><span class="sxs-lookup"><span data-stu-id="a545c-108">Select what you want tooreplicate and where you want tooreplicate to.</span></span>

1. <span data-ttu-id="a545c-109">Fare clic su **Site Recovery** > **Passaggio 1: Preparare l'infrastruttura** > **Obiettivo di protezione**.</span><span class="sxs-lookup"><span data-stu-id="a545c-109">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>
2. <span data-ttu-id="a545c-110">Selezionare **toorecovery sito**e selezionare **Sì, con Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="a545c-110">Select **toorecovery site**, and select **Yes, with Hyper-V**.</span></span>
3. <span data-ttu-id="a545c-111">Selezionare **Sì** tooindicate si utilizza un host Hyper-V hello toomanage VMM.</span><span class="sxs-lookup"><span data-stu-id="a545c-111">Select **Yes** tooindicate you're using VMM toomanage hello Hyper-V hosts.</span></span>
4. <span data-ttu-id="a545c-112">Selezionare **Sì** se si dispone di un server VMM secondario.</span><span class="sxs-lookup"><span data-stu-id="a545c-112">Select **Yes** if you have a secondary VMM server.</span></span> <span data-ttu-id="a545c-113">Se si distribuisce la replica tra cloud in un unico server VMM, fare clic su **No**.</span><span class="sxs-lookup"><span data-stu-id="a545c-113">If you're deploying replication between clouds on a single VMM server, click **No**.</span></span> <span data-ttu-id="a545c-114">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="a545c-114">Then click **OK**.</span></span>

    ![Scegliere gli obiettivi](./media/vmm-to-vmm-walkthrough-create-vault/choose-goals.png)



## <a name="next-steps"></a><span data-ttu-id="a545c-116">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a545c-116">Next steps</span></span>

<span data-ttu-id="a545c-117">Andare troppo[passaggio 6: configurare l'origine della replica hello e di destinazione](vmm-to-vmm-walkthrough-source-target.md).</span><span class="sxs-lookup"><span data-stu-id="a545c-117">Go too[Step 6: Set up hello replication source and target](vmm-to-vmm-walkthrough-source-target.md).</span></span>
