---
title: un disco Linux personalizzato con Azure CLI 2.0 aaaUpload | Documenti Microsoft
description: Creare e caricare un disco rigido virtuale (VHD) di tooAzure con modello di distribuzione di gestione risorse di hello e hello Azure CLI 2.0
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
ms.date: 07/10/2017
ms.author: cynthn
ms.openlocfilehash: cf8556ab4dfe6c4e5eff4e99fe1ddc44393f774c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-with-hello-azure-cli-20"></a>Caricare e creare una VM Linux da disco personalizzato con hello Azure CLI 2.0
In questo articolo viene illustrato come tooupload account tooan un disco rigido virtuale (VHD) di archiviazione di Azure con hello 2.0 CLI di Azure e creare le macchine virtuali Linux dal disco personalizzato. È anche possibile eseguire questi passaggi con hello [CLI di Azure 1.0](upload-vhd-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Questa funzionalità consente tooinstall e configurare un requisiti tooyour distribuzione di Linux e quindi utilizzare tale disco rigido virtuale tooquickly creare macchine virtuali di Azure (VM).

Questo argomento viene utilizzato l'account di archiviazione per hello finali dischi rigidi virtuali, ma è inoltre possibile eseguire questi passaggi tramite [dischi gestiti](upload-vhd.md). 

## <a name="quick-commands"></a>Comandi rapidi
Se è necessario tooquickly attività hello, hello seguente hello dettagli sezione base tooupload comandi tooAzure un disco rigido virtuale. Ulteriori informazioni e il contesto per ogni passaggio è reperibile rest hello del documento hello, [avvio qui](#requirements).

Assicurarsi di aver hello più recente [CLI di Azure 2.0](/cli/azure/install-az-cli2) installato e registrato con un account Azure tooan [accesso az](/cli/azure/#login).

In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati. I nomi dei parametri di esempio includono `myResourceGroup`, `mystorageaccount` e `mydisks`.

Creare prima un gruppo di risorse con [az group create](/cli/azure/group#create). esempio Hello crea un gruppo di risorse denominato `myResourceGroup` in hello `WestUs` percorso:

```azurecli
az group create --name myResourceGroup --location westus
```

Creare un toohold di account di archiviazione dei dischi virtuali con [creare account di archiviazione az](/cli/azure/storage/account#create). esempio Hello crea un account di archiviazione denominato `mystorageaccount`:

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

Elencare le chiavi di accesso hello per l'account di archiviazione con [elenco di chiavi di account di archiviazione az](/cli/azure/storage/account/keys#list). Annotare il valore di `key1`:

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
```

Creare un contenitore all'interno dell'account di archiviazione tramite la chiave di archiviazione hello ottenuto con [creare il contenitore di archiviazione az](/cli/azure/storage/container#create). esempio Hello crea un contenitore denominato `mydisks` utilizzando hello valore chiave di archiviazione da `key1`:

```azurecli
az storage container create --account-name mystorageaccount \
    --account-key key1 --name mydisks
```

Infine, caricare il contenitore di toohello disco rigido virtuale è stato creato con [caricamento blob di archiviazione az](/cli/azure/storage/blob#upload). Specificare percorso locale di hello tooyour disco rigido virtuale in `/path/to/disk/mydisk.vhd`:

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

Specificare hello URI tooyour disco (`--image`) con [creare vm az](/cli/azure/vm#create). esempio Hello crea una macchina virtuale denominata `myVM` mediante hello disco virtuale caricato in precedenza:

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisk/myDisks.vhd \
    --use-unmanaged-disk
```

account di archiviazione di destinazione Hello è toobe hello stesso come in cui è caricato il disco virtuale. Inoltre necessario toospecify o rispondere a richieste di, tutti i parametri aggiuntivi richiesti dal hello di hello **creare vm az** comando, ad esempio una rete virtuale, indirizzo IP pubblico, nome utente e le chiavi SSH. Altre informazioni su hello [parametri di gestione risorse di CLI disponibili](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).

## <a name="requirements"></a>Requisiti
hello toocomplete seguendo la procedura, è necessario:

* **Sistema operativo Linux installato in un file con estensione vhd** -installare un [distribuzione Linux approvate per Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (o vedere [informazioni per distribuzioni non approvate](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa disco virtuale in hello disco rigido virtuale formato. Più strumenti esistono toocreate una macchina virtuale e disco rigido virtuale:
  * Installare e configurare [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) o [KVM](http://www.linux-kvm.org/page/RunningKVM), prestando attenzione toouse il formato di immagine disco rigido virtuale. Se necessario, è possibile [convertire un'immagine](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) usando `qemu-img convert`.
  * È anche possibile usare Hyper-V [in Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) o [in Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).

> [!NOTE]
> il formato VHDX più recente di Hello non è supportato in Azure. Quando si crea una macchina virtuale, è possibile specificare file VHD come formato hello. Se necessario, è possibile convertire VHDX dischi tooVHD con [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) o hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) cmdlet di PowerShell. Inoltre, Azure non supporta il caricamento di dischi rigidi virtuali dinamici, pertanto è necessario tooconvert tali toostatic dischi VHD prima del caricamento. È possibile utilizzare strumenti come [utilità di disco rigido virtuale di Azure per passare](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dischi dinamici durante il processo di hello di caricamento tooAzure.
> 
> 

* Macchine virtuali create dal disco personalizzato devono risiedere in hello stesso account di archiviazione come disco hello
  * Creare un toohold account e il contenitore di archiviazione, il disco personalizzato e le macchine virtuali create
  * Una volta create tutte le VM, è possibile eliminare il disco

Assicurarsi di aver hello più recente [CLI di Azure 2.0](/cli/azure/install-az-cli2) installato e registrato con un account Azure tooan [accesso az](/cli/azure/#login).

In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati. I nomi dei parametri di esempio includono `myResourceGroup`, `mystorageaccount` e `mydisks`.

<a id="prepimage"></a>

## <a name="prepare-hello-disk-toobe-uploaded"></a>Preparare hello disco toobe caricato
Azure supporta svariate distribuzioni di Linux (vedere la sezione [Distribuzioni approvate](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Hello seguenti articoli semplificato come tooprepare hello diverse distribuzioni di Linux che sono supportate in Azure:

* **[Distribuzioni basate su CentOS](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[SLES e openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Altro - Distribuzioni non approvate](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**

Vedere anche hello  **[note sull'installazione di Linux](create-upload-generic.md#general-linux-installation-notes)**  per suggerimenti generali sulla preparazione di immagini Linux per Azure.

> [!NOTE]
> Hello [contratto di servizio di piattaforma Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/) applica tooVMs in esecuzione Linux solo quando una delle hello approvate per le distribuzioni viene utilizzata con i dettagli di configurazione hello come specificato nelle versioni supportate in [Linux in approvate per Azure Distribuzioni](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
> 

## <a name="create-a-resource-group"></a>Creare un gruppo di risorse
Gruppi di risorse in modo logico riunire toosupport di risorse di Azure hello tutte le macchine virtuali, ad esempio una rete virtuale hello e archiviazione. Per altre informazioni sui gruppi di risorse, vedere la [panoramica dei gruppi di risorse](../../azure-resource-manager/resource-group-overview.md). Prima di caricare il disco personalizzato e la creazione di macchine virtuali, è necessario innanzitutto toocreate un gruppo di risorse con [gruppo az creare](/cli/azure/group#create).

esempio Hello crea un gruppo di risorse denominato `myResourceGroup` in hello `westus` percorso:

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-a-storage-account"></a>Creare un account di archiviazione

Creare un account di archiviazione per il disco personalizzato e le VM con [az storage account create](/cli/azure/storage/account#create). Tutte le macchine virtuali con dischi non gestite che vengono creati tramite il toobe necessità disco personalizzata in hello stesso account di archiviazione come disco. 

esempio Hello crea un account di archiviazione denominato `mystorageaccount` nel gruppo di risorse hello creato in precedenza:

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

## <a name="list-storage-account-keys"></a>Ottenere chiavi degli account di archiviazione
Azure genera due chiavi di accesso a 512 bit per ogni account di archiviazione. Queste chiavi di accesso vengono utilizzate per l'autenticazione account di archiviazione toohello, ad esempio toocarry le operazioni di scrittura. Altre informazioni sui [gestione accedere qui toostorage](../../storage/common/storage-create-storage-account.md#manage-your-storage-account). Visualizzare le chiavi di accesso hello con [elenco di chiavi di account di archiviazione az](/cli/azure/storage/account/keys#list).

Visualizza chiavi di accesso hello hello account di archiviazione che è stato creato:

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
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
Prendere nota del `key1` come sarà necessario utilizzarlo toointeract con l'account di archiviazione in passaggi successivi hello.

## <a name="create-a-storage-container"></a>Creare un contenitore di archiviazione
In hello allo stesso modo di creare directory diverse toologically organizzare file system locale, creare contenitori all'interno di un tooorganize di account di archiviazione dei dischi. Un account di archiviazione può contenere un numero qualsiasi di contenitori. Creare un contenitore con [az storage container create](/cli/azure/storage/container#create).

esempio Hello crea un contenitore denominato `mydisks`:

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

## <a name="upload-vhd"></a>Caricare il file VHD.
Caricare ora il disco personalizzato con [az storage blob upload](/cli/azure/storage/blob#upload). Caricare e archiviare il disco personalizzato come BLOB di pagine.

Specificare la chiave di accesso, il contenitore hello creato nel passaggio precedente hello e quindi hello disco con percorsi toohello personalizzato nel computer locale:

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

## <a name="create-hello-vm"></a>Creare VM hello
toocreate una macchina virtuale con dischi non gestiti, specificare disco tooyour URI di hello (`--image`) con [creare vm az](/cli/azure/vm#create). esempio Hello crea una macchina virtuale denominata `myVM` mediante hello disco virtuale caricato in precedenza:

Specificare hello `--image` parametro con [creare vm az](/cli/azure/vm#create) toopoint tooyour personalizzato disco. Verificare che `--storage-account` corrispondenze hello account di archiviazione in cui è memorizzato nel disco personalizzato. Non si dispone toouse hello stesso contenitore come hello toostore disco personalizzata nelle macchine virtuali. Apportare eventuali altri contenitori che toocreate hello come hello passaggi precedenti prima di caricare il disco personalizzato.

esempio Hello crea una macchina virtuale denominata `myVM` dal disco personalizzato:

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd \
    --use-unmanaged-disk
```

È comunque necessario toospecify o rispondere a richieste di, tutti i parametri aggiuntivi richiesti dal hello di hello **creare vm az** comando, ad esempio nome utente e le chiavi SSH.


## <a name="resource-manager-template"></a>Modello di Resource Manager
Modelli di gestione risorse di Azure sono i file JavaScript Object Notation (JSON) che definiscono l'ambiente hello desiderato toobuild. modelli di Hello sono suddivisi in toodifferent i provider di risorse, ad esempio compute o rete. È possibile utilizzare i modelli esistenti o crearne di nuovi. Altre informazioni sull' [uso di Resource Manager e relativi modelli](../../azure-resource-manager/resource-group-overview.md).

All'interno di hello `Microsoft.Compute/virtualMachines` provider del modello, è un `storageProfile` nodo che contiene i dettagli di configurazione hello per la macchina virtuale. Hello due parametri principali tooedit sono hello `image` e `vhd` URI che puntano tooyour personalizzato e disco virtuale della nuova macchina virtuale. esempio Hello viene illustrato un esempio di hello JSON per l'utilizzo di un disco personalizzato:

```json
"storageProfile": {
          "osDisk": {
            "name": "myVM",
            "osType": "Linux",
            "caching": "ReadWrite",
            "createOption": "FromImage",
            "image": {
              "uri": "https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd"
            },
            "vhd": {
              "uri": "https://mystorageaccount.blob.core.windows.net/vhds/newvmname.vhd"
            }
          }
```

È possibile utilizzare [questo toocreate modello esistente di una macchina virtuale da un'immagine personalizzata](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) o leggere le informazioni sulle [la creazione di modelli di Azure Resource Manager](../../azure-resource-manager/resource-group-authoring-templates.md). 

Dopo aver creato un modello configurato, utilizzare [distribuzione gruppo az creare](/cli/azure/group/deployment#create) toocreate le macchine virtuali. Specificare l'URI del modello di JSON hello con hello `--template-uri` parametro:

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-uri https://uri.to.template/mytemplate.json
```

Se si dispone di un file JSON archiviato localmente nel computer in uso, è possibile utilizzare hello `--template-file` parametro invece:

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a>Passaggi successivi
Dopo avere preparato e caricato il disco rigido virtuale, è possibile ottenere altre informazioni sull' [uso di Azure Resource Manager e dei modelli](../../azure-resource-manager/resource-group-overview.md). È inoltre possibile troppo[aggiungere un disco dati](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour nuove macchine virtuali. Se si dispone di applicazioni in esecuzione in macchine virtuali che è necessario tooaccess, verificare troppo[aprire le porte e gli endpoint](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

