---
title: Usare l'archiviazione file di Azure con Linux | Microsoft Docs
description: Informazioni su come montare una condivisione file di Azure tramite SMB in Linux.
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
ms.openlocfilehash: 27b393a899c60a3a0393619f338a396dff659498
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="use-azure-file-storage-with-linux"></a><span data-ttu-id="8f446-103">Usare l'archiviazione file di Azure con Linux</span><span class="sxs-lookup"><span data-stu-id="8f446-103">Use Azure File storage with Linux</span></span>
<span data-ttu-id="8f446-104">[Archiviazione file di Azure](storage-dotnet-how-to-use-files.md) è il file system cloud facile da usare di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8f446-104">[Azure File storage](storage-dotnet-how-to-use-files.md) is Microsoft's easy to use cloud file system.</span></span> <span data-ttu-id="8f446-105">Le condivisioni file di Azure possono essere montate nelle distribuzioni di Linux usando il [pacchetto cifs-utils](https://wiki.samba.org/index.php/LinuxCIFS_utils) dal [progetto Samba](https://www.samba.org/).</span><span class="sxs-lookup"><span data-stu-id="8f446-105">Azure File shares can be mounted in Linux distributions using the [cifs-utils package](https://wiki.samba.org/index.php/LinuxCIFS_utils) from the [Samba project](https://www.samba.org/).</span></span> <span data-ttu-id="8f446-106">Questo articolo illustra due modi per montare una condivisione file di Azure: su richiesta con il comando `mount` e all'avvio creando una voce in `/etc/fstab`.</span><span class="sxs-lookup"><span data-stu-id="8f446-106">This article shows two ways to mount an Azure File share: on-demand with the `mount` command and on-boot by creating an entry in `/etc/fstab`.</span></span>

> [!NOTE]  
> <span data-ttu-id="8f446-107">Per montare una condivisione file di Azure al di fuori dell'area di Azure in cui è ospitata, ad esempio in locale o in un'area di Azure diversa, il sistema operativo deve supportare la funzionalità di crittografia di SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="8f446-107">In order to mount an Azure File share outside of the Azure region it is hosted in, such as on-premises or in a different Azure region, the OS must support the encryption functionality of SMB 3.0.</span></span> <span data-ttu-id="8f446-108">La funzionalità di crittografia per SMB 3.0 per Linux è stata introdotta nel kernel 4.11.</span><span class="sxs-lookup"><span data-stu-id="8f446-108">Encryption feature for SMB 3.0 for Linux was introduced in 4.11 kernel.</span></span> <span data-ttu-id="8f446-109">Questa funzionalità consente di montare la condivisione file di Azure in locale o in un'altra area di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f446-109">This feature enables mounting of Azure File share from on-premises or a different Azure region.</span></span> <span data-ttu-id="8f446-110">Al momento della pubblicazione, di questa funzionalità è stato eseguito il backport in Ubuntu 16.04 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="8f446-110">At the time of publishing, this functionality has been backported to Ubuntu from 16.04 and above.</span></span>


## <a name="prerequisities-for-mounting-an-azure-file-share-with-linux-and-the-cifs-utils-package"></a><span data-ttu-id="8f446-111">Prerequisiti per il montaggio di una condivisione file di Azure con Linux e il pacchetto cifs-utils</span><span class="sxs-lookup"><span data-stu-id="8f446-111">Prerequisities for mounting an Azure File share with Linux and the cifs-utils package</span></span>
* <span data-ttu-id="8f446-112">**Selezionare una distribuzione Linux in cui sia possibile installare il pacchetto cifs-utils**: Microsoft consiglia le distribuzioni Linux seguenti nella raccolta immagini di Azure:</span><span class="sxs-lookup"><span data-stu-id="8f446-112">**Pick a Linux distribution that can have the cifs-utils package installed**: Microsoft recommends the following Linux distributions in the Azure image gallery:</span></span>

    * <span data-ttu-id="8f446-113">Ubuntu Server 14.04+</span><span class="sxs-lookup"><span data-stu-id="8f446-113">Ubuntu Server 14.04+</span></span>
    * <span data-ttu-id="8f446-114">RHEL 7+</span><span class="sxs-lookup"><span data-stu-id="8f446-114">RHEL 7+</span></span>
    * <span data-ttu-id="8f446-115">CentOS 7+</span><span class="sxs-lookup"><span data-stu-id="8f446-115">CentOS 7+</span></span>
    * <span data-ttu-id="8f446-116">Debian 8</span><span class="sxs-lookup"><span data-stu-id="8f446-116">Debian 8</span></span>
    * <span data-ttu-id="8f446-117">openSUSE 13.2+</span><span class="sxs-lookup"><span data-stu-id="8f446-117">openSUSE 13.2+</span></span>
    * <span data-ttu-id="8f446-118">SUSE Linux Enterprise Server 12</span><span class="sxs-lookup"><span data-stu-id="8f446-118">SUSE Linux Enterprise Server 12</span></span>

* <span data-ttu-id="8f446-119"><a id="install-cifs-utils"></a>**Il pacchetto cifs-utils è installato**: il pacchetto cifs-utils può essere installato tramite l'utilità di gestione dei pacchetti nella distribuzione Linux scelta.</span><span class="sxs-lookup"><span data-stu-id="8f446-119"><a id="install-cifs-utils"></a>**The cifs-utils package is installed**: The cifs-utils can be installed using the package manager on the Linux distribution of your choice.</span></span> 

    <span data-ttu-id="8f446-120">Nelle distribuzioni basate su **Ubuntu** e **Debian** usare l'utilità di gestione dei pacchetti `apt-get`:</span><span class="sxs-lookup"><span data-stu-id="8f446-120">On **Ubuntu** and **Debian-based** distributions, use the `apt-get` package manager:</span></span>

    ```
    sudo apt-get update
    sudo apt-get install cifs-utils
    ```

    <span data-ttu-id="8f446-121">In **RHEL** e **CentOS** usare l'utilità di gestione dei pacchetti `yum`:</span><span class="sxs-lookup"><span data-stu-id="8f446-121">On **RHEL** and **CentOS**, use the `yum` package manager:</span></span>

    ```
    sudo yum install samba-client samba-common cifs-utils
    ```

    <span data-ttu-id="8f446-122">In **openSUSE** usare l'utilità di gestione dei pacchetti `zypper`:</span><span class="sxs-lookup"><span data-stu-id="8f446-122">On **openSUSE**, use the `zypper` package manager:</span></span>

    ```
    sudo zypper install samba*
    ```

    <span data-ttu-id="8f446-123">In altre distribuzioni usare l'utilità di gestione dei pacchetti appropriata o [compilare il codice sorgente](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).</span><span class="sxs-lookup"><span data-stu-id="8f446-123">On other distributions, use the appropriate package manager or [compile from source](https://wiki.samba.org/index.php/LinuxCIFS_utils#Download).</span></span>

* <span data-ttu-id="8f446-124">**Scegliere le autorizzazioni per le directory e i file della condivisione montata**: negli esempi seguenti viene usato 0777 per concedere le autorizzazioni di lettura, scrittura ed esecuzione a tutti gli utenti.</span><span class="sxs-lookup"><span data-stu-id="8f446-124">**Decide on the directory/file permissions of the mounted share**: In the examples below, we use 0777, to give read, write, and execute permissions to all users.</span></span> <span data-ttu-id="8f446-125">È possibile sostituirlo con altre [autorizzazioni chmod](https://en.wikipedia.org/wiki/Chmod) in base alle proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="8f446-125">You can replace it with other [chmod permissions](https://en.wikipedia.org/wiki/Chmod) as desired.</span></span> 

* <span data-ttu-id="8f446-126">**Nome dell'account di archiviazione**: per montare una condivisione file di Azure, sarà necessario il nome dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="8f446-126">**Storage Account Name**: To mount an Azure File share, you will need the name of the storage account.</span></span>

* <span data-ttu-id="8f446-127">**Chiave dell'account di archiviazione**: per montare una condivisione file di Azure, sarà necessaria la chiave dell'account primaria (o secondaria).</span><span class="sxs-lookup"><span data-stu-id="8f446-127">**Storage Account Key**: To mount an Azure File share, you will need the primary (or secondary) storage key.</span></span> <span data-ttu-id="8f446-128">Le chiavi di firma di accesso condiviso non sono attualmente supportate per il montaggio.</span><span class="sxs-lookup"><span data-stu-id="8f446-128">SAS keys are not currently supported for mounting.</span></span>

* <span data-ttu-id="8f446-129">**Assicurarsi che la porta 445 sia aperta**: SMB comunica tramite la porta TCP 445. Verificare che il firewall non blocchi le porte TCP 445 dal computer client.</span><span class="sxs-lookup"><span data-stu-id="8f446-129">**Ensure port 445 is open**: SMB communicates over TCP port 445 - check to see if your firewall is not blocking TCP ports 445 from client machine.</span></span>

## <a name="mount-the-azure-file-share-on-demand-with-mount"></a><span data-ttu-id="8f446-130">Montare la condivisione file di Azure su richiesta con `mount`</span><span class="sxs-lookup"><span data-stu-id="8f446-130">Mount the Azure File share on-demand with `mount`</span></span>
1. <span data-ttu-id="8f446-131">**[Installare il pacchetto cifs-utils per la distribuzione Linux](#install-cifs-utils)**.</span><span class="sxs-lookup"><span data-stu-id="8f446-131">**[Install the cifs-utils package for your Linux distribution](#install-cifs-utils)**.</span></span>

2. <span data-ttu-id="8f446-132">**Creare una cartella per il punto di montaggio**: questa operazione può essere eseguita in qualsiasi posizione nel file system.</span><span class="sxs-lookup"><span data-stu-id="8f446-132">**Create a folder for the mount point**: This can be done anywhere on the file system.</span></span>

    ```
    mkdir mymountpoint
    ```

3. <span data-ttu-id="8f446-133">**Usare il comando mount per montare la condivisione file di Azure**: ricordarsi di sostituire `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, con le informazioni appropriate.</span><span class="sxs-lookup"><span data-stu-id="8f446-133">**Use the mount command to mount the Azure File share**: Remember to replace `<storage-account-name>`, `<share-name>`, and `<storage-account-key>` with the proper information.</span></span>

    ```
    sudo mount -t cifs //<storage-account-name>.file.core.windows.net/<share-name> ./mymountpoint -o vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino
    ```

> [!Note]  
> <span data-ttu-id="8f446-134">Dopo che la condivisione file di Azure è stata completata, è possibile usare `sudo umount ./mymountpoint` per smontare la condivisione.</span><span class="sxs-lookup"><span data-stu-id="8f446-134">When you are done using the Azure File share, you may use `sudo umount ./mymountpoint` to unmount the share.</span></span>

## <a name="create-a-persistent-mount-point-for-the-azure-file-share-with-etcfstab"></a><span data-ttu-id="8f446-135">Creare un punto di montaggio permanente per la condivisione file di Azure con `/etc/fstab`</span><span class="sxs-lookup"><span data-stu-id="8f446-135">Create a persistent mount point for the Azure File share with `/etc/fstab`</span></span>
1. <span data-ttu-id="8f446-136">**[Installare il pacchetto cifs-utils per la distribuzione Linux](#install-cifs-utils)**.</span><span class="sxs-lookup"><span data-stu-id="8f446-136">**[Install the cifs-utils package for your Linux distribution](#install-cifs-utils)**.</span></span>

2. <span data-ttu-id="8f446-137">**Creare una cartella per il punto di montaggio**: questa operazione può essere eseguita in qualsiasi posizione nel file system, ma è necessario prendere nota del percorso assoluto della cartella.</span><span class="sxs-lookup"><span data-stu-id="8f446-137">**Create a folder for the mount point**: This can be done anywhere on the file system, but you need to note the absolute path of the folder.</span></span> <span data-ttu-id="8f446-138">L'esempio seguente crea una cartella nella radice.</span><span class="sxs-lookup"><span data-stu-id="8f446-138">The following example creates a folder under root.</span></span>

    ```
    sudo mkdir /mymountpoint
    ```

3. <span data-ttu-id="8f446-139">**Usare il comando seguente per accodare la riga seguente a `/etc/fstab`: ricordarsi di sostituire** , `<storage-account-name>`, `<share-name>`, `<storage-account-key>` con le informazioni appropriate.</span><span class="sxs-lookup"><span data-stu-id="8f446-139">**Use the following command to append the following line to `/etc/fstab`**: Remember to replace `<storage-account-name>`, `<share-name>`, and `<storage-account-key>` with the proper information.</span></span>

    ```
    sudo bash -c 'echo "//<storage-account-name>.file.core.windows.net/<share-name> /mymountpoint cifs vers=3.0,username=<storage-account-name>,password=<storage-account-key>,dir_mode=0777,file_mode=0777,serverino" >> /etc/fstab'
    ```

> [!Note]  
> <span data-ttu-id="8f446-140">Per montare la condivisione file di Azure dopo la modifica, è possibile usare `sudo mount -a` `/etc/fstab` anziché riavviare il computer.</span><span class="sxs-lookup"><span data-stu-id="8f446-140">You can use `sudo mount -a` to mount the Azure File share after editing `/etc/fstab` instead of rebooting.</span></span>

## <a name="feedback"></a><span data-ttu-id="8f446-141">Commenti e suggerimenti</span><span class="sxs-lookup"><span data-stu-id="8f446-141">Feedback</span></span>
<span data-ttu-id="8f446-142">Siamo interessati all'opinione degli utenti Linux.</span><span class="sxs-lookup"><span data-stu-id="8f446-142">Linux users, we want to hear from you!</span></span>

<span data-ttu-id="8f446-143">L'archiviazione di file di Azure per il gruppo di utenti Linux fornisce un forum per condividere commenti e suggerimenti durante la valutazione e l'adozione dell'archiviazione di file su Linux.</span><span class="sxs-lookup"><span data-stu-id="8f446-143">The Azure File storage for Linux users' group provides a forum for you to share feedback as you evaluate and adopt File storage on Linux.</span></span> <span data-ttu-id="8f446-144">Inviare un messaggio di posta elettronica ad [Azure File storage Linux Users](mailto:azurefileslinuxusers@microsoft.com) per entrare nel gruppo degli utenti.</span><span class="sxs-lookup"><span data-stu-id="8f446-144">Email [Azure File storage Linux Users](mailto:azurefileslinuxusers@microsoft.com) to join the users' group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f446-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8f446-145">Next steps</span></span>
<span data-ttu-id="8f446-146">Vedere i collegamenti seguenti per ulteriori informazioni sull'archiviazione file di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f446-146">See these links for more information about Azure File storage.</span></span>
* [<span data-ttu-id="8f446-147">Riferimento API REST del servizio File</span><span class="sxs-lookup"><span data-stu-id="8f446-147">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)
* [<span data-ttu-id="8f446-148">Uso di Azure PowerShell con Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="8f446-148">Using Azure PowerShell with Azure storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="8f446-149">Come usare AzCopy con Archiviazione di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="8f446-149">How to use AzCopy with Microsoft Azure storage</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="8f446-150">Uso dell'interfaccia della riga di comando di Azure con Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="8f446-150">Using the Azure CLI with Azure storage</span></span>](storage-azure-cli.md#create-and-manage-file-shares)
* [<span data-ttu-id="8f446-151">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="8f446-151">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="8f446-152">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="8f446-152">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)
