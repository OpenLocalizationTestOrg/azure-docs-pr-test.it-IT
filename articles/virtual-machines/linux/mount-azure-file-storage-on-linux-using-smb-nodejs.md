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
# <a name="mount-azure-file-storage-on-linux-vms-by-using-smb-with-azure-cli-10"></a><span data-ttu-id="5fec6-103">Montare Archiviazione file di Azure in VM Linux usando SMB con l'interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="5fec6-103">Mount Azure File storage on Linux VMs by using SMB with Azure CLI 1.0</span></span>

<span data-ttu-id="5fec6-104">Questo articolo illustra come archiviazione di File di Azure in una VM Linux utilizzando toomount hello protocollo Server Message Block (SMB).</span><span class="sxs-lookup"><span data-stu-id="5fec6-104">This article shows how toomount Azure File storage on a Linux VM by using hello Server Message Block (SMB) protocol.</span></span> <span data-ttu-id="5fec6-105">Archiviazione di file offre le condivisioni file nel cloud hello tramite il protocollo SMB standard di hello.</span><span class="sxs-lookup"><span data-stu-id="5fec6-105">File storage offers file shares in hello cloud via hello standard SMB protocol.</span></span> <span data-ttu-id="5fec6-106">requisiti di Hello sono:</span><span class="sxs-lookup"><span data-stu-id="5fec6-106">hello requirements are:</span></span>

* <span data-ttu-id="5fec6-107">Un [account Azure](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="5fec6-107">An [Azure account](https://azure.microsoft.com/pricing/free-trial/)</span></span>
* [<span data-ttu-id="5fec6-108">File di chiavi pubbliche e private Secure Shell (SSH)</span><span class="sxs-lookup"><span data-stu-id="5fec6-108">Secure Shell (SSH) public and private key files</span></span>](mac-create-ssh-keys.md)

## <a name="cli-versions-toouse"></a><span data-ttu-id="5fec6-109">Toouse di versioni CLI</span><span class="sxs-lookup"><span data-stu-id="5fec6-109">CLI versions toouse</span></span>
<span data-ttu-id="5fec6-110">È possibile completare l'attività hello utilizzando una delle seguenti versioni di interfaccia della riga di comando (CLI) hello:</span><span class="sxs-lookup"><span data-stu-id="5fec6-110">You can complete hello task by using one of hello following command-line interface (CLI) versions:</span></span>

- <span data-ttu-id="5fec6-111">[Azure CLI 1.0](#quick-commands) : l'interfaccia CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)</span><span class="sxs-lookup"><span data-stu-id="5fec6-111">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="5fec6-112">[Azure CLI 2.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)-la prossima generazione CLI per modello di distribuzione di gestione risorse hello</span><span class="sxs-lookup"><span data-stu-id="5fec6-112">[Azure CLI 2.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)- our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="5fec6-113">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="5fec6-113">Quick commands</span></span>
<span data-ttu-id="5fec6-114">attività hello tooaccomplish rapidamente, procedura hello in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="5fec6-114">tooaccomplish hello task quickly, follow hello steps in this section.</span></span> <span data-ttu-id="5fec6-115">Per ulteriori informazioni e il contesto, iniziare in corrispondenza di hello ["Procedura dettagliata"](mount-azure-file-storage-on-linux-using-smb.md#detailed-walkthrough) sezione.</span><span class="sxs-lookup"><span data-stu-id="5fec6-115">For more detailed information and context, begin at hello ["Detailed walkthrough"](mount-azure-file-storage-on-linux-using-smb.md#detailed-walkthrough) section.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="5fec6-116">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5fec6-116">Prerequisites</span></span>
* <span data-ttu-id="5fec6-117">Un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="5fec6-117">A resource group</span></span>
* <span data-ttu-id="5fec6-118">Una rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="5fec6-118">An Azure virtual network</span></span>
* <span data-ttu-id="5fec6-119">Un gruppo di sicurezza di rete con SSH in ingresso</span><span class="sxs-lookup"><span data-stu-id="5fec6-119">A network security group with an SSH inbound</span></span>
* <span data-ttu-id="5fec6-120">Una subnet</span><span class="sxs-lookup"><span data-stu-id="5fec6-120">A subnet</span></span>
* <span data-ttu-id="5fec6-121">Un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="5fec6-121">An Azure storage account</span></span>
* <span data-ttu-id="5fec6-122">Chiavi dell'account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="5fec6-122">Azure storage account keys</span></span>
* <span data-ttu-id="5fec6-123">Una condivisione di archiviazione file di Azure</span><span class="sxs-lookup"><span data-stu-id="5fec6-123">An Azure File storage share</span></span>
* <span data-ttu-id="5fec6-124">Una VM Linux</span><span class="sxs-lookup"><span data-stu-id="5fec6-124">A Linux VM</span></span>

<span data-ttu-id="5fec6-125">Sostituire gli esempi con le impostazioni desiderate.</span><span class="sxs-lookup"><span data-stu-id="5fec6-125">Replace any examples with your own settings.</span></span>

### <a name="create-a-directory-for-hello-local-mount"></a><span data-ttu-id="5fec6-126">Creare una directory di montaggio locale hello</span><span class="sxs-lookup"><span data-stu-id="5fec6-126">Create a directory for hello local mount</span></span>

```bash
mkdir -p /mnt/mymountpoint
```

### <a name="mount-hello-file-storage-smb-share-toohello-mount-point"></a><span data-ttu-id="5fec6-127">Punto di montaggio di hello File archiviazione SMB condivisione toohello di montaggio</span><span class="sxs-lookup"><span data-stu-id="5fec6-127">Mount hello File storage SMB share toohello mount point</span></span>

```bash
sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mymountpoint -o vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

### <a name="persist-hello-mount-after-a-reboot"></a><span data-ttu-id="5fec6-128">Persistenza mount hello dopo il riavvio</span><span class="sxs-lookup"><span data-stu-id="5fec6-128">Persist hello mount after a reboot</span></span>
<span data-ttu-id="5fec6-129">Aggiungere hello successiva riga troppo`/etc/fstab`:</span><span class="sxs-lookup"><span data-stu-id="5fec6-129">Add hello following line too`/etc/fstab`:</span></span>

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="5fec6-130">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="5fec6-130">Detailed walkthrough</span></span>

<span data-ttu-id="5fec6-131">Archiviazione di file offre le condivisioni file cloud hello che utilizzano il protocollo SMB standard di hello.</span><span class="sxs-lookup"><span data-stu-id="5fec6-131">File storage offers file shares in hello cloud that use hello standard SMB protocol.</span></span> <span data-ttu-id="5fec6-132">Con una versione più recente di hello di archiviazione di File, è inoltre possibile collegare una condivisione file da qualsiasi sistema operativo che supporta SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="5fec6-132">With hello latest release of File storage, you can also mount a file share from any OS that supports SMB 3.0.</span></span> <span data-ttu-id="5fec6-133">Quando si utilizza un montaggio SMB su Linux, si ottiene backup semplice tooa affidabile e permanente archiviazione percorso di archiviazione supportata da un contratto di servizio.</span><span class="sxs-lookup"><span data-stu-id="5fec6-133">When you use an SMB mount on Linux, you get easy backups tooa robust, permanent archiving storage location that is supported by an SLA.</span></span>

<span data-ttu-id="5fec6-134">Lo spostamento di file da un montaggio SMB tooan di macchina virtuale ospitata in archiviazione di File è che toodebug un ottimo modo Registra.</span><span class="sxs-lookup"><span data-stu-id="5fec6-134">Moving files from a VM tooan SMB mount that's hosted on File storage is a great way toodebug logs.</span></span> <span data-ttu-id="5fec6-135">Ciò accade perché hello condivisione SMB stesso può essere installato localmente tooyour workstation di Windows, Linux o Mac.</span><span class="sxs-lookup"><span data-stu-id="5fec6-135">That's because hello same SMB share can be mounted locally tooyour Mac, Linux, or Windows workstation.</span></span> <span data-ttu-id="5fec6-136">SMB non è hello la soluzione migliore per lo streaming di Linux o registrata dall'applicazione in tempo reale, poiché il protocollo SMB hello non compilato toohandle loro registrazione elevato.</span><span class="sxs-lookup"><span data-stu-id="5fec6-136">SMB isn't hello best solution for streaming Linux or application logs in real time, because hello SMB protocol is not built toohandle such heavy logging duties.</span></span> <span data-ttu-id="5fec6-137">Per raccogliere l'output di log applicazioni o Linux è preferibile usare uno strumento dedicato con livello di registrazione unificato come Fluentd piuttosto che SMB.</span><span class="sxs-lookup"><span data-stu-id="5fec6-137">A dedicated, unified logging layer tool such as Fluentd would be a better choice than SMB for collecting Linux and application logging output.</span></span>

<span data-ttu-id="5fec6-138">Per questa procedura dettagliata, è creare prerequisiti hello necessari toofirst creare la condivisione di archiviazione di File hello e quindi montare tramite SMB in una VM Linux.</span><span class="sxs-lookup"><span data-stu-id="5fec6-138">For this detailed walkthrough, we create hello prerequisites needed toofirst create hello File storage share, and then mount it via SMB on a Linux VM.</span></span>

1. <span data-ttu-id="5fec6-139">Creare un account di archiviazione di Azure utilizzando hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="5fec6-139">Create an Azure storage account by using hello following code:</span></span>

    ```azurecli
    azure storage account create myStorageAccount \
    --sku-name lrs \
    --kind storage \
    -l westus \
    -g myResourceGroup
    ```

2. <span data-ttu-id="5fec6-140">Mostra chiavi dell'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="5fec6-140">Show hello storage account keys.</span></span>

    <span data-ttu-id="5fec6-141">Quando si crea un account di archiviazione, le chiavi dell'account hello vengono create in coppie, in modo che possono essere ruotate senza interruzione del servizio.</span><span class="sxs-lookup"><span data-stu-id="5fec6-141">When you create a storage account, hello account keys are created in pairs so that they can be rotated without any service interruption.</span></span> <span data-ttu-id="5fec6-142">Quando si passa toohello seconda chiave nella coppia hello, si crea una nuova coppia di chiavi.</span><span class="sxs-lookup"><span data-stu-id="5fec6-142">When you switch toohello second key in hello pair, you create a new key pair.</span></span> <span data-ttu-id="5fec6-143">Nuove chiavi dell'account di archiviazione vengono sempre create in coppie, accertarsi di disporre sempre di almeno uno spazio di archiviazione inutilizzato di tooswitch pronto chiave per.</span><span class="sxs-lookup"><span data-stu-id="5fec6-143">New storage account keys are always created in pairs, ensuring that you always have at least one unused storage key ready tooswitch to.</span></span> <span data-ttu-id="5fec6-144">chiavi dell'account di archiviazione hello tooshow, utilizzare hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="5fec6-144">tooshow hello storage account keys, use hello following code:</span></span>

    ```azurecli
    azure storage account keys list myStorageAccount \
    --resource-group myResourceGroup
    ```
3. <span data-ttu-id="5fec6-145">Creare la condivisione di archiviazione di File hello.</span><span class="sxs-lookup"><span data-stu-id="5fec6-145">Create hello File storage share.</span></span>

    <span data-ttu-id="5fec6-146">condivisione di File di archiviazione Hello contiene una condivisione SMB hello.</span><span class="sxs-lookup"><span data-stu-id="5fec6-146">hello File storage share contains hello SMB share.</span></span> <span data-ttu-id="5fec6-147">quota Hello è sempre espressa in gigabyte (GB).</span><span class="sxs-lookup"><span data-stu-id="5fec6-147">hello quota is always expressed in gigabytes (GB).</span></span> <span data-ttu-id="5fec6-148">toocreate hello condivisione File di archiviazione, usare hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="5fec6-148">toocreate hello File storage share, use hello following code:</span></span>

    ```azurecli
    azure storage share create mystorageshare \
    --quota 10 \
    --account-name myStorageAccount \
    --account-key nPOgPR<--snip-->4Q==
    ```

4. <span data-ttu-id="5fec6-149">Creare la directory di punto di montaggio hello.</span><span class="sxs-lookup"><span data-stu-id="5fec6-149">Create hello mount-point directory.</span></span>

    <span data-ttu-id="5fec6-150">È necessario creare una directory locale in hello toomount hello Linux file system per di condivisione SMB.</span><span class="sxs-lookup"><span data-stu-id="5fec6-150">You must create a local directory in hello Linux file system toomount hello SMB share to.</span></span> <span data-ttu-id="5fec6-151">Qualsiasi elemento scritto o letto dalla directory di montaggio locale hello viene inoltrato toohello condivisione SMB ospitata in archiviazione di File.</span><span class="sxs-lookup"><span data-stu-id="5fec6-151">Anything written or read from hello local mount directory is forwarded toohello SMB share that's hosted on File storage.</span></span> <span data-ttu-id="5fec6-152">directory di hello toocreate, utilizzare hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="5fec6-152">toocreate hello directory, use hello following code:</span></span>

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

5. <span data-ttu-id="5fec6-153">Montare hello condivisione SMB tramite hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="5fec6-153">Mount hello SMB share by using hello following code:</span></span>

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=myStorageAccount,password=myStorageAccountkey,dir_mode=0777,file_mode=0777
    ```

6. <span data-ttu-id="5fec6-154">Mantenere hello SMB montare il riavvio del sistema.</span><span class="sxs-lookup"><span data-stu-id="5fec6-154">Persist hello SMB mount through reboots.</span></span>

    <span data-ttu-id="5fec6-155">Quando si riavvia hello VM Linux, hello montata condivisione SMB viene disinstallata durante l'arresto.</span><span class="sxs-lookup"><span data-stu-id="5fec6-155">When you reboot hello Linux VM, hello mounted SMB share is unmounted during shutdown.</span></span> <span data-ttu-id="5fec6-156">condivisione SMB di tooremount hello all'avvio del sistema, è necessario aggiungere un toohello riga /etc/fstab. Linux.</span><span class="sxs-lookup"><span data-stu-id="5fec6-156">tooremount hello SMB share on boot, you must add a line toohello Linux /etc/fstab.</span></span> <span data-ttu-id="5fec6-157">Linux Usa hello fstab file toolist hello file System che deve toomount durante il processo di avvio hello.</span><span class="sxs-lookup"><span data-stu-id="5fec6-157">Linux uses hello fstab file toolist hello file systems that it needs toomount during hello boot process.</span></span> <span data-ttu-id="5fec6-158">Aggiunta condivisione SMB di hello garantisce che la condivisione archiviazione File hello è un sistema di file montati in modo permanente per hello VM Linux.</span><span class="sxs-lookup"><span data-stu-id="5fec6-158">Adding hello SMB share ensures that hello File storage share is a permanently mounted file system for hello Linux VM.</span></span> <span data-ttu-id="5fec6-159">Aggiunta di hello File archiviazione SMB condivisione tooa nuova macchina virtuale è possibile quando si utilizza cloud init.</span><span class="sxs-lookup"><span data-stu-id="5fec6-159">Adding hello File storage SMB share tooa new VM is possible when you use cloud-init.</span></span>

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a><span data-ttu-id="5fec6-160">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5fec6-160">Next steps</span></span>

- [<span data-ttu-id="5fec6-161">Utilizzo di cloud init toocustomize una VM Linux durante la creazione</span><span class="sxs-lookup"><span data-stu-id="5fec6-161">Using cloud-init toocustomize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="5fec6-162">Aggiungere un tooa disco VM Linux</span><span class="sxs-lookup"><span data-stu-id="5fec6-162">Add a disk tooa Linux VM</span></span>](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="5fec6-163">Crittografare i dischi in una VM Linux con hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="5fec6-163">Encrypt disks on a Linux VM by using hello Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
