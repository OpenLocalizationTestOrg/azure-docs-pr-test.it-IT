---
title: aaaSet un criterio di replica per tooAzure replica VMware VM con Azure Site Recovery | Documenti Microsoft
description: "Vengono riepilogati i passaggi di hello è necessario tooset un criterio di replica per la replica di archiviazione di macchine virtuali VMware tooAzure"
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
ms.openlocfilehash: 12870f3f98a4dd412221b817581403cd4bf7a76d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-set-up-a-replication-policy-for-vmware-vm-replication-tooazure"></a><span data-ttu-id="4b1d0-103">Passaggio 9: Configurare un criterio di replica per VMware VM replica tooAzure</span><span class="sxs-lookup"><span data-stu-id="4b1d0-103">Step 9: Set up a replication policy for VMware VM replication tooAzure</span></span>


<span data-ttu-id="4b1d0-104">Questo articolo viene descritto come tooset un criterio di replica quando si esegue la replica di macchine virtuali VMware tooAzure utilizzando hello [Azure Site Recovery](site-recovery-overview.md) di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4b1d0-104">This article describes how tooset up a replication policy when you're replicating VMware VMs tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="4b1d0-105">Inviare commenti e domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="4b1d0-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="configure-a-policy"></a><span data-ttu-id="4b1d0-106">Configurare i criteri</span><span class="sxs-lookup"><span data-stu-id="4b1d0-106">Configure a policy</span></span>

<span data-ttu-id="4b1d0-107">Ottenere una rapida panoramica video prima di iniziare:</span><span class="sxs-lookup"><span data-stu-id="4b1d0-107">Get a quick video overview before you start:</span></span>
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. <span data-ttu-id="4b1d0-108">toocreate nuovi criteri di replica, fare clic su **dell'infrastruttura di Site Recovery** > **criteri di replica** > **+ criterio di replica**.</span><span class="sxs-lookup"><span data-stu-id="4b1d0-108">toocreate a new replication policy, click **Site Recovery infrastructure** > **Replication Policies** > **+Replication Policy**.</span></span>
2. <span data-ttu-id="4b1d0-109">In **Creare i criteri di replica** specificare un nome per i criteri.</span><span class="sxs-lookup"><span data-stu-id="4b1d0-109">In **Create replication policy**, specify a policy name.</span></span>
3. <span data-ttu-id="4b1d0-110">In **soglia RPO**, specificare il limite RPO hello.</span><span class="sxs-lookup"><span data-stu-id="4b1d0-110">In **RPO threshold**, specify hello RPO limit.</span></span> <span data-ttu-id="4b1d0-111">Questo valore specifica la frequenza con cui vengono creati punti di ripristino dei dati.</span><span class="sxs-lookup"><span data-stu-id="4b1d0-111">This value specifies how often data recovery points are created.</span></span> <span data-ttu-id="4b1d0-112">Se la replica continua supera questo limite, viene generato un avviso.</span><span class="sxs-lookup"><span data-stu-id="4b1d0-112">An alert is generated if continuous replication exceeds this limit.</span></span>
4. <span data-ttu-id="4b1d0-113">In **conservazione del punto di ripristino**, specificare per quanto tempo (in ore) è un intervallo di conservazione hello per ogni punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="4b1d0-113">In **Recovery point retention**, specify (in hours) how long hello retention window is for each recovery point.</span></span> <span data-ttu-id="4b1d0-114">Macchine virtuali replicate possono essere ripristinati tooany punto in una finestra.</span><span class="sxs-lookup"><span data-stu-id="4b1d0-114">Replicated VMs can be recovered tooany point in a window.</span></span> <span data-ttu-id="4b1d0-115">Backup too24 conservazione ore è supportata per i computer replicati archiviazione toopremium e 72 ore per l'archiviazione standard.</span><span class="sxs-lookup"><span data-stu-id="4b1d0-115">Up too24 hours retention is supported for machines replicated toopremium storage, and 72 hours for standard storage.</span></span>
5. <span data-ttu-id="4b1d0-116">In **Frequenza snapshot coerenti con l'app**specificare la frequenza, in minuti, per la creazione di punti di ripristino contenenti snapshot coerenti con l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4b1d0-116">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points containing application-consistent snapshots will be created.</span></span> <span data-ttu-id="4b1d0-117">Fare clic su **OK** criteri hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="4b1d0-117">Click **OK** toocreate hello policy.</span></span>

    ![Criteri di replica](./media/vmware-walkthrough-replication/gs-replication2.png)
8. <span data-ttu-id="4b1d0-119">Quando si crea un nuovo criterio associata automaticamente con il server di configurazione di hello.</span><span class="sxs-lookup"><span data-stu-id="4b1d0-119">When you create a new policy it's automatically associated with hello configuration server.</span></span> <span data-ttu-id="4b1d0-120">Per impostazione predefinita vengono creati automaticamente criteri corrispondenti per il failback.</span><span class="sxs-lookup"><span data-stu-id="4b1d0-120">By default, a matching policy is automatically created for failback.</span></span> <span data-ttu-id="4b1d0-121">Ad esempio, se hello criterio di replica è **rep criteri** verrà utilizzato come criterio di failback hello **rep-criteri-failback**.</span><span class="sxs-lookup"><span data-stu-id="4b1d0-121">For example, if hello replication policy is **rep-policy** then hello failback policy will be **rep-policy-failback**.</span></span> <span data-ttu-id="4b1d0-122">Questi criteri non vengono usati fino a quando non si avvia un failback da Azure.</span><span class="sxs-lookup"><span data-stu-id="4b1d0-122">This policy isn't used until you initiate a failback from Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b1d0-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4b1d0-123">Next steps</span></span>

<span data-ttu-id="4b1d0-124">Andare troppo[passaggio 10: installare il servizio Mobility hello](vmware-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="4b1d0-124">Go too[Step 10: Install hello Mobility service](vmware-walkthrough-install-mobility.md)</span></span>
