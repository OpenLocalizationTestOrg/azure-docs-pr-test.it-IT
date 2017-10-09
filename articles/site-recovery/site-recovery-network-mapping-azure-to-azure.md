---
title: mapping di aaaNetwork tra due aree di Azure in Azure Site Recovery | Documenti Microsoft
description: Azure Site Recovery coordina la replica di hello, failover e il ripristino delle macchine virtuali e server fisici. Informazioni su failover tooAzure o un Data Center secondario.
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: pratshar
ms.openlocfilehash: 4f80c44e3f94eaf446bc01a7041d91fe34aa78d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="network-mapping-between-two-azure-regions"></a><span data-ttu-id="53643-104">Mapping di rete tra due aree di Azure</span><span class="sxs-lookup"><span data-stu-id="53643-104">Network mapping between two Azure regions</span></span>


<span data-ttu-id="53643-105">Questo articolo viene descritto come toomap Azure reti virtuali tra due regioni di Azure tra loro.</span><span class="sxs-lookup"><span data-stu-id="53643-105">This article describes how toomap Azure virtual networks of two Azure regions with each other.</span></span> <span data-ttu-id="53643-106">Mapping di rete garantisce che, quando macchina virtuale replicata viene creato nella destinazione hello regione di Azure, viene creato nella rete virtuale hello che sia mappata toovirtual rete della macchina virtuale di origine hello.</span><span class="sxs-lookup"><span data-stu-id="53643-106">Network mapping ensures that when replicated virtual machine is created in hello target Azure region, it is created on hello virtual network that is mapped toovirtual network of hello source virtual machine.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="53643-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="53643-107">Prerequisites</span></span>
<span data-ttu-id="53643-108">Prima di mappare le reti, assicurarsi di avere creato [reti virtuali di Azure](../virtual-network/virtual-networks-overview.md) nelle aree di Azure di origine e di destinazione.</span><span class="sxs-lookup"><span data-stu-id="53643-108">Before you map networks make sure, you have created [Azure virtual networks](../virtual-network/virtual-networks-overview.md) in both source and target Azure regions.</span></span>

## <a name="map-networks"></a><span data-ttu-id="53643-109">Mappare le reti</span><span class="sxs-lookup"><span data-stu-id="53643-109">Map networks</span></span>

<span data-ttu-id="53643-110">una rete virtuale di Azure nella rete virtuale tooanother di un'area di Azure in un'altra area, andare tooSite ripristino infrastruttura toomap -> il Mapping di rete (per macchine virtuali di Azure) e creare un mapping di rete.</span><span class="sxs-lookup"><span data-stu-id="53643-110">toomap an Azure virtual network in one Azure region tooanother virtual network in another region, go tooSite Recovery Infrastructure -> Network Mapping (For Azure Virtual Machines) and create a network mapping.</span></span>

![Mapping di rete](./media/site-recovery-network-mapping-azure-to-azure/network-mapping1.png)


<span data-ttu-id="53643-112">In hello esempio riportato di seguito la macchina virtuale è in esecuzione nell'area Asia orientale e viene replicato tooSoutheast Asia.</span><span class="sxs-lookup"><span data-stu-id="53643-112">In hello example below my virtual machine is running in East Asia region and is being replicated tooSoutheast Asia.</span></span>

<span data-ttu-id="53643-113">Selezionare una rete di origine e destinazione hello e quindi fare clic su OK toocreate un mapping di rete da Asia orientale tooSoutheast Asia.</span><span class="sxs-lookup"><span data-stu-id="53643-113">Select hello source and target network and then click OK toocreate a network mapping from East Asia tooSoutheast Asia.</span></span>

![Mapping di rete](./media/site-recovery-network-mapping-azure-to-azure/network-mapping2.png)


<span data-ttu-id="53643-115">Hello stesso cosa toocreate un mapping di rete da Asia sudorientale tooEast Asia.</span><span class="sxs-lookup"><span data-stu-id="53643-115">Do hello same thing toocreate a network mapping from Southeast Asia tooEast Asia.</span></span>  
![Mapping di rete](./media/site-recovery-network-mapping-azure-to-azure/network-mapping3.png)


## <a name="mapping-network-when-enabling-replication"></a><span data-ttu-id="53643-117">Mapping di rete durante l'abilitazione della replica</span><span class="sxs-lookup"><span data-stu-id="53643-117">Mapping network when enabling replication</span></span>

<span data-ttu-id="53643-118">Se il mapping di rete non viene eseguito quando si esegue la replica di una macchina virtuale per hello prima ora modulo una regione di Azure tooanother, quindi è possibile scegliere rete di destinazione come parte di hello stesso processo.</span><span class="sxs-lookup"><span data-stu-id="53643-118">If network mapping is not done when you are replicating a virtual machine for hello first time form one Azure region tooanother, then you can choose target network as part of hello same process.</span></span> <span data-ttu-id="53643-119">Site Recovery crea i mapping di rete da tootarget paese di origine e di destinazione toosource paese in base alle selezioni.</span><span class="sxs-lookup"><span data-stu-id="53643-119">Site Recovery creates network mappings from source region tootarget region and from target region toosource region based on this selection.</span></span>   

![Mapping di rete](./media/site-recovery-network-mapping-azure-to-azure/network-mapping4.png)

<span data-ttu-id="53643-121">Per impostazione predefinita, il ripristino del sito viene creata una rete nell'area di destinazione hello toohello identici rete di origine e aggiungendo '-ripristino automatico di sistema ' come nome di rete di origine hello toohello suffisso.</span><span class="sxs-lookup"><span data-stu-id="53643-121">By default, Site Recovery creates a network in hello target region that is identical toohello source network and by adding '-asr' as a suffix toohello name of hello source network.</span></span> <span data-ttu-id="53643-122">È possibile scegliere una rete già creata facendo clic su personalizza.</span><span class="sxs-lookup"><span data-stu-id="53643-122">You can choose an already created network by clicking Customize.</span></span>

![Mapping di rete](./media/site-recovery-network-mapping-azure-to-azure/network-mapping5.png)


<span data-ttu-id="53643-124">Se viene già eseguito il mapping di rete hello, è possibile modificare una rete virtuale di destinazione hello durante l'abilitazione della replica.</span><span class="sxs-lookup"><span data-stu-id="53643-124">If hello network mapping is already done, you can't change hello target virtual network while enabling replication.</span></span> <span data-ttu-id="53643-125">toochange, modificare il mapping di rete esistente.</span><span class="sxs-lookup"><span data-stu-id="53643-125">toochange it, modify existing network mapping.</span></span>  

![Mapping di rete](./media/site-recovery-network-mapping-azure-to-azure/network-mapping6.png)

![Mapping di rete](./media/site-recovery-network-mapping-azure-to-azure/modify-network-mapping.png)

> [!IMPORTANT]
> <span data-ttu-id="53643-128">Se si modifica un mapping di rete da 1 a area tooregion-2, assicurarsi che si modifica il mapping di rete hello da tooregion area-2-1 anche.</span><span class="sxs-lookup"><span data-stu-id="53643-128">If you modify a network mapping from region-1 tooregion-2, make sure you modify hello network mapping from region-2 tooregion-1 as well.</span></span>
>
>


## <a name="subnet-selection"></a><span data-ttu-id="53643-129">Selezione della subnet</span><span class="sxs-lookup"><span data-stu-id="53643-129">Subnet selection</span></span>
<span data-ttu-id="53643-130">Subnet della macchina virtuale di destinazione hello è selezionata in base al nome della subnet hello della macchina virtuale di origine hello hello.</span><span class="sxs-lookup"><span data-stu-id="53643-130">Subnet of hello target virtual machine is selected based on hello name of hello subnet of hello source virtual machine.</span></span> <span data-ttu-id="53643-131">Se è presente una subnet di hello stesso nome della macchina virtuale di hello origine disponibile in rete di destinazione hello, che viene scelto per la macchina virtuale di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="53643-131">If there is a subnet of hello same name as that of hello source virtual machine available in hello target network, then that is chosen for hello target virtual machine.</span></span> <span data-ttu-id="53643-132">Se è presente alcuna subnet con hello stesso nome nella rete di destinazione hello, in ordine alfabetico prima subnet viene scelto come hello subnet di destinazione.</span><span class="sxs-lookup"><span data-stu-id="53643-132">If there is no subnet with hello same name in hello target network, then alphabetically first subnet is chosen as hello target subnet.</span></span> <span data-ttu-id="53643-133">È possibile modificare questa subnet passando tooCompute e le impostazioni di rete della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="53643-133">You can modify this subnet by going tooCompute and Network settings of hello virtual machine.</span></span>

![Modificare la subnet](./media/site-recovery-network-mapping-azure-to-azure/modify-subnet.png)


## <a name="ip-address"></a><span data-ttu-id="53643-135">Indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="53643-135">IP address</span></span>

<span data-ttu-id="53643-136">Indirizzo IP per ogni interfaccia di rete hello di macchina virtuale di destinazione hello viene scelto come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="53643-136">IP address for each of hello network interface of hello target virtual machine is chosen as follows:</span></span>

### <a name="dhcp"></a><span data-ttu-id="53643-137">DHCP</span><span class="sxs-lookup"><span data-stu-id="53643-137">DHCP</span></span>
<span data-ttu-id="53643-138">Se hello interfaccia di rete della macchina virtuale di origine hello utilizza DHCP, l'interfaccia di rete della macchina virtuale di destinazione hello anche viene impostata come DHCP.</span><span class="sxs-lookup"><span data-stu-id="53643-138">If hello network interface of hello source virtual machine is using DHCP, then network interface of hello target virtual machine is also set as DHCP.</span></span>

### <a name="static-ip"></a><span data-ttu-id="53643-139">IP statico</span><span class="sxs-lookup"><span data-stu-id="53643-139">Static IP</span></span>
<span data-ttu-id="53643-140">Se l'interfaccia di rete hello della macchina virtuale di origine hello Usa indirizzo IP statico, quindi interfaccia di rete della macchina virtuale di destinazione hello viene impostato anche toouse IP statico.</span><span class="sxs-lookup"><span data-stu-id="53643-140">If hello network interface of hello source virtual machine is using Static IP, then network interface of hello target virtual machine is also set toouse Static IP.</span></span> <span data-ttu-id="53643-141">L'indirizzo IP statico viene scelto come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="53643-141">Static IP is chosen as follows:</span></span>

#### <a name="same-address-space"></a><span data-ttu-id="53643-142">Stesso spazio di indirizzi</span><span class="sxs-lookup"><span data-stu-id="53643-142">Same address space</span></span>

<span data-ttu-id="53643-143">Se dispone di subnet di origine hello e destinazione hello hello stesso spazio di indirizzi, quindi l'indirizzo IP di destinazione è uguale a IP hello hello interfaccia di rete della macchina virtuale di origine hello.</span><span class="sxs-lookup"><span data-stu-id="53643-143">If hello source subnet and hello target subnet have hello same address space, then target IP is set same as hello IP of  hello network interface of hello source virtual machine.</span></span> <span data-ttu-id="53643-144">Se lo stesso IP non è disponibile, alcuni altri IP disponibili è impostato come indirizzo IP di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="53643-144">If same IP is not available, then some other available IP is set as hello target IP.</span></span>

#### <a name="different-address-space"></a><span data-ttu-id="53643-145">Spazio di indirizzi diverso</span><span class="sxs-lookup"><span data-stu-id="53643-145">Different address space</span></span>

<span data-ttu-id="53643-146">Se hello origine subnet e subnet di destinazione di hello dispone di spazio degli indirizzi diversi, indirizzo IP di destinazione è impostato come qualsiasi indirizzo IP disponibile nella subnet di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="53643-146">If hello source subnet and hello target subnet have different address space, then target IP is set as any available IP in hello target subnet.</span></span>

<span data-ttu-id="53643-147">È possibile modificare l'indirizzo IP di destinazione hello in ogni interfaccia di rete passando tooCompute e le impostazioni di rete della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="53643-147">You can modify hello target IP on each network interface by going tooCompute and Network settings of hello virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="53643-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="53643-148">Next steps</span></span>

- <span data-ttu-id="53643-149">Altre informazioni sulle [indicazioni sulla rete per la replica di VM di Azure](site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="53643-149">Learn about [networking guidance for replicating Azure VMs](site-recovery-azure-to-azure-networking-guidance.md).</span></span>
