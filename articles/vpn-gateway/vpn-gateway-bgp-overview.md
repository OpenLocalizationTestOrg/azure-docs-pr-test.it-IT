---
title: aaaOverview di BGP con gateway VPN di Azure | Documenti Microsoft
description: Questo articolo fornisce una panoramica di BGP con i gateway VPN di Azure.
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: f8c3985c-c128-4f34-835c-0e88742bf36e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/12/2017
ms.author: yushwang
ms.openlocfilehash: ced3f77ecd791c84fb72b96447e839be3bf94846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-bgp-with-azure-vpn-gateways"></a>Panoramica di BGP con i gateway VPN di Azure
Questo articolo fornisce una panoramica di BGP (Border Gateway Protocol) nei gateway VPN di Azure.

BGP è hello protocollo di routing standard comunemente utilizzato nelle hello Internet tooexchange routing e raggiungibilità informazioni tra due o più reti. Quando usata nel contesto di hello di reti virtuali di Azure, il protocollo BGP Abilita gateway VPN di Azure hello e i dispositivi VPN locali, chiamati peer BGP o elementi adiacenti, tooexchange "Invia" che indicherà entrambi i gateway su disponibilità hello e raggiungibilità per quelli i prefissi toogo tramite gateway hello o router coinvolti. BGP inoltre è possibile abilitare il routing di transito tra più reti mediante propagazione di route, un gateway BGP apprende da uno tooall peer BGP altri peer BGP. 

## <a name="why-use-bgp"></a>Perché usare BGP
BGP è una funzionalità facoltativa che può essere usata con i gateway VPN di Azure basati su route. Assicurarsi inoltre che il dispositivo VPN locale supporta BGP prima di abilitare funzionalità hello. È possibile continuare toouse i gateway VPN di Azure e i dispositivi VPN locali senza BGP. È hello equivalente di utilizzo delle route statiche (senza BGP) *e* con routing dinamico con il protocollo BGP tra Azure e le reti.

BGP offre nuove funzionalità e numerosi vantaggi, illustrati di seguito.

### <a name="support-automatic-and-flexible-prefix-updates"></a>Supporto per l'aggiornamento automatico e flessibile dei prefissi
Con il protocollo BGP, è necessario solo un peer BGP minima prefisso specifico tooa toodeclare tramite tunnel VPN S2S IPsec hello. Può essere più piccolo di un prefisso dell'host (/ 32) di hello indirizzo IP del peer BGP del dispositivo VPN locale. È possibile controllare quale locale i prefissi di rete desiderata tooadvertise tooAzure tooallow tooaccess la rete virtuale di Azure.

È anche possibile segnalare prefissi più grandi, che possono includere alcuni dei prefissi di indirizzo della rete virtuale, come uno spazio di indirizzi IP privato di grandi dimensioni, ad esempio 10.0.0.0/8. Si noti anche se i prefissi di hello non possono essere identici con uno qualsiasi dei prefissi di rete virtuale. Tali prefissi di rete virtuale tooyour identiche delle route verranno rifiutate.

### <a name="support-multiple-tunnels-between-a-vnet-and-an-on-premises-site-with-automatic-failover-based-on-bgp"></a>Supporto di più tunnel tra una rete virtuale e un sito locale con failover automatico basato su BGP
È possibile stabilire più connessioni tra i dispositivi VPN locali e di rete virtuale di Azure in hello nello stesso percorso. Questa funzionalità fornisce più tunnel (percorsi) tra due reti di hello in una configurazione attivo-attivo. Se uno dei tunnel hello è disconnessa, verranno ritirate route corrispondente hello tramite il protocollo BGP e traffico hello viene spostato automaticamente toohello rimanenti tunnel.

Hello seguente diagramma illustra un semplice esempio di questo programma di installazione a disponibilità elevata:

![Più percorsi attivi](./media/vpn-gateway-bgp-overview/multiple-active-tunnels.png)

### <a name="support-transit-routing-between-your-on-premises-networks-and-multiple-azure-vnets"></a>Supporto del routing di transito tra le reti locali e più reti virtuali di Azure
BGP consente a più gateway toolearn e propagare i prefissi da reti diverse, se sono direttamente o indirettamente collegati. Questo consente il routing di transito con i gateway VPN di Azure tra i siti locali o tra più reti virtuali di Azure.

Hello diagramma seguente viene illustrato un esempio di una topologia di multi-hop con percorsi multipli che possono transito del traffico tra reti locali due hello attraverso il gateway VPN di Azure all'interno di Networks Microsoft hello:

![Transito multihop](./media/vpn-gateway-bgp-overview/full-mesh-transit.png)

## <a name="bgp-faq"></a>DOMANDE FREQUENTI SU BGP
[!INCLUDE [vpn-gateway-bgp-faq-include](../../includes/vpn-gateway-bpg-faq-include.md)]

## <a name="next-steps"></a>Passaggi successivi
Vedere [introduzione BGP nel gateway VPN di Azure](vpn-gateway-bgp-resource-manager-ps.md) per passaggi tooconfigure BGP per le connessioni di rete virtuale a cross-premise.

