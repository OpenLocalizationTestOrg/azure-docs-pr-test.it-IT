---
title: Creare un insieme di credenziali per la replica Hyper-V in un sito secondario con Azure Site Recovery | Microsoft Docs
description: Illustra come creare un insieme di credenziali durante la replica di VM Hyper-V in un sito System Center VMM secondario con Azure Site Recovery.
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
ms.openlocfilehash: 28cfcf12b2e369f96664c163c0b6f2aa8a6ddcb9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="step-5-create-a-vault-for-hyper-v-replication-to-a-secondary-site"></a><span data-ttu-id="99f9b-103">Passaggio 5: Creare un insieme di credenziali per la replica Hyper-V in un sito secondario</span><span class="sxs-lookup"><span data-stu-id="99f9b-103">Step 5: Create a vault for Hyper-V replication to a secondary site</span></span>

<span data-ttu-id="99f9b-104">Dopo la preparazione di [server System Center Virtual Machine Manager (VMM) locali e host/cluster Hyper-V](vmm-to-vmm-walkthrough-vmm-hyper-v.md) per la replica Hyper-V in un sito secondario tramite [Azure Site Recovery](site-recovery-overview.md), è possibile creare un insieme di credenziali di Servizi di ripristino e selezionare lo scenario di replica.</span><span class="sxs-lookup"><span data-stu-id="99f9b-104">After preparing on-premises [System Center Virtual Machine Manager (VMM) servers and Hyper-V hosts/clusters](vmm-to-vmm-walkthrough-vmm-hyper-v.md) for Hyper-V replication to a secondary site using [Azure Site Recovery](site-recovery-overview.md), you can create a Recovery Services vault, and select the replication scenario.</span></span>

<span data-ttu-id="99f9b-105">È possibile inviare commenti nella parte inferiore di questo articolo oppure nel [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="99f9b-105">After reading this article, post any comments at the bottom, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="99f9b-106">Creare un insieme di credenziali di Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="99f9b-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]


## <a name="choose-a-protection-goal"></a><span data-ttu-id="99f9b-107">Scegliere un obiettivo di protezione</span><span class="sxs-lookup"><span data-stu-id="99f9b-107">Choose a protection goal</span></span>

<span data-ttu-id="99f9b-108">Selezionare gli elementi da replicare e la posizione in cui eseguire la replica.</span><span class="sxs-lookup"><span data-stu-id="99f9b-108">Select what you want to replicate and where you want to replicate to.</span></span>

1. <span data-ttu-id="99f9b-109">Fare clic su **Site Recovery** > **Passaggio 1: Preparare l'infrastruttura** > **Obiettivo di protezione**.</span><span class="sxs-lookup"><span data-stu-id="99f9b-109">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>
2. <span data-ttu-id="99f9b-110">Selezionare **Nel sito di ripristino**, quindi fare clic su **Yes, with Hyper-V** (Sì, con Hyper-V).</span><span class="sxs-lookup"><span data-stu-id="99f9b-110">Select **To recovery site**, and select **Yes, with Hyper-V**.</span></span>
3. <span data-ttu-id="99f9b-111">Selezionare **Sì** per indicare che si usa VMM per gestire gli host Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="99f9b-111">Select **Yes** to indicate you're using VMM to manage the Hyper-V hosts.</span></span>
4. <span data-ttu-id="99f9b-112">Selezionare **Sì** se si dispone di un server VMM secondario.</span><span class="sxs-lookup"><span data-stu-id="99f9b-112">Select **Yes** if you have a secondary VMM server.</span></span> <span data-ttu-id="99f9b-113">Se si distribuisce la replica tra cloud in un unico server VMM, fare clic su **No**.</span><span class="sxs-lookup"><span data-stu-id="99f9b-113">If you're deploying replication between clouds on a single VMM server, click **No**.</span></span> <span data-ttu-id="99f9b-114">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="99f9b-114">Then click **OK**.</span></span>

    ![Scegliere gli obiettivi](./media/vmm-to-vmm-walkthrough-create-vault/choose-goals.png)



## <a name="next-steps"></a><span data-ttu-id="99f9b-116">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="99f9b-116">Next steps</span></span>

<span data-ttu-id="99f9b-117">Andare al [Passaggio 6: Configurare l'origine e la destinazione della replica](vmm-to-vmm-walkthrough-source-target.md).</span><span class="sxs-lookup"><span data-stu-id="99f9b-117">Go to [Step 6: Set up the replication source and target](vmm-to-vmm-walkthrough-source-target.md).</span></span>