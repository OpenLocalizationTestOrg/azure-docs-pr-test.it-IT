---
title: "aaaOverview delle configurazioni a disponibilità elevata con gateway VPN di Azure | Documenti Microsoft"
description: "Questo articolo offre una panoramica delle opzioni di configurazione a disponibilità elevata con gateway VPN di Azure."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: a8bfc955-de49-4172-95ac-5257e262d7ea
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/24/2016
ms.author: yushwang
ms.openlocfilehash: 316293b9ac79645bf9bb9e89fbc4aa8f3eacd209
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="highly-available-cross-premises-and-vnet-to-vnet-connectivity"></a>Connettività cross-premise e da rete virtuale a rete virtuale a disponibilità elevata
Questo articolo offre una panoramica delle opzioni di configurazione a disponibilità elevata per la connettività cross-premise e da rete virtuale a rete virtuale con gateway VPN di Azure.

## <a name = "activestandby"></a>Informazioni sulla ridondanza dei gateway VPN di Azure
Ogni gateway VPN di Azure è costituito da due istanze in una configurazione di tipo attivo-standby. Per interventi di manutenzione pianificata o non pianificato interruzione che si verifica istanze attive toohello, istanza standby hello sarebbe assumerà automaticamente il controllo (failover) e riprendere hello VPN S2S o connessioni di rete virtuale a. passare Hello causerà una breve interruzione. Per la manutenzione pianificata, connettività hello devono essere ripristinate entro 10 secondi too15. Per problemi non pianificati, ripristino della connessione hello sarà più lungo, su 1 too1 minuti e mezzo minuti nel caso peggiore hello. Per il gateway VPN P2S di toohello le connessioni client, è necessario tooreconnect dai computer client hello utenti hello e connessioni P2S hello verranno disconnesso.

![Attivo-standby](./media/vpn-gateway-highlyavailable/active-standby.png)

## <a name="highly-available-cross-premises-connectivity"></a>Connettività cross-premise a disponibilità elevata
tooprovide una migliore disponibilità per il cross locali connessioni, sono disponibili due opzioni:

* Più dispositivi VPN locali
* Gateway VPN di Azure di tipo attivo-attivo
* Combinazione di entrambe le opzioni

### <a name = "activeactiveonprem"></a>Più dispositivi VPN locali
È possibile utilizzare più dispositivi VPN dal gateway locale rete tooconnect tooyour VPN di Azure, come illustrato nel seguente diagramma hello:

![Più dispositivi VPN locali](./media/vpn-gateway-highlyavailable/multiple-onprem-vpns.png)

Questa configurazione fornisce più tunnel attivi da hello stesso Azure VPN gateway tooyour dispositivi locali in hello nello stesso percorso. Esistono alcuni requisiti e vincoli:

1. È necessario toocreate più connessioni VPN S2S dal tooAzure dispositivi VPN. Quando ci si connettono a più dispositivi VPN da hello tooAzure di rete locale stesso, è necessario toocreate un gateway di rete locale per ogni dispositivo VPN e una connessione dal gateway VPN di Azure gateway toohello rete locale.
2. gateway di rete locale Hello corrispondente dispositivi VPN tooyour deve avere gli indirizzi IP pubblici univoci nella proprietà "GatewayIpAddress" hello.
3. Per questa configurazione è necessario BGP. Ogni gateway di rete locale che rappresenta un dispositivo VPN deve avere un indirizzo IP peer BGP univoco specificato nella proprietà "BgpPeerIpAddress" hello.
4. campo di proprietà AddressPrefix Hello in ogni gateway di rete locale non deve sovrapporsi. È necessario specificare "BgpPeerIpAddress" hello in /32 formato CIDR nel campo AddressPrefix hello, ad esempio, 10.200.200.254/32.
5. È consigliabile utilizzare il protocollo BGP tooadvertise hello stesso prefissi di hello locale stesso gateway VPN di Azure tooyour di prefissi di rete e hello traffico verrà inoltrato tramite questi tunnel contemporaneamente.
6. Ogni connessione viene conteggiato rispetto al numero massimo di hello di tunnel per il gateway VPN di Azure, Basic e Standard SKU, 10 e 30 per HighPerformance SKU. 

In questa configurazione, i gateway VPN di Azure hello è ancora in modalità attivo-standby, pertanto hello stesso comportamento di failover e brevi interruzioni verranno comunque eseguito come descritto [sopra](#activestandby). Questa configurazione protegge tuttavia da errori o interruzioni nella rete locale e nei dispositivi VPN.

### <a name="active-active-azure-vpn-gateway"></a>Gateway VPN di Azure di tipo attivo-attivo
È ora possibile creare un gateway VPN di Azure in una configurazione attivo-attivo, in cui entrambe le istanze del gateway hello che macchine virtuali stabiliranno che dispositivo VPN locale tooyour i tunnel VPN S2S come mostrato hello seguente diagramma:

![Attivo-attivo](./media/vpn-gateway-highlyavailable/active-active.png)

In questa configurazione, ogni istanza del gateway di Azure avrà un indirizzo IP pubblico univoco e ogni consentirà di stabilire un dispositivo VPN S2S IPsec/IKE tunnel tooyour locale VPN specificato in una connessione e il gateway di rete locale. Si noti che entrambi i tunnel VPN sono effettivamente una parte di hello stessa connessione. Verrà comunque tooconfigure il tooaccept di dispositivo VPN locale o se stabilire due VPN S2S tunnel toothose due Azure VPN gateway gli indirizzi IP pubblici.

Poiché le istanze di Azure gateway hello nella configurazione attivo-attivo, il traffico di hello da tooyour la rete virtuale di Azure locale rete verrà instradata tramite i tunnel entrambi contemporaneamente, anche se il dispositivo VPN locale potrebbe preferire un tunnel Hello altri. Si noti anche se hello passerà sempre dello stesso flusso TCP o UDP hello stesso tunnel o percorso, a meno che non si verifica un evento di manutenzione su una delle istanze di hello.

Una manutenzione pianificata o un evento non pianificato caso l'istanza del gateway tooone, tunnel IPsec hello da tale istanza di tooyour locale verrà disconnesso dispositivo VPN. Hello route corrispondente nei dispositivi VPN devono essere rimossi o ritirate automaticamente in modo che il traffico hello verrà trasferito su toohello altri active tunnel IPsec. Sul lato Azure hello, passare hello verrà eseguita automaticamente da hello interessato toohello active istanza.

### <a name="dual-redundancy-active-active-vpn-gateways-for-both-azure-and-on-premises-networks"></a>Doppia ridondanza: gateway VPN di tipo attivo-attivo sia per Azure che per le reti locali
la soluzione più affidabile Hello è gateway attivo-attivo di hello toocombine in rete e Azure, come illustrato nel seguente diagramma di hello.

![Doppia ridondanza](./media/vpn-gateway-highlyavailable/dual-redundancy.png)

Qui creare il gateway VPN di Azure hello in una configurazione attivo-attivo del programma di installazione e creare due gateway di rete locale e due connessioni per i due VPN dispositivi locali come descritto in precedenza. risultato Hello è disponibile una connettività a maglia completa di 4 tunnel IPsec tra la rete virtuale di Azure e la rete locale.

Tutti i gateway e i tunnel sono attivi da hello lato Azure, in modo che sia il traffico hello distribuiti a tutti i 4 tunnel contemporaneamente, anche se ogni TCP o UDP flusso nuovamente seguire hello tunnel stesso o percorso dalla hello lato Azure. Anche se suddividendo il traffico di hello, potrebbe apparire leggermente migliore velocità effettiva tramite i tunnel IPsec hello, hello obiettivo principale quello di questa configurazione è per la disponibilità elevata. E scadenza toohello natura statistica di diffusione hello, è difficile tooprovide misurazione di hello sul traffico di applicazione diverse condizioni determineranno velocità effettiva aggregata di hello.

Questa topologia richiede due gateway di rete locale e due connessioni toosupport hello alcuni dispositivi VPN locali e BGP è obbligatorio tooallow hello due connessioni toohello stessa rete locale. Questi requisiti sono hello stesso come hello [sopra](#activeactiveonprem). 

## <a name="highly-available-vnet-to-vnet-connectivity-through-azure-vpn-gateways"></a>Connettività da rete virtuale a rete virtuale a disponibilità elevata tramite gateway VPN di Azure
Hello stessa configurazione attivo-attivo può anche applicare le connessioni di rete virtuale a tooAzure. È possibile creare il gateway VPN attivo-attivo per entrambe le reti virtuali e connetterli hello tooform insieme stesso completo mesh connettività dei 4 tunnel tra due reti virtuali, come illustrato nell'hello diagramma seguito hello:

![Tra reti virtuali](./media/vpn-gateway-highlyavailable/vnet-to-vnet.png)

In questo modo sono sempre una coppia di tra due reti virtuali hello per qualsiasi evento di manutenzione pianificata, fornire anche una migliore disponibilità i tunnel. Anche se hello stessa topologia per la connettività cross-premise richiede due connessioni, topologia di rete virtuale a hello illustrata in precedenza sarà necessari una sola connessione per ogni gateway. Inoltre, BGP è facoltativo, a meno che il routing di transito sulla connessione di rete virtuale a hello è obbligatorio.

## <a name="next-steps"></a>Passaggi successivi
Vedere [la configurazione di gateway VPN attivo-attivo per Cross-premise e le connessioni di rete virtuale a](vpn-gateway-activeactive-rm-powershell.md) per passaggi tooconfigure attivo-attivo cross-premise e connessioni di rete virtuale a.

