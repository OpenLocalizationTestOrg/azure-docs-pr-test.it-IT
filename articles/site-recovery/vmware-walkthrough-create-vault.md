---
title: Configurare un insieme di credenziali per la replica VMware in Azure usando Azure Site Recovery | Microsoft Docs
description: Vengono riepilogati i passaggi necessari per configurare un insieme di credenziali per la replica VMware in Azure usando Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8bce940e-f19f-4418-8360-aee7b073519a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: dca95ad46b8de587140c3573ba6ed5702a122032
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="step-7-set-up-a-vault-for-vmware-replication-to-azure"></a><span data-ttu-id="b80d4-103">Passaggio 7: Configurare un insieme di credenziali per la replica VMware in Azure</span><span class="sxs-lookup"><span data-stu-id="b80d4-103">Step 7: Set up a vault for VMware replication to Azure</span></span>


<span data-ttu-id="b80d4-104">Questo articolo descrive come configurare un insieme di credenziali e specificare ciò di cui si vuole eseguire la replica dall'ambiente locale ad Azure usando il servizio [Azure Site Recovery](site-recovery-overview.md) nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b80d4-104">This article describes how to set up a vault, and specify what you want to replicate from your on-premises location, to Azure using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


<span data-ttu-id="b80d4-105">Inserire commenti e domande nella parte inferiore di questo articolo oppure nel [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="b80d4-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="b80d4-106">Creare un insieme di credenziali di Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="b80d4-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a><span data-ttu-id="b80d4-107">Scegliere un obiettivo di protezione</span><span class="sxs-lookup"><span data-stu-id="b80d4-107">Select a protection goal</span></span>

<span data-ttu-id="b80d4-108">Selezionare gli elementi da replicare e la posizione in cui eseguire la replica.</span><span class="sxs-lookup"><span data-stu-id="b80d4-108">Select what you want to replicate, and where you want to replicate to.</span></span>

1. <span data-ttu-id="b80d4-109">Fare clic su **Insiemi di credenziali dei servizi di ripristino** e quindi sull'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="b80d4-109">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="b80d4-110">Nel menu Risorsa fare clic su **Site Recovery** > **Preparare l'infrastruttura** > **Obiettivo di protezione**.</span><span class="sxs-lookup"><span data-stu-id="b80d4-110">In the Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="b80d4-111">In **Obiettivo di protezione** selezionare **In Azure** > **Sì, con VMware vSphere Hypervisor**.</span><span class="sxs-lookup"><span data-stu-id="b80d4-111">In **Protection goal**, select **To Azure** > **Yes, with VMware vSphere Hypervisor**.</span></span>



## <a name="next-steps"></a><span data-ttu-id="b80d4-112">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b80d4-112">Next steps</span></span>

<span data-ttu-id="b80d4-113">Andare a [Passaggio 8: Configurare l'origine e la destinazione](vmware-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="b80d4-113">Go to [Step 8: Set up source and target](vmware-walkthrough-source-target.md)</span></span>
