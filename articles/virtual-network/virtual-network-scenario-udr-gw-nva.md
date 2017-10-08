---
title: connessione aaaHybrid con applicazioni di livello 2 | Documenti Microsoft
description: "Informazioni su come toodeploy Appliance virtuali e UDR toocreate un ambiente a più livelli applicazione in Azure"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 1f509bec-bdd1-470d-8aa4-3cf2bb7f6134
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/05/2016
ms.author: jdial
ms.openlocfilehash: 53599862289dbf9c6ab3289b0cb8dda6430f20f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-appliance-scenario"></a>Scenario dell'appliance virtuale
Uno scenario comune tra i clienti di Azure più grandi è hello necessità tooprovide toohello un'applicazione a due livelli esposto Internet, consentendo allo stesso livello di back-toohello accesso da un data center locale. Questo documento verrà illustrati uno scenario utilizzando le route di definito dall'utente (UDR), un Gateway VPN e network Appliance virtuali toodeploy un ambiente a due livelli che soddisfi i seguenti requisiti hello:

* Applicazione Web deve essere accessibile da Internet pubblica solo hello.
* Applicazione hello hosting del server Web deve essere in grado di tooaccess un server applicazioni back-end.
* Tutto il traffico da applicazione web di Internet toohello hello deve passare attraverso un accessorio virtuale di firewall. Questa appliance virtuale verrà usata solo per il traffico Internet.
* Tutto il traffico verso i server applicazioni toohello deve passare attraverso un accessorio virtuale di firewall. Questo dispositivo virtuale verrà utilizzato per l'accesso provenienti da una rete locale hello tramite un Gateway VPN e server di accesso toohello back-end end.
* Gli amministratori devono essere in grado di toomanage hello firewall dispositivi di rete dal computer locale, utilizzando un terzo firewall appliance virtuale utilizzati esclusivamente per scopi di gestione.

Si tratta di uno scenario di rete perimetrale standard con una rete perimetrale e una rete protetta. Questo scenario può essere creato in Azure usando gruppi di sicurezza di rete, appliance virtuali firewall o una combinazione di entrambi. tabella Hello riportata di seguito vengono illustrate alcune hello vantaggi e svantaggi tra NSGs e Appliance virtuali firewall.

|  | Vantaggi | Svantaggi |
| --- | --- | --- |
| NSG |Nessun costo. <br/>Integrato nel controllo degli accessi in base al ruolo di Azure. <br/>Le regole possono essere create in modelli di Azure Resource Manager. |La complessità può variare in ambienti più grandi. |
| Firewall |Controllo completo del piano dati. <br/>Gestione centrale con console firewall. |Costo dell'appliance firewall. <br/>Non integrato nel controllo degli accessi in base al ruolo di Azure. |

soluzione Hello seguente Usa firewall Appliance virtuali tooimplement uno scenario di rete protetta/rete Perimetrale.

## <a name="considerations"></a>Considerazioni
È possibile distribuire l'ambiente hello illustrati in precedenza in Azure utilizzando diverse funzionalità disponibili oggi, come indicato di seguito.

* **Rete virtuale**. Una rete virtuale di Azure funziona nella rete di on-premise tooan modo simile e può essere suddiviso in uno o più subnet tooprovide traffico isolamento e la separazione dei compiti.
* **Appliance virtuale**. Alcuni partner forniscono Appliance virtuali in hello Azure Marketplace che può essere utilizzato per i firewall di tre hello descritti in precedenza. 
* **Route definite dall'utente**. Tabelle di routing possono contenere UDRs utilizzate da Azure flusso hello toocontrol rete dei pacchetti all'interno di una rete virtuale. Queste tabelle di routing possono essere applicato toosubnets. Una delle funzionalità più recenti di hello in Azure è possibilità di hello tooapply un toohello tabella route GatewaySubnet, fornendo hello possibilità tooforward tutto il traffico in rete virtuale di Azure hello proviene ibrida connessione tooa appliance virtuale.
* **Inoltro IP**. Per impostazione predefinita, hello Azure motore rete inoltrare pacchetti toovirtual schede di interfaccia rete (NIC) solo se corrisponde a indirizzo IP di destinazione dei pacchetti hello hello indirizzo IP NIC. Pertanto, se un UDR definisce che un pacchetto deve essere inviato tooa appliance virtuale di base, hello Azure motore rete scenderanno tale pacchetto. pacchetto di hello tooensure viene recapitato tooa macchina virtuale (in questo caso, un accessorio virtuale) che non è destinazione effettiva di hello per i pacchetti hello, è necessario tooenable l'inoltro IP per il dispositivo virtuale hello.
* **Gruppi di sicurezza di rete**. esempio Hello seguente non avvalersi della NSGs, ma è possibile utilizzare subnet toohello NSGs applicato e/o schede di rete in questa soluzione toofurther filtro hello il traffico da e verso le subnet e schede di rete.

![IPv6 connectivity](./media/virtual-network-scenario-udr-gw-nva/figure01.png)

In questo esempio è associata una sottoscrizione che contiene la seguente sintassi hello:

* 2 gruppi di risorse, non illustrati nel diagramma hello. 
  * **ONPREMRG**. Contiene tutte le risorse necessarie toosimulate una rete locale.
  * **AZURERG**. Contiene tutte le risorse necessarie per l'ambiente di rete virtuale di Azure hello. 
* Una rete virtuale denominata **onpremvnet** utilizzato toomimic segmentato di un data center locale come indicato di seguito.
  * **onpremsn1**. Subnet contenente una macchina virtuale (VM) in esecuzione Ubuntu toomimic un server locale.
  * **onpremsn2**. Subnet contenente una macchina virtuale in esecuzione Ubuntu toomimic un computer locale utilizzato da un amministratore.
* È un accessorio virtuale di firewall denominato **OPFW** su **onpremvnet** utilizzato toomaintain un tunnel troppo**azurevnet**.
* Una rete virtuale denominata **azurevnet** segmentata come indicato di seguito.
  * **azsn1**. Subnet firewall esterno utilizzata esclusivamente per i firewall esterno hello. Tutto il traffico Internet in ingresso passerà attraverso questa subnet. Questa subnet contiene solo un firewall esterno toohello NIC collegato.
  * **azsn2**. Subnet front-end che ospita una macchina virtuale in esecuzione come server web che verrà eseguito da hello Internet.
  * **azsn3**. Subnet di back-end che ospita una macchina virtuale in esecuzione un server applicazioni back-end che eseguiranno l'accesso a server web front-end di hello.
  * **azsn4**. Subnet di gestione utilizzato esclusivamente tooprovide Gestione accesso tooall firewall dispositivi virtuali. Questa subnet contiene solo una scheda di rete per ogni dispositivo virtuale firewall utilizzato nella soluzione hello.
  * **GatewaySubnet**. Subnet connessione ibrida di Azure necessarie per la connettività di tooprovide ExpressRoute e VPN Gateway tra reti virtuali di Azure e altre reti. 
* Sono disponibili 3 Appliance virtuale firewall in hello **azurevnet** rete. 
  * **AZF1**. Firewall esterno esposto toohello rete Internet pubblica utilizzando una risorsa di indirizzo IP pubblica in Azure. È necessario avere un modello da hello Marketplace o direttamente dal fornitore del dispositivo, che esegue il provisioning appliance virtuale 3-NIC tooensure.
  * **AZF2**. Firewall interno utilizzato traffico toocontrol tra **azsn2** e **azsn3**. Anche questa è un'appliance virtuale con 3 schede di interfaccia di rete.
  * **AZF3**. Gestione firewall di tooadministrators accessibile da hello locale datacenter e subnet di gestione connesso tooa utilizzato toomanage Appliance firewall tutti. È possibile richiedere uno direttamente dal fornitore del dispositivo o modelli sono disponibili 2 NIC appliance virtuale hello Marketplace.

## <a name="user-defined-routing-udr"></a>Routing definito dall'utente
Ogni subnet in Azure può essere collegato tooa UDR tabella utilizzata toodefine modalità di routing avviato in tale subnet di traffico. Se non è definito alcun UDRs, Azure Usa impostazione predefinita le route tooallow traffico tooflow da una subnet tooanother. toobetter comprendere UDRs, visitare [quali sono le route definite dall'utente e l'inoltro IP](virtual-networks-udr-overview.md#ip-forwarding).

comunicazione tooensure viene eseguita tramite appliance firewall destra hello, in base ai requisiti ultimo hello precedenti, è necessario toocreate hello segue la tabella di routing contenente UDRs in **azurevnet**.

### <a name="azgwudr"></a>azgwudr
In questo scenario, hello solo il traffico che passa da on-premise tooAzure saranno utilizzati toomanage hello firewall connettendosi troppo**AZF3**, e che il traffico deve passare attraverso firewall interno hello, **AZF2**. Pertanto, solo una route è necessaria in hello **GatewaySubnet** come illustrato di seguito.

| Destination | Hop successivo | Spiegazione |
| --- | --- | --- |
| 10.0.4.0/24 |10.0.3.11 |Consente di firewall di gestione locale traffico tooreach **AZF3** |

### <a name="azsn2udr"></a>azsn2udr
| Destination | Hop successivo | Spiegazione |
| --- | --- | --- |
| 10.0.3.0/24 |10.0.2.11 |Consente il traffico toohello back-end subnet che ospita il server applicazioni hello tramite **AZF2** |
| 0.0.0.0/0 |10.0.2.10 |Consente a tutti gli altri toobe traffico instradato tramite **AZF1** |

### <a name="azsn3udr"></a>azsn3udr
| Destination | Hop successivo | Spiegazione |
| --- | --- | --- |
| 10.0.2.0/24 |10.0.3.10 |Consente il traffico troppo**azsn2** tooflow dal server Web toohello di server app attraverso **AZF2** |

È inoltre necessario toocreate le tabelle di route per le subnet hello **onpremvnet** toomimic hello locale Data Center.

### <a name="onpremsn1udr"></a>onpremsn1udr
| Destination | Hop successivo | Spiegazione |
| --- | --- | --- |
| 192.168.2.0/24 |192.168.1.4 |Consente il traffico troppo**onpremsn2** tramite **OPFW** |

### <a name="onpremsn2udr"></a>onpremsn2udr
| Destination | Hop successivo | Spiegazione |
| --- | --- | --- |
| 10.0.3.0/24 |192.168.2.4 |Consente di subnet con traffico toohello eseguito in Azure tramite **OPFW** |
| 192.168.1.0/24 |192.168.2.4 |Consente il traffico troppo**onpremsn1** tramite **OPFW** |

## <a name="ip-forwarding"></a>Inoltro IP
UDR e l'inoltro IP sono funzionalità che è possibile utilizzare in combinazione tooallow Appliance virtuali toobe utilizzato toocontrol flusso del traffico in una rete virtuale di Azure.  Un dispositivo virtuale è semplicemente una macchina virtuale che esegue un'applicazione che consente il traffico di rete toohandle in qualche modo, ad esempio un firewall o un dispositivo NAT.

Questo dispositivo virtuale che VM deve essere in grado di tooreceive il traffico in ingresso che viene risolto non tooitself. tooallow un traffico tooreceive VM inoltrate tooother destinazioni, è necessario abilitare l'inoltro IP per hello macchina virtuale. Si tratta di un'impostazione, non è un'impostazione hello del sistema operativo guest di Azure. Il dispositivo virtuale ancora esigenze toorun tipo di applicazione toohandle hello il traffico in ingresso e distribuirla in modo appropriato.

toolearn ulteriori informazioni sull'inoltro IP, visitare [quali sono le route definite dall'utente e l'inoltro IP](virtual-networks-udr-overview.md#ip-forwarding).

Ad esempio, si supponga di che aver hello dopo l'installazione in una rete virtuale di Azure:

* La subnet **onpremsn1** contiene una macchina virtuale denominata **onpremvm1**.
* La subnet **onpremsn2** contiene una macchina virtuale denominata **onpremvm2**.
* Appliance virtuale denominato **OPFW** è connesso troppo**onpremsn1** e **onpremsn2**.
* Una route definita dall'utente collegato troppo**onpremsn1** specifica che tutto il traffico troppo**onpremsn2** devono essere inviati troppo**OPFW**.

In questo punto, se **onpremvm1** tenta di una connessione con tooestablish **onpremvm2**, hello UDR verrà utilizzato e il traffico verrà inviato troppo**OPFW** come hop successivo hello. Tenere presente che hello destinazione pacchetto effettivo non viene modificato, ancora visualizzato **onpremvm2** hello destinazione. 

Senza attivato per l'inoltro IP **OPFW**, hello la logica di rete virtuale Azure eliminerà i pacchetti hello, poiché consente solo i pacchetti inviati toobe tooa VM se hello indirizzo IP della macchina virtuale è la destinazione hello per i pacchetti hello.

Con inoltro IP, la logica di rete virtuale di Azure hello inoltrerà tooOPFW pacchetti hello, senza modificare l'indirizzo di destinazione originale. **OPFW** deve gestire i pacchetti hello e determinare quali toodo con essi.

Scenario di hello sopra toowork, è necessario abilitare l'inoltro IP nelle schede NIC hello per **OPFW**, **AZF1**, **AZF2**, e **AZF3** utilizzati per routing (tutte le NIC ad eccezione di quelli hello toohello collegato gestione subnet). 

## <a name="firewall-rules"></a>Regole del firewall
Come descritto in precedenza, solo l'inoltro IP garantisce Appliance virtuali toohello i pacchetti vengono inviati. Il dispositivo è ancora necessario toodecide quali toodo con tali pacchetti. Nel precedente scenario hello, sarà necessario hello toocreate alle regole nei dispositivi:

### <a name="opfw"></a>OPFW
OPFW rappresenta un dispositivo locale contenente hello seguenti regole:

* **Route**: tutto il traffico too10.0.0.0/16 (**azurevnet**) devono essere inviati tramite tunnel **ONPREMAZURE**.
* **Criteri**: consentire tutto il traffico bidirezionale tra **port2** e **ONPREMAZURE**.

### <a name="azf1"></a>AZF1
AZF1 rappresenta un'appliance virtuale Azure contenente hello seguenti regole:

* **Criteri**: consentire tutto il traffico bidirezionale tra **port1** e **port2**.

### <a name="azf2"></a>AZF2
AZF2 rappresenta un'appliance virtuale Azure contenente hello seguenti regole:

* **Route**: tutto il traffico too10.0.0.0/16 (**onpremvnet**) deve essere inviato l'indirizzo IP del gateway Azure toohello (ad esempio, 10.0.0.1) tramite **port1**.
* **Criteri**: consentire tutto il traffico bidirezionale tra **port1** e **port2**.

## <a name="network-security-groups-nsgs"></a>Gruppi di sicurezza di rete (NGS)
In questo scenario i gruppi di sicurezza di rete non vengono usati. Tuttavia, è possibile applicare NSGs tooeach subnet toorestrict traffico in entrata e in uscita. Ad esempio, è possibile applicare hello subnet FW esterna di NSG regole toohello seguente.

**In ingresso**

* Consenti tutto il traffico TCP da hello Internet tooport 80 su tutte le VM nella subnet hello.
* Nega tutto il traffico Internet hello.

**In uscita**

* Nega tutto il traffico toohello Internet.

## <a name="high-level-steps"></a>Passaggi di livello elevato
toodeploy questo scenario, seguire hello passaggi di alto livello seguenti.

1. Account di accesso tooyour sottoscrizione Azure.
2. Se si desidera toodeploy hello di toomimic una rete virtuale locale rete, il provisioning delle risorse di hello che fanno parte di **ONPREMRG**.
3. Il provisioning di risorse hello che fanno parte di **AZURERG**.
4. Tunnel hello effettuare il provisioning da **onpremvnet** troppo**azurevnet**.
5. Una volta che vengono effettuato il provisioning di tutte le risorse, effettuare l'accesso troppo**onpremvm2** e ping 10.0.3.101 tootest connettività tra **onpremsn2** e **azsn3**.

