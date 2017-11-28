---
title: Configurare un insieme di credenziali per la replica di server fisici in Azure usando Azure Site Recovery | Microsoft Docs
description: Vengono riepilogati i passaggi necessari per configurare un insieme di credenziali per la replica di server fisici in Azure usando Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d99f2605-f417-4995-be77-5323136b814f
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: deb5ad0495edc969b374795eeb2698326dd4ff4d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="step-6-set-up-a-vault-for-physical-server-replication-to-azure"></a><span data-ttu-id="5f7e8-103">Passaggio 6: Configurare un insieme di credenziali per la replica di server fisici in Azure</span><span class="sxs-lookup"><span data-stu-id="5f7e8-103">Step 6: Set up a vault for physical server replication to Azure</span></span>


<span data-ttu-id="5f7e8-104">Questo articolo descrive come configurare un insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="5f7e8-104">This article describes how to set up a vault.</span></span> <span data-ttu-id="5f7e8-105">Per creare l'insieme di credenziali e specificare ciò di cui si vuole eseguire la replica dall'ambiente locale in Azure, usare il servizio [Azure Site Recovery](site-recovery-overview.md) nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5f7e8-105">You create the vault, and specify what you want to replicate from your on-premises location to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


<span data-ttu-id="5f7e8-106">Inserire commenti e domande nella parte inferiore di questo articolo oppure nel [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="5f7e8-106">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="5f7e8-107">Creare un insieme di credenziali di Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="5f7e8-107">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a><span data-ttu-id="5f7e8-108">Scegliere un obiettivo di protezione</span><span class="sxs-lookup"><span data-stu-id="5f7e8-108">Select a protection goal</span></span>

<span data-ttu-id="5f7e8-109">Selezionare gli elementi da replicare e la posizione in cui eseguire la replica.</span><span class="sxs-lookup"><span data-stu-id="5f7e8-109">Select what you want to replicate, and where you want to replicate to.</span></span>

1. <span data-ttu-id="5f7e8-110">Fare clic su **Insiemi di credenziali dei servizi di ripristino** e quindi sull'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="5f7e8-110">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="5f7e8-111">Nel menu Risorsa fare clic su **Site Recovery** > **Preparare l'infrastruttura** > **Obiettivo di protezione**.</span><span class="sxs-lookup"><span data-stu-id="5f7e8-111">In the Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="5f7e8-112">In **Obiettivo di protezione** selezionare **To Azure (In Azure)** > **Non virtualizzato/Altro**.</span><span class="sxs-lookup"><span data-stu-id="5f7e8-112">In **Protection goal**, select **To Azure** > **Not virtualized/Other**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="5f7e8-113">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5f7e8-113">Next steps</span></span>

<span data-ttu-id="5f7e8-114">Andare a [Passaggio 7: Configurare l'origine e la destinazione](physical-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="5f7e8-114">Go to [Step 7: Set up source and target](physical-walkthrough-source-target.md)</span></span>
