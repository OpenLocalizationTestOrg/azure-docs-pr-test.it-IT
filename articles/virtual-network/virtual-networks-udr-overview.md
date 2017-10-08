---
title: le route definite aaaUser e l'inoltro IP in Azure | Documenti Microsoft
description: Informazioni su come le route definite dall'utente tooconfigure (UDR) e l'inoltro IP tooforward traffico toonetwork Appliance virtuali in Azure.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: c39076c4-11b7-4b46-a904-817503c4b486
ms.service: virtual-network
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f1f1d46166d5a7c776f472b7ade1354d943ece10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="user-defined-routes-and-ip-forwarding"></a>Route definite dall'utente e inoltro IP

Quando si aggiunta macchine virtuali (VM) tooa rete virtuale (VNet) in Azure, si noterà che le macchine virtuali hello siano in grado di toocommunicate tra loro attraverso la rete hello, automaticamente. Non è necessario un gateway, toospecify anche se hello macchine virtuali presenti in subnet diverse. Hello lo stesso vale per la comunicazione da hello macchine virtuali toohello rete Internet pubblica e rete locale di tooyour anche quando una connessione ibrida da Azure tooyour proprietario Data Center è presente.

Questo flusso di comunicazione è possibile poiché Azure Usa una serie di sistema route toodefine come flussi di traffico IP. Route di sistema di controllare il flusso di hello di comunicazione in hello seguenti scenari:

* Dall'interno hello stessa subnet.
* Da un tooanother subnet all'interno di una rete virtuale.
* Da macchine virtuali toohello Internet.
* Da una rete virtuale tooanother rete virtuale tramite un gateway VPN.
* Da una rete virtuale tooanother rete virtuale tramite il Peering di reti virtuali (concatenamento di servizio).
* Da una rete virtuale tooyour rete locale tramite un gateway VPN.

Hello riportato di seguito è illustrata un'installazione semplice con una rete virtuale, due subnet e alcune macchine virtuali, insieme a hello route di sistema che consentono di tooflow traffico IP.

![Route di sistema in Azure](./media/virtual-networks-udr-overview/Figure1.png)

Sebbene l'utilizzo di hello delle route di sistema facilita traffico automaticamente per la distribuzione, vi sono casi in cui si desidera toocontrol hello routing dei pacchetti tramite un dispositivo virtuale. È possibile pertanto mediante la creazione di route definite dall'utente che specificare dell'hop successivo per i pacchetti di propagazione appliance virtuale tooyour toogo subnet specifica tooa invece hello, e attivazione di indirizzi IP per l'inoltro hello macchina virtuale in esecuzione come appliance virtuale hello.

Hello figura seguente mostra un esempio di route definite dall'utente e inoltro tooforce pacchetti IP inviati tooone subnet da un altro toogo tramite un dispositivo virtuale su una subnet terzo.

![Route di sistema in Azure](./media/virtual-networks-udr-overview/Figure2.png)

> [!IMPORTANT]
> Le route definite dall'utente vengono applicati tootraffic lasciando una subnet provenienti da qualunque risorsa (ad esempio le interfacce di rete collegati tooVMs) in subnet hello. Non è possibile creare route toospecify come il traffico passa una subnet da hello Internet, per l'istanza. dispositivo di Hello che si desidera inoltrare il traffico toocannot trovarsi in hello stessa subnet in cui ha origine il traffico di hello. Creare sempre una subnet separata per i dispositivi. 
> 
> 

## <a name="route-resource"></a>Risorsa di route
I pacchetti vengono instradati in una rete TCP/IP in base a una tabella di route definita in ogni nodo nella rete fisica hello. Una tabella di routing è che un insieme di route singoli utilizzato toodecide in pacchetti tooforward basato su destinazione hello indirizzo IP. Una route è costituita dai seguenti hello:

| Proprietà | Descrizione | Vincoli | Considerazioni |
| --- | --- | --- | --- |
| Prefisso indirizzo |si applica la route hello Hello destinazione CIDR toowhich, ad esempio 10.1.0.0/16. |Deve essere un intervallo CIDR valido che rappresenta gli indirizzi di hello rete Internet pubblica, rete virtuale di Azure o Data Center locale. |Verificare che hello **prefisso dell'indirizzo** non contiene alcun indirizzo hello hello **indirizzo hop successivo**, in caso contrario i pacchetti verranno immesso in un ciclo dal hop successivo di hello origine toohello senza mai raggiungere destinazione Hello. |
| Tipo hop successivo |tipo di Hello del pacchetto di hello hop di Azure deve essere inviato. |Deve essere uno dei seguenti valori hello: <br/> **Rete virtuale**. Rappresenta una rete virtuale locale hello. Ad esempio, se si dispone di due subnet, 10.1.0.0/16 e 10.2.0.0/16 nella stessa rete virtuale di hello, route hello per ogni subnet nella tabella di route hello avrà un valore hop successivo di *rete virtuale*. <br/> **Gateway di rete virtuale**. Rappresenta un Gateway VPN S2S Azure. <br/> **Internet**. Rappresenta il gateway Internet hello predefinito fornito dall'infrastruttura di Azure hello. <br/> **Dispositivo virtuale**. Rappresenta un accessorio virtuale di cui è stato aggiunto tooyour rete virtuale di Azure. <br/> **Nessuno**. Rappresenta un black hole. I pacchetti inoltrati buco nero tooa non verranno inoltrati affatto. |È consigliabile utilizzare **Appliance virtuale** toodirect tooa macchina virtuale o il bilanciamento del carico di Azure indirizzo IP interno del traffico.  Questo tipo consente di specificare di hello di un indirizzo IP come descritto di seguito. È consigliabile utilizzare un **Nessuno** digitare pacchetti toostop dalla propagazione tooa dato di destinazione. |
| Indirizzo hop successivo |indirizzo dell'hop successivo Hello contiene l'indirizzo IP hello devono inoltrare i pacchetti. I valori hop successivi sono consentiti solo in route in cui è di tipo dell'hop successivo hello *Appliance virtuale*. |Deve essere un indirizzo IP raggiungibile all'interno di hello rete virtuale in cui viene applicata hello Route definita dall'utente, senza passare attraverso un **Virtual Network Gateway**. indirizzo IP Hello è toobe hello in caso di applicazione di rete virtuale stessa, o in una rete virtuale peered. |Se l'indirizzo IP hello rappresenta una macchina virtuale, assicurarsi di abilitare [inoltro IP](#IP-forwarding) in Azure per hello macchina virtuale. Se hello rappresenta hello interno indirizzo IP di bilanciamento del carico di Azure, assicurarsi di disporre della regola per ogni porta di bilanciamento del carico corrispondente si desidera bilanciare tooload.|

In Azure PowerShell alcuni dei valori di "NextHopType" hello hanno nomi diversi:

* Rete virtuale è VnetLocal
* Gateway di rete virtuale è VirtualNetworkGateway
* Appliance virtuale è VirtualAppliance
* Internet è Internet
* Nessuno è None

### <a name="system-routes"></a>Route di sistema
Ogni subnet creata in una rete virtuale viene associata automaticamente a una tabella di routing contenente hello segue le regole di sistema route:

* **Regola di rete virtuale locale**: questa regola viene creata automaticamente per ogni subnet in una rete virtuale. Specifica che è presente un collegamento diretto tra le macchine virtuali hello nella rete virtuale hello e non vi è alcun intermedia hop successivo.
* **Regola locale**: questa regola si applica a intervallo di indirizzi locali toohello tooall il traffico destinato e Usa il gateway VPN come destinazione dell'hop successivo hello.
* **Regola Internet**: questa regola gestisce tutto il traffico destinato toohello Internet pubblico (indirizzo prefisso 0.0.0.0/0) e gateway internet di infrastruttura utilizza hello come hello hop successivo per tutto il traffico destinato toohello Internet.

### <a name="user-defined-routes"></a>Route definite dall'utente
Per la maggior parte degli ambienti è necessario solo delle route sistema hello già definite da Azure. Tuttavia, è possibile necessario toocreate una tabella di routing e aggiungere una o più route in casi specifici, ad esempio:

* Il tunneling forzato toohello Internet tramite la rete locale.
* Utilizzo di dispositivi virtuali nell'ambiente Azure.

Negli scenari di hello precedenti, verrà dispone di una tabella di route toocreate e aggiungere tooit route definite dall'utente. È possibile avere più tabelle di route e hello stessa tabella di route può essere associati tooone o altre subnet. E ogni subnet può essere solo tabella singola route tooa associato. Tutte le macchine virtuali e servizi cloud in una subnet usare hello route tabella associata toothat subnet.

Subnet si basano sulle route di sistema fino a una tabella di routing associata toohello subnet. Una volta che esiste un’associazione,il routing viene eseguito in base alla corrispondenza più lunga del prefisso (LPM) tra le route definite dall'utente e le route predefinite. Se è presente più di una route con hello LPM stesso corrisponde una route è selezionata in base origine hello seguente ordine:

1. Route definita utente
2. Route BGP (quando viene utilizzato ExpressRoute)
3. La route di sistema

toolearn toocreate utente definizione route, vedere [come tooCreate instrada e attivare l'inoltro IP in Azure](virtual-network-create-udr-arm-template.md).

> [!IMPORTANT]
> Route definite dall'utente vengono applicati tooAzure solo le macchine virtuali e i servizi cloud. Ad esempio, se si desidera tooadd appliance virtuale firewall tra la rete locale e Azure, sarà necessario toocreate una route definita dall'utente per le tabelle di Azure di route per l'inoltro di tutto il traffico verso toohello locale indirizzo spazio toohello virtuale dispositivo. È inoltre possibile aggiungere che un utente definito route (UDR) toohello GatewaySubnet tooforward tutto il traffico da sedi tooAzure tramite appliance virtuale hello. Si tratta di un'aggiunta recente.
> 
> 

### <a name="bgp-routes"></a>Route BGP
Se si dispone di una connessione ExpressRoute tra la rete locale e Azure, è possibile abilitare le route toopropagate BGP dal tooAzure di rete locale. Vengono utilizzate queste route BGP in hello esattamente come le route di sistema e utente definito route in ogni subnet di Azure. Per altre informazioni, vedere [Panoramica tecnica relativa a ExpressRoute](../expressroute/expressroute-introduction.md).

> [!IMPORTANT]
> È possibile configurare la forza di toouse ambiente Azure tunneling forzato attraverso la rete locale tramite la creazione di una route definita dall'utente per 0.0.0.0/0 subnet che usa il gateway VPN hello come hop successivo hello. Tuttavia, funziona solo se si utilizza un gateway VPN, non ExpressRoute. Per ExpressRoute, il tunneling forzato viene configurato tramite BGP.
> 
> 

## <a name="ip-forwarding"></a>Inoltro IP
Come descritto in precedenza, uno dei hello motivi principali toocreate una route definita dall'utente è dell'appliance virtuale tooforward traffico tooa. Un dispositivo virtuale è semplicemente una macchina virtuale che esegue un'applicazione che consente il traffico di rete toohandle in qualche modo, ad esempio un firewall o un dispositivo NAT.

Questo dispositivo virtuale che VM deve essere in grado di tooreceive il traffico in ingresso che viene risolto non tooitself. tooallow un traffico tooreceive VM inoltrate tooother destinazioni, è necessario abilitare l'inoltro IP per hello macchina virtuale. Si tratta di un'impostazione, non è un'impostazione hello del sistema operativo guest di Azure.

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come troppo[creare route nel modello di distribuzione di gestione risorse di hello](virtual-network-create-udr-arm-template.md) e associarli toosubnets. 
* Informazioni su come troppo[creare route nel modello di distribuzione classica hello](virtual-network-create-udr-classic-ps.md) e associarli toosubnets.

