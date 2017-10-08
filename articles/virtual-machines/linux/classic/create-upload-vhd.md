---
title: aaaCreate e caricare un tooAzure VHD Linux | Documenti Microsoft
description: Creare e caricare un Azure disco rigido virtuale (VHD) che contiene sistema operativo Linux di hello utilizzando hello modello di distribuzione classica
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8058ff98-db03-4309-9bf4-69842bd64dd4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: iainfou
ms.openlocfilehash: 77b01316386c4a6eb68c129fa68d42f0a8996edc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-and-uploading-a-virtual-hard-disk-that-contains-hello-linux-operating-system"></a>Creazione e caricamento di un disco rigido virtuale contenente hello del sistema operativo Linux
> [!IMPORTANT] 
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni. È anche possibile [caricare un'immagine disco personalizzata tramite Azure Resource Manager](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Questo articolo illustra come toocreate e caricare un disco rigido virtuale (VHD), è possibile utilizzarlo come la propria immagine toocreate di macchine virtuali in Azure. Informazioni su come il sistema operativo hello tooprepare quindi è possibile usare toocreate più macchine virtuali in base che l'immagine. 


## <a name="prerequisites"></a>Prerequisiti
Questo articolo si presuppone di aver hello seguenti elementi:

* **Sistema operativo Linux installato in un file con estensione vhd** -è stato installato un [distribuzione Linux approvate per Azure](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (o vedere [informazioni per distribuzioni non approvate](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) disco virtuale tooa in formato VHD hello. Più strumenti esistono toocreate una macchina virtuale e disco rigido virtuale:
  * Installare e configurare [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) o [KVM](http://www.linux-kvm.org/page/RunningKVM), prestando attenzione toouse il formato di immagine disco rigido virtuale. Se necessario, è possibile [convertire un'immagine](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) usando `qemu-img convert`.
  * È anche possibile usare Hyper-V [in Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) o [in Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).

> [!NOTE]
> il formato VHDX più recente di Hello non è supportato in Azure. Quando si crea una macchina virtuale, è possibile specificare file VHD come formato hello. Se necessario, è possibile convertire VHDX dischi tooVHD con [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) o hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) cmdlet di PowerShell. Inoltre, Azure non supporta il caricamento di dischi rigidi virtuali dinamici, pertanto è necessario tooconvert tali toostatic dischi VHD prima del caricamento. È possibile utilizzare strumenti come [utilità di disco rigido virtuale di Azure per passare](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dischi dinamici durante il processo di hello di caricamento tooAzure.

* **Interfaccia della riga di comando di Azure** -hello installazione più recente [interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) hello tooupload disco rigido virtuale.

<a id="prepimage"></a>

## <a name="step-1-prepare-hello-image-toobe-uploaded"></a>Passaggio 1: Preparare hello immagine toobe caricato
Azure supporta svariate distribuzioni di Linux (vedere la sezione [Distribuzioni approvate](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Hello seguenti articoli illustra come tooprepare hello diverse distribuzioni di Linux che sono supportate in Azure. Dopo aver completato i passaggi seguenti guide hello hello, sono disponibili qui dopo aver un file VHD che è pronto tooupload tooAzure:

* **[Distribuzioni basate su CentOS](../create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Debian Linux](../debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Oracle Linux](../oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Red Hat Enterprise Linux](../redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[SLES e openSUSE](../suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Ubuntu](../create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Altro - Distribuzioni non approvate](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**

> [!NOTE]
> contratto di servizio di piattaforma Azure Hello applica toovirtual computer hello viene utilizzato solo quando una delle hello approvate per le distribuzioni del sistema operativo Linux con i dettagli di configurazione hello come specificato nelle versioni supportate [Linux in distribuzioni Azure-Endorsed ](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Tutte le distribuzioni di Linux nella raccolta di immagini di Azure hello sono avallate distribuzioni con la configurazione richiesta hello.
> 
> 

Vedere anche hello  **[note sull'installazione di Linux](../create-upload-generic.md#general-linux-installation-notes)**  per suggerimenti generali sulla preparazione di immagini Linux per Azure.

<a id="connect"></a>

## <a name="step-2-prepare-hello-connection-tooazure"></a>Passaggio 2: Preparare hello connessione tooAzure
Assicurarsi che si utilizza il modello di distribuzione classica hello Ciao CLI di Azure (`azure config mode asm`), quindi accedi tooyour account:

```azurecli
azure login
```


<a id="upload"></a>

## <a name="step-3-upload-hello-image-tooazure"></a>Passaggio 3: Caricare hello immagine tooAzure
È necessario un tooupload di account di archiviazione di file di disco rigido virtuale per. È possibile usare un account di archiviazione esistente o [crearne uno nuovo](../../../storage/common/storage-create-storage-account.md).

Usare hello Azure CLI tooupload hello immagine utilizzando hello comando seguente:

```azurecli
azure vm image create <ImageName> `
    --blob-url <BlobStorageURL>/<YourImagesFolder>/<VHDName> `
    --os Linux <PathToVHDFile>
```

Nell'esempio precedente hello:

* **BlobStorageURL** hello URL per l'account di archiviazione hello Prevedi toouse
* **YourImagesFolder** è il contenitore di hello nell'archiviazione blob in cui si desidera toostore delle immagini
* **VHDName** è hello etichetta visualizzata nel disco rigido virtuale di portale tooidentify hello.
* **PathToVHDFile** è hello di percorso completo e il nome del file con estensione vhd hello nel computer.

Hello comando seguente viene illustrato un esempio completo:

```azurecli
azure vm image create myImage `
    --blob-url https://mystorage.blob.core.windows.net/vhds/myimage.vhd `
    --os Linux /home/ahmet/myimage.vhd
```

## <a name="step-4-create-a-vm-from-hello-image"></a>Passaggio 4: Creare una macchina virtuale dall'immagine hello
Si crea una macchina virtuale utilizzando `azure vm create` in hello esattamente come una macchina virtuale di regolare. Specificare nome hello assegnato l'immagine nel passaggio precedente hello. Nel seguente esempio di hello, utilizziamo hello **myImage** nome immagine fornito nel passaggio precedente hello:

```azurecli
azure vm create --userName ops --password P@ssw0rd! --vm-size Small --ssh `
    --location "West US" "myDeployedVM" myImage
```

toocreate le proprie macchine virtuali, fornire la propria username + password, indirizzo, nome DNS e nome dell'immagine.

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni, vedere [riferimento CLI di Azure per il modello di distribuzione classica Azure hello](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).

[Step 1: Prepare hello image toobe uploaded]:#prepimage
[Step 2: Prepare hello connection tooAzure]:#connect
[Step 3: Upload hello image tooAzure]:#upload
