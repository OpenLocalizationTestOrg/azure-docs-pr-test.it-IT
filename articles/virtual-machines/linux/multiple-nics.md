---
title: "una VM Linux di Azure con più schede di rete aaaCreate | Documenti Microsoft"
description: "Informazioni su come toocreate una VM Linux con più schede di rete associata tooit modelli hello CLI di Azure 2.0 o gestione delle risorse."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 5d2d04d0-fc62-45fa-88b1-61808a2bc691
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 2723405914777a5dce4354d4f5d8413e357f58e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-virtual-machine-in-azure-with-multiple-network-interface-cards"></a>Come toocreate una macchina virtuale di Linux in Azure con la rete di più schede di interfaccia
È possibile creare una macchina virtuale (VM) in Azure con più tooit interfacce (NIC) collegate di rete virtuale. Uno scenario comune è toohave subnet diverse per la connettività front-end e back-end, o una rete dedicata tooa monitoraggio o una soluzione di backup. In questo articolo illustra in dettaglio come toocreate una macchina virtuale con più schede di rete associata tooit e come le schede NIC tooadd o rimuovere da una macchina virtuale esistente. Per informazioni dettagliate, incluso come toocreate più schede di rete all'interno del proprio Bash script, altre informazioni sui [la distribuzione di macchine virtuali multi-NIC](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md). Le differenti [dimensioni della macchina virtuale](sizes.md) supportano un numero variabile di schede di rete, pertanto scegliere le dimensioni della macchina virtuale di conseguenza.

In questo articolo illustra in dettaglio come toocreate una macchina virtuale con più schede di rete con hello CLI di Azure 2.0. È anche possibile eseguire questi passaggi con hello [CLI di Azure 1.0](multiple-nics-nodejs.md).


## <a name="create-supporting-resources"></a>Creare risorse di supporto
Hello installazione più recente [CLI di Azure 2.0](/cli/azure/install-az-cli2) e accedere con un account Azure tooan [accesso az](/cli/azure/#login).

In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati. I nomi dei parametri di esempio includono *myResourceGroup*, *mystorageaccount* e *myVM*.

Creare prima un gruppo di risorse con [az group create](/cli/azure/group#create). esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *eastus* percorso:

```azurecli
az group create --name myResourceGroup --location eastus
```

Creare una rete virtuale di hello con [creazione della rete virtuale di rete az](/cli/azure/network/vnet#create). esempio Hello crea una rete virtuale denominata *myVnet* e subnet denominata *mySubnetFrontEnd*:

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnetFrontEnd \
    --subnet-prefix 192.168.1.0/24
```

Creare una subnet per il traffico di back-end hello con [creare subnet della rete virtuale rete az](/cli/azure/network/vnet/subnet#create). esempio Hello crea una subnet denominata *mySubnetBackEnd*:

```azurecli
az network vnet subnet create \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

Creare un gruppo di sicurezza di rete con il comando [az network nsg create](/cli/azure/network/nsg#create). esempio Hello crea un gruppo di sicurezza di rete denominato *myNetworkSecurityGroup*:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="create-and-configure-multiple-nics"></a>Creare e configurare più schede di interfaccia di rete
Creare due schede di interfaccia di rete con il comando [az network nic create](/cli/azure/network/nic#create). esempio Hello crea due schede di rete, denominati *myNic1* e *myNic2*connesse, gruppo di sicurezza rete hello, con una scheda di rete che connettono tooeach subnet:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic1 \
    --vnet-name myVnet \
    --subnet mySubnetFrontEnd \
    --network-security-group myNetworkSecurityGroup
az network nic create \
    --resource-group myResourceGroup \
    --name myNic2 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

## <a name="create-a-vm-and-attach-hello-nics"></a>Creare una macchina virtuale e collegare le schede NIC hello
Quando si crea hello macchina virtuale, specificare le schede NIC hello creato con `--nics`. È necessario anche tootake attenzione quando si seleziona hello dimensioni della macchina virtuale. Vi sono limiti per il numero totale di schede di rete che è possibile aggiungere VM tooa hello. Ulteriori informazioni sulle [dimensioni delle macchine virtuali di Linux](sizes.md). 

Creare una VM con il comando [az vm create](/cli/azure/vm#create). esempio Hello crea una macchina virtuale denominata *myVM*:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --size Standard_DS3_v2 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic1 myNic2
```

## <a name="add-a-nic-tooa-vm"></a>Aggiungere un tooa NIC VM
passaggi precedenti Hello creato una macchina virtuale con più schede di rete. È inoltre possibile aggiungere NIC tooan esistente VM con hello CLI di Azure 2.0. 

Creare un'altra scheda di interfaccia di rete con [az network nic create](/cli/azure/network/nic#create). esempio Hello crea una scheda di rete denominata *myNic3* connesso toohello subnet di back-end e il gruppo di sicurezza di rete creato nei passaggi precedenti hello:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic3 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

tooadd tooan una scheda di rete macchina virtuale esistente, prima di deallocare hello macchina virtuale con [az vm deallocare](/cli/azure/vm#deallocate). esempio Hello dealloca hello macchina virtuale denominata *myVM*:

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

Aggiungere NIC con hello [scheda nic vm az aggiungere](/cli/azure/vm/nic#add). Hello esempio aggiunge *myNic3* troppo*myVM*:

```azurecli
az vm nic add \
    --resource-group myResourceGroup \
    --vm-name myVM \
    --nics myNic3
```

Avvia macchina virtuale con hello [inizio vm az](/cli/azure/vm#start):

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```

## <a name="remove-a-nic-from-a-vm"></a>Rimuovere una scheda di interfaccia di rete da una VM
tooremove una scheda di rete da una macchina virtuale esistente, prima di deallocare hello VM con [az vm deallocare](/cli/azure/vm#deallocate). esempio Hello dealloca hello macchina virtuale denominata *myVM*:

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

Rimuovere hello NIC con [rimuovere la scheda nic vm az](/cli/azure/vm/nic#remove). Hello esempio seguente viene rimosso *myNic3* da *myVM*:

```azurecli
az vm nic remove \
    --resource-group myResourceGroup \
    --vm-name myVM 
    --nics myNic3
```

Avvia macchina virtuale con hello [inizio vm az](/cli/azure/vm#start):

```azurecli
az vm start --resource-group myResourceGroup --name myVM
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
Revisione [le dimensioni di VM Linux](sizes.md) durante il tentativo di toocreating una macchina virtuale con più schede di rete. Prestare attenzione toohello massimo NIC supporta ogni dimensione della macchina virtuale. 
