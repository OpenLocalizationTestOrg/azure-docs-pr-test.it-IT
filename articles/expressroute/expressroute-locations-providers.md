---
title: "Località e provider di connettività: Azure ExpressRoute | Documentazione Microsoft"
description: "In questo articolo fornisce una panoramica dettagliata dei percorsi in cui vengono offerti i servizi e come tooconnect tooAzure aree. Ordinati in base alla località."
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
ms.assetid: feb67da3-5abc-4acb-bad4-f78e3c541ded
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/17/2017
ms.author: kaanan
ms.openlocfilehash: 838d52701d177aa7f13e845b7bde66d07b5efed6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-partners-and-peering-locations"></a>Partner e località di peering per ExpressRoute

> [!div class="op_single_selector"]
> * [Località per provider](expressroute-locations.md)
> * [Provider per località](expressroute-locations-providers.md)


Hello nelle tabelle di questo articolo è fornire informazioni sui provider di connettività di ExpressRoute, ExpressRoute geografico, servizi cloud Microsoft supportati tramite ExpressRoute e integratori di ExpressRoute (SIs).

## <a name="partners"></a>Provider di connettività ExpressRoute
ExpressRoute è supportato in tutte le aree e le località di Azure. Hello mappa seguente fornisce un elenco di aree di Azure e i percorsi di ExpressRoute. Percorsi di ExpressRoute, vedere toothose in cui Microsoft peer con diversi provider di servizi.

![Mappa delle località][0]

Se si è connessi tooat almeno una posizione di ExpressRoute nell'area di natura geopolitica hello, sarà necessario servizi di accesso tooAzure di tutte le aree all'interno di un'area di natura geopolitica. 

### <a name="azure-regions-tooexpressroute-locations-within-a-geopolitical-region"></a>Percorsi tooExpressRoute di aree di Azure all'interno di un'area di natura geopolitica
Hello nella tabella seguente fornisce una mappa delle aree di Azure tooExpressRoute posizioni all'interno di un'area di natura geopolitica.

| **Area geopolitica** | **Aree di Azure** | **Località per ExpressRoute** |
| --- | --- | --- |
| **America del Nord** |Stati Uniti orientali, Stati Uniti occidentali, Stati Uniti orientali 2, Stati Uniti occidentali 2, Stati Uniti centrali, Stati Uniti centro-meridionali, Stati Uniti centro-settentrionali, Stati Uniti centro-occidentali, Canada centrale, Canada orientale |Atlanta, Chicago, Dallas, Denver, Las Vegas, Los Angeles, Miami, New York, San Antonio, Seattle, Silicon Valley, Washington DC, Montreal, Quebec City, Toronto |
| **America del Sud** |Brasile meridionale |Sao Paulo |
| **Europa** |Europa settentrionale, Europa occidentale, Regno Unito occidentale, Regno Unito meridionale |Amsterdam, Dublino, Londra, Newport (Galles), Parigi |
| **Asia** |Asia orientale, Asia sudorientale |Hong Kong, Singapore |
| **Giappone** |Giappone occidentale, Giappone orientale |Osaka, Tokyo |
| **Australia** |Australia sudorientale, Australia orientale |Melbourne, Sydney |
| **India** |India occidentale, India centrale, India Meridionale |Chennai, Mumbai |
| **Corea del Sud** |Corea centrale, Corea meridionale |Busan, Seoul |

### <a name="regions-and-geopolitical-boundaries-for-national-clouds"></a>Aree e confini geopolitici per cloud nazionali
tabella Hello seguente fornisce informazioni sulle aree e i limiti di natura geopolitici per cloud nazionale.

| **Area geopolitica** | **Aree di Azure** | **Località per ExpressRoute** |
| --- | --- | --- |
| **Cloud del governo degli Stati Uniti** |US Gov Iowa, US Gov Virginia, US DoD Central, US DoD East  |Chicago, Dallas, New York, Seattle, Silicon Valley, Washington DC |
| **Cina** |Cina meridionale, Cina orientale |Pechino, Shanghai |
| **Germania** |Germania centrale, Germania orientale |Berlino, Francoforte |

Non è supportata la connettività tra le aree di natura geopolitiche sullo standard hello SKU ExpressRoute. Sarà necessario tooenable hello ExpressRoute premium componente aggiuntivo toosupport globale la connettività. Ambienti di cloud toonational connettività non è supportata. È possibile utilizzare il provider di connettività in caso di necessità.

## <a name="locations"></a>Località dei provider di connettività

Hello nella tabella seguente illustra hello e connettività percorsi di provider di servizi per ogni posizione. Se si desidera tooview i provider di servizi e i percorsi di hello per i quali possono fornire assistenza, vedere [percorsi dal provider di servizi](expressroute-locations.md#locations). 


### <a name="production-azure"></a>Produzione Azure
| **Località** | **Provider di servizi** |
| --- | --- |
| **Amsterdam** |Aryaka Networks, AT&T NetBond, British Telecom, Colt, Equinix, euNetworks, GÉANT, InterCloud, Internet Solutions - Cloud Connect, Interxion, KPN, Level 3 Communications, Megaport, Orange, Tata Communications, TeleCity Group, Telefonica, Telenor, Verizon, Zayo Group |
| **Atlanta** |Equinix |
| **Busan** |LG CNS |
| **Chennai** | Airtel+, Global CloudXchange (GCX), SIFY, Tata Communications |
| **Chicago** |AT&T NetBond, Comcast, Equinix, Level 3 Communications, Megaport, Verizon, Zayo Group |
| **Dallas** |Aryaka Networks, AT&T NetBond, Cologix, Equinix, Level 3 Communications, Megaport, Verizon, Zayo Group+ |
| **Denver** |CoreSite |
| **Dublino** |Colt, Interxion, Telecity Group |
| **Hong Kong** |Aryaka Networks, British Telecom, China Telecom Global, Equinix, Megaport, Orange, PCCW Global Limited, Tata Communications, Verizon |
| **Las Vegas** |Level 3 Communications, Megaport |
| **Londra** |AT&T NetBond, British Telecom, Colt, Equinix, InterCloud, Internet Solutions - Cloud Connect, Interxion, Jisc, Level 3 Communications, Megaport, MTN, NTT Communications, Orange, Tata Communications, Telecity Group, Telehouse - KDDI, Telenor, Verizon, Vodafone, Zayo Group+ |
| **Los Angeles** |CoreSite, Equinix, Megaport, NTT, Zayo Group |
| **Melbourne** |AARNet, Equinix, Megaport, NEXTDC, Telstra Corporation |
| **Miami** |C3ntro+, Megaport, Neutrona Networks |
| **Montreal** |Bell Canada, Cologix |
| **Mumbai** |Airtel+, Sify, Tata Communications |
| **New York** |Coresite, Equinix, Megaport, Zayo Group |
| **Newport(Wales)** |Dati di nuova generazione |
| **Osaka** |Equinix, Internet Initiative Japan Inc. - IIJ, NTT Communications, NTT SmartConnect, Softbank |
| **Parigi** |Colt, Interxion, Equinix, Orange |
| **Quebec City** | Megaport |
| **San Antonio** |Megaport |
| **Sao Paulo** |Ascenty Data Centers+, Equinix, Level 3 Communications, Neutrona Networks, Telefonica, UOLDIVEO |
| **Seattle** |Equinix, Level 3 Communications, Megaport |
| **Seoul** |KINX, LG CNS, Sejong Telecom |
| **Silicon Valley** |Aryaka Networks, AT&T NetBond, British Telecom, CenturyLink+, Comcast, Console, Equinix, Level 3 Communications, Megaport, Orange, Tata Communications, Verizon, Zayo Group |
| **Singapore** |Aryaka Networks, AT&T NetBond, British Telecom, Equinix, InterCloud, Level 3 Communications, Megaport, NTT Communications, Orange, SingTel, Tata Communications, Verizon |
| **Sydney** |AARNet, AT&T NetBond, British Telecom, Equinix, Megaport, NEXTDC, Orange, Telstra Corporation, Verizon |
| **Tokyo** |Aryaka Networks, AT&T NetBond, British Telecom, Colt, Equinix, Internet Initiative Japan Inc. - IIJ, NTT Communications, Softbank, Verizon |
| **Toronto** |AT&T NetBond, Bell Canada, Cologix, Console, Equinix, Megaport, Telus, Zayo Group |
| **Washington DC** |Aryaka Networks, AT&T NetBond, British Telecom, Comcast, Equinix, InterCloud, Level 3 Communications, Megaport, NTT Communications, Orange, Tata Communications, Verizon, Zayo Group |

 **+** indica disponibile a breve

### <a name="national-cloud-environments"></a>Ambienti cloud nazionali

### <a name="us-government-cloud"></a>Cloud del governo degli Stati Uniti
| **Posizione** | **Provider di servizi** |
| --- | --- |
| **Chicago** |AT&T NetBond, Equinix, Level 3 Communications, Verizon |
| **Dallas** |Equinix, Megaport, Verizon |
| **New York** |Equinix, Level 3 Communications+, Verizon |
| **Silicon Valley** | Equinix, Level 3 Communications |
| **Seattle** | Equinix |
| **Washington DC** |AT&T NetBond, Equinix, Level 3 Communications, Verizon |

### <a name="china"></a>Cina
| **Posizione** | **Provider di servizi** |
| --- | --- |
| **Pechino** |China Telecom |
| **Shanghai** |China Telecom |

vedere, più toolearn [ExpressRoute in Cina](http://www.windowsazure.cn/home/features/expressroute/)

### <a name="germany"></a>Germania
| **Posizione** | **Provider di servizi** |
| --- | --- |
| **Berlino** |Colt+, e-shelter, Megaport+, T-Systems |
| **Francoforte** |Colt, Equinix, Interxion |

## <a name="c1partners"></a>Connettività con provider di scambio
Se il provider di connettività non è incluso nelle sezioni precedenti, sarà comunque possibile creare una connessione.

* Se sono connessi tooany di scambi di hello nella precedente tabella hello, verificare con il toosee di provider di connettività. È possibile verificare l'esempio hello collega toogather ulteriori informazioni sui servizi offerti dai provider di exchange. Diversi provider di connettività sono già connessi tooEthernet scambi.
  * [Cologix](http://www.cologix.com/)
  * [Console](https://www.consoleconnect.com/partners/cloudsaas/)
  * [CoreSite](http://www.coresite.com/)
  * [Equinix Cloud Exchange](http://www.equinix.com/services/interconnection-connectivity/cloud-exchange/)
  * [Interxion](http://www.interxion.com/)
  * [NEXTDC](http://www.nextdc.com/)
  * [Megaport](https://www.megaport.com/services/microsoft-expressroute/)
  * [TeleCity CloudIX](http://www.telecitygroup.com/colocation-services/cloud-ix.htm)
* Dispone il provider di servizi di estendere il percorso di peering toohello rete di scelta.
  * Assicurarsi che il provider di connettività estenda la connettività con disponibilità elevata, in modo che non siano presenti singoli punti di errore.
* Ordinare un circuito ExpressRoute con exchange hello come provider di connettività tooconnect tooMicrosoft.
  * Seguire i passaggi in [creare un circuito ExpressRoute](expressroute-howto-circuit-classic.md) tooset della connettività.

## <a name="c1partners"></a>Connettività con provider di servizi aggiuntivi
| **Posizione** | **Exchange** | **Provider di connettività** |
| --- | --- | --- |
| **Amsterdam** | Equinix, Telecity | Eurofiber, Fastweb S.p.A, Nianet |
| **Chicago** | Equinix | Lightower, Windstream |
| **Dallas** | Equinix, Megaport | C3ntro Telecom, Cox Business, Data Foundry, Transtelco |
| **Francoforte** | Telecity | Nianet, QSC AG |
| **Hong Kong** | Equinix | Macroview Telecom |
| **Londra** | Equinix, euNetworks, Telecity | Bezeq International Ltd., Epsilon, Exponential E, HSO, NexGen Networks, Tamares Telecom, Zain |
| **Los Angeles** | Equinix |Transtelco |
| **Madrid** | Level3 | Zertia |
| **Montreal** | Cologix, Equinix | Airgate Technologies. Inc, Cogeco Peer 1, Rogers, Zirro |
| **New York** |Equinix, Megaport | Altice Business, Lightower, Webair |
| **Seattle** |Equinix | Alaska Communications |
| **Silicon Valley** |Equinix | Cox Business, Windstream |
| **Singapore** |Equinix |1CLOUDSTAR, Epsilon Telecommunications Limited, LGA Telecom, United Information Highway (UIH) |
| **Slough** | Equinix | HSO|
| **Sydney** | Megaport | Macquarie Telecom Group|
| **Tokyo** | Equinix | ARTERIA Networks Corporation, BroadBand Tower, Inc. |
| **Toronto** | Equinix | Airgate Technologies. Inc, Cogeco Peer 1, Rogers, Thinktel, Zirro|
| **Washington DC** |Equinix | Altice Business, Gtt Communications Inc, Epsilon, Lightower, Masergy, Windstream |

## <a name="expressroute-system-integrators"></a>Integratori di sistemi ExpressRoute
Abilitazione toofit connettività privata che possono essere difficile le proprie esigenze, in base alla scala di hello della rete. Si può funzionare con qualsiasi di hello integratori di sistema elencati nella seguente tabella tooassist hello è con tooExpressRoute onboarding.

| **Continente** | **Integratori di sistemi** |
| --- | --- |
| **Asia** |Avanade Inc., OneAs1a |
| **Australia** | Ensyst, IT Consultancy, MOQdigital, Vigilant.IT |
| **Europa** |Avanade Inc., Altogee, Bright Skies GmbH, Inframon, MSG Services, New Signature, Nelite, Orange Networks, sol-tec |
| **America del Nord** |Avanade Inc., Equinix Professional Services, FlexManage, Perficient, Presidio |
| **America del Sud** |Avanade Inc. |
## <a name="next-steps"></a>Passaggi successivi
* Per ulteriori informazioni su ExpressRoute, vedere hello [domande frequenti su ExpressRoute](expressroute-faqs.md).
* Verificare che vengano soddisfatti tutti i prerequisiti. Vedere [Prerequisiti per ExpressRoute](expressroute-prerequisites.md).

<!--Image References-->
[0]: ./media/expressroute-locations/expressroute-locations-map.png "Mappa delle località"
