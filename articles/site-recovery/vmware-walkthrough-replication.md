---
title: Configurare criteri di replica per la replica di VM VMware in Azure con Azure Site Recovery | Microsoft Docs
description: Vengono riepilogati i passaggi necessari per configurare criteri di replica per la replica di VM VMware in Archiviazione di Azure
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d7874bd8-6626-4668-9ec9-dbd2d26f8f81
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 3c4b7ad16e6a03fb605447def18f7475d502fdd1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="step-9-set-up-a-replication-policy-for-vmware-vm-replication-to-azure"></a><span data-ttu-id="f7007-103">Passaggio 9: Configurare criteri di replica per la replica di VM VMware in Azure</span><span class="sxs-lookup"><span data-stu-id="f7007-103">Step 9: Set up a replication policy for VMware VM replication to Azure</span></span>


<span data-ttu-id="f7007-104">Questo articolo illustra come configurare criteri di replica quando si esegue la replica di VM VMware in Azure usando il servizio [Azure Site Recovery](site-recovery-overview.md) nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f7007-104">This article describes how to set up a replication policy when you're replicating VMware VMs to Azure using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


<span data-ttu-id="f7007-105">Inserire commenti e domande nella parte inferiore di questo articolo oppure nel [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="f7007-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="configure-a-policy"></a><span data-ttu-id="f7007-106">Configurare i criteri</span><span class="sxs-lookup"><span data-stu-id="f7007-106">Configure a policy</span></span>

<span data-ttu-id="f7007-107">Ottenere una rapida panoramica video prima di iniziare:</span><span class="sxs-lookup"><span data-stu-id="f7007-107">Get a quick video overview before you start:</span></span>
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. <span data-ttu-id="f7007-108">Per creare nuovi criteri di replica, fare clic su **Infrastruttura di Site Recovery** > **Criteri di replica** > **+Criteri di replica**.</span><span class="sxs-lookup"><span data-stu-id="f7007-108">To create a new replication policy, click **Site Recovery infrastructure** > **Replication Policies** > **+Replication Policy**.</span></span>
2. <span data-ttu-id="f7007-109">In **Creare i criteri di replica** specificare un nome per i criteri.</span><span class="sxs-lookup"><span data-stu-id="f7007-109">In **Create replication policy**, specify a policy name.</span></span>
3. <span data-ttu-id="f7007-110">In **Soglia RPO**specificare il limite per RPO.</span><span class="sxs-lookup"><span data-stu-id="f7007-110">In **RPO threshold**, specify the RPO limit.</span></span> <span data-ttu-id="f7007-111">Questo valore specifica la frequenza con cui vengono creati punti di ripristino dei dati.</span><span class="sxs-lookup"><span data-stu-id="f7007-111">This value specifies how often data recovery points are created.</span></span> <span data-ttu-id="f7007-112">Se la replica continua supera questo limite, viene generato un avviso.</span><span class="sxs-lookup"><span data-stu-id="f7007-112">An alert is generated if continuous replication exceeds this limit.</span></span>
4. <span data-ttu-id="f7007-113">In **Conservazione del punto di ripristino** specificare la durata in ore dell'intervallo di conservazione per ogni punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="f7007-113">In **Recovery point retention**, specify (in hours) how long the retention window is for each recovery point.</span></span> <span data-ttu-id="f7007-114">Le VM replicate possono essere ripristinate in qualsiasi punto all'interno di un intervallo.</span><span class="sxs-lookup"><span data-stu-id="f7007-114">Replicated VMs can be recovered to any point in a window.</span></span> <span data-ttu-id="f7007-115">È supportata la conservazione fino a 24 ore per le macchine replicate in Archiviazione Premium e fino a 72 ore per Archiviazione Standard.</span><span class="sxs-lookup"><span data-stu-id="f7007-115">Up to 24 hours retention is supported for machines replicated to premium storage, and 72 hours for standard storage.</span></span>
5. <span data-ttu-id="f7007-116">In **Frequenza snapshot coerenti con l'app**specificare la frequenza, in minuti, per la creazione di punti di ripristino contenenti snapshot coerenti con l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f7007-116">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points containing application-consistent snapshots will be created.</span></span> <span data-ttu-id="f7007-117">Fare clic su **OK** per creare i criteri.</span><span class="sxs-lookup"><span data-stu-id="f7007-117">Click **OK** to create the policy.</span></span>

    ![Criteri di replica](./media/vmware-walkthrough-replication/gs-replication2.png)
8. <span data-ttu-id="f7007-119">Quando si creano nuovi criteri, questi vengono associati automaticamente al server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="f7007-119">When you create a new policy it's automatically associated with the configuration server.</span></span> <span data-ttu-id="f7007-120">Per impostazione predefinita vengono creati automaticamente criteri corrispondenti per il failback.</span><span class="sxs-lookup"><span data-stu-id="f7007-120">By default, a matching policy is automatically created for failback.</span></span> <span data-ttu-id="f7007-121">Se, ad esempio, il criterio di replica è **rep-policy**, il criterio di failback sarà **rep-policy-failback**.</span><span class="sxs-lookup"><span data-stu-id="f7007-121">For example, if the replication policy is **rep-policy** then the failback policy will be **rep-policy-failback**.</span></span> <span data-ttu-id="f7007-122">Questi criteri non vengono usati fino a quando non si avvia un failback da Azure.</span><span class="sxs-lookup"><span data-stu-id="f7007-122">This policy isn't used until you initiate a failback from Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7007-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f7007-123">Next steps</span></span>

<span data-ttu-id="f7007-124">Andare a [Passaggio 10: Installare il servizio Mobility](vmware-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="f7007-124">Go to [Step 10: Install the Mobility service](vmware-walkthrough-install-mobility.md)</span></span>
