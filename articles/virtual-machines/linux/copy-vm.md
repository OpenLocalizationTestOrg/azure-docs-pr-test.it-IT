---
title: una VM Linux mediante Azure CLI 2.0 aaaCopy | Documenti Microsoft
description: Informazioni su come toocreate una copia della macchina virtuale Linux di Azure mediante Azure CLI 2.0 e i dischi gestiti.
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 03/10/2017
ms.author: cynthn
ms.openlocfilehash: ee34a4259dd0c1e7bf49312fe3fe3ba809bf69e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-linux-vm-by-using-azure-cli-20-and-managed-disks"></a>Creare una copia di una VM Linux di Azure usando l'interfaccia della riga di comando di Azure 2.0 e i dischi gestiti


In questo articolo viene illustrato come una copia della macchina virtuale Azure (VM) in esecuzione Linux usando toocreate hello Azure CLI 2.0 e il modello di distribuzione Azure Resource Manager hello. È anche possibile eseguire questi passaggi con hello [CLI di Azure 1.0](copy-vm-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

È anche possibile [caricare e creare una VM da un disco rigido virtuale](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="prerequisites"></a>Prerequisiti


-   Installare l'[interfaccia della riga di comando di Azure 2.0](/cli/azure/install-az-cli2)

-   Accedi tooan account Azure con [accesso az](/cli/azure/#login).

-   Toouse una macchina virtuale di Azure per avere hello origine per la copia.

## <a name="step-1-stop-hello-source-vm"></a>Passaggio 1: Arresta macchina virtuale di origine hello


Deallocare una macchina virtuale di origine hello utilizzando [az vm deallocare](/cli/azure/vm#deallocate).
esempio Hello dealloca hello macchina virtuale denominata **myVM** nel gruppo di risorse hello **myResourceGroup**:

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

## <a name="step-2-copy-hello-source-vm"></a>Passaggio 2: Copiare una macchina virtuale di origine hello


toocopy una macchina virtuale, si crea una copia del disco rigido virtuale sottostante di hello. Questo processo crea un disco rigido virtuale specifico come disco gestita che contiene hello impostazioni come hello e la stessa configurazione di macchina virtuale di origine.

Per altre informazioni su Azure Managed Disks, vedere [Azure Managed Disks overview](../windows/managed-disks-overview.md) (Panoramica di Azure Managed Disks). 

1.  Elenco di ogni macchina virtuale e hello il nome del relativo disco del sistema operativo con [elenco vm az](/cli/azure/vm#list). Hello esempio seguente vengono elencate tutte le macchine virtuali nel gruppo di risorse denominato **myResourceGroup**:
    
    ```azurecli
    az vm list -g myTestRG --query '[].{Name:name,DiskName:storageProfile.osDisk.name}' --output table
    ```

    Hello l'output è simile toohello seguente esempio:

    ```azurecli
    Name    DiskName
    ------  --------
    myVM    myDisk
    ```

1.  Disco di hello copia creando un nuovo gestito disco tramite [disco az creare](/cli/azure/disk#create). esempio Hello crea un disco denominato **myCopiedDisk** da hello gestito disco denominato **myDisk**:

    ```azurecli
    az disk create --resource-group myResourceGroup --name myCopiedDisk --source myDisk
    ``` 

1.  Verificare i dischi di hello gestito ora nel gruppo di risorse utilizzando [elenco disco az](/cli/azure/disk#list). esempio Hello Elenca dischi hello gestito nel gruppo di risorse hello denominato **myResourceGroup**:

    ```azurecli
    az disk list --resource-group myResourceGroup --output table
    ```

1.  Ignorare troppo["passaggio 3: configurare una rete virtuale"](#step-3-set-up-a-virtual-network).


## <a name="step-3-set-up-a-virtual-network"></a>Passaggio 3: Configurare una rete virtuale


Hello passaggi facoltativi seguenti creare una nuova rete virtuale, subnet, l'indirizzo IP pubblico e scheda di interfaccia di rete virtuale (NIC).

Se si copia una macchina virtuale per la risoluzione dei problemi relativi a scopo o altre distribuzioni, è consigliabile non toouse una macchina virtuale in una rete virtuale esistente.

Se si desidera toocreate un'infrastruttura di rete virtuale per le macchine virtuali di copiate, quindi seguire hello alcuni passaggi. Se non si desidera toocreate una rete virtuale, andare troppo[passaggio 4: creare una macchina virtuale](#step-4-create-a-vm).

1.  Creare una rete virtuale hello utilizzando [creazione della rete virtuale di rete az](/cli/azure/network/vnet#create). esempio Hello crea una rete virtuale denominata **myVnet** e una subnet denominata **mySubnet**:

    ```azurecli
    az network vnet create --resource-group myResourceGroup --location westus --name myVnet \
        --address-prefix 192.168.0.0/16 --subnet-name mySubnet --subnet-prefix 192.168.1.0/24
    ```

1.  Creare un indirizzo IP pubblico usando il comando [az network public-ip create](/cli/azure/network/public-ip#create). esempio Hello crea un indirizzo IP pubblico denominato **myPublicIP** con nome DNS hello **mypublicdns**. (nome DNS hello deve essere univoco, quindi specificare un nome univoco.)

    ```azurecli
    az network public-ip create --resource-group myResourceGroup --location westus \
        --name myPublicIP --dns-name mypublicdns --allocation-method static --idle-timeout 4
    ```

1.  Creare una scheda NIC hello utilizzando [az rete nic creare](/cli/azure/network/nic#create).
    esempio Hello crea una scheda di rete denominata **myNic** toothe collegati che **mySubnet** subnet:

    ```azurecli
    az network nic create --resource-group myResourceGroup --location westus --name myNic \
        --vnet-name myVnet --subnet mySubnet --public-ip-address myPublicIP
    ```

## <a name="step-4-create-a-vm"></a>Passaggio 4: Creare una macchina virtuale

Ora è possibile creare una macchina virtuale usando il comando [az vm create](/cli/azure/vm#create).

Specificare hello copiato toouse gestito disco come disco del sistema operativo hello (-disco del sistema operativo collegare), come segue:

```azurecli
az vm create --resource-group myResourceGroup --name myCopiedVM \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics myNic --size Standard_DS1_v2 --os-type Linux \
    --attach-os-disk myCopiedDisk
```

## <a name="next-steps"></a>Passaggi successivi

toolearn come toouse CLI di Azure toomanage la nuova macchina virtuale, vedere [i comandi CLI di Azure per Gestione risorse di Azure hello](../azure-cli-arm-commands.md).
