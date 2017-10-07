---
title: aaaSet un criterio di replica per macchina virtuale Hyper-V (con VMM) replica tooAzure con Azure Site Recovery | Documenti Microsoft
description: Viene descritto come tooset un criterio di replica per macchina virtuale Hyper-V (con VMM) replica tooAzure con Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: ee808b20-324b-4198-b831-edb65b95e8b7
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: e1579fde559ca34eca19a01e740fec28a0df2f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-set-up-a-replication-policy-for-hyper-v-vm-replication-with-vmm-tooazure"></a><span data-ttu-id="ed96b-103">Passaggio 10: Configurare un criterio di replica per macchina virtuale Hyper-V replica (con VMM) tooAzure</span><span class="sxs-lookup"><span data-stu-id="ed96b-103">Step 10: Set up a replication policy for Hyper-V VM replication (with VMM) tooAzure</span></span>


<span data-ttu-id="ed96b-104">Dopo l'impostazione [mapping di rete](vmm-to-azure-walkthrough-network-mapping.md), usare questo tooconfigure articolo un criterio di replica T\tooreplicate locale macchine virtuali Hyper-V gestite in tooAzure cloud di System Center Virtual Machine Manager (VMM), utilizzando hello [ Azure Site Recovery](site-recovery-overview.md) di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ed96b-104">After setting up [network mapping](vmm-to-azure-walkthrough-network-mapping.md), use this article tooconfigure a replication policy T\tooreplicate on-premises Hyper-V virtual machines managed in System Center Virtual Machine Manager (VMM) clouds tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="ed96b-105">Dopo aver letto questo articolo, inviare eventuali commenti nella parte inferiore di hello o in hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="ed96b-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="create-a-policy"></a><span data-ttu-id="ed96b-106">Creare un criterio</span><span class="sxs-lookup"><span data-stu-id="ed96b-106">Create a policy</span></span>

1. <span data-ttu-id="ed96b-107">toocreate nuovi criteri di replica, fare clic su **Prepare infrastruttura** > **le impostazioni di replica** > **+ crea e associa**.</span><span class="sxs-lookup"><span data-stu-id="ed96b-107">toocreate a new replication policy, click **Prepare infrastructure** > **Replication Settings** > **+Create and associate**.</span></span>

    ![Rete](./media/vmm-to-azure-walkthrough-replication/gs-replication.png)
2. <span data-ttu-id="ed96b-109">In **Criteri di creazione e associazione**specificare il nome dei criteri.</span><span class="sxs-lookup"><span data-stu-id="ed96b-109">In **Create and associate policy**, specify a policy name.</span></span>
3. <span data-ttu-id="ed96b-110">In **frequenza di copia**, specificare la frequenza con cui si desidera dati delta tooreplicate dopo la replica iniziale hello (ogni 30 secondi, 5 o 15 minuti).</span><span class="sxs-lookup"><span data-stu-id="ed96b-110">In **Copy frequency**, specify how often you want tooreplicate delta data after hello initial replication (every 30 seconds, 5 or 15 minutes).</span></span>

    > [!NOTE]
    >  <span data-ttu-id="ed96b-111">Quando la replica di archiviazione toopremium, non è supportata una frequenza secondo 30.</span><span class="sxs-lookup"><span data-stu-id="ed96b-111">A 30 second frequency isn't supported when replicating toopremium storage.</span></span> <span data-ttu-id="ed96b-112">limitazione di Hello è determinato dal numero di hello di snapshot per ogni blob (100) supportato da archiviazione premium.</span><span class="sxs-lookup"><span data-stu-id="ed96b-112">hello limitation is determined by hello number of snapshots per blob (100) supported by premium storage.</span></span> [<span data-ttu-id="ed96b-113">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="ed96b-113">Learn more</span></span>](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob)

4. <span data-ttu-id="ed96b-114">In **conservazione del punto di ripristino**, specificare in ore, per quanto tempo il periodo di memorizzazione hello verrà per ogni punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="ed96b-114">In **Recovery point retention**, specify in hours how long hello retention window will be for each recovery point.</span></span> <span data-ttu-id="ed96b-115">Macchine virtuali protette possono essere ripristinati tooany punto all'interno di una finestra.</span><span class="sxs-lookup"><span data-stu-id="ed96b-115">Protected machines can be recovered tooany point within a window.</span></span>
5. <span data-ttu-id="ed96b-116">In **Frequenza snapshot coerenti con l'app**specificare la frequenza, da 1 a 12 ore, per la creazione di punti di ripristino contenenti snapshot coerenti con l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ed96b-116">In **App-consistent snapshot frequency**, specify how frequently (1-12 hours) recovery points containing application-consistent snapshots will be created.</span></span> <span data-ttu-id="ed96b-117">Hyper-V usa due tipi di snapshot, uno snapshot standard che fornisce uno snapshot incrementale dell'intera macchina virtuale di hello e uno snapshot coerente dell'applicazione che accetta uno snapshot del punto nel tempo dei dati dell'applicazione hello macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="ed96b-117">Hyper-V uses two types of snapshots — a standard snapshot that provides an incremental snapshot of hello entire virtual machine, and an application-consistent snapshot that takes a point-in-time snapshot of hello application data inside hello virtual machine.</span></span> <span data-ttu-id="ed96b-118">Snapshot coerenti dell'applicazione usare tooensure del servizio Copia Shadow del Volume (VSS) che le applicazioni sono in uno stato coerente durante hello snapshot.</span><span class="sxs-lookup"><span data-stu-id="ed96b-118">Application-consistent snapshots use Volume Shadow Copy Service (VSS) tooensure that applications are in a consistent state when hello snapshot is taken.</span></span> <span data-ttu-id="ed96b-119">Si noti che se si abilita snapshot coerenti dell'applicazione, influisce negativamente sulle prestazioni di hello delle applicazioni in esecuzione in macchine virtuali di origine.</span><span class="sxs-lookup"><span data-stu-id="ed96b-119">Note that if you enable application-consistent snapshots, it will affect hello performance of applications running on source virtual machines.</span></span> <span data-ttu-id="ed96b-120">Verificare che il valore di hello impostato è minore hello numero di punti di ripristino aggiuntivi configurati.</span><span class="sxs-lookup"><span data-stu-id="ed96b-120">Ensure that hello value you set is less than hello number of additional recovery points you configure.</span></span>
6. <span data-ttu-id="ed96b-121">In **ora inizio replica iniziale**, indicare quando toostart hello la replica iniziale.</span><span class="sxs-lookup"><span data-stu-id="ed96b-121">In **Initial replication start time**, indicate when toostart hello initial replication.</span></span> <span data-ttu-id="ed96b-122">la replica di Hello viene eseguita tramite la larghezza di banda internet pertanto è opportuno tooschedule è di fuori dell'orario di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="ed96b-122">hello replication occurs over your internet bandwidth so you might want tooschedule it outside your busy hours.</span></span>
7. <span data-ttu-id="ed96b-123">In **crittografare i dati archiviati in Azure**, specificare se tooencrypt dati rest nell'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="ed96b-123">In **Encrypt data stored on Azure**, specify whether tooencrypt at rest data in Azure storage.</span></span> <span data-ttu-id="ed96b-124">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="ed96b-124">Then click **OK**.</span></span>

    ![Criteri di replica](./media/vmm-to-azure-walkthrough-replication/gs-replication2.png)
8. <span data-ttu-id="ed96b-126">Quando si crea un nuovo criterio automaticamente associato hello cloud VMM.</span><span class="sxs-lookup"><span data-stu-id="ed96b-126">When you create a new policy it's automatically associated with hello VMM cloud.</span></span> <span data-ttu-id="ed96b-127">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="ed96b-127">Click **OK**.</span></span> <span data-ttu-id="ed96b-128">È possibile associare altri cloud VMM (e hello macchine virtuali in essi contenuti) con questo criterio di replica in **replica** > Nome criterio > **associare Cloud VMM**.</span><span class="sxs-lookup"><span data-stu-id="ed96b-128">You can associate additional VMM clouds (and hello VMs in them) with this replication policy in **Replication** > policy name > **Associate VMM Cloud**.</span></span>

    ![Criteri di replica](./media/vmm-to-azure-walkthrough-replication/policy-associate.png)



## <a name="next-steps"></a><span data-ttu-id="ed96b-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ed96b-130">Next steps</span></span>

<span data-ttu-id="ed96b-131">Andare troppo[passaggio 11: abilitare la replica](vmm-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="ed96b-131">Go too[Step 11: Enable replication](vmm-to-azure-walkthrough-enable-replication.md)</span></span>
