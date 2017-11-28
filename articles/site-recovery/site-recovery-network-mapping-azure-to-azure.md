---
title: Mapping di rete tra due aree di Azure in Azure Site Recovery | Microsoft Docs
description: Azure Site Recovery coordina la replica, il failover e il ripristino di macchine virtuali e server fisici. Informazioni sul failover in Azure o in un centro dati secondario.
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
ms.openlocfilehash: 9d6a806ec533259797080fbfee2c38f918ebd8a2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="network-mapping-between-two-azure-regions"></a><span data-ttu-id="33fdd-104">Mapping di rete tra due aree di Azure</span><span class="sxs-lookup"><span data-stu-id="33fdd-104">Network mapping between two Azure regions</span></span>


<span data-ttu-id="33fdd-105">Questo articolo descrive come mappare tra loro le reti virtuali di Azure di due aree di Azure.</span><span class="sxs-lookup"><span data-stu-id="33fdd-105">This article describes how to map Azure virtual networks of two Azure regions with each other.</span></span> <span data-ttu-id="33fdd-106">Il mapping di rete assicura che quando la macchina virtuale replicata viene creata nell'area di Azure di destinazione, verrà creata nella rete virtuale mappata alla rete virtuale della macchina virtuale di origine.</span><span class="sxs-lookup"><span data-stu-id="33fdd-106">Network mapping ensures that when replicated virtual machine is created in the target Azure region, it is created on the virtual network that is mapped to virtual network of the source virtual machine.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="33fdd-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="33fdd-107">Prerequisites</span></span>
<span data-ttu-id="33fdd-108">Prima di mappare le reti, assicurarsi di avere creato [reti virtuali di Azure](../virtual-network/virtual-networks-overview.md) nelle aree di Azure di origine e di destinazione.</span><span class="sxs-lookup"><span data-stu-id="33fdd-108">Before you map networks make sure, you have created [Azure virtual networks](../virtual-network/virtual-networks-overview.md) in both source and target Azure regions.</span></span>

## <a name="map-networks"></a><span data-ttu-id="33fdd-109">Mappare le reti</span><span class="sxs-lookup"><span data-stu-id="33fdd-109">Map networks</span></span>

<span data-ttu-id="33fdd-110">Per mappare una rete virtuale di Azure in un'area di Azure a un'altra rete virtuale in un'altra area, passare a Site Recovery Infrastructure (Infrastruttura di Site Recovery) -> Mapping di rete (per macchine virtuali di Azure) e creare un mapping di rete.</span><span class="sxs-lookup"><span data-stu-id="33fdd-110">To map an Azure virtual network in one Azure region to another virtual network in another region, go to Site Recovery Infrastructure -> Network Mapping (For Azure Virtual Machines) and create a network mapping.</span></span>

![Mapping di rete](./media/site-recovery-network-mapping-azure-to-azure/network-mapping1.png)


<span data-ttu-id="33fdd-112">Nell'esempio seguente la macchina virtuale è in esecuzione nell'area Asia orientale e viene replicata in Asia sud-orientale.</span><span class="sxs-lookup"><span data-stu-id="33fdd-112">In the example below my virtual machine is running in East Asia region and is being replicated to Southeast Asia.</span></span>

<span data-ttu-id="33fdd-113">Selezionare la rete di origine e di destinazione e quindi fare clic su OK per creare un mapping di rete da Asia orientale ad Asia sud-orientale.</span><span class="sxs-lookup"><span data-stu-id="33fdd-113">Select the source and target network and then click OK to create a network mapping from East Asia to Southeast Asia.</span></span>

![Mapping di rete](./media/site-recovery-network-mapping-azure-to-azure/network-mapping2.png)


<span data-ttu-id="33fdd-115">Eseguire la stessa procedura per creare un mapping di rete da Asia sud-orientale ad Asia orientale.</span><span class="sxs-lookup"><span data-stu-id="33fdd-115">Do the same thing to create a network mapping from Southeast Asia to East Asia.</span></span>  
![Mapping di rete](./media/site-recovery-network-mapping-azure-to-azure/network-mapping3.png)


## <a name="mapping-network-when-enabling-replication"></a><span data-ttu-id="33fdd-117">Mapping di rete durante l'abilitazione della replica</span><span class="sxs-lookup"><span data-stu-id="33fdd-117">Mapping network when enabling replication</span></span>

<span data-ttu-id="33fdd-118">Se il mapping di rete non viene eseguito alla prima replica di una macchina virtuale da un'area di Azure a un'altra, è possibile scegliere la rete di destinazione come parte dello stesso processo.</span><span class="sxs-lookup"><span data-stu-id="33fdd-118">If network mapping is not done when you are replicating a virtual machine for the first time form one Azure region to another, then you can choose target network as part of the same process.</span></span> <span data-ttu-id="33fdd-119">Site Recovery crea mapping di rete dall'area di origine all'area di destinazione e dall'area di destinazione all'area di origine in base a questa selezione.</span><span class="sxs-lookup"><span data-stu-id="33fdd-119">Site Recovery creates network mappings from source region to target region and from target region to source region based on this selection.</span></span>   

![Mapping di rete](./media/site-recovery-network-mapping-azure-to-azure/network-mapping4.png)

<span data-ttu-id="33fdd-121">Per impostazione predefinita, Site Recovery crea una rete nell'area di destinazione che corrisponde alla rete di origine e aggiunge "-asr" come suffisso al nome della rete di origine.</span><span class="sxs-lookup"><span data-stu-id="33fdd-121">By default, Site Recovery creates a network in the target region that is identical to the source network and by adding '-asr' as a suffix to the name of the source network.</span></span> <span data-ttu-id="33fdd-122">È possibile scegliere una rete già creata facendo clic su personalizza.</span><span class="sxs-lookup"><span data-stu-id="33fdd-122">You can choose an already created network by clicking Customize.</span></span>

![Mapping di rete](./media/site-recovery-network-mapping-azure-to-azure/network-mapping5.png)


<span data-ttu-id="33fdd-124">Se il mapping di rete è già stato eseguito, non è possibile modificare la rete virtuale di destinazione durante l'abilitazione della replica.</span><span class="sxs-lookup"><span data-stu-id="33fdd-124">If the network mapping is already done, you can't change the target virtual network while enabling replication.</span></span> <span data-ttu-id="33fdd-125">Per cambiarla, modificare il mapping di rete esistente.</span><span class="sxs-lookup"><span data-stu-id="33fdd-125">To change it, modify existing network mapping.</span></span>  

![Mapping di rete](./media/site-recovery-network-mapping-azure-to-azure/network-mapping6.png)

![Mapping di rete](./media/site-recovery-network-mapping-azure-to-azure/modify-network-mapping.png)

> [!IMPORTANT]
> <span data-ttu-id="33fdd-128">Se si modifica un mapping di rete dall'area 1 all'area 2, assicurarsi di modificare il mapping di rete anche dall'area 2 all'area 1.</span><span class="sxs-lookup"><span data-stu-id="33fdd-128">If you modify a network mapping from region-1 to region-2, make sure you modify the network mapping from region-2 to region-1 as well.</span></span>
>
>


## <a name="subnet-selection"></a><span data-ttu-id="33fdd-129">Selezione della subnet</span><span class="sxs-lookup"><span data-stu-id="33fdd-129">Subnet selection</span></span>
<span data-ttu-id="33fdd-130">La subnet della macchina virtuale di destinazione viene selezionata in base al nome della subnet della macchina virtuale di destinazione.</span><span class="sxs-lookup"><span data-stu-id="33fdd-130">Subnet of the target virtual machine is selected based on the name of the subnet of the source virtual machine.</span></span> <span data-ttu-id="33fdd-131">Se nella rete di destinazione è presente una subnet con nome corrispondente a quello della macchina virtuale di origine, tale subnet verrà scelta per la macchina virtuale di destinazione.</span><span class="sxs-lookup"><span data-stu-id="33fdd-131">If there is a subnet of the same name as that of the source virtual machine available in the target network, then that is chosen for the target virtual machine.</span></span> <span data-ttu-id="33fdd-132">Se nella rete di destinazione non è presente alcuna subnet con lo stesso nome, la prima subnet in ordine alfabetico viene scelta come subnet di destinazione.</span><span class="sxs-lookup"><span data-stu-id="33fdd-132">If there is no subnet with the same name in the target network, then alphabetically first subnet is chosen as the target subnet.</span></span> <span data-ttu-id="33fdd-133">È possibile modificare questa subnet passando alle impostazioni Calcolo e rete della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="33fdd-133">You can modify this subnet by going to Compute and Network settings of the virtual machine.</span></span>

![Modificare la subnet](./media/site-recovery-network-mapping-azure-to-azure/modify-subnet.png)


## <a name="ip-address"></a><span data-ttu-id="33fdd-135">Indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="33fdd-135">IP address</span></span>

<span data-ttu-id="33fdd-136">L'indirizzo IP per ogni interfaccia di rete della macchina virtuale di destinazione viene scelto come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="33fdd-136">IP address for each of the network interface of the target virtual machine is chosen as follows:</span></span>

### <a name="dhcp"></a><span data-ttu-id="33fdd-137">DHCP</span><span class="sxs-lookup"><span data-stu-id="33fdd-137">DHCP</span></span>
<span data-ttu-id="33fdd-138">Se l'interfaccia di rete della macchina virtuale di origine usa DHCP, anche l'interfaccia di rete della macchina virtuale di destinazione viene impostata come DHCP.</span><span class="sxs-lookup"><span data-stu-id="33fdd-138">If the network interface of the source virtual machine is using DHCP, then network interface of the target virtual machine is also set as DHCP.</span></span>

### <a name="static-ip"></a><span data-ttu-id="33fdd-139">IP statico</span><span class="sxs-lookup"><span data-stu-id="33fdd-139">Static IP</span></span>
<span data-ttu-id="33fdd-140">Se l'interfaccia di rete della macchina virtuale di origine usa un indirizzo IP statico, anche l'interfaccia di rete della macchina virtuale di destinazione viene impostata per usare un indirizzo IP statico.</span><span class="sxs-lookup"><span data-stu-id="33fdd-140">If the network interface of the source virtual machine is using Static IP, then network interface of the target virtual machine is also set to use Static IP.</span></span> <span data-ttu-id="33fdd-141">L'indirizzo IP statico viene scelto come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="33fdd-141">Static IP is chosen as follows:</span></span>

#### <a name="same-address-space"></a><span data-ttu-id="33fdd-142">Stesso spazio di indirizzi</span><span class="sxs-lookup"><span data-stu-id="33fdd-142">Same address space</span></span>

<span data-ttu-id="33fdd-143">Se la subnet di origine e la subnet di destinazione hanno lo stesso spazio di indirizzi, l'indirizzo IP di destinazione viene impostato come uguale all'indirizzo IP dell'interfaccia di rete della macchina virtuale di origine.</span><span class="sxs-lookup"><span data-stu-id="33fdd-143">If the source subnet and the target subnet have the same address space, then target IP is set same as the IP of  the network interface of the source virtual machine.</span></span> <span data-ttu-id="33fdd-144">Se lo stesso indirizzo IP non è disponibile, un altro indirizzo IP disponibile viene impostato come indirizzo IP di destinazione.</span><span class="sxs-lookup"><span data-stu-id="33fdd-144">If same IP is not available, then some other available IP is set as the target IP.</span></span>

#### <a name="different-address-space"></a><span data-ttu-id="33fdd-145">Spazio di indirizzi diverso</span><span class="sxs-lookup"><span data-stu-id="33fdd-145">Different address space</span></span>

<span data-ttu-id="33fdd-146">Se la subnet di origine e la subnet di destinazione hanno spazi di indirizzi diversi, l'indirizzo IP di destinazione viene impostato su un qualsiasi indirizzo IP disponibile nella subnet di destinazione.</span><span class="sxs-lookup"><span data-stu-id="33fdd-146">If the source subnet and the target subnet have different address space, then target IP is set as any available IP in the target subnet.</span></span>

<span data-ttu-id="33fdd-147">È possibile modificare l'indirizzo IP di destinazione in ogni interfaccia di rete passando alle impostazioni Calcolo e rete della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="33fdd-147">You can modify the target IP on each network interface by going to Compute and Network settings of the virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="33fdd-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="33fdd-148">Next steps</span></span>

- <span data-ttu-id="33fdd-149">Altre informazioni sulle [indicazioni sulla rete per la replica di VM di Azure](site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="33fdd-149">Learn about [networking guidance for replicating Azure VMs](site-recovery-azure-to-azure-networking-guidance.md).</span></span>
