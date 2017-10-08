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
# <a name="use-azure-file-storage-with-linux"></a><span data-ttu-id="d1ec1-103">Usare l'archiviazione file di Azure con Linux</span><span class="sxs-lookup"><span data-stu-id="d1ec1-103">Use Azure File storage with Linux</span></span>
<span data-ttu-id="d1ec1-104">[Archiviazione di Azure File](../storage-dotnet-how-to-use-files.md) è facile toouse cloud file sistema Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d1ec1-104">[Azure File storage](../storage-dotnet-how-to-use-files.md) is Microsoft's easy toouse cloud file system.</span></span> <span data-ttu-id="d1ec1-105">Condivisioni File Azure possono essere installate nelle distribuzioni di Linux mediante hello [pacchetto cifs-utils](https://wiki.samba.org/index.php/LinuxCIFS_utils) da hello [progetto Samba](https://www.samba.org/).</span><span class="sxs-lookup"><span data-stu-id="d1ec1-105">Azure File shares can be mounted in Linux distributions using hello [cifs-utils package](https://wiki.samba.org/index.php/LinuxCIFS_utils) from hello [Samba project](https://www.samba.org/).</span></span> <span data-ttu-id="d1ec1-106">Questo articolo illustra due modi toomount una condivisione di File di Azure: su richiesta con hello `mount` comando e avvio creando una voce in `/etc/fstab`.</span><span class="sxs-lookup"><span data-stu-id="d1ec1-106">This article shows two ways toomount an Azure File share: on-demand with hello `mount` command and on-boot by creating an entry in `/etc/fstab`.</span></span>

> [!NOTE]  
> <span data-ttu-id="d1ec1-107">In ordine toomount una condivisione di File di Azure di fuori di hello regione di Azure che è ospitato in, ad esempio in locale o in un'area diversa di Azure, hello del sistema operativo deve supportare la funzionalità di crittografia hello di SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="d1ec1-107">In order toomount an Azure File share outside of hello Azure region it is hosted in, such as on-premises or in a different Azure region, hello OS must support hello encryption functionality of SMB 3.0.</span></span> <span data-ttu-id="d1ec1-108">La funzionalità di crittografia per SMB 3.0 per Linux è stata introdotta nel kernel 4.11.</span><span class="sxs-lookup"><span data-stu-id="d1ec1-108">Encryption feature for SMB 3.0 for Linux was introduced in 4.11 kernel.</span></span> <span data-ttu-id="d1ec1-109">Questa funzionalità consente di montare la condivisione file di Azure in locale o in un'altra area di Azure.</span><span class="sxs-lookup"><span data-stu-id="d1ec1-109">This feature enables mounting of Azure File share from on-premises or a different Azure region.</span></span> <span data-ttu-id="d1ec1-110">In fase di hello della pubblicazione, questa funzionalità è stata backported tooUbuntu da 16.04 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="d1ec1-110">At hello time of publishing, this functionality has been backported tooUbuntu from 16.04 and above.</span></span>


## <a name="prerequisities-for-mounting-an-azure-file-share-with-linux-and-hello-cifs-utils-package"></a><span data-ttu-id="d1ec1-111">Dei prerequisiti per il montaggio di una condivisione di File di Azure con Linux e hello pacchetto cifs-utils</span><span class="sxs-lookup"><span data-stu-id="d1ec1-111">Prerequisities for mounting an Azure File share with Linux and hello cifs-utils package</span></span>
* <span data-ttu-id="d1ec1-112">**Selezionare una distribuzione di Linux che può essere installato il pacchetto hello cifs-utils**: si consiglia di hello seguendo le distribuzioni di Linux nella raccolta di immagini di Azure hello:</span><span class="sxs-lookup"><span data-stu-id="d1ec1-112">**Pick a Linux distribution that can have hello cifs-utils package installed**: Microsoft recommends hello following Linux distributions in hello Azure image gallery:</span></span>

    * <span data-ttu-id="d1ec1-113">Ubuntu Server 14.04+</span><span class="sxs-lookup"><span data-stu-id="d1ec1-113">Ubuntu Server 14.04+</span></span>
    * <span data-ttu-id="d1ec1-114">RHEL 7+</span><span class="sxs-lookup"><span data-stu-id="d1ec1-114">RHEL 7+</span></span>
    * <span data-ttu-id="d1ec1-115">CentOS 7+</span><span class="sxs-lookup"><span data-stu-id="d1ec1-115">CentOS 7+</span></span>
    * <span data-ttu-id="d1ec1-116">Debian 8</span><span class="sxs-lookup"><span data-stu-id="d1ec1-116">Debian 8</span></span>
    * <span data-ttu-id="d1ec1-117">openSUSE 13.2+</span><span class="sxs-lookup"><span data-stu-id="d1ec1-117">openSUSE 13.2+</span></span>
    * <span data-ttu-id="d1ec1-118">SUSE Linux Enterprise Server 12</span><span class="sxs-lookup"><span data-stu-id="d1ec1-118">SUSE Linux Enterprise Server 12</span></span>

* <span data-ttu-id="d1ec1-119"><a id="install-cifs-utils"></a>**Hello cifs-utils viene installato**: hello cifs-utils può essere installato usando Gestione pacchetti hello in distribuzioni di Linux hello di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="d1ec1-119"><a id="install-cifs-utils"></a>**hello cifs-utils package is installed**: hello cifs-utils can be installed using hello package manager on hello Linux distribution of your choice.</span></span> 

    <span data-ttu-id="d1ec1-120">In **Ubuntu** e **basato su Debian** distribuzioni, utilizzare hello `apt-get` Gestione pacchetti:</span><span class="sxs-lookup"><span data-stu-id="d1ec1-120">On **Ubuntu** and **Debian-based** distributions, use hello `apt-get` package manager:</span></span>

    ```
    sudo apt-get update
    sudo apt-get install cifs-utils
    ```

    <span data-ttu-id="d1ec1-121">In **RHEL** e **CentOS**, utilizzare hello `yum` Gestione pacchetti:</span><span class="sxs-lookup"><span data-stu-id="d1ec1-121">On **RHEL** and **CentOS**, use hello `yum` package manager:</span></span>

    ```
    sudo yum install samba-client samba-common cifs-utils
    ```

    <span data-ttu-id="d1ec1-122">In **openSUSE**, utilizzare hello `zypper` Gestione pacchetti:</span><span class="sxs-lookup"><span data-stu-id="d1ec1-122">On **openSUSE**, use hello `zypper` package manager:</span></span>

    ```
    sudo zypper install samba*
    ```

    <span data-ttu-id="d1ec1-123">In altre distribuzioni, usare Gestione di pacchetti appropriato hello o [compilare dall'origine](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).</span><span class="sxs-lookup"><span data-stu-id="d1ec1-123">On other distributions, use hello appropriate package manager or [compile from source](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).</span></span>

* <span data-ttu-id="d1ec1-124">**Scegliere le autorizzazioni di file e directory hello della condivisione montato hello**: esempio hello riportato di seguito, si usano 0777, toogive leggere, scrivere ed eseguire le autorizzazioni tooall utenti.</span><span class="sxs-lookup"><span data-stu-id="d1ec1-124">**Decide on hello directory/file permissions of hello mounted share**: In hello examples below, we use 0777, toogive read, write, and execute permissions tooall users.</span></span> <span data-ttu-id="d1ec1-125">È possibile sostituirlo con altre [autorizzazioni chmod](https://en.wikipedia.org/wiki/Chmod) in base alle proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="d1ec1-125">You can replace it with other [chmod permissions](https://en.wikipedia.org/wiki/Chmod) as desired.</span></span> 

* <span data-ttu-id="d1ec1-126">**Nome Account di archiviazione**: condividere un File di Azure toomount, si sarà necessario hello nome dell'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="d1ec1-126">**Storage Account Name**: toomount an Azure File share, you will need hello name of hello storage account.</span></span>

* <span data-ttu-id="d1ec1-127">**Chiave dell'Account di archiviazione**: condividere un File di Azure toomount, si sarà necessario hello chiave di archiviazione primaria (o secondario).</span><span class="sxs-lookup"><span data-stu-id="d1ec1-127">**Storage Account Key**: toomount an Azure File share, you will need hello primary (or secondary) storage key.</span></span> <span data-ttu-id="d1ec1-128">Le chiavi di firma di accesso condiviso non sono attualmente supportate per il montaggio.</span><span class="sxs-lookup"><span data-stu-id="d1ec1-128">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="d1ec1-129">**Verificare che sia aperta la porta 445**: SMB comunica sulla porta TCP 445 - controllare le porte toosee se il firewall non stia bloccando TCP 445 da computer client.</span><span class="sxs-lookup"><span data-stu-id="d1ec1-129">**Ensure port 445 is open**: SMB communicates over TCP port 445 - check toosee if your firewall is not blocking TCP ports 445 from client machine.</span></span>

## <a name="mount-hello-azure-file-share-on-demand-with-mount"></a><span data-ttu-id="d1ec1-130">Montare hello su richiesta con condivisione di File di Azure`mount`</span><span class="sxs-lookup"><span data-stu-id="d1ec1-130">Mount hello Azure File share on-demand with `mount`</span></span>
1. <span data-ttu-id="d1ec1-131">**[Installare il pacchetto di cifs-utils hello per le distribuzioni di Linux](#install-cifs-utils)**.</span><span class="sxs-lookup"><span data-stu-id="d1ec1-131">**[Install hello cifs-utils package for your Linux distribution](#install-cifs-utils)**.</span></span>

2. <span data-ttu-id="d1ec1-132">**Creare una cartella per il punto di montaggio hello**: questa operazione può essere eseguita in un punto qualsiasi nel file system di hello.</span><span class="sxs-lookup"><span data-stu-id="d1ec1-132">**Create a folder for hello mount point**: This can be done anywhere on hello file system.</span></span>

    ```
    mkdir mymountpoint
    ```

3. <span data-ttu-id="d1ec1-133">**Condivisione File di Azure usare hello montaggio comando toomount hello**: ricordare tooreplace `<storage-account-name>`, `<share-name>`, e `<storage-account-key>` con le informazioni appropriate hello.</span><span class="sxs-lookup"><span data-stu-id="d1ec1-133">**Use hello mount command toomount hello Azure File share**: Remember tooreplace `<storage-account-name>`, `<share-name>`, and `<storage-account-key>` with hello proper information.</span></span>

    ```
    sudo mount -t cifs //<storage-account-name>.file.core.windows.net/<share-name> ./mymountpoint -o vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino
    ```

> [!Note]  
> <span data-ttu-id="d1ec1-134">Al termine utilizzando hello condivisione File di Azure, è possibile utilizzare `sudo umount ./mymountpoint` condivisione hello toounmount.</span><span class="sxs-lookup"><span data-stu-id="d1ec1-134">When you are done using hello Azure File share, you may use `sudo umount ./mymountpoint` toounmount hello share.</span></span>

## <a name="create-a-persistent-mount-point-for-hello-azure-file-share-with-etcfstab"></a><span data-ttu-id="d1ec1-135">Creare un punto di montaggio permanente per la condivisione di File di Azure hello con`/etc/fstab`</span><span class="sxs-lookup"><span data-stu-id="d1ec1-135">Create a persistent mount point for hello Azure File share with `/etc/fstab`</span></span>
1. <span data-ttu-id="d1ec1-136">**[Installare il pacchetto di cifs-utils hello per le distribuzioni di Linux](#install-cifs-utils)**.</span><span class="sxs-lookup"><span data-stu-id="d1ec1-136">**[Install hello cifs-utils package for your Linux distribution](#install-cifs-utils)**.</span></span>

2. <span data-ttu-id="d1ec1-137">**Creare una cartella per il punto di montaggio hello**: questa operazione può essere eseguita in un punto qualsiasi nel file system di hello, ma è necessario toonote hello di percorso assoluto della cartella hello.</span><span class="sxs-lookup"><span data-stu-id="d1ec1-137">**Create a folder for hello mount point**: This can be done anywhere on hello file system, but you need toonote hello absolute path of hello folder.</span></span> <span data-ttu-id="d1ec1-138">Hello di esempio seguente crea una cartella radice.</span><span class="sxs-lookup"><span data-stu-id="d1ec1-138">hello following example creates a folder under root.</span></span>

    ```
    sudo mkdir /mymountpoint
    ```

3. <span data-ttu-id="d1ec1-139">**Comando che segue di hello utilizzare hello tooappend successiva riga troppo`/etc/fstab`**: ricordare tooreplace `<storage-account-name>`, `<share-name>`, e `<storage-account-key>` con le informazioni appropriate hello.</span><span class="sxs-lookup"><span data-stu-id="d1ec1-139">**Use hello following command tooappend hello following line too`/etc/fstab`**: Remember tooreplace `<storage-account-name>`, `<share-name>`, and `<storage-account-key>` with hello proper information.</span></span>

    ```
    sudo bash -c 'echo "//<storage-account-name>.file.core.windows.net/<share-name> /mymountpoint cifs vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino" >> /etc/fstab'
    ```

> [!Note]  
> <span data-ttu-id="d1ec1-140">È possibile utilizzare `sudo mount -a` toomount hello Azure in una condivisione dopo la modifica `/etc/fstab` anziché in fase di riavvio.</span><span class="sxs-lookup"><span data-stu-id="d1ec1-140">You can use `sudo mount -a` toomount hello Azure File share after editing `/etc/fstab` instead of rebooting.</span></span>

## <a name="feedback"></a><span data-ttu-id="d1ec1-141">Commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="d1ec1-141">Feedback</span></span>
<span data-ttu-id="d1ec1-142">Gli utenti Linux, desideriamo toohear da parte dell'utente.</span><span class="sxs-lookup"><span data-stu-id="d1ec1-142">Linux users, we want toohear from you!</span></span>

<span data-ttu-id="d1ec1-143">archiviazione di File di Azure per il gruppo degli utenti Linux Hello forum dedicato a si tooshare feedback valutare e adottare l'archiviazione di File in Linux.</span><span class="sxs-lookup"><span data-stu-id="d1ec1-143">hello Azure File storage for Linux users' group provides a forum for you tooshare feedback as you evaluate and adopt File storage on Linux.</span></span> <span data-ttu-id="d1ec1-144">Messaggio di posta elettronica [archiviazione di File di Azure utenti Linux](mailto:azurefileslinuxusers@microsoft.com) gruppo degli utenti di toojoin hello.</span><span class="sxs-lookup"><span data-stu-id="d1ec1-144">Email [Azure File storage Linux Users](mailto:azurefileslinuxusers@microsoft.com) toojoin hello users' group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1ec1-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d1ec1-145">Next steps</span></span>
<span data-ttu-id="d1ec1-146">Vedere i collegamenti seguenti per ulteriori informazioni sull'archiviazione file di Azure.</span><span class="sxs-lookup"><span data-stu-id="d1ec1-146">See these links for more information about Azure File storage.</span></span>
* [<span data-ttu-id="d1ec1-147">Riferimento API REST del servizio File</span><span class="sxs-lookup"><span data-stu-id="d1ec1-147">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
* [<span data-ttu-id="d1ec1-148">Come toouse AzCopy con l'archiviazione di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="d1ec1-148">How toouse AzCopy with Microsoft Azure storage</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [<span data-ttu-id="d1ec1-149">Con l'archiviazione di Azure hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="d1ec1-149">Using hello Azure CLI with Azure storage</span></span>](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)
* [<span data-ttu-id="d1ec1-150">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="d1ec1-150">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="d1ec1-151">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="d1ec1-151">Troubleshooting</span></span>](storage-troubleshoot-linux-file-connection-problems.md)
