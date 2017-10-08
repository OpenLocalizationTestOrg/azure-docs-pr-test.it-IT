---
title: 'Panoramica di Gateway VPN: Creare connessioni VPN cross-premise reti virtuali tooAzure | Documenti Microsoft'
description: Questa panoramica di Gateway VPN illustra hello modi tooconnect tooAzure reti virtuali con una connessione VPN su Internet hello. Sono inclusi i diagrammi delle configurazioni della connessione di base.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 2358dd5a-cd76-42c3-baf3-2f35aadc64c8
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/05/2017
ms.author: cherylmc
ms.openlocfilehash: 899270734270632a5b12d56021c924e977725a7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="about-vpn-gateway"></a>Informazioni sul gateway VPN

Un gateway VPN è un tipo di gateway di rete virtuale che invia il traffico crittografato attraverso un tooan connessione pubblica posizione locale. È inoltre possibile utilizzare il traffico VPN gateway toosend crittografati tra reti virtuali di Azure tramite rete Microsoft hello. toosend encrypted traffico di rete tra la rete virtuale di Azure e il sito locale, è necessario creare un gateway VPN per la rete virtuale.

Ogni rete virtuale può avere solo un gateway VPN, tuttavia, è possibile creare più connessioni toohello stesso gateway VPN. Una configurazione di connessione multisito ne è un esempio. Quando si crea più connessioni toohello stesso gateway VPN, tutti i tunnel VPN, inclusi VPN Point-to-Site, condivisione hello larghezza di banda disponibile per il gateway hello.

### <a name="whatis"></a>Informazioni sul gateway di rete virtuale

Un gateway di rete virtuale è costituito da due o più macchine virtuali che sono distribuiti tooa subnet specifica chiamata hello GatewaySubnet. macchine virtuali che si trovano in hello GatewaySubnet vengono creati quando si crea il gateway di rete virtuale hello Hello. Il gateway di rete virtuale le macchine virtuali sono le tabelle di routing configurato toocontain e gateway toohello specifico di servizi gateway. È possibile configurare direttamente le macchine virtuali che fanno parte del gateway di rete virtuale hello hello ed evitare di distribuire risorse aggiuntive toohello GatewaySubnet.

Quando si crea un gateway di rete virtuale utilizzando il tipo di gateway hello "Vpn", viene creato un tipo specifico di gateway di rete virtuale che esegue la crittografia del traffico. un gateway VPN. Too45 minuti toocreate può richiedere un gateway VPN. Questo avviene perché hello macchine virtuali per il gateway VPN hello vengono distribuito toohello GatewaySubnet e configurato con impostazioni hello specificate. Hello SKU di Gateway selezionato determina le potenzialità hello le macchine virtuali sono.

## <a name="gwsku"></a>SKU del gateway

[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

## <a name="configuring"></a>Configurazione di un gateway VPN

Una connessione gateway VPN si basa su più risorse configurate con impostazioni specifiche. La maggior parte delle risorse hello può essere configurata separatamente, anche se devono essere configurati in un determinato ordine, in alcuni casi.

### <a name="settings"></a>Impostazioni

le impostazioni di Hello scelto per ogni risorsa sono critici toocreating ha stabilito una connessione. Per informazioni sulle singole risorse e le impostazioni per il gateway VPN, vedere [Informazioni sulle impostazioni del gateway VPN](vpn-gateway-about-vpn-gateway-settings.md). Hello articolo sono contenute informazioni toohelp comprendere i tipi di gateway, tipi di VPN, i tipi di connessione, subnet gateway, gateway di rete locale e varie altre impostazioni di risorsa se si desidera tooconsider.

### <a name="tools"></a>Strumenti di distribuzione

È possibile avviare la creazione e configurazione delle risorse mediante uno strumento di configurazione, ad esempio hello portale di Azure. In un secondo momento, è possibile decidere di tooswitch tooanother strumento, come PowerShell, tooconfigure altre risorse, o modificare le risorse esistenti, se applicabile. Attualmente, è possibile configurare ogni impostazione della risorsa e la risorsa nel portale di Azure hello. istruzioni di Hello negli articoli hello per ogni topologia di connessione specifica quando è necessario uno strumento di configurazione specifico. 

### <a name="models"></a>Modello di distribuzione

Quando si configura un gateway VPN, hello i passaggi dipendono dal modello di distribuzione hello utilizzato toocreate la rete virtuale. Ad esempio, se è stata creata la rete virtuale utilizzando il modello di distribuzione classica hello, si usano le linee guida hello e istruzioni per la distribuzione classica hello toocreate del modello e configurare le impostazioni del gateway VPN. Per altre informazioni sui modelli di distribuzione, vedere [Confronto tra distribuzione di Azure Resource Manager e classica: comprensione dei modelli di implementazione e dello stato delle risorse](../azure-resource-manager/resource-manager-deployment-model.md).

## <a name="diagrams"></a>Diagrammi delle topologie di connessione

È importante tooknow che sono disponibili diverse configurazioni per le connessioni gateway VPN. È necessario toodetermine la migliore configurazione adatta alle proprie esigenze. Nelle sezioni hello riportato di seguito, è possibile visualizzare i diagrammi di topologia e le informazioni sui seguenti connessioni gateway VPN hello: hello le sezioni seguenti contenga tabelle cui elencano:

* Modello di distribuzione disponibile
* Strumenti di configurazione disponibili
* Collegamenti che consentono di accedere direttamente tooan articolo, se disponibile

Utilizzare hello diagrammi e le descrizioni toohelp hello selezionare connessione topologia toomatch esigenze. Hello diagrammi mostrano hello topologie principali della linea di base, ma è possibile toobuild configurazioni più complesse utilizzando i diagrammi di hello come linea guida.

## <a name="s2smulti"></a>Da sito a sito e multisito (tunnel VPN IPsec/IKE)

### <a name="S2S"></a>Da sito a sito

Una connessione gateway VPN da sito a sito (S2S) avviene tramite un tunnel VPN IPsec/IKE (IKEv1 o IKEv2). Una connessione S2S richiede un VPN dispositivo si trova in locale che dispone di un tooit di indirizzo IP pubblico e non si trova dietro un NAT. Le connessioni S2S possono essere usate per le configurazioni cross-premise e ibride.   

![Esempio di connessione gateway VPN di Azure da sito a sito](./media/vpn-gateway-about-vpngateways/vpngateway-site-to-site-connection-diagram.png)

### <a name="Multi"></a>Multisito

Questo tipo di connessione è una variante di hello connessione Site-to-Site. Creare più di una connessione VPN da gateway di rete virtuale, in genere connessione toomultiple siti locali. Quando si usano più connessioni, è necessario usare una rete VPN di tipo RouteBased (nota come gateway dinamico nell'ambito delle reti virtuali classiche). Poiché ogni rete virtuale può avere solo un gateway VPN, tutte le connessioni tramite gateway hello condividono la larghezza di banda disponibile hello. Questo tipo di connessione è spesso definito "multisito".

![Esempio di connessione gateway VPN di Azure multisito](./media/vpn-gateway-about-vpngateways/vpngateway-multisite-connection-diagram.png)

### <a name="deployment-models-and-methods-for-site-to-site-and-multi-site"></a>Metodi e modelli di distribuzione per connessioni da sito a sito e multisito

[!INCLUDE [vpn-gateway-table-site-to-site](../../includes/vpn-gateway-table-site-to-site-include.md)]

## <a name="P2S"></a>Da punto a sito (VPN su SSTP)

Un gateway VPN da punto a sito (P2S) consente di creare una rete virtuale tooyour di connessione protetta da un computer client. Le connessioni VPN Point-to-Site sono utili quando si desidera tooconnect tooyour rete virtuale da una posizione remota, ad esempio quando sono il telelavoro da casa o di una conferenza. Una VPN P2S è anche un toouse soluzione utile anziché una VPN da sito a sito quando si dispone solo alcuni client che richiedono tooconnect tooa rete virtuale. 

A differenza delle connessioni da sito a sito, le connessioni da punto a sito non necessitano di un indirizzo IP pubblico locale o di un dispositivo VPN. Connessioni P2S possono essere utilizzate con le connessioni S2S tramite hello stesso gateway VPN, purché tutti i requisiti di configurazione di hello per entrambe le connessioni sono compatibili.

Usa P2S hello SSTP Secure Socket Tunneling Protocol (), che è un protocollo di rete VPN basata su SSL. Viene stabilita una connessione di VPN P2S avviandolo dal computer client hello.

![Esempio di connessione gateway VPN di Azure da punto a sito](./media/vpn-gateway-about-vpngateways/vpngateway-point-to-site-connection-diagram.png)

### <a name="deployment-models-and-methods-for-point-to-site"></a>Metodi e modelli di distribuzione per connessioni da punto a sito

[!INCLUDE [vpn-gateway-table-point-to-site](../../includes/vpn-gateway-table-point-to-site-include.md)]

## <a name="V2V"></a>Connessioni da rete virtuale a rete virtuale (tunnel VPN IPsec/IKE)

La connessione di una rete virtuale (VNet a VNet) tooanother di rete virtuale è simile tooconnecting un percorso di rete virtuale tooan locale del sito. Entrambi i tipi di connettività di utilizzare un tooprovide gateway VPN un tunnel sicuro tramite IPsec/IKE. È anche possibile combinare una comunicazione tra reti virtuali con configurazioni di connessioni multisito. Questo permette di definire topologie di rete che consentono di combinare la connettività cross-premise con la connettività tra reti virtuali.

Hello reti virtuali connesse può essere:

* in hello stesso o in aree diverse
* in hello sottoscrizioni uguale o diverse 
* in hello modelli di distribuzione uguale o diverso

![Esempio di connessione di Azure tra reti virtuali Gateway VPN tooVNet](./media/vpn-gateway-about-vpngateways/vpngateway-vnet-to-vnet-connection-diagram.png)

### <a name="connections-between-deployment-models"></a>Connessioni tra modelli di distribuzione

Azure offre attualmente di due modelli di distribuzione: classica e Resource Manager. Se si usa Azure da qualche tempo, si dispone probabilmente di VM e istanze del ruolo di Azure in esecuzione su una rete virtuale classica. Le VM e le istanze del ruolo più recenti potrebbero invece essere in esecuzione su una rete virtuale creata in Resource Manager. È possibile creare una connessione tra hello reti virtuali tooallow risorse hello in una rete virtuale toocommunicate direttamente con le risorse in un altro.

### <a name="vnet-peering"></a>Peering reti virtuali

Potrebbe essere in grado di toouse peering toocreate la connessione, reti virtuali fino a quando la rete virtuale soddisfa i requisiti specifici. Peering reti virtuali non usa un gateway di rete virtuale. Per altre informazioni, vedere [Peering reti virtuali](../virtual-network/virtual-network-peering-overview.md).

### <a name="deployment-models-and-methods-for-vnet-to-vnet"></a>Metodi e modelli di distribuzione per connessioni da rete virtuale a rete virtuale

[!INCLUDE [vpn-gateway-table-vnet-to-vnet](../../includes/vpn-gateway-table-vnet-to-vnet-include.md)]

## <a name="ExpressRoute"></a>ExpressRoute (connessione privata dedicata)

Microsoft Azure ExpressRoute consente di estendere le reti locali nel cloud di Microsoft hello su una connessione privata dedicata mediante un provider di connettività. Con ExpressRoute, è possibile stabilire i servizi cloud di tooMicrosoft connessioni, come Microsoft Azure, Office 365 e CRM Online. La connettività può essere stabilita da una rete (IP VPN) any-to-any, da una rete Ethernet punto a punto o da una Cross Connection virtuale tramite un provider di connettività presso una struttura di condivisione del percorso.

Le connessioni ExpressRoute non sfruttano hello rete Internet pubblica. In questo modo toooffer connessioni ExpressRoute più affidabilità, velocità più elevate, minori latenze e una maggiore sicurezza rispetto alle connessioni tramite hello Internet.

Una connessione ExpressRoute non usa un gateway VPN, anche se usa un gateway di rete virtuale come parte della configurazione obbligatoria. In una connessione ExpressRoute, gateway di rete virtuale hello è configurato con tipo di gateway hello 'ExpressRoute' anziché 'Vpn'. Per ulteriori informazioni su ExpressRoute, vedere hello [Panoramica tecnica su ExpressRoute](../expressroute/expressroute-introduction.md).

## <a name="coexisting"></a>Connessioni coesistenti da sito a sito ed ExpressRoute

ExpressRoute è una connessione diretta dalla rate WAN dedicata (non in rete Internet pubblica hello) tooMicrosoft servizi, incluso Azure. Site-to-Site VPN traffico crittografati tramite hello viaggi Internet pubblica. Viene tooconfigure in grado di connessioni VPN Site-to-Site ed ExpressRoute per stessa rete virtuale hello presenta diversi vantaggi.

È possibile configurare una VPN da sito a sito come un percorso di failover sicura per ExpressRoute o usare una VPN Site-to-Site tooconnect toosites che non fanno parte della rete, ma che sono connessi tramite ExpressRoute. Si noti che questa configurazione richiede due gateway di rete virtuale per hello stessa rete virtuale, uno usando il tipo di gateway 'Vpn' hello e hello utilizzando il tipo di gateway hello 'ExpressRoute'.

![Esempio di connessioni coesistenti ExpressRoute e gateway VPN](./media/vpn-gateway-about-vpngateways/expressroute-vpngateway-coexisting-connections-diagram.png)

### <a name="deployment-models-and-methods-for-s2s-and-expressroute"></a>Metodi e modelli di distribuzione per le connessioni da sito a sito ed ExpressRoute

[!INCLUDE [vpn-gateway-table-coexist](../../includes/vpn-gateway-table-coexist-include.md)]

## <a name="pricing"></a>Prezzi

[!INCLUDE [vpn-gateway-about-pricing-include](../../includes/vpn-gateway-about-pricing-include.md)]

Per informazioni sugli SKU del gateway VPN, vedere [SKU del gateway](vpn-gateway-about-vpn-gateway-settings.md#gwsku).

## <a name="faq"></a>Domande frequenti

Per domande frequenti sul gateway VPN, vedere hello [domande frequenti su Gateway VPN](vpn-gateway-vpn-faq.md).

## <a name="next-steps"></a>Passaggi successivi

- Pianificare la configurazione del gateway VPN. Vedere [Pianificazione e progettazione per il gateway VPN](vpn-gateway-plan-design.md).
- Hello vista [domande frequenti su Gateway VPN](vpn-gateway-vpn-faq.md) per ulteriori informazioni.
- Hello vista [sottoscrizione e limiti dei servizi](../azure-subscription-service-limits.md#networking-limits).
- Informazioni su alcune delle hello altre chiavi [funzionalità di rete](../networking/networking-overview.md) di Azure.
