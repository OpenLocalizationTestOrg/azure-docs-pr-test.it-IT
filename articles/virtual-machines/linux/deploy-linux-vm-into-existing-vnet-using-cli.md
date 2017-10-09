---
title: aaaDeploy le macchine virtuali Linux in una rete esistente con Azure CLI 2.0 | Documenti Microsoft
description: Informazioni su come una macchina virtuale di Linux in una rete virtuale esistente usando toodeploy hello Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 0df44b3437002df050db56f3b3899083fb49d803
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-cli"></a>Come toodeploy una macchina virtuale di Linux in una rete virtuale di Azure esistente con hello CLI di Azure

Questo articolo illustra come toouse hello Azure CLI 2.0 toodeploy una macchina virtuale (VM) in una rete virtuale esistente. requisiti di Hello sono:

- [Un account di Azure](https://azure.microsoft.com/pricing/free-trial/)
- [File di chiavi SSH pubbliche e private](mac-create-ssh-keys.md)

È anche possibile eseguire questi passaggi con hello [CLI di Azure 1.0](deploy-linux-vm-into-existing-vnet-using-cli-nodejs.md).


## <a name="quick-commands"></a>Comandi rapidi
Se è necessario tooquickly attività hello, hello successiva sezione Dettagli comandi hello necessari. Ulteriori informazioni e il contesto per ogni passaggio è reperibile rest hello del documento hello, [avvio qui](#detailed-walkthrough).

toocreate questo ambiente personalizzato, è necessario più recente hello [CLI di Azure 2.0](/cli/azure/install-az-cli2) installato e registrato con un account Azure tooan [accesso az](/cli/azure/#login).

In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati. I nomi dei parametri di esempio includono *myResourceGroup*, *myVnet* e *myVM*.

**Pre-requisiti:** gruppo di risorse di Azure, rete virtuale e subnet, gruppo di sicurezza di rete con SSH in ingresso e una scheda di interfaccia di rete virtuale.

### <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a>Distribuire hello VM nell'infrastruttura di rete virtuale hello

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

## <a name="detailed-walkthrough"></a>Procedura dettagliata

Gli asset di Azure, come le reti virtuali e i gruppi di sicurezza di rete devono essere risorse statiche, ovvero di lunga durata e distribuite raramente. Dopo la distribuzione di una rete virtuale, può essere riutilizzato per nuove distribuzioni senza alcuna infrastruttura toohello effetto negativo. Pensare a una rete virtuale come un commutatore di rete tradizionale hardware: non è necessario passare un nuovo hardware per ciascuna distribuzione tooconfigure. Con una rete virtuale configurata correttamente, è possibile continuare toodeploy nuove macchine virtuali in tale rete virtuale più volte con poche, eventuali modifiche necessarie per la durata hello della rete virtuale hello.

toocreate questo ambiente personalizzato, è necessario più recente hello [CLI di Azure 2.0](/cli/azure/install-az-cli2) installato e registrato con un account Azure tooan [accesso az](/cli/azure/#login).

In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati. I nomi dei parametri di esempio includono *myResourceGroup*, *myVnet* e *myVM*.

## <a name="create-hello-resource-group"></a>Creare il gruppo di risorse hello

Creare innanzitutto un tooorganize gruppo di risorse di Azure tutti gli oggetti creati in questa procedura dettagliata. Per altre informazioni sui gruppi di risorse, vedere [Panoramica di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md). Creare il gruppo di risorse hello con [gruppo az creare](/cli/azure/group#create). esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *eastus* percorso:

```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

## <a name="create-hello-virtual-network"></a>Creare una rete virtuale hello

Consente di compilare un hello toolaunch di rete virtuale di Azure le macchine virtuali in. Per ulteriori informazioni sulle reti virtuali, vedere [creare una rete virtuale mediante Azure CLI hello](../../virtual-network/virtual-networks-create-vnet-arm-cli.md). Creare una rete virtuale di hello con [creazione della rete virtuale di rete az](/cli/azure/network/vnet#create). esempio Hello crea una rete virtuale denominata *myVnet* e subnet denominata *mySubnet*:

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefix 10.10.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 10.10.1.0/24
```

## <a name="create-hello-network-security-group"></a>Creare un gruppo di sicurezza di rete hello

Gruppi di sicurezza di rete di Azure sono equivalenti tooa firewall a livello di rete hello. Per ulteriori informazioni sui gruppi di sicurezza di rete, vedere [come i gruppi di sicurezza di rete toocreate in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md). Creare un gruppo di sicurezza di rete hello con [rete az creare](/cli/azure/network/nsg#create). esempio Hello crea un gruppo di sicurezza di rete denominato *myNetworkSecurityGroup*:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-ssh-allow-rule"></a>Aggiungere una regola di assenso SSH in ingresso

Hello VM richiede l'accesso da internet, in modo da una regola che consente la porta in ingresso 22 traffico toobe passati tramite hello rete tooport 22 hello VM è necessario hello. Aggiungere una regola in ingresso per il gruppo di sicurezza di rete hello con [creare una regola gruppo rete az](/cli/azure/network/nsg/rule#create). esempio Hello crea una regola denominata *myNetworkSecurityGroupRuleSSH*:

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleSSH \
    --priority 1000 \
    --protocol tcp \
    --destination-port-range 22 \
```

## <a name="attach-hello-subnet-toohello-network-security-group"></a>Collegare gruppi di sicurezza di rete di hello subnet toohello

regole di gruppo di sicurezza di rete Hello possono essere applicato tooa subnet o un'interfaccia di rete virtuale specifica. Consente di collegare la subnet tooour hello rete sicurezza gruppo. Collegare il gruppo di sicurezza della rete toohello subnet con [aggiornare subnet rete virtuale di rete az](/cli/azure/network/vnet/subnet#update):

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="add-a-virtual-network-interface-card-toohello-subnet"></a>Aggiungere una subnet di toohello scheda di interfaccia rete virtuale

Schede di interfaccia di rete virtuale (VNics) sono importanti, come è possibile riutilizzare gli connettendo le macchine virtuali toodifferent. In questo modo consente hello tookeep VNic come una risorsa statica hello macchine virtuali può essere temporaneo. Creare una scheda di rete virtuale e associarlo a subnet hello [az rete nic creare](/cli/azure/network/nic#create). esempio Hello crea una scheda di rete virtuale denominata *myNic*:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet
```

## <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a>Distribuire hello VM nell'infrastruttura di rete virtuale hello

Bloccare tutto il traffico in ingresso, ad eccezione di porta 22 per SSH è disponibile una rete virtuale e subnet e una subnet hello di tooprotect gruppo di sicurezza di rete. è ora possibile distribuire Hello VM all'interno di questa infrastruttura di rete esistente.

Creare la macchina virtuale con [az vm create](/cli/azure/vm#create). Per ulteriori informazioni su hello flag toouse con toodeploy hello Azure CLI 2.0 una VM completezza, vedere [creare un ambiente completo di Linux mediante Azure CLI hello](create-cli-complete.md).

Hello di esempio seguente crea una macchina virtuale tramite dischi gestiti di Azure. I dischi vengono gestiti dalla piattaforma Azure hello e non richiedono alcun toostore preparazione o percorso li. Per altre informazioni sui dischi gestiti, vedere [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md) (Panoramica di Azure Managed Disks). Se si desiderano dischi toouse non gestita, vedere la nota aggiuntive hello sotto.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

Se si usa Managed Disks, ignorare questo passaggio. Se si desiderano dischi toouse non gestita, è necessario hello tooadd seguendo i dischi parametri aggiuntivi toohello procedere comando toocreate non gestita nell'account di archiviazione hello denominato `mystorageaccount`: 

```azurecli
    --use-unmanaged-disk \
    --storage-account mystorageaccount
```

Utilizzando hello CLI flag toocall risorse esistente, indicando hello toodeploy Azure VM all'interno di una rete esistente hello. Una volta distribuite la rete virtuale e la subnet possono essere usate come risorse statiche o permanenti nell'area di Azure. In questo esempio, si non creare e assegnare un toohello di indirizzo IP pubblico scheda di rete virtuale, in modo che questa macchina virtuale non è accessibile pubblicamente su Internet hello. Per ulteriori informazioni, vedere [creare una macchina virtuale con un indirizzo IP pubblico statico mediante Azure CLI hello](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md).

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni su modi toocreate le macchine virtuali in Azure, vedere hello seguenti risorse:

* [Utilizzare un toocreate modello di gestione risorse di Azure una distribuzione specifica](../windows/cli-deploy-templates.md)
* [Creare un ambiente Linux completo mediante l'interfaccia della riga di comando di Azure](create-cli-complete.md)
* [Creare una VM Linux in Azure usando i modelli](create-ssh-secured-vm-from-template.md)
