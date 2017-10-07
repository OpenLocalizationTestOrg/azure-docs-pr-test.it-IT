---
title: requisiti di aaaNAT per circuiti ExpressRoute | Documenti Microsoft
description: Questa pagina fornisce informazioni dettagliate sui requisiti per la configurazione e la gestione di NAT per circuiti ExpressRoute.
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 867bf936-c851-485f-84c8-d8d6e33fee9f
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: cherylmc
ms.openlocfilehash: 09a0e841235de3f6b85e32172d7f99f20b5baf54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-nat-requirements"></a>Requisiti NAT di ExpressRoute
tooconnect tooMicrosoft servizi cloud tramite ExpressRoute, si sarà necessario tooset backup e gestiscono NAT. Alcuni provider di connettività offrono la configurazione e la gestione di NAT come servizio gestito. Verificare con il toosee di provider di connettività se offrono tale servizio. In caso contrario, è necessario rispettare i requisiti di toohello descritti di seguito. 

Hello revisione [ExpressRoute circuiti e domini di routing](expressroute-circuit-peerings.md) pagina tooget una panoramica di hello vari domini di routing. toomeet hello pubblici relativi all'indirizzo IP per Azure pubblico e peering Microsoft, è consigliabile configurare NAT tra la rete e Microsoft. In questa sezione fornisce una descrizione dettagliata dell'infrastruttura NAT hello che è necessario tooset backup.

## <a name="nat-requirements-for-azure-public-peering"></a>Requisiti NAT per il peering pubblico di Azure
percorso di peering pubblico Azure Hello consente si tooconnect tooall servizi ospitati in Azure tramite i relativi indirizzi IP pubblici. Sono inclusi i servizi elencati nella hello [domande frequenti su ExpessRoute](expressroute-faqs.md) e tutti i servizi ospitati da parte degli ISV in Microsoft Azure. 

> [!IMPORTANT]
> Connettività tooMicrosoft Azure servizi pubblici peering viene sempre avviato dalla rete nella rete di Microsoft hello. Pertanto, non possono essere avviate dalla rete tooyour servizi di Microsoft Azure tramite ExpressRoute. Se si è tentato, toothese pacchetti inviati annunciati IP utilizzerà hello internet invece di ExpressRoute.
> 

Il traffico destinato tooMicrosoft Azure nel peering pubblico deve essere toovalid SNATed che indirizzi IPv4 pubblici prima che essi immettere rete Microsoft hello. Figura Hello seguente offre un quadro generale delle modalità hello NAT potrebbe essere impostato hello toomeet sopra requisito.

![](./media/expressroute-nat/expressroute-nat-azure-public.png) 

### <a name="nat-ip-pool-and-route-advertisements"></a>Annunci di route e pool IP di NAT
È necessario assicurarsi che il traffico sta entrando hello Azure percorso di peering pubblico con un indirizzo IPv4 pubblico valido. Microsoft deve essere proprietario di hello toovalidate in grado di hello pool di indirizzi IPv4 NAT contro un internazionale routing Internet del Registro di sistema (RIR) o da un registro di routing Internet (IRR). Un controllo non verrà eseguito in base a hello come numero il corso peering con e hello indirizzi IP utilizzati per hello NAT. Fare riferimento toohello [requisiti di routing ExpressRoute](expressroute-routing.md) pagina per informazioni sui registri di routing.

Non esistono restrizioni sulla lunghezza hello del prefisso IP NAT hello pubblicato tramite il peering. È necessario monitorare pool NAT hello e assicurarsi che non sono esaurite delle sessioni NAT.

> [!IMPORTANT]
> Hello pool IP NAT annunciati tooMicrosoft non può essere annunciato toohello Internet. Servizi di integrazione applicativa tooother Microsoft verrà interrotta.
> 
> 

## <a name="nat-requirements-for-microsoft-peering"></a>Requisiti NAT per il peering Microsoft
percorso di peering Microsoft Hello consente di connettersi ai servizi cloud tooMicrosoft che non sono supportati tramite hello Azure percorso di peering pubblico. elenco di Hello dei servizi include servizi di Office 365, ad esempio Exchange Online, SharePoint Online, Skype for Business e Dynamics 365. Microsoft prevede una connettività bidirezionale toosupport nel peering Microsoft hello. Il traffico destinato tooMicrosoft cloud services deve essere toovalid SNATed che indirizzi IPv4 pubblici prima che essi immettere rete Microsoft hello. Traffico di rete tooyour dai servizi cloud Microsoft deve essere il tooprevent bordo Internet SNATed [routing asimmetrica](expressroute-asymmetric-routing.md). Figura Hello seguente offre un quadro generale delle modalità hello NAT deve essere il programma di installazione per il peering Microsoft.

![](./media/expressroute-nat/expressroute-nat-microsoft.png) 

### <a name="traffic-originating-from-your-network-destined-toomicrosoft"></a>Traffico proveniente dal tooMicrosoft rete destinati a
* È necessario assicurarsi che il traffico sta entrando in percorso di peering Microsoft hello con un indirizzo IPv4 pubblico valido. Microsoft deve essere proprietario di hello toovalidate in grado di hello pool di indirizzi IPv4 NAT con hello internazionali routing internet Registro di sistema (RIR) o da un registro di routing internet (IRR). Un controllo non verrà eseguito in base a hello come numero il corso peering con e hello indirizzi IP utilizzati per hello NAT. Fare riferimento toohello [requisiti di routing ExpressRoute](expressroute-routing.md) pagina per informazioni sui registri di routing.
* Indirizzi IP usati per hello installazione del peering pubblico di Azure e altri circuiti ExpressRoute non può essere annunciato tooMicrosoft tramite sessione BGP hello. Non vi è alcuna restrizione sulla lunghezza hello del prefisso IP NAT hello pubblicato tramite il peering.
  
  > [!IMPORTANT]
  > Hello pool IP NAT annunciati tooMicrosoft non può essere annunciato toohello Internet. Servizi di integrazione applicativa tooother Microsoft verrà interrotta.
  > 
  > 

### <a name="traffic-originating-from-microsoft-destined-tooyour-network"></a>Il traffico proveniente da Microsoft destinati a tooyour rete
* Alcuni scenari richiedono gli endpoint tooservice connettività tooinitiate Microsoft ospitati all'interno della rete. Un tipico esempio di scenario hello sarebbe server tooADFS connettività ospitate nella rete da Office 365. In questi casi, devono determinare una perdita di prefissi appropriati dalla rete in peering Microsoft hello. 
* È necessario il traffico SNAT Microsoft hello edge Internet gli endpoint del servizio all'interno del tooprevent rete [routing asimmetrica](expressroute-asymmetric-routing.md). Le richieste **e le risposte** con un IP di destinazione corrispondente a una route ricevuta tramite ExpressRoute verranno sempre inviate tramite ExpressRoute. Routing asimmetrica esistente se viene ricevuta richiesta di hello tramite hello Internet con hello risposta inviato tramite ExpressRoute. SNATing hello Microsoft il traffico in ingresso hello Internet edge forza toohello indietro di risposta il traffico Internet edge, risolvere il problema di hello.

![Routing asimmetrico con ExpressRoute](./media/expressroute-asymmetric-routing/AsymmetricRouting2.png)

## <a name="next-steps"></a>Passaggi successivi
* Consultare i requisiti di toohello per [Routing](expressroute-routing.md) e [QoS](expressroute-qos.md).
* Per informazioni sul flusso di lavoro, vedere [Flussi di lavoro e stati di provisioning di un circuito ExpressRoute](expressroute-workflows.md).
* Configurare la connessione ExpressRoute.
  
  * [Creare un circuito ExpressRoute](expressroute-howto-circuit-classic.md)
  * [Configurare il routing](expressroute-howto-routing-classic.md)
  * [Collegare un circuito ExpressRoute di tooan rete virtuale](expressroute-howto-linkvnet-classic.md)

