---
title: domande frequenti sulla rete virtuale aaaAzure | Documenti Microsoft
description: "Le risposte toohello più domande frequenti sulle reti virtuali di Microsoft Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 54bee086-a8a5-4312-9866-19a1fba913d0
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/18/2017
ms.author: jdial
ms.openlocfilehash: c2f9faee41b9c45e8bb196c58282d597ae732e54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-network-frequently-asked-questions-faq"></a>Domande frequenti sulla rete virtuale di Azure

## <a name="virtual-network-basics"></a>Nozioni di base sulla rete virtuale

### <a name="what-is-an-azure-virtual-network-vnet"></a>Che cos'è una rete virtuale di Azure?
Una rete virtuale di Azure (VNet) è una rappresentazione della rete nel cloud hello. È un isolamento logico di hello sottoscrizione tooyour cloud di Azure dedicato. È possibile utilizzare le reti virtuali tooprovision e gestire reti private virtuali (VPN) in Azure e, facoltativamente, hello collegamento reti virtuali con altre reti virtuali in Azure o con locale toocreate ibrida o cross-premise soluzioni di infrastrutture IT. Ogni rete virtuale che è creare ha il proprio blocco CIDR e può essere collegato tooother reti locali e reti virtuali fino a quando non si sovrappongano blocchi CIDR hello. È inoltre controllo delle impostazioni del server DNS per le reti virtuali e la segmentazione della rete virtuale di hello in subnet.

Usare le reti virtuali per:

* Creare una rete virtuale privata dedicata solo cloud. Per una soluzione personalizzata, non è sempre necessaria una configurazione cross-premise. Quando si crea una rete virtuale, i servizi e macchine virtuali all'interno della rete virtuale possono comunicare direttamente e in modo sicuro tra loro nel cloud hello. Mantiene il traffico in modo protetto all'interno di hello rete virtuale, ma consente ancora tooconfigure le connessioni di endpoint per le macchine virtuali hello e i servizi che richiedono la comunicazione Internet come parte della soluzione.
* Estendere in modo sicuro il data center con reti, è possibile compilare la capacità del Data Center di scalabilità toosecurely (S2S) VPN da sito a sito tradizionali. VPN S2S utilizzare IPSEC tooprovide una connessione sicura tra il gateway VPN di aziendale e Azure.
* Scenari di cloud ibrido di abilitare di che le reti virtuali consentono hello flessibilità toosupport una gamma di scenari cloud ibridi. È possibile connettersi in modo sicuro le applicazioni basate su cloud tooany tipo sistemi Unix e di sistema locale, ad esempio mainframe.

### <a name="how-do-i-know-if-i-need-a-vnet"></a>Come scoprire se è necessaria una rete virtuale?
Hello [Panoramica di rete virtuale](virtual-networks-overview.md) articolo fornisce una tabella che faciliti hello migliore rete dell'opzione di progettazione.

### <a name="how-do-i-get-started"></a>Come iniziare?
Visitare hello [documentazione della rete virtuale](https://docs.microsoft.com/azure/virtual-network/) tooget avviato. Questo contenuto offre una panoramica e sulla distribuzione per tutte le funzionalità di rete virtuale hello.

### <a name="can-i-use-vnets-without-cross-premises-connectivity"></a>È possibile usare reti virtuali senza connettività cross-premise?
Sì. Si può usare una rete virtuale senza la connettività ibrida. Ciò è particolarmente utile se si desidera toorun i controller di dominio Active Directory di Microsoft Windows Server e farm di SharePoint in Azure.

### <a name="can-i-perform-wan-optimization-between-vnets-or-a-vnet-and-my-on-premises-data-center"></a>È possibile eseguire l'ottimizzazione WAN tra reti virtuali o tra una rete virtuale e il data center locale?

Sì. È possibile distribuire un [appliance virtuale di rete di ottimizzazione WAN](https://azure.microsoft.com/marketplace/?term=wan+optimization) da diversi fornitori tramite hello Azure Marketplace.

## <a name="configuration"></a>Configurazione

### <a name="what-tools-do-i-use-toocreate-a-vnet"></a>Operazioni strumenti usare toocreate una rete virtuale?
È possibile utilizzare i seguenti strumenti toocreate hello o configurare una rete virtuale:

* Portale di Azure (per reti virtuali classiche e di Resource Manager).
* Un file di configurazione di rete (netcfg - solo per reti virtuali classiche). Vedere hello [configurare una rete virtuale usando un file di configurazione di rete](virtual-networks-using-network-configuration-file.md) articolo.
* PowerShell (per reti virtuali classiche e di Resource Manager).
* Interfaccia della riga di comando di Azure (per reti virtuali classiche e di Resource Manager).

### <a name="what-address-ranges-can-i-use-in-my-vnets"></a>Quali intervalli di indirizzi è possibile usare nelle reti virtuali?
Qualsiasi intervallo di indirizzi IP definito in [RFC 1918](http://tools.ietf.org/html/rfc1918). Ad esempio, 10.0.0.0/16.

### <a name="can-i-have-public-ip-addresses-in-my-vnets"></a>È possibile avere indirizzi IP pubblici nelle reti virtuali?
Sì. Per ulteriori informazioni su intervalli di indirizzi IP pubblici, vedere hello [spazio di indirizzi IP pubblici in una rete virtuale](virtual-networks-public-ip-within-vnet.md) articolo. Gli indirizzi IP pubblici non sarà accessibili direttamente da Internet hello.

### <a name="is-there-a-limit-toohello-number-of-subnets-in-my-vnet"></a>Esiste un toohello limita il numero di subnet nella rete virtuale?
Sì. Hello lettura [Azure limita](../azure-subscription-service-limits.md#networking-limits) articolo per informazioni dettagliate. Gli spazi degli indirizzi della subnet non possono sovrapporsi.

### <a name="are-there-any-restrictions-on-using-ip-addresses-within-these-subnets"></a>Esistono restrizioni sull'uso di indirizzi IP all'interno di tali subnet?
Sì. Azure riserva alcuni indirizzi IP all'interno di ogni subnet. gli indirizzi IP e il cognome di subnet hello Hello sono riservati per conformità al protocollo, insieme a 3 più indirizzi utilizzato per i servizi di Azure.

### <a name="how-small-and-how-large-can-vnets-and-subnets-be"></a>Quanto piccole o grandi possono essere le reti virtuali e le subnet?
è supportata la subnet più piccola Hello è/29 e hello più grande è/8 (utilizzando le definizioni di subnet CIDR).

### <a name="can-i-bring-my-vlans-tooazure-using-vnets"></a>È possibile trasferire il tooAzure VLAN utilizzando le reti virtuali?
No. Le reti virtuali sono sovrapposizioni di livello 3. Azure non supporta alcuna semantica di livello 2.

### <a name="can-i-specify-custom-routing-policies-on-my-vnets-and-subnets"></a>È possibile specificare criteri di routing personalizzati nelle reti virtuali e nelle subnet?
Sì. È possibile usare User Defined Routing (UDR). Per altre informazioni su UDR, vedere [Route e inoltro IP definiti dall'utente](virtual-networks-udr-overview.md).

### <a name="do-vnets-support-multicast-or-broadcast"></a>Le reti virtuali supportano la distribuzione multicast o broadcast?
No. La distribuzione multicast o broadcast non è supportata.

### <a name="what-protocols-can-i-use-within-vnets"></a>Quali protocolli è possibile usare all'interno delle reti virtuali?
All'interno delle reti virtuali è possibile usare i protocolli TCP, UDP e ICMP TCP/IP. I pacchetti incapsulati IP in IP, multicast e broadcast e i pacchetti Generic Routing Encapsulation (GRE) sono bloccati all'interno delle reti virtuali. 

### <a name="can-i-ping-my-default-routers-within-a-vnet"></a>È possibile eseguire il ping dei router predefiniti all'interno di una rete virtuale?
No.

### <a name="can-i-use-tracert-toodiagnose-connectivity"></a>È possibile utilizzare tracert toodiagnose connettività?
No.

### <a name="can-i-add-subnets-after-hello-vnet-is-created"></a>È possibile aggiungere subnet dopo hello che è creazione della rete virtuale?
Sì. Subnet possono essere aggiunti tooVNets in qualsiasi momento purché l'indirizzo di subnet hello non fa parte di un'altra subnet nella rete virtuale hello.

### <a name="can-i-modify-hello-size-of-my-subnet-after-i-create-it"></a>È possibile modificare la subnet di dimensioni hello dopo la relativa creazione?
Sì. È possibile aggiungere, rimuovere, espandere o compattare una subnet se non sono presenti macchine virtuali o servizi distribuiti al suo interno.

### <a name="can-i-modify-subnets-after-i-created-them"></a>È possibile modificare le subnet dopo averle create?
Sì. È possibile aggiungere, rimuovere e modificare blocchi CIDR hello utilizzati da una rete virtuale.

### <a name="can-i-connect-toohello-internet-if-i-am-running-my-services-in-a-vnet"></a>È possibile connettersi toohello internet se si eseguono i servizi in una rete virtuale?
Sì. Tutti i servizi distribuiti all'interno di una rete virtuale possono connettersi toohello internet. Ogni servizio cloud distribuito in Azure è un VIP indirizzabile pubblicamente tooit assegnato. Sarà necessario toodefine gli endpoint di input per i ruoli PaaS e per le macchine virtuali tooenable queste connessioni tooaccept servizi da hello internet.

### <a name="do-vnets-support-ipv6"></a>Le reti virtuali supportano IPv6?
No. Al momento non è possibile usare IPv6 con le reti virtuali.

### <a name="can-a-vnet-span-regions"></a>Una rete virtuale può estendersi a più aree?
No. Una rete virtuale è limitato tooa singola area.

### <a name="can-i-connect-a-vnet-tooanother-vnet-in-azure"></a>È possibile collegare una rete virtuale in Azure di tooanother rete virtuale?
Sì. È possibile connettersi tramite una rete virtuale tooanother rete virtuale:
- Gateway VPN di Azure. Hello lettura [configurare una connessione di rete virtuale a](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) articolo per informazioni dettagliate. 
- Peering di rete virtuale. Hello lettura [Panoramica peering reti virtuali](virtual-network-peering-overview.md) articolo per informazioni dettagliate.

## <a name="name-resolution-dns"></a>Risoluzione del nome (DNS)

### <a name="what-are-my-dns-options-for-vnets"></a>Quali sono le opzioni DNS per le reti virtuali?
Tabella di decisione di utilizzare hello in hello [risoluzione dei nomi per le macchine virtuali e istanze del ruolo](virtual-networks-name-resolution-for-vms-and-role-instances.md) tooguide pagina tutti hello DNS opzioni disponibili.

### <a name="can-i-specify-dns-servers-for-a-vnet"></a>È possibile specificare i server DNS per una rete virtuale?
Sì. È possibile specificare indirizzi IP del server DNS nelle impostazioni di rete virtuale hello. Questo verrà applicato come server DNS di hello predefiniti per tutte le macchine virtuali nella rete virtuale hello.

### <a name="how-many-dns-servers-can-i-specify"></a>Quanti server DNS è possibile specificare?
Hello riferimento [Azure limita](../azure-subscription-service-limits.md#networking-limits) articolo per informazioni dettagliate.

### <a name="can-i-modify-my-dns-servers-after-i-have-created-hello-network"></a>È possibile modificare i server DNS dopo aver creato la rete hello?
Sì. È possibile modificare l'elenco dei server DNS hello per la rete virtuale in qualsiasi momento. Se si modifica l'elenco dei server DNS, è necessario toorestart delle macchine virtuali hello in una rete virtuale affinché possano toopick nuovo server DNS di hello.

### <a name="what-is-azure-provided-dns-and-does-it-work-with-vnets"></a>Qual è il DNS fornito da Azure e funziona con le reti virtuali?
Il DNS fornito da Azure è un servizio DNS multi-tenant offerto da Microsoft. Azure registra tutte le macchine virtuali e le istanze del ruolo del servizio cloud in questo servizio. Questo servizio fornisce la risoluzione dei nomi mediante il nome host per le macchine virtuali e istanze del ruolo contenute all'interno di hello stesso servizio cloud e nome di dominio completo per le macchine virtuali e istanze del ruolo in hello stessa rete virtuale. Hello lettura [risoluzione dei nomi per le macchine virtuali e istanze del ruolo](virtual-networks-name-resolution-for-vms-and-role-instances.md) toolearn articolo ulteriori informazioni su DNS.

> [!NOTE]
> È presente una limitazione in toohello questo tempo primi 100 servizi cloud in una rete virtuale per la risoluzione di nomi tra tenant mediante DNS fornito da Azure. Se si utilizza il proprio server DNS, questa limitazione non viene applicata.
> 
> 

### <a name="can-i-override-my-dns-settings-on-a-per-vm--service-basis"></a>È possibile ignorare le impostazioni DNS in base alla macchina virtuale/al servizio?
Sì. È possibile impostare i server DNS in una per ogni cloud servizio base toooverride hello impostazioni predefinite di rete. Tuttavia, è consigliabile usare quanto più possibile DNS a livello di rete.

### <a name="can-i-bring-my-own-dns-suffix"></a>È possibile trasferire il suffisso DNS personalizzato?
No. Non è possibile specificare un suffisso DNS personalizzato per le reti virtuali.

## <a name="connecting-virtual-machines"></a>Connessione di macchine virtuali

### <a name="can-i-deploy-vms-tooa-vnet"></a>È possibile distribuire le macchine virtuali tooa rete virtuale?
Sì. Tooa di interfacce (NIC) collegate rete tutte le VM distribuite tramite modello di distribuzione di gestione risorse di hello deve essere connesso tooa rete virtuale. Macchine virtuali distribuite tramite il modello di distribuzione classica hello possono facoltativamente essere connesso tooa rete virtuale.

### <a name="what-are-hello-different-types-of-ip-addresses-i-can-assign-toovms"></a>Quali sono hello diversi tipi di indirizzi IP è possibile assegnare tooVMs?
* **Privato:** assegnato tooeach NIC all'interno di ogni macchina virtuale. indirizzo Hello viene assegnato tramite uno dei metodi statici o dinamici di hello. Gli indirizzi IP privati vengono assegnati da intervallo di hello specificato nelle impostazioni di hello subnet della rete virtuale. Le risorse distribuite tramite il modello di distribuzione classica hello vengono assegnate indirizzi IP privati, anche se non sono connessi tooa rete virtuale. Un indirizzo IP privato assegnato con hello metodo dinamico rimane assegnato tooa risorsa fino a quando non viene eliminata risorse hello (servizio Cloud o macchine virtuali gli slot di distribuzione). Un indirizzo IP privato assegnato con metodo dinamico hello può variare quando una macchina virtuale viene riavviata dopo già hello arrestato (deallocato). Un indirizzo IP privato assegnato con hello metodo statico rimane assegnati tooa risorsa fino a quando non hello risorsa viene eliminata. Se è necessario tooensure l'indirizzo IP privato di hello per una risorsa non cambia mai fino a quando non hello risorsa viene eliminata, assegnare un indirizzo IP privato con metodo statico hello.
* **Pubblico:** tooNICs facoltativamente assegnato collegato tooVMs distribuite tramite il modello di distribuzione del hello Azure Resource Manager. Hello indirizzo può essere assegnato con metodo di allocazione statica o dinamica hello. Tutte le macchine virtuali e servizi Cloud le istanze del ruolo distribuite tramite il modello di distribuzione classica hello esistono all'interno di un servizio cloud, che viene assegnato un *dinamica*, pubblica indirizzo IP virtuale (VIP). Facoltativamente, è possibile assegnare un indirizzo IP pubblico *statico*, detto [indirizzo IP riservato](virtual-networks-reserved-public-ip.md), come indirizzo VIP. È possibile assegnare tooindividual di indirizzi IP pubblici e istanze del ruolo di servizi Cloud o macchine virtuali distribuite tramite il modello di distribuzione classica hello. Questi sono detti [indirizzi IP pubblici a livello di istanza (ILPIP)](virtual-networks-instance-level-public-ip.md) e possono essere assegnati in modo dinamico.

### <a name="can-i-reserve-a-private-ip-address-for-a-vm-that-i-will-create-at-a-later-time"></a>È possibile riservare un indirizzo IP privato per una macchina virtuale che verrà creata in un secondo momento?
No. Non è possibile riservare un indirizzo IP privato. Se è disponibile un indirizzo IP privato sarà assegnato tooa macchina virtuale o istanza di ruolo dal server DHCP hello. Che VM possono o non possono essere hello quello che si desidera hello private IP indirizzo toobe assegnato a. È possibile, tuttavia, modificare hello indirizzo IP privato un già creata VM tooany disponibile indirizzo IP privato.

### <a name="do-private-ip-addresses-change-for-vms-in-a-vnet"></a>Gli indirizzi IP privati vengono modificati per le macchine virtuali in una rete virtuale?
Dipende. Un indirizzo IP privato dinamico rimane assegnato a una macchina virtuale finché questa non viene arrestata, ovvero deallocata, o eliminata. Un indirizzo IP privato statico rimane associato a una macchina virtuale finché questa non viene eliminata.

### <a name="can-i-manually-assign-ip-addresses-toonics-within-hello-vm-operating-system"></a>È possibile assegnare manualmente tooNICs gli indirizzi IP all'interno del sistema operativo VM hello?
Sì, ma non è consigliabile. Modificando manualmente l'indirizzo IP hello per una scheda di rete all'interno del sistema operativo della macchina virtuale potrebbe danneggiare toolosing connettività toohello VM se l'indirizzo IP hello assegnato tooa NIC all'interno di hello macchina virtuale di Azure sono stati toochange.

### <a name="what-happens-toomy-ip-addresses-if-i-stop-a-cloud-service-deployment-slot-or-shutdown-a-vm-from-within-hello-operating-system"></a>Gli indirizzi IP toomy cosa accade se arresta un slot di distribuzione del servizio Cloud o un arresto una macchina virtuale dal sistema operativo hello?
Niente. gli indirizzi IP Hello (VIP pubblico, pubblici e privati) rimangono slot di distribuzione del servizio cloud toohello assegnato o macchina virtuale. Gli indirizzi dinamici vengono rilasciati solo se la macchina virtuale viene arrestata, ovvero deallocata, o eliminata oppure se lo slot di distribuzione del servizio cloud viene eliminato. Facendo clic su hello **arrestare** pulsante per una macchina virtuale nel portale di Azure hello imposta tooStopped il relativo stato (deallocato). In questo caso, hello VM perderà l'indirizzo IP.

### <a name="can-i-move-vms-from-one-subnet-tooanother-subnet-in-a-vnet-without-re-deploying"></a>È possibile spostare le macchine virtuali da una subnet di tooanother subnet in una rete virtuale senza ripetere la distribuzione?
Sì. È possibile trovare ulteriori informazioni in hello [come toomove una macchina virtuale o il ruolo dell'istanza tooa diverse subnet](virtual-networks-move-vm-role-to-subnet.md) articolo.

### <a name="can-i-configure-a-static-mac-address-for-my-vm"></a>È possibile configurare un indirizzo MAC statico per la macchina virtuale?
No. Un indirizzo MAC non può essere configurato in modo statico.

### <a name="will-hello-mac-address-remain-hello-same-for-my-vm-once-it-has-been-created"></a>Hello indirizzo MAC rimarrà hello stesso per la macchina virtuale dopo averla creata?
Sì, hello indirizzo MAC rimarrà hello che uguali per una macchina virtuale distribuita tramite Gestione risorse di hello e modelli di distribuzione classica finché viene eliminato. In precedenza, hello indirizzo MAC è stato rilasciato se hello macchina virtuale è stata arrestata (deallocata), ma ora indirizzo MAC hello viene mantenuta anche quando hello macchina virtuale è in stato deallocato hello.

### <a name="can-i-connect-toohello-internet-from-a-vm-in-a-vnet"></a>È possibile connettersi toohello internet da una macchina virtuale in una rete virtuale?
Sì. Istanze del ruolo tutte le macchine virtuali e servizi Cloud distribuite all'interno di una rete virtuale possono connettersi toohello Internet.

## <a name="azure-services-that-connect-toovnets"></a>Servizi di Azure che si connettono tooVNets

### <a name="can-i-use-azure-app-service-web-apps-with-a-vnet"></a>È possibile usare le app Web del servizio app di Azure con una rete virtuale?
Sì. È possibile distribuire le app Web all'interno di una rete virtuale tramite un ambiente del servizio app. Tutte le app Web possono connettersi in modo sicuro e accedere alle risorse in una rete virtuale di Azure, se è stata configurata una connessione da punto a sito per la rete virtuale. Per ulteriori informazioni, vedere hello seguenti articoli:

* [Creare app Web in un ambiente del servizio app](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [Integrare un'app in una rete virtuale di Azure](../app-service-web/web-sites-integrate-with-vnet.md)
* [Utilizzo dell’integrazione della rete virtuale e delle connessioni ibride con app Web](../app-service-web/web-sites-integrate-with-vnet.md#hybrid-connections-and-app-service-environments)

### <a name="can-i-deploy-cloud-services-with-web-and-worker-roles-paas-in-a-vnet"></a>È possibile distribuire i servizi cloud con ruolo di lavoro e Web (PaaS) in una rete virtuale?
Sì. Facoltativamente, è possibile distribuire istanze del ruolo dei servizi cloud all'interno di reti virtuali. toodo in tal caso, specificare il nome di rete virtuale hello e mapping di ruolo/subnet hello nella sezione di configurazione di rete hello della configurazione del servizio. Non è necessario tooupdate i file binari.

### <a name="can-i-connect-a-virtual-machine-scale-set-vmss-tooa-vnet"></a>È possibile collegare un tooa impostare scala macchina virtuale (VMSS) tra reti virtuali?
Sì. È necessario connettersi a una rete virtuale di tooa VMSS.

### <a name="can-i-move-my-services-in-and-out-of-vnets"></a>È possibile spostare i servizi all’interno e all’esterno delle reti virtuali?
No. Non è possibile spostare i servizi all'interno e all'esterno delle reti virtuali. Si verrà hanno toodelete e distribuire di nuovo toomove servizio hello è tooanother rete virtuale.

## <a name="security"></a>Sicurezza

### <a name="what-is-hello-security-model-for-vnets"></a>Che cos'è il modello di sicurezza hello per le reti virtuali?
Le reti virtuali sono completamente isolate una da altra e altri servizi ospitati in hello dell'infrastruttura di Azure. Una rete virtuale è un limite di attendibilità.

### <a name="can-i-restrict-inbound-or-outbound-traffic-flow-toovnet-connected-resources"></a>È possibile limitare le risorse connesso tooVNet del flusso di traffico in ingresso o in uscita?
Sì. È possibile applicare [gruppi di sicurezza di rete](virtual-networks-nsg.md) tooindividual subnet all'interno di una rete virtuale, le schede NIC associata tooa rete virtuale, o entrambi.

### <a name="can-i-implement-a-firewall-between-vnet-connected-resources"></a>È possibile implementare un firewall tra le risorse connesse alla rete virtuale?
Sì. È possibile distribuire un [appliance virtuale di rete firewall](https://azure.microsoft.com/en-us/marketplace/?term=firewall) da diversi fornitori tramite hello Azure Marketplace.

### <a name="is-there-information-available-about-securing-vnets"></a>Sono disponibili informazioni sulla protezione di reti virtuali?
Sì. Vedere hello [Cenni preliminari sulla sicurezza di rete di Azure](../security/security-network-overview.md) articolo per informazioni dettagliate.

## <a name="apis-schemas-and-tools"></a>API, schemi e strumenti

### <a name="can-i-manage-vnets-from-code"></a>È possibile gestire le reti virtuali dal codice?
Sì. È possibile utilizzare le API REST per le reti virtuali in hello [Azure Resource Manager](https://msdn.microsoft.com/library/mt163658.aspx) e [classica (servizio di gestione)](http://go.microsoft.com/fwlink/?LinkId=296833)) i modelli di distribuzione.

### <a name="is-there-tooling-support-for-vnets"></a>È disponibile il supporto degli strumenti per le reti virtuali?
Sì. Altre informazioni:
- Hello toodeploy portale Azure reti virtuali tramite hello [Azure Resource Manager](virtual-networks-create-vnet-arm-pportal.md) e [classico](virtual-networks-create-vnet-classic-pportal.md) modelli di distribuzione.
- PowerShell toomanage reti virtuali distribuite tramite hello [Gestione risorse](/powershell/resourcemanager/azurerm.network/v3.1.0/azurerm.network.md) e [classico](/powershell/module/azure/?view=azuresmps-3.7.0) modelli di distribuzione.
- Hello [Azure interfaccia della riga di comando (CLI)](../virtual-machines/azure-cli-arm-commands.md#azure-network-commands-to-manage-network-resources) toomanage reti virtuali distribuite tramite entrambi i modelli di distribuzione.  
