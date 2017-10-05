---
title: Montare l'archiviazione file di Azure su VM Linux usando SMB | Microsoft Docs
description: Come montare l'archiviazione file di Azure su VM Linux usando SMB con l'interfaccia della riga di comando di Azure 2.0
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
ms.openlocfilehash: 9eae17b304f8a987b44ebed8906dabd8ff3a36a8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="mount-azure-file-storage-on-linux-vms-using-smb"></a><span data-ttu-id="c0595-103">Montare l'archiviazione file di Azure su VM Linux usando SMB</span><span class="sxs-lookup"><span data-stu-id="c0595-103">Mount Azure File storage on Linux VMs using SMB</span></span>

<span data-ttu-id="c0595-104">Questo articolo descrive come usare il servizio di archiviazione file di Azure su una VM Linux usando un montaggio SMB con l'interfaccia della riga di comando di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="c0595-104">This article shows you how to utilize the Azure File storage service on a Linux VM using an SMB mount with the Azure CLI 2.0.</span></span> <span data-ttu-id="c0595-105">L'archiviazione file di Azure offre condivisioni file nel cloud usando il protocollo SMB standard.</span><span class="sxs-lookup"><span data-stu-id="c0595-105">Azure File storage offers file shares in the cloud using the standard SMB protocol.</span></span> <span data-ttu-id="c0595-106">È possibile anche eseguire questi passaggi tramite l'[interfaccia della riga di comando di Azure 1.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c0595-106">You can also perform these steps with the [Azure CLI 1.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="c0595-107">I requisiti sono:</span><span class="sxs-lookup"><span data-stu-id="c0595-107">The requirements are:</span></span>

- [<span data-ttu-id="c0595-108">Un account di Azure</span><span class="sxs-lookup"><span data-stu-id="c0595-108">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
- [<span data-ttu-id="c0595-109">File di chiavi SSH pubbliche e private</span><span class="sxs-lookup"><span data-stu-id="c0595-109">SSH public and private key files</span></span>](mac-create-ssh-keys.md)

## <a name="quick-commands"></a><span data-ttu-id="c0595-110">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="c0595-110">Quick Commands</span></span>

* <span data-ttu-id="c0595-111">Un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="c0595-111">A resource group</span></span>
* <span data-ttu-id="c0595-112">Una rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="c0595-112">An Azure virtual network</span></span>
* <span data-ttu-id="c0595-113">Un gruppo di sicurezza di rete con SSH in ingresso</span><span class="sxs-lookup"><span data-stu-id="c0595-113">A network security group with an SSH inbound</span></span>
* <span data-ttu-id="c0595-114">Una subnet</span><span class="sxs-lookup"><span data-stu-id="c0595-114">A subnet</span></span>
* <span data-ttu-id="c0595-115">Un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="c0595-115">An Azure storage account</span></span>
* <span data-ttu-id="c0595-116">Chiavi dell'account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="c0595-116">Azure storage account keys</span></span>
* <span data-ttu-id="c0595-117">Una condivisione di archiviazione file di Azure</span><span class="sxs-lookup"><span data-stu-id="c0595-117">An Azure File storage share</span></span>
* <span data-ttu-id="c0595-118">Una VM Linux</span><span class="sxs-lookup"><span data-stu-id="c0595-118">A Linux VM</span></span>

<span data-ttu-id="c0595-119">Sostituire gli esempi con le impostazioni desiderate.</span><span class="sxs-lookup"><span data-stu-id="c0595-119">Replace any examples with your own settings.</span></span>

### <a name="create-a-directory-for-the-local-mount"></a><span data-ttu-id="c0595-120">Creare una directory per il montaggio locale</span><span class="sxs-lookup"><span data-stu-id="c0595-120">Create a directory for the local mount</span></span>

```bash
mkdir -p /mnt/mymountpoint
```

### <a name="mount-the-file-storage-smb-share-to-the-mount-point"></a><span data-ttu-id="c0595-121">Montare la condivisione SMB di archiviazione file sul punto di montaggio</span><span class="sxs-lookup"><span data-stu-id="c0595-121">Mount the File storage SMB share to the mount point</span></span>

```bash
sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mymountpoint -o vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

### <a name="persist-the-mount-after-a-reboot"></a><span data-ttu-id="c0595-122">Rendere persistente il montaggio dopo un riavvio</span><span class="sxs-lookup"><span data-stu-id="c0595-122">Persist the mount after a reboot</span></span>
<span data-ttu-id="c0595-123">Per farlo, aggiungere la riga seguente a `/etc/fstab`:</span><span class="sxs-lookup"><span data-stu-id="c0595-123">To do so, add the following line to the `/etc/fstab`:</span></span>

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="c0595-124">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="c0595-124">Detailed walkthrough</span></span>

<span data-ttu-id="c0595-125">L'archiviazione file offre condivisioni file nel cloud che usano il protocollo SMB standard.</span><span class="sxs-lookup"><span data-stu-id="c0595-125">File storage offers file shares in the cloud that use the standard SMB protocol.</span></span> <span data-ttu-id="c0595-126">Con la versione più recente di archiviazione file è anche possibile montare una condivisione di file da un sistema operativo che supporta SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="c0595-126">With the latest release of File storage, you can also mount a file share from any OS that supports SMB 3.0.</span></span> <span data-ttu-id="c0595-127">Quando si usa un montaggio SMB in Linux è possibile eseguire facilmente copie di backup in un percorso di archiviazione affidabile e permanente supportato da un Contratto di servizio.</span><span class="sxs-lookup"><span data-stu-id="c0595-127">When you use an SMB mount on Linux, you get easy backups to a robust, permanent archiving storage location that is supported by an SLA.</span></span>

<span data-ttu-id="c0595-128">Lo spostamento di file da una VM a un montaggio SMB ospitato nell'archiviazione file è un ottimo modo per eseguire il debug dei log,</span><span class="sxs-lookup"><span data-stu-id="c0595-128">Moving files from a VM to an SMB mount that's hosted on File storage is a great way to debug logs.</span></span> <span data-ttu-id="c0595-129">dato che la stessa condivisione SMB può essere montata in locale in workstation Mac, Linux o Windows.</span><span class="sxs-lookup"><span data-stu-id="c0595-129">That's because the same SMB share can be mounted locally to your Mac, Linux, or Windows workstation.</span></span> <span data-ttu-id="c0595-130">SMB non è la soluzione migliore per eseguire lo streaming di log applicazioni o Linux in tempo reale perché il protocollo SMB non è stato creato per la gestione di attività di registrazione così impegnative.</span><span class="sxs-lookup"><span data-stu-id="c0595-130">SMB isn't the best solution for streaming Linux or application logs in real time, because the SMB protocol is not built to handle such heavy logging duties.</span></span> <span data-ttu-id="c0595-131">Per raccogliere l'output di log applicazioni o Linux è preferibile usare uno strumento dedicato con livello di registrazione unificato come Fluentd piuttosto che SMB.</span><span class="sxs-lookup"><span data-stu-id="c0595-131">A dedicated, unified logging layer tool such as Fluentd would be a better choice than SMB for collecting Linux and application logging output.</span></span>

<span data-ttu-id="c0595-132">Per questa procedura dettagliata vengono definiti i prerequisiti necessari prima per creare la condivisione di archiviazione file di Azure e quindi per montarla tramite SMB in una VM Linux.</span><span class="sxs-lookup"><span data-stu-id="c0595-132">For this detailed walkthrough, we create the prerequisites needed to first create the File storage share, and then mount it via SMB on a Linux VM.</span></span>

1. <span data-ttu-id="c0595-133">Creare un gruppo di risorse con [az group create](/cli/azure/group#create) per contenere la condivisione file.</span><span class="sxs-lookup"><span data-stu-id="c0595-133">Create a resource group with [az group create](/cli/azure/group#create) to hold the file share.</span></span>

    <span data-ttu-id="c0595-134">Per creare un gruppo di risorse denominato `myResourceGroup` nell'area "Stati Uniti occidentali" usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="c0595-134">To create a resource group named `myResourceGroup` in the "West US" location, use the following example:</span></span>

    ```azurecli
    az group create --name myResourceGroup --location westus
    ```

2. <span data-ttu-id="c0595-135">Creare un account di archiviazione di Azure con [az storage account create](/cli/azure/storage/account#create) per archiviare i file effettivi.</span><span class="sxs-lookup"><span data-stu-id="c0595-135">Create an Azure storage account with [az storage account create](/cli/azure/storage/account#create) to store the actual files.</span></span>

    <span data-ttu-id="c0595-136">Per creare un account di archiviazione denominato mystorageaccount usando SKU di archiviazione Standard_LRS, usare l'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="c0595-136">To create a storage account named mystorageaccount by using the Standard_LRS storage SKU, use the following example:</span></span>

    ```azurecli
    az storage account create --resource-group myResourceGroup \
        --name mystorageaccount \
        --location westus \
        --sku Standard_LRS
    ```

3. <span data-ttu-id="c0595-137">Visualizzare le chiavi dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="c0595-137">Show the storage account keys.</span></span>

    <span data-ttu-id="c0595-138">Quando si crea un account di archiviazione, le chiavi dell'account vengono create a coppie perché possano essere ruotate senza interrompere il servizio.</span><span class="sxs-lookup"><span data-stu-id="c0595-138">When you create a storage account, the account keys are created in pairs so that they can be rotated without any service interruption.</span></span> <span data-ttu-id="c0595-139">Quando si passa alla seconda chiave della coppia, viene creata una nuova coppia di chiavi.</span><span class="sxs-lookup"><span data-stu-id="c0595-139">When you switch to the second key in the pair, you create a new key pair.</span></span> <span data-ttu-id="c0595-140">Le nuove chiavi dell'account di archiviazione vengono sempre create a coppie in modo da avere sempre a disposizione almeno una chiave dell'account di archiviazione non usata alla quale passare.</span><span class="sxs-lookup"><span data-stu-id="c0595-140">New storage account keys are always created in pairs, ensuring that you always have at least one unused storage account key ready to switch to.</span></span>

    <span data-ttu-id="c0595-141">Usare [az storage account keys list](/cli/azure/storage/account/keys#list) per visualizzare le chiavi dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="c0595-141">View the storage account keys with the [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span> <span data-ttu-id="c0595-142">L'esempio seguente elenca le chiavi dell'account di archiviazione denominato `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="c0595-142">The storage account keys for the named `mystorageaccount` are listed in the following example:</span></span>

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount
    ```

    <span data-ttu-id="c0595-143">Per estrarre una singola chiave usare il flag `--query`.</span><span class="sxs-lookup"><span data-stu-id="c0595-143">To extract a single key, use the `--query` flag.</span></span> <span data-ttu-id="c0595-144">L'esempio seguente estrae la prima chiave (`[0]`):</span><span class="sxs-lookup"><span data-stu-id="c0595-144">The following example extracts the first key (`[0]`):</span></span>

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount \
        --query '[0].{Key:value}' --output tsv
    ```

4. <span data-ttu-id="c0595-145">Creare la condivisione di archiviazione file.</span><span class="sxs-lookup"><span data-stu-id="c0595-145">Create the File storage share.</span></span>

    <span data-ttu-id="c0595-146">La condivisione di archiviazione file contiene la condivisione SMB con [az storage share create](/cli/azure/storage/share#create).</span><span class="sxs-lookup"><span data-stu-id="c0595-146">The File storage share contains the SMB share with [az storage share create](/cli/azure/storage/share#create).</span></span> <span data-ttu-id="c0595-147">La quota è sempre espressa in gigabyte (GB).</span><span class="sxs-lookup"><span data-stu-id="c0595-147">The quota is always expressed in gigabytes (GB).</span></span> <span data-ttu-id="c0595-148">Passare a una delle chiavi dal comando precedente `az storage account keys list`.</span><span class="sxs-lookup"><span data-stu-id="c0595-148">Pass in one of the keys from the preceding `az storage account keys list` command.</span></span> <span data-ttu-id="c0595-149">Creare una condivisione denominata mystorageshare con una quota di 10 GB con l'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="c0595-149">Create a share named mystorageshare with a 10-GB quota by using the following example:</span></span>

    ```azurecli
    az storage share create --name mystorageshare \
        --quota 10 \
        --account-name mystorageaccount \
        --account-key nPOgPR<--snip-->4Q==
    ```

5. <span data-ttu-id="c0595-150">Creare una directory del punto di montaggio.</span><span class="sxs-lookup"><span data-stu-id="c0595-150">Create a mount-point directory.</span></span>

    <span data-ttu-id="c0595-151">Nel file system di Linux creare una directory locale nella quale montare la condivisione SMB.</span><span class="sxs-lookup"><span data-stu-id="c0595-151">Create a local directory in the Linux file system to mount the SMB share to.</span></span> <span data-ttu-id="c0595-152">Qualsiasi elemento scritto o letto dalla directory di montaggio locale viene inoltrato alla condivisione SMB ospitata nell'archiviazione file.</span><span class="sxs-lookup"><span data-stu-id="c0595-152">Anything written or read from the local mount directory is forwarded to the SMB share that's hosted on File storage.</span></span> <span data-ttu-id="c0595-153">Per creare una directory locale in /mnt/mymountdirectory, usare l'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="c0595-153">To create a local directory at /mnt/mymountdirectory, use the following example:</span></span>

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

6. <span data-ttu-id="c0595-154">Montare la condivisione SMB nella directory locale.</span><span class="sxs-lookup"><span data-stu-id="c0595-154">Mount the SMB share to the local directory.</span></span>

    <span data-ttu-id="c0595-155">Fornire il proprio nome utente dell'account di archiviazione e la chiave dell'account di archiviazione per le credenziali di montaggio nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="c0595-155">Provide your own storage account username and storage account key for the mount credentials as follows:</span></span>

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=mystorageaccount,password=mystorageaccountkey,dir_mode=0777,file_mode=0777
    ```

7. <span data-ttu-id="c0595-156">Mantenere il montaggio di SMB dopo il riavvio del sistema.</span><span class="sxs-lookup"><span data-stu-id="c0595-156">Persist the SMB mount through reboots.</span></span>

    <span data-ttu-id="c0595-157">Quando si riavvia la VM Linux, durante la fase di arresto viene smontata la condivisione SMB montata.</span><span class="sxs-lookup"><span data-stu-id="c0595-157">When you reboot the Linux VM, the mounted SMB share is unmounted during shutdown.</span></span> <span data-ttu-id="c0595-158">Per consentire il rimontaggio della condivisione SMB all'avvio, aggiungere una riga a /etc/fstab di Linux.</span><span class="sxs-lookup"><span data-stu-id="c0595-158">To remount the SMB share on boot, add a line to the Linux /etc/fstab.</span></span> <span data-ttu-id="c0595-159">Linux usa il file fstab per elencare i file system da montare durante la fase di avvio.</span><span class="sxs-lookup"><span data-stu-id="c0595-159">Linux uses the fstab file to list the file systems that it needs to mount during the boot process.</span></span> <span data-ttu-id="c0595-160">Aggiungendo la condivisione SMB si garantisce che la condivisione di archiviazione file costituisca un file system montato in modo permanente per la VM Linux.</span><span class="sxs-lookup"><span data-stu-id="c0595-160">Adding the SMB share ensures that the File storage share is a permanently mounted file system for the Linux VM.</span></span> <span data-ttu-id="c0595-161">L'aggiunta della condivisione SMB di archiviazione file in una nuova VM è possibile quando si usa cloud-init.</span><span class="sxs-lookup"><span data-stu-id="c0595-161">Adding the File storage SMB share to a new VM is possible when you use cloud-init.</span></span>

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a><span data-ttu-id="c0595-162">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c0595-162">Next steps</span></span>

- [<span data-ttu-id="c0595-163">Uso di cloud-init per personalizzare una VM Linux durante la creazione</span><span class="sxs-lookup"><span data-stu-id="c0595-163">Using cloud-init to customize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="c0595-164">Aggiungere un disco a una VM Linux</span><span class="sxs-lookup"><span data-stu-id="c0595-164">Add a disk to a Linux VM</span></span>](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="c0595-165">Crittografare i dischi di una VM Linux usando l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="c0595-165">Encrypt disks on a Linux VM by using the Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
