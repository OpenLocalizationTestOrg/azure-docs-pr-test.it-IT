---
title: 'Panoramica di ExpressRoute: Estendere la tooAzure di rete locale tramite una connessione privata | Documenti Microsoft'
description: Questa panoramica tecnica di ExpressRoute viene illustrata una connessione ExpressRoute tooextend il tooAzure di rete locale tramite una connessione privata.
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: fd95dcd5-df1d-41d6-85dd-e91d0091af05
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: cherylmc
ms.openlocfilehash: 01301e1205c12ecdab34dc9d9b92bc7489e7826c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-overview"></a>Panoramica di ExpressRoute
Microsoft Azure ExpressRoute consente di estendere le reti locali nel cloud di Microsoft hello tramite una connessione privata mediante un provider di connettività. Con ExpressRoute, è possibile stabilire i servizi cloud di tooMicrosoft connessioni, come Microsoft Azure, Office 365 e Dynamics 365.

La connettività può essere stabilita da una rete (IP VPN) any-to-any, da una rete Ethernet punto a punto o da una Cross Connection virtuale tramite un provider di connettività presso una struttura di condivisione del percorso. Le connessioni ExpressRoute non sfruttano hello rete Internet pubblica. In questo modo toooffer connessioni ExpressRoute più affidabilità, velocità più elevate, minori latenze e una maggiore sicurezza rispetto alle connessioni tramite hello Internet. Per informazioni su come tooconnect tooMicrosoft la rete tramite ExpressRoute, vedere [modelli di connettività di ExpressRoute](expressroute-connectivity-models.md).

![](./media/expressroute-introduction/expressroute-connection-overview.png)

## <a name="key-benefits"></a>Vantaggi principali

* Connettività Layer 3 tra la rete locale e hello Cloud Microsoft tramite un provider di connettività. La connettività può essere stabilita da una rete (IPVPN) any-to-any, da una connessione Ethernet punto a punto o con una Cross Connection virtuale tramite scambio Ethernet.
* Servizi cloud di connettività tooMicrosoft di tutte le aree nell'area di natura geopolitica hello.
* Servizi di connettività globale tooMicrosoft tutte le regioni con il componente aggiuntivo premium ExpressRoute.
* Routing dinamico tra la rete e Microsoft con protocolli standard del settore (BGP).
* Ridondanza incorporata in ogni località di peering per una maggiore affidabilità.
* [Contratto di servizio](https://azure.microsoft.com/support/legal/sla/)per i tempi di attività delle connessioni.
* Supporto QoS per Skype for Business.

Per ulteriori informazioni, vedere hello [domande frequenti su ExpressRoute](expressroute-faqs.md).

## <a name="features"></a>Funzionalità

### <a name="layer-3-connectivity"></a>Connettività di livello 3
Microsoft utilizza settore standard dinamica routing protocol (BGP) tooexchange instrada tra la rete locale, le istanze in Azure e Microsoft indirizzi pubblici.  Vengono stabilite più sessioni BGP con la rete per profili di traffico diversi. Ulteriori informazioni, vedere hello [ExpressRoute circuiti e domini di routing](expressroute-circuit-peerings.md) articolo.

### <a name="redundancy"></a>Ridondanza
Ogni circuito ExpressRoute è costituito da due connessioni tootwo Microsoft Enterprise edge router (MSEEs) dal provider di connettività hello / la rete perimetrale. Microsoft richiede una connessione BGP doppia dal provider di connettività hello o il lato – uno tooeach MSEE. È possibile scegliere i dispositivi di archiviazione con ridondanza non toodeploy / Ethernet circuiti l'estremità. Tuttavia, i provider di connettività utilizzano dispositivi ridondanti tooensure che le connessioni vengono passate tooMicrosoft in modo ridondante. Una configurazione della connettività Layer 3 ridondante è un requisito per il nostro [SLA](https://azure.microsoft.com/support/legal/sla/) toobe valido.

### <a name="connectivity-toomicrosoft-cloud-services"></a>Servizi cloud tooMicrosoft di connettività
[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

Le connessioni ExpressRoute abilitare accesso toohello seguenti servizi:

* Servizi di Microsoft Azure
* Servizi di Microsoft Office 365
* Microsoft Dynamics 365

È possibile visitare hello [domande frequenti su ExpressRoute](expressroute-faqs.md) pagina per un elenco dettagliato dei servizi supportati tramite ExpressRoute.

### <a name="connectivity-tooall-regions-within-a-geopolitical-region"></a>Aree di tooall connettività all'interno di un'area di natura geopolitica
È possibile connettersi tooMicrosoft in uno dei nostri [percorsi peering](expressroute-locations.md) e tooall di accedere alle aree all'interno di area geopolitici hello. 

Ad esempio, se si è connessi tramite ExpressRoute tooMicrosoft Amsterdam, è necessario servizi di accesso tooall Microsoft cloud ospitati in Nord Europa e dell'Europa occidentale. Vedere hello [ExpressRoute partner e località di peering](expressroute-locations.md) articolo per una panoramica delle aree geopolitici hello associati regioni cloud di Microsoft e percorsi peering ExpressRoute corrispondenti.

### <a name="global-connectivity-with-expressroute-premium-add-on"></a>Connettività globale con il componente aggiuntivo ExpressRoute Premium
È possibile abilitare la connettività tooextend funzionalità dei componenti aggiuntivi di hello ExpressRoute premium attraverso i limiti di natura geopolitici. Ad esempio, se si è connessi tooMicrosoft Amsterdam attraverso ExpressRoute, si avrà accesso tooall Microsoft cloud i servizi ospitati in tutte le aree del mondo hello (national cloud sono esclusi). È possibile accedere a servizi distribuiti in Sud America o Australia hello stessa modalità di accesso hello Nord e aree Europa occidentale.

### <a name="rich-connectivity-partner-ecosystem"></a>Ecosistema di partner di connettività avanzata
ExpressRoute presenta un ecosistema di partner di connettività e SI in continua crescita. È possibile fare riferimento toohello [ExpressRoute provider e i percorsi](expressroute-locations.md) articolo per informazioni più recenti di hello.

### <a name="connectivity-toonational-clouds"></a>Cloud toonational connettività
Microsoft gestisce ambienti cloud isolati per aree geopolitiche speciali e segmenti di clienti. Fare riferimento toohello [ExpressRoute provider e i percorsi](expressroute-locations.md) pagina per un elenco di cloud nazionale e provider.

### <a name="bandwidth-options"></a>Opzioni di larghezza di banda
È possibile acquistare circuiti ExpressRoute per un'ampia gamma di larghezze di banda. Le larghezze di banda supportate sono elencate di seguito. Essere toocheck verificare con l'elenco di hello connettività provider toodetermine di larghezze di banda supportate che forniscono.

* 50 Mbps
* 100 Mbps
* 200 Mbps
* 500 Mbps
* 1 Gbps
* 2 Gbps
* 5 Gbps
* 10 Gbps

### <a name="dynamic-scaling-of-bandwidth"></a>Scalabilità dinamica della larghezza di banda
È possibile aumentare hello ExpressRoute circuito della larghezza di banda (in base ad approssimazioni ottimali) senza tootear verso il basso le connessioni. 

### <a name="flexible-billing-models"></a>Modelli di fatturazione flessibili
È possibile selezionare il modello di fatturazione più adatto per le proprie esigenze. Scegliere tra i modelli di fatturazione hello elencati di seguito. Per ulteriori informazioni, vedere hello [domande frequenti su ExpressRoute](expressroute-faqs.md).

* **Dati illimitati**. circuito ExpressRoute Hello viene addebitato in base a una tariffa mensile e trasferimento di tutti i dati in entrata e in uscita viene aggiunto a titolo gratuito. 
* **Dati a consumo**. circuito ExpressRoute Hello viene addebitato in base a una tariffa mensile. Nella tariffa è incluso il trasferimento di tutti i dati in entrata. Il trasferimento dei dati in uscita invece viene addebitato per GB di dati trasferiti. Le tariffe per il trasferimento dei dati variano in base all'area.
* **Componente aggiuntivo ExpressRoute Premium**. premium ExpressRoute Hello è un componente aggiuntivo su hello circuito ExpressRoute. componente aggiuntivo di Hello ExpressRoute premium fornisce hello seguenti funzionalità: 
  * Limiti di route maggiore per pubblici e Azure peering privato di Azure da too10 di 4.000 route, le route 000.
  * Connettività globale per i servizi. Un circuito ExpressRoute creato in qualsiasi area (esclusi i cloud nazionale) avranno accesso tooresources in qualsiasi altra area in HelloWorld. Ad esempio, una rete virtuale creata nell'Europa occidentale è accessibile attraverso un circuito ExpressRoute fornito nella Silicon Valley.
  * Maggior numero di collegamenti di rete virtuale per il circuito ExpressRoute da limite di dimensioni maggiori tooa 10, a seconda della larghezza di banda hello del circuito hello.

## <a name="faq"></a>domande frequenti

Per domande frequenti su ExpressRoute, vedere hello [domande frequenti su ExpressRoute](expressroute-faqs.md).

## <a name="next-steps"></a>Passaggi successivi

* Altre informazioni sui [Modelli di connettività di ExpressRoute](expressroute-connectivity-models.md).
* Informazioni sulle connessioni e i domini di routing ExpressRoute. Vedere [Circuiti e domini di routing ExpressRoute](expressroute-circuit-peerings.md).
* Trovare un provider di servizi. Vedere [Partner e località di peering per Azure ExpressRoute](expressroute-locations.md).
* Verificare che vengano soddisfatti tutti i prerequisiti. Vedere [Prerequisiti per ExpressRoute](expressroute-prerequisites.md).
* Consultare i requisiti di toohello per [Routing](expressroute-routing.md), [NAT](expressroute-nat.md), e [QoS](expressroute-qos.md).
* Configurare la connessione ExpressRoute.
  * [Creare un circuito ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md)
  * [Configurare il peering per un circuito ExpressRoute](expressroute-howto-routing-portal-resource-manager.md)
  * [Connettersi a un circuito ExpressRoute di tooan rete virtuale](expressroute-howto-linkvnet-portal-resource-manager.md)
* Informazioni su alcune delle hello altre chiavi [funzionalità di rete](../networking/networking-overview.md) di Azure.
