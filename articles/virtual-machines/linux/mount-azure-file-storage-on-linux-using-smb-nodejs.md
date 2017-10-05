---
title: Montare Archiviazione file di Azure in VM Linux usando SMB con l'interfaccia della riga di comando di Azure 1.0 | Microsoft Docs
description: Come montare Archiviazione file di Azure in VM Linux usando SMB
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
ms.openlocfilehash: 4951860630f0aad107d0846d52ebe4423ee0b91c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="mount-azure-file-storage-on-linux-vms-by-using-smb-with-azure-cli-10"></a><span data-ttu-id="336b7-103">Montare Archiviazione file di Azure in VM Linux usando SMB con l'interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="336b7-103">Mount Azure File storage on Linux VMs by using SMB with Azure CLI 1.0</span></span>

<span data-ttu-id="336b7-104">Questo articolo illustra come montare Archiviazione file di Azure in una VM Linux usando il protocollo Server Message Block (SMB).</span><span class="sxs-lookup"><span data-stu-id="336b7-104">This article shows how to mount Azure File storage on a Linux VM by using the Server Message Block (SMB) protocol.</span></span> <span data-ttu-id="336b7-105">Archiviazione file offre condivisioni file nel cloud tramite il protocollo SMB standard.</span><span class="sxs-lookup"><span data-stu-id="336b7-105">File storage offers file shares in the cloud via the standard SMB protocol.</span></span> <span data-ttu-id="336b7-106">I requisiti sono:</span><span class="sxs-lookup"><span data-stu-id="336b7-106">The requirements are:</span></span>

* <span data-ttu-id="336b7-107">Un [account Azure](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="336b7-107">An [Azure account](https://azure.microsoft.com/pricing/free-trial/)</span></span>
* [<span data-ttu-id="336b7-108">File di chiavi pubbliche e private Secure Shell (SSH)</span><span class="sxs-lookup"><span data-stu-id="336b7-108">Secure Shell (SSH) public and private key files</span></span>](mac-create-ssh-keys.md)

## <a name="cli-versions-to-use"></a><span data-ttu-id="336b7-109">Versioni dell'interfaccia della riga di comando da usare</span><span class="sxs-lookup"><span data-stu-id="336b7-109">CLI versions to use</span></span>
<span data-ttu-id="336b7-110">È possibile completare l'attività usando una delle versioni seguenti dell'interfaccia della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="336b7-110">You can complete the task by using one of the following command-line interface (CLI) versions:</span></span>

- <span data-ttu-id="336b7-111">[Interfaccia della riga di comando di Azure 1.0](#quick-commands): l'interfaccia della riga di comando per i modelli di distribuzione classica e di gestione delle risorse (questo articolo)</span><span class="sxs-lookup"><span data-stu-id="336b7-111">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="336b7-112">[Interfaccia della riga di comando di Azure 2.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json): interfaccia della riga di comando di nuova generazione per il modello di distribuzione Resource Manager</span><span class="sxs-lookup"><span data-stu-id="336b7-112">[Azure CLI 2.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)- our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="336b7-113">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="336b7-113">Quick commands</span></span>
<span data-ttu-id="336b7-114">Per eseguire rapidamente l'attività, seguire i passaggi in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="336b7-114">To accomplish the task quickly, follow the steps in this section.</span></span> <span data-ttu-id="336b7-115">Per informazioni più dettagliate e di contesto, iniziare con la sezione ["Procedura dettagliata"](mount-azure-file-storage-on-linux-using-smb.md#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="336b7-115">For more detailed information and context, begin at the ["Detailed walkthrough"](mount-azure-file-storage-on-linux-using-smb.md#detailed-walkthrough) section.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="336b7-116">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="336b7-116">Prerequisites</span></span>
* <span data-ttu-id="336b7-117">Un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="336b7-117">A resource group</span></span>
* <span data-ttu-id="336b7-118">Una rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="336b7-118">An Azure virtual network</span></span>
* <span data-ttu-id="336b7-119">Un gruppo di sicurezza di rete con SSH in ingresso</span><span class="sxs-lookup"><span data-stu-id="336b7-119">A network security group with an SSH inbound</span></span>
* <span data-ttu-id="336b7-120">Una subnet</span><span class="sxs-lookup"><span data-stu-id="336b7-120">A subnet</span></span>
* <span data-ttu-id="336b7-121">Un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="336b7-121">An Azure storage account</span></span>
* <span data-ttu-id="336b7-122">Chiavi dell'account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="336b7-122">Azure storage account keys</span></span>
* <span data-ttu-id="336b7-123">Una condivisione di archiviazione file di Azure</span><span class="sxs-lookup"><span data-stu-id="336b7-123">An Azure File storage share</span></span>
* <span data-ttu-id="336b7-124">Una VM Linux</span><span class="sxs-lookup"><span data-stu-id="336b7-124">A Linux VM</span></span>

<span data-ttu-id="336b7-125">Sostituire gli esempi con le impostazioni desiderate.</span><span class="sxs-lookup"><span data-stu-id="336b7-125">Replace any examples with your own settings.</span></span>

### <a name="create-a-directory-for-the-local-mount"></a><span data-ttu-id="336b7-126">Creare una directory per il montaggio locale</span><span class="sxs-lookup"><span data-stu-id="336b7-126">Create a directory for the local mount</span></span>

```bash
mkdir -p /mnt/mymountpoint
```

### <a name="mount-the-file-storage-smb-share-to-the-mount-point"></a><span data-ttu-id="336b7-127">Montare la condivisione SMB di archiviazione file sul punto di montaggio</span><span class="sxs-lookup"><span data-stu-id="336b7-127">Mount the File storage SMB share to the mount point</span></span>

```bash
sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mymountpoint -o vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

### <a name="persist-the-mount-after-a-reboot"></a><span data-ttu-id="336b7-128">Rendere persistente il montaggio dopo un riavvio</span><span class="sxs-lookup"><span data-stu-id="336b7-128">Persist the mount after a reboot</span></span>
<span data-ttu-id="336b7-129">Aggiungere la riga seguente a `/etc/fstab`:</span><span class="sxs-lookup"><span data-stu-id="336b7-129">Add the following line to `/etc/fstab`:</span></span>

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="336b7-130">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="336b7-130">Detailed walkthrough</span></span>

<span data-ttu-id="336b7-131">L'archiviazione file offre condivisioni file nel cloud che usano il protocollo SMB standard.</span><span class="sxs-lookup"><span data-stu-id="336b7-131">File storage offers file shares in the cloud that use the standard SMB protocol.</span></span> <span data-ttu-id="336b7-132">Con la versione più recente di archiviazione file è anche possibile montare una condivisione di file da un sistema operativo che supporta SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="336b7-132">With the latest release of File storage, you can also mount a file share from any OS that supports SMB 3.0.</span></span> <span data-ttu-id="336b7-133">Quando si usa un montaggio SMB in Linux è possibile eseguire facilmente copie di backup in un percorso di archiviazione affidabile e permanente supportato da un Contratto di servizio.</span><span class="sxs-lookup"><span data-stu-id="336b7-133">When you use an SMB mount on Linux, you get easy backups to a robust, permanent archiving storage location that is supported by an SLA.</span></span>

<span data-ttu-id="336b7-134">Lo spostamento di file da una VM a un montaggio SMB ospitato nell'archiviazione file è un ottimo modo per eseguire il debug dei log,</span><span class="sxs-lookup"><span data-stu-id="336b7-134">Moving files from a VM to an SMB mount that's hosted on File storage is a great way to debug logs.</span></span> <span data-ttu-id="336b7-135">dato che la stessa condivisione SMB può essere montata in locale in workstation Mac, Linux o Windows.</span><span class="sxs-lookup"><span data-stu-id="336b7-135">That's because the same SMB share can be mounted locally to your Mac, Linux, or Windows workstation.</span></span> <span data-ttu-id="336b7-136">SMB non è la soluzione migliore per eseguire lo streaming di log applicazioni o Linux in tempo reale perché il protocollo SMB non è stato creato per la gestione di attività di registrazione così impegnative.</span><span class="sxs-lookup"><span data-stu-id="336b7-136">SMB isn't the best solution for streaming Linux or application logs in real time, because the SMB protocol is not built to handle such heavy logging duties.</span></span> <span data-ttu-id="336b7-137">Per raccogliere l'output di log applicazioni o Linux è preferibile usare uno strumento dedicato con livello di registrazione unificato come Fluentd piuttosto che SMB.</span><span class="sxs-lookup"><span data-stu-id="336b7-137">A dedicated, unified logging layer tool such as Fluentd would be a better choice than SMB for collecting Linux and application logging output.</span></span>

<span data-ttu-id="336b7-138">Per questa procedura dettagliata vengono definiti i prerequisiti necessari prima per creare la condivisione di Archiviazione file di Azure e quindi per montarla tramite SMB in una VM Linux.</span><span class="sxs-lookup"><span data-stu-id="336b7-138">For this detailed walkthrough, we create the prerequisites needed to first create the File storage share, and then mount it via SMB on a Linux VM.</span></span>

1. <span data-ttu-id="336b7-139">Creare un account di archiviazione di Azure usando il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="336b7-139">Create an Azure storage account by using the following code:</span></span>

    ```azurecli
    azure storage account create myStorageAccount \
    --sku-name lrs \
    --kind storage \
    -l westus \
    -g myResourceGroup
    ```

2. <span data-ttu-id="336b7-140">Visualizzare le chiavi dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="336b7-140">Show the storage account keys.</span></span>

    <span data-ttu-id="336b7-141">Quando si crea un account di archiviazione, le chiavi dell'account vengono create a coppie perché possano essere ruotate senza interrompere il servizio.</span><span class="sxs-lookup"><span data-stu-id="336b7-141">When you create a storage account, the account keys are created in pairs so that they can be rotated without any service interruption.</span></span> <span data-ttu-id="336b7-142">Quando si passa alla seconda chiave della coppia, viene creata una nuova coppia di chiavi.</span><span class="sxs-lookup"><span data-stu-id="336b7-142">When you switch to the second key in the pair, you create a new key pair.</span></span> <span data-ttu-id="336b7-143">Le nuove chiavi dell'account di archiviazione vengono sempre create a coppie in modo da avere sempre a disposizione almeno una chiave di archiviazione non usata alla quale passare.</span><span class="sxs-lookup"><span data-stu-id="336b7-143">New storage account keys are always created in pairs, ensuring that you always have at least one unused storage key ready to switch to.</span></span> <span data-ttu-id="336b7-144">Per visualizzare le chiavi dell'account di archiviazione usare il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="336b7-144">To show the storage account keys, use the following code:</span></span>

    ```azurecli
    azure storage account keys list myStorageAccount \
    --resource-group myResourceGroup
    ```
3. <span data-ttu-id="336b7-145">Creare la condivisione di Archiviazione file.</span><span class="sxs-lookup"><span data-stu-id="336b7-145">Create the File storage share.</span></span>

    <span data-ttu-id="336b7-146">La condivisione di Archiviazione file contiene la condivisione SMB.</span><span class="sxs-lookup"><span data-stu-id="336b7-146">The File storage share contains the SMB share.</span></span> <span data-ttu-id="336b7-147">La quota è sempre espressa in gigabyte (GB).</span><span class="sxs-lookup"><span data-stu-id="336b7-147">The quota is always expressed in gigabytes (GB).</span></span> <span data-ttu-id="336b7-148">Per creare la condivisione di Archiviazione file usare il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="336b7-148">To create the File storage share, use the following code:</span></span>

    ```azurecli
    azure storage share create mystorageshare \
    --quota 10 \
    --account-name myStorageAccount \
    --account-key nPOgPR<--snip-->4Q==
    ```

4. <span data-ttu-id="336b7-149">Creare la directory del punto di montaggio.</span><span class="sxs-lookup"><span data-stu-id="336b7-149">Create the mount-point directory.</span></span>

    <span data-ttu-id="336b7-150">Nel file system di Linux è necessario creare una directory locale nella quale montare la condivisione SMB.</span><span class="sxs-lookup"><span data-stu-id="336b7-150">You must create a local directory in the Linux file system to mount the SMB share to.</span></span> <span data-ttu-id="336b7-151">Qualsiasi elemento scritto o letto dalla directory di montaggio locale viene inoltrato alla condivisione SMB ospitata in Archiviazione file.</span><span class="sxs-lookup"><span data-stu-id="336b7-151">Anything written or read from the local mount directory is forwarded to the SMB share that's hosted on File storage.</span></span> <span data-ttu-id="336b7-152">Per creare la directory usare il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="336b7-152">To create the directory, use the following code:</span></span>

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

5. <span data-ttu-id="336b7-153">Montare la condivisione SMB usando il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="336b7-153">Mount the SMB share by using the following code:</span></span>

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=myStorageAccount,password=myStorageAccountkey,dir_mode=0777,file_mode=0777
    ```

6. <span data-ttu-id="336b7-154">Rendere persistente il montaggio SMB dopo il riavvio.</span><span class="sxs-lookup"><span data-stu-id="336b7-154">Persist the SMB mount through reboots.</span></span>

    <span data-ttu-id="336b7-155">Quando si riavvia la VM Linux, durante la fase di arresto viene smontata la condivisione SMB montata.</span><span class="sxs-lookup"><span data-stu-id="336b7-155">When you reboot the Linux VM, the mounted SMB share is unmounted during shutdown.</span></span> <span data-ttu-id="336b7-156">Per rimontare la condivisione SMB all'avvio, è necessario aggiungere una riga al file /etc/fstab di Linux.</span><span class="sxs-lookup"><span data-stu-id="336b7-156">To remount the SMB share on boot, you must add a line to the Linux /etc/fstab.</span></span> <span data-ttu-id="336b7-157">Linux usa il file fstab per elencare i file system da montare durante la fase di avvio.</span><span class="sxs-lookup"><span data-stu-id="336b7-157">Linux uses the fstab file to list the file systems that it needs to mount during the boot process.</span></span> <span data-ttu-id="336b7-158">Aggiungendo la condivisione SMB si garantisce che la condivisione di archiviazione file costituisca un file system montato in modo permanente per la VM Linux.</span><span class="sxs-lookup"><span data-stu-id="336b7-158">Adding the SMB share ensures that the File storage share is a permanently mounted file system for the Linux VM.</span></span> <span data-ttu-id="336b7-159">L'aggiunta della condivisione SMB di archiviazione file in una nuova VM è possibile quando si usa cloud-init.</span><span class="sxs-lookup"><span data-stu-id="336b7-159">Adding the File storage SMB share to a new VM is possible when you use cloud-init.</span></span>

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a><span data-ttu-id="336b7-160">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="336b7-160">Next steps</span></span>

- [<span data-ttu-id="336b7-161">Uso di cloud-init per personalizzare una VM Linux durante la creazione</span><span class="sxs-lookup"><span data-stu-id="336b7-161">Using cloud-init to customize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="336b7-162">Aggiungere un disco a una VM Linux</span><span class="sxs-lookup"><span data-stu-id="336b7-162">Add a disk to a Linux VM</span></span>](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="336b7-163">Crittografare i dischi di una VM Linux usando l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="336b7-163">Encrypt disks on a Linux VM by using the Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
