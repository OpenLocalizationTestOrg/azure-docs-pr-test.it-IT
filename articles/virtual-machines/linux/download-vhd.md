---
title: aaaDownload un VHD Linux di Azure | Documenti Microsoft
description: Scaricare un VHD Linux utilizzando hello Azure CLI e hello portale di Azure.
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: davidmu
ms.openlocfilehash: 7e08e985a64a6be581b8f5eedcce60fbd314eaf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="download-a-linux-vhd-from-azure"></a>Scaricare un disco rigido virtuale Linux da Azure

In questo articolo viene illustrato come toodownload un [Linux disco rigido virtuale (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) file da Azure tramite hello Azure CLI e portale di Azure. 

Macchine virtuali (VM) in uso Azure [dischi](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) come un toostore sul posto del sistema operativo, applicazioni e dati. Tutte le macchine virtuali di Azure dispongono di almeno due dischi: un disco del sistema operativo Windows e un disco temporaneo. disco del sistema operativo Hello viene inizialmente creato da un'immagine e il disco di sistema operativo hello e immagine hello sono dischi rigidi virtuali archiviati in un account di archiviazione di Azure. Anche le macchine virtuali possono disporre di uno o più dischi dati archiviati in dischi rigidi virtuali.

Installare l'[interfaccia della riga di comando di Azure 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2), se non è già installata.

## <a name="stop-hello-vm"></a>Arrestare VM hello

Un disco rigido virtuale non può essere scaricato da Azure se è collegato tooa in esecuzione sulla macchina virtuale. È necessario toodownload VM hello toostop un disco rigido virtuale. Se si desidera toouse un disco rigido virtuale come un [immagine](tutorial-custom-images.md) toocreate altre macchine virtuali con nuovi dischi, è necessario toodeprovision e generalizzare sistema operativo hello contenuto in hello arrestare VM hello e file. hello toouse VHD come disco per una nuova istanza della macchina virtuale esistente o disco dati, solo necessario toostop e deallocare hello macchina virtuale.

toouse hello VHD come toocreate un'immagine con altre macchine virtuali, completare questi passaggi:

1. Usare SSH, nome dell'account hello e indirizzo IP pubblico hello di hello VM tooconnect tooit e deprovisioning. salve + utente parametro anche rimuove l'ultimo account di provisioning utente hello. Se si sono salvare le credenziali dell'account in toohello VM, omettere questo parametro utente +. Hello esempio seguente viene rimosso ultimo account di provisioning utente hello:

    ```bash
    ssh azureuser@40.118.249.235
    sudo waagent -deprovision+user -force
    exit 
    ```

2. Accedi tooyour account Azure con [accesso az](https://docs.microsoft.com/cli/azure/#login).
3. Arrestare e deallocare hello macchina virtuale.

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

4. Generalizzare hello macchina virtuale. 

    ```azurecli
    az vm generalize --resource-group myResourceGroup --name myVM
    ``` 

hello toouse VHD come disco per una nuova istanza della macchina virtuale esistente o disco dati, completare questi passaggi:

1.  Accedi toohello [portale di Azure](https://portal.azure.com/).
2.  Nel menu Hub hello, fare clic su **macchine virtuali**.
3.  Selezionare hello VM hello elenco.
4.  Nel Pannello di hello per hello VM, fare clic su **arrestare**.

    ![Arrestare la macchina virtuale](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a>Generare l'URL SAS

file di disco rigido virtuale hello toodownload, è necessario toogenerate un [firma di accesso condiviso (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL. Quando viene generato l'URL di hello, un'ora di scadenza viene assegnata toohello URL.

1.  Dal menu hello del pannello hello hello VM, fare clic su **dischi**.
2.  Selezionare il disco del sistema operativo hello per hello macchina virtuale e quindi fare clic su **esportare**.
3.  Fare clic su **Genera URL**.

    ![Generare l'URL](./media/download-vhd/export-generate.png)

## <a name="download-vhd"></a>Scaricare il disco rigido virtuale

1.  In URL hello che è stato generato, fare clic su file VHD hello di Download.

    ![Scaricare il disco rigido virtuale](./media/download-vhd/export-download.png)

2.  Potrebbe essere necessario tooclick **salvare** nel download di hello browser toostart hello. il nome predefinito Hello per file di disco rigido virtuale hello è *abcd*.

    ![Fare clic su Salva nel browser hello](./media/download-vhd/export-save.png)

## <a name="next-steps"></a>Passaggi successivi

- Informazioni su come troppo[caricare e creare una VM Linux da disco personalizzato con hello Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 
- [Gestire i dischi Azure hello Azure CLI](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

