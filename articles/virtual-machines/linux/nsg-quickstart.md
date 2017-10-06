---
title: aaaOpen porte tooa VM Linux con Azure CLI 2.0 | Documenti Microsoft
description: Informazioni su come tooopen una porta / creare una VM Linux di tooyour endpoint utilizzando la distribuzione di gestione risorse di Azure hello del modello e hello Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: eef9842b-495a-46cf-99a6-74e49807e74e
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: c79b31206e97558171609cf033bb3cb3370777c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="open-ports-and-endpoints-tooa-linux-vm-with-hello-azure-cli"></a>Aprire le porte e gli endpoint tooa VM Linux con hello CLI di Azure
Aprire una porta o creare un endpoint, tooa macchina virtuale (VM) in Azure tramite la creazione di un filtro di rete su una subnet o l'interfaccia di rete VM. Questi filtri, che consentono di controllare il traffico in ingresso e in uscita, posizionare in una risorsa toohello gruppo di sicurezza di rete associata che riceve il traffico di hello. Si userà un esempio comune di traffico Web sulla porta 80. In questo articolo illustra come tooopen tooa una porta VM con hello CLI di Azure 2.0. È anche possibile eseguire questi passaggi con hello [CLI di Azure 1.0](nsg-quickstart-nodejs.md).


## <a name="quick-commands"></a>Comandi rapidi
Gruppo di sicurezza di rete toocreate e regole, è necessario hello più recente [CLI di Azure 2.0](/cli/azure/install-az-cli2) installato e registrato con un account Azure tooan [accesso az](/cli/azure/#login).

In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati. I nomi dei parametri di esempio includono *myResourceGroup*, *myNetworkSecurityGroup* e *myVnet*.

Creare un gruppo di sicurezza di rete hello con [rete az creare](/cli/azure/network/nsg#create). esempio Hello crea un gruppo di sicurezza di rete denominato *myNetworkSecurityGroup* in hello *eastus* percorso:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

Aggiungere una regola con [creare una regola gruppo rete az](/cli/azure/network/nsg/rule#create) tooallow HTTP traffico webserver tooyour (o modificare per proprio scenario, ad esempio la connettività di accesso o database SSH). esempio Hello crea una regola denominata *myNetworkSecurityGroupRule* tooallow TCP il traffico sulla porta 80:

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1000 \
    --destination-port-range 80
```

Associare il gruppo di sicurezza di rete hello con interfaccia di rete della macchina virtuale (NIC) [aggiornamento nic di rete az](/cli/azure/network/nic#update). esempio Hello associa una scheda di rete esistente denominato *myNic* con il gruppo di sicurezza di rete denominata hello *myNetworkSecurityGroup*:

```azurecli
az network nic update \
    --resource-group myResourceGroup \
    --name myNic \
    --network-security-group myNetworkSecurityGroup
```

In alternativa, è possibile associare il gruppo di sicurezza di rete a una subnet di rete virtuale con [aggiornare subnet rete virtuale di rete az](/cli/azure/network/vnet/subnet#update) anziché semplicemente toohello interfaccia di rete in una singola macchina virtuale. esempio Hello associa una subnet esistente denominata *mySubnet* in hello *myVnet* rete virtuale con il gruppo di sicurezza di rete denominata hello *myNetworkSecurityGroup*:

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="more-information-on-network-security-groups"></a>Altre informazioni sui gruppi di sicurezza di rete
Hello rapido comandi consentono di tooget backup e in esecuzione con traffico propagazione tooyour macchina virtuale. Gruppi di sicurezza di rete forniscono numerose funzionalità eccellenti e granularità per il controllo tooyour di accedere alle risorse. Per altre informazioni, leggere l'articolo sulla [creazione di un gruppo di sicurezza di rete e di regole dell'elenco di controllo di accesso qui](tutorial-virtual-network.md#secure-network-traffic).

Per le applicazioni Web a disponibilità elevata, è consigliabile inserire le macchine virtuali dietro a un Azure Load Balancer. bilanciamento del carico di Hello distribuisce il traffico tooVMs, con un gruppo di sicurezza di rete che consente di filtrare il traffico. Per ulteriori informazioni, vedere [come macchine saldo tooload virtuali Linux in Azure toocreate applicazioni a disponibilità elevata](tutorial-load-balancer.md).

## <a name="next-steps"></a>Passaggi successivi
In questo esempio è stato creato il traffico HTTP tooallow una semplice regola. È possibile trovare informazioni sulla creazione di ambienti più dettagliati in hello seguenti articoli:

* [Panoramica di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)
* [Che cos'è un gruppo di sicurezza di rete](../../virtual-network/virtual-networks-nsg.md)
