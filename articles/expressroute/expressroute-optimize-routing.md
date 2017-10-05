---
title: 'Ottimizzare il routing in ExpressRoute: Azure | Microsoft Docs'
description: "Questa pagina contiene informazioni dettagliate su come ottimizzare il routing in presenza di più circuiti ExpressRoute per la connessione tra Microsoft e la rete aziendale."
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: 
ms.assetid: fca53249-d9c3-4cff-8916-f8749386a4dd
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/06/2017
ms.author: charwen
ms.openlocfilehash: c3a85b9445d69330c3f6c7d298169efddb6ecca0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="optimize-expressroute-routing"></a>Ottimizzare il routing in ExpressRoute
In presenza di più circuiti ExpressRoute sono disponibili più percorsi per connettersi a Microsoft. Il routing può quindi risultare non ottimale, ovvero è possibile che il traffico usi un percorso più lungo per raggiungere Microsoft e da Microsoft la rete del cliente. Più lungo è il percorso di rete, maggiore sarà la latenza che ha un impatto diretto sull'esperienza utente e sulle prestazioni dell'applicazione. Questo articolo descrive il problema e illustra come ottimizzare il routing con tecnologie di routing standard.

## <a name="suboptimal-routing-from-customer-to-microsoft"></a>Routing non ottimale dal cliente a Microsoft
Per esaminare il problema di routing si userà un esempio. Si supponga di avere due sedi negli Stati Uniti: una a Los Angeles e una a New York. Gli uffici sono connessi tramite una rete WAN (Wide Area Network), che può essere la propria rete backbone o la VPN IP del provider di servizi. Sono disponibili due circuiti ExpressRoute, uno negli Stati Uniti occidentali e uno negli Stati Uniti orientali, anch'essi connessi tramite la rete WAN. Naturalmente, per la connessione alla rete Microsoft esistono due percorsi. Si supponga ora di avere una distribuzione di Azure, ad esempio il servizio app di Azure, negli Stati Uniti occidentali e negli Stati Uniti orientali. Si vogliono connettere gli utenti di Los Angeles alla distribuzione di Azure negli Stati Uniti occidentali e gli utenti di New York alla distribuzione di Azure negli Stati Uniti orientali perché, secondo quanto annunciato dall'amministratore del servizio, per assicurare esperienze ottimali è consigliabile che gli utenti di ogni ufficio accedano ai servizi di Azure nelle vicinanze. Sfortunatamente, il piano funziona correttamente per gli utenti della costa orientale, ma non per quelli della costa occidentale. Di seguito è riportata la causa del problema. In ogni circuito ExpressRoute vengono pubblicati sia il prefisso di Azure negli Stati Uniti orientali (23.100.0.0/16) che il prefisso di Azure negli Stati Uniti occidentali (13.100.0.0/16). Se non si conosce l'area di provenienza di un prefisso, non si potrà differenziarne la gestione. Ritenendo che entrambi i prefissi siano più vicini agli Stati Uniti orientali rispetto agli Stati Uniti occidentali, la rete WAN potrebbe indirizzare gli utenti di entrambi gli uffici al circuito ExpressRoute negli Stati Uniti orientali. Molti utenti nell'ufficio di Los Angeles avranno di conseguenza un'esperienza insoddisfacente.

![Problema caso 1 ExpressRoute: routing non ottimale dal cliente a Microsoft](./media/expressroute-optimize-routing/expressroute-case1-problem.png)

### <a name="solution-use-bgp-communities"></a>Soluzione: usare BGP Community
Per ottimizzare il routing per gli utenti di entrambi gli uffici, è necessario sapere quale prefisso proviene da Azure negli Stati Uniti occidentali e quale da Azure negli Stati Uniti orientali. Queste informazioni vengono codificate con i [valori di BGP Community](expressroute-routing.md). È stato assegnato un valore di BGP Community univoco per ogni area di Azure, ad esempio "12076:51004" per gli Stati Uniti orientali, "12076:51006" per gli Stati Uniti occidentali. Dopo aver appreso da quale area di Azure proviene ogni prefisso, si può scegliere il circuito ExpressRoute da configurare come preferito. Poiché si usa BGP per lo scambio di informazioni di routing, è possibile usare il valore di BGP relativo alla preferenza locale per determinare il routing. In questo esempio è possibile assegnare un valore di preferenza locale 13.100.0.0/16 più alto negli Stati Uniti occidentali di quello negli Stati Uniti orientali e, in modo analogo, un valore di preferenza locale 23.100.0.0/16 più alto negli Stati Uniti orientali rispetto a quello negli Stati Uniti occidentali. Questa configurazione garantirà che, quando sono disponibili entrambi i percorsi per connettersi a Microsoft, gli utenti di Los Angeles useranno il circuito ExpressRoute negli Stati Uniti occidentali per connettersi ad Azure negli Stati Uniti occidentali, mentre gli utenti di New York useranno il circuito ExpressRoute negli Stati Uniti orientali per connettersi ad Azure negli Stati Uniti orientali. Il routing è ottimizzato su entrambi i lati. 

![Soluzione caso 1 ExpressRoute: usare BGP Community](./media/expressroute-optimize-routing/expressroute-case1-solution.png)

> [!NOTE]
> La stessa tecnica, con la preferenza locale, può essere applicata al routing dal cliente alla rete virtuale di Azure. I prefissi annunciati da Azure alla rete del cliente non vengono contrassegnati con il valore di BGP Community. Dato che si sa quale distribuzione della rete virtuale è vicina a un determinato ufficio, tuttavia, è possibile configurare i router di conseguenza in modo che venga preferito un circuito ExpressRoute rispetto a un altro.
>
>

## <a name="suboptimal-routing-from-microsoft-to-customer"></a>Routing non ottimale da Microsoft al cliente
Ecco un altro esempio in cui le connessioni da Microsoft usano un percorso più lungo per raggiungere la rete del cliente. In questo caso, si usano i server di Exchange in locale ed Exchange Online in un [ambiente ibrido](https://technet.microsoft.com/library/jj200581%28v=exchg.150%29.aspx). Gli uffici sono connessi a una rete WAN. Si annunciano a Microsoft i prefissi dei server locali in entrambi gli uffici tramite i due circuiti ExpressRoute. Nel caso, ad esempio, di migrazione delle cassette postali, Exchange Online avvierà le connessioni ai server locali. La connessione all'ufficio di Los Angeles viene purtroppo instradata al circuito ExpressRoute negli Stati Uniti orientali, attraversando l'intero continente prima di ritornare alla costa occidentale. La causa di questo problema è simile a quella del primo. Senza indicazioni la rete Microsoft non può stabilire quale prefisso del cliente è più vicino agli Stati Uniti orientali e quale agli Stati Uniti occidentali. Può quindi accadere che venga scelga il percorso errato per l'ufficio di Los Angeles.

![Caso 2 ExpressRoute: routing non ottimale da Microsoft al cliente](./media/expressroute-optimize-routing/expressroute-case2-problem.png)

### <a name="solution-use-as-path-prepending"></a>Soluzione: anteporre AS PATH
Esistono due soluzioni al problema. La prima consiste semplicemente nell'annunciare il prefisso locale per l'ufficio di Los Angeles, 177.2.0.0/31, sul circuito ExpressRoute negli Stati Uniti occidentali e il prefisso locale per l'ufficio di New York, 177.2.0.2/31, sul circuito ExpressRoute negli Stati Uniti orientali. Di conseguenza, Microsoft avrà un solo percorso per connettersi agli uffici del cliente. Non esistono ambiguità e il routing risulta ottimizzato. Con questa progettazione è necessario considerare la strategia di failover. Nel caso di interruzione del percorso verso Microsoft tramite ExpressRoute, è necessario assicurarsi che Exchange Online possa comunque connettersi ai server locali. 

La seconda soluzione consiste nel continuare ad annunciare entrambi i prefissi in entrambi i circuiti ExpressRoute e, inoltre, indicare qual è il prefisso vicino a un determinato ufficio. Poiché è supportata l'anteposizione di AS PATH in BGP, si può configurare AS PATH nel prefisso per determinare il routing. In questo esempio si può estendere AS PATH per 172.2.0.0/31 negli Stati Uniti orientali, in modo che venga preferito il circuito ExpressRoute negli Stati Uniti occidentali per il traffico destinato a questo prefisso. La rete Microsoft considera infatti più breve il percorso per questo prefisso rispetto a quello negli Stati Uniti orientali. Allo stesso modo si può estendere AS PATH per 172.2.0.2/31 negli Stati Uniti occidentali, in modo che venga preferito il circuito ExpressRoute negli Stati Uniti orientali. Il routing è ottimizzato per entrambi gli uffici. Con questa progettazione, se un circuito ExpressRoute viene interrotto, Exchange Online può comunque raggiungere il cliente tramite un altro circuito ExpressRoute e la rete WAN. 

> [!IMPORTANT]
> I numeri AS privati in AS PATH per i prefissi ricevuti su peering Microsoft vengono rimossi. L'aggiunta di numeri AS pubblici in AS PATH è necessaria per determinare il routing per peering Microsoft.
> 
> 

![Soluzione caso 2 ExpressRoute: anteporre AS PATH](./media/expressroute-optimize-routing/expressroute-case2-solution.png)

> [!NOTE]
> Anche se gli esempi illustrati qui si riferiscono ai peer Microsoft e pubblici, le stesse funzionalità sono supportate per il peer privato. L'anteposizione di AS PATH funziona poi in un singolo circuito ExpressRoute, per determinare la selezione dei percorsi primari e secondari.
> 
> 

## <a name="suboptimal-routing-between-virtual-networks"></a>Routing non ottimale tra reti virtuali
Con ExpressRoute, è possibile abilitare la comunicazione da rete virtuale a rete virtuale collegando le reti virtuali a un circuito ExpressRoute. Se vengono collegate a più circuiti ExpressRoute, il routing tra le reti virtuali può risultare non ottimale. Si consideri ad esempio di avere due circuiti ExpressRoute, uno negli Stati Uniti occidentali e uno negli Stati Uniti orientali. In ogni area sono presenti due reti virtuali, in una sono distribuiti i server Web e nell'altra i server applicazioni. A scopo di ridondanza, si collegano le due reti virtuali di ogni area sia al circuito ExpressRoute locale che al circuito ExpressRoute remoto. Come illustrato di seguito, da ogni rete virtuale esistono due percorsi all'altra rete virtuale. Le reti virtuali non rilevano quale circuito ExpressRoute è locale e quale è invece remoto. Di conseguenza, eseguendo il routing ECMP (Equal-Cost-Multi-Path) per il bilanciamento del carico del traffico tra reti virtuali, alcuni flussi di traffico seguono il percorso più lungo e vengono instradati sul circuito ExpressRoute remoto.

![Caso 3 ExpressRoute: routing non ottimale tra reti virtuali](./media/expressroute-optimize-routing/expressroute-case3-problem.png)

### <a name="solution-assign-a-high-weight-to-local-connection"></a>Soluzione: assegnare un peso elevato alla connessione locale
La soluzione è semplice. Dato che la posizione delle reti virtuali e dei circuiti è nota, è possibile indicare il percorso che dovrà essere preferito da ogni rete virtuale. Per questo esempio, in particolare, si assegna alla connessione locale un peso superiore rispetto alla connessione remota (vedere l'esempio di configurazione [qui](expressroute-howto-linkvnet-arm.md#modify-a-virtual-network-connection)). Quando una rete virtuale riceve un prefisso dell'altra rete virtuale su più connessioni, per l'invio del traffico destinato a tale prefisso preferisce la connessione con il peso più elevato.

![Soluzione caso 3 ExpressRoute: assegnare un peso elevato alla connessione locale](./media/expressroute-optimize-routing/expressroute-case3-solution.png)

> [!NOTE]
> Per determinare il routing dalla rete virtuale alla rete locale, se si hanno più circuiti ExpressRoute, è anche possibile configurare il peso di una connessione anziché anteporre AS PATH applicando la tecnica descritta nel secondo scenario riportato sopra. Per ogni prefisso, per decidere come inviare il traffico verrà sempre esaminato il peso della connessione prima della lunghezza di AS PATH.
>
>
