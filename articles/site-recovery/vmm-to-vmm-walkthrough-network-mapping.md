---
title: Mappare reti per la replica di VM Hyper-V VM in un sito secondario con Azure Site Recovery | Microsoft Docs
description: Descrive come mappare le reti durante la replica di VM Hyper-V in un sito VMM secondario con Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 461b7c1c-ef61-4005-aeec-2324e727a3d0
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 606e2d3d0e31b9d80200105e812f9d7bbbcf939c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="step-7-map-networks-for-hyper-v-vm-replication-to-a-secondary-site"></a><span data-ttu-id="bb8aa-103">Passaggio 7: Mappare reti per la replica di VM Hyper-V in un sito secondario</span><span class="sxs-lookup"><span data-stu-id="bb8aa-103">Step 7: Map networks for Hyper-V VM replication to a secondary site</span></span>


<span data-ttu-id="bb8aa-104">Dopo avere configurato le [impostazioni di origine e di destinazione](vmm-to-vmm-walkthrough-source-target.md) per la replica di macchine virtuali Hyper-V in un sito System Center Virtual Machine Manager (VMM) secondario, usare le istruzioni disponibili in questo articolo per configurare il mapping di rete per la replica di macchine virtuali Hyper-V in un sito secondario tramite [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bb8aa-104">After setting up [source and target settings](vmm-to-vmm-walkthrough-source-target.md) for replicating Hyper-V virtual machines (VMs) to a secondary System Center Virtual Machine Manager (VMM) site, use this article to configure network mapping for Hyper-V virtual machine (VM) replication to a secondary site, using  [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="bb8aa-105">È possibile inviare commenti nella parte inferiore di questo articolo oppure nel [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="bb8aa-105">After reading this article, post any comments at the bottom, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="bb8aa-106">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="bb8aa-106">Before you start</span></span>

- <span data-ttu-id="bb8aa-107">Leggere le informazioni sul [mapping di rete](vmm-to-vmm-walkthrough-network.md#network-mapping-overview) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="bb8aa-107">Learn about [network mapping](vmm-to-vmm-walkthrough-network.md#network-mapping-overview) before you start.</span></span>
- <span data-ttu-id="bb8aa-108">Verificare che le macchine virtuali sui server VMM siano connesse a una rete VM.</span><span class="sxs-lookup"><span data-stu-id="bb8aa-108">Verify that virtual machines on VMM servers are connected to a VM network.</span></span>

## <a name="configure-network-mapping"></a><span data-ttu-id="bb8aa-109">Configurare il mapping di rete</span><span class="sxs-lookup"><span data-stu-id="bb8aa-109">Configure network mapping</span></span>

1. <span data-ttu-id="bb8aa-110">In **Mapping di rete** > **Mapping di rete** fare clic su **+Mapping di rete**.</span><span class="sxs-lookup"><span data-stu-id="bb8aa-110">In **Network Mapping** > **Network mappings**, click **+Network Mapping**.</span></span>
2. <span data-ttu-id="bb8aa-111">Nella scheda **Aggiungi mapping di rete** selezionare i server VMM di origine e di destinazione.</span><span class="sxs-lookup"><span data-stu-id="bb8aa-111">In **Add network mapping** tab, select the source and target VMM servers.</span></span> <span data-ttu-id="bb8aa-112">Vengono recuperate le reti VM associate ai server VMM.</span><span class="sxs-lookup"><span data-stu-id="bb8aa-112">The VM networks associated with the VMM servers are retrieved.</span></span>
3. <span data-ttu-id="bb8aa-113">In **Rete di origine**selezionare la rete che si vuole usare nell'elenco di reti VM associate al server VMM primario.</span><span class="sxs-lookup"><span data-stu-id="bb8aa-113">In **Source network**, select the network you want to use from the list of VM networks associated with the primary VMM server.</span></span>
4. <span data-ttu-id="bb8aa-114">In **Rete di destinazione** selezionare la rete che si vuole usare nel server VMM secondario.</span><span class="sxs-lookup"><span data-stu-id="bb8aa-114">In **Target network**, select the network you want to use on the secondary VMM server.</span></span> <span data-ttu-id="bb8aa-115">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="bb8aa-115">Then click **OK**.</span></span>

    ![Mapping di rete](./media/vmm-to-vmm-walkthrough-network-mapping/network-mapping2.png)

<span data-ttu-id="bb8aa-117">Quando ha inizio il mapping di rete vengono eseguite le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="bb8aa-117">Here's what happens when network mapping begins:</span></span>

* <span data-ttu-id="bb8aa-118">Tutte le macchine virtuali di replica esistenti che corrispondono alla rete VM di origine verranno connesse alle reti VM di destinazione.</span><span class="sxs-lookup"><span data-stu-id="bb8aa-118">Any existing replica virtual machines that correspond to the source VM network will be connected to the target VM network.</span></span>
* <span data-ttu-id="bb8aa-119">Dopo la replica, le nuove macchine virtuali connesse alla rete VM di origine verranno connesse alla rete mappata di destinazione.</span><span class="sxs-lookup"><span data-stu-id="bb8aa-119">New virtual machines that are connected to the source VM network will be connected to the target mapped network after replication.</span></span>
* <span data-ttu-id="bb8aa-120">Se si modifica un mapping esistente con una nuova rete, le macchine virtuali di replica verranno connesse usando le nuove impostazioni.</span><span class="sxs-lookup"><span data-stu-id="bb8aa-120">If you modify an existing mapping with a new network, replica virtual machines will be connected using the new settings.</span></span>
* <span data-ttu-id="bb8aa-121">Se la rete di destinazione dispone di più subnet e una di esse ha lo stesso nome di una subnet in cui si trova la macchina virtuale di origine, la macchina virtuale di replica sarà connessa a tale subnet di destinazione dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="bb8aa-121">If the target network has multiple subnets and one of those subnets has the same name as subnet on which the source virtual machine is located, then the replica virtual machine will be connected to that target subnet after failover.</span></span> <span data-ttu-id="bb8aa-122">Se non è presente una subnet di destinazione con un nome corrispondente, la macchina virtuale sarà connessa alla prima subnet della rete.</span><span class="sxs-lookup"><span data-stu-id="bb8aa-122">If there’s no target subnet with a matching name, the virtual machine will be connected to the first subnet in the network.</span></span>



## <a name="next-steps"></a><span data-ttu-id="bb8aa-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bb8aa-123">Next steps</span></span>

<span data-ttu-id="bb8aa-124">Andare al [Passaggio 8: Configurare un criterio di replica](vmm-to-vmm-walkthrough-replication.md).</span><span class="sxs-lookup"><span data-stu-id="bb8aa-124">Go to [Step 8: Configure a replication policy](vmm-to-vmm-walkthrough-replication.md).</span></span>