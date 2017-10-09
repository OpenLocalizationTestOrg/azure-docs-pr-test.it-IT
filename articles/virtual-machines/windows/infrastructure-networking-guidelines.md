---
title: linee guida infrastruttura - Windows networking aaaAzure | Documenti Microsoft
description: Informazioni su hello progettazione e implementazione di linee guida fondamentali per la distribuzione di rete virtuale in servizi di infrastruttura di Azure.
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e2d45973-5eba-4904-8ba0-1821f64feed7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 64c288957e7c7b89578d871a74ff45ce470ed922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-networking-infrastructure-guidelines-for-windows-vms"></a>Linee guida sull'infrastruttura di rete di Azure per macchine virtuali Windows 

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

Questo articolo è incentrato su hello comprensione necessari passaggi per la rete virtuale in Azure e la connettività tra ambienti locali esistenti di pianificazione.

## <a name="implementation-guidelines-for-virtual-networks"></a>Linee guida di implementazione per reti virtuali
Decisioni:

* Il tipo di rete virtuale è necessario toohost il carico di lavoro IT o dell'infrastruttura (solo cloud o cross-premise)?
* Per le reti virtuali cross-premise, quanto spazio di indirizzi è necessario macchine virtuali e subnet hello toohost ora e per l'espansione ragionevole in hello futuri?
* Sono lo scopo toocreate centralizzata delle reti virtuali o Crea reti virtuali singoli per ogni gruppo di risorse?

Attività:

* Definire spazio di indirizzi hello hello reti virtuali toobe creato.
* Definire hello set di subnet e lo spazio degli indirizzi di hello per ognuno.
* Per le reti virtuali cross-premise, definire il set di hello di spazi degli indirizzi di rete locale per le località locale hello hello macchine virtuali in tooreach necessità di hello rete virtuale.
* Utilizzo locale rete team tooensure hello appropriato il routing viene configurato durante la creazione di reti virtuali cross-premise.
* Creare una rete virtuale di hello utilizzando la convenzione di denominazione.

## <a name="virtual-networks"></a>Reti virtuali
Le reti virtuali sono necessarie toosupport le comunicazioni tra macchine virtuali (VM). Come avviene con le reti fisiche, è possibile definire subnet, indirizzo IP personalizzato, impostazioni DNS, filtro di protezione e bilanciamento del carico. Utilizzando un [gateway VPN](../../vpn-gateway/vpn-gateway-about-vpngateways.md) o [circuito Express Route](../../expressroute/expressroute-introduction.md), è possibile connettere reti virtuali di Azure tooyour sulle reti locali. Altre informazioni sulle [reti virtuali e sui relativi componenti](../../virtual-network/virtual-networks-overview.md).

L'uso dei gruppi di risorse offre maggiore flessibilità alla progettazione dei componenti di rete virtuali. Macchine virtuali possono connettersi a reti toovirtual all'esterno del gruppo di risorse. Un approccio di progettazione comune sarebbe toocreate centralizzato i gruppi di risorse che contengono l'infrastruttura di rete core che può essere gestito da un team comune, e quindi le macchine virtuali e le relative applicazioni distribuite tooseparate gruppi di risorse. Questo approccio consente l'accesso i proprietari delle applicazioni toohello gruppo di risorse contenente le proprie macchine virtuali senza dover aprire la configurazione di accesso toohello di hello più ampio virtuale le risorse di rete.

## <a name="site-connectivity"></a>Connettività del sito
### <a name="cloud-only-virtual-networks"></a>Reti virtuali solo cloud
Se i computer e utenti locali non richiedono la connettività in corso tooVMs in una rete virtuale di Azure, la progettazione della rete virtuale è semplice:

![Diagramma rete virtuale di base solo cloud](./media/infrastructure-networking-guidelines/vnet01.png)

Questo approccio è in genere indicato per i carichi di lavoro con connessione Internet, come nel caso di un server Web basato su Internet. È possibile gestire queste VM tramite RDP o connessioni VPN da punto a sito.

Perché non si connettano rete locale tooyour, solo Azure reti virtuali possono utilizzare qualsiasi parte dello spazio di indirizzi IP privato hello, anche se hello stesso spazio privato è in utilizzate in locale.

### <a name="cross-premises-virtual-networks"></a>Reti virtuali cross-premise
Se i computer e utenti locali richiedono tooVMs connettività in corso in una rete virtuale di Azure, creare una rete virtuale cross-premise.  Connessione rete locale tooyour con un ExpressRoute o una connessione VPN da sito a sito.

![Diagramma rete virtuale cross-premise](./media/infrastructure-networking-guidelines/vnet02.png)

In questa configurazione, hello rete virtuale di Azure è essenzialmente un'estensione basata su cloud della rete locale.

Dal momento che si connettono tooyour rete locale, tra più sedi, le reti virtuali è necessario usare una parte dello spazio di indirizzi hello utilizzato dall'organizzazione che è univoco. In hello stesso modo che sedi aziendali diverse vengono assegnate una subnet IP specifica, Azure diventa un'altra posizione se si estende fuori della rete.

tooallow tootravel di pacchetti dalla rete locale tooyour rete virtuale cross-premise, è necessario configurare il set di hello rilevanti on-premise di prefissi di indirizzo come parte della definizione di rete locale hello per la rete virtuale hello. A seconda di indirizzo hello spazio hello virtuale rete hello set e di rilevanti locale percorsi, possono esistere molte prefissi di indirizzi della rete locale hello.

È possibile convertire una rete virtuale di rete virtuale solo cloud tooa cross-premise, ma è più probabile che richiede è IP toore spazio degli indirizzi di rete virtuale e alle risorse di Azure. Pertanto, valutare attentamente se una rete virtuale è necessario rete locale di toobe tooyour connessi quando si assegna una subnet IP.

## <a name="subnets"></a>Subnet
Queste ultime consentono di tooorganize risorse correlate, ovvero in modo logico (ad esempio, una subnet per le macchine virtuali associate toohello stessa applicazione), o fisicamente (ad esempio, una subnet per ogni gruppo di risorse). È anche possibile ricorrere a tecniche di isolamento subnet per una maggiore sicurezza.

Per le reti virtuali cross-premise, è necessario progettare subnet con hello stesse convenzioni utilizzate per le risorse locali. **Azure sempre utilizza hello primi tre indirizzi IP hello dello spazio degli indirizzi per ogni subnet**. numero di hello toodetermine di indirizzi necessari per la subnet hello, avviare contando il numero di hello di macchine virtuali che è ora necessario. Stima per la crescita futura e quindi utilizzare hello dimensioni della subnet hello hello toodetermine della tabella seguente.

| Numero di macchine virtuali necessarie | Numero di bit di host necessari | Dimensioni della subnet hello |
| --- | --- | --- |
| 1-3 |3 |/29 |
| 4–11 |4 |/28 |
| 12–27 |5 |/27 |
| 28–59 |6 |/26 |
| 60–123 |7 |/25 |

> [!NOTE]
> Per la subnet locale normale, numero massimo di hello di indirizzi di host per una subnet con i bit host n è 2<sup> n </sup> : 2. Per una subnet di Azure, numero massimo di hello di indirizzi di host per una subnet con i bit host n è 2<sup> n </sup> – 5 (2 e 3 per gli indirizzi di hello che utilizza Azure su ciascuna subnet).
> 
> 

Se si sceglie una subnet con dimensioni troppo piccolo, ha toore IP e ridistribuire hello macchine virtuali nella subnet hello.

## <a name="network-security-groups"></a>Gruppi di sicurezza di rete
È possibile applicare filtrando il traffico toohello regole che passano attraverso le reti virtuali utilizzando i gruppi di sicurezza di rete. È possibile compilare granulare toosecure regole filtro all'ambiente di rete virtuale, il controllo in entrata e in uscita del traffico, origine e destinazione intervalli IP consentito di porte e così via. Gruppi di sicurezza di rete può essere applicato toosubnets all'interno di una rete virtuale o direttamente tooa interfaccia di rete virtuale. È consigliabile toohave un certo livello di gruppo di sicurezza di rete filtrare il traffico sulle reti virtuali. Altre informazioni sulle [Gruppi di sicurezza di rete](../../virtual-network/virtual-networks-nsg.md).

## <a name="additional-network-components"></a>Componenti di rete aggiuntivi
Come accade in un'infrastruttura di rete locale fisica, la rete virtuale di Azure non contiene necessariamente solo subnet e indirizzi IP. Quando si progetta l'infrastruttura dell'applicazione, è opportuno tooincorporate alcuni di questi componenti aggiuntivi:

* [Gateway VPN](../../vpn-gateway/vpn-gateway-about-vpngateways.md) -connettere reti virtuali di Azure tooother virtuali di Azure reti o connettersi a reti locali tooon tramite una connessione VPN da sito a sito. Per connessioni dedicate e sicure, implementare connessioni di Express Route. È anche possibile offrire l'accesso diretto agli utenti con connessioni VPN da punto a sito.
* [Bilanciamento del carico](../../load-balancer/load-balancer-overview.md) - Offre il bilanciamento del carico del traffico per il traffico interno ed esterno in base alle esigenze.
* [Gateway applicazione](../../application-gateway/application-gateway-introduction.md) : HTTP con bilanciamento del carico a livello di applicazione hello, che fornisce alcuni vantaggi aggiuntivi per le applicazioni web anziché la distribuzione di bilanciamento del carico Azure hello.
* [Gestione traffico](../../traffic-manager/traffic-manager-overview.md) - basato su DNS distribuzione toodirect gli utenti finali toohello endpoint più vicino disponibile dell'applicazione, consentendo di toohost il traffico dell'applicazione da Data Center di Azure in aree diverse.

## <a name="next-steps"></a>Passaggi successivi
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

