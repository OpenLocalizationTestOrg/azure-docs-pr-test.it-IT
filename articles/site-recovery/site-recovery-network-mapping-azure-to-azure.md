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
# <a name="network-mapping-between-two-azure-regions"></a>Mapping di rete tra due aree di Azure


Questo articolo viene descritto come toomap Azure reti virtuali tra due regioni di Azure tra loro. Mapping di rete garantisce che, quando macchina virtuale replicata viene creato nella destinazione hello regione di Azure, viene creato nella rete virtuale hello che sia mappata toovirtual rete della macchina virtuale di origine hello.  

## <a name="prerequisites"></a>Prerequisiti
Prima di mappare le reti, assicurarsi di avere creato [reti virtuali di Azure](../virtual-network/virtual-networks-overview.md) nelle aree di Azure di origine e di destinazione.

## <a name="map-networks"></a>Mappare le reti

una rete virtuale di Azure nella rete virtuale tooanother di un'area di Azure in un'altra area, andare tooSite ripristino infrastruttura toomap -> il Mapping di rete (per macchine virtuali di Azure) e creare un mapping di rete.

![Mapping di rete](./media/site-recovery-network-mapping-azure-to-azure/network-mapping1.png)


In hello esempio riportato di seguito la macchina virtuale è in esecuzione nell'area Asia orientale e viene replicato tooSoutheast Asia.

Selezionare una rete di origine e destinazione hello e quindi fare clic su OK toocreate un mapping di rete da Asia orientale tooSoutheast Asia.

![Mapping di rete](./media/site-recovery-network-mapping-azure-to-azure/network-mapping2.png)


Hello stesso cosa toocreate un mapping di rete da Asia sudorientale tooEast Asia.  
![Mapping di rete](./media/site-recovery-network-mapping-azure-to-azure/network-mapping3.png)


## <a name="mapping-network-when-enabling-replication"></a>Mapping di rete durante l'abilitazione della replica

Se il mapping di rete non viene eseguito quando si esegue la replica di una macchina virtuale per hello prima ora modulo una regione di Azure tooanother, quindi è possibile scegliere rete di destinazione come parte di hello stesso processo. Site Recovery crea i mapping di rete da tootarget paese di origine e di destinazione toosource paese in base alle selezioni.   

![Mapping di rete](./media/site-recovery-network-mapping-azure-to-azure/network-mapping4.png)

Per impostazione predefinita, il ripristino del sito viene creata una rete nell'area di destinazione hello toohello identici rete di origine e aggiungendo '-ripristino automatico di sistema ' come nome di rete di origine hello toohello suffisso. È possibile scegliere una rete già creata facendo clic su personalizza.

![Mapping di rete](./media/site-recovery-network-mapping-azure-to-azure/network-mapping5.png)


Se viene già eseguito il mapping di rete hello, è possibile modificare una rete virtuale di destinazione hello durante l'abilitazione della replica. toochange, modificare il mapping di rete esistente.  

![Mapping di rete](./media/site-recovery-network-mapping-azure-to-azure/network-mapping6.png)

![Mapping di rete](./media/site-recovery-network-mapping-azure-to-azure/modify-network-mapping.png)

> [!IMPORTANT]
> Se si modifica un mapping di rete da 1 a area tooregion-2, assicurarsi che si modifica il mapping di rete hello da tooregion area-2-1 anche.
>
>


## <a name="subnet-selection"></a>Selezione della subnet
Subnet della macchina virtuale di destinazione hello è selezionata in base al nome della subnet hello della macchina virtuale di origine hello hello. Se è presente una subnet di hello stesso nome della macchina virtuale di hello origine disponibile in rete di destinazione hello, che viene scelto per la macchina virtuale di destinazione hello. Se è presente alcuna subnet con hello stesso nome nella rete di destinazione hello, in ordine alfabetico prima subnet viene scelto come hello subnet di destinazione. È possibile modificare questa subnet passando tooCompute e le impostazioni di rete della macchina virtuale hello.

![Modificare la subnet](./media/site-recovery-network-mapping-azure-to-azure/modify-subnet.png)


## <a name="ip-address"></a>Indirizzo IP

Indirizzo IP per ogni interfaccia di rete hello di macchina virtuale di destinazione hello viene scelto come indicato di seguito:

### <a name="dhcp"></a>DHCP
Se hello interfaccia di rete della macchina virtuale di origine hello utilizza DHCP, l'interfaccia di rete della macchina virtuale di destinazione hello anche viene impostata come DHCP.

### <a name="static-ip"></a>IP statico
Se l'interfaccia di rete hello della macchina virtuale di origine hello Usa indirizzo IP statico, quindi interfaccia di rete della macchina virtuale di destinazione hello viene impostato anche toouse IP statico. L'indirizzo IP statico viene scelto come indicato di seguito:

#### <a name="same-address-space"></a>Stesso spazio di indirizzi

Se dispone di subnet di origine hello e destinazione hello hello stesso spazio di indirizzi, quindi l'indirizzo IP di destinazione è uguale a IP hello hello interfaccia di rete della macchina virtuale di origine hello. Se lo stesso IP non è disponibile, alcuni altri IP disponibili è impostato come indirizzo IP di destinazione hello.

#### <a name="different-address-space"></a>Spazio di indirizzi diverso

Se hello origine subnet e subnet di destinazione di hello dispone di spazio degli indirizzi diversi, indirizzo IP di destinazione è impostato come qualsiasi indirizzo IP disponibile nella subnet di destinazione hello.

È possibile modificare l'indirizzo IP di destinazione hello in ogni interfaccia di rete passando tooCompute e le impostazioni di rete della macchina virtuale hello.

## <a name="next-steps"></a>Passaggi successivi

- Altre informazioni sulle [indicazioni sulla rete per la replica di VM di Azure](site-recovery-azure-to-azure-networking-guidance.md).
