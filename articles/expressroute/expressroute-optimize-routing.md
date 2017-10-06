---
title: 'Ottimizzare il routing in ExpressRoute: Azure | Microsoft Docs'
description: "Questa pagina fornisce informazioni dettagliate su come toooptimize routing quando si dispone di più ExpressRoute circuiti che la connessione tra Microsoft e la rete aziendale."
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
ms.openlocfilehash: ebcfb638f67a9ac78c3e476668bfd0bb0ffb9985
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-expressroute-routing"></a>Ottimizzare il routing in ExpressRoute
Quando si dispone di più circuiti ExpressRoute, è necessario più di un percorso tooconnect tooMicrosoft. Di conseguenza, il routing non ottimali può verificarsi -, ovvero il traffico potrebbe richiedere un tooreach percorso più lungo, Microsoft e Microsoft tooyour network. Hello più hello percorso di rete, una latenza maggiore hello hello. che ha un impatto diretto sull'esperienza utente e sulle prestazioni dell'applicazione. In questo articolo verrà spiegare il problema e spiegare come toooptimize ciclo tramite hello tecnologie standard di routine.

## <a name="suboptimal-routing-from-customer-toomicrosoft"></a>Non ottimali routing dal cliente tooMicrosoft
Esaminiamo un Chiudi problema di routing hello da un esempio. Si supponga di che disporre di due uffici hello Stati Uniti, uno a Los Angeles e uno di New York. Gli uffici sono connessi tramite una rete WAN (Wide Area Network), che può essere la propria rete backbone o la VPN IP del provider di servizi. Si dispone di due circuiti ExpressRoute, uno negli Stati Uniti occidentali e uno negli Stati Uniti orientali, anche connessi hello WAN. Ovviamente, si dispone di rete di due percorsi tooconnect toohello Microsoft. Si supponga ora di avere una distribuzione di Azure, ad esempio il servizio app di Azure, negli Stati Uniti occidentali e negli Stati Uniti orientali. L'intenzione è tooconnect dagli utenti nel Los Angeles tooAzure Stati Uniti occidentali e gli utenti in New York tooAzure Stati Uniti orientali, perché l'amministratore del servizio annuncia che agli utenti di ogni accesso office hello nelle vicinanze di servizi di Azure per un'esperienza ottimale. Sfortunatamente, il piano di hello avviene anche per gli utenti di costa orientale hello ma non per gli utenti di hello costa occidentale. causa Hello del problema di hello è seguente hello. Su ogni circuito ExpressRoute, si identificano tooyou prefisso hello in Azure Stati Uniti orientali (23.100.0.0/16) sia il prefisso hello in Azure Stati Uniti occidentali (13.100.0.0/16). Se non si conosce il prefisso dal quale area, non si è in grado di tootreat, in modo diverso. La rete WAN sembrare entrambi i prefissi hello sono orientale tooUS più vicino di Stati Uniti occidentali e quindi indirizzare entrambi toohello agli utenti di office circuito ExpressRoute negli Stati Uniti orientali. Fine hello, sarà necessario numerosi utenti scontenti hello Los Angeles office.

![Problema di ExpressRoute caso 1 - non ottimale routing dal cliente tooMicrosoft](./media/expressroute-optimize-routing/expressroute-case1-problem.png)

### <a name="solution-use-bgp-communities"></a>Soluzione: usare BGP Community
toooptimize routing per entrambi gli utenti di office, è necessario tooknow il prefisso è dall'Azure Stati Uniti occidentali e da Azure Stati Uniti orientali. Queste informazioni vengono codificate con i [valori di BGP Community](expressroute-routing.md). È stato assegnato un tooeach di valore univoco di Community BGP regione di Azure, ad esempio "12076:51004" per gli Stati Uniti orientali, "12076:51006" per gli Stati Uniti occidentali. Dopo aver appreso da quale area di Azure proviene ogni prefisso, si può scegliere il circuito ExpressRoute da configurare come preferito. Poiché si usa informazioni di routing di hello BGP tooexchange, è possibile utilizzare tooinfluence di preferenza locale BGP routing. In questo esempio, è possibile assegnare una versione successiva locale preferenza valore too13.100.0.0/16 negli Stati Uniti occidentali rispetto negli Stati Uniti orientali e, in modo analogo, una versione successiva locale preferenza valore too23.100.0.0/16 negli Stati Uniti orientali negli Stati Uniti occidentali. Questa configurazione garantisce che, quando entrambi i percorsi tooMicrosoft sono disponibili, gli utenti a Los Angeles avrà il circuito ExpressRoute hello in Stati Uniti occidentali tooconnect tooAzure Stati Uniti occidentali mentre gli utenti di New York accettano hello ExpressRoute in Stati Uniti orientali tooAzure Stati Uniti orientali . Il routing è ottimizzato su entrambi i lati. 

![Soluzione caso 1 ExpressRoute: usare BGP Community](./media/expressroute-optimize-routing/expressroute-case1-solution.png)

> [!NOTE]
> Hello stessa tecnica, preferenza locale, può essere applicato toorouting dal cliente tooAzure rete virtuale. Non è contrassegnare i prefissi di toohello valore BGP Community annunciati dalla rete di Azure tooyour. Tuttavia, poiché si sa quali la distribuzione di rete virtuale Chiudi toowhich dell'ufficio, è possibile configurare i router conseguenza tooanother circuito ExpressRoute di una tooprefer.
>
>

## <a name="suboptimal-routing-from-microsoft-toocustomer"></a>Routing di Microsoft toocustomer ottimale
Di seguito è riportato un altro esempio in cui le connessioni da Microsoft richiedono un tooreach percorso più lungo della rete. In questo caso, si usano i server di Exchange in locale ed Exchange Online in un [ambiente ibrido](https://technet.microsoft.com/library/jj200581%28v=exchg.150%29.aspx). Uffici sono connesso tooa WAN. Annunciare prefissi hello dei server locali in entrambi i tooMicrosoft uffici attraverso i circuiti ExpressRoute hello due. Exchange Online verrà avviata connessioni toohello ai server locali in casi come la migrazione delle cassette postali. Sfortunatamente, hello connessione tooyour di Los Angeles è indirizzato toohello circuito ExpressRoute negli Stati Uniti orientali prima dell'attraversamento costa occidentale di hello intero toohello indietro continent. causa del problema hello Hello è simile toohello un primo. Senza un hint, rete Microsoft hello non è possibile indicare il prefisso del cliente è orientale tooUS Chiudi e quello che è chiudere tooUS occidentale. Si verifica toopick office tooyour del percorso non valido di hello Los Angeles.

![ExpressRoute caso 2: routing di Microsoft toocustomer ottimale](./media/expressroute-optimize-routing/expressroute-case2-problem.png)

### <a name="solution-use-as-path-prepending"></a>Soluzione: anteporre AS PATH
Esistono due problema toohello di soluzioni. Hello prima uno consiste semplicemente annunciare il prefisso locale per l'ufficio di Los Angeles, 177.2.0.0/31, nel circuito ExpressRoute hello negli Stati Uniti occidentali e locale del prefisso per l'ufficio di New York, 177.2.0.2/31, nel circuito ExpressRoute hello negli Stati Uniti orientali. Di conseguenza, vi è solo un percorso per Microsoft tooconnect tooeach ufficio. Non esistono ambiguità e il routing risulta ottimizzato. Con questa struttura, è necessario toothink sulla strategia di failover. In hello evento che hello tooMicrosoft percorso tramite ExpressRoute è interrotto, è necessario assicurarsi che Exchange Online possono comunque connettersi server locali tooyour toomake. 

seconda soluzione hello è che si continua tooadvertise entrambi i prefissi hello in due circuiti ExpressRoute e inoltre si fornisce un hint di individuare quale prefisso è toowhich Chiudi uno ufficio. Poiché un sostegno anteponendo percorso AS BGP, è possibile configurare hello come percorso per il routing di tooinfluence il prefisso. In questo esempio, è possibile prolungare hello percorso AS per 172.2.0.0/31 negli Stati Uniti orientali, in modo che si preferisce circuito ExpressRoute di hello negli Stati Uniti occidentali per il traffico destinato per il prefisso (come la rete verrà ritenuto prefisso toothis di hello percorso più breve in occidentale hello). Analogamente è possibile prolungare hello percorso AS per 172.2.0.2/31 negli Stati Uniti occidentali, in modo che verrà preferiamo circuito ExpressRoute hello negli Stati Uniti orientali. Il routing è ottimizzato per entrambi gli uffici. Con questa progettazione, se un circuito ExpressRoute viene interrotto, Exchange Online può comunque raggiungere il cliente tramite un altro circuito ExpressRoute e la rete WAN. 

> [!IMPORTANT]
> Si rimuove private i numeri di hello come percorso per i prefissi hello ricevuti nel Peering Microsoft. È necessario tooappend pubblica come numeri in hello percorso AS tooinfluence routing per il Peering Microsoft.
> 
> 

![Soluzione caso 2 ExpressRoute: anteporre AS PATH](./media/expressroute-optimize-routing/expressroute-case2-solution.png)

> [!NOTE]
> Negli esempi di hello forniti di seguito sono per Microsoft e di peering pubblico, è supportato hello stesse funzionalità per il peering privato hello. Inoltre, hello percorso AS anteponendo funziona all'interno di un singolo circuito ExpressRoute, selezione hello tooinfluence dei percorsi di hello primario e secondario.
> 
> 

## <a name="suboptimal-routing-between-virtual-networks"></a>Routing non ottimale tra reti virtuali
Con ExpressRoute, è possibile abilitare la rete virtuale tooVirtual rete (che è noto anche come "Reti virtuali") collegando il circuito ExpressRoute tooan la comunicazione. Quando vengono collegati circuiti ExpressRoute toomultiple, routing non ottimali può verificarsi tra reti virtuali hello. Si consideri ad esempio di avere due circuiti ExpressRoute, uno negli Stati Uniti occidentali e uno negli Stati Uniti orientali. In ogni area sono presenti due reti virtuali, I server web vengono distribuiti in una rete virtuale e server applicazioni in hello altri. Per garantire la ridondanza, si collega hello due reti virtuali in ogni area tooboth hello locale il circuito ExpressRoute e hello remoto circuito ExpressRoute. Come può essere illustrato di seguito, da ogni rete virtuale sono presenti due percorsi toohello altra rete virtuale. le reti virtuali Hello non conoscono il circuito ExpressRoute locale e quello remoto. Di conseguenza come avviene il traffico tra reti della rete virtuale tooload saldo routing uguale-Cost Multi Path ECMP (), alcuni flussi di traffico richiederà percorso più lungo di hello e vengono instradati al circuito ExpressRoute remoto hello.

![Caso 3 ExpressRoute: routing non ottimale tra reti virtuali](./media/expressroute-optimize-routing/expressroute-case3-problem.png)

### <a name="solution-assign-a-high-weight-toolocal-connection"></a>Soluzione: assegnare una connessione di toolocal peso elevata
soluzione hello è semplice. Poiché si conosce la posizione circuiti di reti virtuali e hello hello, è possibile fornire il percorso di ogni rete virtuale deve utilizzare. In modo specifico per questo esempio, si assegna una maggiore peso toohello connessione locale di connessione remota toohello (vedere l'esempio di configurazione hello [qui](expressroute-howto-linkvnet-arm.md#modify-a-virtual-network-connection)). Quando una rete virtuale riceve prefisso hello di hello altre reti virtuali in più connessioni preferiranno connessione hello con hello massimo peso toosend il traffico destinato a tale prefisso.

![Soluzione ExpressRoute caso 3: assegnare un peso elevata toolocal connessione](./media/expressroute-optimize-routing/expressroute-case3-solution.png)

> [!NOTE]
> È anche possibile influenzare routing dalla rete locale tooyour di rete virtuale, se si dispone di più circuiti ExpressRoute, configurando il peso di hello di una connessione anziché applicare percorso AS anteponendo, una tecnica descritta in hello secondo scenario precedente. Per ogni prefisso, verranno sempre esaminati peso connessione hello prima hello lunghezza del percorso AS quando si decide come toosend traffico.
>
>
