---
title: "una VM Linux di Azure con più schede di rete aaaCreate | Documenti Microsoft"
description: "Informazioni su come toocreate una VM Linux con più schede di rete associata tooit modelli hello CLI di Azure o di gestione delle risorse."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 457dab734ceeeefd35cddaf1ebb9ea0a82f4e207
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-multiple-nics-using-hello-azure-cli-10"></a>Creare una macchina virtuale Linux con più schede di rete utilizzando hello Azure CLI 1.0
È possibile creare una macchina virtuale (VM) in Azure con più tooit interfacce (NIC) collegate di rete virtuale. Uno scenario comune è toohave subnet diverse per la connettività front-end e back-end, o una rete dedicata tooa monitoraggio o una soluzione di backup. Questo articolo fornisce comandi rapidi toocreate una macchina virtuale con più schede di rete associate tooit. Per informazioni dettagliate, incluso come toocreate più schede di rete all'interno del proprio Bash script, altre informazioni sui [la distribuzione di macchine virtuali multi-NIC](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md). Le differenti [dimensioni della macchina virtuale](sizes.md) supportano un numero variabile di schede di rete, pertanto scegliere le dimensioni della macchina virtuale di conseguenza.

> [!WARNING]
> Quando si crea una macchina virtuale: non è possibile aggiungere schede NIC tooan esistente VM con hello Azure CLI 1.0, è necessario collegare più schede di rete. È possibile [aggiungere NIC tooan esistente VM con hello Azure CLI 2.0](multiple-nics.md). È anche possibile [creare una macchina virtuale in base a dischi virtuali originale hello](copy-vm.md) e creare più schede di rete quando si distribuisce hello macchina virtuale.


## <a name="cli-versions-toocomplete-hello-task"></a>Attività hello toocomplete versioni CLI
È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:

- [Azure CLI 1.0](#create-supporting-resources) : l'interfaccia CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)
- [Azure CLI 2.0](multiple-nics.md) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello


## <a name="create-supporting-resources"></a>Creare risorse di supporto
Assicurarsi di avere hello [CLI di Azure](../../cli-install-nodejs.md) effettuato l'accesso e utilizzo della modalità di gestione delle risorse:

```azurecli
azure config mode arm
```

In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati. I nomi dei parametri di esempio includono *myResourceGroup*, *mystorageaccount* e *myVM*.

Creare prima un gruppo di risorse. esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *eastus* percorso:

```azurecli
azure group create myResourceGroup --location eastus
```

Creare un toohold di account di archiviazione delle macchine virtuali. esempio Hello crea un account di archiviazione denominato *mystorageaccount*:

```azurecli
azure storage account create mystorageaccount \
    --resource-group myResourceGroup \
    --location eastus \
    --kind Storage \
    --sku-name PLRS
```

Creare una rete virtuale di tooconnect le macchine virtuali. esempio Hello crea una rete virtuale denominata *myVnet* con un prefisso dell'indirizzo *192.168.0.0/16*:

```azurecli
azure network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefixes 192.168.0.0/16
```

Creare due subnet per la rete virtuale: una per il traffico front-end e l'altra per il traffico di back-end. esempio Hello crea due subnet, denominata *mySubnetFrontEnd* e *mySubnetBackEnd*:

```azurecli
azure network vnet subnet create \
    --resource-group myResourceGroup \
    --location myVnet \
    --name mySubnetFrontEnd \
    --address-prefix 192.168.1.0/24
azure network vnet subnet create \
    --resource-group myResourceGroup \
    --location myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

## <a name="create-and-configure-multiple-nics"></a>Creare e configurare più schede di interfaccia di rete
È possibile leggere altre informazioni su [la distribuzione di più schede di rete mediante Azure CLI hello](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md), inclusi gli script di processo hello scorrere in ciclo toocreate tutte le NIC hello.

esempio Hello crea due schede di rete, denominati *myNic1* e *myNic2*, con una scheda di rete che connettono tooeach subnet:

```azurecli
azure network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic1 \
    --subnet-vnet-name myVnet \
    --subnet-name mySubnetFrontEnd
azure network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic2 \
    --subnet-vnet-name myVnet \
    --subnet-name mySubnetBackEnd
```

In genere si crea anche un [Network Security Group](../../virtual-network/virtual-networks-nsg.md) o [bilanciamento del carico](../../load-balancer/load-balancer-overview.md) toohelp gestire e distribuire il traffico tra le macchine virtuali. esempio Hello crea un gruppo di sicurezza di rete denominata *myNetworkSecurityGroup*:

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

Associare il gruppo di sicurezza di rete toohello NIC utilizzando `azure network nic set`. Hello esempio associa *myNic1* e *myNic2* con *myNetworkSecurityGroup*:

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --name myNic1 \
    --network-security-group-name myNetworkSecurityGroup
azure network nic set \
    --resource-group myResourceGroup \
    --name myNic2 \
    --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-a-vm-and-attach-hello-nics"></a>Creare una macchina virtuale e collegare le schede NIC hello
Quando si creano hello VM, è ora possibile specificare più schede di rete. Utilizzano invece `--nic-name` tooprovide una singola scheda di rete, usare invece la `--nic-names` e fornire un elenco delimitato da virgole di schede di rete. È necessario anche tootake attenzione quando si seleziona hello dimensioni della macchina virtuale. Vi sono limiti per il numero totale di schede di rete che è possibile aggiungere VM tooa hello. Ulteriori informazioni sulle [dimensioni delle macchine virtuali di Linux](sizes.md). Hello esempio seguente viene illustrato come toospecify più schede di rete e quindi una macchina virtuale di dimensione che supporta l'utilizzo di più schede di rete (*Standard_DS2_v2*):

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --location eastus \
    --os-type linux \
    --nic-names myNic1,myNic2 \
    --vm-size Standard_DS2_v2 \
    --storage-account-name mystorageaccount \
    --image-urn UbuntuLTS \
    --admin-username azureuser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub
```

## <a name="create-multiple-nics-using-resource-manager-templates"></a>Creare più schede di interfaccia di rete usando i modelli di Resource Manager
Modelli di gestione risorse di Azure utilizzano dichiarativa JSON file toodefine l'ambiente. È possibile consultare una [panoramica di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md). Modelli di gestione risorse forniscono un modo toocreate più istanze di una risorsa durante la distribuzione, ad esempio la creazione di più schede di rete. Utilizzare *copia* numero hello toospecify di toocreate istanze:

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

Ulteriori informazioni sulla [creazione di più istanze utilizzando *Copia*](../../resource-group-create-multiple.md). 

È inoltre possibile utilizzare un `copyIndex()` toothen aggiungere un nome di risorsa tooa numero, che consente di toocreate `myNic1`, `myNic2`, e così via hello seguito è riportato un esempio di aggiunta di valore di indice hello:

```json
"name": "[concat('myNic', copyIndex())]", 
```

È possibile consultare un esempio completo di [creazione di più schede di rete utilizzando i modelli di Resource Manager](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).

## <a name="next-steps"></a>Passaggi successivi
Verificare che tooreview [le dimensioni di VM Linux](sizes.md) durante il tentativo di toocreating una macchina virtuale con più schede di rete. Prestare attenzione toohello massimo NIC supporta ogni dimensione della macchina virtuale. 

Tenere presente che non è possibile aggiungere ulteriori tooan di schede di rete VM esistente, è necessario creare tutte le NIC hello quando si distribuisce hello macchina virtuale. Prestare attenzione quando si pianifica la toomake le distribuzioni di avere hello necessaria la connettività di rete sin hello.

