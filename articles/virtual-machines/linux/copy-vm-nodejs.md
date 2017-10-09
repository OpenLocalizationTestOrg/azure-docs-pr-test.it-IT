---
title: una copia della VM Linux con hello Azure CLI 1.0 aaaCreate | Documenti Microsoft
description: Informazioni su come toocreate una copia della macchina virtuale Linux di Azure con hello Azure CLI 1.0 nel modello di distribuzione di gestione risorse di hello
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 997a2c8109e7083ececd76fd1013e9ed4d3e6afd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-linux-virtual-machine-running-on-azure-with-hello-azure-cli-10"></a>Creare una copia di una macchina virtuale di Linux in esecuzione in Azure con hello Azure CLI 1.0
In questo articolo viene illustrato come una copia della macchina virtuale di Azure (VM) in esecuzione Linux utilizzando toocreate hello il modello di distribuzione di gestione risorse. Innanzitutto copiato hello del sistema operativo e dischi tooa nuovo contenitore di dati, quindi impostare le risorse di rete hello e creare hello nuova macchina virtuale.

È anche possibile [caricare e creare una VM da un'immagine disco personalizzata](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="cli-versions-toocomplete-hello-task"></a>Attività hello toocomplete versioni CLI
È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:

- CLI di Azure 1.0-nostri CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)
- [Azure CLI 2.0](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello

## <a name="before-you-begin"></a>Prima di iniziare
Verificare che siano soddisfatti i seguenti prerequisiti prima di iniziare i passaggi di hello hello:

* Si dispone di hello [CLI di Azure](../../cli-install-nodejs.md) scaricato e installato nel computer. 
* Sono anche necessarie alcune informazioni sulla VM Linux di Azure esistente:

| Informazioni sulla VM di origine | Dove tooget è |
| --- | --- |
| Nome della VM. |`azure vm list` |
| Nome del gruppo di risorse |`azure vm list` |
| Location |`azure vm list` |
| Nome dell'account di archiviazione |`azure storage account list -g <resourceGroup>` |
| Nome del contenitore |`azure storage container list -a <sourcestorageaccountname>` |
| Nome del file VHD della VM di origine |`azure storage blob list --container <containerName>` |

* È necessario toomake elencate alcune scelte sulla nuova macchina virtuale:   <br> -Nome contenitore    <br> -Nome della VM    <br> -Dimensioni della VM    <br> -Nome della vNet    <br> -Nome della SubNet    <br> -Nome dell'IP    <br> -Nome NIC

## <a name="login-and-set-your-subscription"></a>Effettuare l'accesso e impostare la sottoscrizione
1. Account di accesso toohello CLI.

    ```azurecli
    azure login
    ```
2. Verificare di essere in modalità Resource Manager.

    ```azurecli
    azure config mode arm
    ```
3. Impostare la sottoscrizione corretta hello. È possibile utilizzare 'elenco di account di azure' toosee tutte le sottoscrizioni.

    ```azurecli
    azure account set mySubscriptionID
    ```

## <a name="stop-hello-vm"></a>Arrestare VM hello
Arrestare e deallocare una macchina virtuale di origine hello. È possibile utilizzare 'elenco di macchine virtuali di azure' tooget un elenco di tutte le macchine virtuali hello nella sottoscrizione e i relativi nomi di gruppo di risorse.

```azurecli
azure vm stop myResourceGroup myVM
azure vm deallocate myResourceGroup MyVM
```


## <a name="copy-hello-vhd"></a>Copiare hello disco rigido virtuale
È possibile copiare hello VHD hello origine archiviazione toohello di destinazione utilizzando hello `azure storage blob copy start`. In questo esempio verrà toocopy hello VHD toohello stesso account di archiviazione, ma un contenitore diverso.

toocopy hello VHD tooanother contenitore hello stesso account di archiviazione, digitare:

```azurecli
azure storage blob copy start \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd \
        myNewContainerName
```

## <a name="set-up-hello-virtual-network-for-your-new-vm"></a>Configurare la rete virtuale di hello per la nuova macchina virtuale
Configurare una rete virtuale e una scheda NIC per la nuova VM. 

```azurecli
azure network vnet create myResourceGroup myVnet -l myLocation

azure network vnet subnet create -a <address.prefix.in.CIDR/format> myResourceGroup myVnet mySubnet

azure network public-ip create myResourceGroup myPublicIP -l myLocation

azure network nic create myResourceGroup myNic -k mySubnet -m myVnet -p myPublicIP -l myLocation
```


## <a name="create-hello-new-vm"></a>Creare hello nuova macchina virtuale
È ora possibile creare una macchina virtuale dal disco virtuale caricato [utilizzando un modello di gestione risorse](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) o tramite hello CLI specificando hello URI tooyour disco copiato digitando:

```azurecli
azure vm create -n myVM -l myLocation -g myResourceGroup -f myNic \
        -z Standard_DS1_v2 -y Linux \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd 
```



## <a name="next-steps"></a>Passaggi successivi
toolearn come toouse CLI di Azure toomanage nuova macchina virtuale, vedere [i comandi CLI di Azure per Gestione risorse di Azure hello](../azure-cli-arm-commands.md).

