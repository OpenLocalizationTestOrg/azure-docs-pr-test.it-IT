---
title: archiviazione di File di Azure nelle macchine virtuali Linux con SMB 1.0 CLI di Azure aaaMount | Documenti Microsoft
description: Come toomount archiviazione di File di Azure nelle macchine virtuali Linux tramite SMB
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
ms.date: 12/07/2016
ms.author: v-livech
ms.openlocfilehash: 14a4224228cadb0ae2f05e8e5c8022ee84f138a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-storage-on-linux-vms-by-using-smb-with-azure-cli-10"></a>Montare Archiviazione file di Azure in VM Linux usando SMB con l'interfaccia della riga di comando di Azure 1.0

Questo articolo illustra come archiviazione di File di Azure in una VM Linux utilizzando toomount hello protocollo Server Message Block (SMB). Archiviazione di file offre le condivisioni file nel cloud hello tramite il protocollo SMB standard di hello. requisiti di Hello sono:

* Un [account Azure](https://azure.microsoft.com/pricing/free-trial/)
* [File di chiavi pubbliche e private Secure Shell (SSH)](mac-create-ssh-keys.md)

## <a name="cli-versions-toouse"></a>Toouse di versioni CLI
È possibile completare l'attività hello utilizzando una delle seguenti versioni di interfaccia della riga di comando (CLI) hello:

- [Azure CLI 1.0](#quick-commands) : l'interfaccia CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)
- [Azure CLI 2.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)-la prossima generazione CLI per modello di distribuzione di gestione risorse hello


## <a name="quick-commands"></a>Comandi rapidi
attività hello tooaccomplish rapidamente, procedura hello in questa sezione. Per ulteriori informazioni e il contesto, iniziare in corrispondenza di hello ["Procedura dettagliata"](mount-azure-file-storage-on-linux-using-smb.md#detailed-walkthrough) sezione.

### <a name="prerequisites"></a>Prerequisiti
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
Aggiungere hello successiva riga troppo`/etc/fstab`:

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a>Procedura dettagliata

Archiviazione di file offre le condivisioni file cloud hello che utilizzano il protocollo SMB standard di hello. Con una versione più recente di hello di archiviazione di File, è inoltre possibile collegare una condivisione file da qualsiasi sistema operativo che supporta SMB 3.0. Quando si utilizza un montaggio SMB su Linux, si ottiene backup semplice tooa affidabile e permanente archiviazione percorso di archiviazione supportata da un contratto di servizio.

Lo spostamento di file da un montaggio SMB tooan di macchina virtuale ospitata in archiviazione di File è che toodebug un ottimo modo Registra. Ciò accade perché hello condivisione SMB stesso può essere installato localmente tooyour workstation di Windows, Linux o Mac. SMB non è hello la soluzione migliore per lo streaming di Linux o registrata dall'applicazione in tempo reale, poiché il protocollo SMB hello non compilato toohandle loro registrazione elevato. Per raccogliere l'output di log applicazioni o Linux è preferibile usare uno strumento dedicato con livello di registrazione unificato come Fluentd piuttosto che SMB.

Per questa procedura dettagliata, è creare prerequisiti hello necessari toofirst creare la condivisione di archiviazione di File hello e quindi montare tramite SMB in una VM Linux.

1. Creare un account di archiviazione di Azure utilizzando hello seguente codice:

    ```azurecli
    azure storage account create myStorageAccount \
    --sku-name lrs \
    --kind storage \
    -l westus \
    -g myResourceGroup
    ```

2. Mostra chiavi dell'account di archiviazione hello.

    Quando si crea un account di archiviazione, le chiavi dell'account hello vengono create in coppie, in modo che possono essere ruotate senza interruzione del servizio. Quando si passa toohello seconda chiave nella coppia hello, si crea una nuova coppia di chiavi. Nuove chiavi dell'account di archiviazione vengono sempre create in coppie, accertarsi di disporre sempre di almeno uno spazio di archiviazione inutilizzato di tooswitch pronto chiave per. chiavi dell'account di archiviazione hello tooshow, utilizzare hello seguente codice:

    ```azurecli
    azure storage account keys list myStorageAccount \
    --resource-group myResourceGroup
    ```
3. Creare la condivisione di archiviazione di File hello.

    condivisione di File di archiviazione Hello contiene una condivisione SMB hello. quota Hello è sempre espressa in gigabyte (GB). toocreate hello condivisione File di archiviazione, usare hello seguente codice:

    ```azurecli
    azure storage share create mystorageshare \
    --quota 10 \
    --account-name myStorageAccount \
    --account-key nPOgPR<--snip-->4Q==
    ```

4. Creare la directory di punto di montaggio hello.

    È necessario creare una directory locale in hello toomount hello Linux file system per di condivisione SMB. Qualsiasi elemento scritto o letto dalla directory di montaggio locale hello viene inoltrato toohello condivisione SMB ospitata in archiviazione di File. directory di hello toocreate, utilizzare hello seguente codice:

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

5. Montare hello condivisione SMB tramite hello seguente codice:

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=myStorageAccount,password=myStorageAccountkey,dir_mode=0777,file_mode=0777
    ```

6. Mantenere hello SMB montare il riavvio del sistema.

    Quando si riavvia hello VM Linux, hello montata condivisione SMB viene disinstallata durante l'arresto. condivisione SMB di tooremount hello all'avvio del sistema, è necessario aggiungere un toohello riga /etc/fstab. Linux. Linux Usa hello fstab file toolist hello file System che deve toomount durante il processo di avvio hello. Aggiunta condivisione SMB di hello garantisce che la condivisione archiviazione File hello è un sistema di file montati in modo permanente per hello VM Linux. Aggiunta di hello File archiviazione SMB condivisione tooa nuova macchina virtuale è possibile quando si utilizza cloud init.

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a>Passaggi successivi

- [Utilizzo di cloud init toocustomize una VM Linux durante la creazione](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Aggiungere un tooa disco VM Linux](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Crittografare i dischi in una VM Linux con hello CLI di Azure](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
