---
title: disco rigido virtuale aaaUpload file tooAzure DevTest Labs con AzCopy | Documenti Microsoft
description: Caricare l'account di archiviazione del toolab file disco rigido virtuale con AzCopy
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 14f9e933b0bd27451f6bcb94841ecc381213e578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-azcopy"></a>Caricare l'account di archiviazione del toolab file disco rigido virtuale con AzCopy

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

In Azure DevTest Labs, i file VHD possono essere utilizzato toocreate immagini personalizzate, che sono utilizzati tooprovision le macchine virtuali. Hello alla procedura seguente fornisce indicazioni tooupload utilità della riga di comando di AzCopy hello utilizzando account di archiviazione del laboratorio di tooa file disco rigido virtuale. Dopo aver caricato il file VHD, hello [passaggi successivi sezione](#next-steps) elenca alcuni articoli che illustrano come un'immagine personalizzata da hello toocreate caricamento del file di disco rigido virtuale. Per altre informazioni sui dischi e sui dischi rigidi virtuali in Azure, vedere [Informazioni sui dischi e sui dischi rigidi virtuali per le macchine virtuali](../virtual-machines/linux/about-disks-and-vhds.md)

> [!NOTE] 
>  
> AzCopy è un'utilità della riga di comando disponibile solo in Windows.

## <a name="step-by-step-instructions"></a>Istruzioni dettagliate

Hello seguenti passaggi percorso di caricamento di un disco rigido virtuale del file tooAzure DevTest Labs utilizzando [AzCopy](http://aka.ms/downloadazcopy). 

1. Ottenere il nome di hello dell'account di archiviazione dell'ambiente di test di hello utilizzando hello portale di Azure:

1. Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Selezionare **più servizi**, quindi selezionare **DevTest Labs** dall'elenco di hello.

1. Elenco dei laboratori hello selezionare lab desiderato hello.  

1. Nel pannello del lab hello, selezionare **configurazione**. 

1. Lab hello **configurazione** pannello seleziona **immagini personalizzate (VHD)**.

1. In hello **immagini personalizzate** pannello selezionare **+ Aggiungi**. 

1. In hello **immagine personalizzata** pannello seleziona **VHD**.

1. In hello **VHD** pannello seleziona **caricare un disco rigido virtuale con PowerShell**.

    ![Carica un file VHD con PowerShell](./media/devtest-lab-upload-vhd-using-azcopy/upload-image-using-psh.png)

1. Hello **carica un'immagine con PowerShell** pannello viene visualizzato un toohello chiamata **Add-AzureVhd** cmdlet. primo parametro Hello (*destinazione*) contiene hello URI per un contenitore blob (*Carica*) in hello seguente formato:

    ```
    https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...
    ``` 

1. Prendere nota di hello completo URI usato nei passaggi successivi.

1. Caricare file VHD hello tramite AzCopy:
 
1. [Scaricare e installare una versione più recente di hello di AzCopy](http://aka.ms/downloadazcopy).

1. Aprire una finestra di comando e passare toohello AzCopy directory di installazione. Facoltativamente, è possibile aggiungere hello AzCopy tooyour sistema percorso di installazione. Per impostazione predefinita, AzCopy è installato toohello seguente directory:

    ```command-line
    %ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy
    ```

1. Per eseguire hello comando al prompt dei comandi di hello seguente utilizzando hello storage account chiave e del blob URI del contenitore. Hello *vhdFileName* . il valore deve toobe racchiuso tra virgolette. processo Hello di caricamento di un file VHD può essere lungo a seconda delle dimensioni di hello del file VHD hello e la velocità della connessione.   

    ```command-line
    AzCopy /Source:<sourceDirectory> /Dest:<blobContainerUri> /DestKey:<storageAccountKey> /Pattern:"<vhdFileName>" /BlobType:page
    ```

## <a name="next-steps"></a>Passaggi successivi

- [Creare un'immagine personalizzata in Azure DevTest Labs da un file VHD utilizzando hello portale di Azure](devtest-lab-create-template.md)
- [Creare un'immagine personalizzata in Azure DevTest Labs da un file VHD usando PowerShell](devtest-lab-create-custom-image-from-vhd-using-powershell.md)