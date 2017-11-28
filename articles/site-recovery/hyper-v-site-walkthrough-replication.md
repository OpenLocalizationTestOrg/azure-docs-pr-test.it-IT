---
title: aaaSet un criterio di replica per macchina virtuale Hyper-V replica (senza System Center VMM) tooAzure con Azure Site Recovery | Documenti Microsoft
description: "Vengono riepilogati i passaggi di hello è necessario tooset un criterio di replica per la replica di archiviazione di macchine virtuali Hyper-V tooAzure"
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 1777e0eb-accb-42b5-a747-11272e131a52
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 4bd7161f4a0f015da0ecf595fbc6861ede5d68b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-set-up-a-replication-policy-for-hyper-v-vm-replication-tooazure"></a><span data-ttu-id="4fb48-103">Passaggio 9: Configurare un criterio di replica per macchina virtuale Hyper-V replica tooAzure</span><span class="sxs-lookup"><span data-stu-id="4fb48-103">Step 9: Set up a replication policy for Hyper-V VM replication tooAzure</span></span>

<span data-ttu-id="4fb48-104">Questo articolo viene descritto come tooset un criterio di replica quando si esegue la replica tooAzure macchine virtuali Hyper-V (senza System Center VMM) usando hello [Azure Site Recovery](site-recovery-overview.md) di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4fb48-104">This article describes how tooset up a replication policy when you're replicating Hyper-V VMs tooAzure (without System Center VMM) using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="4fb48-105">Inviare commenti e domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="4fb48-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="about-snapshots"></a><span data-ttu-id="4fb48-106">Informazioni sugli snapshot</span><span class="sxs-lookup"><span data-stu-id="4fb48-106">About snapshots</span></span>

<span data-ttu-id="4fb48-107">Hyper-V usa due tipi di snapshot, uno snapshot standard che fornisce uno snapshot incrementale dell'intera macchina virtuale di hello e uno snapshot coerente dell'applicazione che accetta uno snapshot del punto nel tempo dei dati dell'applicazione hello macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="4fb48-107">Hyper-V uses two types of snapshots — a standard snapshot that provides an incremental snapshot of hello entire virtual machine, and an application-consistent snapshot that takes a point-in-time snapshot of hello application data inside hello virtual machine.</span></span>
    - <span data-ttu-id="4fb48-108">Snapshot coerenti dell'applicazione usare tooensure del servizio Copia Shadow del Volume (VSS) che le applicazioni sono in uno stato coerente durante hello snapshot.</span><span class="sxs-lookup"><span data-stu-id="4fb48-108">Application-consistent snapshots use Volume Shadow Copy Service (VSS) tooensure that applications are in a consistent state when hello snapshot is taken.</span></span>
    - <span data-ttu-id="4fb48-109">Se si abilita snapshot coerenti dell'applicazione, influisce negativamente sulle prestazioni di hello delle applicazioni in esecuzione in macchine virtuali di origine.</span><span class="sxs-lookup"><span data-stu-id="4fb48-109">If you enable application-consistent snapshots, it will affect hello performance of applications running on source virtual machines.</span></span> <span data-ttu-id="4fb48-110">Verificare che il valore di hello impostato è minore hello numero di punti di ripristino aggiuntivi configurati.</span><span class="sxs-lookup"><span data-stu-id="4fb48-110">Ensure that hello value you set is less than hello number of additional recovery points you configure.</span></span>

## <a name="set-up-a-replication-policy"></a><span data-ttu-id="4fb48-111">Configurare criteri di replica</span><span class="sxs-lookup"><span data-stu-id="4fb48-111">Set up a replication policy</span></span>

1. <span data-ttu-id="4fb48-112">toocreate nuovi criteri di replica, fare clic su **Prepare infrastruttura** > **le impostazioni di replica** > **+ crea e associa**.</span><span class="sxs-lookup"><span data-stu-id="4fb48-112">toocreate a new replication policy, click **Prepare infrastructure** > **Replication Settings** > **+Create and associate**.</span></span>

    ![Rete](./media/hyper-v-site-walkthrough-replication/gs-replication.png)
2. <span data-ttu-id="4fb48-114">In **Criteri di creazione e associazione**specificare il nome dei criteri.</span><span class="sxs-lookup"><span data-stu-id="4fb48-114">In **Create and associate policy**, specify a policy name.</span></span>
3. <span data-ttu-id="4fb48-115">In **frequenza di copia**, specificare la frequenza con cui si desidera dati delta tooreplicate dopo la replica iniziale hello (ogni 30 secondi, 5 o 15 minuti).</span><span class="sxs-lookup"><span data-stu-id="4fb48-115">In **Copy frequency**, specify how often you want tooreplicate delta data after hello initial replication (every 30 seconds, 5 or 15 minutes).</span></span>

    > [!NOTE]
    > <span data-ttu-id="4fb48-116">Quando la replica di archiviazione toopremium, non è supportata una frequenza secondo 30.</span><span class="sxs-lookup"><span data-stu-id="4fb48-116">A 30 second frequency isn't supported when replicating toopremium storage.</span></span> <span data-ttu-id="4fb48-117">limitazione di Hello è determinato dal numero di hello di snapshot per ogni blob (100) supportato da archiviazione premium.</span><span class="sxs-lookup"><span data-stu-id="4fb48-117">hello limitation is determined by hello number of snapshots per blob (100) supported by premium storage.</span></span> <span data-ttu-id="4fb48-118">[Altre informazioni](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob)</span><span class="sxs-lookup"><span data-stu-id="4fb48-118">[Learn more](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob).</span></span>

4. <span data-ttu-id="4fb48-119">In **conservazione del punto di ripristino**, specificare in ore il tempo è un intervallo di conservazione hello per ogni punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="4fb48-119">In **Recovery point retention**, specify in hours how long hello retention window is for each recovery point.</span></span> <span data-ttu-id="4fb48-120">Macchine virtuali possono essere ripristinati tooany punto all'interno di una finestra.</span><span class="sxs-lookup"><span data-stu-id="4fb48-120">VMs can be recovered tooany point within a window.</span></span>
5. <span data-ttu-id="4fb48-121">In **Frequenza snapshot coerenti con l'app** specificare la frequenza, da 1 a 12 ore, per la creazione di punti di ripristino contenenti snapshot coerenti con l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4fb48-121">In **App-consistent snapshot frequency**, specify how frequently (1-12 hours) recovery points containing application-consistent snapshots are created.</span></span>
6. <span data-ttu-id="4fb48-122">In **ora inizio replica iniziale**, specificare quando toostart hello la replica iniziale.</span><span class="sxs-lookup"><span data-stu-id="4fb48-122">In **Initial replication start time**, specify when toostart hello initial replication.</span></span> <span data-ttu-id="4fb48-123">la replica di Hello viene eseguita tramite la larghezza di banda internet pertanto è opportuno tooschedule è di fuori dell'orario di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="4fb48-123">hello replication occurs over your internet bandwidth so you might want tooschedule it outside your busy hours.</span></span> <span data-ttu-id="4fb48-124">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="4fb48-124">Then click **OK**.</span></span>

    ![Criteri di replica](./media/hyper-v-site-walkthrough-replication/gs-replication2.png)

<span data-ttu-id="4fb48-126">Quando si crea un nuovo criterio, è associata automaticamente a sito Hyper-V hello.</span><span class="sxs-lookup"><span data-stu-id="4fb48-126">When you create a new policy, it's automatically associated with hello Hyper-V site.</span></span> <span data-ttu-id="4fb48-127">È possibile associare un sito Hyper-V (e hello macchine virtuali in esso) a più criteri di replica in **replica** > criteri-name > **associare sito Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="4fb48-127">You can associate a Hyper-V site (and hello VMs in it) with multiple replication policies in **Replication** > policy-name > **Associate Hyper-V Site**.</span></span>



## <a name="next-steps"></a><span data-ttu-id="4fb48-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4fb48-128">Next steps</span></span>

<span data-ttu-id="4fb48-129">Andare troppo[passaggio 10: abilitare la replica](hyper-v-site-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="4fb48-129">Go too[Step 10: Enable replication](hyper-v-site-walkthrough-enable-replication.md)</span></span>
