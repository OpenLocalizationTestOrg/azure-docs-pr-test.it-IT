---
title: domande frequenti su ExpressRoute aaaAzure | Documenti Microsoft
description: domande frequenti su ExpressRoute Hello contiene informazioni sui servizi di Azure supportata, il costo, dati e le connessioni, contratto di servizio, provider e percorsi, della larghezza di banda e altri dettagli tecnici.
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: 09b17bc4-d0b3-4ab0-8c14-eed730e1446e
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: c01e83f1497103e2fa85251dce6fb41844e46e9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-faq"></a>Domande frequenti su ExpressRoute

## <a name="what-is-expressroute"></a>Che cos'è ExpressRoute?

ExpressRoute è un servizio di Azure che permette di creare connessioni private tra i data center Microsoft e l'infrastruttura disponibile localmente o in una struttura con percorso condiviso. Le connessioni ExpressRoute non sfruttano l'affidabilità di rete Internet pubblica e offrono una maggiore sicurezza, hello e velocità più elevate e ridurre le latenze rispetto alle connessioni tramite hello Internet.

### <a name="what-are-hello-benefits-of-using-expressroute-and-private-network-connections"></a>Quali sono hello vantaggi dell'utilizzo di connessioni di rete privata ed ExpressRoute?

Le connessioni ExpressRoute non sfruttano hello rete Internet pubblica. Offrono una maggiore sicurezza, affidabilità e velocità, eseguite regolarmente con latenze inferiore e coerente rispetto alle connessioni tramite hello Internet. In alcuni casi, tramite dati tootransfer di connessioni ExpressRoute tra dispositivi locali e Azure può produrre vantaggi significativi.

### <a name="where-is-hello-service-available"></a>In cui è disponibile il servizio hello?

Per informazioni sulla località e la disponibilità del servizio, vedere [Partner e località per ExpressRoute](expressroute-locations.md).

### <a name="how-can-i-use-expressroute-tooconnect-toomicrosoft-if-i-dont-have-partnerships-with-one-of-hello-expressroute-carrier-partners"></a>Come è possibile utilizzare ExpressRoute tooconnect tooMicrosoft se non si dispone di una partnership con uno dei partner di hello gestore ExpressRoute?

È possibile selezionare un gestore regionale e inserite tooone connessioni Ethernet di exchange supportata hello sedi dei provider. È quindi possibile connettersi a Microsoft nel percorso di provider hello. Controllare l'ultima sezione di hello di [ExpressRoute partner e i percorsi](expressroute-locations.md) toosee se il provider di servizi è presente in uno dei percorsi di exchange hello. Sarà quindi possibile ordinare un circuito ExpressRoute tramite hello servizio provider tooconnect tooAzure.

### <a name="how-much-does-expressroute-cost"></a>Quanto costa ExpressRoute?

Per informazioni sui prezzi, vedere [Dettagli prezzi](https://azure.microsoft.com/pricing/details/expressroute/) .

### <a name="if-i-pay-for-an-expressroute-circuit-of-a-given-bandwidth-does-hello-vpn-connection-i-purchase-from-my-network-service-provider-have-toobe-hello-same-speed"></a>Se pago per un circuito ExpressRoute di una determinata larghezza di banda, hello connessione VPN acquistata con il provider di servizi hanno toobe hello stessa velocità?

No. È possibile acquistare una connessione VPN di qualsiasi velocità dal provider di servizi. Tuttavia, tooAzure la connessione è limitato toohello ExpressRoute circuito della larghezza di banda acquistato.

### <a name="if-i-pay-for-an-expressroute-circuit-of-a-given-bandwidth-do-i-have-hello-ability-tooburst-up-toohigher-speeds-if-necessary"></a>Se si acquista un circuito ExpressRoute di una determinata larghezza di banda, è necessario hello possibilità tooburst backup velocità toohigher se necessario?

Sì. Circuiti ExpressRoute sono configurati tooallow tooburst tootwo ore di hello limite di larghezza di banda acquistato, senza alcun costo aggiuntivo. Controllare con toosee di provider del servizio che supportano questa funzionalità.

### <a name="can-i-use-hello-same-private-network-connection-with-virtual-network-and-other-azure-services-simultaneously"></a>È possibile utilizzare hello stesso privata rete connessione con la rete virtuale e altri servizi di Azure contemporaneamente?

Sì. Un circuito ExpressRoute, una volta impostato, consente tooaccess servizi all'interno di una rete virtuale e altri servizi di Azure contemporaneamente. Connettere reti di toovirtual nel percorso di peering privato hello e tooother servizi tramite il percorso di peering pubblico di hello.

### <a name="does-expressroute-offer-a-service-level-agreement-sla"></a>ExpressRoute offre un contratto di servizio?

Per informazioni, vedere hello [ExpressRoute SLA](https://azure.microsoft.com/support/legal/sla/) pagina.

## <a name="supported-services"></a>Servizi supportati

ExpressRoute supporta [tre domini di routing](expressroute-circuit-peerings.md) per diversi tipi di servizi.

### <a name="private-peering"></a>Peering privato

* Reti virtuali, inclusi tutti i servizi cloud e tutte le macchine virtuali

### <a name="public-peering"></a>Peering pubblico

* Power BI
* Dynamics 365 for Finance Operations (noto in precedenza come Dynamics AX Online)
* La maggior parte delle hello Azure servizi con hello alcune eccezioni seguenti:
  * RETE CDN
  * Test del carico di Visual Studio Team Services
  * Multi-Factor Authentication
  * Gestione traffico

### <a name="microsoft-peering"></a>Peering Microsoft

* [Office 365](http://aka.ms/ExpressRouteOffice365)
* Applicazioni Dynamics 365 Customer Engagement (precedentemente note come CRM Online)
  * Dynamics 365 for Sales
  * Dynamics 365 for Customer Service
  * Dynamics 365 for Field Service
  * Dynamics 365 for Project Service

## <a name="data-and-connections"></a>Dati e connessioni

### <a name="are-there-limits-on-hello-amount-of-data-that-i-can-transfer-using-expressroute"></a>Esistono limiti alla quantità di hello di dati trasferibili usando ExpressRoute?

È non impostare un limite alla quantità di hello di trasferimento dei dati. Fare riferimento troppo[prezzi](https://azure.microsoft.com/pricing/details/expressroute/) per informazioni sui tassi di larghezza di banda.

### <a name="what-connection-speeds-are-supported-by-expressroute"></a>Quali sono le velocità di connessione supportate da ExpressRoute?

Offerte relative alle larghezze di banda supportate:

50 Mbps, 100 Mbps, 200 Mbps, 500 Mbps, 1 Gbps, 2 Gbps, 5 Gbps, 10 Gbps

### <a name="which-service-providers-are-available"></a>Quali provider del servizio sono disponibili?

Vedere [ExpressRoute partner e i percorsi](expressroute-locations.md) per elenco hello del provider di servizi e i percorsi.

## <a name="technical-details"></a>Dettagli tecnici

### <a name="what-are-hello-technical-requirements-for-connecting-my-on-premises-location-tooazure"></a>Quali sono i requisiti tecnici di hello per la connessione my tooAzure percorso locale?

Per informazioni sui requisiti, vedere la [pagina dei prerequisiti di ExpressRoute](expressroute-prerequisites.md).

### <a name="are-connections-tooexpressroute-redundant"></a>Sono tooExpressRoute connessioni ridondanti?

Sì. Ogni circuito ExpressRoute ha una coppia ridondante di cross-connessioni configurate tooprovide la disponibilità elevata.

### <a name="will-i-lose-connectivity-if-one-of-my-expressroute-links-fail"></a>In caso di errore di un collegamento a ExpressRoute, verrà persa la connettività?

Non la connettività verrà persa se uno di hello tra le connessioni si verifica un errore. Carico hello toosupport disponibili della rete è una connessione ridondante. È inoltre possibile creare più circuiti in un diverso peering percorso tooachieve resilienza per gli errori.

### <a name="onep2plink"></a>Se non si è posizionato in uno scambio di cloud e il provider del servizio offre la connessione da punto a punto, sono necessarie due connessioni fisiche tooorder tra la rete locale e Microsoft?

Se il provider di servizi è possibile stabilire due circuiti virtuali a Ethernet per la connessione fisica hello, è sufficiente una connessione fisica. Hello connessione fisica (ad esempio, un'in fibra ottica) viene terminato su un livello 1 (L1) dispositivo (vedere l'immagine di hello). circuiti virtuali Ethernet di Hello due sono contrassegnati con l'ID VLAN diversi, uno per il circuito primario hello e uno per hello secondario. Tali ID VLAN sono nell'intestazione Ethernet hello 802.1 q esterno. intestazione Ethernet Hello 802.1 q interna (non illustrato) è mappata tooa specifico [il dominio di routing ExpressRoute](expressroute-circuit-peerings.md).

![](./media/expressroute-faqs/expressroute-p2p-ref-arch.png)

### <a name="can-i-extend-one-of-my-vlans-tooazure-using-expressroute"></a>È possibile estendere una delle my tooAzure VLAN tramite ExpressRoute?

No. Non sono supportate estensioni alla connettività di livello 2 in Azure.

### <a name="can-i-have-more-than-one-expressroute-circuit-in-my-subscription"></a>La sottoscrizione può includere più di un circuito ExpressRoute?

Sì. La sottoscrizione può includere più di un circuito ExpressRoute. Hello predefinito limite too10. È possibile contattare limite hello tooincrease di supporto Microsoft, se necessario.

### <a name="can-i-have-expressroute-circuits-from-different-service-providers"></a>Si possono usare circuiti ExpressRoute di diversi provider di servizi?

Sì. È possibile usare i circuiti ExpressRoute con molti provider di servizi. Ogni circuito ExpressRoute è associato a un solo provider di servizi. 

### <a name="can-i-have-multiple-expressroute-circuits-in-hello-same-location"></a>È possibile avere più circuiti ExpressRoute in hello nello stesso percorso?

Sì. È possibile avere più circuiti ExpressRoute, con hello uguali o diversi provider di servizi nella stessa posizione di hello. Tuttavia, non è possibile collegare più toohello di circuito ExpressRoute stesso virtuale di rete da hello stesso percorso.

### <a name="how-do-i-connect-my-virtual-networks-tooan-expressroute-circuit"></a>Come si connette il circuito ExpressRoute di tooan di reti virtuali

passaggi di base di Hello sono:

* Stabilire un circuito ExpressRoute e dispone il provider di servizi di hello abilitarlo.
* Si o il provider di hello, è necessario configurare hello BGP peering (s).
* Collegare il circuito ExpressRoute hello toohello alla rete virtuale.

Per altre informazioni, vedere [Flussi di lavoro e stati di provisioning di un circuito ExpressRoute](expressroute-workflows.md).

### <a name="are-there-connectivity-boundaries-for-my-expressroute-circuit"></a>Sono previsti limiti di connettività per il circuito ExpressRoute?

Sì. Hello [ExpressRoute partner e i percorsi](expressroute-locations.md) articolo viene fornita una panoramica dei limiti di hello connettività per un circuito ExpressRoute. La connettività per un circuito ExpressRoute è limitato tooa singola regione di natura geopolitica. Connettività può essere espanso toocross geopolitici aree abilitando funzionalità premium di hello ExpressRoute.

### <a name="can-i-link-toomore-than-one-virtual-network-tooan-expressroute-circuit"></a>È possibile collegare toomore rispetto a una rete virtuale tooan circuito ExpressRoute?

Sì. È possibile disporre le connessioni di reti virtuali too10 su un circuito ExpressRoute standard e di too100 un [circuito ExpressRoute premium](#expressroute-premium). 

### <a name="i-have-multiple-azure-subscriptions-that-contain-virtual-networks-can-i-connect-virtual-networks-that-are-in-separate-subscriptions-tooa-single-expressroute-circuit"></a>Sono disponibili più sottoscrizioni di Azure che contengono reti virtuali. È possibile connettere reti virtuali presenti sottoscrizioni separate tooa singolo circuito ExpressRoute?

Sì. È possibile autorizzare backup too10 altri toouse le sottoscrizioni di Azure, un singolo circuito ExpressRoute. Per aumentare questo limite, è possibile abilitare la funzionalità premium di hello ExpressRoute.

Per altre informazioni, vedere [Condivisione di un circuito ExpressRoute tra più sottoscrizioni](expressroute-howto-linkvnet-arm.md).

### <a name="are-virtual-networks-connected-toohello-same-circuit-isolated-from-each-other"></a>Sono toohello connessi a reti virtuali stesso circuito isolato tra loro?

No. Da un routing toohello collegato a reti della prospettiva, tutte virtuali stesso circuito ExpressRoute fanno parte della stesso dominio di routing hello e non sono isolate una da altra. Se è necessario indirizzare l'isolamento, è necessario toocreate un circuito ExpressRoute separato.

### <a name="can-i-have-one-virtual-network-connected-toomore-than-one-expressroute-circuit"></a>È possibile avere una rete virtuale connessa toomore rispetto a un circuito ExpressRoute?

Sì. È possibile collegare una singola rete virtuale con i circuiti ExpressRoute toofour. Devono essere ordinati in quattro [località per ExpressRoute](expressroute-locations.md)diverse.

### <a name="can-i-access-hello-internet-from-my-virtual-networks-connected-tooexpressroute-circuits"></a>È possibile accedere hello Internet dal mio circuiti tooExpressRoute connesso reti virtuali?

Sì. Se non si hanno annunciato route predefinite (0.0.0.0/0) o prefissi di route Internet tramite sessione BGP hello, è possibile connettersi toohello Internet da un circuito ExpressRoute di tooan rete virtuale collegata.

### <a name="can-i-block-internet-connectivity-toovirtual-networks-connected-tooexpressroute-circuits"></a>È possibile bloccare Internet connettività toovirtual reti connesse tooExpressRoute circuiti?

Sì. È possibile pubblicizzare predefinito route (0.0.0.0/0) tooblock tutti i computer Internet connettività toovirtual distribuito all'interno di una rete virtuale e indirizzare tutto il traffico attraverso il circuito ExpressRoute hello out.

Se si annunciano le route predefinite, si forzare tooservices traffico offerti su pubblico locale tooyour indietro peering (ad esempio l'archiviazione di Azure e database di SQL Server). Sarà necessario tooconfigure il tooAzure traffico tooreturn router tramite il percorso di peering pubblico di hello o hello Internet.

### <a name="can-virtual-networks-linked-toohello-same-expressroute-circuit-talk-tooeach-other"></a>Reti virtuali collegate toohello possibile stesso circuito ExpressRoute parlare tooeach altri?

Sì. Macchine virtuali distribuite in toohello connessi a reti virtuali stesso circuito ExpressRoute possa comunicare tra loro.

### <a name="can-i-use-site-to-site-connectivity-for-virtual-networks-in-conjunction-with-expressroute"></a>È possibile usare la connettività da sito per reti virtuali insieme a ExpressRoute?

Sì. ExpressRoute può coesistere con VPN da sito a sito.

### <a name="can-i-move-a-virtual-network-from-site-to-site--point-to-site-configuration-toouse-expressroute"></a>È possibile spostare una rete virtuale da sito a sito o point-to-site configurazione toouse ExpressRoute?

Sì. Sarà necessario toocreate un gateway ExpressRoute all'interno della rete virtuale. Ecco un breve tempo di inattività associato hello processo.

### <a name="why-is-there-a-public-ip-address-associated-with-hello-expressroute-gateway-on-a-virtual-network"></a>Perché è un indirizzo IP pubblico associato gateway ExpressRoute hello in una rete virtuale?

indirizzo IP pubblico Hello viene utilizzato per la gestione interna solo. Questo indirizzo IP pubblico non è esposto toohello Internet e non costituisce un'esposizione di sicurezza della rete virtuale.

### <a name="what-do-i-need-tooconnect-tooazure-storage-over-expressroute"></a>Cosa devo tooconnect tooAzure archiviazione tramite ExpressRoute?

Si deve stabilire un circuito ExpressRoute e configurare le route per il peering pubblico.

### <a name="are-there-limits-on-hello-number-of-routes-i-can-advertise"></a>Esistono limiti sul numero di hello di route che pubblicabili?

Sì. Vengono accettati i prefissi di route too4000 per il peering privato e 200 per il peering pubblico e peering Microsoft. È possibile aumentare questo too10, 000 route per il peering privato se si abilita la funzionalità premium di hello ExpressRoute.

### <a name="are-there-restrictions-on-ip-ranges-i-can-advertise-over-hello-bgp-session"></a>Sono previste restrizioni per gli intervalli IP che pubblicabili tramite sessione BGP hello?

Non si accettano i prefissi privati (RFC1918) in hello pubblico e sessione BGP peering Microsoft.

### <a name="what-happens-if-i-exceed-hello-bgp-limits"></a>Cosa accade se si superano i limiti BGP hello?

Le sessioni BGP saranno rimosse. Saranno ripristinate quando il numero di prefissi hello scende sotto il limite di hello.

### <a name="what-is-hello-expressroute-bgp-hold-time-can-it-be-adjusted"></a>Che cos'è hello BGP ExpressRoute contenere ora? È possibile regolarlo?

tempo di attesa Hello è 180. messaggi keep-alive Hello vengono inviati ogni 60 secondi. Questi sono fisse impostazioni su hello lato Microsoft non può essere modificato. È possibile che si tooconfigure diversi timer e i parametri di sessione BGP hello verranno negoziati di conseguenza.

### <a name="after-i-advertise-hello-default-route-00000-toomy-virtual-networks-i-cant-activate-windows-running-on-my-azure-vms-how-tooi-fix-this"></a>Dopo annunciare reti virtuali toomy hello predefinito route (0.0.0.0/0), Impossibile attivare Windows in esecuzione su macchine virtuali di Azure. Come tooI risolvere il problema?

Hello passaggi riconoscere Azure richiesta di attivazione hello:

1. Stabilire hello peering pubblico per il circuito ExpressRoute.
2. Eseguire una ricerca DNS e di trovare l'indirizzo IP hello del **kms.core.windows.net**
3. Hello servizio di gestione delle chiavi deve riconoscere la richiesta di attivazione hello proviene da Azure e onore hello richiesta. Effettuare uno dei seguenti tre attività hello.

   * Nella rete locale, hello instradare il traffico destinato hello indirizzo IP ottenuto nel passaggio 2 tooAzure indietro tramite hello di peering pubblico.
   * Disporre i NSP provider selettore di precisione pin hello traffico indietro tooAzure tramite il peering pubblico hello.
   * Creare una route definita dall'utente che IP hello punti con Internet come hop successivo e applicarlo toohello subnet in cui queste macchine virtuali sono.

### <a name="can-i-change-hello-bandwidth-of-an-expressroute-circuit"></a>È possibile modificare la larghezza di banda hello di un circuito ExpressRoute?

Sì, è possibile tentare di larghezza di banda hello tooincrease del circuito ExpressRoute in hello portale di Azure o tramite PowerShell. Se è la capacità disponibile sulla porta di hello fisico in cui è stato creato il circuito, la modifica ha esito positivo. 

Se la modifica non riesce, significa che non è disponibile una capacità sufficiente a sinistra nella porta corrente hello o è necessario un nuovo circuito ExpressRoute con maggiore larghezza di banda hello toocreate o che non è presente capacità aggiuntive in tale posizione, nel qual caso non sarà possibile larghezza di banda hello tooincrease. 

Sarà inoltre necessario toofollow con il tooensure di provider di connettività che aggiornano le limitazioni di hello all'interno di aumento della larghezza di banda loro reti toosupport hello. Tuttavia, non è possibile, ridurre la larghezza di banda hello del circuito ExpressRoute. Si dispone di un nuovo circuito ExpressRoute con larghezza di banda inferiore toocreate ed elimina il circuito precedente hello.

### <a name="how-do-i-change-hello-bandwidth-of-an-expressroute-circuit"></a>Come è possibile modificare la larghezza di banda hello di un circuito ExpressRoute?

È possibile aggiornare la larghezza di banda hello del circuito ExpressRoute hello utilizzando hello API REST o il cmdlet PowerShell.

## <a name="expressroute-premium"></a>ExpressRoute Premium

### <a name="what-is-expressroute-premium"></a>Che cos'è ExpressRoute Premium?

ExpressRoute premium è una raccolta di hello seguenti caratteristiche:

* Aumentato limite della tabella di routing da too10 route 4000, 000 route per il peering privato.
* Aumento del numero di reti virtuali che possono essere collegato toohello circuito ExpressRoute (valore predefinito è 10). Per ulteriori informazioni, vedere hello [ExpressRoute limiti](#limits) tabella.
* Connettività tooOffice 365 e Dynamics 365.
* Connettività globale su hello Microsoft core network. È ora possibile collegare una VNet in un'area geopolitica a un circuito ExpressRoute in un'altra area.<br>
    **Esempi:**

    *  È possibile collegare una rete virtuale creata in Europa occidentale tooan circuito ExpressRoute creato Silicon Valley. 
    *  In hello peering pubblico, i prefissi di altre aree di natura geopolitiche vengono annunciati in modo che sia possibile connettersi a, ad esempio, SQL Azure in Europa occidentale da un circuito Silicon Valley.


### <a name="limits"></a>Il numero di reti virtuali è possibile collegare circuito ExpressRoute tooan se è attivata premium ExpressRoute?

Hello nelle tabelle seguenti mostrano i limiti di ExpressRoute hello e numero di hello di reti virtuali al circuito ExpressRoute:

[!INCLUDE [ExpressRoute limits](../../includes/expressroute-limits.md)]

### <a name="how-do-i-enable-expressroute-premium"></a>Come si abilita ExpressRoute Premium?

Funzionalità premium di ExpressRoute può essere abilitata quando è abilitata la funzionalità di hello e può essere arrestata aggiornando lo stato di hello circuito. È possibile abilitare premium ExpressRoute al momento della creazione circuito, oppure chiamare hello API REST o i cmdlet di PowerShell.

### <a name="how-do-i-disable-expressroute-premium"></a>Come si disabilita ExpressRoute Premium?

È possibile disabilitare premium ExpressRoute chiamando hello API REST o il cmdlet PowerShell. È necessario assicurarsi che le prestazioni ai termini della connettività esigenze toomeet hello predefinito prima di disabilitare premium ExpressRoute. Se la percentuale di utilizzo viene ridimensionata oltre i limiti predefiniti hello, premium ExpressRoute toodisable di hello richiesta ha esito negativo.

### <a name="can-i-pick-and-choose-hello-features-i-want-from-hello-premium-feature-set"></a>È scegliere funzioni hello desiderate dal set di funzionalità premium hello?

No. Non è possibile selezionare le funzionalità di hello. Quando si attiva ExpressRoute Premium, vengono abilitate tutte le funzionalità.

### <a name="how-much-does-expressroute-premium-cost"></a>Quanto costa ExpressRoute Premium?

Fare riferimento troppo[prezzi](https://azure.microsoft.com/pricing/details/expressroute/) costo.

### <a name="do-i-pay-for-expressroute-premium-in-addition-toostandard-expressroute-charges"></a>Posso pagare per ExpressRoute premium inoltre toostandard spese ExpressRoute?

Sì. ExpressRoute premium addebitati costi circuito ExpressRoute e spese richieste dal provider di connettività hello.

## <a name="expressroute-for-office-365-and-dynamics-365"></a>ExpressRoute per Office 365 e Dynamics 365

[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

### <a name="how-do-i-create-an-expressroute-circuit-tooconnect-toooffice-365-services-and-dynamics-365"></a>Come creare un tooconnect circuito ExpressRoute servizi tooOffice 365 e Dynamics 365?

1. Hello revisione [pagina dei prerequisiti di ExpressRoute](expressroute-prerequisites.md) toomake che siano soddisfatti i requisiti di hello.
2. che siano soddisfatti tooensure che richiede la connettività, esaminare hello elenco di provider di servizi e i percorsi hello [ExpressRoute partner e i percorsi](expressroute-locations.md) articolo.
3. Per pianificare i requisiti relativi alla capacità, vedere la pagina relativa alla [pianificazione e al perfezionamento delle prestazioni di rete per Office 365](http://aka.ms/tune/).
4. Seguire i passaggi di hello elencati in hello tooset di flussi di lavoro della connettività [flussi di lavoro di ExpressRoute per provisioning del circuito e lo stato del circuito](expressroute-workflows.md).

> [!IMPORTANT]
> Assicurarsi che è stato abilitato componente aggiuntivo di ExpressRoute premium quando la configurazione di servizi di integrazione applicativa tooOffice 365 e Dynamics 365.
> 
> 

### <a name="do-i-need-tooenable-azure-public-peering-tooconnect-toooffice-365-services-and-dynamics-365"></a>È necessario tooenable Azure pubblica peering tooconnect tooOffice 365 services e Dynamics 365?

No, è necessario solo tooenable Peering Microsoft. TooAzure il traffico di autenticazione AD verrà inviato tramite il Peering Microsoft. 

### <a name="can-my-existing-expressroute-circuits-support-connectivity-toooffice-365-services-and-dynamics-365"></a>My circuiti ExpressRoute esistenti supporta servizi di integrazione applicativa tooOffice 365 e Dynamics 365?

Sì. Il circuito ExpressRoute esistente può essere configurato toosupport connettività tooOffice 365 services. Assicurarsi di disporre di sufficiente capacità tooconnect tooOffice 365 i servizi e che è stato abilitato un componente aggiuntivo premium. [Pianificazione e al perfezionamento delle prestazioni di rete per Office 365](http://aka.ms/tune/) aiuta a pianificare le esigenze di connettività. Vedere inoltre [Creare e modificare un circuito ExpressRoute](expressroute-howto-circuit-classic.md).

### <a name="what-office-365-services-can-be-accessed-over-an-expressroute-connection"></a>A quali servizi di Office 365 è possibile accedere tramite una connessione ExpressRoute?

Fare riferimento troppo[gli intervalli di indirizzi IP e gli URL di Office 365](http://aka.ms/o365endpoints) pagina per un elenco aggiornato dei servizi supportati tramite ExpressRoute.

### <a name="how-much-does-expressroute-for-office-365-services-and-dynamics-365-cost"></a>Quanto costa ExpressRoute per i servizi di Office 365 e Dynamics 365?

Servizi di Office 365 e Dynamics 365 richiedono toobe di componente aggiuntivo premium abilitato. Vedere hello [pagina dei dettagli dei prezzi](https://azure.microsoft.com/pricing/details/expressroute/) di costi.

### <a name="what-regions-is-expressroute-for-office-365-supported-in"></a>In quali aree è supportato ExpressRoute per Office 365?

Vedere [Partner e località di peering per Azure ExpressRoute](expressroute-locations.md) per ottenere informazioni.

### <a name="can-i-access-office-365-over-hello-internet-even-if-expressroute-was-configured-for-my-organization"></a>È possibile accedere Office 365 su hello Internet, anche se per l'organizzazione è stato configurato ExpressRoute?

Sì. Gli endpoint del servizio di 365 Office sono raggiungibili tramite hello Internet, anche se è stato configurato ExpressRoute per la rete. Se trovano in un percorso di servizi di 365 tooOffice tooconnect configurato tramite ExpressRoute, verrà effettuata la connessione tramite ExpressRoute.

### <a name="can-i-access-office-365-us-government-community-gcc-services-over-an-azure-us-government-expressroute-circuit"></a>È possibile accedere ai servizi US Government Community (GCC) di Office 365 tramite un circuito ExpressRoute di Azure per enti pubblici statunitensi?

Sì. Gli endpoint del servizio di Office 365 GCC sono raggiungibili tramite hello Azure US Government ExpressRoute. Tuttavia, è prima necessario tooopen ticket di supporto su hello prefissi hello tooprovide portale Azure si intende tooadvertise tooMicrosoft. Verranno stabiliti la connettività tooOffice 365 GCC servizi dopo il ticket di supporto hello viene risolto. 

### <a name="can-dynamics-365-for-operations-formerly-known-as-dynamics-ax-online-be-accessed-over-an-expressroute-connection"></a>È possibile accedere a Dynamics 365 for Operations (noto in precedenza come) Dynamics AX Online tramite una connessione ExpressRoute?

Sì. [Dynamics 365 for Operations](https://www.microsoft.com/dynamics365/operations) è ospitato in Azure. È possibile abilitare peering pubblico di Azure sul tooit di tooconnect circuito ExpressRoute.

## <a name="route-filters-for-microsoft-peering"></a>Filtri di route per il peering Microsoft

### <a name="i-am-turning-on-microsoft-peering-for-hello-first-time-what-routes-will-i-see"></a>Sono accensione peering Microsoft hello per la prima volta, le route viene visualizzata?

Non verrà visualizzata nessuna route. È necessario tooattach gli annunci di prefisso una route filtro tooyour circuito toostart. Per istruzioni, vedere [Configurare i filtri di route per il peering Microsoft](how-to-routefilter-powershell.md).

### <a name="i-turned-on-microsoft-peering-and-now-i-am-trying-tooselect-exchange-online-but-it-is-giving-me-an-error-that-i-am-not-authorized-toodo-it"></a>L'attivazione nel peering Microsoft e ora sono tooselect durante il tentativo Exchange Online, ma me contenente un errore che non si è autorizzato toodo.

Quando si usano filtri di route, tutti i clienti possono attivare il peering Microsoft. Tuttavia, per l'utilizzo di servizi di Office 365, è comunque necessario tooget autorizzata da Office 365.

### <a name="do-i-need-tooget-authorization-for-turning-on-dynamics-365-over-microsoft-peering"></a>È necessario tooget autorizzazione per l'attivazione tramite il peering Microsoft Dynamics 365?

No, non è necessaria l'autorizzazione per Dynamics 365. È possibile creare una regola e selezionare la community di Dynamics 365 senza autorizzazione.

### <a name="i-already-have-microsoft-peering-how-can-i-take-advantage-of-route-filters"></a>Dispongo già del peering Microsoft, come posso usare al meglio i filtri di route?

È possibile creare un filtro di route, servizi selezionare hello desiderato toouse e collegare hello peering Microsoft tooyour filtro. Per istruzioni, vedere [Configurare i filtri di route per il peering Microsoft](how-to-routefilter-powershell.md).

### <a name="i-have-microsoft-peering-at-one-location-now-i-am-trying-tooenable-it-at-another-location-and-i-am-not-seeing-any-prefixes"></a>È necessario Microsoft peering in una posizione, ora sto cercando tooenable in un'altra posizione e non vengono visualizzati tutti i prefissi degli spazi.

* Microsoft peering di circuiti ExpressRoute che sono stati configurati precedente tooAugust 1, 2017 disporrà di tutti i prefissi di servizio pubblicati tramite Microsoft peering, anche se non sono definiti i filtri di route.

* Microsoft peering di circuiti ExpressRoute configurati o dopo il 1 agosto 2017 non avrà alcun prefisso annunciato fino a quando non è associato un filtro di route toohello circuito. Per impostazione predefinita, non verrà visualizzato alcun prefisso.
