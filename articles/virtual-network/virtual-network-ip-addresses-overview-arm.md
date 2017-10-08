---
title: tipi di indirizzi aaaIP in Azure | Documenti Microsoft
description: Informazioni sugli indirizzi IP pubblici e privati in Azure.
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-resource-manager
ms.assetid: 610b911c-f358-4cfe-ad82-8b61b87c3b7e
ms.service: virtual-network
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.openlocfilehash: 402d3707c00f0b3bf3ef1febd5ade66223da74bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="ip-address-types-and-allocation-methods-in-azure"></a>Tipi di indirizzi IP e metodi di allocazione in Azure
È possibile assegnare gli indirizzi IP di tooAzure il toocommunicate risorse con altre risorse di Azure, la rete locale e hello Internet. In Azure è possibile usare due tipi di indirizzi IP:

* **Gli indirizzi IP pubblici**: utilizzato per la comunicazione con Internet, inclusi i servizi di Azure pubblico hello
* **Gli indirizzi IP privati**: utilizzato per la comunicazione all'interno di una rete virtuale di Azure (VNet) e di rete locale quando si utilizza un gateway VPN o tooextend circuito ExpressRoute tooAzure la rete.

> [!NOTE]
> Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../resource-manager-deployment-model.md).  In questo articolo viene illustrato l'utilizzo modello di distribuzione di gestione delle risorse hello, si consiglia di per la maggior parte delle nuove distribuzioni anziché hello [modello di distribuzione classica](virtual-network-ip-addresses-overview-classic.md).
> 

Se si ha familiarità con il modello di distribuzione classica hello, controllare hello [differenze IP addressing tra classico e Gestione risorse](virtual-network-ip-addresses-overview-classic.md#differences-between-resource-manager-and-classic-deployments).

## <a name="public-ip-addresses"></a>Indirizzi IP pubblici
Gli indirizzi IP pubblici consentono toocommunicate risorse di Azure con Internet e Azure servizi pubblici, ad esempio [Cache Redis di Azure](https://azure.microsoft.com/services/cache/), [hub eventi di Azure](https://azure.microsoft.com/services/event-hubs/), [database SQL](../sql-database/sql-database-technical-overview.md), e [archiviazione di Azure](../storage/common/storage-introduction.md).

In Gestione risorse di Azure un [indirizzo IP pubblico](resource-groups-networking.md#public-ip-address) è una risorsa che ha proprietà specifiche. È possibile associare una risorsa di indirizzo IP pubblica a una delle seguenti risorse hello:

* Macchine virtuali (VM)
* Servizi di bilanciamento del carico con connessione Internet
* Gateway VPN
* Gateway di applicazione

### <a name="allocation-method"></a>Metodo di allocazione
Esistono due metodi in cui un indirizzo IP viene allocato tooa *pubblica* risorsa IP - *dinamica* o *statico*. metodo di allocazione predefinito Hello è *dinamica*, dove un indirizzo IP è **non** allocato in fase di hello della creazione. Indirizzo IP pubblico hello, invece, viene allocato quando si avvia (o creare) risorse hello associato (ad esempio, un bilanciamento del carico o di macchina virtuale). indirizzo IP Hello viene rilasciata quando si arresta (o eliminare) la risorsa hello. In questo modo toochange indirizzo IP di hello quando si arresta e avvia una risorsa.

indirizzo IP di hello tooensure hello stesso per rimangono hello risorse associate, è possibile impostare il metodo di allocazione hello in modo esplicito troppo*statico*. In questo caso un indirizzo IP viene assegnato immediatamente. Viene rilasciata solo quando si elimina la risorsa hello o si modifica il relativo metodo di allocazione troppo*dinamica*.

> [!NOTE]
> Anche quando si imposta il metodo di allocazione hello troppo*statico*, non è possibile specificare hello effettivo IP indirizzo assegnato toohello *risorsa IP pubblica*. Al contrario, si ottiene allocato da un pool di indirizzi IP disponibili nella località di Azure hello risorse hello viene creata.
>

Indirizzi IP pubblici statici utilizzati frequentemente hello seguenti scenari:

* Gli utenti finali devono toocommunicate di regole firewall tooupdate con le risorse di Azure.
* La risoluzione del nome DNS, in cui una modifica dell'indirizzo IP richiederebbe l'aggiornamento dei record A.
* Le risorse di Azure comunicano con altri servizi o altre app che usano il modello di sicurezza basato su indirizzi IP.
* Utilizzare l'indirizzo IP tooan collegato i certificati SSL.

> [!NOTE]
> elenco Hello intervalli IP da cui gli indirizzi IP pubblici (dinamico o statico) tooAzure le risorse vengono allocati sia pubblicata nel [intervalli IP dei Data Center Azure](https://www.microsoft.com/download/details.aspx?id=41653).
>

### <a name="dns-hostname-resolution"></a>Risoluzione del nome host DNS
È possibile specificare un'etichetta di nome di dominio DNS per una risorsa IP pubblica, che consente di creare un mapping per *domainnamelabel*. *percorso*. cloudapp.azure.com toohello indirizzo IP pubblico nel server DNS gestito di Azure hello. Ad esempio, se si crea una risorsa IP pubblica con **contoso** come un *domainnamelabel* in hello **Stati Uniti occidentali** Azure *percorso*, hello il nome di dominio completo (FQDN) **contoso.westus.cloudapp.azure.com** risolverà l'indirizzo IP pubblico toohello della risorsa hello. È possibile utilizzare questo toocreate FQDN di un record CNAME di dominio personalizzato che punta a indirizzo IP pubblico toohello in Azure.

> [!IMPORTANT]
> Ogni etichetta di nome di dominio creata deve essere univoca nella relativa posizione di Azure.  
>

### <a name="virtual-machines"></a>Macchine virtuali
È possibile associare un indirizzo IP pubblico con un [Windows](../virtual-machines/windows/overview.md) o [Linux](../virtual-machines/virtual-machines-linux-about.md) VM tramite l'assegnazione tooits **interfaccia di rete**. Nel caso di hello di una macchina virtuale con più interfacce di rete, è possibile assegnarlo toohello *primario* solo l'interfaccia di rete. È possibile assegnare un statico pubblico IP indirizzo tooa VM o dinamico.

### <a name="internet-facing-load-balancers"></a>Servizi di bilanciamento del carico con connessione Internet
È possibile associare un indirizzo IP pubblico con un [bilanciamento del carico di Azure](../load-balancer/load-balancer-overview.md), assegnandole toohello bilanciamento del carico **front-end** configurazione. Questo indirizzo IP pubblico viene usato come indirizzo IP virtuale (VIP) di bilanciamento del carico. È possibile assegnare un dinamico o statico pubblico IP indirizzo tooa bilanciamento del carico front-end. È inoltre possibile assegnare più pubblica IP indirizzi tooa bilanciamento del carico front-end, che consente di [multi-VIP](../load-balancer/load-balancer-multivip.md) scenari come un ambiente multi-tenant con siti Web basati su SSL.

### <a name="vpn-gateways"></a>Gateway VPN
[Gateway VPN di Azure](../vpn-gateway/vpn-gateway-about-vpngateways.md) è tooconnect utilizzata una rete locale reti virtuali di Azure o tooan del tooother di rete virtuale di Azure (VNet). È necessario un tooits di indirizzo IP pubblico tooassign **configurazione IP** tooenable è toocommunicate con rete remota hello. Attualmente, è possibile assegnare solo un *dinamica* gateway VPN tooa con indirizzo IP pubblico.

### <a name="application-gateways"></a>Gateway di applicazione
È possibile associare un indirizzo IP pubblico di Azure [Gateway applicazione](../application-gateway/application-gateway-introduction.md), tramite l'assegnazione del gateway toohello **front-end** configurazione. Questo indirizzo IP pubblico viene usato come indirizzo VIP con carico bilanciato. Attualmente, è possibile assegnare solo un *dinamica* pubblica tooan applicazione gateway front-end configurazione degli indirizzi IP.

### <a name="at-a-glance"></a>Riepilogo
tabella Hello riportata di seguito mostra proprietà specifiche di hello attraverso il quale può essere un indirizzo IP pubblico associato tooa risorsa di primo livello e i metodi di allocazione possibili hello (statici o dinamici) che possono essere utilizzati.

| Risorse di livello superiore | Associazione di indirizzi IP | dinamico | statico |
| --- | --- | --- | --- |
| Macchine virtuali |interfaccia di rete |Sì |Sì |
| Bilanciamento del carico |Configurazione front-end |Sì |Sì |
| Gateway VPN |Configurazione IP del gateway |Sì |No |
| gateway applicazione |Configurazione front-end |Sì |No |

## <a name="private-ip-addresses"></a>Indirizzi IP privati
Gli indirizzi IP privati consentono toocommunicate risorse di Azure con le altre risorse in un [rete virtuale](virtual-networks-overview.md) o a una rete locale tramite un gateway VPN o un circuito ExpressRoute, senza utilizzare un indirizzo IP raggiungibile con Internet.

Nel modello di distribuzione Azure Resource Manager hello, un indirizzo IP privato è associato toohello seguenti tipi di risorse di Azure:

* VM
* Servizi di bilanciamento del carico interno
* Gateway di applicazione

### <a name="allocation-method"></a>Metodo di allocazione
Un indirizzo IP privato viene allocato dall'indirizzo hello è collegato l'intervallo di hello subnet toowhich hello risorsa. intervallo di indirizzi Hello della subnet hello stesso è una parte dell'intervallo di indirizzi della rete virtuale di hello.

Un indirizzo IP privato viene allocato con due metodi: *dinamico* o *statico*. metodo di allocazione predefinito Hello è *dinamica*, in cui l'indirizzo IP hello viene allocato automaticamente dalla subnet hello risorsa (tramite DHCP). Questo indirizzo IP può cambiare quando si arresta e avvia una risorsa hello.

È possibile impostare il metodo di allocazione hello troppo*statico* tooensure hello IP indirizzo rimane hello stesso. In questo caso, è necessario anche un indirizzo IP valido che fa parte della subnet della risorsa hello tooprovide.

Gli indirizzi IP privati statici vengono comunemente usati per:

* Macchine virtuali che fungono da controller di dominio o server DNS.
* Risorse che richiedono regole del firewall basate su indirizzi IP.
* Risorse accessibili da altre app o risorse tramite un indirizzo IP.

### <a name="virtual-machines"></a>Macchine virtuali
Un indirizzo IP privato è assegnato toohello **interfaccia di rete** di un [Windows](../virtual-machines/windows/overview.md) o [Linux](../virtual-machines/virtual-machines-linux-about.md) macchina virtuale. Nel caso di una macchina virtuale con più interfacce di rete, a ogni interfaccia viene assegnato un indirizzo IP privato. È possibile specificare il metodo di allocazione hello come dinamico o statico per un'interfaccia di rete.

#### <a name="internal-dns-hostname-resolution-for-vms"></a>Risoluzione del nome host DNS interno per le macchine virtuali
Tutte le macchine virtuali di Azure sono configurate con [server DNS gestiti da Azure](virtual-networks-name-resolution-for-vms-and-role-instances.md#azure-provided-name-resolution) per impostazione predefinita, a meno che non si configurino in modo esplicito server DNS personalizzati. Questi server DNS forniscono la risoluzione dei nomi interna per le macchine virtuali che risiedono all'interno di hello stessa rete virtuale.

Quando si crea una macchina virtuale, un mapping per l'indirizzo IP privato di hello hostname tooits viene aggiunto toohello i server DNS gestito di Azure. In caso di un'interfaccia di multi-rete VM, viene eseguito il mapping di hello hostname indirizzo IP privato toohello hello principale dell'interfaccia di rete.

Macchine virtuali configurate con i server DNS gestito di Azure sarà in grado di tooresolve hello hostnames di tutte le macchine virtuali all'interno gli indirizzi IP privati tootheir di rete virtuale.

### <a name="internal-load-balancers-ilb--application-gateways"></a>Servizi di bilanciamento del carico interno e gateway applicazione
È possibile assegnare un toohello di indirizzo IP privato **front-end** configurazione di un [bilanciamento del carico interno Azure](../load-balancer/load-balancer-internal-overview.md) (ILB) o un [Gateway applicazione Azure](../application-gateway/application-gateway-introduction.md). Questo indirizzo IP privato funge da un endpoint interno, accessibile solo toohello risorse di rete virtuale (VNet) e reti remote hello connessi toohello rete virtuale. È possibile assegnare sia una dinamica o statica privato toohello front-end configurazione degli indirizzi IP.

### <a name="at-a-glance"></a>Riepilogo
tabella Hello riportata di seguito mostra proprietà specifiche di hello attraverso il quale può essere un indirizzo IP privato tooa associato risorsa di primo livello e i metodi di allocazione possibili hello (statici o dinamici) che possono essere utilizzati.

| Risorse di livello superiore | Associazione di indirizzi IP | dinamico | statico |
| --- | --- | --- | --- |
| Macchine virtuali |interfaccia di rete |Sì |Sì |
| Bilanciamento del carico |Configurazione front-end |Sì |Sì |
| gateway applicazione |Configurazione front-end |Sì |Sì |

## <a name="limits"></a>Limiti
Hello limiti imposti su indirizzi IP sono indicati in set completo di hello di [limiti per la rete](../azure-subscription-service-limits.md#networking-limits) in Azure. Questi limiti sono classificati per area e per sottoscrizione. È possibile [contattare il supporto tecnico](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade) limiti predefiniti di hello tooincrease dei limiti massimi di toohello in base alle esigenze aziendali.

## <a name="pricing"></a>Prezzi
Per gli indirizzi IP pubblici può essere previsto un addebito nominale. toolearn più sull'indirizzo IP indirizzo prezzi di Azure, revisione hello [dei prezzi di indirizzo IP](https://azure.microsoft.com/pricing/details/ip-addresses) pagina.

## <a name="next-steps"></a>Passaggi successivi
* [Distribuire una macchina virtuale con un indirizzo IP pubblico statico utilizzando hello portale di Azure](virtual-network-deploy-static-pip-arm-portal.md)
* [Distribuire una VM con un IP pubblico statico tramite un modello](virtual-network-deploy-static-pip-arm-template.md)
* [Distribuire una macchina virtuale con un indirizzo IP privato statico utilizzando hello portale di Azure](virtual-networks-static-private-ip-arm-pportal.md)
