---
title: il mapping di rete per la replica delle macchine virtuali Hyper-V in VMM aaaConfigure cloud tooAzure con Azure Site Recovery | Documenti Microsoft
description: Viene descritto come tooconfigure il mapping di rete durante la replica delle macchine virtuali Hyper-V in VMM cloud tooAzure con Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 081a9fdb0ffa4114099e9bcb9c1b1e43ad26ecbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-configure-network-mapping-for-hyper-v-replication-with-vmm-tooazure"></a><span data-ttu-id="02900-103">Passaggio 9: Configurare il mapping di rete per Hyper-V replica (con VMM) tooAzure</span><span class="sxs-lookup"><span data-stu-id="02900-103">Step 9: Configure network mapping for Hyper-V replication (with VMM) tooAzure</span></span>

<span data-ttu-id="02900-104">Dopo aver impostato hello [le impostazioni di replica di origine e destinazione](vmm-to-azure-walkthrough-source-target.md), utilizzare questo mapping toomap di articolo tooconfigure rete tra le reti VM di VMM in locale e le reti di Azure.</span><span class="sxs-lookup"><span data-stu-id="02900-104">After you set up hello [source and target replication settings](vmm-to-azure-walkthrough-source-target.md), use this article tooconfigure network mapping toomap between on-premises VMM VM networks, and Azure networks.</span></span>

<span data-ttu-id="02900-105">Inviare commenti e domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="02900-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="02900-106">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="02900-106">Before you start</span></span>

- <span data-ttu-id="02900-107">Informazioni sul [mapping di rete](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span><span class="sxs-lookup"><span data-stu-id="02900-107">Learn about [network mapping](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span></span>
- <span data-ttu-id="02900-108">[Preparare VMM per il mapping di rete](vmm-to-azure-walkthrough-network.md#prepare-vmm-for-network-mapping).</span><span class="sxs-lookup"><span data-stu-id="02900-108">[Prepare VMM for network mapping](vmm-to-azure-walkthrough-network.md#prepare-vmm-for-network-mapping).</span></span> 
- <span data-ttu-id="02900-109">Verificare che le macchine virtuali nel server VMM hello siano rete VM tooa connessi e di aver creato almeno una rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="02900-109">Verify that virtual machines on hello VMM server are connected tooa VM network, and that you've created at least one Azure virtual network.</span></span> <span data-ttu-id="02900-110">Più reti VM possono essere mappate tooa singola rete di Azure.</span><span class="sxs-lookup"><span data-stu-id="02900-110">Multiple VM networks can be mapped tooa single Azure network.</span></span>

## <a name="configure-mapping"></a><span data-ttu-id="02900-111">Configurare il mapping</span><span class="sxs-lookup"><span data-stu-id="02900-111">Configure mapping</span></span>

<span data-ttu-id="02900-112">Per configurare il mapping, procedere come segue:</span><span class="sxs-lookup"><span data-stu-id="02900-112">Configure mapping as follows:</span></span>

1. <span data-ttu-id="02900-113">In **infrastruttura di Site Recovery** > **mapping di rete** > **Mapping di rete**, fare clic su hello **+ Mapping di rete**  icona.</span><span class="sxs-lookup"><span data-stu-id="02900-113">In **Site Recovery Infrastructure** > **Network mappings** > **Network Mapping**, click hello **+Network Mapping** icon.</span></span>

    ![Mapping di rete](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping1.png)
2. <span data-ttu-id="02900-115">In **aggiungere mapping di rete**, selezionare server VMM di origine hello e **Azure** come destinazione di hello.</span><span class="sxs-lookup"><span data-stu-id="02900-115">In **Add network mapping**, select hello source VMM server, and **Azure** as hello target.</span></span>
3. <span data-ttu-id="02900-116">Verificare la sottoscrizione hello e modello di distribuzione hello dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="02900-116">Verify hello subscription and hello deployment model after failover.</span></span>
4. <span data-ttu-id="02900-117">In **rete di origine**selezionare rete VM di hello origine locale si desidera toomap dall'elenco di hello associato al server VMM hello.</span><span class="sxs-lookup"><span data-stu-id="02900-117">In **Source network**, select hello source on-premises VM network you want toomap from hello list associated with hello VMM server.</span></span>
5. <span data-ttu-id="02900-118">In **rete di destinazione**, selezionare hello in quale replica di macchine virtuali di Azure sarà disponibile quando si crea rete di Azure.</span><span class="sxs-lookup"><span data-stu-id="02900-118">In **Target network**, select hello Azure network in which replica Azure VMs will be located when they're created.</span></span> <span data-ttu-id="02900-119">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="02900-119">Then click **OK**.</span></span>

    ![Mapping di rete](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping2.png)

<span data-ttu-id="02900-121">Quando ha inizio il mapping di rete vengono eseguite le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="02900-121">Here's what happens when network mapping begins:</span></span>

* <span data-ttu-id="02900-122">Macchine virtuali esistenti in una rete VM origine hello sono connessi toohello rete di destinazione quando avviare il mapping.</span><span class="sxs-lookup"><span data-stu-id="02900-122">Existing VMs on hello source VM network are connected toohello target network when mapping begins.</span></span> <span data-ttu-id="02900-123">Rete VM di origine connesso toohello di nuove macchine virtuali connessi toohello eseguito il mapping di rete di Azure, quando viene eseguita la replica.</span><span class="sxs-lookup"><span data-stu-id="02900-123">New VMs connected toohello source VM network are connected toohello mapped Azure network when replication occurs.</span></span>
* <span data-ttu-id="02900-124">Se si modifica un mapping di rete esistente, macchine virtuali di replica è possibile connettersi utilizzando le nuove impostazioni hello.</span><span class="sxs-lookup"><span data-stu-id="02900-124">If you modify an existing network mapping, replica virtual machines connect using hello new settings.</span></span>
* <span data-ttu-id="02900-125">Se la rete di destinazione hello dispone di più subnet e una di queste subnet è hello stesso nome di subnet nella macchina virtuale di origine che hello si trova, quindi hello macchina virtuale di replica si connette toothat subnet di destinazione dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="02900-125">If hello target network has multiple subnets, and one of those subnets has hello same name as subnet on which hello source virtual machine is located, then hello replica virtual machine connects toothat target subnet after failover.</span></span>
* <span data-ttu-id="02900-126">Se non è presente alcuna subnet di destinazione con un nome corrispondente, macchina virtuale hello si connette toohello prima subnet nella rete hello.</span><span class="sxs-lookup"><span data-stu-id="02900-126">If there’s no target subnet with a matching name, hello virtual machine connects toohello first subnet in hello network.</span></span>



## <a name="next-steps"></a><span data-ttu-id="02900-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="02900-127">Next steps</span></span>

<span data-ttu-id="02900-128">Andare troppo[passaggio 10: creare un criterio di replica](vmm-to-azure-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="02900-128">Go too[Step 10: Create a replication policy](vmm-to-azure-walkthrough-replication.md)</span></span>
