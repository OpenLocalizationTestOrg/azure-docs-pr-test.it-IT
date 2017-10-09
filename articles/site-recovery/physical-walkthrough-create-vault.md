---
title: aaaSet di un insieme di credenziali per il server fisico replica tooAzure usando Azure Site Recovery | Documenti Microsoft
description: "Vengono riepilogati i passaggi di hello è necessario tooset backup tooAzure di server fisici tooreplicate un insieme di credenziali usando Azure Site Recovery"
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
ms.openlocfilehash: 988928e3ece31116823f132cc39223fe44443468
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-set-up-a-vault-for-physical-server-replication-tooazure"></a><span data-ttu-id="41816-103">Passaggio 6: Configurare un insieme di credenziali per tooAzure replica server fisico</span><span class="sxs-lookup"><span data-stu-id="41816-103">Step 6: Set up a vault for physical server replication tooAzure</span></span>


<span data-ttu-id="41816-104">Questo articolo viene descritto come tooset di un insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="41816-104">This article describes how tooset up a vault.</span></span> <span data-ttu-id="41816-105">Creare l'insieme di credenziali hello e specificare gli elementi da tooreplicate dal tooAzure percorso locale, utilizzando hello [Azure Site Recovery](site-recovery-overview.md) di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="41816-105">You create hello vault, and specify what you want tooreplicate from your on-premises location tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="41816-106">Inviare commenti e domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="41816-106">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="41816-107">Creare un insieme di credenziali di Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="41816-107">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a><span data-ttu-id="41816-108">Scegliere un obiettivo di protezione</span><span class="sxs-lookup"><span data-stu-id="41816-108">Select a protection goal</span></span>

<span data-ttu-id="41816-109">Selezionare gli elementi da tooreplicate, e in cui si desidera tooreplicate per.</span><span class="sxs-lookup"><span data-stu-id="41816-109">Select what you want tooreplicate, and where you want tooreplicate to.</span></span>

1. <span data-ttu-id="41816-110">Fare clic su **Insiemi di credenziali dei servizi di ripristino** e quindi sull'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="41816-110">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="41816-111">In hello risorsa Menu, fare clic su **Site Recovery** > **preparare l'infrastruttura** > **obiettivi della protezione dati**.</span><span class="sxs-lookup"><span data-stu-id="41816-111">In hello Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="41816-112">In **obiettivi della protezione dati**selezionare **tooAzure** > **non virtualizzato/altri**.</span><span class="sxs-lookup"><span data-stu-id="41816-112">In **Protection goal**, select **tooAzure** > **Not virtualized/Other**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="41816-113">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="41816-113">Next steps</span></span>

<span data-ttu-id="41816-114">Andare troppo[passaggio 7: configurare l'origine e di destinazione](physical-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="41816-114">Go too[Step 7: Set up source and target](physical-walkthrough-source-target.md)</span></span>
