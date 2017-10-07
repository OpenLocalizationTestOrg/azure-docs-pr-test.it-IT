---
title: aaaAzure e panoramica di rete VM Linux | Documenti Microsoft
description: Una panoramica di rete delle VM Linux e Azure.
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: b5420e35-0463-4456-9803-6142db150f2e
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 10/25/2016
ms.author: v-livech
ms.openlocfilehash: c3de2dc583c62160e10c0e97e96fef49b9eaffbf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-and-linux-vm-network-overview"></a>Panoramica di rete delle macchine virtuali Linux e Azure
## <a name="virtual-networks"></a>Reti virtuali
Una rete virtuale di Azure (VNet) è una rappresentazione della rete nel cloud hello. È un isolamento logico di hello sottoscrizione tooyour cloud di Azure dedicato. È possibile controllare completamente i blocchi di indirizzi IP hello, impostazioni DNS, i criteri di sicurezza e le tabelle di route all'interno di questa rete. È anche possibile segmentare ulteriormente la rete virtuale in subnet e avviare macchine virtuali (VM) IaaS di Azure e/o servizi cloud (istanze del ruolo PaaS). Inoltre, è possibile collegare rete locale tooyour rete virtuale hello utilizzando una delle opzioni di connettività hello disponibili in Azure. In pratica, è possibile espandere le tooAzure di rete, con il controllo completo su blocchi di indirizzi IP con il vantaggio di hello di scala enterprise che fornisce Azure.

* [Panoramica di Rete virtuale.](../../virtual-network/virtual-networks-overview.md)

una rete virtuale utilizzando toocreate hello CLI di Azure, visitare toofollow qui hello procedura dettagliata.

* [Come una rete virtuale utilizzando toocreate hello CLI di Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)

## <a name="network-security-groups"></a>Gruppi di sicurezza di rete
Rete gruppo di sicurezza () contiene un elenco di regole di elenco di controllo di accesso (ACL) che consentono o negano il traffico di rete tooyour istanze di macchina virtuale in una rete virtuale. I gruppi di sicurezza di rete possono essere associati a subnet o singole istanze VM in una subnet. Quando un gruppo è associata a una subnet, regole ACL hello si applicano le istanze VM hello tooall nella subnet. Inoltre, il traffico tooan singole macchine Virtuali è possibile limitare ulteriormente l'associazione di un gruppo direttamente toothat macchina virtuale.

* [Che cos'è un gruppo di sicurezza di rete](../../virtual-network/virtual-networks-nsg.md)
* [Come NSGs toocreate in hello CLI di Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)

## <a name="user-defined-routes"></a>Route definite dall'utente
Quando si aggiunta macchine virtuali (VM) tooa rete virtuale (VNet) in Azure, si noterà che le macchine virtuali hello siano in grado di toocommunicate tra loro attraverso la rete hello, automaticamente. Non è necessario un gateway, toospecify anche se hello macchine virtuali presenti in subnet diverse. Hello lo stesso vale per la comunicazione da hello macchine virtuali toohello rete Internet pubblica e rete locale di tooyour anche quando una connessione ibrida da Azure tooyour proprietario Data Center è presente.

* [Informazioni sulle route definite dall'utente e sull'inoltro IP](../../virtual-network/virtual-networks-udr-overview.md)
* [Creare un UDR in hello CLI di Azure](../../virtual-network/virtual-network-create-udr-arm-cli.md)

## <a name="associating-a-fqdn-tooyour-linux-vm"></a>Associazione di un tooyour FQDN VM Linux
Quando si crea una macchina virtuale (VM) in hello portale di Azure con modello di distribuzione di gestione risorse hello, un indirizzo IP pubblico risorsa per la macchina virtuale hello viene automaticamente creata. Utilizzare questo hello di accesso tooremotely indirizzo IP VM. Anche se il portale di hello non crea un nome di dominio completo o un FQDN, per impostazione predefinita, è possibile aggiungere uno dopo aver creato hello macchina virtuale.

* [Creare un nome di dominio completo nel portale di Azure hello](portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="network-interfaces"></a>Interfacce di rete
Un'interfaccia di rete (NIC) è l'interconnessione hello tra una macchina virtuale (VM) e hello rete software sottostante. Questo articolo spiega è un'interfaccia di rete e come utilizzarlo nel modello di distribuzione Azure Resource Manager hello.

* [Interfacce di rete virtuale](../../virtual-network/virtual-network-network-interface.md)

## <a name="virtual-nics-and-dns-labeling"></a>Etichettatura DNS e NIC virtuali
Se si dispone di un server che è necessario toobe permanenti, ma tale server viene considerato come bovini e viene eliminata e distribuito spesso, si desidererà toouse DNS l'assegnazione di etichette al nome di hello NIC toopersist su hello rete virtuale.  Con hello seguendo una procedura dettagliata si installerà una NIC con un indirizzo IP statico denominata in modo permanente.

* [Creare un ambiente completo di Linux mediante hello CLI di Azure](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="virtual-network-gateways"></a>Gateway di rete virtuale
Viene utilizzato un gateway di rete virtuale toosend il traffico di rete tra reti virtuali di Azure e i percorsi locali e anche tra le reti virtuali in Azure (da-rete). Quando si configura un gateway VPN, è necessario creare e configurare un gateway di rete virtuale e una connessione del gateway di rete virtuale.

* [Informazioni sul gateway VPN](../../vpn-gateway/vpn-gateway-about-vpngateways.md)

## <a name="internal-load-balancing"></a>Bilanciamento del carico interno
Azure Load Balancer è un servizio di bilanciamento del carico di livello 4 (TCP, UDP). servizio di bilanciamento del carico Hello garantisce disponibilità elevata mediante la distribuzione del traffico in entrata tra le istanze del servizio di integrità in servizi cloud o macchine virtuali in un set di bilanciamento del carico. Azure Load Balancer può anche presentare tali servizi su più porte, più indirizzi IP o entrambi.

* [Creazione di un bilanciamento del carico interno utilizzando hello CLI di Azure](../../load-balancer/load-balancer-get-started-internet-arm-cli.md)

