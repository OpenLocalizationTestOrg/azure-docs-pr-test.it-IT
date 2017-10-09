---
title: routing aaaAsymmetric | Documenti Microsoft
description: "In questo articolo illustra i problemi di hello che un cliente potrebbe venire con il routing asimmetrica in una rete con più collegamenti tooa destinazione."
documentationcenter: na
services: expressroute
author: osamazia
manager: carmonm
editor: 
ms.assetid: a754bff9-95c9-44b5-9796-377fc21e8322
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: osamam
ms.openlocfilehash: 01a16242437a3674dcfe27b074911a829a6c1abd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="asymmetric-routing-with-multiple-network-paths"></a>Routing asimmetrico con più percorsi di rete
Questo articolo illustra il modo in cui il traffico di rete di inoltro e di ritorno può seguire route diverse quando sono disponibili più percorsi tra l'origine e la destinazione di rete.

È importante toounderstand due concetti toounderstand asimmetrica di routing. Uno è effetto hello di più percorsi di rete. altri Hello è come i dispositivi, ad esempio un firewall, mantenere lo stato. Questi tipi di dispositivi sono detti dispositivi con stato. Una combinazione di questi due fattori crea gli scenari in rete a cui il traffico viene eliminato da un dispositivo con stato perché il dispositivo con stato hello è stato rilevato che il traffico è stato originato con dispositivo hello stesso.

## <a name="multiple-network-paths"></a>Più percorsi di rete
Quando una rete aziendale ha solo un collegamento toohello, passa a Internet tramite il provider di servizi Internet, tutto il traffico tooand da hello Internet hello stesso percorso. Spesso le società acquistano più circuiti, come percorsi ridondanti, tooimprove tempo di attività. In questo caso, è possibile che il traffico che passa all'esterno delle rete hello, toohello Internet, passa attraverso un collegamento e hello restituiscono il traffico passa attraverso un collegamento diverso. Questa approccio viene definito comunemente routing asimmetrico. Nel routing asimmetrica, inversa il traffico di rete un percorso diverso rispetto al flusso originale hello.

![Rete con più percorsi](./media/expressroute-asymmetric-routing/AsymmetricRouting3.png)

Anche se si verifica principalmente in hello Internet, anche routing asimmetrica applica tooother combinazioni di più percorsi. Si applica, ad esempio, percorso Internet tooan sia un percorso privato che toohello stessa destinazione e i percorsi privati toomultiple che toohello stessa destinazione.

Ogni router lungo il percorso di hello, dall'origine toodestination, Calcola hello migliore percorso tooreach una destinazione. determinazione del router del percorso possibili migliore Hello è basata su due fattori principali:

* Il routing tra le reti esterne è basato sul protocollo di routing, ovvero il protocollo BGP (Border Gateway Protocol). BGP Accetta annunci da altre istanze e li esegue attraverso una serie di passaggi toodetermine hello percorso toohello destinato destinazione migliore. Percorso migliore hello archivia nella tabella di routing.
* lunghezza Hello di una subnet mask associata a una route influisce sui percorsi di routing. Se un router riceve più annunci per hello stesso indirizzo IP, ma con subnet mask diverse, i router hello preferisce annuncio hello con più subnet mask perché è considerata un percorso più specifico.

## <a name="stateful-devices"></a>Dispositivi con stato
Router esaminare hello IP intestazione di un pacchetto per il routing. Alcuni dispositivi esaminare più in dettaglio all'interno di pacchetti hello. Questi dispositivi esaminano in genere le intestazioni di tipo Layer4, ovvero TCP (Transmission Control Protocol) o UDP (User Datagram Protocol) oppure addirittura di tipo Layer7 (livello dell'applicazione). Si tratta di dispositivi di sicurezza o di dispositivi di ottimizzazione della larghezza di banda. 

Un esempio comune di dispositivo con stato è rappresentato dal firewall. Un firewall consente o nega il toopass un pacchetto tramite le relative interfacce in base ai vari campi come protocollo, porta TCP/UDP e intestazioni di URL. Questo livello di analisi dei pacchetti inserisce un pesante carico di elaborazione nel dispositivo hello. prestazioni tooimprove, firewall hello analizza pacchetto prima di hello di un flusso. Se è consentito tooproceed pacchetti hello, mantiene le informazioni sul flusso hello nella tabella dello stato. Sono consentiti tutti i pacchetti successivi toothis correlati flusso basato sulla determinazione iniziale hello. Un pacchetto che fa parte di un flusso esistente può arrivare al firewall hello. Se firewall hello non ha informazioni di stato precedenti, firewall hello Elimina i pacchetti hello.

## <a name="asymmetric-routing-with-expressroute"></a>Routing asimmetrico con ExpressRoute
Quando ci si connette tooMicrosoft tramite Azure ExpressRoute, le modifiche di rete come segue:

* Si dispone di più collegamenti tooMicrosoft. Un collegamento è la connessione Internet esistente e altri hello è tramite ExpressRoute. Alcuni tooMicrosoft traffico potrebbe passare attraverso Internet hello ma tornare tramite ExpressRoute o viceversa.
* Tramite ExpressRoute si ricevono indirizzi IP più specifici. In tal caso, per il traffico proveniente da tooMicrosoft la rete per servizi offerti tramite ExpressRoute, router è sempre preferiscono ExpressRoute.

toounderstand hello effetto queste due modifiche in una rete, si prendano in considerazione alcuni scenari. Ad esempio, si dispone di un solo circuito toohello Internet e si utilizzano tutti i servizi Microsoft tramite Internet hello. traffico Hello da attraversa di tooMicrosoft e di nuovo la rete hello stesso collegamento Internet e passa attraverso il firewall hello. i record di firewall Hello hello flusso come si vede il pacchetto prima di hello e restituisce i pacchetti sono consentiti perché flusso hello esiste nella tabella di stato hello.

![Routing asimmetrico con ExpressRoute](./media/expressroute-asymmetric-routing/AsymmetricRouting1.png)

A questo punto si abilita ExpressRoute e si utilizzano i servizi offerti da Microsoft tramite ExpressRoute. Tutti gli altri servizi di Microsoft vengono utilizzati su hello Internet. Si distribuisce un firewall separate del bordo che è connesso tooExpressRoute. Microsoft annuncia rete tooyour di prefissi più specifici tramite ExpressRoute per servizi specifici. L'infrastruttura di routing sceglie ExpressRoute come percorso preferito di hello per tali prefissi. Se non si annuncia il tooMicrosoft di indirizzi IP pubblici tramite ExpressRoute, in cui Microsoft comunica con gli indirizzi IP pubblici tramite hello Internet. Inoltrare il traffico da tooMicrosoft la rete utilizza ExpressRoute e inversa il traffico proveniente da Microsoft hello Internet. Quando il firewall hello bordo hello rileva un pacchetto di risposta per un flusso che non viene trovato nella tabella di stato hello, Elimina il traffico di ritorno hello.

Se si sceglie di hello toouse stessa conversione indirizzi di rete (NAT) dal pool per ExpressRoute e per Internet hello, vedrai problemi analoghi con client hello nella rete sugli indirizzi IP privati. Le richieste per servizi quali Windows Update passare tramite hello Internet perché gli indirizzi IP per questi servizi non vengono annunciati tramite ExpressRoute. Tuttavia, il traffico di ritorno hello vengono restituiti tramite ExpressRoute. Se Microsoft riceve un indirizzo IP con hello stesso la subnet mask dall'hello Internet ed ExpressRoute, privilegia ExpressRoute hello Internet. Se un firewall o un altro dispositivo con stato che si trovano i margini della rete e con connessione ExpressRoute non dispone di alcuna informazione sul flusso hello precedente, Elimina i pacchetti hello appartenenti toothat flusso.

## <a name="asymmetric-routing-solutions"></a>Soluzioni per il routing asimmetrico
Si dispone di due problema di hello toosolve le principali opzioni di routing asimmetrica. Uno è tramite il routing e hello altri prevede l'uso di origine basato su NAT (SNAT).

### <a name="routing"></a>Routing.
Verificare che gli indirizzi IP pubblici siano collegamenti tooappropriate annunciato wide area network (WAN). Ad esempio, se si desidera toouse hello Internet per il traffico di autenticazione ed ExpressRoute per il traffico di posta elettronica, non deve annunciare gli indirizzi IP pubblici di Active Directory Federation Services (ADFS) tramite ExpressRoute. Analogamente, assicurarsi che non tooexpose un locale gli indirizzi tooIP di server AD FS hello router riceve tramite ExpressRoute. Le route ricevute tramite ExpressRoute sono più specifiche in modo che siano percorso preferito di hello ExpressRoute per tooMicrosoft il traffico di autenticazione. dando luogo al routing asimmetrico.

Se si desidera toouse ExpressRoute per l'autenticazione, assicurarsi che si desidera annunciare gli indirizzi IP pubblici di ADFS tramite ExpressRoute senza NAT. In questo modo, il traffico che proviene da Microsoft e passa tooan locale server AD FS passa tramite ExpressRoute. Traffico di ritorno tooMicrosoft cliente Usa ExpressRoute perché è route preferito hello su hello Internet.

### <a name="source-based-nat"></a>Source NAT
È possibile risolvere i problemi del routing asimmetrico anche tramite SNAT. Ad esempio, non sono annunciate hello indirizzo IP di un server Simple Mail Transfer Protocol (SMTP) locale tramite ExpressRoute intendi hello toouse Internet per questo tipo di comunicazione. Una richiesta che ha origine da Microsoft e quindi passa tooyour locale server SMTP attraversa hello Internet. Si SNAT hello indirizzo IP di ingresso richiesta tooan interno. Inversa dal server SMTP hello del traffico toohello firewall periferico (che si utilizza per NAT) anziché tramite ExpressRoute. il traffico di ritorno Hello torna tramite hello Internet.

![Configurazione della rete con Source NAT](./media/expressroute-asymmetric-routing/AsymmetricRouting2.png)

## <a name="asymmetric-routing-detection"></a>Rilevamento del routing asimmetrico
Traceroute è hello migliore modo toomake che il traffico di rete che attraversa percorso hello previsto. Se si prevede che il traffico dal percorso del locale SMTP server tooMicrosoft tootake hello Internet, hello previsto traceroute è da hello SMTP server tooOffice 365. risultato Hello convalida che il traffico in uscita effettivamente da rete verso Internet hello e non per ExpressRoute.

