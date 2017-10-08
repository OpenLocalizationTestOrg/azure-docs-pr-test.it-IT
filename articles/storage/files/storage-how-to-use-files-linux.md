---
title: archiviazione di File di Azure con Linux aaaUse | Documenti Microsoft
description: Informazioni su come toomount un File di Azure condividono su SMB in Linux.
services: storage
documentationcenter: na
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 6edc37ce-698f-4d50-8fc1-591ad456175d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/8/2017
ms.author: renash
ms.openlocfilehash: eeaa24b7f9e646724c5d86ae1e80dfdadaff34fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-file-storage-with-linux"></a>Usare l'archiviazione file di Azure con Linux
[Archiviazione di Azure File](../storage-dotnet-how-to-use-files.md) è facile toouse cloud file sistema Microsoft. Condivisioni File Azure possono essere installate nelle distribuzioni di Linux mediante hello [pacchetto cifs-utils](https://wiki.samba.org/index.php/LinuxCIFS_utils) da hello [progetto Samba](https://www.samba.org/). Questo articolo illustra due modi toomount una condivisione di File di Azure: su richiesta con hello `mount` comando e avvio creando una voce in `/etc/fstab`.

> [!NOTE]  
> In ordine toomount una condivisione di File di Azure di fuori di hello regione di Azure che è ospitato in, ad esempio in locale o in un'area diversa di Azure, hello del sistema operativo deve supportare la funzionalità di crittografia hello di SMB 3.0. La funzionalità di crittografia per SMB 3.0 per Linux è stata introdotta nel kernel 4.11. Questa funzionalità consente di montare la condivisione file di Azure in locale o in un'altra area di Azure. In fase di hello della pubblicazione, questa funzionalità è stata backported tooUbuntu da 16.04 e versioni successive.


## <a name="prerequisities-for-mounting-an-azure-file-share-with-linux-and-hello-cifs-utils-package"></a>Dei prerequisiti per il montaggio di una condivisione di File di Azure con Linux e hello pacchetto cifs-utils
* **Selezionare una distribuzione di Linux che può essere installato il pacchetto hello cifs-utils**: si consiglia di hello seguendo le distribuzioni di Linux nella raccolta di immagini di Azure hello:

    * Ubuntu Server 14.04+
    * RHEL 7+
    * CentOS 7+
    * Debian 8
    * openSUSE 13.2+
    * SUSE Linux Enterprise Server 12

* <a id="install-cifs-utils"></a>**Hello cifs-utils viene installato**: hello cifs-utils può essere installato usando Gestione pacchetti hello in distribuzioni di Linux hello di propria scelta. 

    In **Ubuntu** e **basato su Debian** distribuzioni, utilizzare hello `apt-get` Gestione pacchetti:

    ```
    sudo apt-get update
    sudo apt-get install cifs-utils
    ```

    In **RHEL** e **CentOS**, utilizzare hello `yum` Gestione pacchetti:

    ```
    sudo yum install samba-client samba-common cifs-utils
    ```

    In **openSUSE**, utilizzare hello `zypper` Gestione pacchetti:

    ```
    sudo zypper install samba*
    ```

    In altre distribuzioni, usare Gestione di pacchetti appropriato hello o [compilare dall'origine](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).

* **Scegliere le autorizzazioni di file e directory hello della condivisione montato hello**: esempio hello riportato di seguito, si usano 0777, toogive leggere, scrivere ed eseguire le autorizzazioni tooall utenti. È possibile sostituirlo con altre [autorizzazioni chmod](https://en.wikipedia.org/wiki/Chmod) in base alle proprie esigenze. 

* **Nome Account di archiviazione**: condividere un File di Azure toomount, si sarà necessario hello nome dell'account di archiviazione hello.

* **Chiave dell'Account di archiviazione**: condividere un File di Azure toomount, si sarà necessario hello chiave di archiviazione primaria (o secondario). Le chiavi di firma di accesso condiviso non sono attualmente supportate per il montaggio.

* **Verificare che sia aperta la porta 445**: SMB comunica sulla porta TCP 445 - controllare le porte toosee se il firewall non stia bloccando TCP 445 da computer client.

## <a name="mount-hello-azure-file-share-on-demand-with-mount"></a>Montare hello su richiesta con condivisione di File di Azure`mount`
1. **[Installare il pacchetto di cifs-utils hello per le distribuzioni di Linux](#install-cifs-utils)**.

2. **Creare una cartella per il punto di montaggio hello**: questa operazione può essere eseguita in un punto qualsiasi nel file system di hello.

    ```
    mkdir mymountpoint
    ```

3. **Condivisione File di Azure usare hello montaggio comando toomount hello**: ricordare tooreplace `<storage-account-name>`, `<share-name>`, e `<storage-account-key>` con le informazioni appropriate hello.

    ```
    sudo mount -t cifs //<storage-account-name>.file.core.windows.net/<share-name> ./mymountpoint -o vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino
    ```

> [!Note]  
> Al termine utilizzando hello condivisione File di Azure, è possibile utilizzare `sudo umount ./mymountpoint` condivisione hello toounmount.

## <a name="create-a-persistent-mount-point-for-hello-azure-file-share-with-etcfstab"></a>Creare un punto di montaggio permanente per la condivisione di File di Azure hello con`/etc/fstab`
1. **[Installare il pacchetto di cifs-utils hello per le distribuzioni di Linux](#install-cifs-utils)**.

2. **Creare una cartella per il punto di montaggio hello**: questa operazione può essere eseguita in un punto qualsiasi nel file system di hello, ma è necessario toonote hello di percorso assoluto della cartella hello. Hello di esempio seguente crea una cartella radice.

    ```
    sudo mkdir /mymountpoint
    ```

3. **Comando che segue di hello utilizzare hello tooappend successiva riga troppo`/etc/fstab`**: ricordare tooreplace `<storage-account-name>`, `<share-name>`, e `<storage-account-key>` con le informazioni appropriate hello.

    ```
    sudo bash -c 'echo "//<storage-account-name>.file.core.windows.net/<share-name> /mymountpoint cifs vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino" >> /etc/fstab'
    ```

> [!Note]  
> È possibile utilizzare `sudo mount -a` toomount hello Azure in una condivisione dopo la modifica `/etc/fstab` anziché in fase di riavvio.

## <a name="feedback"></a>Commenti e suggerimenti
Gli utenti Linux, desideriamo toohear da parte dell'utente.

archiviazione di File di Azure per il gruppo degli utenti Linux Hello forum dedicato a si tooshare feedback valutare e adottare l'archiviazione di File in Linux. Messaggio di posta elettronica [archiviazione di File di Azure utenti Linux](mailto:azurefileslinuxusers@microsoft.com) gruppo degli utenti di toojoin hello.

## <a name="next-steps"></a>Passaggi successivi
Vedere i collegamenti seguenti per ulteriori informazioni sull'archiviazione file di Azure.
* [Riferimento API REST del servizio File](http://msdn.microsoft.com/library/azure/dn167006.aspx)
* [Come toouse AzCopy con l'archiviazione di Microsoft Azure](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [Con l'archiviazione di Azure hello CLI di Azure](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)
* [Domande frequenti](../storage-files-faq.md)
* [Risoluzione dei problemi](storage-troubleshoot-linux-file-connection-problems.md)
