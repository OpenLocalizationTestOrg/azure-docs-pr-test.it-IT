---
title: Rete virtuale aaaAzure | Documenti Microsoft
description: "Informazioni sui concetti e sulle funzionalità di Rete virtuale di Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 9633de4b-a867-4ddf-be3c-a332edf02e24
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/23/2017
ms.author: jdial
ms.openlocfilehash: 55ae6a131d882ad893aeffcaa4127bc47beda552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-network"></a>Rete virtuale di Azure

Hello consente di servizio di rete virtuale di Azure è toosecurely tooeach altre risorse di Azure di connettersi con le reti virtuali (Vnet). Una rete virtuale è una rappresentazione della rete nel cloud hello. Una rete virtuale è un isolamento logico di hello sottoscrizione tooyour cloud di Azure dedicato. È inoltre possibile connettere una rete locale tooyour di reti virtuali. Hello seguente immagine illustra alcune funzionalità di hello di hello del servizio di rete virtuale di Azure:

![Diagramma di rete](./media/virtual-networks-overview/virtual-network-overview.png)

toolearn ulteriori informazioni su hello seguenti funzionalità di rete virtuale di Azure, fare clic su funzionalità hello:
- **[Isolamento:](#isolation)** le reti virtuali sono isolate una dall'altra. È possibile creare reti virtuali separate per lo sviluppo, test e produzione che hello utilizzare blocchi di indirizzi CIDR stesso. È altrimenti possibile creare più reti virtuali che usano blocchi di indirizzi CIDR diversi e connettere tra loro le reti. Una rete virtuale può essere segmentata in più subnet. Azure fornisce la risoluzione dei nomi interna per le macchine virtuali e istanze del ruolo di servizi Cloud connesso tooa rete virtuale. È possibile configurare facoltativamente toouse una rete virtuale dei propri server DNS, anziché utilizzare la risoluzione dei nomi interno di Azure.
- **[Connettività Internet:](#internet)**  accederanno a tutte le macchine virtuali (VM) di Azure e servizi Cloud le istanze del ruolo sono connesso tooa rete virtuale toohello Internet, per impostazione predefinita. È inoltre possibile abilitare le risorse toospecific di accesso in ingresso, in base alle esigenze.
- **[Connettività a risorse di Azure:](#within-vnet)**  risorse, ad esempio servizi Cloud e macchine virtuali di Azure possono essere connesso toohello stessa rete virtuale. le risorse di Hello possono connettersi tooeach altri indirizzi IP privati, anche se sono presenti in subnet diverse. Azure offre predefinito routing tra subnet, le reti virtuali e reti locali, in modo da non avere tooconfigure e gestire le route.
- **[Connettività tra reti virtuali:](#connect-vnets)**  reti virtuali possono essere connesso tooeach altri, l'abilitazione di risorse connessa tooany toocommunicate di rete virtuale con qualsiasi risorsa di qualsiasi altra rete virtuale.
- **[Connettività locale:](#connect-on-premises)**  reti virtuali possono essere reti locali tooon connessi tramite connessioni di rete privata tra la rete e Azure o tramite una connessione VPN site-to-site over hello Internet.
- **[Applicazione di filtri al traffico:](#filtering)** il traffico di rete delle VM e delle istanze del ruolo Servizi cloud può essere filtrato in ingresso e in uscita per indirizzo IP e porta di origine, indirizzo IP e porta di destinazione e protocollo.
- **[Routing:](#routing)** facoltativamente, è possibile sostituire il routing predefinito di Azure configurando route personalizzate o usando route BGP attraverso un gateway di rete.

## <a name = "isolation"></a>Isolamento e segmentazione delle reti

È possibile implementare più reti virtuali in ogni [sottoscrizione](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription) e [area](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#region) di Azure. Ogni rete virtuale è isolata dalle altre. Per ogni rete virtuale è possibile:
- Specificare uno spazio indirizzi IP privato personalizzato con indirizzi pubblici e privati (RFC 1918). Azure Assegna risorse connesso toohello rete virtuale un indirizzo IP privato da assegnare spazio di indirizzi di hello.
- Segmento hello rete virtuale in uno o più subnet e allocare una parte della subnet di tooeach spazio di indirizzi di hello rete virtuale.
- Utilizzare la risoluzione dei nomi fornita da Azure oppure specificare che server DNS per l'utilizzo da risorse connesso tooa rete virtuale. ulteriori informazioni sulla risoluzione dei nomi in reti virtuali, leggere hello toolearn [risoluzione dei nomi per le macchine virtuali e servizi Cloud](virtual-networks-name-resolution-for-vms-and-role-instances.md) articolo.

## <a name = "internet"></a>Connettersi a Internet toohello
Tutte le risorse collegate tooa rete virtuale dispone di connettività in uscita toohello Internet per impostazione predefinita. indirizzo IP privato Hello della risorsa hello è l'indirizzo di rete di origine convertito (SNAT) tooa indirizzo IP da hello dell'infrastruttura di Azure. ulteriori informazioni sulla connettività Internet in uscita, leggere hello toolearn [informazioni sulle connessioni in uscita in Azure](..\load-balancer\load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json#standalone-vm-with-no-instance-level-public-ip-address) articolo. È possibile modificare la connettività predefinito hello implementando routing personalizzato e filtrare il traffico.

toocommunicate in ingresso risorse tooAzure hello Internet o toocommunicate toohello in uscita deve essere assegnato un indirizzo IP pubblico a Internet senza SNAT, una risorsa. informazioni su indirizzi IP pubblici, leggere hello toolearn [gli indirizzi IP pubblici](virtual-network-public-ip-address.md) articolo.

## <a name="within-vnet"></a>Connettere risorse di Azure
È possibile connettere più risorse di Azure tooa rete virtuale, ad esempio macchine virtuali (VM), servizi Cloud, gli ambienti del servizio App e il set di scalabilità di macchine virtuali. Macchine virtuali si connettono tooa subnet all'interno di una rete virtuale tramite un'interfaccia di rete (NIC). altre informazioni sulle schede di rete, leggere hello toolearn [interfacce di rete](virtual-network-network-interface.md) articolo.

## <a name="connect-vnets"></a>Connettere reti virtuali

È possibile connettere reti virtuali tooeach altri, l'abilitazione di risorse collegato tooeither toocommunicate di rete virtuale tra loro attraverso reti virtuali. È possibile utilizzare uno o entrambi hello opzioni tooconnect reti virtuali tooeach altri seguenti:
- **Peering:** risorse Abilita connesso toodifferent reti virtuali di Azure all'interno di hello stesso toocommunicate località di Azure tra loro. Hello larghezza di banda e latenza tra reti virtuali sono hello hello stesso come se le risorse di hello erano connesso toohello stessa rete virtuale. toolearn ulteriori informazioni su peering, leggere hello [peering di rete virtuale](virtual-network-peering-overview.md) articolo.
- **Connessione di rete virtuale a:** risorse Abilita connesso toodifferent rete virtuale di Azure all'interno di hello uguali o diversi percorsi di Azure. A differenza del peering, la larghezza di banda tra le reti virtuali è limitata perché il traffico deve passare attraverso un gateway VPN di Azure. ulteriori informazioni sulla connessione di reti virtuali con una connessione di rete virtuale a, leggere hello toolearn [configurare una connessione di rete virtuale a](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) articolo.

## <a name="connect-on-premises"></a>La connessione di rete locale tooan

È possibile connettere il tooa di rete locale virtuale usando qualsiasi combinazione di hello le opzioni seguenti:
- **Rete privata virtuale (VPN) Point-to-site:** stabilita tra una singola rete connessa tooyour PC e hello rete virtuale. Questo tipo di connessione è molto utile se principianti con Azure o per gli sviluppatori, perché richiede senza modifiche tooyour una rete esistente. connessione Hello Usa la comunicazione di tooprovide crittografato hello SSTP protocollo su hello Internet tra hello PC e hello rete virtuale. latenza Hello per una VPN point-to-site è imprevedibile, poiché il traffico di hello attraversa hello Internet.
- **VPN da sito a sito:** viene stabilita una connessione tra il dispositivo VPN e un gateway VPN di Azure. Questo tipo di connessione consente a qualsiasi risorsa locale, si autorizza tooaccess una rete virtuale. connessione di Hello è una VPN IPSec/IKE che fornisce comunicazioni crittografate tramite hello Internet tra il dispositivo locale e il gateway VPN di Azure hello. latenza Hello per una connessione site-to-site è imprevedibile, poiché il traffico di hello attraversa hello Internet.
- **Azure ExpressRoute:** viene stabilita una connessione tra la rete e Azure tramite un partner ExpressRoute. La connessione è privata. Il traffico non attraversa hello Internet. latenza Hello per una connessione ExpressRoute è prevedibile, poiché il traffico non deve attraversare hello Internet.

informazioni su tutte le hello connessione opzioni precedenti, leggere hello toolearn [diagrammi della topologia di connessione](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#diagrams) articolo.

## <a name="filtering"></a>Filtrare il traffico di rete
È possibile filtrare il traffico di rete tra subnet utilizzando uno o entrambi hello le opzioni seguenti:
- **Gruppi di sicurezza (gruppo) di rete:** ogni gruppo può contenere più regole di sicurezza in ingresso e in uscita che consentono il traffico toofilter dal protocollo, porta e indirizzo IP di origine e destinazione. È possibile applicare un tooeach gruppo NIC in una macchina virtuale. È inoltre possibile applicare una subnet toohello NSG una scheda di rete o altre risorse di Azure, è connesso. ulteriori informazioni sulla NSGs, leggere hello toolearn [gruppi di sicurezza di rete](virtual-networks-nsg.md) articolo.
- **Appliance virtuali di rete:** un'appliance virtuale di rete è una VM che esegue software con un funzione di rete, ad esempio un firewall. Visualizzare un elenco di NVAs disponibile in hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/category/networking?page=1&subcategories=appliances). Sono anche disponibili appliance virtuali di rete che eseguono l'ottimizzazione WAN e altre funzioni per il traffico di rete. Le appliance virtuali di rete vengono in genere usate con route BGP o definite dall'utente. È inoltre possibile utilizzare un traffico toofilter NVA tra reti virtuali.

## <a name="routing"></a>Instradare il traffico di rete

Azure crea le tabelle di route che consentono le risorse subnet tooany connesso toocommunicate qualsiasi rete virtuale tra loro, per impostazione predefinita. È possibile implementare uno o entrambi i seguenti opzioni toooverride hello hello route predefinite che Azure crea:
- **Le route definite dall'utente:** è possibile creare tabelle di routing personalizzata con le route che controllano in cui il traffico viene indirizzato toofor ogni subnet. altre informazioni sulle route definite dall'utente, leggere hello toolearn [le route definite dall'utente](virtual-networks-udr-overview.md) articolo.
- **Le route BGP:** se ci si connette la rete locale tooyour di rete virtuale utilizzando una connessione Gateway VPN di Azure o ExpressRoute, è possibile propagare tooyour delle route BGP reti virtuali.

## <a name="pricing"></a>Prezzi

Per le reti virtuali, le subnet, le tabelle di route e i gruppi di sicurezza di rete non è previsto alcun addebito. All'utilizzo della larghezza di banda Internet in uscita, agli indirizzi IP pubblici, al peering reti virtuali, ai gateway VPN e a ExpressRoute vengono applicate specifiche strutture di prezzi. Hello vista [rete virtuale](https://azure.microsoft.com/pricing/details/virtual-network), [Gateway VPN](https://azure.microsoft.com/pricing/details/vpn-gateway), e [ExpressRoute](https://azure.microsoft.com/pricing/details/expressroute) prezzi pagine per altre informazioni.

## <a name="faq"></a>domande frequenti

tooreview domande frequenti sulla rete virtuale, vedere hello [domande frequenti sulla rete virtuale](virtual-networks-faq.md) articolo.


## <a name="next-steps"></a>Passaggi successivi

- Creare una rete virtuale di prima e connettersi qualche tooit di macchine virtuali, completando i passaggi hello hello [creare la prima rete virtuale](virtual-network-get-started-vnet-subnet.md) articolo.
- Creare una rete virtuale di tooa connessione point-to-site completando i passaggi hello hello [configurare una connessione point-to-site](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) articolo.
- Informazioni su alcune delle hello altre chiavi [funzionalità di rete](../networking/networking-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json) di Azure.
