---
title: aaaOpen porte tooa VM Linux con 1.0 CLI di Azure | Documenti Microsoft
description: Informazioni su come tooopen una porta / creare una VM Linux di tooyour endpoint utilizzando la distribuzione di gestione risorse di Azure hello del modello e hello Azure CLI 1.0
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 337c37d151f527b43d4852291159b2f70a00accc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="opening-ports-and-endpoints-tooa-linux-vm-in-azure-using-hello-azure-cli-10"></a>Apertura porte ed endpoint tooa VM Linux in Azure tramite hello Azure CLI 1.0
Aprire una porta o creare un endpoint, tooa macchina virtuale (VM) in Azure tramite la creazione di un filtro di rete su una subnet o l'interfaccia di rete VM. Questi filtri, che consentono di controllare il traffico in ingresso e in uscita, posizionare in una risorsa toohello gruppo di sicurezza di rete associata che riceve il traffico di hello. Si userà un esempio comune di traffico Web sulla porta 80. In questo articolo viene illustrato come una porta tooa VM utilizzando tooopen hello Azure CLI 1.0.


## <a name="cli-versions-toocomplete-hello-task"></a>Attività hello toocomplete versioni CLI
È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:

- [Azure CLI 1.0](#quick-commands) : l'interfaccia CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)
- [Azure CLI 2.0](nsg-quickstart.md) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello


## <a name="quick-commands"></a>Comandi rapidi
toocreate un gruppo di sicurezza di rete e le regole è necessario [hello Azure CLI 1.0](../../cli-install-nodejs.md) installati e utilizzando la modalità di gestione risorse:

```azurecli
azure config mode arm
```

In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati. I nomi dei parametri di esempio includono *myResourceGroup*, *myNetworkSecurityGroup* e *myVnet*.

Creare il gruppo di sicurezza di rete immettendo nomi e percorso in modo appropriato. esempio Hello crea un gruppo di sicurezza di rete denominata *myNetworkSecurityGroup* in hello *eastus* percorso:

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

Aggiungere un server Web tooyour di traffico HTTP tooallow regola (o modificare per proprio scenario, ad esempio la connettività di accesso o database SSH). esempio Hello crea una regola denominata *myNetworkSecurityGroupRule* tooallow TCP il traffico sulla porta 80:

```azurecli
azure network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --destination-port-range 80 \
    --access allow
```

Associare l'interfaccia di rete della macchina virtuale (NIC) hello il gruppo di sicurezza di rete. esempio Hello associa una scheda di rete esistente denominato *myNic* con il gruppo di sicurezza di rete denominata hello *myNetworkSecurityGroup*:

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --name myNic
```

In alternativa, è possibile associare il gruppo di sicurezza di rete con una subnet della rete virtuale anziché semplicemente toohello interfaccia di rete in una singola macchina virtuale. esempio Hello associa una subnet esistente denominata *mySubnet* in hello *myVnet* rete virtuale con il gruppo di sicurezza di rete denominata hello *myNetworkSecurityGroup*:

```azurecli
azure network vnet subnet set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --vnet-name myVnet --name mySubnet
```

## <a name="more-information-on-network-security-groups"></a>Altre informazioni sui gruppi di sicurezza di rete
Hello rapido comandi consentono di tooget backup e in esecuzione con traffico propagazione tooyour macchina virtuale. Gruppi di sicurezza di rete forniscono numerose funzionalità eccellenti e granularità per il controllo tooyour di accedere alle risorse. Per altre informazioni, leggere l'articolo sulla [creazione di un gruppo di sicurezza di rete e di regole dell'elenco di controllo di accesso qui](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).

È possibile definire le regole dell'elenco di controllo di accesso e i gruppi di sicurezza di rete come parte dei modelli di Azure Resource Manager. Per altre informazioni, leggere l'articolo [Come creare NSG utilizzando un modello](../../virtual-network/virtual-networks-create-nsg-arm-template.md).

Se è necessario toouse il port forwarding toomap una porta interna tooan di porta esterna univoco nella VM, utilizzare un servizio di bilanciamento del carico e le regole Network Address Translation (NAT). Ad esempio, è possibile desidera tooexpose la porta TCP 8080 esternamente e il traffico diretto tooTCP porta 80 in una macchina virtuale. Per altre informazioni, leggere l'articolo relativo alla [creazione di un servizio di bilanciamento del carico per Internet](../../load-balancer/load-balancer-get-started-internet-arm-cli.md).

## <a name="next-steps"></a>Passaggi successivi
In questo esempio è stato creato il traffico HTTP tooallow una semplice regola. È possibile trovare informazioni sulla creazione di ambienti più dettagliati in hello seguenti articoli:

* [Panoramica di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)
* [Che cos'è un gruppo di sicurezza di rete](../../virtual-network/virtual-networks-nsg.md)
* [Panoramica di Azure Resource Manager per i servizi di bilanciamento del carico](../../load-balancer/load-balancer-arm.md)

