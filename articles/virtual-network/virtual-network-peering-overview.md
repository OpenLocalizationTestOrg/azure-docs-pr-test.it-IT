---
title: peering reti virtuali aaaAzure | Documenti Microsoft
description: Informazioni sul peering reti virtuali in Azure.
services: virtual-network
documentationcenter: na
author: NarayanAnnamalai
manager: jefco
editor: tysonn
ms.assetid: eb0ba07d-5fee-4db0-b1cb-a569b7060d2a
ms.service: virtual-network
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: narayan
ms.openlocfilehash: 46a14b416a7d4389f79a3cd7c55e388b5d312577
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-network-peering"></a>Peering di rete virtuale
Rete virtuale consente di peering hello di si tooconnect due reti virtuali nella stessa area geografica tramite hello rete backbone di Azure. Una volta il peering, due reti virtuali hello visualizzata come una sola, per scopi di connettività. reti virtuali Hello due vengono ancora gestite come risorse diverse, ma le macchine virtuali in hello peering reti virtuali possono comunicare tra loro direttamente, utilizzando gli indirizzi IP privati.

il traffico tra macchine virtuali in hello Hello peering reti virtuali viene instradato tramite l'infrastruttura di Azure, proprio come il traffico viene instradato tra macchine virtuali in hello hello stessa rete virtuale. Alcuni dei vantaggi di hello dell'utilizzo di peering di rete virtuale:

* Connessione a bassa latenza e larghezza di banda elevata tra le risorse in reti virtuali diverse.
* Hello possibilità toouse risorse come dispositivi di rete e i gateway VPN come punti di transito in una rete virtuale peered.
* Hello possibilità toopeer due reti virtuali create con modello di distribuzione Azure Resource Manager hello o toopeer una rete virtuale viene creata attraverso la rete virtuale di gestione risorse tooa creato tramite il modello di distribuzione classica hello. Hello lettura [modelli di distribuzione Azure comprendere](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) toolearn articolo ulteriori informazioni sulle differenze di hello tra i modelli di distribuzione di Azure hello due.

## <a name="requirements-constraints"></a>Requisiti e vincoli

* Hello peering reti virtuali devono esistere in hello stessa regione di Azure. È possibile connettere reti virtuali in diverse aree di Azure usando un [gateway VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V).
* Hello peering reti virtuali è necessario spazi di indirizzi IP non sovrapposte.
* Non è possibile aggiungere o eliminare spazi di indirizzi da una rete virtuale dopo che ne è stato effettuato il peering con un'altra rete virtuale.
* Il peering viene eseguito tra due reti virtuali senza alcuna relazione transitiva derivata nei peering. Ad esempio, se virtualNetworkA è stato effettuato il peering con virtualNetworkB e virtualNetworkB è stato effettuato il peering con virtualNetworkC, virtualNetworkA è *non* toovirtualNetworkC peering.
* È possibile connettersi a reti virtuali presenti in due diverse sottoscrizioni, come tempo un utente con privilegi (vedere [autorizzazioni specifiche](create-peering-different-deployment-models-subscriptions.md#permissions)) di entrambe le sottoscrizioni autorizza peering hello e le sottoscrizioni di hello sono associato toohello stesso Tenant di Azure Active Directory. È possibile utilizzare un [Gateway VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V) tooconnect reti virtuali in sottoscrizioni associate toodifferent tenant di Active Directory.
* Se entrambi vengono creati tramite il modello di distribuzione del hello Gestione risorse o se viene creata una rete virtuale e modello di distribuzione di gestione risorse di hello e hello altri viene creato tramite il modello di distribuzione classica hello, è possano peering reti virtuali. Due reti virtuali create tramite il modello di distribuzione classica hello non possono essere tuttavia il peering tooeach altre. È possibile utilizzare un [Gateway VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V) tooconnect due reti virtuali create tramite il modello di distribuzione classica hello.
* Se la comunicazione tra macchine virtuali in reti virtuali peering hello non presenta alcuna restrizione di larghezza di banda aggiuntiva, sussiste una larghezza di banda di rete massima a seconda delle dimensioni della macchina virtuale che si applica comunque hello. ulteriori informazioni sulla larghezza di banda di rete massima per le dimensioni di macchina virtuale diversa, leggere hello toolearn [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) o [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) gli articoli di dimensioni di macchina virtuale.
* La risoluzione dei nomi DNS interni fornita da Azure per le macchine virtuali non funziona tra le reti virtuali con peering. Macchine virtuali hanno nomi DNS interni che fanno risolubile solo all'interno di rete virtuale locale hello. È tuttavia possibile configurare le reti virtuali di macchine virtuali connesse toopeered come server DNS per una rete virtuale. Per ulteriori informazioni, leggere hello [risoluzione dei nomi utilizzando il proprio server DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) articolo.

![Peering di rete virtuale di base](./media/virtual-networks-peering-overview/figure01.png)

## <a name="connectivity"></a>Connettività
Dopo due reti virtuali sono il peering, le risorse in una rete virtuale possono connettersi direttamente con le risorse di rete virtuale di peering hello. reti virtuali Hello due hanno completo IP a livello di connettività.

latenza di rete Hello per è un round trip tra due macchine virtuali in reti virtuali peering hello uguale a quello di un round trip all'interno di una singola rete virtuale. velocità effettiva della rete Hello dipende dalla larghezza di banda hello è consentito per la macchina virtuale hello, dimensioni tooits proporzionale. Non vi è alcuna restrizione sulla larghezza di banda all'interno di peering hello aggiuntive.

il traffico tra macchine virtuali in reti virtuali peering Hello viene indirizzato direttamente tramite hello Azure infrastruttura di back-end, non tramite un gateway.

Rete virtuale connessa tooa di macchine virtuali può accedere hello con bilanciamento del carico endpoint interni nella rete virtuale di peering hello. Gruppi di sicurezza di rete possono essere applicati nella rete virtuale tooblock accesso tooother le reti virtuali o le subnet, se desiderato.

Quando si configura il peering di rete virtuale, è possibile aprire o chiudere regole gruppo di sicurezza rete hello tra reti virtuali hello. Se si apre completa connettività tra reti virtuali peering (che è l'opzione predefinita hello), è possibile applicare rete sicurezza gruppi toospecific subnet o le macchine virtuali tooblock o negare l'accesso specifico. gruppi di sicurezza di rete toolearn altre informazioni sulla lettura hello [Panoramica di gruppi di sicurezza di rete](virtual-networks-nsg.md) articolo.

## <a name="service-chaining"></a>Concatenamento dei servizi
È possibile configurare le route definite dall'utente che computer toovirtual punto peering reti virtuali come hello "hop successivo" IP indirizzo tooenable il concatenamento di servizi. Consente il concatenamento di servizio si toodirect traffico da un dispositivo virtuale in tooa rete virtuale in una rete virtuale peered tramite le route definite dall'utente.

Anche in modo efficace, è possibile creare ambienti di tipo hub e spoke, in cui hub hello può ospitare i componenti dell'infrastruttura, ad esempio un dispositivo di rete virtuale. Tutte le reti virtuali spoke hello quindi è possono connettersi con la rete virtuale di hello hub. Il traffico tramite dispositivi virtuali di rete che sono in esecuzione nella rete virtuale di hello hub. In breve, peering reti virtuali consente hello indirizzo IP hop successivo sull'indirizzo IP di una macchina virtuale nella rete virtuale di peering hello hello definito dall'utente route toobe hello. altre informazioni sulle route definite dall'utente, leggere hello toolearn [panoramica delle route definite dall'utente](virtual-networks-udr-overview.md) articolo.

## <a name="gateways-and-on-premises-connectivity"></a>Gateway e connettività locale
Ogni rete virtuale, indipendentemente dal fatto è il peering con un'altra rete virtuale, può comunque dispone di un proprio gateway e utilizzarlo come rete di tooconnect tooan locale. È inoltre possibile configurare [le connessioni di rete virtuale di rete virtuale](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json) mediante gateway, anche se sono peering reti virtuali hello.

Quando vengono configurate entrambe le opzioni l'interconnessione di rete virtuale, il traffico tra reti virtuali hello hello viene convogliato tramite la configurazione di peering hello (vale a dire tramita hello backbone di Azure).

Quando sono peering reti virtuali, è possibile configurare il gateway hello come una rete di transito tooan punto locale nella rete virtuale di peering hello. In questo caso, rete virtuale hello che utilizza un gateway remoto non può avere un proprio gateway. Una rete virtuale può avere un solo gateway, gateway Hello può essere un gateway locale o remoto (hello peering rete virtuale), come illustrato nella seguente immagine hello:

![Peering reti virtuali con transito](./media/virtual-networks-peering-overview/figure02.png)

Transito gateway non è supportato nella relazione di peering hello tra reti virtuali create tramite diversi modelli di distribuzione. Entrambe le reti virtuali in una relazione di peering hello devono essere state create tramite Gestione risorse per toowork di transito un gateway.

Quando sono peering reti virtuali hello che condividono una sola connessione Azure ExpressRoute, hello tra di essi del traffico tramite una relazione di peering hello (vale a dire tramita hello rete backbone di Azure). Comunque, è possibile utilizzare il gateway locale in ogni circuito di rete virtuale tooconnect toohello locale. oppure usare un gateway condiviso e configurare il transito per la connettività locale.

## <a name="provisioning"></a>Provisioning
Il peering di rete virtuale è un'operazione con privilegi. È una funzione separata nello spazio dei nomi VirtualNetworks hello. Un utente può essere fornita peering tooauthorize diritti specifici. Un utente che dispone di rete virtuale di accesso in lettura-scrittura toohello eredita automaticamente questi diritti.

Un utente che sia un amministratore o un utente con privilegi di possibilità di peering hello è possibile avviare un'operazione di peering su un'altra rete virtuale. Se esiste una corrispondenza richiesta per il peering in hello altro lato, e se vengono soddisfatti altri requisiti, hello peering viene stabilito.

## <a name="limits"></a>Limiti
Vi sono limiti al numero di hello di peering consentiti per una singola rete virtuale. Per ulteriori informazioni, esaminare hello [i limiti di rete di Azure](../azure-subscription-service-limits.md#networking-limits).

## <a name="pricing"></a>Prezzi
È previsto un importo minimo per il traffico in ingresso e in uscita che usa un peering di rete virtuale. Per ulteriori informazioni, vedere hello [pagina dei prezzi](https://azure.microsoft.com/pricing/details/virtual-network).

## <a name="next-steps"></a>Passaggi successivi

* Completare un'esercitazione sul peering di reti virtuali. Un peering di rete virtuale verrà creato tra reti virtuali create tramite hello stesso o diversi modelli di distribuzione esistenti in hello sottoscrizioni uguale o diverse. Completare un'esercitazione per uno dei seguenti scenari hello:
 
    |Modello di distribuzione di Azure  | Subscription  |
    |---------|---------|
    |Entrambi Resource Manager |[Uguale](virtual-network-create-peering.md)|
    | |[Diversa](create-peering-different-subscriptions.md)|
    |Uno di Resource Manager, uno della versione classica     |[Uguale](create-peering-different-deployment-models.md)|
    | |[Diversa](create-peering-different-deployment-models-subscriptions.md)|

* Informazioni su come toocreate un [topologia di rete hub e spoke](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) 
* Altre informazioni su tutti [impostazioni peer della rete virtuale e come toochange li](virtual-network-manage-peering.md)
