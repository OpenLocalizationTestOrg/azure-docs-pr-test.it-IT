---
title: gruppi di sicurezza aaaNetwork in Azure | Documenti Microsoft
description: Informazioni su come flusso di traffico tooisolate e il controllo all'interno di reti virtuali tramite firewall hello distribuito in Azure utilizzando i gruppi di sicurezza di rete.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 20e850fc-6456-4b5f-9a3f-a8379b052bc9
ms.service: virtual-network
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/11/2016
ms.author: jdial
ms.openlocfilehash: 3528ce833dab17977327c3c9ae0e78316e5e6a05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="filter-network-traffic-with-network-security-groups"></a>Filtrare il traffico di rete con gruppi di sicurezza di rete

Un rete gruppo di sicurezza () contiene un elenco di regole di sicurezza che consentono o negano tooresources il traffico di rete connessa tooAzure reti virtuali (VNet). NSGs può essere associato toosubnets, singole macchine virtuali (classico), o interfacce di rete (NIC) collegati tooVMs Gestione risorse (). Quando un gruppo è subnet tooa associato, hello regole tooall risorse toohello connesso subnet. Il traffico può essere limitato ulteriormente associando anche un gruppo tooa macchina virtuale o scheda di rete.

> [!NOTE]
> Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo di entrambi i modelli, ma Microsoft consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.

## <a name="nsg-resource"></a>Risorsa del gruppo di sicurezza di rete
NSGs contenere hello le proprietà seguenti:

| Proprietà | Descrizione | Vincoli | Considerazioni |
| --- | --- | --- | --- |
| Nome |Nome per hello NSG |Deve essere univoco all'interno di area hello.<br/>Può contenere lettere, numeri, caratteri di sottolineatura, punti e trattini.<br/>Deve iniziare con una lettera o un numero.<br/>Deve terminare con una lettera, un numero o un carattere di sottolineatura.<br/>Non può superare gli 80 caratteri. |Poiché potrebbe essere necessario toocreate NSGs diversi, assicurarsi di avere una convenzione di denominazione che rende facile tooidentify funzione hello il NSGs. |
| Region |Azure [area](https://azure.microsoft.com/regions) in hello gruppo è stato creato. |NSGs può essere solo tooresources associato all'interno di hello hello NSG stessa area. |toolearn su quanti NSGs per area, è possibile avere letto hello [Azure limita](../azure-subscription-service-limits.md#virtual-networking-limits-classic) articolo.|
| Gruppo di risorse |Hello [gruppo di risorse](../azure-resource-manager/resource-group-overview.md#resource-groups) hello nel gruppo. |Anche se è presente un gruppo in un gruppo di risorse, può essere associato tooresources in qualsiasi gruppo di risorse come risorsa hello fa parte di hello stessa area Azure hello gruppo. |Gruppi di risorse è toomanage utilizzati insieme, come un'unità di distribuzione di più risorse.<br/>È possibile considerare il raggruppamento hello NSG con risorse di cui che è associata. |
| Regole |Regole in ingresso e in uscita che definiscono il traffico consentito o rifiutato. | |Vedere hello [regole NSG](#Nsg-rules) sezione di questo articolo. |

> [!NOTE]
> ACL basati su endpoint e sicurezza di rete gruppi non sono supportati in hello stessa istanza di macchina virtuale. Se si desidera toouse un gruppo e si dispone già di un endpoint ACL sul posto, è necessario rimuovere prima endpoint hello ACL. modalità di lettura di un ACL, tooremove toolearn hello [Gestione controllo elenchi accesso (ACL) per gli endpoint tramite PowerShell](virtual-networks-acl-powershell.md) articolo.
> 

### <a name="nsg-rules"></a>Regole NSG
Regole di NSG contengono hello le proprietà seguenti:

| Proprietà | Descrizione | Vincoli | Considerazioni |
| --- | --- | --- | --- |
| **Nome** |Nome regola hello. |Deve essere univoco all'interno di area hello.<br/>Può contenere lettere, numeri, caratteri di sottolineatura, punti e trattini.<br/>Deve iniziare con una lettera o un numero.<br/>Deve terminare con una lettera, un numero o un carattere di sottolineatura.<br/>Non può superare gli 80 caratteri. |Si potrebbe dispone di diverse regole all'interno di un gruppo, quindi assicurarsi che seguire una convenzione di denominazione che consente di funzione hello tooidentify della regola. |
| **Protocollo** |Protocollo toomatch per regola hello. |TCP, UDP o * |Utilizzare * come un protocollo include ICMP (solo traffico est-ovest), come come TCP e UDP e può ridurre il numero di hello regole, è necessario.<br/>AT hello stesso tempo, utilizzando * potrebbe essere troppo ampia un approccio, pertanto è consigliabile utilizzare * solo quando necessario. |
| **Intervallo porte di origine** |Origine toomatch intervallo di porte per la regola di hello. |Numero di porta da 1 too65535, intervallo di porte singolo (esempio: 1-65535), o * (per tutte le porte). |Le porte di origine potrebbero essere temporanee. A meno che il programma client non usi una porta specifica, usare * nella maggior parte dei casi.<br/>Provare gli intervalli di porte toouse come possibili tooavoid hello necessario per più regole.<br/>Non è possibile raggruppare più porte o intervalli di porte con una virgola. |
| **Intervallo di porte di destinazione** |Destinazione toomatch intervallo di porte per la regola di hello. |Numero di porta da 1 too65535, intervallo di porte singolo (esempio: 1-65535), o \* (per tutte le porte). |Provare gli intervalli di porte toouse come possibili tooavoid hello necessario per più regole.<br/>Non è possibile raggruppare più porte o intervalli di porte con una virgola. |
| **Prefisso dell'indirizzo di origine** |Origine indirizzo prefisso o un tag toomatch per regola hello. |Singolo indirizzo IP (ad esempio, 10.10.10.10), subnet IP (ad esempio, 192.168.1.0/24), [tag predefinito](#default-tags) o * (per tutti gli indirizzi). |Considerare l'utilizzo di intervalli, i tag predefiniti, e * numero hello tooreduce di regole. |
| **Prefisso dell’indirizzo di destinazione** |Destinazione indirizzo prefisso o un tag toomatch per regola hello. | Singolo indirizzo IP (ad esempio, 10.10.10.10), subnet IP (ad esempio, 192.168.1.0/24), [tag predefinito](#default-tags) o * (per tutti gli indirizzi). |Considerare l'utilizzo di intervalli, i tag predefiniti, e * numero hello tooreduce di regole. |
| **Direzione** |Direzione del traffico toomatch per regola hello. |In ingresso o in uscita. |Le regole in ingresso e in uscita vengono elaborate separatamente, in base alla direzione. |
| **Priorità** |Le regole vengono controllate in ordine di hello di priorità. Dopo che è stata applicata una regola, non viene verificata la corrispondenza di altre regole. | Numero compreso tra 100 e 4096. | È consigliabile creare regole del passaggio di priorità per 100 per ogni spazio tooleave regola per le nuove regole che è possibile creare in hello future. |
| **Accedere** |Tipo di accesso tooapply se hello regola corrispondente. | Consentire o rifiutare. | Tenere presente che se non è presente una regola di autorizzazione per un pacchetto, hello verrà ignorato. |

I gruppi di sicurezza di rete contengono due set di regole: le regola in ingresso e quelle in uscita. priorità di Hello per una regola deve essere univoca all'interno di ogni set. 

![Elaborazione delle regole dei gruppi di sicurezza di rete](./media/virtual-network-nsg-overview/figure3.png) 

immagine precedente Hello viene illustrata la modalità di elaborazione delle regole di gruppo.

### <a name="default-tags"></a>Tag predefiniti
I tag predefiniti sono identificatori forniti dal sistema tooaddress una categoria di indirizzi IP. È possibile utilizzare i tag predefiniti in hello **il prefisso di indirizzo di origine** e **prefisso di indirizzo di destinazione** proprietà di qualsiasi regola. Esistono tre tag predefiniti utilizzabili.

* **VirtualNetwork** Gestione risorse () (**VIRTUAL_NETWORK** per classica): questo tag include spazio degli indirizzi di rete virtuale hello (intervalli CIDR definiti in Azure), tutti gli spazi degli indirizzi locale connesso e connesso Azure le reti virtuali (reti locali).
* **AzureLoadBalancer** (Resource Manager) o **AZURE_LOADBALANCER** (distribuzione classica): questo tag identifica il servizio di bilanciamento del carico dell'infrastruttura di Azure. tag Hello traduce tooan derivano IP dei Data Center di Azure in cui di probe di integrità di Azure.
* **Internet** Gestione risorse () (**INTERNET** per classica): questo tag indica spazio di indirizzi IP hello che è di fuori di rete virtuale hello e raggiungibili dalla rete Internet pubblica. intervallo di Hello include hello [spazio IP pubblico di Azure proprietà](https://www.microsoft.com/download/details.aspx?id=41653).

### <a name="default-rules"></a>Regole predefinite
Tutti i gruppi di sicurezza di rete contengono un set di regole predefinite. le regole predefinite di Hello non possono essere eliminate, ma poiché vengono assegnati priorità più bassa hello, possono essere sostituite dalle regole di hello creati. 

le regole predefinite di Hello consentono e non consentire il traffico come indicato di seguito:
- **Rete virtuale:** il traffico che ha origine e termina in una rete virtuale è consentito sia in ingresso che in uscita.
- **Internet:** il traffico in uscita è consentito, mentre il traffico in ingresso viene bloccato.
- **Bilanciamento del carico:** integrità hello tooprobe di Azure consente carico bilanciamento del carico delle macchine virtuali e istanze del ruolo. Se non si usa un set con bilanciamento del carico, è possibile eseguire l'override di questa regola.

**Regole predefinite In ingresso**

| Nome | Priorità | IP di origine | Porta di origine | IP di destinazione | Porta di destinazione | Protocollo | Accesso |
| --- | --- | --- | --- | --- | --- | --- | --- |
| AllowVNetInBound |65000 | VirtualNetwork | * | VirtualNetwork | * | * | CONSENTI |
| AllowAzureLoadBalancerInBound | 65001 | AzureLoadBalancer | * | * | * | * | CONSENTI |
| DenyAllInBound |65500 | * | * | * | * | * | NEGA |

**Regole predefinite In uscita**

| Nome | Priorità | IP di origine | Porta di origine | IP di destinazione | Porta di destinazione | Protocollo | Accesso |
| --- | --- | --- | --- | --- | --- | --- | --- |
| AllowVnetOutBound | 65000 | VirtualNetwork | * | VirtualNetwork | * | * | CONSENTI |
| AllowInternetOutBound | 65001 | * | * | Internet | * | * | CONSENTI |
| DenyAllOutBound | 65500 | * | * | * | * | * | NEGA |

## <a name="associating-nsgs"></a>Associazione di gruppi di sicurezza di rete
È possibile associare un tooVMs gruppo schede di rete e subnet, a seconda del modello di distribuzione hello in uso, come indicato di seguito:

* **Macchina virtuale (solo versione classica):** vengono applicate le regole di sicurezza tooall traffico da e verso hello macchina virtuale. 
* **Scheda di rete (solo per Gestione risorse):** vengono applicate le regole di sicurezza tooall traffico da e verso hello NIC hello NSG è associato. In una macchina virtuale multi-NIC, è possibile applicare diversi (o hello stesso) tooeach gruppo NIC singolarmente. 
* **Subnet (Gestione risorse e classica):** vengono applicate le regole di sicurezza tooany traffico da e verso le risorse connesso toohello rete virtuale.

È possibile associare diversi NSGs tooa VM (o una scheda di rete, a seconda del modello di distribuzione hello) e hello subnet connessa a una scheda di rete o di una macchina virtuale. Le regole di sicurezza applicato toohello traffico, in base alla priorità, in ogni gruppo, in hello segue ordine:

- **Traffico in ingresso**

  1. **GRUPPO applicato toosubnet:** se una subnet gruppo ha un traffico toodeny regole di corrispondenza, hello verrà ignorato.

  2. **GRUPPO applicato tooNIC** Gestione risorse () o alla macchina virtuale (classico): NSG VM\NIC se dispone di una regola di corrispondenza che impedisca il traffico, i pacchetti vengono eliminati in hello VM\NIC, anche se una subnet gruppo dispone di una regola di corrispondenza che consenta il traffico.

- **Traffico in uscita**

  1. **GRUPPO applicato tooNIC** Gestione risorse () o alla macchina virtuale (classico): se un gruppo VM\NIC dispone di una regola di corrispondenza che impedisca il traffico, i pacchetti vengono eliminati.

  2. **GRUPPO applicato toosubnet:** se una subnet gruppo dispone di una regola di corrispondenza che impedisca il traffico, vengono ignorati pacchetti, anche se un gruppo VM\NIC dispone di una regola di corrispondenza che consenta il traffico.

> [!NOTE]
> Anche se è possibile associare solo un singolo gruppo tooa subnet VM o NIC; è possibile associare hello molte risorse stesso tooas gruppo desiderato.
>

## <a name="implementation"></a>Implementazione
È possibile implementare NSGs hello Gestione risorse o i modelli di distribuzione classica utilizzando hello seguenti strumenti:

| Documentazione di distribuzione | Classico | Gestione risorse |
| --- | --- | --- |
| Portale di Azure   | Sì | [Sì](virtual-networks-create-nsg-arm-pportal.md) |
| PowerShell     | [Sì](virtual-networks-create-nsg-classic-ps.md) | [Sì](virtual-networks-create-nsg-arm-ps.md) |
| Interfaccia della riga di comando di Azure **versione 1**   | [Sì](virtual-networks-create-nsg-classic-cli.md) | [Sì](virtual-networks-create-nsg-cli-nodejs.md) |
| Interfaccia della riga di comando di Azure **versione 2**   | No | [Sì](virtual-networks-create-nsg-arm-cli.md) |
| Modello di Azure Resource Manager   | No  | [Sì](virtual-networks-create-nsg-arm-template.md) |

## <a name="planning"></a>Pianificazione
Prima di implementare NSGs, è necessario hello tooanswer seguenti domande:

1. I tipi di risorse si vogliono toofilter traffico tooor da? È possibile connettere risorse come interfacce di rete (Resource Manager), VM (distribuzione classica), servizi cloud, ambienti del servizio dell'applicazione e set di scalabilità di macchine virtuali. 
2. Sono risorse hello è toofilter traffico da e verso toosubnets connesso in reti virtuali esistenti?

Per ulteriori informazioni sulla pianificazione per la sicurezza di rete in Azure, leggere hello [servizi Cloud e di sicurezza di rete](../best-practices-network-security.md) articolo. 

## <a name="design-considerations"></a>Considerazioni sulla progettazione
Dopo avere stabilito le risposte hello domande toohello hello [pianificazione](#Planning) sezione, esaminare le sezioni seguenti prima di definire il NSGs hello:

### <a name="limits"></a>Limiti
Vi sono limiti numero toohello NSGs è consentito in una sottoscrizione e numero di regole per ogni gruppo. informazioni sui limiti di hello, leggere hello toolearn [Azure limita](../azure-subscription-service-limits.md#networking-limits) articolo.

### <a name="vnet-and-subnet-design"></a>Progettazione di reti virtuali e subnet
Poiché NSGs possono essere applicati toosubnets, è possibile ridurre il numero di hello di NSGs raggruppamento delle risorse in base alla subnet e applicando NSGs toosubnets.  Se si decide di tooapply NSGs toosubnets, è possibile che le reti virtuali esistenti e si dispone di subnet non definite con NSGs presente. È possibile necessario toodefine toosupport di reti virtuali e le subnet di nuovo la struttura di gruppo e distribuire le nuove subnet nuova tooyour di risorse. È quindi possibile definire un toomove strategia di migrazione nuove subnet di risorse toohello esistente. 

### <a name="special-rules"></a>Regole speciali
Se si blocca il traffico consentito in base alle regole di hello, l'infrastruttura non può comunicare con servizi di Azure essenziali:

* **Indirizzo IP virtuale del nodo host hello:** servizi di infrastruttura di base come DHCP, DNS e il monitoraggio dello stato vengono forniti tramite host virtualizzato hello 168.63.129.16 l'indirizzo IP. Questo indirizzo IP pubblico appartiene tooMicrosoft ed è hello unico indirizzo IP virtualizzato usato in tutte le aree a questo scopo. Questo indirizzo IP viene eseguito il mapping toohello indirizzo IP fisico del computer server hello (nodo host) hosting hello macchina virtuale. nodo host Hello funge da origine probe hello per hello inoltro DHCP hello e resolver ricorsivo DNS di hello carico probe di integrità del servizio di bilanciamento e probe di integrità macchina hello. Indirizzo IP toothis di comunicazione non è un attacco.
* **Licenze (Servizio di gestione delle chiavi)**: le immagini Windows in esecuzione nelle VM devono essere concesse in licenza. tooensure licenze, una richiesta viene inviata server host di servizio di gestione delle chiavi toohello che gestiscono tali query. Hello richiesta in uscita attraverso la porta 1688.

### <a name="icmp-traffic"></a>Traffico ICMP
le regole di gruppo correnti Hello consentono solo i protocolli *TCP* o *UDP*. Non esiste un tag specifico per *ICMP*. Tuttavia, il traffico ICMP è consentito all'interno di una rete virtuale dalla regola predefinita di hello AllowVNetInBound, che consente di tooand il traffico da qualsiasi porta e protocollo all'interno di hello rete virtuale.

### <a name="subnets"></a>Subnet
* Si consideri hello numero di livelli che richiede il carico di lavoro. Tramite una subnet, con una subnet toohello di gruppo applicato, è possibile isolare ogni livello. 
* Se è necessario tooimplement una subnet per un gateway VPN o un circuito ExpressRoute, **non** si applicano a una subnet toothat di gruppo. In caso contrario, la connettività cross-premise o tra reti virtuali potrebbe non funzionare. 
* Se è necessario tooimplement un accessorio virtuale di rete (NVA), connettersi proprie subnet di hello NVA tooits e il nome di route definite dall'utente (UDR) tooand hello NVA. È possibile implementare un livello di subnet del traffico toofilter NSG da e verso questa subnet. ulteriori informazioni sulla UDRs, leggere hello toolearn [le route definite dall'utente](virtual-networks-udr-overview.md) articolo.

### <a name="load-balancers"></a>Servizi di bilanciamento del carico
* Considerare l'indirizzo di rete e di bilanciamento del carico hello regole translation (NAT) per ogni servizio di bilanciamento del carico utilizzato da tutti i carichi di lavoro. Le regole NAT sono pool back-end tooa associato che contiene le schede NIC di gestione risorse () o le istanze del ruolo di servizi Cloud di macchine virtuali / (classico). È consigliabile creare un gruppo per ogni pool back-end, consentendo solo il traffico mappato in base alle regole hello implementati in servizi di bilanciamento del carico hello. Creazione di un gruppo per ogni pool back-end garantisce che il traffico in arrivo pool back-end toohello direttamente (anziché tramite bilanciamento del carico hello), viene inoltre filtrato.
* Nelle distribuzioni classiche è creare endpoint che eseguono il mapping delle porte in un tooports bilanciamento di carico in cui le macchine virtuali o le istanze del ruolo. È anche possibile creare un proprio servizio di bilanciamento del carico pubblico tramite Resource Manager. porta di destinazione Hello per il traffico in ingresso è della porta effettivamente hello in hello macchina virtuale o istanza del ruolo, non la porta hello esposta da un servizio di bilanciamento del carico. porta di origine Hello e l'indirizzo per hello connessione toohello su che macchina virtuale è una porta e indirizzo hello computer remoto in hello Internet, non la porta hello e indirizzo esposto dal servizio di bilanciamento del carico hello.
* Quando si crea il traffico toofilter NSGs in arrivo tramite un servizio di bilanciamento del carico interno (ILB), hello porta e indirizzo intervallo di origine applicato provengono da hello computer, non hello bilanciamento del carico di origine. intervallo di porte e indirizzi di destinazione Hello sono quelle del computer di destinazione hello, non hello bilanciamento del carico.

### <a name="other"></a>Altre
* Gli elenchi di controllo di accesso basati su endpoint (ACL) e NSGs non sono supportate in hello stessa istanza di macchina virtuale. Se si desidera toouse un gruppo e si dispone già di un endpoint ACL sul posto, è necessario rimuovere prima endpoint hello ACL. Per informazioni su come tooremove un endpoint ACL, vedere hello [gestire gli ACL endpoint](virtual-networks-acl-powershell.md) articolo.
* In Gestione risorse, è possibile utilizzare un tooa associata gruppo NIC per le macchine virtuali con più schede di rete tooenable management (accesso remoto) in una base per ogni scheda di rete. Associazione univoco NSGs tooeach NIC consente la separazione dei tipi di traffico tra schede di rete.
* Utilizzare toohello simile di bilanciamento del carico, per filtrare il traffico proveniente da altre reti virtuali, è necessario utilizzare l'intervallo di indirizzi di origine di hello del computer remoto hello, non i gateway hello connessione hello reti virtuali.
* Molti servizi di Azure non possono essere connesso tooVNets. Se una risorsa di Azure non è connesso tooa rete virtuale, è possibile utilizzare una risorsa di toohello NSG toofilter il traffico.  Leggere la documentazione di hello per i servizi di hello utilizzare toodetermine se il servizio di hello può essere connesso tooa rete virtuale.

## <a name="sample-deployment"></a>Distribuzione di esempio
un'applicazione hello tooillustrate delle informazioni di hello in questo articolo, si consideri uno scenario comune di un'applicazione di due livello mostrato nella seguente immagine hello:

![Gruppi di sicurezza di rete](./media/virtual-network-nsg-overview/figure1.png)

Come illustrato nel diagramma hello, hello *Web1* e *Web2* le macchine virtuali sono connessa toohello *front-end* subnet e hello *DB1* e *DB2* le macchine virtuali sono connessa toohello *back-end* subnet.  Entrambe le subnet fanno parte di hello *TestVNet* rete virtuale. Hello componenti dell'applicazione ogni eseguito all'interno di una rete virtuale di tooa macchina virtuale di Azure connessa. scenario di Hello è hello seguenti requisiti:

1. Separazione del traffico tra hello WEB e server di database.
2. Inoltro del traffico regole dai server web sulla porta 80 hello carico bilanciamento tooall di bilanciamento del carico.
3. Caricare il servizio di bilanciamento NAT regole inoltrare il traffico proveniente nel bilanciamento del carico hello in tooport 50001 porta 3389 nel hello WEB1 VM.
4. Nessun toohello accesso front-end o back-end macchine virtuali da hello Internet, ad eccezione di requisiti, 2 e 3.
5. Nessun accesso a Internet in uscita dal server WEB o di database di hello.
6. Tooport 3389 dei server web è consentito l'accesso dalla subnet front-end hello.
7. Tooport 3389 di qualsiasi server di database è consentito l'accesso dalla subnet front-end hello.
8. Tooport 1433 di tutti i server di database è consentito l'accesso dalla subnet front-end hello.
9. Separazione del traffico di gestione (porta 3389) e del traffico di database (1433) su interfacce di rete diverse nei server DB.

Requisiti di 1 a 6 (eccetto i requisiti di 3 e 4) sono tutti gli spazi toosubnet ristretto. Hello NSGs seguenti requisiti hello precedente, riducendo al minimo il numero di hello di NSGs necessarie:

### <a name="frontend"></a>FrontEnd
**Regole in ingresso**

| Regola | Accesso | Priorità | Intervallo di indirizzi di origine | Porta di origine | Intervallo di indirizzi di destinazione | Porta di destinazione | Protocollo |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Allow-Inbound-HTTP-Internet | CONSENTI | 100 | Internet | * | * | 80 | TCP |
| Allow-Inbound-RDP-Internet | CONSENTI | 200 | Internet | * | * | 3389 | TCP |
| Deny-Inbound-All | NEGA | 300 | Internet | * | * | * | TCP |

**Regole in uscita**

| Regola | Accesso | Priorità | Intervallo di indirizzi di origine | Porta di origine | Intervallo di indirizzi di destinazione | Porta di destinazione | Protocollo |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Deny-Internet-All |NEGA |100 | * | * | Internet | * | * |

### <a name="backend"></a>BackEnd
**Regole in ingresso**

| Regola | Accesso | Priorità | Intervallo di indirizzi di origine | Porta di origine | Intervallo di indirizzi di destinazione | Porta di destinazione | Protocollo |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Deny-Internet-All | NEGA | 100 | Internet | * | * | * | * |

**Regole in uscita**

| Regola | Accesso | Priorità | Intervallo di indirizzi di origine | Porta di origine | Intervallo di indirizzi di destinazione | Porta di destinazione | Protocollo |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Deny-Internet-All | NEGA | 100 | * | * | Internet | * | * |

Hello NSGs seguente vengono create e associate tooNICs in hello macchine virtuali seguenti:

### <a name="web1"></a>WEB1
**Regole in ingresso**

| Regola | Accesso | Priorità | Intervallo di indirizzi di origine | Porta di origine | Intervallo di indirizzi di destinazione | Porta di destinazione | Protocollo |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Allow-Inbound-RDP-Internet | CONSENTI | 100 | Internet | * | * | 3389 | TCP |
| Allow-Inbound-HTTP-Internet | CONSENTI | 200 | Internet | * | * | 80 | TCP |

> [!NOTE]
> intervallo di indirizzi di origine di Hello per le regole precedenti hello **Internet**, hello non l'indirizzo IP virtuale del servizio di bilanciamento del carico hello. porta di origine Hello è *, non 500001. Le regole NAT per servizi di bilanciamento del carico non sono hello come regole di sicurezza di gruppo. Le regole di sicurezza di gruppo sono sempre correlati toohello origine e destinazione finale di traffico, **non** bilanciamento del carico hello tra due hello. 
> 
> 

### <a name="web2"></a>WEB2
**Regole in ingresso**

| Regola | Accesso | Priorità | Intervallo di indirizzi di origine | Porta di origine | Intervallo di indirizzi di destinazione | Porta di destinazione | Protocollo |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Deny-Inbound-RDP-Internet | NEGA | 100 | Internet | * | * | 3389 | TCP |
| Allow-Inbound-HTTP-Internet | CONSENTI | 200 | Internet | * | * | 80 | TCP |

### <a name="db-servers-management-nic"></a>Server DB (interfaccia di rete per gestione)
**Regole in ingresso**

| Regola | Accesso | Priorità | Intervallo di indirizzi di origine | Porta di origine | Intervallo di indirizzi di destinazione | Porta di destinazione | Protocollo |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Allow-Inbound-RDP-Front-end | CONSENTI | 100 | 192.168.1.0/24 | * | * | 3389 | TCP |

### <a name="db-servers-database-traffic-nic"></a>Server DB (interfaccia di rete per traffico di database)
**Regole in ingresso**

| Regola | Accesso | Priorità | Intervallo di indirizzi di origine | Porta di origine | Intervallo di indirizzi di destinazione | Porta di destinazione | Protocollo |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Allow-Inbound-SQL-Front-end | CONSENTI | 100 | 192.168.1.0/24 | * | * | 1433 | TCP |

Poiché alcune delle NSGs hello sono associati tooindividual schede di rete, le regole di hello sono per le risorse distribuite tramite Gestione risorse. La combinazione delle regole per la subnet e l'interfaccia di rete dipende dal modo in cui sono associate. 

## <a name="next-steps"></a>Passaggi successivi
* [Distribuire gruppi di sicurezza di rete (Resource Manager)](virtual-networks-create-nsg-arm-pportal.md).
* [Distribuire gruppi di sicurezza di rete (distribuzione classica)](virtual-networks-create-nsg-classic-ps.md).
* [Gestire i log dei gruppi di sicurezza di rete](virtual-network-nsg-manage-log.md).
* [Risolvere i problemi relativi ai gruppi di sicurezza di rete] (virtual-network-nsg-troubleshoot-portal.md)
