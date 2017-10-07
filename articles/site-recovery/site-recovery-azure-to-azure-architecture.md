---
title: aaaHow non replica macchina virtuale di Azure tra le aree di Azure di lavoro in Azure Site Recovery?  | Microsoft Docs
description: In questo articolo viene fornita una panoramica dei componenti e architettura utilizzata durante la replica delle macchine virtuali di Azure tra le aree di Azure tramite il servizio di Azure Site Recovery hello.
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/29/2017
ms.author: sujayt
ms.openlocfilehash: 01eda83e490821f8afc8a2973c18a19453a2e84a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-vm-replication-work-in-site-recovery"></a><span data-ttu-id="206e2-104">Funzionamento della replica di VM di Azure in Site Recovery</span><span class="sxs-lookup"><span data-stu-id="206e2-104">How does Azure VM replication work in Site Recovery?</span></span>


<span data-ttu-id="206e2-105">In questo articolo descrive i componenti di hello e i processi coinvolti nella replica e il ripristino delle macchine virtuali di Azure (VM) da un'area tooanother utilizzando hello [Azure Site Recovery](site-recovery-overview.md) servizio.</span><span class="sxs-lookup"><span data-stu-id="206e2-105">This article describes hello components and processes involved in replicating and recovering Azure virtual machines (VMs) from one region tooanother by using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

>[!NOTE]
><span data-ttu-id="206e2-106">Replica di macchina virtuale di Azure con hello servizio Site Recovery è attualmente in anteprima.</span><span class="sxs-lookup"><span data-stu-id="206e2-106">Azure VM replication with hello Site Recovery service is currently in preview.</span></span>

<span data-ttu-id="206e2-107">Inviare eventuali commenti nella parte inferiore di hello di questo articolo, o porre domande in hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="206e2-107">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="architectural-components"></a><span data-ttu-id="206e2-108">Componenti dell'architettura</span><span class="sxs-lookup"><span data-stu-id="206e2-108">Architectural components</span></span>

<span data-ttu-id="206e2-109">Hello seguente diagramma mostra una panoramica generale di un ambiente di macchina virtuale di Azure in un'area specifica (in questo esempio, il percorso di Stati Uniti orientali hello).</span><span class="sxs-lookup"><span data-stu-id="206e2-109">hello following diagram provides a high-level view of an Azure VM environment in a specific region (in this example, hello East US location).</span></span> <span data-ttu-id="206e2-110">In un ambiente di VM di Azure:</span><span class="sxs-lookup"><span data-stu-id="206e2-110">In an Azure VM environment:</span></span>
- <span data-ttu-id="206e2-111">Le app possono essere in esecuzione in macchine virtuali con dischi distribuiti tra gli account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="206e2-111">Apps can be running on VMs with disks spread across storage accounts.</span></span>
- <span data-ttu-id="206e2-112">Hello macchine virtuali può essere inclusi in uno o più subnet all'interno di una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="206e2-112">hello VMs can be included in one or more subnets within a virtual network.</span></span>

![customer-environment](./media/site-recovery-azure-to-azure-architecture/source-environment.png)

<span data-ttu-id="206e2-114">Informazioni sui prerequisiti per la distribuzione hello e requisiti di hello [matrice del supporto](site-recovery-support-matrix-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="206e2-114">Learn about hello deployment prerequisites and requirements in hello [support matrix](site-recovery-support-matrix-azure-to-azure.md).</span></span>

## <a name="replication-process"></a><span data-ttu-id="206e2-115">Processo di replica</span><span class="sxs-lookup"><span data-stu-id="206e2-115">Replication process</span></span>

### <a name="step-1"></a><span data-ttu-id="206e2-116">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="206e2-116">Step 1</span></span>

<span data-ttu-id="206e2-117">Quando si abilita la replica di macchina virtuale di Azure nel portale di Azure hello, hello risorse visualizzate in hello seguente diagramma e la tabella vengono creati automaticamente nell'area di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="206e2-117">When you enable Azure VM replication in hello Azure portal, hello resources shown in hello following diagram and table are automatically created in hello target region.</span></span> <span data-ttu-id="206e2-118">Per impostazione predefinita, le risorse vengono create in base alle impostazioni dell'area di origine.</span><span class="sxs-lookup"><span data-stu-id="206e2-118">By default, resources are created based on source region settings.</span></span> <span data-ttu-id="206e2-119">È possibile personalizzare le impostazioni di destinazione hello come richiesto.</span><span class="sxs-lookup"><span data-stu-id="206e2-119">You can customize hello target settings as required.</span></span> <span data-ttu-id="206e2-120">[Altre informazioni](site-recovery-replicate-azure-to-azure.md)</span><span class="sxs-lookup"><span data-stu-id="206e2-120">[Learn more](site-recovery-replicate-azure-to-azure.md).</span></span>

![Abilitare il processo di replica - Passaggio 1](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-1.png)

<span data-ttu-id="206e2-122">**Risorsa**</span><span class="sxs-lookup"><span data-stu-id="206e2-122">**Resource**</span></span> | <span data-ttu-id="206e2-123">**Dettagli**</span><span class="sxs-lookup"><span data-stu-id="206e2-123">**Details**</span></span>
--- | ---
<span data-ttu-id="206e2-124">**Gruppo di risorse di destinazione**</span><span class="sxs-lookup"><span data-stu-id="206e2-124">**Target resource group**</span></span> | <span data-ttu-id="206e2-125">Hello toowhich gruppo di risorse appartengono le macchine virtuali replicate dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="206e2-125">hello resource group toowhich replicated VMs belong after failover.</span></span>
<span data-ttu-id="206e2-126">**Rete virtuale di destinazione**</span><span class="sxs-lookup"><span data-stu-id="206e2-126">**Target virtual network**</span></span> | <span data-ttu-id="206e2-127">rete virtuale Hello in cui si trovano le macchine virtuali replicate dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="206e2-127">hello virtual network in which replicated VMs are located after failover.</span></span> <span data-ttu-id="206e2-128">Un mapping di rete viene creato tra le reti virtuali di origine e di destinazione e viceversa.</span><span class="sxs-lookup"><span data-stu-id="206e2-128">A network mapping is created between source and target virtual networks, and vice versa.</span></span>
<span data-ttu-id="206e2-129">**Account di archiviazione della cache**</span><span class="sxs-lookup"><span data-stu-id="206e2-129">**Cache storage accounts**</span></span> | <span data-ttu-id="206e2-130">Prima che le modifiche nell'origine che sono macchine virtuali replicate toohello account di archiviazione di destinazione, vengono rilevati e inviati toohello account di archiviazione della cache nel percorso di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="206e2-130">Before changes on source VMs are replicated toohello target storage account, they are tracked and sent toohello cache storage account in hello target location.</span></span> <span data-ttu-id="206e2-131">In questo modo un impatto minimo sulle app di produzione in esecuzione su hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="206e2-131">This ensures minimal impact on production apps running on hello VM.</span></span>
<span data-ttu-id="206e2-132">**Account di archiviazione di destinazione**</span><span class="sxs-lookup"><span data-stu-id="206e2-132">**Target storage accounts**</span></span>  | <span data-ttu-id="206e2-133">Gli account di archiviazione di dati di hello destinazione percorso toowhich hello viene replicata.</span><span class="sxs-lookup"><span data-stu-id="206e2-133">Storage accounts in hello target location toowhich hello data is replicated.</span></span>
<span data-ttu-id="206e2-134">**Set di disponibilità di destinazione**</span><span class="sxs-lookup"><span data-stu-id="206e2-134">**Target availability sets**</span></span>  | <span data-ttu-id="206e2-135">Set di disponibilità in cui hello replicata le macchine virtuali si trovano dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="206e2-135">Availability sets in which hello replicated VMs are located after failover.</span></span>

### <a name="step-2"></a><span data-ttu-id="206e2-136">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="206e2-136">Step 2</span></span>

<span data-ttu-id="206e2-137">Come la replica è abilitata, viene automaticamente installata hello estensione per il ripristino del sito servizio di mobilità hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="206e2-137">As replication is enabled, hello Site Recovery extension Mobility service is automatically installed on hello VM.</span></span> <span data-ttu-id="206e2-138">si verifica in seguito Hello:</span><span class="sxs-lookup"><span data-stu-id="206e2-138">hello following occurs:</span></span>

1. <span data-ttu-id="206e2-139">Hello VM è registrato con il ripristino del sito.</span><span class="sxs-lookup"><span data-stu-id="206e2-139">hello VM is registered with Site Recovery.</span></span>

2. <span data-ttu-id="206e2-140">La replica continua è configurata per hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="206e2-140">Continuous replication is configured for hello VM.</span></span> <span data-ttu-id="206e2-141">Dati scrive sul hello macchina virtuale i dischi vengono sempre trasferiti toohello account di archiviazione della cache nel percorso di origine hello.</span><span class="sxs-lookup"><span data-stu-id="206e2-141">Data writes on hello VM disks are continuously transferred toohello cache storage account in hello source location.</span></span>

   ![Abilitare il processo di replica - Passaggio 2](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-2.png)

   >[!IMPORTANT]
   > <span data-ttu-id="206e2-143">Il ripristino del sito non deve mai la connettività in ingresso toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="206e2-143">Site Recovery never needs inbound connectivity toohello VM.</span></span> <span data-ttu-id="206e2-144">Hello VM deve solo gli indirizzi URL/IP di connettività in uscita tooSite ripristino del servizio, gli indirizzi URL/IP l'autenticazione di Office 365 e gli indirizzi IP account di archiviazione della cache.</span><span class="sxs-lookup"><span data-stu-id="206e2-144">hello VM needs only outbound connectivity tooSite Recovery service URLs/IP addresses, Office 365 authentication URLs/IP addresses, and cache storage account IP addresses.</span></span> <span data-ttu-id="206e2-145">Per ulteriori informazioni, vedere hello [informazioni aggiuntive sulla rete per la replica delle macchine virtuali di Azure](site-recovery-azure-to-azure-networking-guidance.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="206e2-145">For more information, see hello [Networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md) article.</span></span>

## <a name="continuous-replication-process"></a><span data-ttu-id="206e2-146">Processo di replica continua</span><span class="sxs-lookup"><span data-stu-id="206e2-146">Continuous replication process</span></span>

<span data-ttu-id="206e2-147">Dopo che utilizza la replica continua, disco operazioni di scrittura sono immediatamente trasferito toohello account di archiviazione della cache.</span><span class="sxs-lookup"><span data-stu-id="206e2-147">After continuous replication is working, disk writes are immediately transferred toohello cache storage account.</span></span> <span data-ttu-id="206e2-148">Il ripristino del sito elabora i dati di hello e lo invia toohello account di archiviazione di destinazione.</span><span class="sxs-lookup"><span data-stu-id="206e2-148">Site Recovery processes hello data and sends it toohello target storage account.</span></span> <span data-ttu-id="206e2-149">Dopo l'elaborazione dati hello, punti di ripristino vengono generati nell'account di archiviazione di destinazione hello ogni pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="206e2-149">After hello data is processed, recovery points are generated in hello target storage account every few minutes.</span></span>

## <a name="failover-process"></a><span data-ttu-id="206e2-150">Processo di failover</span><span class="sxs-lookup"><span data-stu-id="206e2-150">Failover process</span></span>

<span data-ttu-id="206e2-151">Quando si avvia un failover, le macchine virtuali vengono create nella rete virtuale di destinazione, gruppo di risorse di destinazione hello alla subnet di destinazione hello e hello di destinazione set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="206e2-151">When you initiate a failover, hello VMs are created in hello target resource group, target virtual network, target subnet, and hello target availability set.</span></span> <span data-ttu-id="206e2-152">Durante un failover è possibile usare qualsiasi punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="206e2-152">During a failover, you can use any recovery point.</span></span>

![Processo di failover](./media/site-recovery-azure-to-azure-architecture/failover.png)

## <a name="next-steps"></a><span data-ttu-id="206e2-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="206e2-154">Next steps</span></span>

- <span data-ttu-id="206e2-155">Altre informazioni sulle [risorse di rete](site-recovery-azure-to-azure-networking-guidance.md) per la replica di VM di Azure.</span><span class="sxs-lookup"><span data-stu-id="206e2-155">Learn about [networking](site-recovery-azure-to-azure-networking-guidance.md) for Azure VM replication.</span></span>
- <span data-ttu-id="206e2-156">Seguire una procedura dettagliata troppo[replicare macchine virtuali di Azure.](site-recovery-azure-to-azure.md)</span><span class="sxs-lookup"><span data-stu-id="206e2-156">Follow a walkthrough too[replicate Azure VMs.](site-recovery-azure-to-azure.md)</span></span>
