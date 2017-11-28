---
title: aaaMap reti per il sito secondario macchina virtuale Hyper-V replica tooa con Azure Site Recovery | Documenti Microsoft
description: Viene descritto come toomap reti per la replica delle macchine virtuali Hyper-V tooa VMM del sito secondario con Azure Site Recovery.
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
ms.openlocfilehash: d4f621df4ce08ae055bc6809daea0b71b76754ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-map-networks-for-hyper-v-vm-replication-tooa-secondary-site"></a><span data-ttu-id="10500-103">Passaggio 7: Eseguire il mapping di reti per il sito secondario di macchina virtuale Hyper-V replica tooa</span><span class="sxs-lookup"><span data-stu-id="10500-103">Step 7: Map networks for Hyper-V VM replication tooa secondary site</span></span>


<span data-ttu-id="10500-104">Dopo l'impostazione [impostazioni di origine e destinazione](vmm-to-vmm-walkthrough-source-target.md) per la replica Hyper-V, macchine virtuali (VM) tooa System Center Virtual Machine Manager (VMM) del sito secondario, utilizzare questo mapping di rete tooconfigure articolo per virtuale Hyper-V Machine (VM) replica tooa secondario del sito, utilizzando [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="10500-104">After setting up [source and target settings](vmm-to-vmm-walkthrough-source-target.md) for replicating Hyper-V virtual machines (VMs) tooa secondary System Center Virtual Machine Manager (VMM) site, use this article tooconfigure network mapping for Hyper-V virtual machine (VM) replication tooa secondary site, using  [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="10500-105">Dopo aver letto questo articolo, inviare eventuali commenti nella parte inferiore di hello o in hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="10500-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="10500-106">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="10500-106">Before you start</span></span>

- <span data-ttu-id="10500-107">Leggere le informazioni sul [mapping di rete](vmm-to-vmm-walkthrough-network.md#network-mapping-overview) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="10500-107">Learn about [network mapping](vmm-to-vmm-walkthrough-network.md#network-mapping-overview) before you start.</span></span>
- <span data-ttu-id="10500-108">Verificare che le macchine virtuali nei server VMM siano connessi tooa rete VM.</span><span class="sxs-lookup"><span data-stu-id="10500-108">Verify that virtual machines on VMM servers are connected tooa VM network.</span></span>

## <a name="configure-network-mapping"></a><span data-ttu-id="10500-109">Configurare il mapping di rete</span><span class="sxs-lookup"><span data-stu-id="10500-109">Configure network mapping</span></span>

1. <span data-ttu-id="10500-110">In **Mapping di rete** > **Mapping di rete** fare clic su **+Mapping di rete**.</span><span class="sxs-lookup"><span data-stu-id="10500-110">In **Network Mapping** > **Network mappings**, click **+Network Mapping**.</span></span>
2. <span data-ttu-id="10500-111">In **aggiungere mapping di rete** , selezionare l'origine hello e i server VMM di destinazione.</span><span class="sxs-lookup"><span data-stu-id="10500-111">In **Add network mapping** tab, select hello source and target VMM servers.</span></span> <span data-ttu-id="10500-112">vengono recuperate le reti VM Hello associate al server VMM hello.</span><span class="sxs-lookup"><span data-stu-id="10500-112">hello VM networks associated with hello VMM servers are retrieved.</span></span>
3. <span data-ttu-id="10500-113">In **rete di origine**selezionare hello rete toouse elenco hello di reti VM associate al server VMM primario hello.</span><span class="sxs-lookup"><span data-stu-id="10500-113">In **Source network**, select hello network you want toouse from hello list of VM networks associated with hello primary VMM server.</span></span>
4. <span data-ttu-id="10500-114">In **rete di destinazione**selezionare hello rete toouse nel server VMM secondario hello.</span><span class="sxs-lookup"><span data-stu-id="10500-114">In **Target network**, select hello network you want toouse on hello secondary VMM server.</span></span> <span data-ttu-id="10500-115">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="10500-115">Then click **OK**.</span></span>

    ![Mapping di rete](./media/vmm-to-vmm-walkthrough-network-mapping/network-mapping2.png)

<span data-ttu-id="10500-117">Quando ha inizio il mapping di rete vengono eseguite le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="10500-117">Here's what happens when network mapping begins:</span></span>

* <span data-ttu-id="10500-118">Le macchine virtuali di replica esistente che corrispondono toohello rete VM di origine sarà connessa toohello rete VM di destinazione.</span><span class="sxs-lookup"><span data-stu-id="10500-118">Any existing replica virtual machines that correspond toohello source VM network will be connected toohello target VM network.</span></span>
* <span data-ttu-id="10500-119">Nuove macchine virtuali che sono connessi toohello rete VM di origine sarà connessa toohello rete mappata di destinazione dopo la replica.</span><span class="sxs-lookup"><span data-stu-id="10500-119">New virtual machines that are connected toohello source VM network will be connected toohello target mapped network after replication.</span></span>
* <span data-ttu-id="10500-120">Se si modifica un mapping esistente con una nuova rete, macchine virtuali di replica verranno connesse usando le nuove impostazioni hello.</span><span class="sxs-lookup"><span data-stu-id="10500-120">If you modify an existing mapping with a new network, replica virtual machines will be connected using hello new settings.</span></span>
* <span data-ttu-id="10500-121">Se la rete di destinazione hello dispone di più subnet e una di queste subnet è hello stesso nome di subnet nella macchina virtuale di origine che hello si trova, quindi hello macchina virtuale di replica sarà connessa toothat subnet di destinazione dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="10500-121">If hello target network has multiple subnets and one of those subnets has hello same name as subnet on which hello source virtual machine is located, then hello replica virtual machine will be connected toothat target subnet after failover.</span></span> <span data-ttu-id="10500-122">Se non è presente alcuna subnet di destinazione con un nome corrispondente, macchina virtuale hello sarà toohello connessi prima subnet nella rete hello.</span><span class="sxs-lookup"><span data-stu-id="10500-122">If there’s no target subnet with a matching name, hello virtual machine will be connected toohello first subnet in hello network.</span></span>



## <a name="next-steps"></a><span data-ttu-id="10500-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="10500-123">Next steps</span></span>

<span data-ttu-id="10500-124">Andare troppo[passaggio 8: configurare un criterio di replica](vmm-to-vmm-walkthrough-replication.md).</span><span class="sxs-lookup"><span data-stu-id="10500-124">Go too[Step 8: Configure a replication policy](vmm-to-vmm-walkthrough-replication.md).</span></span>
