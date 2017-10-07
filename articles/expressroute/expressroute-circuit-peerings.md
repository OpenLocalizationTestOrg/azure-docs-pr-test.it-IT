---
title: aaaAzure ExpressRoute circuiti e domini di routing | Documenti Microsoft
description: Questa pagina viene fornita una panoramica di circuiti ExpressRoute e domini di routing hello.
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: 6f0c5d8e-cc60-4a04-8641-2c211bda93d9
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: cherylmc
ms.openlocfilehash: 1d43cbf668accdd7aa4efb053ea1e9027d10e4a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-circuits-and-routing-domains"></a>Circuiti e domini di routing ExpressRoute
 È necessario ordinare un *circuito ExpressRoute* tooconnect il tooMicrosoft infrastruttura locale tramite un provider di connettività. Figura Hello seguente fornisce una rappresentazione logica della connettività tra la rete WAN e Microsoft.

![](./media/expressroute-circuit-peerings/expressroute-basic.png)

## <a name="expressroute-circuits"></a>Circuiti ExpressRoute
Un *circuito ExpressRoute* rappresenta una connessione logica tra un'infrastruttura locale e i servizi cloud Microsoft tramite un provider di connettività. È possibile ordinare più circuiti ExpressRoute. Ogni circuito può essere in hello stesso o in aree diverse e può essere connesso tooyour localmente tramite i provider di connettività diversi. 

Circuiti ExpressRoute non eseguono il mapping delle entità fisiche tooany. Un circuito è identificato in modo univoco da un GUID standard denominato chiave di servizio. chiave del servizio Hello è hello informazione solo le informazioni scambiate tra Microsoft e i provider di connettività hello è. Hello. s-key non è un segreto per motivi di sicurezza. Viene applicato un mapping 1:1 tra un circuito ExpressRoute e hello tasto s.

Può avere un circuito ExpressRoute di peering indipendenti toothree: privato di Azure pubblico, Azure e Microsoft. Ogni peering è una coppia di sessioni BGP indipendenti, ognuna configurata in modo ridondante per garantire la disponibilità elevata. Esiste un mapping 1:N (1 <= N <= 3) tra un circuito ExpressRoute e i domini di routing. Per un circuito ExpressRoute può essere abilitato uno, due o tutti e tre i peering.

Ogni circuito ha una larghezza di banda predefinito (50 Mbps, 100 Mbps, 200 Mbps, 500 Mbps, 1 Gbps, 10 Gbps) e provider di connettività tooa mappati e un percorso di peering. larghezza di banda Hello selezionato viene condivisa tra tutti hello peering per il circuito hello. 

### <a name="quotas-limits-and-limitations"></a>Quote, limiti e limitazioni
Per ogni circuito ExpressRoute si applicano quote e limiti predefiniti. Fare riferimento toohello [sottoscrizione Azure e limiti dei servizi, quote e vincoli](../azure-subscription-service-limits.md) pagina per informazioni aggiornate sulle quote.

## <a name="expressroute-routing-domains"></a>Domini di routing ExpressRoute
A un circuito ExpressRoute sono associati più domini di routing, ovvero pubblico di Azure, privato di Azure e Microsoft. Ognuno dei domini di routing hello configurato in modo identico in una coppia di router (attivo-attivo o la condivisione di caricamento configurazione) per la disponibilità elevata. Servizi di Azure sono classificati come *pubblica Azure* e *privato Azure* toorepresent hello schemi di indirizzamento IP.

![](./media/expressroute-circuit-peerings/expressroute-peerings.png)

### <a name="private-peering"></a>Peering privato
Servizi, ovvero le macchine virtuali (IaaS) di calcolo di Azure e servizi cloud (PaaS) distribuiti all'interno di una rete virtuale possono essere connesso tramite dominio peering privato hello. dominio di peering privato Hello viene considerato un'estensione della rete core attendibile toobe in Microsoft Azure. È possibile configurare la connettività bidirezionale tra la rete di base e le reti virtuali (VNet) di Azure. Il peer consente di connettere macchine toovirtual e nel cloud servizi direttamente nei relativi indirizzi IP privati.  

È possibile connettere più di una rete virtuale toohello peering dominio privato. Hello revisione [pagina delle domande frequenti](expressroute-faqs.md) per informazioni su limiti e limitazioni. È possibile visitare hello [sottoscrizione Azure e limiti dei servizi, quote e vincoli](../azure-subscription-service-limits.md) pagina per informazioni aggiornate sui limiti.  Fare riferimento toohello [Routing](expressroute-routing.md) pagina per informazioni dettagliate sulla configurazione del routing.

### <a name="public-peering"></a>Peering pubblico
I servizi quali Archiviazione, database SQL e Siti Web di Azure vengono offerti su indirizzi IP pubblici. È possibile connettersi in modo privato tooservices ospitati su indirizzi IP pubblici, inclusi gli indirizzi VIP dei servizi cloud, tramite dominio di routing peering pubblico hello. È possibile connettersi hello pubblica peering dominio tooyour rete Perimetrale e tooall Azure hello di servizi su indirizzi IP pubblici dalla rate WAN senza tooconnect tramite internet. 

La connettività viene sempre avviata dalla WAN tooMicrosoft Azure servizi. Servizi di Microsoft Azure non sarà in grado di tooinitiate connessioni alla rete tramite il dominio di routing. Dopo aver abilitato il peering pubblico, sarà in grado di tooconnect tooall Azure servizi. È non consentono di servizi di selezione tooselectively per il quale è annunciare le route per. È possibile esaminare hello elenco di prefissi è annunciare tooyou tramite il peering hello [intervalli IP dei data center Microsoft Azure](http://www.microsoft.com/download/details.aspx?id=41653) pagina. pagina Hello viene aggiornato ogni settimana.

È possibile definire i filtri di route personalizzati all'interno del tooconsume solo hello le route di rete che è necessario. Fare riferimento toohello [Routing](expressroute-routing.md) pagina per informazioni dettagliate sulla configurazione del routing. 

Vedere hello [pagina delle domande frequenti](expressroute-faqs.md) per ulteriori informazioni sui servizi tramite dominio di routing peering pubblico hello è supportato. 

### <a name="microsoft-peering"></a>Peering Microsoft
[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

Connettività tooall altri Microsoft online services (ad esempio servizi di Office 365) sarà tramite il peering Microsoft hello. Si abilita la connettività bidirezionale tra i servizi cloud Microsoft e di rete WAN tramite hello Microsoft peering il dominio di routing. È necessario connettersi a servizi cloud tooMicrosoft solo su indirizzi IP pubblici appartenenti dall'utente o il provider di connettività ed è necessario rispettare le regole di tooall hello definito. Vedere hello [prerequisiti di ExpressRoute](expressroute-prerequisites.md) pagina per altre informazioni.

Vedere hello [pagina delle domande frequenti](expressroute-faqs.md) per ulteriori informazioni sui servizi supportati, i costi e i dettagli di configurazione. Vedere hello [ExpressRoute percorsi](expressroute-locations.md) pagina per informazioni sull'elenco hello dei provider di connettività che offrono supporto del peering Microsoft.

## <a name="routing-domain-comparison"></a>Confronto tra i domini di routing
tabella Hello seguente confronta tre domini di routing hello.

|  | **Peering privato** | **Peering pubblico** | **Peering Microsoft** |
| --- | --- | --- | --- |
| **Numero massimo di prefissi supportati per peering** |4000 per impostazione predefinita, 10.000 con ExpressRoute Premium |200 |200 |
| **Intervalli di indirizzi IP supportati** |Qualsiasi indirizzo IPv4 valido entro la rete WAN. |Indirizzi IPv4 pubblici di proprietà dell'utente o del provider di connettività. |Indirizzi IPv4 pubblici di proprietà dell'utente o del provider di connettività. |
| **Requisiti del numero AS** |Numeri AS pubblici e privati. È necessario esserne proprietari hello pubblico sotto forma di numero, se si sceglie toouse uno. |Numeri AS pubblici e privati. È tuttavia necessario dimostrare la proprietà degli indirizzi IP pubblici. |Numeri AS pubblici e privati. È tuttavia necessario dimostrare la proprietà degli indirizzi IP pubblici. |
| **Indirizzi IP per l'interfaccia di routing** |Indirizzi IP pubblici e RFC1918 |Tooyou registrati nei registri di sistema routing gli indirizzi IP pubblici. |Tooyou registrati nei registri di sistema routing gli indirizzi IP pubblici. |
| **Supporto per Hash MD5** |Sì |Sì |Sì |

È possibile scegliere tooenable uno o più domini di routing hello come parte del circuito ExpressRoute. È possibile scegliere tutti i domini di routing hello mettere in toohave hello stesso VPN se si desidera toocombine in un singolo dominio di routing. È anche possibile inserire tali in domini di routing diversi, diagramma toohello simile. Hello consigliato di configurazione è il peering privato è connesso direttamente toohello rete di base e hello pubblica e collegamenti di peering Microsoft sono connessi tooyour DMZ.

Se si sceglie toohave tutti e tre le sessioni di peering, è necessario disporre di tre coppie di sessioni BGP (una sola coppia per ogni tipo di peering). coppie di sessione BGP Hello forniscono un collegamento altamente disponibile. Se si stabilisce la connessione tramite provider di connettività di livello 2, l'utente sarà responsabile della configurazione e della gestione del routing. Per altre informazioni, è consigliabile consultare hello [flussi di lavoro](expressroute-workflows.md) per la configurazione di ExpressRoute.

## <a name="next-steps"></a>Passaggi successivi
* Trovare un provider di servizi. Vedere l'articolo relativo ai [provider di servizi e alle località ExpressRoute](expressroute-locations.md).
* Verificare che vengano soddisfatti tutti i prerequisiti. Vedere [Prerequisiti per ExpressRoute](expressroute-prerequisites.md).
* Configurare la connessione ExpressRoute.
  * [Creare e gestire circuiti ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md)
  * [Configurare il routing (peering) per circuiti ExpressRoute](expressroute-howto-routing-portal-resource-manager.md)

