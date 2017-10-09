---
title: copia una VM Linux personalizzato con l'interfaccia CLI di Azure 2.0 o aaaUpload | Documenti Microsoft
description: Caricare o copiare una macchina virtuale personalizzata con modello di distribuzione di gestione risorse di hello e hello Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a8c7818f-eb65-409e-aa91-ce5ae975c564
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 07/06/2017
ms.author: cynthn
ms.openlocfilehash: 79af897120a6ba7f4a427ba6c7d0c31b7b870bd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-vm-from-custom-disk-with-hello-azure-cli-20"></a>Creare una VM Linux da disco personalizzata con hello Azure CLI 2.0

<!-- rename toocreate-vm-specialized -->

In questo articolo illustra come tooupload un personalizzato disco rigido virtuale (VHD) o copiare un un disco rigido virtuale esistente in Azure e creare nuove macchine virtuali Linux (VM) da disco personalizzata hello. È possibile installare e configurare un requisiti tooyour distribuzione di Linux e quindi utilizzare tale disco rigido virtuale tooquickly creare una nuova macchina virtuale di Azure.

Se si desidera toocreate più macchine virtuali dal disco personalizzato, si deve creare un'immagine dal disco rigido virtuale o macchina virtuale. Per ulteriori informazioni, vedere [creare un'immagine personalizzata di una macchina virtuale di Azure utilizzando hello CLI](tutorial-custom-images.md).

Sono disponibili due opzioni:
* [Caricare un VHD](#option-1-upload-a-specialized-vhd)
* [Copiare una VM di Azure esistente](#option-2-copy-an-existing-azure-vm)

## <a name="quick-commands"></a>Comandi rapidi

Quando si crea una nuova macchina virtuale utilizzando [creare vm az](/cli/azure/vm#create) da un disco specializzato o personalizzato è **allegare** disco hello (-disco del sistema operativo collegare) anziché specificare un'immagine personalizzata o marketplace (-immagine). esempio Hello crea una macchina virtuale denominata *myVM* utilizzando hello gestito disco denominato *myManagedDisk* creato dal disco rigido virtuale personalizzato:

```azurecli
az vm create --resource-group myResourceGroup --location eastus --name myVM \
   --os-type linux --attach-os-disk myManagedDisk
```

## <a name="requirements"></a>Requisiti
hello toocomplete seguendo la procedura, è necessario:

* Una macchina virtuale Linux che è stata preparata per l'uso in Azure. Hello [Prepare hello VM](#prepare-the-vm) sezione di questo articolo descrive come toofind distro le informazioni specifiche sull'installazione di hello agente Linux Azure (waagent) che è necessario per hello VM toowork correttamente in Azure e si toobe in grado di tooconnect tooit tramite SSH.
* il file VHD Hello da un oggetto esistente [distribuzione Linux approvate per Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (o vedere [informazioni per distribuzioni non approvate](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa disco virtuale in formato VHD hello. Più strumenti esistono toocreate una macchina virtuale e disco rigido virtuale:
  * Installare e configurare [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) o [KVM](http://www.linux-kvm.org/page/RunningKVM), prestando attenzione toouse il formato di immagine disco rigido virtuale. Se necessario, è possibile [convertire un'immagine](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) usando **qemu-img convert**.
  * È anche possibile usare Hyper-V [in Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) o [in Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).

> [!NOTE]
> il formato VHDX più recente di Hello non è supportato in Azure. Quando si crea una macchina virtuale, è possibile specificare file VHD come formato hello. Se necessario, è possibile convertire VHDX dischi tooVHD con [qemu img convertire](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) o hello [Convert-VHD](https://technet.microsoft.com/library/hh848454.aspx) cmdlet di PowerShell. Inoltre, Azure non supporta il caricamento di dischi rigidi virtuali dinamici, pertanto è necessario tooconvert tali toostatic dischi VHD prima del caricamento. È possibile utilizzare strumenti come [utilità di disco rigido virtuale di Azure per passare](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dischi dinamici durante il processo di hello di caricamento tooAzure.
> 
> 


* Assicurarsi di aver hello più recente [CLI di Azure 2.0](/cli/azure/install-az-cli2) installato e registrato con un account Azure tooan [accesso az](/cli/azure/#login).

In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati. I nomi dei parametri di esempio includono *myResourceGroup*, *mystorageaccount* e *mydisks*.

<a id="prepimage"></a>

## <a name="prepare-hello-vm"></a>Preparare hello VM

Azure supporta svariate distribuzioni di Linux (vedere la sezione [Distribuzioni approvate](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Hello seguenti articoli semplificato come tooprepare hello diverse distribuzioni di Linux che sono supportate in Azure:

* [Distribuzioni basate su CentOS](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [SLES e openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Altro - Distribuzioni non approvate](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Vedere anche hello [note sull'installazione di Linux](create-upload-generic.md#general-linux-installation-notes) per suggerimenti generali sulla preparazione di immagini Linux per Azure.

> [!NOTE]
> Hello [contratto di servizio di piattaforma Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applica tooVMs in esecuzione Linux solo quando una delle hello approvate per le distribuzioni viene utilizzata con i dettagli di configurazione hello come specificato nelle versioni supportate in [Linux in approvate per Azure Distribuzioni](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
> 

## <a name="option-1-upload-a-vhd"></a>Opzione 1: caricare un disco rigido virtuale

È possibile caricare un disco rigido virtuale personalizzato in esecuzione in un computer locale o che è stato esportato da un altro cloud. disco rigido virtuale hello toouse toocreate una nuova macchina virtuale di Azure, è necessario un archivio di tooa tooupload hello VHD account e creare un disco gestito da hello disco rigido virtuale. 

### <a name="create-a-resource-group"></a>Creare un gruppo di risorse

Prima di caricare il disco personalizzato e la creazione di macchine virtuali, è necessario innanzitutto toocreate un gruppo di risorse con [gruppo az creare](/cli/azure/group#create).

esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *eastus* percorso: [Panoramica di dischi gestiti di Azure](../windows/managed-disks-overview.md)
```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

### <a name="create-a-storage-account"></a>Creare un account di archiviazione

Creare un account di archiviazione per il disco personalizzato e le VM con [az storage account create](/cli/azure/storage/account#create). 

esempio Hello crea un account di archiviazione denominato *mystorageaccount* nel gruppo di risorse hello creato in precedenza:

```azurecli
az storage account create \
    --resource-group myResourceGroup \
    --location eastus \
    --name mystorageaccount \
    --kind Storage \
    --sku Standard_LRS
```

### <a name="list-storage-account-keys"></a>Ottenere chiavi degli account di archiviazione
Azure genera due chiavi di accesso a 512 bit per ogni account di archiviazione. Queste chiavi di accesso vengono utilizzate per l'autenticazione account di archiviazione toohello, ad esempio l'esecuzione di operazioni di scrittura. Altre informazioni sui [gestione accedere qui toostorage](../../storage/common/storage-create-storage-account.md#manage-your-storage-account). Visualizzare le chiavi di accesso hello con [elenco di chiavi di account di archiviazione az](/cli/azure/storage/account/keys#list).

Visualizza chiavi di accesso hello hello account di archiviazione che è stato creato:

```azurecli
az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount
```

output di Hello è simile a:

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK
```
Prendere nota del **key1** come sarà necessario utilizzarlo toointeract con l'account di archiviazione in passaggi successivi hello.

### <a name="create-a-storage-container"></a>Creare un contenitore di archiviazione
In hello allo stesso modo di creare directory diverse toologically organizzare file system locale, creare contenitori all'interno di un tooorganize di account di archiviazione dei dischi. Un account di archiviazione può contenere un numero qualsiasi di contenitori. Creare un contenitore con [az storage container create](/cli/azure/storage/container#create).

esempio Hello crea un contenitore denominato *mydisks*:

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

### <a name="upload-hello-vhd"></a>Caricare hello disco rigido virtuale
Caricare ora il disco personalizzato con [az storage blob upload](/cli/azure/storage/blob#upload). Caricare e archiviare il disco personalizzato come BLOB di pagine.

Specificare la chiave di accesso, il contenitore hello creato nel passaggio precedente hello e quindi hello disco con percorsi toohello personalizzato nel computer locale:

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 \
    --container-name mydisks \
    --type page \
    --file /path/to/disk/mydisk.vhd \
    --name myDisk.vhd
```
Caricamento hello disco rigido virtuale potrebbe richiedere qualche minuto.

### <a name="create-a-managed-disk"></a>Creare un disco gestito


Creare un disco gestito da hello VHD utilizzando [disco az creare](/cli/azure/disk#create). esempio Hello crea un disco gestito denominato *myManagedDisk* caricato dal disco rigido virtuale hello tooyour denominato account di archiviazione e contenitore:

```azurecli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
  --source https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd
```
## <a name="option-2-copy-an-existing-vm"></a>Opzione 2: copiare una macchina virtuale esistente

È inoltre possibile creare hello personalizzato macchina virtuale in Azure e quindi copia disco hello del sistema operativo e di collegarlo tooa nuova VM toocreate un'altra copia. L'operazione è corretta per il test, ma se si desidera toouse una macchina virtuale di Azure esistente come modello hello per più nuove macchine virtuali, è effettivamente necessario creare un **immagine** invece. Per ulteriori informazioni sulla creazione di un'immagine da una macchina virtuale di Azure esistente, vedere [creare un'immagine personalizzata di una macchina virtuale di Azure utilizzando hello CLI](tutorial-custom-images.md)

### <a name="create-a-snapshot"></a>Creare uno snapshot

Questo esempio crea uno snapshot di una macchina virtuale denominata *myVM* nel gruppo di risorse *myResourceGroup* e uno snapshot denominato *osDiskSnapshot*.

```azure-cli
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create \
    -g myResourceGroup \
    --source "$osDiskId" \
    --name osDiskSnapshot
```
###  <a name="create-hello-managed-disk"></a>Disco gestito hello creare

Creare un nuovo disco gestito da snapshot hello.

Ottenere l'ID di hello dello snapshot hello. In questo esempio è denominato snapshot hello *osDiskSnapshot* ed è in hello *myResourceGroup* gruppo di risorse.

```azure-cli
snapshotId=$(az snapshot show --name osDiskSnapshot --resource-group myResourceGroup --query [id] -o tsv)
```

Disco gestito hello creato. In questo esempio, si creerà un disco gestito denominato *myManagedDisk* dallo snapshot che ha una dimensione di 128 GB nell'archiviazione standard.

```azure-cli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
    --sku Standard_LRS \
    --size-gb 128 \
    --source $snapshotId
```

## <a name="create-hello-vm"></a>Creare VM hello

A questo punto, creare la macchina virtuale con [creare vm az](/cli/azure/vm#create) e collegamento (-disco del sistema operativo collegare) hello gestiti disco come disco di hello del sistema operativo. esempio Hello crea una macchina virtuale denominata *myNewVM* utilizzando hello gestito disco creato dal disco rigido virtuale caricato:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNewVM \
    --os-type linux \
    --attach-os-disk myManagedDisk
```

Dovrebbe essere in grado di tooSSH in hello VM utilizzando le credenziali di hello dalla macchina virtuale di origine hello. 

## <a name="next-steps"></a>Passaggi successivi
Dopo avere preparato e caricato il disco rigido virtuale, è possibile ottenere altre informazioni sull' [uso di Azure Resource Manager e dei modelli](../../azure-resource-manager/resource-group-overview.md). È inoltre possibile troppo[aggiungere un disco dati](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour nuove macchine virtuali. Se si dispone di applicazioni in esecuzione in macchine virtuali che è necessario tooaccess, verificare troppo[aprire le porte e gli endpoint](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

