---
title: Rete virtuale (VNet) aaaAzure piano e Guida alla progettazione | Documenti Microsoft
description: "Informazioni su come tooplan e progettare le reti virtuali in Azure in base ai requisiti di isolamento, la connettività e posizione."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 3a4a9aea-7608-4d2e-bb3c-40de2e537200
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/08/2016
ms.author: jdial
ms.openlocfilehash: f3ffadf8cf254f64b1f86b44f90315d2bc679f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="plan-and-design-azure-virtual-networks"></a>Pianificare e progettare reti virtuali di Azure
Tooexperiment una rete virtuale con la creazione è abbastanza semplice, ma è possibile che si distribuire più reti virtuali su tempo toosupport hello esigenze della propria organizzazione. Con una pianificazione e progettazione, si verrà toodeploy in grado di reti virtuali e connettere le risorse di hello che è necessario in modo più efficace. Se non si ha familiarità con le reti virtuali, è consigliabile si [informazioni sulle reti virtuali](virtual-networks-overview.md) e [come toodeploy](virtual-networks-create-vnet-arm-pportal.md) uno prima di procedere.

## <a name="plan"></a>Pianificazione
Per ottenere buoni risultati, è fondamentale una conoscenza approfondita delle sottoscrizioni, delle aree e delle risorse di rete di Azure. È possibile utilizzare l'elenco di hello considerazioni seguito come un punto di partenza. Dopo aver appreso tali considerazioni, è possibile definire requisiti hello per la progettazione della rete.

### <a name="considerations"></a>Considerazioni
Prima di rispondere alle seguenti domande di pianificazione hello, prendere in considerazione i seguenti hello:

* Tutti gli oggetti creati in Azure sono composti da una o più risorse. Una macchina virtuale (VM) è una risorsa hello scheda di rete (NIC) utilizzata da una macchina virtuale è una risorsa, indirizzo IP pubblico hello utilizzato da una scheda di rete è una risorsa, hello di rete virtuale hello NIC connessa toois una risorsa.
* Le risorse vengono create all'interno di un' [area](https://azure.microsoft.com/regions/#services) e una sottoscrizione di Azure. Risorse possono essere solo tooa connesso rete virtuale presente in hello stessa risorsa di hello regione e sottoscrizione.
* È possibile connettersi tooeach altre reti virtuali utilizzando:
    * **[Rete virtuale peering](virtual-network-peering-overview.md)**: le reti virtuali hello devono esistere in hello stessa regione di Azure. Larghezza di banda tra risorse nel peering reti virtuali è hello stesso come se le risorse di hello erano connesso toohello stessa rete virtuale.
    * **Un Azure [Gateway VPN](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)**: le reti virtuali hello possono esistere in hello stesso, o diverse aree di Azure. Larghezza di banda tra le risorse in reti virtuali connesse tramite un Gateway VPN è limitata dalla larghezza di banda hello di hello Gateway VPN.
* È possibile connettersi rete locale di reti virtuali tooyour utilizzando uno dei hello [opzioni di connettività](../vpn-gateway/vpn-gateway-about-vpngateways.md#s2smulti) disponibili in Azure.
* Risorse diverse possono essere raggruppate in [gruppi di risorse](../azure-resource-manager/resource-group-overview.md#resource-groups), rendendo più semplice risorse di hello toomanage come unità. Un gruppo di risorse può contenere risorse da più aree, come risorse di hello appartenere toohello stessa sottoscrizione.

### <a name="define-requirements"></a>Definire i requisiti
Usare domande hello seguito come un punto di partenza per la progettazione della rete di Azure.    

1. Le posizioni di Azure saranno necessario utilizzare toohost reti virtuali?
2. È necessario tooprovide comunicazione tra questi percorsi di Azure?
3. È necessario tooprovide comunicazione tra il VNet(s) di Azure e il data center locale?
4. Quante VM IaaS (Infrastructure as a Service), ruoli dei servizi cloud e app Web sono necessari per la soluzione?
5. È necessario tooisolate il traffico in base ai gruppi di macchine virtuali (i server web, ovvero front-end e server di database back-end)?
6. È necessario che il flusso del traffico toocontrol utilizzando Appliance virtuali?
7. Fare gli utenti necessità diversi set di autorizzazioni toodifferent risorse di Azure?

### <a name="understand-vnet-and-subnet-properties"></a>Comprendere le proprietà della rete virtuale e della subnet
Le risorse della rete virtuale e della subnet consentono di definire un limite di sicurezza per i carichi di lavoro in esecuzione in Azure. Una rete virtuale è caratterizzata da una raccolta di spazi di indirizzi, definiti come blocchi CIDR.

> [!NOTE]
> Gli amministratori di rete hanno familiarità con la notazione CIDR. Se non si ha familiarità con CIDR, è possibile [ottenere maggiori informazioni](http://whatismyipaddress.com/cidr).
>
>

Le reti virtuali contengono hello le proprietà seguenti.

| Proprietà | Descrizione | Vincoli |
| --- | --- | --- |
| **nome** |Nome della rete virtuale |Stringa di caratteri too80. Può contenere lettere, numeri, caratteri di sottolineatura, punti o trattini. Deve iniziare con una lettera o un numero. Deve terminare con una lettera, un numero o un carattere di sottolineatura. Può contenere lettere maiuscole o minuscole. |
| **location** |Località di Azure (anche tooas cui regione). |Deve essere uno dei hello posizioni di Azure validi. |
| **addressSpace** |Raccolta di prefissi di indirizzo che costituiscono hello rete virtuale nella notazione CIDR. |Deve essere una matrice di blocchi di indirizzi CIDR validi, inclusi intervalli di indirizzi IP pubblici. |
| **subnet** |Raccolta di subnet che costituiscono hello rete virtuale |vedere la tabella di proprietà subnet hello seguente. |
| **dhcpOptions** |Oggetto che contiene un'unica proprietà obbligatoria denominata **dnsServers**. | |
| **dnsServers** |Matrice di server DNS utilizzati dal hello rete virtuale. Se non si specifica alcun server, viene usata la risoluzione dei nomi interna di Azure. |Deve essere una matrice di backup dei server DNS too10, utilizzando un indirizzo IP. |

Una subnet è una risorsa figlio di una rete virtuale e consente di definire i segmenti degli spazi di indirizzi all'interno di un blocco CIDR, usando i prefissi degli indirizzi IP. Schede di rete possono essere aggiunte toosubnets e tooVMs connesso, fornisce la connettività per diversi carichi di lavoro.

Subnet contengono hello le proprietà seguenti.

| Proprietà | Descrizione | Vincoli |
| --- | --- | --- |
| **nome** |Nome della subnet |Stringa di caratteri too80. Può contenere lettere, numeri, caratteri di sottolineatura, punti o trattini. Deve iniziare con una lettera o un numero. Deve terminare con una lettera, un numero o un carattere di sottolineatura. Può contenere lettere maiuscole o minuscole. |
| **location** |Località di Azure (anche tooas cui regione). |Deve essere uno dei hello posizioni di Azure validi. |
| **addressPrefix** |Singolo prefisso di indirizzo di subnet hello in notazione CIDR |Deve essere un singolo blocco CIDR che fa parte di uno degli spazi di indirizzi della rete virtuale di hello. |
| **networkSecurityGroup** |Subnet toohello NSG applicato | |
| **routeTable** |Tabella di route applicato toohello subnet | |
| **ipConfigurations** |Raccolta di oggetti di configurazione IP usati da schede di rete connessa toohello subnet | |

### <a name="name-resolution"></a>Risoluzione dei nomi
Per impostazione predefinita, utilizza la rete virtuale [la risoluzione dei nomi fornita da Azure](virtual-networks-name-resolution-for-vms-and-role-instances.md) hello di tooresolve nomi all'interno di hello rete virtuale e nella rete Internet pubblica. Tuttavia, se ci si connette i data center locale tooyour di reti virtuali, è necessario tooprovide [il proprio server DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md) tooresolve nomi tra le reti.  

### <a name="limits"></a>Limiti
Esaminare i limiti di rete hello in hello [Azure limita](../azure-subscription-service-limits.md#networking-limits) tooensure articolo che non sia in conflitto con i limiti di hello la progettazione. Alcun limiti possono essere aumentati aprendo un ticket di supporto.

### <a name="role-based-access-control-rbac"></a>Controllo degli accessi in base al ruolo
È possibile utilizzare [Azure RBAC](../active-directory/role-based-access-built-in-roles.md) livello hello toocontrol di utenti diversi di accesso potrebbe disporre di risorse toodifferent in Azure. In questo modo è possibile isolare il lavoro hello eseguita dal team in base alle proprie esigenze.

Come quanto riguarda le reti virtuali sono interessati, gli utenti di hello **rete collaboratore** ruolo dispongono del controllo completo sulle risorse di rete virtuale di Azure Resource Manager. Analogamente, gli utenti di hello **classico rete collaboratore** ruolo dispongono del controllo completo sulle risorse di rete virtuale classica.

> [!NOTE]
> È anche possibile [creare propri ruoli](../active-directory/role-based-access-control-configure.md) tooseparate esigenze amministrative.
>
>

## <a name="design"></a>Progettazione
Dopo avere stabilito le risposte hello domande toohello hello [pianificare](#Plan) sezione, esaminare hello seguenti prima di definire le reti virtuali.

### <a name="number-of-subscriptions-and-vnets"></a>Numero di sottoscrizioni e reti virtuali
È necessario considerare la creazione di più reti virtuali in hello seguenti scenari:

* **Macchine virtuali che devono toobe posizionate in diverse posizioni Azure**. Le reti virtuali in Azure fanno riferimento a un'area geografica e non possono estendersi a più località. Pertanto, è necessario almeno una rete virtuale per ogni località di Azure da macchine virtuali toohost nel.
* **I carichi di lavoro che richiedono toobe completamente isolato dagli altri**. È possibile creare reti virtuali separate, tale hello anche usare spazi di indirizzi IP stesso, tooisolate carichi di lavoro diversi uno da altro.

Tenere presente che vengono visualizzati sopra i limiti di hello per area, per ogni sottoscrizione. Pertanto, che è possibile utilizzare più limite di hello tooincrease le sottoscrizioni di risorse che è possibile gestire in Azure. È possibile utilizzare una VPN site-to-site, o un circuito ExpressRoute, tooconnect reti virtuali in diverse sottoscrizioni.

### <a name="subscription-and-vnet-design-patterns"></a>Modelli di progettazione per sottoscrizioni e reti virtuali
tabella di Hello seguente illustra alcuni modelli di progettazione comuni per l'utilizzo di sottoscrizioni e le reti virtuali.

| Scenario | Diagramma | Vantaggi | Svantaggi |
| --- | --- | --- | --- |
| Singola sottoscrizione, due reti virtuali per app |![Singola sottoscrizione](./media/virtual-network-vnet-plan-design-arm/figure1.png) |Toomanage una sola sottoscrizione. |Numero massimo di reti virtuali per area di Azure. Oltre questo limite, sono necessarie ulteriori sottoscrizioni. Hello revisione [Azure limita](../azure-subscription-service-limits.md#networking-limits) articolo per informazioni dettagliate. |
| Una sottoscrizione per app, due reti virtuali per app |![Singola sottoscrizione](./media/virtual-network-vnet-plan-design-arm/figure2.png) |Usa solo due reti virtuali per sottoscrizione. |Più difficile toomanage quando sono presenti troppe app. |
| Una sottoscrizione per business unit, due reti virtuali per app. |![Singola sottoscrizione](./media/virtual-network-vnet-plan-design-arm/figure3.png) |Equilibrio tra numero di sottoscrizioni e reti virtuali. |Numero massimo di reti virtuali per business unit (sottoscrizione). Hello revisione [Azure limita](../azure-subscription-service-limits.md#networking-limits) articolo per informazioni dettagliate. |
| Una sottoscrizione per business unit, due reti virtuali per gruppo di app. |![Singola sottoscrizione](./media/virtual-network-vnet-plan-design-arm/figure4.png) |Equilibrio tra numero di sottoscrizioni e reti virtuali. |Le app devono essere isolate usando subnet e gruppi di sicurezza di rete. |

### <a name="number-of-subnets"></a>Numero di subnet
È necessario considerare più subnet in una rete virtuale in hello seguenti scenari:

* **Numero insufficiente di indirizzi IP privati per tutte le schede di interfaccia di rete in una subnet**. Se lo spazio degli indirizzi di subnet non contiene il numero sufficiente di indirizzi IP per il numero di hello di schede di rete nella subnet hello, è necessario toocreate più subnet. Tenere presente che Azure riserva 5 indirizzi IP privati da ogni subnet che non possono essere utilizzati: hello prima e ultima indirizzi di hello spazio di indirizzi (indirizzo di subnet hello e multicast) e 3 indirizzi toobe utilizzato internamente (per scopi DNS e DHCP).
* **Sicurezza**. È possibile utilizzare gruppi di tooseparate di subnet di macchine virtuali rispetto a altro per i carichi di lavoro che dispone di un multi-livello struttura e applicare diverse [rete sicurezza gruppi](virtual-networks-nsg.md#subnets) per queste subnet.
* **Connettività ibrida**. È possibile utilizzare anche gateway VPN e circuiti ExpressRoute[connettersi](../vpn-gateway/vpn-gateway-about-vpngateways.md#s2smulti) tooone le reti virtuali in un altro tooyour locali e nel data center. Gateway VPN e circuiti ExpressRoute richiedono una subnet di propri toobe creato.
* **Appliance virtuali**. È possibile usare un'appliance virtuale, ad esempio un firewall, un acceleratore WAN o un gateway VPN in una rete virtuale di Azure. Quando si esegue questa operazione, è necessario troppo[instradare il traffico](virtual-networks-udr-overview.md) toothose accessori e isolarli nella propria subnet.

### <a name="subnet-and-nsg-design-patterns"></a>Modelli di progettazione di subnet e gruppi di sicurezza di rete
tabella di Hello seguente illustra alcuni modelli di progettazione comuni per l'utilizzo di subnet.

| Scenario | Diagramma | Vantaggi | Svantaggi |
| --- | --- | --- | --- |
| Singola subnet, gruppi di sicurezza di rete per livello dell'applicazione, per applicazione |![Singola subnet](./media/virtual-network-vnet-plan-design-arm/figure5.png) |Solo una subnet toomanage. |Più tooisolate necessarie di NSGs ogni applicazione. |
| Una subnet per app, gruppi di sicurezza di rete per livello dell'applicazione |![Subnet per app](./media/virtual-network-vnet-plan-design-arm/figure6.png) |Toomanage NSGs meno. |Più subnet toomanage. |
| Una subnet per livello dell'applicazione, gruppi di sicurezza di rete per app. |![Subnet per livello](./media/virtual-network-vnet-plan-design-arm/figure7.png) |Equilibrio tra numero di subnet e gruppi di sicurezza di rete. |Numero massimo di NSG per sottoscrizione. Hello revisione [Azure limita](../azure-subscription-service-limits.md#networking-limits) articolo per informazioni dettagliate. |
| Una subnet per livello dell'applicazione, per app, gruppi di sicurezza di rete per subnet |![Subnet per livello per app](./media/virtual-network-vnet-plan-design-arm/figure8.png) |Probabile numero inferiore di gruppi di sicurezza di rete. |Più subnet toomanage. |

## <a name="sample-design"></a>Progettazione di esempio
un'applicazione hello tooillustrate delle informazioni di hello in questo articolo, prendere in considerazione hello seguente scenario.

Si lavora per un'azienda con 2 data center in America del Nord e due data center in Europa. Identificato 6 cliente diverso applicazioni gestite da 2 diverse unità aziendali che si desidera tooAzure toomigrate come un progetto pilota. architettura di base per le applicazioni di hello Hello sono i seguenti:

* App1, App2, App3 e App4 sono applicazioni Web ospitate su server Linux con Ubuntu in esecuzione. Ogni applicazione si connette il server di applicazione separata tooa che ospita servizi RESTful nei server Linux. servizi RESTful Hello connettono database di MySQL tooa back-end.
* App5 e App6 sono applicazioni Web ospitate in Windows Server con Windows Server 2012 R2 in esecuzione. Ogni applicazione si connette tooa database di SQL Server back-end.
* Tutte le app sono attualmente ospitate in uno dei centri dati della società hello in Nord America.
* data center locale di Hello utilizzare lo spazio degli indirizzi di 10.0.0.0/8 hello.

È necessario disporre di una soluzione di rete virtuale che soddisfi i seguenti requisiti hello toodesign:

* Ogni business unit non deve dipendere dal consumo di risorse di altre business unit.
* È necessario ridurre la quantità hello di reti virtuali e subnet gestione toomake più semplice.
* Ogni business unit deve avere una singola rete virtuale di test/sviluppo usata per tutte le applicazioni.
* Ogni applicazione è ospitata in 2 diversi data center di Azure per continente (America del Nord ed Europa).
* Le applicazioni sono completamente isolate l'una dall'altra.
* Ogni applicazione può essere usato dai clienti in hello Internet tramite HTTP.
* Ogni applicazione è accessibile per gli utenti connessi toohello locale data Center tramite un tunnel crittografato.
* Connessione locale tooon data Center deve utilizzare i dispositivi VPN esistenti.
* Hello gruppo rete della società deve avere il controllo completo sulla configurazione della rete virtuale hello.
* Sviluppatori in ogni business unit devono essere in grado di toodeploy macchine virtuali tooexisting subnet.
* Tutte le applicazioni verranno migrate come se fossero tooAzure (sollevamento e spostamento).
* database Hello in ogni posizione devono essere replicati tooother Azure posizioni una volta al giorno.
* Ogni applicazione deve usare 5 server Web front-end, 2 server applicazioni (se necessario) e 2 server database.

### <a name="plan"></a>Pianificazione
È consigliabile iniziare la progettazione della pianificazione per rispondere alle domande hello in hello [definiscono i requisiti](#Define-requirements) sezione come illustrato di seguito.

1. Le posizioni di Azure saranno necessario utilizzare toohost reti virtuali?

    2 località in America del Nord e 2 località in Europa. È consigliabile scegliere basati sulla posizione fisica di hello del data center locale esistente. In questo modo la connessione da tooAzure le posizioni fisiche avrà una migliore latenza.
2. È necessario tooprovide comunicazione tra questi percorsi di Azure?

    Sì. Poiché i database di hello devono essere replicati tooall percorsi.
3. È necessario tooprovide comunicazione tra il VNet(s) di Azure e il data center locale?

    Sì. Poiché gli utenti connessi toohello locale data Center deve essere applicazioni hello in grado di tooaccess attraverso un tunnel crittografato.
4. Quante VM IaaS sono necessarie per la soluzione?

    200 VM IaaS. App1, App2, App3 e App4 richiedono 5 server Web, 2 server applicazioni e 2 server database per ognuna. Questo equivale a un totale di 9 VM IaaS per applicazione o 36 VM IaaS. App5 e App6 richiedono 5 server Web e 2 server database. Questo equivale a un totale di 7 VM IaaS per applicazione o 14 VM IaaS. Per questo motivo, sono necessarie 50 VM IaaS per tutte le applicazioni in ogni area di Azure. Poiché è necessario aree toouse 4, saranno presenti 200 macchine virtuali IaaS.

    I server DNS tooprovide in ogni rete virtuale o il nome di tooresolve centri dati in locale, è necessario anche tra le macchine virtuali IaaS di Azure e la rete locale.
5. È necessario tooisolate il traffico in base ai gruppi di macchine virtuali (i server web, ovvero front-end e server di database back-end)?

    Sì. Le applicazioni devono essere completamente isolate l'una dall'altra e anche ogni livello dell'applicazione deve essere isolato.
6. È necessario che il flusso del traffico toocontrol utilizzando Appliance virtuali?

    No. Dispositivi di rete può essere utilizzato tooprovide maggiore controllo del flusso del traffico, tra cui registrazione più dettagliata di piano dati.
7. Fare gli utenti necessità diversi set di autorizzazioni toodifferent risorse di Azure?

    Sì. Hello rete team deve controllo completo sulle impostazioni di rete virtuale di hello, mentre gli sviluppatori devono essere solo in grado di toodeploy le subnet esistente toopre macchine virtuali.

### <a name="design"></a>Progettazione
È consigliabile seguire progettazione hello specificando le sottoscrizioni, le reti virtuali, subnet e NSGs. I gruppi di sicurezza di rete verranno discussi qui, ma è consigliabile acquisire altre informazioni sui [gruppi di sicurezza di rete](virtual-networks-nsg.md) prima di completare la progettazione.

**Numero di sottoscrizioni e reti virtuali**

Hello seguenti requisiti è toosubscriptions correlati e le reti virtuali:

* Ogni business unit non deve dipendere dal consumo di risorse di altre business unit.
* È necessario ridurre la quantità hello di reti virtuali e subnet.
* Ogni business unit deve avere una singola rete virtuale di test/sviluppo usata per tutte le applicazioni.
* Ogni applicazione è ospitata in 2 diversi data center di Azure per continente (America del Nord ed Europa).

In base a tali requisiti, è necessaria una sottoscrizione per ogni business unit. In questo modo, il consumo di risorse di una business unit non influirà sui limiti per le altre business unit. Poiché si desidera toominimize hello numero di reti virtuali, è consigliabile utilizzare hello **una sottoscrizione per ogni business unit, due reti virtuali per ogni gruppo di applicazioni** di schema come illustrato di seguito.

![Singola sottoscrizione](./media/virtual-network-vnet-plan-design-arm/figure9.png)

È inoltre necessario spazio di indirizzi hello toospecify per ogni rete virtuale. Poiché è necessaria la connettività tra hello centri dati in locale e hello aree di Azure, spazio degli indirizzi di hello utilizzato per le reti virtuali di Azure non può essere in conflitto con la rete locale hello e spazio di indirizzo hello utilizzato da ogni rete virtuale non deve essere in conflitto con altre reti virtuali esistenti. È possibile utilizzare gli spazi degli indirizzi hello nella tabella hello sotto toosatisfy questi requisiti.  

| **Sottoscrizione** | **Rete virtuale** | **Area di Azure** | **Spazio degli indirizzi** |
| --- | --- | --- | --- |
| BU1 |ProdBU1US1 |Stati Uniti occidentali |172.16.0.0/16 |
| BU1 |ProdBU1US2 |Stati Uniti orientali |172.17.0.0/16 |
| BU1 |ProdBU1EU1 |Europa settentrionale |172.18.0.0/16 |
| BU1 |ProdBU1EU2 |Europa occidentale |172.19.0.0/16 |
| BU1 |TestDevBU1 |Stati Uniti occidentali |172.20.0.0/16 |
| BU2 |TestDevBU2 |Stati Uniti occidentali |172.21.0.0/16 |
| BU2 |ProdBU2US1 |Stati Uniti occidentali |172.22.0.0/16 |
| BU2 |ProdBU2US2 |Stati Uniti orientali |172.23.0.0/16 |
| BU2 |ProdBU2EU1 |Europa settentrionale |172.24.0.0/16 |
| BU2 |ProdBU2EU2 |Europa occidentale |172.25.0.0/16 |

**Numero di subnet e gruppi di sicurezza di rete**

Hello seguenti requisiti è correlati toosubnets e NSGs:

* È necessario ridurre la quantità hello di reti virtuali e subnet.
* Le applicazioni sono completamente isolate l'una dall'altra.
* Ogni applicazione può essere usato dai clienti in hello Internet tramite HTTP.
* Ogni applicazione è accessibile per gli utenti connessi toohello locale data Center tramite un tunnel crittografato.
* Connessione locale tooon data Center deve utilizzare i dispositivi VPN esistenti.
* database Hello in ogni posizione devono essere replicati tooother Azure posizioni una volta al giorno.

In base a tali requisiti, è possibile utilizzare una subnet per ogni livello di applicazione e traffico toofilter NSGs per ogni applicazione. In questo modo, sono sufficienti 3 subnet in ogni rete virtuale (front-end, livello dell'applicazione e livello dati) e un gruppo di sicurezza di rete per applicazione per ogni subnet. In questo caso, è necessario ricorrere hello **una subnet per ogni livello di applicazione, NSGs per ogni app** modello di progettazione. Figura che segue Hello di seguito viene illustrato l'utilizzo di hello del modello di struttura hello che rappresenta hello **ProdBU1US1** rete virtuale.

![Una subnet per livello, un gruppo di sicurezza di rete per applicazione per livello](./media/virtual-network-vnet-plan-design-arm/figure11.png)

Tuttavia, è necessario anche toocreate una subnet aggiuntiva per la connettività VPN hello tra hello reti virtuali e i data center locale. Ed è necessario spazio di indirizzi hello toospecify per ogni subnet. Hello figura seguente mostra una soluzione di esempio per **ProdBU1US1** rete virtuale. È necessario replicare questo scenario per ogni rete virtuale. Ogni colore rappresenta un'applicazione diversa.

![Rete virtuale di esempio](./media/virtual-network-vnet-plan-design-arm/figure10.png)

**Controllo dell’accesso**

Salve, i seguenti requisiti correlati tooaccess controllo:

* Hello gruppo rete della società deve avere il controllo completo sulla configurazione della rete virtuale hello.
* Sviluppatori in ogni business unit devono essere in grado di toodeploy macchine virtuali tooexisting subnet.

In base a tali requisiti, è possibile aggiungere utenti da hello rete toohello team predefinito **rete collaboratore** ruolo in ogni sottoscrizione; e creare un ruolo personalizzato per hello gli sviluppatori di applicazioni nell'assegnazione di ogni sottoscrizione subnet tooexisting macchine virtuali di loro diritti tooadd.

## <a name="next-steps"></a>Passaggi successivi
* [Distribuire una rete virtuale](virtual-networks-create-vnet-arm-template-click.md) in base a uno scenario.
* Comprendere come troppo[il bilanciamento del carico](../load-balancer/load-balancer-overview.md) le macchine virtuali IaaS e [gestire il routing tramite più aree di Azure](../traffic-manager/traffic-manager-overview.md).
* Altre informazioni, vedere [NSGs e come tooplan e progettazione](virtual-networks-nsg.md) una soluzione di gruppo.
* Altre informazioni sulle [opzioni di connettività cross-premise e della rete virtuale](../vpn-gateway/vpn-gateway-about-vpngateways.md#s2smulti).
