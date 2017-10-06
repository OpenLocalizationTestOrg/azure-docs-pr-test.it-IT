---
title: toocreate filtro di pacchetti di FreeBSD aaaUse un firewall in Azure | Documenti Microsoft
description: Informazioni su come toodeploy NAT firewall utilizzando del FreeBSD PF in Azure.
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/20/2017
ms.author: kyliel
ms.openlocfilehash: 3d3a5dde2ca03ba6fc384581c786f5eb746e6d92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-freebsds-packet-filter-toocreate-a-secure-firewall-in-azure"></a>Come toocreate filtro di pacchetti di FreeBSD toouse un firewall sicuro in Azure
Questo articolo descrive come toodeploy firewall NAT con filtro del FreeBSD di chi tramite il modello di gestione risorse di Azure per scenario comune di server web.

## <a name="what-is-pf"></a>Informazioni su PF
PF (Packet Filter, chiamato anche pf) è un filtro di pacchetti con stato con licenza BSD, un componente software fondamentale per un firewall. Dalla sua creazione, PF si è rapidamente evoluto e ora dispone di numerosi vantaggi rispetto ad altri firewall disponibili. Network Address Translation (NAT) è in PF dopo un giorno, quindi Utilità di pianificazione pacchetti e gestione di coda attiva sono state integrate in PF, grazie all'integrazione hello ALTQ e rendendo configurabili tramite la configurazione di cartelle pubbliche. Le funzionalità, ad esempio pfsync e protocollo CARP per il failover e ridondanza, authpf per la sessione di autenticazione e proxy ftp tooease firewall hello difficile protocollo FTP, sono inoltre esteso PF. In breve, PF è un firewall potente e ricco di funzionalità. 

## <a name="get-started"></a>Attività iniziali
Se si desidera configurare un firewall sicuro nel cloud hello per i server web, è possibile iniziare subito. È inoltre possibile applicare script hello utilizzati in questa tooset del modello di gestione risorse di Azure backup la topologia di rete.
modello di gestione risorse di Azure Hello configurare una macchina virtuale FreeBSD che esegue /redirection NAT PF e due FreeBSD le macchine virtuali con il server web Nginx hello installato e configurato. Inoltre tooperforming NAT per due server web di hello in uscita del traffico, macchina virtuale di hello NAT/reindirizzamento intercetta le richieste HTTP e reindirizza toohello due server web in modo round robin. Hello rete virtuale utilizza hello privato non instradabile IP indirizzo spazio 10.0.0.2/24 ed è possibile modificare i parametri hello del modello di hello. modello di Azure Resource Manager Hello definisce anche una tabella di route per l'intera rete virtuale, che è una raccolta di route singoli utilizzato route predefinito di Azure toooverride basate sull'indirizzo IP di destinazione hello hello. 

![pf_topology](./media/freebsd-pf-nat/pf_topology.jpg)
    
### <a name="deploy-through-azure-cli"></a>Distribuire tramite l'interfaccia della riga di comando di Azure
È necessario più recente hello [CLI di Azure 2.0](/cli/azure/install-az-cli2) installato e registrato con un account Azure tooan [accesso az](/cli/azure/#login). Come prima cosa creare un gruppo di risorse con [az group create](/cli/azure/group#create). esempio Hello crea il nome di un gruppo di risorse `myResourceGroup` in hello `West US` percorso.

```azurecli
az group create --name myResourceGroup --location westus
```

Successivamente, distribuire il modello di hello [pf-freebsd-setup](https://github.com/Azure/azure-quickstart-templates/tree/master/pf-freebsd-setup) con [distribuzione gruppo az creare](/cli/azure/group/deployment#create). Scaricare [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/pf-freebsd-setup/azuredeploy.parameters.json) in hello stesso percorso e definire i valori di risorsa, ad esempio `adminPassword`, `networkPrefix`, e `domainNamePrefix`. 

```azurecli
az group deployment create --resource-group myResourceGroup --name myDeploymentName \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/pf-freebsd-setup/azuredeploy.json \
    --parameters '@azuredeploy.parameters.json' --verbose
```

Dopo circa cinque minuti, si riceveranno informazioni hello di `"provisioningState": "Succeeded"`. È quindi possibile ssh front-end toohello VM (NAT) o accedere ai server web Nginx in un browser utilizzando l'indirizzo IP pubblico hello o FQDN di front-end hello VM (NAT). Hello esempio seguente vengono elencati il nome FQDN e indirizzo IP pubblico assegnato front-end toohello VM (NAT) in hello `myResourceGroup` gruppo di risorse. 

```azurecli
az network public-ip list --resource-group myResourceGroup
```
    
## <a name="next-steps"></a>Passaggi successivi
Si desidera tooset il proprio protocollo NAT in Azure? Open Source, gratuito ma potente? PF è quindi una scelta ottimale. Tramite il modello di hello [pf-freebsd-setup](https://github.com/Azure/azure-quickstart-templates/tree/master/pf-freebsd-setup), è necessario solo cinque minuti tooset di un firewall NAT con FreeBSD utilizzo di bilanciamento del carico di round robin PF in Azure per scenario comune di server web. 

Se si desidera offerta hello toolearn di FreeBSD in Azure, fare riferimento troppo[tooFreeBSD introduzione in Azure](freebsd-intro-on-azure.md).

Se si desidera tooknow ulteriori informazioni sulle cartelle pubbliche, fare riferimento troppo[manuale FreeBSD](https://www.freebsd.org/doc/handbook/firewalls-pf.html) o [manuale dell'utente-PF](https://www.freebsd.org/doc/handbook/firewalls-pf.html).
