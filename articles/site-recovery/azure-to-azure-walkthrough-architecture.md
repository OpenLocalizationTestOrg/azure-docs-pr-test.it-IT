---
title: Esaminare l'architettura per la replica di VM di Azure tra aree di Azure | Microsoft Docs
description: Questo articolo offre una panoramica dei componenti e dell'architettura usati per la replica di VM di Azure tra aree di Azure con il servizio Azure Site Recovery.
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
ms.openlocfilehash: f471add4f4dee26482e2820fb06d010d6c0c0e88
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="step-1-review-the-architecture-for-azure-vm-replication-between-azure-regions"></a><span data-ttu-id="0628b-103">Passaggio 1: Esaminare l'architettura per la replica di VM di Azure tra aree di Azure</span><span class="sxs-lookup"><span data-stu-id="0628b-103">Step 1: Review the architecture for Azure VM replication between Azure regions</span></span>


<span data-ttu-id="0628b-104">Dopo aver esaminato i [passaggi elencati nella panoramica](azure-to-azure-walkthrough-overview.md) per questa distribuzione, questo articolo consente di conoscere i componenti e i processi usati per la replica e il ripristino di macchine virtuali (VM) di Azure da un'area di Azure a un'altra con [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0628b-104">After reviewing the [overview steps](azure-to-azure-walkthrough-overview.md) for this deployment, read this article to understand the components and processes used when replicating and recovering Azure virtual machines (VMs) from one Azure region to another, using [Azure Site Recovery](site-recovery-overview.md).</span></span>

- <span data-ttu-id="0628b-105">Al termine dell'articolo, si avrà una conoscenza precisa del funzionamento della replica di VM in un'altra area.</span><span class="sxs-lookup"><span data-stu-id="0628b-105">When you finish the article, you should have a clear understanding of how Azure VM replication to another region works.</span></span>
- <span data-ttu-id="0628b-106">È possibile inserire commenti alla fine di questo articolo oppure porre domande nel [forum sui Servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="0628b-106">Post any comments at the bottom of this article, or ask questions in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

>[!NOTE]
><span data-ttu-id="0628b-107">La replica di VM di Azure con il servizio Site Recovery è attualmente disponibile in anteprima.</span><span class="sxs-lookup"><span data-stu-id="0628b-107">Azure VM replication with the Site Recovery service is currently in preview.</span></span>



## <a name="architectural-components"></a><span data-ttu-id="0628b-108">Componenti dell'architettura</span><span class="sxs-lookup"><span data-stu-id="0628b-108">Architectural components</span></span>

<span data-ttu-id="0628b-109">Il diagramma seguente fornisce una visualizzazione generale di un ambiente di VM di Azure in un'area specifica. In questo esempio si tratta dell'area Stati Uniti orientali.</span><span class="sxs-lookup"><span data-stu-id="0628b-109">The following diagram provides a high-level view of an Azure VM environment in a specific region (in this example, the East US location).</span></span> <span data-ttu-id="0628b-110">In un ambiente di VM di Azure:</span><span class="sxs-lookup"><span data-stu-id="0628b-110">In an Azure VM environment:</span></span>
- <span data-ttu-id="0628b-111">Le app possono essere in esecuzione in macchine virtuali con dischi distribuiti tra gli account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="0628b-111">Apps can be running on VMs with disks spread across storage accounts.</span></span>
- <span data-ttu-id="0628b-112">Le VM possono essere incluse in una o più subnet in una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="0628b-112">The VMs can be included in one or more subnets within a virtual network.</span></span>

![customer-environment](./media/azure-to-azure-walkthrough-architecture/source-environment.png)

## <a name="replication-process"></a><span data-ttu-id="0628b-114">Processo di replica</span><span class="sxs-lookup"><span data-stu-id="0628b-114">Replication process</span></span>

### <a name="step-1"></a><span data-ttu-id="0628b-115">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="0628b-115">Step 1</span></span>

<span data-ttu-id="0628b-116">Quando si abilita la replica di VM di Azure nel portale di Azure, le risorse visualizzate nel diagramma e nella tabella seguenti vengono create automaticamente nell'area di destinazione.</span><span class="sxs-lookup"><span data-stu-id="0628b-116">When you enable Azure VM replication in the Azure portal, the resources shown in the following diagram and table are automatically created in the target region.</span></span> <span data-ttu-id="0628b-117">Per impostazione predefinita, le risorse vengono create in base alle impostazioni dell'area di origine.</span><span class="sxs-lookup"><span data-stu-id="0628b-117">By default, resources are created based on source region settings.</span></span> <span data-ttu-id="0628b-118">È possibile personalizzare le impostazioni di destinazione in base alle esigenze specifiche.</span><span class="sxs-lookup"><span data-stu-id="0628b-118">You can customize the target settings as required.</span></span> <span data-ttu-id="0628b-119">[Altre informazioni](site-recovery-replicate-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="0628b-119">[Learn more](site-recovery-replicate-azure-to-azure.md).</span></span>

![Abilitare il processo di replica - Passaggio 1](./media/azure-to-azure-walkthrough-architecture/enable-replication-step-1.png)

<span data-ttu-id="0628b-121">**Risorsa**</span><span class="sxs-lookup"><span data-stu-id="0628b-121">**Resource**</span></span> | <span data-ttu-id="0628b-122">**Dettagli**</span><span class="sxs-lookup"><span data-stu-id="0628b-122">**Details**</span></span>
--- | ---
<span data-ttu-id="0628b-123">**Gruppo di risorse di destinazione**</span><span class="sxs-lookup"><span data-stu-id="0628b-123">**Target resource group**</span></span> | <span data-ttu-id="0628b-124">Gruppo di risorse a cui appartengono le VM replicate dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="0628b-124">The resource group to which replicated VMs belong after failover.</span></span>
<span data-ttu-id="0628b-125">**Rete virtuale di destinazione**</span><span class="sxs-lookup"><span data-stu-id="0628b-125">**Target virtual network**</span></span> | <span data-ttu-id="0628b-126">Rete virtuale in cui si trovano le VM replicate dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="0628b-126">The virtual network in which replicated VMs are located after failover.</span></span> <span data-ttu-id="0628b-127">Un mapping di rete viene creato tra le reti virtuali di origine e di destinazione e viceversa.</span><span class="sxs-lookup"><span data-stu-id="0628b-127">A network mapping is created between source and target virtual networks, and vice versa.</span></span>
<span data-ttu-id="0628b-128">**Account di archiviazione della cache**</span><span class="sxs-lookup"><span data-stu-id="0628b-128">**Cache storage accounts**</span></span> | <span data-ttu-id="0628b-129">Prima che le modifiche apportate nelle VM di origine vengano replicate nell'account di archiviazione di destinazione, vengono registrate e inviate all'account di archiviazione della cache nel percorso di destinazione.</span><span class="sxs-lookup"><span data-stu-id="0628b-129">Before changes on source VMs are replicated to the target storage account, they are tracked and sent to the cache storage account in the target location.</span></span> <span data-ttu-id="0628b-130">In questo modo si assicura un impatto minimo sulle app di produzione in esecuzione nella VM.</span><span class="sxs-lookup"><span data-stu-id="0628b-130">This ensures minimal impact on production apps running on the VM.</span></span>
<span data-ttu-id="0628b-131">**Account di archiviazione di destinazione**</span><span class="sxs-lookup"><span data-stu-id="0628b-131">**Target storage accounts**</span></span>  | <span data-ttu-id="0628b-132">Account di archiviazione nel percorso di destinazione in cui vengono replicati i dati.</span><span class="sxs-lookup"><span data-stu-id="0628b-132">Storage accounts in the target location to which the data is replicated.</span></span>
<span data-ttu-id="0628b-133">**Set di disponibilità di destinazione**</span><span class="sxs-lookup"><span data-stu-id="0628b-133">**Target availability sets**</span></span>  | <span data-ttu-id="0628b-134">Set di disponibilità in cui si trovano le VM replicate dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="0628b-134">Availability sets in which the replicated VMs are located after failover.</span></span>

### <a name="step-2"></a><span data-ttu-id="0628b-135">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="0628b-135">Step 2</span></span>

<span data-ttu-id="0628b-136">Poiché la replica è abilitata, il servizio Mobility dell'estensione di Site Recovery viene installato automaticamente nella VM.</span><span class="sxs-lookup"><span data-stu-id="0628b-136">As replication is enabled, the Site Recovery extension Mobility service is automatically installed on the VM.</span></span> <span data-ttu-id="0628b-137">Vengono eseguite le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="0628b-137">The following occurs:</span></span>

1. <span data-ttu-id="0628b-138">La VM viene registrata in Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="0628b-138">The VM is registered with Site Recovery.</span></span>

2. <span data-ttu-id="0628b-139">La replica continua viene configurata per la VM.</span><span class="sxs-lookup"><span data-stu-id="0628b-139">Continuous replication is configured for the VM.</span></span> <span data-ttu-id="0628b-140">Le operazioni di scrittura di dati nei dischi delle VM vengono trasferite continuamente nell'account di archiviazione della cache nel percorso di origine.</span><span class="sxs-lookup"><span data-stu-id="0628b-140">Data writes on the VM disks are continuously transferred to the cache storage account in the source location.</span></span>

   ![Abilitare il processo di replica - Passaggio 2](./media/azure-to-azure-walkthrough-architecture/enable-replication-step-2.png)

  
  <span data-ttu-id="0628b-142">Si noti che Site Recovery non necessita mai della connettività in ingresso per la VM.</span><span class="sxs-lookup"><span data-stu-id="0628b-142">Note that Site Recovery never needs inbound connectivity to the VM.</span></span> <span data-ttu-id="0628b-143">È necessaria solo la connettività in uscita agli URL/indirizzi IP del servizio Site Recovery, agli URL/indirizzi IP di autenticazione di Office 365 e agli indirizzi IP dell'account di archiviazione della cache.</span><span class="sxs-lookup"><span data-stu-id="0628b-143">Only outbound connectivity to Site Recovery service URLs/IP addresses, Office 365 authentication URLs/IP addresses, and cache storage account IP addresses is needed.</span></span> 

## <a name="continuous-replication-process"></a><span data-ttu-id="0628b-144">Processo di replica continua</span><span class="sxs-lookup"><span data-stu-id="0628b-144">Continuous replication process</span></span>

<span data-ttu-id="0628b-145">Quando la replica continua è attivata correttamente, le operazioni di scrittura nei dischi vengono trasferite immediatamente nell'account di archiviazione della cache.</span><span class="sxs-lookup"><span data-stu-id="0628b-145">After continuous replication is working, disk writes are immediately transferred to the cache storage account.</span></span> <span data-ttu-id="0628b-146">Site Recovery elabora i dati e li invia all'account di archiviazione di destinazione.</span><span class="sxs-lookup"><span data-stu-id="0628b-146">Site Recovery processes the data and sends it to the target storage account.</span></span> <span data-ttu-id="0628b-147">Dopo l'elaborazione dei dati, vengono generati punti di ripristino nell'account di archiviazione di destinazione a intervalli di pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="0628b-147">After the data is processed, recovery points are generated in the target storage account every few minutes.</span></span>

## <a name="failover-process"></a><span data-ttu-id="0628b-148">Processo di failover</span><span class="sxs-lookup"><span data-stu-id="0628b-148">Failover process</span></span>

<span data-ttu-id="0628b-149">Quando si avvia un failover, le VM vengono create nel gruppo di risorse di destinazione, nella rete virtuale di destinazione, nella subnet di destinazione e nel set di disponibilità di destinazione.</span><span class="sxs-lookup"><span data-stu-id="0628b-149">When you initiate a failover, the VMs are created in the target resource group, target virtual network, target subnet, and the target availability set.</span></span> <span data-ttu-id="0628b-150">Durante un failover è possibile usare qualsiasi punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="0628b-150">During a failover, you can use any recovery point.</span></span>

![Processo di failover](./media/azure-to-azure-walkthrough-architecture/failover.png)

## <a name="next-steps"></a><span data-ttu-id="0628b-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0628b-152">Next steps</span></span>

<span data-ttu-id="0628b-153">Andare a [Passaggio 2: Esaminare i prerequisiti e le limitazioni](azure-to-azure-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="0628b-153">Go to [Step 2: Verify prerequisites and limitations](azure-to-azure-walkthrough-prerequisites.md)</span></span>
