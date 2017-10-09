---
title: aaaVirtual reti e macchine virtuali Windows in Azure | Documenti Microsoft
description: "Informazioni sulle funzionalità di rete in relazione toohello nozioni fondamentali sulla creazione di macchine virtuali di Windows in Azure."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 5493e9f7-7d45-4e98-be9a-657a53708746
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: e28a4782f9f6c69f6101e45dbb560ccd694a1e07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-networks-and-windows-virtual-machines-in-azure"></a>Reti virtuali e macchine virtuali Windows in Azure 

Quando si crea una macchina virtuale (VM) di Azure, è necessario creare una [rete virtuale](../../virtual-network/virtual-networks-overview.md) o usarne una esistente. È inoltre necessario toodecide come le macchine virtuali sono previsti toobe accede hello rete virtuale. È importante troppo[piano prima di creare risorse](../../virtual-network/virtual-network-vnet-plan-design-arm.md) e assicurarsi di aver compreso hello [limiti delle risorse di rete](../../azure-subscription-service-limits.md#networking-limits).

Nella seguente illustrazione di hello, le macchine virtuali vengono rappresentate come server web e server di database. Ogni set di macchine virtuali vengono assegnati a subnet tooseparate hello rete virtuale.

![rete virtuale di Azure](./media/network-overview/vnetoverview.png)

È possibile creare una rete virtuale prima di creare una macchina virtuale oppure è possibile creare reti virtuali hello durante la creazione di una macchina virtuale. La rete virtuale viene creata dall'utente oppure automaticamente quando si crea una VM.

Creare queste risorse toosupport comunicazione con una macchina virtuale:

- Interfacce di rete
- Indirizzi IP
- Rete virtuale e subnet

Inoltre toothose risorse di base, è opportuno anche considerare queste risorse facoltative:

- Gruppi di sicurezza di rete
- Servizi di bilanciamento del carico 

## <a name="network-interfaces"></a>Interfacce di rete

Oggetto [interfaccia di rete (NIC)](../../virtual-network/virtual-network-network-interface.md) è interconnessione hello tra una macchina virtuale e una rete virtuale (VNet). Una macchina virtuale deve avere almeno una scheda di rete, ma può avere più di uno, a seconda delle dimensioni di hello di hello macchina virtuale creata. Per informazioni sul numero di interfacce di rete supportate a seconda delle dimensioni della VM, vedere [Dimensioni delle macchine virtuali in Azure](sizes.md). 

Se si desidera toocreate una macchina virtuale con più di una scheda di rete, è necessario creare hello VM con almeno due.  Dopo la creazione è possibile aggiungere schede aggiuntive toohello numero supportato dalle dimensioni VM hello, ma non è possibile aggiungere altre schede di rete tooa VM solo creato con uno, indipendentemente dal numero di schede di rete supporta hello dimensioni della macchina virtuale. 

Se hello VM viene aggiunto il set di disponibilità tooan, tutte le macchine virtuali all'interno di set di disponibilità hello devono avere uno o più schede di rete. Le macchine virtuali con più di una scheda di rete non sono obbligatorie toohave hello stesso numero di schede di rete, ma devono tutti avere almeno due.

Ogni tooa NIC associata deve essere presente nella macchina virtuale hello stessa posizione e una sottoscrizione come hello macchina virtuale. Ogni scheda di rete deve essere connesso tooa rete virtuale presente in hello stessa località di Azure e di sottoscrizione come hello scheda di rete. Dopo la creazione di una scheda di rete, è possibile modificare la subnet hello a che è connesso, ma non è possibile modificare hello rete virtuale è connessa a.  Ogni scheda NIC associata tooa che macchina virtuale viene assegnato un indirizzo MAC che non cambia finché non viene eliminato hello macchina virtuale.

Questa tabella elenca i metodi di hello che è possibile utilizzare toocreate un'interfaccia di rete.

| Metodo | Description |
| ------ | ----------- |
| Portale di Azure | Quando si crea una macchina virtuale nel portale di Azure hello, un'interfaccia di rete viene creata automaticamente per l'utente (non è possibile utilizzare una scheda di rete creare separatamente). portale Hello crea una macchina virtuale con una sola scheda di rete. Se si desidera toocreate una macchina virtuale con più di una scheda di rete, è necessario crearlo con un metodo diverso. |
| [Azure PowerShell](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) | Utilizzare [New AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) con hello **- PublicIpAddressId** identificatore hello tooprovide di parametro dell'indirizzo IP pubblico hello creato in precedenza. |
| [Interfaccia della riga di comando di Azure](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md) | Identificatore hello tooprovide dell'indirizzo IP pubblico hello indirizzi che si utilizzo creato in precedenza, [az rete nic creare](https://docs.microsoft.com/cli/azure/network/nic#create) con hello **-indirizzo ip pubblico** parametro. |
| [Modello](../../virtual-network/virtual-network-deploy-multinic-arm-template.md) | Vedere [Network Interface in a Virtual Network with Public IP Address](https://github.com/Azure/azure-quickstart-templates/tree/master/101-nic-publicip-dns-vnet) (Interfaccia di rete in una rete virtuale con indirizzo IP pubblico) per istruzioni sulla distribuzione di un'interfaccia di rete con un modello. |

## <a name="ip-addresses"></a>Indirizzi IP 

È possibile assegnare questi tipi di [gli indirizzi IP](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) tooa NIC in Azure:

- **Gli indirizzi IP pubblici** -toocommunicate in ingresso e in uscita (senza conversione indirizzi di rete (NAT)) utilizzato con hello Internet e altre risorse di Azure non è connesso tooa rete virtuale. L'assegnazione di un tooa di indirizzo IP pubblico NIC è facoltativo. Per gli indirizzi IP pubblici è previsto un addebito nominale ed è fissato un numero massimo per ogni sottoscrizione.
- **Gli indirizzi IP privati** : utilizzate per la comunicazione all'interno di una rete virtuale, la rete locale e hello Internet (con NAT). È necessario assegnare almeno un private IP indirizzo tooa macchina virtuale. toolearn ulteriori informazioni su NAT in Azure, leggere [informazioni sulle connessioni in uscita in Azure](../../load-balancer/load-balancer-outbound-connections.md).

È possibile assegnare tooVMs di indirizzi IP pubblici o servizi di bilanciamento del carico con connessione internet. È possibile assegnare tooVMs di indirizzi IP privati e servizi di bilanciamento del carico interno. Assegnare tooa gli indirizzi IP utilizzando un'interfaccia di rete VM.

Sono disponibili due metodi in cui un indirizzo IP viene allocato tooa risorse - dinamica o statica. metodo di allocazione predefinito Hello è dinamico, in cui non è possibile allocare un indirizzo IP quando viene creato. Al contrario, l'indirizzo IP hello viene allocato quando si crea una macchina virtuale o avvia una macchina virtuale arrestata. indirizzo IP Hello viene rilasciata quando si arresta o Elimina hello macchina virtuale. 

indirizzo IP di hello tooensure per macchina virtuale rimane hello hello stesso, è possibile impostare in modo esplicito il metodo di allocazione hello toostatic. In questo caso, un indirizzo IP viene assegnato immediatamente. Viene rilasciata solo quando si elimina hello VM o modificare il relativo toodynamic metodo di allocazione.
    
Questa tabella elenca i metodi di hello che è possibile utilizzare un indirizzo IP toocreate.

| Metodo | Descrizione |
| ------ | ----------- |
| [Portale di Azure](../../virtual-network/virtual-network-deploy-static-pip-arm-portal.md) | Per impostazione predefinita, gli indirizzi IP pubblici sono dinamici e possono cambiare hello indirizzo associato toothem hello macchina virtuale viene arrestata o eliminata. Usa tooguarantee che hello VM sempre hello stesso indirizzo IP pubblico, creare un indirizzo IP pubblico statico. Per impostazione predefinita, il portale di hello assegna un dinamica private IP indirizzo tooa NIC durante la creazione di una macchina virtuale. È possibile modificare questo toostatic dopo hello che viene creata la VM.|
| [Azure PowerShell](../../virtual-network/virtual-network-deploy-static-pip-arm-ps.md) | Utilizzare [New AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) con hello **- AllocationMethod** parametro come dinamico o statico. |
| [Interfaccia della riga di comando di Azure](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md) | Utilizzare [az rete public-ip creare](https://docs.microsoft.com/cli/azure/network/public-ip#create) con hello **-metodo di allocazione** parametro come dinamico o statico. |
| [Modello](../../virtual-network/virtual-network-deploy-static-pip-arm-template.md) | Vedere [Network Interface in a Virtual Network with Public IP Address](https://github.com/Azure/azure-quickstart-templates/tree/master/101-nic-publicip-dns-vnet) (Interfaccia di rete in una rete virtuale con indirizzo IP pubblico) per istruzioni sulla distribuzione di un indirizzo IP pubblico con un modello. |

Dopo aver creato un indirizzo IP pubblico, è possibile associarlo a una macchina virtuale tramite l'assegnazione tooa scheda di rete.

## <a name="virtual-network-and-subnets"></a>Rete virtuale e subnet

Una subnet è un intervallo di indirizzi IP nella rete virtuale hello. È possibile dividere la rete virtuale in più subnet per obiettivi di organizzazione e sicurezza. Ogni scheda di rete in una macchina virtuale è connessa tooone subnet in una rete virtuale. Schede di rete il toosubnets connesso (uguale o diverso) all'interno di una rete virtuale può comunicare tra loro senza alcuna configurazione aggiuntiva.

Quando si configura una rete virtuale, specificare la topologia hello, inclusi subnet e gli spazi di indirizzi disponibili hello. Se hello rete virtuale è tooother toobe connesso le reti in reti virtuali o locale, è necessario selezionare gli intervalli di indirizzi che non si sovrappongano. gli indirizzi IP Hello sono privati e non sono accessibili da Internet, è vero solo per indirizzi IP non routeable di hello quali 10.0.0.0/8, 172.16.0.0/12 o 192.168.0.0/16 hello. A questo punto, Azure considera qualsiasi intervallo di indirizzi come parte di hello privata VNet spazio degli indirizzi IP che è raggiungibile in rete virtuale, all'interno delle reti virtuali interconnesse e dal percorso di on-premise hello. 

Se si lavora in un'organizzazione in cui un altro utente è responsabile per le reti interne hello, è consigliabile consultare toothat persona prima di selezionare lo spazio degli indirizzi. Assicurarsi che non si verificano sovrapposizioni e informarli hello spazio toouse in modo non tentano toouse hello stesso intervallo di indirizzi IP. 

Per impostazione predefinita, non vi è alcun limite di sicurezza tra subnet, pertanto le macchine virtuali in ognuna di queste subnet possono comunicare con tooone un altro. Tuttavia, è possibile impostare rete sicurezza gruppi, che consentono di toocontrol hello traffico flusso tooand dalla subnet e tooand da macchine virtuali. 

Questa tabella elenca i metodi di hello che è possibile utilizzare toocreate una rete virtuale e le subnet.   

| Metodo | Descrizione |
| ------ | ----------- |
| [Portale di Azure](../../virtual-network/virtual-networks-create-vnet-arm-pportal.md) | Se si consente a Azure di creare una rete virtuale quando si crea una macchina virtuale, il nome di hello è una combinazione di nome gruppo di risorse hello contenente hello rete virtuale e **- vnet**. lo spazio degli indirizzi Hello è 10.0.0.0/24, nome subnet obbligatorio hello è **predefinito**, e l'intervallo di indirizzi subnet hello è 10.0.0.0/24. |
| [Azure PowerShell](../../virtual-network/virtual-networks-create-vnet-arm-ps.md) | Utilizzare [New AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmVirtualNetworkSubnetConfig) e [New AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmVirtualNetwork) toocreate una subnet e un rete virtuale. È inoltre possibile utilizzare [Aggiungi AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig) tooadd tooan una subnet rete virtuale esistente. |
| [Interfaccia della riga di comando di Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md) | Hello subnet e hello rete virtuale vengono creati nel hello stesso tempo. Fornire un **-subnet-name** parametro troppo[creazione della rete virtuale di rete az](https://docs.microsoft.com/cli/azure/network/vnet#create) con il nome di subnet hello. |
| [Modello](../../virtual-network/virtual-networks-create-vnet-arm-template-click.md) | Hello toocreate modo più semplice una rete virtuale e subnet è toodownload un modello esistente, ad esempio [rete virtuale con due subnet](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets)e modificarla in base alle esigenze. |

## <a name="network-security-groups"></a>Gruppi di sicurezza di rete

Oggetto [rete gruppo di sicurezza ()](../../virtual-network/virtual-networks-nsg.md) contiene un elenco di regole di elenco di controllo di accesso (ACL) che consentono o negano toosubnets il traffico di rete, schede di rete o entrambi. NSGs può essere associata a una subnet o singole schede di rete connessa tooa subnet. Quando un gruppo è associata a una subnet, hello ACL regole tooall hello macchine virtuali nella subnet. Inoltre, il traffico tooan singoli NIC può essere limitato mediante l'associazione di un gruppo direttamente tooa scheda di rete.

I gruppi di sicurezza di rete includono due tipi di regole: In ingresso e In uscita. priorità di Hello per una regola deve essere univoca all'interno di ogni set. Ogni regola ha proprietà di protocollo, intervalli di porte di origine e destinazione, prefissi degli indirizzi, direzione del traffico, priorità e tipo di accesso. 

Tutti i gruppi di sicurezza di rete contengono un set di regole predefinite. le regole predefinite di Hello non possono essere eliminate, ma poiché vengono assegnati priorità più bassa hello, possono essere sostituite dalle regole di hello creati. 

Quando si associa un tooa gruppo NIC, le regole di accesso di rete hello in hello gruppo vengono applicati toothat solo scheda di rete. Se un gruppo è applicato tooa singola scheda di rete in una macchina virtuale multi-NIC, non si applica il traffico toohello altre schede di rete. È possibile associare diversi NSGs tooa NIC (o macchina virtuale, a seconda del modello di distribuzione hello) e hello subnet associata a una scheda di rete o di una macchina virtuale. Priorità è assegnata in base alla direzione hello del traffico.

Verificare troppo[piano](../../virtual-network/virtual-networks-nsg.md#planning) il NSGs quando si pianificano le macchine virtuali e rete virtuale.

Questa tabella elenca i metodi di hello che è possibile utilizzare toocreate un gruppo di sicurezza di rete.

| Metodo | Descrizione |
| ------ | ----------- |
| [Portale di Azure](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md) | Quando si crea una macchina virtuale nel portale di Azure hello, un gruppo viene automaticamente creato e associato toohello NIC hello portale crea. nome Hello di hello NSG è una combinazione del nome hello hello VM e **- nsg**. Questo gruppo contiene una regola in ingresso con una priorità di 1000, servizio set tooRDP, hello protocollo set tooTCP, porta impostata too3389 e tooAllow impostazione dell'azione. Se si desidera tooallow qualsiasi altro traffico in entrata toohello VM, è necessario aggiungere regole aggiuntive toohello gruppo. |
| [Azure PowerShell](../../virtual-network/virtual-networks-create-nsg-arm-ps.md) | Utilizzare [New AzureRmNetworkSecurityRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmNetworkSecurityRuleConfig) e fornire informazioni sulle regole di hello necessario. Utilizzare [New AzureRmNetworkSecurityGroup](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmNetworkSecurityGroup) toocreate hello gruppo. Utilizzare [Set AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/Set-AzureRmVirtualNetworkSubnetConfig) tooconfigure hello NSG per subnet hello. Utilizzare [Set AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) tooadd hello NSG toohello rete virtuale. |
| [Interfaccia della riga di comando di Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md) | Utilizzare [rete az creare](https://docs.microsoft.com/cli/azure/network/nsg#create) tooinitially creare hello gruppo. Utilizzare [creare una regola gruppo rete az](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) tooadd toohello gruppo di regole. Utilizzare [aggiornare subnet rete virtuale di rete az](https://docs.microsoft.com/en-us/cli/azure/network/vnet/subnet#update) subnet toohello NSG di tooadd hello. |
| [Modello](../../virtual-network/virtual-networks-create-nsg-arm-template.md) | Vedere [Create a Network Security Group](https://github.com/Azure/azure-quickstart-templates/tree/master/101-security-group-create) (Creare un gruppo di sicurezza di rete) per istruzioni sulla distribuzione di un gruppo di sicurezza di rete con un modello. |

## <a name="load-balancers"></a>Servizi di bilanciamento del carico

[Il bilanciamento del carico Azure](../../load-balancer/load-balancer-overview.md) offre prestazioni elevate, disponibilità e la rete tooyour applicazioni. Un servizio di bilanciamento del carico può essere configurata troppo[bilanciare il traffico Internet in entrata](../../load-balancer/load-balancer-internet-overview.md) tooVMs o [bilanciare il traffico tra le macchine virtuali in una rete virtuale](../../load-balancer/load-balancer-internal-overview.md). Un servizio di bilanciamento del carico può anche di bilanciare il traffico tra computer locali e macchine virtuali in una rete tra più sedi o inoltrare il traffico esterno tooa macchina virtuale specifica.

Hello il carico del servizio di bilanciamento mappe in ingresso e in uscita del traffico tra hello pubblica indirizzo IP e porta del servizio di bilanciamento del carico hello e indirizzo IP privato hello e la porta di hello macchina virtuale.

Quando si crea un servizio di bilanciamento del carico è anche necessario considerare questi elementi di configurazione:

- **Configurazione IP front-end**: un servizio di bilanciamento del carico può includere uno o più indirizzi IP front-end, anche noti come IP virtuali (indirizzi VIP). In ingresso per il traffico hello fungono da questi indirizzi IP.
- **Pool di indirizzi back-end** : gli indirizzi IP associati al carico di toowhich NIC hello viene distribuita.
- **Le regole NAT** -definisce la modalità di traffico attraversa IP front-end hello e IP back-end toohello distribuita.
- **Regole di bilanciamento del carico** -esegue il mapping di un determinato IP front-end e porta combinazione tooa set di indirizzi IP back-end e combinazione di porta. Un bilanciamento del carico singolo può avere più regole di bilanciamento del carico. Ogni regola è una combinazione di un IP e una porta front-end e un IP e una porta back-end associata alle VM.
- **[Probe](../../load-balancer/load-balancer-custom-probe-overview.md)**  -monitor hello integrità delle macchine virtuali. Quando un probe ha esito negativo toorespond, bilanciamento del carico hello interrompe l'invio di nuove connessioni toohello macchina virtuale non integro. connessioni esistenti Hello non sono interessate e le nuove connessioni vengono inviate le macchine virtuali toohealthy.

Questa tabella elenca i metodi di hello che è possibile utilizzare toocreate un bilanciamento del carico con connessione internet.

| Metodo | Description |
| ------ | ----------- |
| Portale di Azure | Attualmente non è possibile creare un servizio di bilanciamento del carico con connessione internet utilizzando hello portale di Azure. |
| [Azure PowerShell](../../load-balancer/load-balancer-get-started-internet-arm-ps.md) | Identificatore hello tooprovide dell'indirizzo IP pubblico hello indirizzi che si utilizzo creato in precedenza, [New AzureRmLoadBalancerFrontendIpConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerFrontendIpConfig) con hello **- PublicIpAddress** parametro. Utilizzare [New AzureRmLoadBalancerBackendAddressPoolConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerBackendAddressPoolConfig) configurazione hello toocreate hello back-end del pool di indirizzi. Utilizzare [New AzureRmLoadBalancerInboundNatRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerInboundNatRuleConfig) toocreate in ingresso regole NAT associate alla configurazione IP front-end hello creato. Utilizzare [New AzureRmLoadBalancerProbeConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerProbeConfig) toocreate hello probe che è necessario. Utilizzare [New AzureRmLoadBalancerRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerRuleConfig) configurazione di bilanciamento del carico hello toocreate. Utilizzare [New AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer) toocreate bilanciamento del carico di hello.|
| [Interfaccia della riga di comando di Azure](../../load-balancer/load-balancer-get-started-internet-arm-cli.md) | Utilizzare [az rete lb creare](https://docs.microsoft.com/cli/azure/network/lb#create) configurazione di bilanciamento del carico iniziale di toocreate hello. Utilizzare [az lb front-end-indirizzo ip di rete creare](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) tooadd hello indirizzo IP pubblico che è stato creato in precedenza. Utilizzare [az lb-pool di indirizzi rete creare](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) configurazione hello tooadd hello back-end del pool di indirizzi. Utilizzare [az rete lb-regola nat in ingresso-creare](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) le regole NAT tooadd. Utilizzare [creare una regola lb rete az](https://docs.microsoft.com/cli/azure/network/lb/rule#create) regole di bilanciamento del carico tooadd hello. Utilizzare [az di rete lb probe creare](https://docs.microsoft.com/cli/azure/network/lb/probe#create) tooadd hello probe. |
| [Modello](../../load-balancer/load-balancer-get-started-internet-arm-template.md) | Utilizzare [2 macchine virtuali in un servizio di bilanciamento del carico e configurare le regole NAT in hello LB](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-natrules) come guida per la distribuzione di un bilanciamento del carico con un modello. |
    
Questa tabella elenca i metodi di hello che è possibile utilizzare toocreate un bilanciamento del carico interno.

| Metodo | Description |
| ------ | ----------- |
| Portale di Azure | Attualmente non è possibile creare un bilanciamento del carico interno utilizzando hello portale di Azure. |
| [Azure PowerShell](../../load-balancer/load-balancer-get-started-ilb-arm-ps.md) | un indirizzo IP privato nella subnet della rete hello, utilizzare tooprovide [New AzureRmLoadBalancerFrontendIpConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerFrontendIpConfig) con hello **- indirizzo IP privato** parametro. Utilizzare [New AzureRmLoadBalancerBackendAddressPoolConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerBackendAddressPoolConfig) configurazione hello toocreate hello back-end del pool di indirizzi. Utilizzare [New AzureRmLoadBalancerInboundNatRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerInboundNatRuleConfig) toocreate in ingresso regole NAT associate alla configurazione IP front-end hello creato. Utilizzare [New AzureRmLoadBalancerProbeConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerProbeConfig) toocreate hello probe che è necessario. Utilizzare [New AzureRmLoadBalancerRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Network/v1.0.13/New-AzureRmLoadBalancerRuleConfig) configurazione di bilanciamento del carico hello toocreate. Utilizzare [New AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer) toocreate bilanciamento del carico di hello.|
| [Interfaccia della riga di comando di Azure](../../load-balancer/load-balancer-get-started-ilb-arm-cli.md) | Hello utilizzare [az rete lb creare](https://docs.microsoft.com/cli/azure/network/lb#create) configurazione di bilanciamento del carico iniziale di comando toocreate hello. toodefine hello indirizzo IP privato, utilizzare [az lb front-end-indirizzo ip di rete creare](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) con hello **-indirizzo ip privato** parametro. Utilizzare [az lb-pool di indirizzi rete creare](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) configurazione hello tooadd hello back-end del pool di indirizzi. Utilizzare [az rete lb-regola nat in ingresso-creare](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) le regole NAT tooadd. Utilizzare [creare una regola lb rete az](https://docs.microsoft.com/cli/azure/network/lb/rule#create) regole di bilanciamento del carico tooadd hello. Utilizzare [az di rete lb probe creare](https://docs.microsoft.com/cli/azure/network/lb/probe#create) tooadd hello probe.|
| [Modello](../../load-balancer/load-balancer-get-started-ilb-arm-template.md) | Utilizzare [2 macchine virtuali in un servizio di bilanciamento del carico e configurare le regole NAT in hello LB](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer) come guida per la distribuzione di un bilanciamento del carico con un modello. |

## <a name="vms"></a>VM

Macchine virtuali possono essere create in hello stessa rete virtuale e può connettersi tooeach altri indirizzi IP privati. Possano connettersi anche se si trovano in subnet diverse senza hello necessità tooconfigure un gateway o utilizzare gli indirizzi IP pubblici. tooput macchine virtuali in una rete virtuale, si crea rete virtuale hello e durante la creazione di ogni macchina virtuale, è assegnare toohello rete virtuale e una subnet. Le VM acquisiscono le impostazioni di rete durante la distribuzione o l'avvio.  

Alle VM viene assegnato un indirizzo IP quando vengono distribuite. Se si distribuiscono più VM in una rete virtuale o in una subnet, gli indirizzi IP verranno assegnati al momento dell'avvio. Un indirizzo IP dinamico (DIP) è l'indirizzo IP interno hello associata a una macchina virtuale. È possibile allocare un tooa DIP statico macchina virtuale. Se si assegna un DIP statico, è consigliabile usare tooavoid una subnet specifica riutilizzo accidentalmente un DIP statico per un'altra macchina virtuale.  

Se si crea una macchina virtuale e successivamente si desidera toomigrate, in una rete virtuale, non è una semplice modifica configurazione. È necessario ridistribuire hello VM in hello rete virtuale. tooredeploy modo più semplice Hello hello toodelete macchina virtuale, ma non tutti i dischi collegati tooit, e quindi ricreare hello VM utilizzando hello dischi originali di hello rete virtuale. 

Questa tabella elenca i metodi di hello che è possibile utilizzare toocreate una macchina virtuale in una rete virtuale.

| Metodo | Descrizione |
| ------ | ----------- |
| [Portale di Azure](../virtual-machines-windows-hero-tutorial.md) | Usa hello impostazioni predefinite di rete che sono stati precedentemente menzionato toocreate una macchina virtuale con una singola scheda di rete. toocreate una macchina virtuale con più schede di rete, è necessario utilizzare un metodo diverso. |
| [Azure PowerShell](../virtual-machines-windows-ps-create.md) | Include l'utilizzo di hello di [Aggiungi AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) tooadd hello NIC creato in precedenza toohello configurazione della macchina virtuale. |
| [Modello](ps-template.md) | Vedere [Very simple deployment of a Windows VM](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) (Distribuzione molto semplice di una VM Windows) per istruzioni sulla distribuzione di una VM con un modello. |

## <a name="next-steps"></a>Passaggi successivi

- Informazioni su come tooconfigure [le route definite dall'utente e l'inoltro IP](../../virtual-network/virtual-networks-udr-overview.md). 
- Informazioni su come tooconfigure [le connessioni di rete virtuale tooVNet](../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).
- Informazioni su come troppo[risolvere route](../../virtual-network/virtual-network-routes-troubleshoot-portal.md).
