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
# <a name="mount-azure-file-storage-on-linux-vms-using-smb"></a><span data-ttu-id="504d5-103">Montare l'archiviazione file di Azure su VM Linux usando SMB</span><span class="sxs-lookup"><span data-stu-id="504d5-103">Mount Azure File storage on Linux VMs using SMB</span></span>

<span data-ttu-id="504d5-104">Questo articolo illustra la modalità di montaggio hello tooutilize servizio di archiviazione di File di Azure in una VM Linux usando un protocollo SMB con hello CLI di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="504d5-104">This article shows you how tooutilize hello Azure File storage service on a Linux VM using an SMB mount with hello Azure CLI 2.0.</span></span> <span data-ttu-id="504d5-105">Archiviazione di File di Azure offre le condivisioni di file in un cloud di hello tramite il protocollo SMB standard di hello.</span><span class="sxs-lookup"><span data-stu-id="504d5-105">Azure File storage offers file shares in hello cloud using hello standard SMB protocol.</span></span> <span data-ttu-id="504d5-106">È anche possibile eseguire questi passaggi con hello [CLI di Azure 1.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="504d5-106">You can also perform these steps with hello [Azure CLI 1.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="504d5-107">requisiti di Hello sono:</span><span class="sxs-lookup"><span data-stu-id="504d5-107">hello requirements are:</span></span>

- [<span data-ttu-id="504d5-108">Un account di Azure</span><span class="sxs-lookup"><span data-stu-id="504d5-108">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
- [<span data-ttu-id="504d5-109">File di chiavi SSH pubbliche e private</span><span class="sxs-lookup"><span data-stu-id="504d5-109">SSH public and private key files</span></span>](mac-create-ssh-keys.md)

## <a name="quick-commands"></a><span data-ttu-id="504d5-110">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="504d5-110">Quick Commands</span></span>

* <span data-ttu-id="504d5-111">Un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="504d5-111">A resource group</span></span>
* <span data-ttu-id="504d5-112">Una rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="504d5-112">An Azure virtual network</span></span>
* <span data-ttu-id="504d5-113">Un gruppo di sicurezza di rete con SSH in ingresso</span><span class="sxs-lookup"><span data-stu-id="504d5-113">A network security group with an SSH inbound</span></span>
* <span data-ttu-id="504d5-114">Una subnet</span><span class="sxs-lookup"><span data-stu-id="504d5-114">A subnet</span></span>
* <span data-ttu-id="504d5-115">Un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="504d5-115">An Azure storage account</span></span>
* <span data-ttu-id="504d5-116">Chiavi dell'account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="504d5-116">Azure storage account keys</span></span>
* <span data-ttu-id="504d5-117">Una condivisione di archiviazione file di Azure</span><span class="sxs-lookup"><span data-stu-id="504d5-117">An Azure File storage share</span></span>
* <span data-ttu-id="504d5-118">Una VM Linux</span><span class="sxs-lookup"><span data-stu-id="504d5-118">A Linux VM</span></span>

<span data-ttu-id="504d5-119">Sostituire gli esempi con le impostazioni desiderate.</span><span class="sxs-lookup"><span data-stu-id="504d5-119">Replace any examples with your own settings.</span></span>

### <a name="create-a-directory-for-hello-local-mount"></a><span data-ttu-id="504d5-120">Creare una directory di montaggio locale hello</span><span class="sxs-lookup"><span data-stu-id="504d5-120">Create a directory for hello local mount</span></span>

```bash
mkdir -p /mnt/mymountpoint
```

### <a name="mount-hello-file-storage-smb-share-toohello-mount-point"></a><span data-ttu-id="504d5-121">Punto di montaggio di hello File archiviazione SMB condivisione toohello di montaggio</span><span class="sxs-lookup"><span data-stu-id="504d5-121">Mount hello File storage SMB share toohello mount point</span></span>

```bash
sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mymountpoint -o vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

### <a name="persist-hello-mount-after-a-reboot"></a><span data-ttu-id="504d5-122">Persistenza mount hello dopo il riavvio</span><span class="sxs-lookup"><span data-stu-id="504d5-122">Persist hello mount after a reboot</span></span>
<span data-ttu-id="504d5-123">toodo in tal caso, aggiungere hello seguente riga toohello `/etc/fstab`:</span><span class="sxs-lookup"><span data-stu-id="504d5-123">toodo so, add hello following line toohello `/etc/fstab`:</span></span>

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="504d5-124">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="504d5-124">Detailed walkthrough</span></span>

<span data-ttu-id="504d5-125">Archiviazione di file offre le condivisioni file cloud hello che utilizzano il protocollo SMB standard di hello.</span><span class="sxs-lookup"><span data-stu-id="504d5-125">File storage offers file shares in hello cloud that use hello standard SMB protocol.</span></span> <span data-ttu-id="504d5-126">Con una versione più recente di hello di archiviazione di File, è inoltre possibile collegare una condivisione file da qualsiasi sistema operativo che supporta SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="504d5-126">With hello latest release of File storage, you can also mount a file share from any OS that supports SMB 3.0.</span></span> <span data-ttu-id="504d5-127">Quando si utilizza un montaggio SMB su Linux, si ottiene backup semplice tooa affidabile e permanente archiviazione percorso di archiviazione supportata da un contratto di servizio.</span><span class="sxs-lookup"><span data-stu-id="504d5-127">When you use an SMB mount on Linux, you get easy backups tooa robust, permanent archiving storage location that is supported by an SLA.</span></span>

<span data-ttu-id="504d5-128">Lo spostamento di file da un montaggio SMB tooan di macchina virtuale ospitata in archiviazione di File è che toodebug un ottimo modo Registra.</span><span class="sxs-lookup"><span data-stu-id="504d5-128">Moving files from a VM tooan SMB mount that's hosted on File storage is a great way toodebug logs.</span></span> <span data-ttu-id="504d5-129">Ciò accade perché hello condivisione SMB stesso può essere installato localmente tooyour workstation di Windows, Linux o Mac.</span><span class="sxs-lookup"><span data-stu-id="504d5-129">That's because hello same SMB share can be mounted locally tooyour Mac, Linux, or Windows workstation.</span></span> <span data-ttu-id="504d5-130">SMB non è hello la soluzione migliore per lo streaming di Linux o registrata dall'applicazione in tempo reale, poiché il protocollo SMB hello non compilato toohandle loro registrazione elevato.</span><span class="sxs-lookup"><span data-stu-id="504d5-130">SMB isn't hello best solution for streaming Linux or application logs in real time, because hello SMB protocol is not built toohandle such heavy logging duties.</span></span> <span data-ttu-id="504d5-131">Per raccogliere l'output di log applicazioni o Linux è preferibile usare uno strumento dedicato con livello di registrazione unificato come Fluentd piuttosto che SMB.</span><span class="sxs-lookup"><span data-stu-id="504d5-131">A dedicated, unified logging layer tool such as Fluentd would be a better choice than SMB for collecting Linux and application logging output.</span></span>

<span data-ttu-id="504d5-132">Per questa procedura dettagliata, è creare prerequisiti hello necessari toofirst creare la condivisione di archiviazione di File hello e quindi montare tramite SMB in una VM Linux.</span><span class="sxs-lookup"><span data-stu-id="504d5-132">For this detailed walkthrough, we create hello prerequisites needed toofirst create hello File storage share, and then mount it via SMB on a Linux VM.</span></span>

1. <span data-ttu-id="504d5-133">Creare un gruppo di risorse con [gruppo az creare](/cli/azure/group#create) toohold condivisione di file hello.</span><span class="sxs-lookup"><span data-stu-id="504d5-133">Create a resource group with [az group create](/cli/azure/group#create) toohold hello file share.</span></span>

    <span data-ttu-id="504d5-134">un gruppo di risorse denominato toocreate `myResourceGroup` nel percorso "Stati Uniti occidentali" hello, utilizzare hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="504d5-134">toocreate a resource group named `myResourceGroup` in hello "West US" location, use hello following example:</span></span>

    ```azurecli
    az group create --name myResourceGroup --location westus
    ```

2. <span data-ttu-id="504d5-135">Creare un account di archiviazione di Azure con [creare account di archiviazione az](/cli/azure/storage/account#create) toostore hello file effettivi.</span><span class="sxs-lookup"><span data-stu-id="504d5-135">Create an Azure storage account with [az storage account create](/cli/azure/storage/account#create) toostore hello actual files.</span></span>

    <span data-ttu-id="504d5-136">toocreate un account di archiviazione denominato mystorageaccount utilizzando l'archiviazione Standard_LRS hello SKU, utilizzare hello esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="504d5-136">toocreate a storage account named mystorageaccount by using hello Standard_LRS storage SKU, use hello following example:</span></span>

    ```azurecli
    az storage account create --resource-group myResourceGroup \
        --name mystorageaccount \
        --location westus \
        --sku Standard_LRS
    ```

3. <span data-ttu-id="504d5-137">Mostra chiavi dell'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="504d5-137">Show hello storage account keys.</span></span>

    <span data-ttu-id="504d5-138">Quando si crea un account di archiviazione, le chiavi dell'account hello vengono create in coppie, in modo che possono essere ruotate senza interruzione del servizio.</span><span class="sxs-lookup"><span data-stu-id="504d5-138">When you create a storage account, hello account keys are created in pairs so that they can be rotated without any service interruption.</span></span> <span data-ttu-id="504d5-139">Quando si passa toohello seconda chiave nella coppia hello, si crea una nuova coppia di chiavi.</span><span class="sxs-lookup"><span data-stu-id="504d5-139">When you switch toohello second key in hello pair, you create a new key pair.</span></span> <span data-ttu-id="504d5-140">Nuove chiavi dell'account di archiviazione vengono sempre create in coppie, accertarsi di disporre sempre di almeno uno spazio di archiviazione inutilizzato account chiave pronto tooswitch per.</span><span class="sxs-lookup"><span data-stu-id="504d5-140">New storage account keys are always created in pairs, ensuring that you always have at least one unused storage account key ready tooswitch to.</span></span>

    <span data-ttu-id="504d5-141">Visualizzare le chiavi di account di archiviazione hello con hello [elenco di chiavi di account di archiviazione az](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="504d5-141">View hello storage account keys with hello [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span> <span data-ttu-id="504d5-142">chiavi di account di archiviazione per hello denominato Hello `mystorageaccount` sono elencati nel seguente esempio hello:</span><span class="sxs-lookup"><span data-stu-id="504d5-142">hello storage account keys for hello named `mystorageaccount` are listed in hello following example:</span></span>

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount
    ```

    <span data-ttu-id="504d5-143">tooextract una sola chiave, utilizzare hello `--query` flag.</span><span class="sxs-lookup"><span data-stu-id="504d5-143">tooextract a single key, use hello `--query` flag.</span></span> <span data-ttu-id="504d5-144">esempio Hello estrae prima chiave hello (`[0]`):</span><span class="sxs-lookup"><span data-stu-id="504d5-144">hello following example extracts hello first key (`[0]`):</span></span>

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount \
        --query '[0].{Key:value}' --output tsv
    ```

4. <span data-ttu-id="504d5-145">Creare la condivisione di archiviazione di File hello.</span><span class="sxs-lookup"><span data-stu-id="504d5-145">Create hello File storage share.</span></span>

    <span data-ttu-id="504d5-146">condivisione di File di archiviazione Hello contiene hello condivisione SMB con [creare la condivisione di archiviazione az](/cli/azure/storage/share#create).</span><span class="sxs-lookup"><span data-stu-id="504d5-146">hello File storage share contains hello SMB share with [az storage share create](/cli/azure/storage/share#create).</span></span> <span data-ttu-id="504d5-147">quota Hello è sempre espressa in gigabyte (GB).</span><span class="sxs-lookup"><span data-stu-id="504d5-147">hello quota is always expressed in gigabytes (GB).</span></span> <span data-ttu-id="504d5-148">Passare una delle chiavi di hello dal precedente hello `az storage account keys list` comando.</span><span class="sxs-lookup"><span data-stu-id="504d5-148">Pass in one of hello keys from hello preceding `az storage account keys list` command.</span></span> <span data-ttu-id="504d5-149">Creare una condivisione denominata mystorageshare con una quota di 10 GB con hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="504d5-149">Create a share named mystorageshare with a 10-GB quota by using hello following example:</span></span>

    ```azurecli
    az storage share create --name mystorageshare \
        --quota 10 \
        --account-name mystorageaccount \
        --account-key nPOgPR<--snip-->4Q==
    ```

5. <span data-ttu-id="504d5-150">Creare una directory del punto di montaggio.</span><span class="sxs-lookup"><span data-stu-id="504d5-150">Create a mount-point directory.</span></span>

    <span data-ttu-id="504d5-151">Creare una directory locale in hello toomount hello Linux file system per di condivisione SMB.</span><span class="sxs-lookup"><span data-stu-id="504d5-151">Create a local directory in hello Linux file system toomount hello SMB share to.</span></span> <span data-ttu-id="504d5-152">Qualsiasi elemento scritto o letto dalla directory di montaggio locale hello viene inoltrato toohello condivisione SMB ospitata in archiviazione di File.</span><span class="sxs-lookup"><span data-stu-id="504d5-152">Anything written or read from hello local mount directory is forwarded toohello SMB share that's hosted on File storage.</span></span> <span data-ttu-id="504d5-153">toocreate una directory locale in /mnt/Retention/ mymountdirectory, utilizzare hello esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="504d5-153">toocreate a local directory at /mnt/mymountdirectory, use hello following example:</span></span>

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

6. <span data-ttu-id="504d5-154">Montaggio di directory locale toohello di hello condivisione SMB.</span><span class="sxs-lookup"><span data-stu-id="504d5-154">Mount hello SMB share toohello local directory.</span></span>

    <span data-ttu-id="504d5-155">Fornire il proprio nome utente account di archiviazione e chiave dell'account di archiviazione per le credenziali di montaggio hello nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="504d5-155">Provide your own storage account username and storage account key for hello mount credentials as follows:</span></span>

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=mystorageaccount,password=mystorageaccountkey,dir_mode=0777,file_mode=0777
    ```

7. <span data-ttu-id="504d5-156">Mantenere hello SMB montare il riavvio del sistema.</span><span class="sxs-lookup"><span data-stu-id="504d5-156">Persist hello SMB mount through reboots.</span></span>

    <span data-ttu-id="504d5-157">Quando si riavvia hello VM Linux, hello montata condivisione SMB viene disinstallata durante l'arresto.</span><span class="sxs-lookup"><span data-stu-id="504d5-157">When you reboot hello Linux VM, hello mounted SMB share is unmounted during shutdown.</span></span> <span data-ttu-id="504d5-158">hello tooremount condivisione SMB all'avvio del sistema, aggiungere un toohello riga /etc/fstab. Linux.</span><span class="sxs-lookup"><span data-stu-id="504d5-158">tooremount hello SMB share on boot, add a line toohello Linux /etc/fstab.</span></span> <span data-ttu-id="504d5-159">Linux Usa hello fstab file toolist hello file System che deve toomount durante il processo di avvio hello.</span><span class="sxs-lookup"><span data-stu-id="504d5-159">Linux uses hello fstab file toolist hello file systems that it needs toomount during hello boot process.</span></span> <span data-ttu-id="504d5-160">Aggiunta condivisione SMB di hello garantisce che la condivisione archiviazione File hello è un sistema di file montati in modo permanente per hello VM Linux.</span><span class="sxs-lookup"><span data-stu-id="504d5-160">Adding hello SMB share ensures that hello File storage share is a permanently mounted file system for hello Linux VM.</span></span> <span data-ttu-id="504d5-161">Aggiunta di hello File archiviazione SMB condivisione tooa nuova macchina virtuale è possibile quando si utilizza cloud init.</span><span class="sxs-lookup"><span data-stu-id="504d5-161">Adding hello File storage SMB share tooa new VM is possible when you use cloud-init.</span></span>

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a><span data-ttu-id="504d5-162">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="504d5-162">Next steps</span></span>

- [<span data-ttu-id="504d5-163">Utilizzo di cloud init toocustomize una VM Linux durante la creazione</span><span class="sxs-lookup"><span data-stu-id="504d5-163">Using cloud-init toocustomize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="504d5-164">Aggiungere un tooa disco VM Linux</span><span class="sxs-lookup"><span data-stu-id="504d5-164">Add a disk tooa Linux VM</span></span>](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="504d5-165">Crittografare i dischi in una VM Linux con hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="504d5-165">Encrypt disks on a Linux VM by using hello Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
