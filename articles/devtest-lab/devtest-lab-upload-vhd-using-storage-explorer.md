---
title: disco rigido virtuale aaaUpload file tooAzure DevTest Labs tramite Esplora archivi di Microsoft Azure | Documenti Microsoft
description: Caricare l'account di archiviazione del toolab file disco rigido virtuale tramite Esplora archivi di Microsoft Azure
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
ms.openlocfilehash: 686691e3676cea4b2d7cd8bf045bc43a792c667e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-microsoft-azure-storage-explorer"></a>Caricare l'account di archiviazione del toolab file disco rigido virtuale tramite Esplora archivi di Microsoft Azure

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

In Azure DevTest Labs, i file VHD possono essere utilizzato toocreate immagini personalizzate, che sono utilizzati tooprovision le macchine virtuali. Questo articolo illustra come toouse [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) account di archiviazione dell'ambiente di test di tooa tooupload un disco rigido virtuale del file. Dopo aver caricato il file VHD, hello [passaggi successivi sezione](#next-steps) elenca alcuni articoli che illustrano come un'immagine personalizzata da hello toocreate caricamento del file di disco rigido virtuale. Per altre informazioni sui dischi e sui dischi rigidi virtuali in Azure, vedere [Informazioni sui dischi e sui dischi rigidi virtuali per le macchine virtuali](../virtual-machines/linux/about-disks-and-vhds.md)

## <a name="step-by-step-instructions"></a>Istruzioni dettagliate

Hello seguenti passaggi percorso di caricamento di un disco rigido virtuale del file Labs tooDevTest utilizzando [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).

1. [Scaricare e installare hello la versione più recente di Microsoft Azure Storage Explorer hello](http://www.storageexplorer.com).

1. Ottenere il nome di hello dell'account di archiviazione dell'ambiente di test di hello utilizzando hello portale di Azure:

    1. Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
    
    1. Selezionare **più servizi**, quindi selezionare **DevTest Labs** dall'elenco di hello.
    
    1. Elenco dei laboratori hello selezionare lab desiderato hello.  
    
    1. Nel pannello del lab hello, selezionare **configurazione**. 
    
    1. Lab hello **configurazione** pannello seleziona **immagini personalizzate (VHD)**.
    
    1. In hello **immagini personalizzate** pannello selezionare **+ Aggiungi**. 
    
    1. In hello **immagine personalizzata** pannello seleziona **VHD**.
    
    1. In hello **VHD** pannello seleziona **caricare un disco rigido virtuale con PowerShell**.
    
        ![Carica un file VHD con PowerShell][0]
    
    1. Hello **carica un'immagine con PowerShell** pannello viene visualizzato un toohello chiamata **Add-AzureVhd** cmdlet. primo parametro Hello (*destinazione*) il nome di account di archiviazione di hello per lab hello in hello seguente formato:
    
        https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/... 

    1. Prendere nota del nome di account di archiviazione hello perché è usato nei passaggi successivi.
    
1. Connettersi tooan account di sottoscrizione di Azure tramite Esplora archivi.

    > [!TIP] 
    > 
    > Esplora archivi supporta diverse opzioni di connessione. In questa sezione viene illustrato l'account di archiviazione tooa connessione associato alla sottoscrizione di Azure. toosee hello altre opzioni di connessione supportate da Esplora archivi, consultare l'articolo toohello [Introduzione a soluzioni di archiviazione](../vs-azure-tools-storage-manage-with-storage-explorer.md).
 
    1. Aprire Esplora archivi.
    
    1. In Esplora archivi, selezionare **Azure Account settings** (Impostazioni account Azure). 
    
        ![Azure Account settings][1]
    
    1. riquadro di sinistra Hello consente di visualizzare gli account Microsoft hello a che è effettuato l'accesso. tooconnect tooanother account, selezionare **aggiungere un account**e seguire hello toosign di finestre di dialogo con un account Microsoft associato ad almeno una sottoscrizione di Azure attiva.
    
        ![Aggiungi un account][2]
    
    1. Quando si accede correttamente con un account Microsoft, riquadro di sinistra hello popola con hello le sottoscrizioni di Azure associate all'account. Selezionare le sottoscrizioni di Azure a cui desidera toowork e quindi selezionare di hello **applica**. (Selezione **tutte le sottoscrizioni** hello di attiva o disattiva la selezione di tutti o nessuno dei hello elencate le sottoscrizioni di Azure.)
    
        ![Selezionare le sottoscrizioni di Azure][3]
    
    1. riquadro di sinistra Hello consente di visualizzare gli account di archiviazione hello associati alle sottoscrizioni Azure hello selezionato.
    
        ![Sottoscrizioni di Azure selezionate][4]

1. Individuare l'account di archiviazione dell'ambiente di test di hello:

    1. Nel riquadro sinistro di Esplora archivi hello, individuare ed espandere nodo hello per la sottoscrizione di Azure che possiede lab hello hello.
    
    1. Nel nodo della sottoscrizione hello, espandere **gli account di archiviazione**.

    1. Espandere i nodi del lab hello storage account nodo tooreveal per **contenitori Blob**, **condivisioni File**, **code**, e **tabelle**.
    
    1. Espandere hello **contenitori Blob** nodo.
    
    1. Selezionare il contenuto di hello caricamenti blob contenitore toodisplay nel riquadro di destra hello.
        
        ![Caricare una directory][5]

1. Caricare file VHD hello tramite Esplora archivi:

    1. Nel riquadro destro di Esplora archivi hello, vedrai un elenco di BLOB hello in hello **Carica** contenitore blob dell'account di archiviazione dell'ambiente di test di hello. Nella barra degli strumenti editor blob hello, selezionare **caricare** 
        
        ![Pulsante Carica][6]
    
    1. Da hello **caricare** menu a discesa, seleziona **caricare i file...** .
    
    1. In hello **caricare file** finestra di dialogo, i puntini di sospensione hello selezionare.
        
        ![Selezionare il file][8]  

    1. In hello **tooupload selezionare file** finestra di dialogo Sfoglia toohello desiderato di file VHD, selezionarlo e quindi selezionare **aprire**.
    
    1. Quando restituito toohello **caricare file** finestra di dialogo Modifica **Blob tipo** troppo**Blob di pagine**.
    
    1. Selezionare **Carica**.

        ![Selezionare il file][9]  
    
    1. Esplora archivi Hello **Log attività** riquadro viene visualizzato lo stato di download hello (insieme ai collegamenti toocancel hello caricamento). processo Hello di caricamento di un file VHD può essere lungo a seconda delle dimensioni di hello del file VHD hello e la velocità della connessione. 

        ![Stato upload-file][10]  

## <a name="next-steps"></a>Passaggi successivi

- [Creare un'immagine personalizzata in Azure DevTest Labs da un file VHD utilizzando hello portale di Azure](devtest-lab-create-template.md)
- [Creare un'immagine personalizzata in Azure DevTest Labs da un file VHD usando PowerShell](devtest-lab-create-custom-image-from-vhd-using-powershell.md)

[0]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-image-using-psh.png
[1]: ./media/devtest-lab-upload-vhd-using-storage-explorer/settings-icon.png
[2]: ./media/devtest-lab-upload-vhd-using-storage-explorer/add-account-link.png
[3]: ./media/devtest-lab-upload-vhd-using-storage-explorer/subscriptions-list.png
[4]: ./media/devtest-lab-upload-vhd-using-storage-explorer/storage-accounts-list.png
[5]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-dir.png
[6]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-button.png
[7]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-files.png
[8]: ./media/devtest-lab-upload-vhd-using-storage-explorer/select-file.png
[9]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-file.png
[10]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-status.png
