---
title: architettura di hello aaaReview per la replica delle macchine virtuali di Azure tra le aree di Azure | Documenti Microsoft
description: In questo articolo viene fornita una panoramica dei componenti e architettura utilizzata durante la replica delle macchine virtuali di Azure tra le aree di Azure tramite il servizio di Azure Site Recovery hello.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/12/2017
ms.author: raynew
ms.openlocfilehash: 4caab4e7a764040f317201d1345c40c73f836d81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-azure-vm-replication-between-azure-regions"></a><span data-ttu-id="b898f-103">Passaggio 1: Esaminare l'architettura di hello per la replica di macchina virtuale di Azure tra le aree di Azure</span><span class="sxs-lookup"><span data-stu-id="b898f-103">Step 1: Review hello architecture for Azure VM replication between Azure regions</span></span>


<span data-ttu-id="b898f-104">Dopo aver esaminato hello [passaggi Panoramica](azure-to-azure-walkthrough-overview.md) per questa distribuzione, leggere questo componenti hello toounderstand di articolo e processi utilizzati quando si esegue la replica e il ripristino delle macchine virtuali di Azure (VM) da un'area di Azure tooanother, utilizzando [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b898f-104">After reviewing hello [overview steps](azure-to-azure-walkthrough-overview.md) for this deployment, read this article toounderstand hello components and processes used when replicating and recovering Azure virtual machines (VMs) from one Azure region tooanother, using [Azure Site Recovery](site-recovery-overview.md).</span></span>

- <span data-ttu-id="b898f-105">Dopo aver articolo hello, è necessario comprendere a fondo il funzionamento area tooanother replica di macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b898f-105">When you finish hello article, you should have a clear understanding of how Azure VM replication tooanother region works.</span></span>
- <span data-ttu-id="b898f-106">Inviare eventuali commenti nella parte inferiore di hello di questo articolo, o porre domande in hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="b898f-106">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

>[!NOTE]
><span data-ttu-id="b898f-107">Replica di macchina virtuale di Azure con hello servizio Site Recovery è attualmente in anteprima.</span><span class="sxs-lookup"><span data-stu-id="b898f-107">Azure VM replication with hello Site Recovery service is currently in preview.</span></span>



## <a name="architectural-components"></a><span data-ttu-id="b898f-108">Componenti dell'architettura</span><span class="sxs-lookup"><span data-stu-id="b898f-108">Architectural components</span></span>

<span data-ttu-id="b898f-109">Hello seguente diagramma mostra una panoramica generale di un ambiente di macchina virtuale di Azure in un'area specifica (in questo esempio, il percorso di Stati Uniti orientali hello).</span><span class="sxs-lookup"><span data-stu-id="b898f-109">hello following diagram provides a high-level view of an Azure VM environment in a specific region (in this example, hello East US location).</span></span> <span data-ttu-id="b898f-110">In un ambiente di VM di Azure:</span><span class="sxs-lookup"><span data-stu-id="b898f-110">In an Azure VM environment:</span></span>
- <span data-ttu-id="b898f-111">Le app possono essere in esecuzione in macchine virtuali con dischi distribuiti tra gli account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b898f-111">Apps can be running on VMs with disks spread across storage accounts.</span></span>
- <span data-ttu-id="b898f-112">Hello macchine virtuali può essere inclusi in uno o più subnet all'interno di una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="b898f-112">hello VMs can be included in one or more subnets within a virtual network.</span></span>

![customer-environment](./media/azure-to-azure-walkthrough-architecture/source-environment.png)

## <a name="replication-process"></a><span data-ttu-id="b898f-114">Processo di replica</span><span class="sxs-lookup"><span data-stu-id="b898f-114">Replication process</span></span>

### <a name="step-1"></a><span data-ttu-id="b898f-115">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="b898f-115">Step 1</span></span>

<span data-ttu-id="b898f-116">Quando si abilita la replica di macchina virtuale di Azure nel portale di Azure hello, hello risorse visualizzate in hello seguente diagramma e la tabella vengono creati automaticamente nell'area di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="b898f-116">When you enable Azure VM replication in hello Azure portal, hello resources shown in hello following diagram and table are automatically created in hello target region.</span></span> <span data-ttu-id="b898f-117">Per impostazione predefinita, le risorse vengono create in base alle impostazioni dell'area di origine.</span><span class="sxs-lookup"><span data-stu-id="b898f-117">By default, resources are created based on source region settings.</span></span> <span data-ttu-id="b898f-118">È possibile personalizzare le impostazioni di destinazione hello come richiesto.</span><span class="sxs-lookup"><span data-stu-id="b898f-118">You can customize hello target settings as required.</span></span> <span data-ttu-id="b898f-119">[Altre informazioni](site-recovery-replicate-azure-to-azure.md)</span><span class="sxs-lookup"><span data-stu-id="b898f-119">[Learn more](site-recovery-replicate-azure-to-azure.md).</span></span>

![Abilitare il processo di replica - Passaggio 1](./media/azure-to-azure-walkthrough-architecture/enable-replication-step-1.png)

<span data-ttu-id="b898f-121">**Risorsa**</span><span class="sxs-lookup"><span data-stu-id="b898f-121">**Resource**</span></span> | <span data-ttu-id="b898f-122">**Dettagli**</span><span class="sxs-lookup"><span data-stu-id="b898f-122">**Details**</span></span>
--- | ---
<span data-ttu-id="b898f-123">**Gruppo di risorse di destinazione**</span><span class="sxs-lookup"><span data-stu-id="b898f-123">**Target resource group**</span></span> | <span data-ttu-id="b898f-124">Hello toowhich gruppo di risorse appartengono le macchine virtuali replicate dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="b898f-124">hello resource group toowhich replicated VMs belong after failover.</span></span>
<span data-ttu-id="b898f-125">**Rete virtuale di destinazione**</span><span class="sxs-lookup"><span data-stu-id="b898f-125">**Target virtual network**</span></span> | <span data-ttu-id="b898f-126">rete virtuale Hello in cui si trovano le macchine virtuali replicate dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="b898f-126">hello virtual network in which replicated VMs are located after failover.</span></span> <span data-ttu-id="b898f-127">Un mapping di rete viene creato tra le reti virtuali di origine e di destinazione e viceversa.</span><span class="sxs-lookup"><span data-stu-id="b898f-127">A network mapping is created between source and target virtual networks, and vice versa.</span></span>
<span data-ttu-id="b898f-128">**Account di archiviazione della cache**</span><span class="sxs-lookup"><span data-stu-id="b898f-128">**Cache storage accounts**</span></span> | <span data-ttu-id="b898f-129">Prima che le modifiche nell'origine che sono macchine virtuali replicate toohello account di archiviazione di destinazione, vengono rilevati e inviati toohello account di archiviazione della cache nel percorso di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="b898f-129">Before changes on source VMs are replicated toohello target storage account, they are tracked and sent toohello cache storage account in hello target location.</span></span> <span data-ttu-id="b898f-130">In questo modo un impatto minimo sulle app di produzione in esecuzione su hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b898f-130">This ensures minimal impact on production apps running on hello VM.</span></span>
<span data-ttu-id="b898f-131">**Account di archiviazione di destinazione**</span><span class="sxs-lookup"><span data-stu-id="b898f-131">**Target storage accounts**</span></span>  | <span data-ttu-id="b898f-132">Gli account di archiviazione di dati di hello destinazione percorso toowhich hello viene replicata.</span><span class="sxs-lookup"><span data-stu-id="b898f-132">Storage accounts in hello target location toowhich hello data is replicated.</span></span>
<span data-ttu-id="b898f-133">**Set di disponibilità di destinazione**</span><span class="sxs-lookup"><span data-stu-id="b898f-133">**Target availability sets**</span></span>  | <span data-ttu-id="b898f-134">Set di disponibilità in cui hello replicata le macchine virtuali si trovano dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="b898f-134">Availability sets in which hello replicated VMs are located after failover.</span></span>

### <a name="step-2"></a><span data-ttu-id="b898f-135">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="b898f-135">Step 2</span></span>

<span data-ttu-id="b898f-136">Come la replica è abilitata, viene automaticamente installata hello estensione per il ripristino del sito servizio di mobilità hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b898f-136">As replication is enabled, hello Site Recovery extension Mobility service is automatically installed on hello VM.</span></span> <span data-ttu-id="b898f-137">si verifica in seguito Hello:</span><span class="sxs-lookup"><span data-stu-id="b898f-137">hello following occurs:</span></span>

1. <span data-ttu-id="b898f-138">Hello VM è registrato con il ripristino del sito.</span><span class="sxs-lookup"><span data-stu-id="b898f-138">hello VM is registered with Site Recovery.</span></span>

2. <span data-ttu-id="b898f-139">La replica continua è configurata per hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b898f-139">Continuous replication is configured for hello VM.</span></span> <span data-ttu-id="b898f-140">Dati scrive sul hello macchina virtuale i dischi vengono sempre trasferiti toohello account di archiviazione della cache nel percorso di origine hello.</span><span class="sxs-lookup"><span data-stu-id="b898f-140">Data writes on hello VM disks are continuously transferred toohello cache storage account in hello source location.</span></span>

   ![Abilitare il processo di replica - Passaggio 2](./media/azure-to-azure-walkthrough-architecture/enable-replication-step-2.png)

  
  <span data-ttu-id="b898f-142">Si noti che il ripristino del sito non deve mai in ingresso connettività toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b898f-142">Note that Site Recovery never needs inbound connectivity toohello VM.</span></span> <span data-ttu-id="b898f-143">Solo in uscita indirizzi URL/IP di servizio di integrazione applicativa tooSite ripristino, l'autenticazione di Office 365 URL/e gli indirizzi IP, indirizzi IP account di archiviazione della cache è necessaria.</span><span class="sxs-lookup"><span data-stu-id="b898f-143">Only outbound connectivity tooSite Recovery service URLs/IP addresses, Office 365 authentication URLs/IP addresses, and cache storage account IP addresses is needed.</span></span> 

## <a name="continuous-replication-process"></a><span data-ttu-id="b898f-144">Processo di replica continua</span><span class="sxs-lookup"><span data-stu-id="b898f-144">Continuous replication process</span></span>

<span data-ttu-id="b898f-145">Dopo che utilizza la replica continua, disco operazioni di scrittura sono immediatamente trasferito toohello account di archiviazione della cache.</span><span class="sxs-lookup"><span data-stu-id="b898f-145">After continuous replication is working, disk writes are immediately transferred toohello cache storage account.</span></span> <span data-ttu-id="b898f-146">Il ripristino del sito elabora i dati di hello e lo invia toohello account di archiviazione di destinazione.</span><span class="sxs-lookup"><span data-stu-id="b898f-146">Site Recovery processes hello data and sends it toohello target storage account.</span></span> <span data-ttu-id="b898f-147">Dopo l'elaborazione dati hello, punti di ripristino vengono generati nell'account di archiviazione di destinazione hello ogni pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="b898f-147">After hello data is processed, recovery points are generated in hello target storage account every few minutes.</span></span>

## <a name="failover-process"></a><span data-ttu-id="b898f-148">Processo di failover</span><span class="sxs-lookup"><span data-stu-id="b898f-148">Failover process</span></span>

<span data-ttu-id="b898f-149">Quando si avvia un failover, le macchine virtuali vengono create nella rete virtuale di destinazione, gruppo di risorse di destinazione hello alla subnet di destinazione hello e hello di destinazione set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="b898f-149">When you initiate a failover, hello VMs are created in hello target resource group, target virtual network, target subnet, and hello target availability set.</span></span> <span data-ttu-id="b898f-150">Durante un failover è possibile usare qualsiasi punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="b898f-150">During a failover, you can use any recovery point.</span></span>

![Processo di failover](./media/azure-to-azure-walkthrough-architecture/failover.png)

## <a name="next-steps"></a><span data-ttu-id="b898f-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b898f-152">Next steps</span></span>

<span data-ttu-id="b898f-153">Andare troppo[passaggio 2: verificare i prerequisiti e limitazioni](azure-to-azure-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="b898f-153">Go too[Step 2: Verify prerequisites and limitations](azure-to-azure-walkthrough-prerequisites.md)</span></span>
