---
title: "Modelli di connettività di ExpressRoute: tooMicrosoft Azure tramite il provider di servizi di rete, gli scambi e provider Ethernet | Documenti Microsoft"
description: "Questo articolo descrive modalità diverse di hello di connettività di rete del cliente hello e servizi Microsoft Azure, Office 365 e Dynamics 365. I clienti possono usare provider MPLS, Cloud Exchange ed Ethernet."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/09/2017
ms.author: cherylmc
ms.openlocfilehash: 2682e6e45b2892869068f132bedb4bb08e3f89a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-connectivity-models"></a>Modelli di connettività di ExpressRoute
È possibile creare una connessione tra la rete locale e cloud Microsoft hello in tre modi diversi, [CloudExchange condivisione percorso](#CloudExchange), [connessione Ethernet](#Ethernet)e [(IPVPN) any per qualsiasi connessione](#IPVPN). I provider di connettività possono fornire uno o più modelli di connettività. Per lavorare con il modello connettività provider toopick hello adatto per l'utente.
<br><br>

![Diagramma dei modelli di connettività di ExpressRoute](./media/expressroute-connectivity-models/expressroute-connectivity-models-diagram.png)

## <a name="CloudExchange"></a>Percorso condiviso in una struttura Cloud Exchange
Se sono posizionati in una struttura con uno scambio di cloud, è possibile ordinare toohello connessioni incrociate virtuale Microsoft cloud tramite Ethernet exchange del provider di hello condivisione percorso. I provider di condivisione percorso offrono connessioni incrociate livello 2 o gestito Layer 3 connessioni incrociate tra l'infrastruttura nella funzionalità di condivisione percorso hello e cloud Microsoft hello.

## <a name="Ethernet"></a>Connessioni Ethernet da punto a punto
È possibile connettere il toohello Data Center o uffici locali Microsoft cloud tramite collegamenti Ethernet Point-to. Provider Ethernet Point to Point può offrire le connessioni di livello 2 o gestiti Layer 3 connessioni tra il sito e hello cloud Microsoft.

## <a name="IPVPN"></a>Reti (IPVPN) any-to-any
È possibile integrare la rete WAN con hello cloud Microsoft. I provider IPVPN (in genere VPN MPLS) forniscono connettività any-to-any tra le succursali e i data center. Hello Microsoft cloud può essere toomake WAN a tooyour interconnessi Cerca solo come qualsiasi altra succursale. I provider WAN offrono in genere connettività gestita di livello 3. Caratteristiche e funzionalità di ExpressRoute sono tutti identici per tutti di hello sopra i modelli di connettività. 

## <a name="next-steps"></a>Passaggi successivi
* Informazioni sulle connessioni e i domini di routing ExpressRoute. Vedere [Circuiti e domini di routing ExpressRoute](expressroute-circuit-peerings.md).
* Informazioni sulle funzionalità di ExpressRoute. Vedere hello [Panoramica tecnica su ExpressRoute](expressroute-introduction.md)
* Trovare un provider di servizi. Vedere [Partner e località di peering per Azure ExpressRoute](expressroute-locations.md).
* Verificare che vengano soddisfatti tutti i prerequisiti. Vedere [Prerequisiti per ExpressRoute](expressroute-prerequisites.md).
* Consultare i requisiti di toohello per [Routing](expressroute-routing.md), [NAT](expressroute-nat.md), e [QoS](expressroute-qos.md).
* Configurare la connessione ExpressRoute.
  * [Creare un circuito ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md)
  * [Configurare il routing](expressroute-howto-routing-portal-resource-manager.md)
  * [Collegare un circuito ExpressRoute di tooan rete virtuale](expressroute-howto-linkvnet-portal-resource-manager.md)
