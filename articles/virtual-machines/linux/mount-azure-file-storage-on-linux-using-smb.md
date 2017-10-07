---
title: archiviazione di File di Azure nelle macchine virtuali Linux con SMB aaaMount | Documenti Microsoft
description: Come archiviazione di File di Azure nelle macchine virtuali Linux con SMB con toomount hello Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/13/2017
ms.author: v-livech
ms.openlocfilehash: 7b34c81e602748b78c924f44a54b876744c28f56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-storage-on-linux-vms-using-smb"></a>Montare l'archiviazione file di Azure su VM Linux usando SMB

Questo articolo illustra la modalità di montaggio hello tooutilize servizio di archiviazione di File di Azure in una VM Linux usando un protocollo SMB con hello CLI di Azure 2.0. Archiviazione di File di Azure offre le condivisioni di file in un cloud di hello tramite il protocollo SMB standard di hello. È anche possibile eseguire questi passaggi con hello [CLI di Azure 1.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). requisiti di Hello sono:

- [Un account di Azure](https://azure.microsoft.com/pricing/free-trial/)
- [File di chiavi SSH pubbliche e private](mac-create-ssh-keys.md)

## <a name="quick-commands"></a>Comandi rapidi

* Un gruppo di risorse
* Una rete virtuale di Azure
* Un gruppo di sicurezza di rete con SSH in ingresso
* Una subnet
* Un account di archiviazione di Azure
* Chiavi dell'account di archiviazione di Azure
* Una condivisione di archiviazione file di Azure
* Una VM Linux

Sostituire gli esempi con le impostazioni desiderate.

### <a name="create-a-directory-for-hello-local-mount"></a>Creare una directory di montaggio locale hello

```bash
mkdir -p /mnt/mymountpoint
```

### <a name="mount-hello-file-storage-smb-share-toohello-mount-point"></a>Punto di montaggio di hello File archiviazione SMB condivisione toohello di montaggio

```bash
sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mymountpoint -o vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

### <a name="persist-hello-mount-after-a-reboot"></a>Persistenza mount hello dopo il riavvio
toodo in tal caso, aggiungere hello seguente riga toohello `/etc/fstab`:

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a>Procedura dettagliata

Archiviazione di file offre le condivisioni file cloud hello che utilizzano il protocollo SMB standard di hello. Con una versione più recente di hello di archiviazione di File, è inoltre possibile collegare una condivisione file da qualsiasi sistema operativo che supporta SMB 3.0. Quando si utilizza un montaggio SMB su Linux, si ottiene backup semplice tooa affidabile e permanente archiviazione percorso di archiviazione supportata da un contratto di servizio.

Lo spostamento di file da un montaggio SMB tooan di macchina virtuale ospitata in archiviazione di File è che toodebug un ottimo modo Registra. Ciò accade perché hello condivisione SMB stesso può essere installato localmente tooyour workstation di Windows, Linux o Mac. SMB non è hello la soluzione migliore per lo streaming di Linux o registrata dall'applicazione in tempo reale, poiché il protocollo SMB hello non compilato toohandle loro registrazione elevato. Per raccogliere l'output di log applicazioni o Linux è preferibile usare uno strumento dedicato con livello di registrazione unificato come Fluentd piuttosto che SMB.

Per questa procedura dettagliata, è creare prerequisiti hello necessari toofirst creare la condivisione di archiviazione di File hello e quindi montare tramite SMB in una VM Linux.

1. Creare un gruppo di risorse con [gruppo az creare](/cli/azure/group#create) toohold condivisione di file hello.

    un gruppo di risorse denominato toocreate `myResourceGroup` nel percorso "Stati Uniti occidentali" hello, utilizzare hello di esempio seguente:

    ```azurecli
    az group create --name myResourceGroup --location westus
    ```

2. Creare un account di archiviazione di Azure con [creare account di archiviazione az](/cli/azure/storage/account#create) toostore hello file effettivi.

    toocreate un account di archiviazione denominato mystorageaccount utilizzando l'archiviazione Standard_LRS hello SKU, utilizzare hello esempio seguente:

    ```azurecli
    az storage account create --resource-group myResourceGroup \
        --name mystorageaccount \
        --location westus \
        --sku Standard_LRS
    ```

3. Mostra chiavi dell'account di archiviazione hello.

    Quando si crea un account di archiviazione, le chiavi dell'account hello vengono create in coppie, in modo che possono essere ruotate senza interruzione del servizio. Quando si passa toohello seconda chiave nella coppia hello, si crea una nuova coppia di chiavi. Nuove chiavi dell'account di archiviazione vengono sempre create in coppie, accertarsi di disporre sempre di almeno uno spazio di archiviazione inutilizzato account chiave pronto tooswitch per.

    Visualizzare le chiavi di account di archiviazione hello con hello [elenco di chiavi di account di archiviazione az](/cli/azure/storage/account/keys#list). chiavi di account di archiviazione per hello denominato Hello `mystorageaccount` sono elencati nel seguente esempio hello:

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount
    ```

    tooextract una sola chiave, utilizzare hello `--query` flag. esempio Hello estrae prima chiave hello (`[0]`):

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount \
        --query '[0].{Key:value}' --output tsv
    ```

4. Creare la condivisione di archiviazione di File hello.

    condivisione di File di archiviazione Hello contiene hello condivisione SMB con [creare la condivisione di archiviazione az](/cli/azure/storage/share#create). quota Hello è sempre espressa in gigabyte (GB). Passare una delle chiavi di hello dal precedente hello `az storage account keys list` comando. Creare una condivisione denominata mystorageshare con una quota di 10 GB con hello di esempio seguente:

    ```azurecli
    az storage share create --name mystorageshare \
        --quota 10 \
        --account-name mystorageaccount \
        --account-key nPOgPR<--snip-->4Q==
    ```

5. Creare una directory del punto di montaggio.

    Creare una directory locale in hello toomount hello Linux file system per di condivisione SMB. Qualsiasi elemento scritto o letto dalla directory di montaggio locale hello viene inoltrato toohello condivisione SMB ospitata in archiviazione di File. toocreate una directory locale in /mnt/Retention/ mymountdirectory, utilizzare hello esempio seguente:

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

6. Montaggio di directory locale toohello di hello condivisione SMB.

    Fornire il proprio nome utente account di archiviazione e chiave dell'account di archiviazione per le credenziali di montaggio hello nel modo seguente:

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=mystorageaccount,password=mystorageaccountkey,dir_mode=0777,file_mode=0777
    ```

7. Mantenere hello SMB montare il riavvio del sistema.

    Quando si riavvia hello VM Linux, hello montata condivisione SMB viene disinstallata durante l'arresto. hello tooremount condivisione SMB all'avvio del sistema, aggiungere un toohello riga /etc/fstab. Linux. Linux Usa hello fstab file toolist hello file System che deve toomount durante il processo di avvio hello. Aggiunta condivisione SMB di hello garantisce che la condivisione archiviazione File hello è un sistema di file montati in modo permanente per hello VM Linux. Aggiunta di hello File archiviazione SMB condivisione tooa nuova macchina virtuale è possibile quando si utilizza cloud init.

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a>Passaggi successivi

- [Utilizzo di cloud init toocustomize una VM Linux durante la creazione](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Aggiungere un tooa disco VM Linux](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Crittografare i dischi in una VM Linux con hello CLI di Azure](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
