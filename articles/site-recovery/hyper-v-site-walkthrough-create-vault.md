---
title: aaaSet di un insieme di credenziali per Hyper-V replica (senza System Center VMM) tooAzure usando Azure Site Recovery | Documenti Microsoft
description: Vengono riepilogati i passaggi di hello tooset di un insieme di credenziali necessarie per Hyper-V replica tooAzure usando Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a936b3e2-0dbe-47ac-a98e-5285d96dc786
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: e3ef8758faab36d19d0968d98a23105bed7830f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-a-vault-for-hyper-v-replication"></a><span data-ttu-id="6b3aa-103">Passaggio 7: Configurare un insieme di credenziali per la replica Hyper-V</span><span class="sxs-lookup"><span data-stu-id="6b3aa-103">Step 7: Set up a vault for Hyper-V replication</span></span>

<span data-ttu-id="6b3aa-104">In questo articolo viene descritto come configurare un insieme di credenziali, tooset e specificare le tooreplicate dal percorso locale, utilizzando hello tooAzure [Azure Site Recovery](site-recovery-overview.md) di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6b3aa-104">This article describes how tooset up a vault, and specify what you want tooreplicate from your on-premises location, tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="6b3aa-105">Inviare commenti e domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="6b3aa-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="6b3aa-106">Creare un insieme di credenziali di Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="6b3aa-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]



## <a name="select-a-protection-goal"></a><span data-ttu-id="6b3aa-107">Scegliere un obiettivo di protezione</span><span class="sxs-lookup"><span data-stu-id="6b3aa-107">Select a protection goal</span></span>

<span data-ttu-id="6b3aa-108">Selezionare gli elementi da tooreplicate, e in cui si desidera tooreplicate per.</span><span class="sxs-lookup"><span data-stu-id="6b3aa-108">Select what you want tooreplicate, and where you want tooreplicate to.</span></span>

1. <span data-ttu-id="6b3aa-109">Fare clic su **Insiemi di credenziali dei servizi di ripristino** e quindi sull'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="6b3aa-109">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="6b3aa-110">In hello risorsa Menu, fare clic su **Site Recovery** > **preparare l'infrastruttura** > **obiettivi della protezione dati**.</span><span class="sxs-lookup"><span data-stu-id="6b3aa-110">In hello Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="6b3aa-111">In **obiettivi della protezione dati**selezionare **tooAzure** > **Sì, con Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="6b3aa-111">In **Protection goal**, select **tooAzure** > **Yes, with Hyper-V**.</span></span> <span data-ttu-id="6b3aa-112">Selezionare **n** tooconfirm VMM non è in uso.</span><span class="sxs-lookup"><span data-stu-id="6b3aa-112">Select **No** tooconfirm you're not using VMM.</span></span> 

    ![Scegliere gli obiettivi](./media/hyper-v-site-walkthrough-create-vault/choose-goals2.png)



## <a name="next-steps"></a><span data-ttu-id="6b3aa-114">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6b3aa-114">Next steps</span></span>

<span data-ttu-id="6b3aa-115">Andare troppo[passaggio 8: Imposta origine e destinazione](hyper-v-site-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="6b3aa-115">Go too[Step 8: Set up source and target](hyper-v-site-walkthrough-source-target.md)</span></span>
