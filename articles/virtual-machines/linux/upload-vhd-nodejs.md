---
title: un'immagine Linux personalizzata con Azure CLI 1.0 aaaUpload | Documenti Microsoft
description: Creare e caricare un disco rigido virtuale (VHD) di tooAzure con un'immagine Linux personalizzata con modello di distribuzione di gestione risorse di hello e hello Azure CLI 1.0.
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a8c7818f-eb65-409e-aa91-ce5ae975c564
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/10/2016
ms.author: iainfou
ms.openlocfilehash: 0bbd232debee1e632233d1c010e388dbc1548bf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-image-by-using-hello-azure-cli-10"></a>Caricare e creare una VM Linux dall'immagine del disco personalizzato utilizzando hello Azure CLI 1.0
Questo articolo illustra come tooupload un disco rigido virtuale (VHD) di tooAzure utilizzando il modello di distribuzione di gestione risorse di hello e creare macchine virtuali Linux da questa immagine personalizzata. Questa funzionalità consente tooinstall e configurare un requisiti tooyour distribuzione di Linux e quindi utilizzare tale disco rigido virtuale tooquickly creare macchine virtuali di Azure (VM).


## <a name="cli-versions-toocomplete-hello-task"></a>Attività hello toocomplete versioni CLI
È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:

- [Azure CLI 1.0](#quick-commands) : l'interfaccia CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)
- [Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello


## <a name="quick-commands"></a>Comandi rapidi
Se è necessario tooquickly attività hello, hello seguente hello dettagli sezione base tooupload comandi tooAzure una macchina virtuale. Ulteriori informazioni e il contesto per ogni passaggio è reperibile rest hello del documento hello, [avvio qui](#requirements).

Assicurarsi di aver [hello Azure CLI 1.0](../../cli-install-nodejs.md) effettuato l'accesso e utilizzo della modalità di gestione delle risorse:

```azurecli
azure config mode arm
```

In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati. I nomi dei parametri di esempio includono `myResourceGroup`, `mystorageaccount` e `myimages`.

Creare prima un gruppo di risorse. esempio Hello crea un gruppo di risorse denominato `myResourceGroup` in hello `WestUs` percorso:

```azurecli
azure group create myResourceGroup --location "WestUS"
```

Creare un toohold di account di archiviazione dei dischi virtuali. esempio Hello crea un account di archiviazione denominato `mystorageaccount`:

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

Elencare le chiavi di accesso hello dell'account di archiviazione. Annotare il valore di `key1`:

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

Creare un contenitore all'interno dell'account di archiviazione tramite la chiave di archiviazione hello ottenuto. esempio Hello crea un contenitore denominato `myimages` utilizzando hello valore chiave di archiviazione da `key1`:

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

Infine, caricare il contenitore toohello disco rigido virtuale che è stato creato. Specificare percorso locale di hello tooyour disco rigido virtuale in `/path/to/disk/mydisk.vhd`:

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

È ora possibile creare una macchina virtuale dal disco virtuale caricato [utilizzando un modello di Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd). È inoltre possibile utilizzare hello CLI specificando disco tooyour URI di hello (`--image-urn`). esempio Hello crea una macchina virtuale denominata `myVM` mediante hello disco virtuale caricato in precedenza:

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
```

account di archiviazione di destinazione Hello è toobe hello stesso come in cui è caricato il disco virtuale. Inoltre necessario toospecify o rispondere a richieste di, tutti i parametri aggiuntivi richiesti dal hello di hello `azure vm create` comando, ad esempio una rete virtuale, indirizzo IP pubblico, nome utente e le chiavi SSH. Altre informazioni su hello [parametri di gestione risorse di CLI disponibili](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).

## <a name="requirements"></a>Requisiti
hello toocomplete seguendo la procedura, è necessario:

* **Sistema operativo Linux installato in un file con estensione vhd** -installare un [distribuzione Linux approvate per Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (o vedere [informazioni per distribuzioni non approvate](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa disco virtuale in hello disco rigido virtuale formato. Più strumenti esistono toocreate una macchina virtuale e disco rigido virtuale:
  * Installare e configurare [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) o [KVM](http://www.linux-kvm.org/page/RunningKVM), prestando attenzione toouse il formato di immagine disco rigido virtuale. Se necessario, è possibile [convertire un'immagine](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) usando `qemu-img convert`.
  * È anche possibile usare Hyper-V [in Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) o [in Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).

> [!NOTE]
> il formato VHDX più recente di Hello non è supportato in Azure. Quando si crea una macchina virtuale, è possibile specificare file VHD come formato hello. Se necessario, è possibile convertire VHDX dischi tooVHD con [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) o hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) cmdlet di PowerShell. Inoltre, Azure non supporta il caricamento di dischi rigidi virtuali dinamici, pertanto è necessario tooconvert tali toostatic dischi VHD prima del caricamento. È possibile utilizzare strumenti come [utilità di disco rigido virtuale di Azure per passare](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dischi dinamici durante il processo di hello di caricamento tooAzure.
> 
> 

* Macchine virtuali create da un'immagine personalizzata devono risiedere in hello stesso account di archiviazione come immagine di hello stessa
  * Creare un toohold account e il contenitore di archiviazione creato le macchine virtuali sia l'immagine personalizzata
  * Una volta create tutte le VM, è possibile eliminare l'immagine.

Assicurarsi di aver [hello Azure CLI 1.0](../../cli-install-nodejs.md) effettuato l'accesso e utilizzo della modalità di gestione delle risorse:

```azurecli
azure config mode arm
```

In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati. I nomi dei parametri di esempio includono `myResourceGroup`, `mystorageaccount` e `myimages`.

<a id="prepimage"></a>

## <a name="prepare-hello-image-toobe-uploaded"></a>Preparare hello immagine toobe caricato
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


## <a name="create-a-resource-group"></a>Creare un gruppo di risorse
Gruppi di risorse in modo logico riunire toosupport di risorse di Azure hello tutte le macchine virtuali, ad esempio una rete virtuale hello e archiviazione. Ulteriori informazioni sui [gruppi di risorse di Azure sono disponibili qui](../../azure-resource-manager/resource-group-overview.md). Prima di caricare l'immagine del disco personalizzato e la creazione di macchine virtuali, è necessario innanzitutto toocreate un gruppo di risorse. 

esempio Hello crea un gruppo di risorse denominato `myResourceGroup` in hello `WestUS` percorso:

```azurecli
azure group create myResourceGroup --location "WestUS"
```

## <a name="create-a-storage-account"></a>Creare un account di archiviazione
Le VM vengono archiviate come BLOB di pagine all'interno di un account di archiviazione. Ulteriori informazioni sull' [archiviazione BLOB di Azure sono disponibili qui](../../storage/common/storage-introduction.md#blob-storage). Creare un account di archiviazione per l'immagine disco personalizzata e le VM. Tutte le macchine virtuali che vengono creati tramite il toobe necessità di immagine disco personalizzata in hello stesso account di archiviazione dell'immagine.

esempio Hello crea un account di archiviazione denominato `mystorageaccount` nel gruppo di risorse hello creato in precedenza:

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

## <a name="list-storage-account-keys"></a>Ottenere chiavi degli account di archiviazione
Azure genera due chiavi di accesso a 512 bit per ogni account di archiviazione. Queste chiavi di accesso vengono utilizzate per l'autenticazione account di archiviazione toohello, ad esempio toocarry le operazioni di scrittura. Altre informazioni sui [gestione accedere qui toostorage](../../storage/common/storage-create-storage-account.md#manage-your-storage-account). È possibile visualizzare i tasti di scelta con hello `azure storage account keys list` comando.

Visualizza chiavi di accesso hello hello account di archiviazione che è stato creato:

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
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
In hello allo stesso modo di creare directory diverse toologically organizzare file system locale, creare contenitori all'interno di un tooorganize di account di archiviazione, i dischi virtuali e le immagini. Un account di archiviazione può contenere un numero qualsiasi di contenitori. 

esempio Hello crea un contenitore denominato `myimages`, che specifica la chiave di accesso hello ottenuto nel passaggio precedente hello (`key1`):

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

## <a name="upload-vhd"></a>Caricare il file VHD.
Ora è effettivamente possibile caricare l'immagine disco personalizzata. Come con tutti i dischi virtuali utilizzati dalle VM, l'immagine disco personalizzata viene caricata e archiviata come BLOB di pagine.

Specificare la chiave di accesso, il contenitore hello creato nel passaggio precedente hello e quindi hello immagine di disco personalizzata toohello percorso sul computer locale:

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

## <a name="create-vm-from-custom-image"></a>Creare una VM in base a un'immagine personalizzata
Quando si creano le macchine virtuali dall'immagine disco personalizzata, specificare l'immagine del disco toohello hello URI. Verificare che hello corrispondenze di account di archiviazione destinazione dove viene archiviata l'immagine disco personalizzata. È possibile creare la macchina virtuale usando il modello di CLI di Azure o Gestione risorse JSON hello.

### <a name="create-a-vm-using-hello-azure-cli"></a>Creare una macchina virtuale utilizzando hello CLI di Azure
Specificare hello `--image-urn` parametro hello `azure vm create` immagine disco personalizzata tooyour toopoint del comando. Verificare che `--storage-account-name` corrispondenze hello account di archiviazione dove viene archiviata l'immagine disco personalizzata. Non si dispone toouse hello stesso contenitore come hello toostore immagine disco personalizzata nelle macchine virtuali. Apportare eventuali altri contenitori che toocreate hello come hello passaggi precedenti prima di caricare immagini del disco rigido personalizzato.

esempio Hello crea una macchina virtuale denominata `myVM` dall'immagine disco personalizzata:

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
    --storage-account-name mystorageaccount
```

È comunque necessario toospecify o rispondere a richieste di, tutti i parametri aggiuntivi richiesti dal hello di hello `azure vm create` comando, ad esempio una rete virtuale, indirizzo IP pubblico, nome utente e le chiavi SSH. Altre informazioni su hello [parametri di gestione risorse di CLI disponibili](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).

### <a name="create-a-vm-using-a-json-template"></a>Creare una VM utilizzando un modello JSON
Modelli di gestione risorse di Azure sono i file JavaScript Object Notation (JSON) che definiscono l'ambiente hello desiderato toobuild. modelli di Hello sono suddivisi in toodifferent i provider di risorse, ad esempio compute o rete. È possibile utilizzare i modelli esistenti o crearne di nuovi. Altre informazioni sull' [uso di Resource Manager e relativi modelli](../../azure-resource-manager/resource-group-overview.md).

All'interno di hello `Microsoft.Compute/virtualMachines` provider del modello, è un `storageProfile` nodo che contiene i dettagli di configurazione hello per la macchina virtuale. Hello due parametri principali tooedit sono hello `image` e `vhd` URI che puntano immagine disco personalizzata tooyour e il disco virtuale della nuova macchina virtuale. esempio Hello viene illustrato un esempio di hello JSON per l'utilizzo di un'immagine del disco personalizzato:

```json
"storageProfile": {
          "osDisk": {
            "name": "myVM",
            "osType": "Linux",
            "caching": "ReadWrite",
            "createOption": "FromImage",
            "image": {
              "uri": "https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd"
            },
            "vhd": {
              "uri": "https://mystorageaccount.blob.core.windows.net/vhds/newvmname.vhd"
            }
          }
```

È possibile utilizzare [questo toocreate modello esistente di una macchina virtuale da un'immagine personalizzata](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) o leggere le informazioni sulle [la creazione di modelli di Azure Resource Manager](../../azure-resource-manager/resource-group-authoring-templates.md). 

Dopo aver creato un modello configurato, creare le macchine virtuali utilizzando hello `azure group deployment create` comando. Specificare l'URI del modello di JSON hello con hello `--template-uri` parametro:

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-uri https://uri.to.template/mytemplate.json
```

Se si dispone di un file JSON archiviato localmente nel computer in uso, è possibile utilizzare hello `--template-file` parametro invece:

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a>Passaggi successivi
Dopo avere preparato e caricato il disco rigido virtuale, è possibile ottenere altre informazioni sull' [uso di Azure Resource Manager e dei modelli](../../azure-resource-manager/resource-group-overview.md). È inoltre possibile troppo[aggiungere un disco dati](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour nuove macchine virtuali. Se si dispone di applicazioni in esecuzione in macchine virtuali che è necessario tooaccess, verificare troppo[aprire le porte e gli endpoint](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

