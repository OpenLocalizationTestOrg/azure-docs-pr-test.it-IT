---
title: Configurare i criteri per la replica in Azure di una macchina virtuale Hyper-V (con VMM) tramite Azure Site Recovery | Microsoft Docs
description: Descrive come configurare i criteri per la replica in Azure di una macchina virtuale Hyper-V (con VMM) tramite Azure Site Recovery
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
ms.openlocfilehash: 592e1c3f647e5b1f1d9aa776657e8f89b60349e1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="step-10-set-up-a-replication-policy-for-hyper-v-vm-replication-with-vmm-to-azure"></a><span data-ttu-id="3ba90-103">Passaggio 10: Configurare i criteri per la replica di una macchina virtuale Hyper-V (con VMM) in Azure</span><span class="sxs-lookup"><span data-stu-id="3ba90-103">Step 10: Set up a replication policy for Hyper-V VM replication (with VMM) to Azure</span></span>


<span data-ttu-id="3ba90-104">Dopo aver configurato il [mapping di rete](vmm-to-azure-walkthrough-network-mapping.md), usare le informazioni in questo articolo per configurare i criteri necessari per la replica in Azure di macchine virtuali Hyper-V locali gestite in cloud di System Center Virtual Machine Manager (VMM) usando il servizio [Azure Site Recovery](site-recovery-overview.md) nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3ba90-104">After setting up [network mapping](vmm-to-azure-walkthrough-network-mapping.md), use this article to configure a replication policy T\to replicate on-premises Hyper-V virtual machines managed in System Center Virtual Machine Manager (VMM) clouds to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="3ba90-105">È possibile inviare commenti nella parte inferiore di questo articolo oppure nel [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="3ba90-105">After reading this article, post any comments at the bottom, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="create-a-policy"></a><span data-ttu-id="3ba90-106">Creare un criterio</span><span class="sxs-lookup"><span data-stu-id="3ba90-106">Create a policy</span></span>

1. <span data-ttu-id="3ba90-107">Per creare nuovi criteri di replica, fare clic su **Preparare l'infrastruttura** > **Impostazioni della replica** > **+Crea e associa**.</span><span class="sxs-lookup"><span data-stu-id="3ba90-107">To create a new replication policy, click **Prepare infrastructure** > **Replication Settings** > **+Create and associate**.</span></span>

    ![Rete](./media/vmm-to-azure-walkthrough-replication/gs-replication.png)
2. <span data-ttu-id="3ba90-109">In **Criteri di creazione e associazione**specificare il nome dei criteri.</span><span class="sxs-lookup"><span data-stu-id="3ba90-109">In **Create and associate policy**, specify a policy name.</span></span>
3. <span data-ttu-id="3ba90-110">In **Frequenza di copia**specificare la frequenza con cui replicare i dati differenziali dopo la replica iniziale, ogni 30 secondi oppure ogni 5 o 15 minuti.</span><span class="sxs-lookup"><span data-stu-id="3ba90-110">In **Copy frequency**, specify how often you want to replicate delta data after the initial replication (every 30 seconds, 5 or 15 minutes).</span></span>

    > [!NOTE]
    >  <span data-ttu-id="3ba90-111">Quando si esegue la replica in archiviazione Premium la frequenza di 30 secondi non è supportata.</span><span class="sxs-lookup"><span data-stu-id="3ba90-111">A 30 second frequency isn't supported when replicating to premium storage.</span></span> <span data-ttu-id="3ba90-112">Il limite è determinato dal numero di snapshot per BLOB (100) supportato dal servizio di archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="3ba90-112">The limitation is determined by the number of snapshots per blob (100) supported by premium storage.</span></span> [<span data-ttu-id="3ba90-113">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="3ba90-113">Learn more</span></span>](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob)

4. <span data-ttu-id="3ba90-114">In **Conservazione del punto di ripristino**specificare la durata in ore dell'intervallo di conservazione per ogni punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="3ba90-114">In **Recovery point retention**, specify in hours how long the retention window will be for each recovery point.</span></span> <span data-ttu-id="3ba90-115">I computer protetti possono essere ripristinati in qualsiasi punto all'interno di un intervallo.</span><span class="sxs-lookup"><span data-stu-id="3ba90-115">Protected machines can be recovered to any point within a window.</span></span>
5. <span data-ttu-id="3ba90-116">In **Frequenza snapshot coerenti con l'app**specificare la frequenza, da 1 a 12 ore, per la creazione di punti di ripristino contenenti snapshot coerenti con l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="3ba90-116">In **App-consistent snapshot frequency**, specify how frequently (1-12 hours) recovery points containing application-consistent snapshots will be created.</span></span> <span data-ttu-id="3ba90-117">Hyper-V utilizza due tipi di snapshot, uno snapshot standard che fornisce uno snapshot incrementale dell'intera macchina virtuale e uno snapshot coerente con l'applicazione che accetta uno snapshot temporizzato dei dati dell'applicazione all'interno della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3ba90-117">Hyper-V uses two types of snapshots — a standard snapshot that provides an incremental snapshot of the entire virtual machine, and an application-consistent snapshot that takes a point-in-time snapshot of the application data inside the virtual machine.</span></span> <span data-ttu-id="3ba90-118">Negli snapshot coerenti dell'applicazione viene usato il servizio Copia Shadow del volume (VSS) per garantire che le applicazioni siano coerenti durante la creazione dello snapshot.</span><span class="sxs-lookup"><span data-stu-id="3ba90-118">Application-consistent snapshots use Volume Shadow Copy Service (VSS) to ensure that applications are in a consistent state when the snapshot is taken.</span></span> <span data-ttu-id="3ba90-119">Si noti che un'eventuale abilitazione di snapshot coerenti dell'applicazione influirà sulle prestazioni delle applicazioni in esecuzione nelle macchine virtuali di origine.</span><span class="sxs-lookup"><span data-stu-id="3ba90-119">Note that if you enable application-consistent snapshots, it will affect the performance of applications running on source virtual machines.</span></span> <span data-ttu-id="3ba90-120">Assicurarsi che il valore impostato sia inferiore al numero di punti di ripristino aggiuntivi configurati.</span><span class="sxs-lookup"><span data-stu-id="3ba90-120">Ensure that the value you set is less than the number of additional recovery points you configure.</span></span>
6. <span data-ttu-id="3ba90-121">In **Ora di inizio della replica iniziale** specificare quando deve essere avviata la replica iniziale.</span><span class="sxs-lookup"><span data-stu-id="3ba90-121">In **Initial replication start time**, indicate when to start the initial replication.</span></span> <span data-ttu-id="3ba90-122">La replica avviene sulla larghezza di banda Internet. È quindi consigliabile pianificarla al di fuori dell'orario di lavoro.</span><span class="sxs-lookup"><span data-stu-id="3ba90-122">The replication occurs over your internet bandwidth so you might want to schedule it outside your busy hours.</span></span>
7. <span data-ttu-id="3ba90-123">In **Crittografare i dati archiviati in Azure**specificare se crittografare i dati inattivi in Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="3ba90-123">In **Encrypt data stored on Azure**, specify whether to encrypt at rest data in Azure storage.</span></span> <span data-ttu-id="3ba90-124">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="3ba90-124">Then click **OK**.</span></span>

    ![Criteri di replica](./media/vmm-to-azure-walkthrough-replication/gs-replication2.png)
8. <span data-ttu-id="3ba90-126">Quando si creano nuovi criteri, questi vengono associati automaticamente al cloud VMM.</span><span class="sxs-lookup"><span data-stu-id="3ba90-126">When you create a new policy it's automatically associated with the VMM cloud.</span></span> <span data-ttu-id="3ba90-127">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="3ba90-127">Click **OK**.</span></span> <span data-ttu-id="3ba90-128">È possibile associare altri cloud VMM (e le VM in essi contenute) a questi criteri di replica in **Replica** > nome del criterio > **Associate VMM Cloud (Associa cloud VMM)**.</span><span class="sxs-lookup"><span data-stu-id="3ba90-128">You can associate additional VMM clouds (and the VMs in them) with this replication policy in **Replication** > policy name > **Associate VMM Cloud**.</span></span>

    ![Criteri di replica](./media/vmm-to-azure-walkthrough-replication/policy-associate.png)



## <a name="next-steps"></a><span data-ttu-id="3ba90-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3ba90-130">Next steps</span></span>

<span data-ttu-id="3ba90-131">Andare a [Passaggio 11: Abilitare la replica](vmm-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="3ba90-131">Go to [Step 11: Enable replication](vmm-to-azure-walkthrough-enable-replication.md)</span></span>
