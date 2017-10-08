---
title: tipi di indirizzi aaaIP in Azure (versione classica) | Documenti Microsoft
description: Informazioni sugli indirizzi IP pubblici e privati (classici) in Azure.
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: 2f8664ab-2daf-43fa-bbeb-be9773efc978
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/11/2016
ms.author: jdial
ms.openlocfilehash: 7e09a5ad5b5f2d55329152b5d843de3c4455d1b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="ip-address-types-and-allocation-methods-classic-in-azure"></a>Tipi di indirizzi IP e metodi di allocazione (modello di distribuzione classica) in Azure
È possibile assegnare gli indirizzi IP di tooAzure il toocommunicate risorse con altre risorse di Azure, la rete locale e hello Internet. Sono disponibili due tipi di indirizzi IP che è possibile usare in Azure: pubblici e privati.

Gli indirizzi IP pubblici utilizzati per la comunicazione con Internet, inclusi i servizi di Azure pubblico hello.

Quando si utilizza un gateway VPN o tooextend circuito ExpressRoute tooAzure la rete, gli indirizzi IP privati vengono utilizzati per la comunicazione all'interno di una rete virtuale di Azure (VNet), un servizio cloud e la rete locale.

> [!IMPORTANT]
> Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../resource-manager-deployment-model.md).  In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Microsoft consiglia di usare Resource Manager per la maggior parte delle distribuzioni più recenti. Informazioni sugli indirizzi IP in Gestione risorse per la lettura hello [gli indirizzi IP](virtual-network-ip-addresses-overview-arm.md) articolo.

## <a name="public-ip-addresses"></a>Indirizzi IP pubblici
Gli indirizzi IP pubblici consentono toocommunicate risorse di Azure con Internet e Azure servizi pubblici, ad esempio [Cache Redis di Azure](https://azure.microsoft.com/services/cache/), [hub eventi di Azure](https://azure.microsoft.com/services/event-hubs/), [database SQL](../sql-database/sql-database-technical-overview.md), e [archiviazione di Azure](../storage/common/storage-introduction.md).

Un indirizzo IP pubblico è associato con i seguenti tipi di risorsa hello:

* Servizi cloud
* Macchine virtuali IaaS
* Istanze del ruolo PaaS
* Gateway VPN
* Gateway di applicazione

### <a name="allocation-method"></a>Metodo di allocazione
Quando un indirizzo IP pubblico deve toobe assegnato tooan risorse di Azure, è *dinamicamente* allocata da un pool di IP pubblici disponibili indirizzo all'interno delle risorse di hello hello posizione viene creato. Questo indirizzo IP viene rilasciato quando risorse hello sono stata arrestata. In caso di un servizio cloud, ciò si verifica quando vengono arrestate tutte le istanze di ruolo hello, che può essere evitata utilizzando un *statico* indirizzo IP (riservato) (vedere [servizi Cloud](#Cloud-services)).

> [!NOTE]
> elenco Hello intervalli IP da cui gli indirizzi IP pubblici tooAzure le risorse vengono allocati sia pubblicata nel [intervalli IP dei Data Center Azure](https://www.microsoft.com/download/details.aspx?id=41653).
> 
> 

### <a name="dns-hostname-resolution"></a>Risoluzione del nome host DNS
Quando si crea un servizio cloud o in una VM IaaS, è necessario tooprovide un nome DNS del servizio cloud che è univoco tra tutte le risorse in Azure. Verrà creato un mapping in hello server DNS gestito di Azure per *dnsname*. cloudapp.net toohello indirizzo IP pubblico della risorsa hello. Ad esempio, quando si crea un servizio cloud con un nome DNS del servizio cloud di **contoso**, il nome di dominio completo hello (FQDN) **contoso.cloudapp.net** risolverà l'indirizzo IP pubblico (VIP) di tooa di servizio cloud Hello. È possibile utilizzare questo toocreate FQDN di un record CNAME di dominio personalizzato che punta a indirizzo IP pubblico toohello in Azure.

### <a name="cloud-services"></a>Servizi cloud
Un servizio cloud ha sempre un indirizzo IP pubblico indirizzo a cui viene fatto riferimento tooas un indirizzo IP virtuale (VIP). È possibile creare endpoint in un cloud servizio tooassociate diverse porte hello VIP toointernal porte di macchine virtuali e istanze del ruolo all'interno del servizio cloud hello. 

Un servizio cloud può contenere più macchine virtuali IaaS, o istanze del ruolo PaaS, tutti esposte tramite hello stesso VIP di servizio cloud. È inoltre possibile assegnare [servizio cloud di più indirizzi VIP tooa](../load-balancer/load-balancer-multivip.md), che consente scenari multi-VIP come ambiente multi-tenant con siti Web basati su SSL.

È possibile verificare l'indirizzo IP pubblico hello di un servizio cloud rimane hello stesso, anche quando tutte le istanze del ruolo di hello vengono arrestati, utilizzando un *statico* indirizzo IP pubblico, di cui viene fatto riferimento tooas [IP riservato](virtual-networks-reserved-public-ip.md). È possibile creare una risorsa IP statica (riservata) in una posizione specifica e assegnarlo tooany di servizio cloud in tale percorso. Non è possibile specificare l'indirizzo IP effettivo hello per l'IP riservato hello, viene allocato dal pool di indirizzi IP disponibili nel percorso di hello che viene creato. Questo indirizzo IP non viene rilasciato finché non viene eliminato esplicitamente.

(Riservato) pubblici indirizzi IP statici sono comunemente usati negli scenari di hello in cui un servizio cloud:

* richiede l'installazione di toobe regole firewall dagli utenti finali.
* dipende dalla risoluzione del nome DNS esterno, e un indirizzo IP dinamico richiederebbe l'aggiornamento dei record A.
* utilizza i servizi Web esterni che usano il modello di sicurezza basato su IP.
* Usa l'indirizzo IP tooan collegato i certificati SSL.

> [!NOTE]
> Quando si crea una VM classica, Azure crea un *servizio cloud* contenitore con un indirizzo IP virtuale (VIP). Quando ha completata la creazione di hello tramite il portale, valore predefinito è RDP o SSH *endpoint* per portale hello è configurato per la connessione toohello macchina virtuale tramite VIP di servizio cloud hello. È possibile riservare il VIP di servizio cloud che fornisce in modo efficace un toohello di tooconnect indirizzo VM IP riservato. È possibile aprire porte aggiuntive tramite la configurazione di più endpoint.
> 
> 

### <a name="iaas-vms-and-paas-role-instances"></a>Istanze del ruolo PaaS e delle macchine virtuali IaaS
È possibile assegnare a un pubblico di indirizzi IP direttamente tooan IaaS [VM](../virtual-machines/virtual-machines-linux-about.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o istanza del ruolo PaaS all'interno di un servizio cloud. Si tratta di cui viene fatto riferimento tooas un indirizzo IP pubblico a livello di istanza ([ILPIP](virtual-networks-instance-level-public-ip.md)). Questo indirizzo IP pubblico può essere solo dinamico.

> [!NOTE]
> Questo comportamento è diverso da hello VIP di servizio cloud hello, che è un contenitore per le macchine virtuali IaaS o PaaS istanze del ruolo, poiché un servizio cloud può contenere più macchine virtuali IaaS, o istanze del ruolo PaaS, tutti esposte tramite hello stessa VIP di servizio.
> 
> 

### <a name="vpn-gateways"></a>Gateway VPN
Oggetto [gateway VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md) possono essere utilizzati tooconnect tooother una rete virtuale di Azure reti di reti virtuali di Azure o in locale. Un gateway VPN viene assegnato un indirizzo IP pubblico *dinamicamente*, che consente la comunicazione con la rete remota hello.

### <a name="application-gateways"></a>Gateway di applicazione
Un Azure [gateway applicazione](../application-gateway/application-gateway-introduction.md) può essere utilizzato per Layer7 bilanciamento del carico del traffico di rete tooroute basato su HTTP. Gateway applicazione viene assegnato un indirizzo IP pubblico *dinamicamente*, che funge da hello VIP con bilanciamento del carico.

### <a name="at-a-glance"></a>Riepilogo
tabella Hello riportata di seguito viene illustrato ogni tipo di risorsa con metodi di allocazione possibili hello (dinamico o statico) e possibilità tooassign più indirizzi IP pubblici.

| Risorsa | Dinamico | statico | Più indirizzi IP |
| --- | --- | --- | --- |
| servizio cloud |Sì |Sì |Sì |
| Istanza del ruolo PaaS o della macchine virtuale IaaS |Sì |No |No |
| gateway VPN |Sì |No |No |
| gateway applicazione |Sì |No |No |

## <a name="private-ip-addresses"></a>Indirizzi IP privati
Gli indirizzi IP privati consentono toocommunicate risorse di Azure con altre risorse in un servizio cloud o un [rete virtuale](virtual-networks-overview.md)(VNet), o di rete locale tooon (tramite un gateway VPN o un circuito ExpressRoute), senza utilizzare un Indirizzo IP raggiungibile con Internet.

Nel modello di distribuzione classico di Azure, un indirizzo IP privato può essere assegnato toohello seguendo le risorse di Azure:

* Istanze del ruolo PaaS e delle macchine virtuali IaaS
* Servizio di bilanciamento del carico interno
* gateway applicazione

### <a name="iaas-vms-and-paas-role-instances"></a>Istanze del ruolo PaaS e delle macchine virtuali IaaS
Macchine virtuali (VM) create con il modello di distribuzione classica hello sono sempre incluse in un servizio cloud, le istanze del ruolo tooPaaS simile. comportamento di Hello di indirizzi IP privati sono pertanto simili per tali risorse.

È importante toonote che può essere un servizio cloud distribuito in due modi:

* Come un servizio cloud *autonomo* , non incluso in una rete virtuale.
* Come parte di una rete virtuale.

#### <a name="allocation-method"></a>Metodo di allocazione
In caso di un *autonomo* servizio cloud, allocare un indirizzo IP privato get di risorse *dinamicamente* intervallo di indirizzi IP privati di hello Data Center di Azure. E può essere utilizzato solo per le comunicazioni con altre macchine virtuali all'interno di hello stesso servizio cloud. Questo indirizzo IP può cambiare quando la risorsa hello viene arrestata e avviata.

In caso di un servizio cloud distribuito in una rete virtuale, le risorse ottenere private alcun indirizzo IP allocato dall'intervallo di indirizzi hello di hello associati subnet (come specificato nella configurazione di rete). Questo indirizzo IP privato è utilizzabile per la comunicazione tra tutte le macchine virtuali all'interno di hello rete virtuale.

Inoltre, nel caso dei servizi cloud all'interno di una rete virtuale, viene allocato *dinamicamente* un indirizzo IP privato (tramite DHCP) per impostazione predefinita. È possibile modificare quando risorse hello vengano arrestata e avviata. tooensure hello IP indirizzo rimane hello stesso, è necessario il metodo di allocazione hello tooset troppo*statico*e fornire un indirizzo IP nell'intervallo di indirizzi corrispondente hello.

Gli indirizzi IP privati statici vengono comunemente usati per:

* Macchine virtuali che fungono da controller di dominio o server DNS.
* Macchine virtuali che richiedono regole firewall basate su indirizzi IP.
* Macchine virtuali che eseguono servizi accessibili da altre applicazioni tramite un indirizzo IP.

#### <a name="internal-dns-hostname-resolution"></a>Risoluzione del nome host DNS interno
Tutte le istanze del ruolo PaaS e delle macchine virtuali Azure sono configurate con [server DNS gestiti da Azure](virtual-networks-name-resolution-for-vms-and-role-instances.md#azure-provided-name-resolution) per impostazione predefinita, a meno che non si configurano in modo esplicito server DNS personalizzati. Questi server DNS forniscono la risoluzione dei nomi interna per le macchine virtuali e istanze del ruolo che si trovano all'interno di hello stesso rete virtuale o un servizio cloud.

Quando si crea una macchina virtuale, un mapping per l'indirizzo IP privato di hello hostname tooits viene aggiunto toohello i server DNS gestito di Azure. In caso di una macchina virtuale multi-NIC, viene eseguito il mapping di hello hostname toohello indirizzo IP privato della hello di rete primaria. Tuttavia, queste informazioni di mapping sono tooresources limitate all'interno di hello stesso servizio cloud o rete virtuale.

In caso di un *autonomo* servizio cloud, sarà possibile i nomi host in grado di tooresolve di tutte le istanze di macchine virtuali o il ruolo all'interno di hello stesso cloud solo servizio. In caso di un servizio cloud all'interno di una rete virtuale, sarà in grado di tooresolve nomi host di tutte le istanze di macchine virtuali o il ruolo di hello all'interno di hello rete virtuale.

### <a name="internal-load-balancers-ilb--application-gateways"></a>Servizi di bilanciamento del carico interno e gateway applicazione
È possibile assegnare un toohello di indirizzo IP privato **front-end** configurazione di un [bilanciamento del carico interno Azure](../load-balancer/load-balancer-internal-overview.md) (ILB) o un [Gateway applicazione Azure](../application-gateway/application-gateway-introduction.md). Questo indirizzo IP privato funge da un endpoint interno, accessibile solo toohello risorse di rete virtuale (VNet) e reti remote hello connessi toohello rete virtuale. È possibile assegnare sia una dinamica o statica privato toohello front-end configurazione degli indirizzi IP. È inoltre possibile assegnare più private IP indirizzi tooenable multi-vip scenari.

### <a name="at-a-glance"></a>Riepilogo
tabella Hello riportata di seguito viene illustrato ogni tipo di risorsa con metodi di allocazione possibili hello (dinamico o statico) e possibilità tooassign più indirizzi IP privati.

| Risorsa | Dinamico | statico | Più indirizzi IP |
| --- | --- | --- | --- |
| Macchine virtuali (in un servizio cloud *autonomo* ) |Sì |Sì |Sì |
| Istanza del ruolo PaaS (in un servizio cloud *autonomo* ) |Sì |No |Sì |
| Istanza del ruolo PaaS o della macchina virtuale (in una VNet) |Sì |Sì |Sì |
| Front-end del servizio di bilanciamento del carico interno |Sì |Sì |Sì |
| Front-end del gateway applicazione |Sì |Sì |Sì |

## <a name="limits"></a>Limiti
Hello tabella seguente vengono indicati i limiti di hello imposti a IP addressing in Azure per ogni sottoscrizione. È possibile [contattare il supporto tecnico](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade) limiti predefiniti di hello tooincrease dei limiti massimi di toohello in base alle esigenze aziendali.

|  | Limite predefinito | Limite massimo |
| --- | --- | --- |
| Indirizzi IP pubblici (dinamici) |5 |contattare il supporto tecnico |
| Indirizzi IP pubblici riservati. |20 |contattare il supporto tecnico |
| Indirizzo VIP pubblico per distribuzione (servizio cloud) |5 |contattare il supporto tecnico |
| Indirizzo VIP privato (ILB) per distribuzione (servizio cloud) |1 |1 |

Assicurarsi di leggere il set completo di hello di [limiti per la rete](../azure-subscription-service-limits.md#networking-limits) in Azure.

## <a name="pricing"></a>Prezzi
Nella maggior parte dei casi, gli indirizzi IP pubblici sono gratuiti. È presente una tariffa nominale toouse statici e/o ulteriori indirizzi IP pubblici. È importante comprendere hello [struttura dei prezzi per gli indirizzi IP pubblici](https://azure.microsoft.com/pricing/details/ip-addresses/).

## <a name="differences-between-resource-manager-and-classic-deployments"></a>Differenze tra le distribuzioni di Gestione risorse e le distribuzioni classiche
Di seguito è un confronto delle funzionalità di indirizzamento IP in Gestione risorse e il modello di distribuzione classica hello.

|  | Risorsa | Classico | Gestione risorse |
| --- | --- | --- | --- |
| **Indirizzo IP pubblico** |***VM*** |Tooas di cui si fa riferimento un ILPIP (solo dinamico) |Tooas di cui un indirizzo IP pubblico (statica o dinamica) |
|  ||Tooan assegnato VM IaaS o un'istanza del ruolo PaaS |Scheda di rete della macchina virtuale toohello associato | |
|  |***Servizio di bilanciamento del carico con connessione Internet*** |Cui tooas VIP (dinamico) o l'indirizzo IP riservato (statico) |Tooas di cui un indirizzo IP pubblico (statica o dinamica) | |
|  ||Servizio cloud tooa assegnato |Configurazione front-end del servizio di bilanciamento di carico toohello associato | |
|  | | | |
| **Indirizzo IP privato** |***VM*** |Tooas di cui si fa riferimento un DIP |Cui tooas un indirizzo IP privato |
|  ||Tooan assegnato VM IaaS o un'istanza del ruolo PaaS |Scheda di rete della macchina virtuale assegnato toohello | |
|  |***Servizio di bilanciamento del carico interno*** |Assegnato toohello bilanciamento del carico interno (statica o dinamica) |Configurazione di front-end di ILB toohello assegnato (statica o dinamica) | |

## <a name="next-steps"></a>Passaggi successivi
* [Distribuire una macchina virtuale con un indirizzo IP privato statico](virtual-networks-static-private-ip-classic-pportal.md) utilizzando hello portale di Azure.

