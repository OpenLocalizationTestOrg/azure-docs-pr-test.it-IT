---
title: Requisiti di ExpressRoute aaaQoS | Documenti Microsoft
description: Questa pagina fornisce informazioni dettagliate sui requisiti per la configurazione e la gestione di QoS per circuiti ExpressRoute.
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: db1c1447-0283-4a09-907b-ae481adc40c7
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: cherylmc
ms.openlocfilehash: 46cc81bd38ff50dd9e7a1bfdd0faa457ff7b2fa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-qos-requirements"></a>Requisiti ExpressRoute QoS
Skype per aziende dispone di diversi carichi di lavoro che richiedono la gestione QoS differenziata. Se si prevede di servizi di vocale tooconsume tramite ExpressRoute, è necessario rispettare i requisiti di toohello descritti di seguito.

![](./media/expressroute-qos/expressroute-qos.png)

> [!NOTE]
> Requisiti di qualità del applicare toohello peering solo Microsoft. i valori DSCP Hello in traffico di rete ricevuti su peering pubblico di Azure e peering privato di Azure sarà too0 reimpostazione. 
> 
> 

Hello nella tabella seguente fornisce un elenco delle indicazioni DSCP utilizzato da Skype for Business. Fare riferimento troppo[gestione QoS per Skype for Business](https://technet.microsoft.com/library/gg405409.aspx) per ulteriori informazioni.

| **Classe di traffico** | **Modalità di gestione (contrassegno DSCP)** | **Carichi di lavoro di Skype per aziende** |
| --- | --- | --- |
| **Voice** |ENTITY FRAMEWORK (46) |Skype / voice di Lync |
| **Interattivo** |AF41 (34) |Video, VBSS |
| AF21 (18) |Condivisione delle app | |
| **Default** |AF11 (10) |Trasferimento di file |
| CS0 (0) |Altro | |

* È consigliabile classificare i carichi di lavoro hello e contrassegnare i valori DSCP hello destra. Seguire indicazioni hello fornite [qui](https://technet.microsoft.com/library/gg405409.aspx) su come contrassegni DSCP tooset nella rete.
* È necessario configurare e supportare più code di QoS nella rete. Voce deve essere una classe autonoma e ricevono un trattamento EF hello specificato nella RFC 3246. 
* È possibile decidere hello meccanismo, criteri di rilevamento di congestione e allocazione della larghezza di banda per ogni classe di traffico di Accodamento. Tuttavia, hello il contrassegno DSCP per Skype per carichi di lavoro di Business deve essere mantenuto. Se si usano i contrassegni DSCP non elencati in precedenza, ad esempio AF31 (26), è necessario riscrivere questa too0 valore DSCP prima dell'invio tooMicrosoft pacchetti hello. Microsoft invia solo i pacchetti contrassegnati con hello valore DSCP mostrato in hello precedente tabella. 

## <a name="next-steps"></a>Passaggi successivi
* Consultare i requisiti di toohello per [Routing](expressroute-routing.md) e [NAT](expressroute-nat.md).
* Vedere l'esempio hello collega tooconfigure la connessione ExpressRoute.
  
  * [Creare un circuito ExpressRoute](expressroute-howto-circuit-classic.md)
  * [Configurare il routing](expressroute-howto-routing-classic.md)
  * [Collegare un circuito ExpressRoute di tooan rete virtuale](expressroute-howto-linkvnet-classic.md)

