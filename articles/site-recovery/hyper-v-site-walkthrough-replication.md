---
title: Configurare i criteri di replica per la replica di VM Hyper-V (senza System Center VMM) in Azure con Azure Site Recovery | Microsoft Docs
description: Vengono riepilogati i passaggi necessari per configurare criteri di replica per la replica di VM Hyper-V in Archiviazione di Azure
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
ms.openlocfilehash: ca5bec5cf1152e6259b9fe7a869edd2d62b88e1a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="step-9-set-up-a-replication-policy-for-hyper-v-vm-replication-to-azure"></a><span data-ttu-id="af6c9-103">Passaggio 9: Configurare criteri di replica per la replica di VM Hyper-V in Azure</span><span class="sxs-lookup"><span data-stu-id="af6c9-103">Step 9: Set up a replication policy for Hyper-V VM replication to Azure</span></span>

<span data-ttu-id="af6c9-104">Questo articolo illustra come configurare criteri di replica quando si esegue la replica di VM Hyper-V in Azure (senza System Center VMM) usando il servizio [Azure Site Recovery](site-recovery-overview.md) nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="af6c9-104">This article describes how to set up a replication policy when you're replicating Hyper-V VMs to Azure (without System Center VMM) using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


<span data-ttu-id="af6c9-105">Inserire commenti e domande nella parte inferiore di questo articolo oppure nel [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="af6c9-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="about-snapshots"></a><span data-ttu-id="af6c9-106">Informazioni sugli snapshot</span><span class="sxs-lookup"><span data-stu-id="af6c9-106">About snapshots</span></span>

<span data-ttu-id="af6c9-107">Hyper-V utilizza due tipi di snapshot, uno snapshot standard che fornisce uno snapshot incrementale dell'intera macchina virtuale e uno snapshot coerente con l'applicazione che accetta uno snapshot temporizzato dei dati dell'applicazione all'interno della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="af6c9-107">Hyper-V uses two types of snapshots — a standard snapshot that provides an incremental snapshot of the entire virtual machine, and an application-consistent snapshot that takes a point-in-time snapshot of the application data inside the virtual machine.</span></span>
    - <span data-ttu-id="af6c9-108">Negli snapshot coerenti dell'applicazione viene usato il servizio Copia Shadow del volume (VSS) per garantire che le applicazioni siano coerenti durante la creazione dello snapshot.</span><span class="sxs-lookup"><span data-stu-id="af6c9-108">Application-consistent snapshots use Volume Shadow Copy Service (VSS) to ensure that applications are in a consistent state when the snapshot is taken.</span></span>
    - <span data-ttu-id="af6c9-109">L'abilitazione di snapshot coerenti con l'applicazione influirà sulle prestazioni delle applicazioni in esecuzione nelle macchine virtuali di origine.</span><span class="sxs-lookup"><span data-stu-id="af6c9-109">If you enable application-consistent snapshots, it will affect the performance of applications running on source virtual machines.</span></span> <span data-ttu-id="af6c9-110">Assicurarsi che il valore impostato sia inferiore al numero di punti di ripristino aggiuntivi configurati.</span><span class="sxs-lookup"><span data-stu-id="af6c9-110">Ensure that the value you set is less than the number of additional recovery points you configure.</span></span>

## <a name="set-up-a-replication-policy"></a><span data-ttu-id="af6c9-111">Configurare criteri di replica</span><span class="sxs-lookup"><span data-stu-id="af6c9-111">Set up a replication policy</span></span>

1. <span data-ttu-id="af6c9-112">Per creare nuovi criteri di replica, fare clic su **Preparare l'infrastruttura** > **Impostazioni della replica** > **+Crea e associa**.</span><span class="sxs-lookup"><span data-stu-id="af6c9-112">To create a new replication policy, click **Prepare infrastructure** > **Replication Settings** > **+Create and associate**.</span></span>

    ![Rete](./media/hyper-v-site-walkthrough-replication/gs-replication.png)
2. <span data-ttu-id="af6c9-114">In **Criteri di creazione e associazione**specificare il nome dei criteri.</span><span class="sxs-lookup"><span data-stu-id="af6c9-114">In **Create and associate policy**, specify a policy name.</span></span>
3. <span data-ttu-id="af6c9-115">In **Frequenza di copia**specificare la frequenza con cui replicare i dati differenziali dopo la replica iniziale, ogni 30 secondi oppure ogni 5 o 15 minuti.</span><span class="sxs-lookup"><span data-stu-id="af6c9-115">In **Copy frequency**, specify how often you want to replicate delta data after the initial replication (every 30 seconds, 5 or 15 minutes).</span></span>

    > [!NOTE]
    > <span data-ttu-id="af6c9-116">Quando si esegue la replica in archiviazione Premium la frequenza di 30 secondi non è supportata.</span><span class="sxs-lookup"><span data-stu-id="af6c9-116">A 30 second frequency isn't supported when replicating to premium storage.</span></span> <span data-ttu-id="af6c9-117">Il limite è determinato dal numero di snapshot per BLOB (100) supportato dal servizio di archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="af6c9-117">The limitation is determined by the number of snapshots per blob (100) supported by premium storage.</span></span> <span data-ttu-id="af6c9-118">[Altre informazioni](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob).</span><span class="sxs-lookup"><span data-stu-id="af6c9-118">[Learn more](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob).</span></span>

4. <span data-ttu-id="af6c9-119">In **Conservazione del punto di recupero** specificare la durata in ore dell'intervallo di conservazione per ogni punto di recupero.</span><span class="sxs-lookup"><span data-stu-id="af6c9-119">In **Recovery point retention**, specify in hours how long the retention window is for each recovery point.</span></span> <span data-ttu-id="af6c9-120">Le macchine virtuali possono essere ripristinate in qualsiasi punto all'interno di un intervallo.</span><span class="sxs-lookup"><span data-stu-id="af6c9-120">VMs can be recovered to any point within a window.</span></span>
5. <span data-ttu-id="af6c9-121">In **Frequenza snapshot coerenti con l'app** specificare la frequenza, da 1 a 12 ore, per la creazione di punti di ripristino contenenti snapshot coerenti con l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="af6c9-121">In **App-consistent snapshot frequency**, specify how frequently (1-12 hours) recovery points containing application-consistent snapshots are created.</span></span>
6. <span data-ttu-id="af6c9-122">In **Ora di inizio della replica iniziale** specificare quando deve essere avviata la replica iniziale.</span><span class="sxs-lookup"><span data-stu-id="af6c9-122">In **Initial replication start time**, specify when to start the initial replication.</span></span> <span data-ttu-id="af6c9-123">La replica avviene sulla larghezza di banda Internet. È quindi consigliabile pianificarla al di fuori dell'orario di lavoro.</span><span class="sxs-lookup"><span data-stu-id="af6c9-123">The replication occurs over your internet bandwidth so you might want to schedule it outside your busy hours.</span></span> <span data-ttu-id="af6c9-124">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="af6c9-124">Then click **OK**.</span></span>

    ![Criteri di replica](./media/hyper-v-site-walkthrough-replication/gs-replication2.png)

<span data-ttu-id="af6c9-126">Quando si creano nuovi criteri, questi vengono associati automaticamente al sito Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="af6c9-126">When you create a new policy, it's automatically associated with the Hyper-V site.</span></span> <span data-ttu-id="af6c9-127">È possibile associare un sito Hyper-V e le VM che contiene a più criteri di replica in **Replica** > nome-criteri > **Associate Hyper-V Site** (Associa sito Hyper-V).</span><span class="sxs-lookup"><span data-stu-id="af6c9-127">You can associate a Hyper-V site (and the VMs in it) with multiple replication policies in **Replication** > policy-name > **Associate Hyper-V Site**.</span></span>



## <a name="next-steps"></a><span data-ttu-id="af6c9-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="af6c9-128">Next steps</span></span>

<span data-ttu-id="af6c9-129">Andare a [Passaggio 10: Abilitare la replica](hyper-v-site-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="af6c9-129">Go to [Step 10: Enable replication](hyper-v-site-walkthrough-enable-replication.md)</span></span>
