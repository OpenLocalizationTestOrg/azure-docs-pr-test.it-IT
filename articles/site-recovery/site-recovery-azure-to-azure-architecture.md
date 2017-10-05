---
title: Funzionamento della replica di macchine virtuali di Azure tra aree di Azure in Azure Site Recovery  | Microsoft Docs
description: Questo articolo fornisce una panoramica dei componenti e dell'architettura usati durante la replica di VM di Azure tra aree di Azure tramite il servizio Azure Site Recovery.
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
ms.openlocfilehash: ec397eaeda963f257d1bd996f1f57189bcde17ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-does-azure-vm-replication-work-in-site-recovery"></a><span data-ttu-id="2a75d-104">Funzionamento della replica di VM di Azure in Site Recovery</span><span class="sxs-lookup"><span data-stu-id="2a75d-104">How does Azure VM replication work in Site Recovery?</span></span>


<span data-ttu-id="2a75d-105">Questo articolo illustra i componenti e i processi interessati dalla replica e dal ripristino delle macchine virtuali di Azure da un'area all'altra tramite il servizio [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2a75d-105">This article describes the components and processes involved in replicating and recovering Azure virtual machines (VMs) from one region to another by using the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

>[!NOTE]
><span data-ttu-id="2a75d-106">La replica di VM di Azure con il servizio Site Recovery è attualmente disponibile in anteprima.</span><span class="sxs-lookup"><span data-stu-id="2a75d-106">Azure VM replication with the Site Recovery service is currently in preview.</span></span>

<span data-ttu-id="2a75d-107">È possibile inserire commenti alla fine di questo articolo oppure porre domande nel [forum sui Servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="2a75d-107">Post any comments at the bottom of this article, or ask questions in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="architectural-components"></a><span data-ttu-id="2a75d-108">Componenti dell'architettura</span><span class="sxs-lookup"><span data-stu-id="2a75d-108">Architectural components</span></span>

<span data-ttu-id="2a75d-109">Il diagramma seguente fornisce una visualizzazione generale di un ambiente di VM di Azure in un'area specifica. In questo esempio si tratta dell'area Stati Uniti orientali.</span><span class="sxs-lookup"><span data-stu-id="2a75d-109">The following diagram provides a high-level view of an Azure VM environment in a specific region (in this example, the East US location).</span></span> <span data-ttu-id="2a75d-110">In un ambiente di VM di Azure:</span><span class="sxs-lookup"><span data-stu-id="2a75d-110">In an Azure VM environment:</span></span>
- <span data-ttu-id="2a75d-111">Le app possono essere in esecuzione in macchine virtuali con dischi distribuiti tra gli account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="2a75d-111">Apps can be running on VMs with disks spread across storage accounts.</span></span>
- <span data-ttu-id="2a75d-112">Le VM possono essere incluse in una o più subnet in una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="2a75d-112">The VMs can be included in one or more subnets within a virtual network.</span></span>

![customer-environment](./media/site-recovery-azure-to-azure-architecture/source-environment.png)

<span data-ttu-id="2a75d-114">Informazioni sui prerequisiti di distribuzione e i requisiti sono disponibili nella [matrice di supporto](site-recovery-support-matrix-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="2a75d-114">Learn about the deployment prerequisites and requirements in the [support matrix](site-recovery-support-matrix-azure-to-azure.md).</span></span>

## <a name="replication-process"></a><span data-ttu-id="2a75d-115">Processo di replica</span><span class="sxs-lookup"><span data-stu-id="2a75d-115">Replication process</span></span>

### <a name="step-1"></a><span data-ttu-id="2a75d-116">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="2a75d-116">Step 1</span></span>

<span data-ttu-id="2a75d-117">Quando si abilita la replica di VM di Azure nel portale di Azure, le risorse visualizzate nel diagramma e nella tabella seguenti vengono create automaticamente nell'area di destinazione.</span><span class="sxs-lookup"><span data-stu-id="2a75d-117">When you enable Azure VM replication in the Azure portal, the resources shown in the following diagram and table are automatically created in the target region.</span></span> <span data-ttu-id="2a75d-118">Per impostazione predefinita, le risorse vengono create in base alle impostazioni dell'area di origine.</span><span class="sxs-lookup"><span data-stu-id="2a75d-118">By default, resources are created based on source region settings.</span></span> <span data-ttu-id="2a75d-119">È possibile personalizzare le impostazioni di destinazione in base alle esigenze specifiche.</span><span class="sxs-lookup"><span data-stu-id="2a75d-119">You can customize the target settings as required.</span></span> <span data-ttu-id="2a75d-120">[Altre informazioni](site-recovery-replicate-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="2a75d-120">[Learn more](site-recovery-replicate-azure-to-azure.md).</span></span>

![Abilitare il processo di replica - Passaggio 1](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-1.png)

<span data-ttu-id="2a75d-122">**Risorsa**</span><span class="sxs-lookup"><span data-stu-id="2a75d-122">**Resource**</span></span> | <span data-ttu-id="2a75d-123">**Dettagli**</span><span class="sxs-lookup"><span data-stu-id="2a75d-123">**Details**</span></span>
--- | ---
<span data-ttu-id="2a75d-124">**Gruppo di risorse di destinazione**</span><span class="sxs-lookup"><span data-stu-id="2a75d-124">**Target resource group**</span></span> | <span data-ttu-id="2a75d-125">Gruppo di risorse a cui appartengono le VM replicate dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="2a75d-125">The resource group to which replicated VMs belong after failover.</span></span>
<span data-ttu-id="2a75d-126">**Rete virtuale di destinazione**</span><span class="sxs-lookup"><span data-stu-id="2a75d-126">**Target virtual network**</span></span> | <span data-ttu-id="2a75d-127">Rete virtuale in cui si trovano le VM replicate dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="2a75d-127">The virtual network in which replicated VMs are located after failover.</span></span> <span data-ttu-id="2a75d-128">Un mapping di rete viene creato tra le reti virtuali di origine e di destinazione e viceversa.</span><span class="sxs-lookup"><span data-stu-id="2a75d-128">A network mapping is created between source and target virtual networks, and vice versa.</span></span>
<span data-ttu-id="2a75d-129">**Account di archiviazione della cache**</span><span class="sxs-lookup"><span data-stu-id="2a75d-129">**Cache storage accounts**</span></span> | <span data-ttu-id="2a75d-130">Prima che le modifiche apportate nelle VM di origine vengano replicate nell'account di archiviazione di destinazione, vengono registrate e inviate all'account di archiviazione della cache nel percorso di destinazione.</span><span class="sxs-lookup"><span data-stu-id="2a75d-130">Before changes on source VMs are replicated to the target storage account, they are tracked and sent to the cache storage account in the target location.</span></span> <span data-ttu-id="2a75d-131">In questo modo si assicura un impatto minimo sulle app di produzione in esecuzione nella VM.</span><span class="sxs-lookup"><span data-stu-id="2a75d-131">This ensures minimal impact on production apps running on the VM.</span></span>
<span data-ttu-id="2a75d-132">**Account di archiviazione di destinazione**</span><span class="sxs-lookup"><span data-stu-id="2a75d-132">**Target storage accounts**</span></span>  | <span data-ttu-id="2a75d-133">Account di archiviazione nel percorso di destinazione in cui vengono replicati i dati.</span><span class="sxs-lookup"><span data-stu-id="2a75d-133">Storage accounts in the target location to which the data is replicated.</span></span>
<span data-ttu-id="2a75d-134">**Set di disponibilità di destinazione**</span><span class="sxs-lookup"><span data-stu-id="2a75d-134">**Target availability sets**</span></span>  | <span data-ttu-id="2a75d-135">Set di disponibilità in cui si trovano le VM replicate dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="2a75d-135">Availability sets in which the replicated VMs are located after failover.</span></span>

### <a name="step-2"></a><span data-ttu-id="2a75d-136">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="2a75d-136">Step 2</span></span>

<span data-ttu-id="2a75d-137">Poiché la replica è abilitata, il servizio Mobility dell'estensione di Site Recovery viene installato automaticamente nella VM.</span><span class="sxs-lookup"><span data-stu-id="2a75d-137">As replication is enabled, the Site Recovery extension Mobility service is automatically installed on the VM.</span></span> <span data-ttu-id="2a75d-138">Vengono eseguite le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="2a75d-138">The following occurs:</span></span>

1. <span data-ttu-id="2a75d-139">La VM viene registrata in Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="2a75d-139">The VM is registered with Site Recovery.</span></span>

2. <span data-ttu-id="2a75d-140">La replica continua viene configurata per la VM.</span><span class="sxs-lookup"><span data-stu-id="2a75d-140">Continuous replication is configured for the VM.</span></span> <span data-ttu-id="2a75d-141">Le operazioni di scrittura di dati nei dischi delle VM vengono trasferite continuamente nell'account di archiviazione della cache nel percorso di origine.</span><span class="sxs-lookup"><span data-stu-id="2a75d-141">Data writes on the VM disks are continuously transferred to the cache storage account in the source location.</span></span>

   ![Abilitare il processo di replica - Passaggio 2](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-2.png)

   >[!IMPORTANT]
   > <span data-ttu-id="2a75d-143">Site Recovery non necessita mai della connettività in ingresso per la VM.</span><span class="sxs-lookup"><span data-stu-id="2a75d-143">Site Recovery never needs inbound connectivity to the VM.</span></span> <span data-ttu-id="2a75d-144">La VM necessita solo della connettività in uscita agli URL/indirizzi IP del servizio Site Recovery, agli URL/indirizzi IP di autenticazione di Office 365 e agli indirizzi IP dell'account di archiviazione della cache.</span><span class="sxs-lookup"><span data-stu-id="2a75d-144">The VM needs only outbound connectivity to Site Recovery service URLs/IP addresses, Office 365 authentication URLs/IP addresses, and cache storage account IP addresses.</span></span> <span data-ttu-id="2a75d-145">Per altre informazioni, vedere l'articolo [Networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md) (Indicazioni sulla rete per la replica di macchine virtuali di Azure).</span><span class="sxs-lookup"><span data-stu-id="2a75d-145">For more information, see the [Networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md) article.</span></span>

## <a name="continuous-replication-process"></a><span data-ttu-id="2a75d-146">Processo di replica continua</span><span class="sxs-lookup"><span data-stu-id="2a75d-146">Continuous replication process</span></span>

<span data-ttu-id="2a75d-147">Quando la replica continua è attivata correttamente, le operazioni di scrittura nei dischi vengono trasferite immediatamente nell'account di archiviazione della cache.</span><span class="sxs-lookup"><span data-stu-id="2a75d-147">After continuous replication is working, disk writes are immediately transferred to the cache storage account.</span></span> <span data-ttu-id="2a75d-148">Site Recovery elabora i dati e li invia all'account di archiviazione di destinazione.</span><span class="sxs-lookup"><span data-stu-id="2a75d-148">Site Recovery processes the data and sends it to the target storage account.</span></span> <span data-ttu-id="2a75d-149">Dopo l'elaborazione dei dati, vengono generati punti di ripristino nell'account di archiviazione di destinazione a intervalli di pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="2a75d-149">After the data is processed, recovery points are generated in the target storage account every few minutes.</span></span>

## <a name="failover-process"></a><span data-ttu-id="2a75d-150">Processo di failover</span><span class="sxs-lookup"><span data-stu-id="2a75d-150">Failover process</span></span>

<span data-ttu-id="2a75d-151">Quando si avvia un failover, le VM vengono create nel gruppo di risorse di destinazione, nella rete virtuale di destinazione, nella subnet di destinazione e nel set di disponibilità di destinazione.</span><span class="sxs-lookup"><span data-stu-id="2a75d-151">When you initiate a failover, the VMs are created in the target resource group, target virtual network, target subnet, and the target availability set.</span></span> <span data-ttu-id="2a75d-152">Durante un failover è possibile usare qualsiasi punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="2a75d-152">During a failover, you can use any recovery point.</span></span>

![Processo di failover](./media/site-recovery-azure-to-azure-architecture/failover.png)

## <a name="next-steps"></a><span data-ttu-id="2a75d-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2a75d-154">Next steps</span></span>

- <span data-ttu-id="2a75d-155">Altre informazioni sulle [risorse di rete](site-recovery-azure-to-azure-networking-guidance.md) per la replica di VM di Azure.</span><span class="sxs-lookup"><span data-stu-id="2a75d-155">Learn about [networking](site-recovery-azure-to-azure-networking-guidance.md) for Azure VM replication.</span></span>
- <span data-ttu-id="2a75d-156">Seguire la procedura dettagliata per [eseguire la replica di VM di Azure](site-recovery-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="2a75d-156">Follow a walkthrough to [replicate Azure VMs.](site-recovery-azure-to-azure.md)</span></span>
