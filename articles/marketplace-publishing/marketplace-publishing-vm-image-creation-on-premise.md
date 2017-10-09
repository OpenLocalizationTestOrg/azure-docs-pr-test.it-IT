---
title: un'immagine di macchina virtuale locale per hello Azure Marketplace aaaCreating | Documenti Microsoft
description: Comprendere ed eseguire i passaggi di hello toocreate un'immagine di macchina virtuale locale e distribuire toohello Azure Marketplace per altri toopurchase.
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 26dfbd5a-8685-4b19-987e-c20ca60540ec
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 04/29/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: c7a265330f1e494db8d0e981a38ee00d85746bb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="develop-an-on-premises-virtual-machine-image-for-hello-azure-marketplace"></a>Sviluppare un'immagine di macchina virtuale locale per hello Azure Marketplace
Si consiglia di sviluppare Azure dischi rigidi virtuali (VHD) direttamente nel cloud hello tramite Remote Desktop Protocol. Tuttavia, se necessario, è possibile toodownload un disco rigido virtuale e sviluppo tramite l'infrastruttura locale.  

Per lo sviluppo locale, è necessario scaricare il sistema operativo hello VHD di hello creato macchina virtuale. Questi passaggi avverrebbero come parte del passaggio 3.3 precedente.  

## <a name="download-a-vhd-image"></a>Scaricare un'immagine di VHD 
### <a name="locate-a-blob-url"></a>Individuare l'URL BLOB
In hello toodownload ordine VHD, individuare innanzitutto URL blob hello per disco del sistema operativo hello.

Individuare nuovi URL blob hello da hello [portale Microsoft Azure](https://portal.azure.com):

1. Andare troppo**Sfoglia** > **macchine virtuali**, e quindi seleziona hello distribuito macchina virtuale.
2. In **configura**selezionare hello **dischi** riquadro, che apre il pannello dischi hello.
   
   ![disegno](media/marketplace-publishing-vm-image-creation-on-premise/img01.png)
3. Seleziona hello **disco del sistema operativo**, che viene aperto un altro pannello contenente le proprietà di disco, inclusi il percorso di VHD hello.
4. Copiare questo URL blob.
   
   ![disegno](media/marketplace-publishing-vm-image-creation-on-premise/img02.png)
5. A questo punto, eliminare hello distribuito una macchina virtuale senza eliminare i dischi di hello sottostante. È anche possibile arrestare hello VM anziché eliminarlo. Non scaricare il disco rigido virtuale del sistema operativo hello quando hello macchina virtuale è in esecuzione.
   
   ![disegno](media/marketplace-publishing-vm-image-creation-on-premise/img03.png)

### <a name="download-a-vhd"></a>Scaricare il VHD
Dopo avere stabilito hello blob URL, è possibile scaricare hello VHD utilizzando hello [portale di Azure](http://manage.windowsazure.com/) o PowerShell.  

> [!NOTE]
> Al momento di hello della creazione di questa Guida, toodownload funzionalità hello un disco rigido virtuale non è ancora presente nel nuovo portale di Microsoft Azure hello.  
> 
> 

**Scaricare hello sistema operativo tramite hello corrente [portale di Azure](http://manage.windowsazure.com/)**

1. Se non è già, accedere toohello portale di Azure.
2. Fare clic su hello **archiviazione** scheda.
3. Selezionare l'account di archiviazione hello all'interno delle quali hello disco rigido virtuale è archiviato.
   
   ![disegno](media/marketplace-publishing-vm-image-creation-on-premise/img04.png)
4. Questo visualizza le proprietà dell'account di archiviazione. Seleziona hello **contenitori** scheda.
   
   ![disegno](media/marketplace-publishing-vm-image-creation-on-premise/img05.png)
5. Selezionare il contenitore di hello in cui hello disco rigido virtuale è archiviato. Per impostazione predefinita, quando creato dal portale di hello, hello VHD è archiviato in un contenitore di dischi rigidi virtuali.
   
   ![disegno](media/marketplace-publishing-vm-image-creation-on-premise/img06.png)
6. Selezionare hello del sistema operativo corretto VHD confrontando hello URL toohello uno che è stato salvato.
7. Fare clic su **Download**.
   
   ![disegno](media/marketplace-publishing-vm-image-creation-on-premise/img07.png)

### <a name="download-a-vhd-by-using-powershell"></a>Scaricare il VHD mediante PowerShell
Inoltre toousing hello portale di Azure, è possibile usare hello [Save-AzureVhd](http://msdn.microsoft.com/library/dn495297.aspx) cmdlet toodownload hello sistema operativo.

        Save-AzureVhd –Source <storageURIOfVhd> `
        -LocalFilePath <diskLocationOnWorkstation> `
        -StorageKey <keyForStorageAccount>
Ad esempio, Save-AzureVhd -Source “https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\baseimagevm.vhd” -StorageKey <String>

> [!NOTE]
> **Save-AzureVhd** dispone anche di un **NumberOfThreads** opzione che può essere utilizzato tooincrease parallelismo toomake hello miglior utilizzo della larghezza di banda disponibile per il download di hello.
> 
> 

## <a name="upload-vhds-tooan-azure-storage-account"></a>Caricare dischi rigidi virtuali tooan account di archiviazione Azure
Se sono preparati i dischi rigidi virtuali locale, è necessario tooupload in uno spazio di archiviazione di account in Azure. Questo passaggio avviene dopo la creazione del VHD locale, ma prima di ottenere una certificazione per l'immagine della macchina virtuale.

### <a name="create-a-storage-account-and-container"></a>Creare un account di archiviazione e un contenitore
È consigliabile che i dischi rigidi virtuali da caricare in un account di archiviazione in un'area in Italia hello. Tutti i VHD per un unico codice SKU devono essere posizionati in un singolo contenitore all'interno di un singolo account di archiviazione.

toocreate un account di archiviazione, è possibile utilizzare hello [portale Microsoft Azure](https://portal.azure.com/), PowerShell o lo strumento da riga di comando di hello Linux.  

**Creare un account di archiviazione dal portale di Microsoft Azure hello**

1. Fare clic su **New**.
2. Selezionare **Archiviazione**.
3. Immettere nome account di archiviazione hello e quindi selezionare un percorso.
   
   ![disegno](media/marketplace-publishing-vm-image-creation-on-premise/img08.png)
4. Fare clic su **Crea**.
5. Pannello Hello hello creato l'account di archiviazione deve essere aperta. In caso contrario, selezionare **Sfoglia** > **Account di archiviazione**. Nell'archiviazione hello account pannello, selezionare l'account di archiviazione hello creato.
6. Selezionare **Contenitori**.
   
   ![disegno](media/marketplace-publishing-vm-image-creation-on-premise/img09.png) 
7. Nel Pannello di contenitori hello, selezionare **Aggiungi**, quindi immettere un nome e hello contenitore le autorizzazioni contenitore. Selezionare **Privato** per le autorizzazioni del contenitore.

> [!TIP]
> È consigliabile creare un contenitore per ogni SKU che si intende toopublish.
> 
> 

  ![disegno](media/marketplace-publishing-vm-image-creation-on-premise/img10.png)

### <a name="create-a-storage-account-by-using-powershell"></a>Creare un account di archiviazione tramite PowerShell
Utilizzo di PowerShell, creare un account di archiviazione tramite hello [New AzureStorageAccount](http://msdn.microsoft.com/library/dn495115.aspx) cmdlet.

        New-AzureStorageAccount -StorageAccountName “mystorageaccount” -Location “West US”

È possibile creare un contenitore all'interno di tale account di archiviazione tramite hello [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) cmdlet.

        New-AzureStorageContainer -Name “containername” -Permission “Off”

> [!NOTE]
> Tali comandi presuppongono che contesto tale account di archiviazione corrente hello è già stata impostata in PowerShell.   Fare riferimento troppo[configurare Azure PowerShell](marketplace-publishing-powershell-setup.md) per ulteriori informazioni sull'installazione di PowerShell.  
> 
> ### <a name="create-a-storage-account-by-using-hello-command-line-tool-for-mac-and-linux"></a>Creare un account di archiviazione usando lo strumento da riga di comando hello per Mac e Linux
> Dallo [strumento da riga di comando per Linux](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)creare un account di archiviazione come segue.
> 
> 

        azure storage account create mystorageaccount --location "West US"

Creare un contenitore come segue.

        azure storage container create containername --account-name mystorageaccount --accountkey <accountKey>

## <a name="upload-a-vhd"></a>Caricare il VHD
Una volta creati account di archiviazione di hello e contenitore, è possibile caricare i dischi rigidi virtuali preparati. È possibile utilizzare PowerShell, lo strumento da riga di comando di hello Linux o altri strumenti di gestione di archiviazione di Azure.

### <a name="upload-a-vhd-via-powershell"></a>Caricare un VHD tramite PowerShell
Hello utilizzare [Add-AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) cmdlet.

        Add-AzureVhd –Destination “http://mystorageaccount.blob.core.windows.net/containername/vmsku.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\vmsku.vhd”

### <a name="upload-a-vhd-by-using-hello-command-line-tool-for-mac-and-linux"></a>Caricare un disco rigido virtuale tramite lo strumento da riga di comando hello per Mac e Linux
Con hello [lo strumento da riga di comando di Linux](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), utilizzare la seguente hello: immagine di macchina virtuale di azure creare <image name> -percorso <Location of hello data center> - sistema operativo Linux<LocationOfLocalVHD>

## <a name="see-also"></a>Vedere anche
* [Creazione di un'immagine di macchina virtuale per hello Marketplace](marketplace-publishing-vm-image-creation.md)
* [Configurazione di Azure PowerShell](marketplace-publishing-powershell-setup.md)

