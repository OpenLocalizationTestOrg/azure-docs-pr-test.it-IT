---
title: aaaUsing Esplora archivi (Preview) con l'archiviazione di File di Azure | Documenti Microsoft
description: Informazioni su come illustrate le procedure toouse toowork di esplorazione dell'archiviazione (anteprima) con file le condivisioni file.
services: storage
documentationcenter: na
author: cawaMS
manager: paulyuk
editor: 
ms.assetid: 
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/09/2017
ms.author: cawa
ms.openlocfilehash: 98eb3cde711ae3dbfdb6ffaec23ae24f822370e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-storage-explorer-preview-with-azure-file-storage"></a>Uso di Storage Explorer (anteprima) con Archiviazione file di Azure

File di archiviazione è un servizio che offre i file nelle condivisioni di hello cloud usando Azure hello protocollo Server Message Block (SMB) standard. Sono supportati sia SMB 2.1 che SMB 3.0. Con l'archiviazione di File di Azure, è possibile eseguire la migrazione di applicazioni legacy che si basano su tooAzure condivisioni file rapidamente e senza costose. È possibile utilizzare File archiviazione tooexpose dati pubblicamente toohello world o dati dell'applicazione toostore privatamente. In questo articolo si apprenderà come toouse toowork di esplorazione dell'archiviazione (anteprima) con file di condivisioni e i file.

## <a name="prerequisites"></a>Prerequisiti

passaggi di hello toocomplete in questo articolo, è necessario seguente hello:

- [Scaricare e installare Storage Explorer (anteprima)](http://www.storageexplorer.com/)

- [Connettersi al servizio o account di archiviazione di Azure tooa](https://docs.microsoft.com//azure/vs-azure-tools-storage-manage-with-storage-explorer#connect-to-a-storage-account-or-service)

## <a name="create-a-file-share"></a>Creare una condivisione file

Tutti i file devono risiedere in una condivisione file, ovvero un semplice raggruppamento logico di file. Un account può contenere un numero illimitato di condivisioni file e ogni condivisione può archiviare un numero illimitato di file.

Hello alla procedura seguente viene illustrato come toocreate una condivisione di file all'interno di soluzioni di archiviazione (anteprima).

1. Aprire Storage Explorer (anteprima).

2. Nel riquadro di sinistra hello, espandere account di archiviazione hello entro il quale si desidera toocreate hello condivisione File

3. Fare doppio clic su **condivisioni File**e - scegliere dal menu di scelta rapida hello - **Crea condivisione File**.

    ![Crea condivisione file](media/vs-azure-tools-storage-explorer-files/image1.png)

4. Verrà visualizzata una casella di testo di sotto di hello **condivisioni File** cartella. Immettere il nome di hello per la condivisione di file. Vedere hello [condividere le regole di denominazione](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container) sezione per un elenco di regole e restrizioni relative alla denominazione condivisioni file.

    ![Denominazione condivisione hello](media/vs-azure-tools-storage-explorer-files/image2.png)

5. Premere **invio** quando toocreate done hello condivisione file, o **Esc** toocancel. Una volta condivisione file hello è stata creata correttamente, verrà visualizzato in hello **condivisioni File** cartella per hello selezionato di account di archiviazione.

    ![nuova condivisione di Hello](media/vs-azure-tools-storage-explorer-files/image3.png)

## <a name="view-a-file-shares-contents"></a>Visualizzare il contenuto di una condivisione file

Le condivisioni file contengono file e cartelle, che a loro volta possono contenere file.

Hello passaggi seguenti viene illustrato come contenuto di hello tooview di un file condivide all'interno di soluzioni di archiviazione (anteprima): +

1. Aprire Storage Explorer (anteprima).

2. Nel riquadro di sinistra hello, espandere account di archiviazione di hello contenente desiderato tooview condivisione di file hello.

3. Espandere l'account di archiviazione hello **condivisioni File**.

4. Condivisione di file hello pulsante destro del mouse si desidera tooview, quindi - scegliere dal menu di scelta rapida hello - **aprire**. È anche possibile fare doppio clic su condivisione file hello desiderato tooview.

    ![Apri condivisione](media/vs-azure-tools-storage-explorer-files/image4.png)

5. riquadro principale Hello verrà visualizzato il contenuto della condivisione di file hello.
    
    ![contenuto della condivisione di Hello](media/vs-azure-tools-storage-explorer-files/image5.png)

## <a name="delete-a-file-share"></a>Eliminare una condivisione file

È possibile creare ed eliminare facilmente le condivisioni file in base alle esigenze. (toosee come toodelete singoli file, fare riferimento a sezione toohello [la gestione dei file in una condivisione file](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)

Hello alla procedura seguente viene illustrato come toodelete una condivisione di file all'interno di soluzioni di archiviazione (anteprima):

1. Aprire Storage Explorer (anteprima).

2. Nel riquadro di sinistra hello, espandere account di archiviazione di hello contenente desiderato tooview condivisione di file hello.

3. Espandere l'account di archiviazione hello **condivisioni File**.

4. Condivisione di file hello pulsante destro del mouse si desidera toodelete, quindi - scegliere dal menu di scelta rapida hello - **eliminare**. È anche possibile premere **eliminare** toodelete hello attualmente selezionato in una condivisione.

    ![Elimina](media/vs-azure-tools-storage-explorer-files/image6.png)

5. Selezionare **Sì** toohello nella finestra di conferma.
    
    ![Finestra di dialogo di conferma](media/vs-azure-tools-storage-explorer-files/image7.png)

## <a name="copy-a-file-share"></a>Copiare una condivisione file

Esplorazione dell'archiviazione (anteprima) permette toocopy Appunti toohello condivisione file e quindi incollare tale condivisione di file in un altro account di archiviazione. (toosee come toocopy singoli file, fare riferimento a sezione toohello [la gestione dei file in una condivisione file](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)

Hello alla procedura seguente viene illustrato come un file toocopy condividere da uno tooanother di account di archiviazione.

1. Aprire Storage Explorer (anteprima).

2. Nel riquadro di sinistra hello, espandere account di archiviazione di hello contenente desiderato toocopy condivisione di file hello.

3. Espandere l'account di archiviazione hello **condivisioni File**.

4. Condivisione di file hello pulsante destro del mouse si desidera toocopy, quindi - scegliere dal menu di scelta rapida hello - **condivisione File di copia**.

    ![Copia condivisione file](media/vs-azure-tools-storage-explorer-files/image8.png)

5. Fare doppio clic su account di archiviazione di destinazione"hello desiderato" in cui desidera toopaste condivisione di file hello e - dal menu di scelta rapida hello - selezionare **Incolla condivisione File**.

    ![Incolla condivisione file](media/vs-azure-tools-storage-explorer-files/image9.png)

## <a name="get-hello-sas-for-a-file-share"></a>Ottenere hello firma di accesso condiviso per una condivisione file

Oggetto [firma di accesso condiviso (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) fornisce l'accesso delegato tooresources nell'account di archiviazione. Ciò significa che è possibile concedere a che un client limitate tooobjects autorizzazioni nell'account di archiviazione per un determinato periodo di tempo e con un set specificato di autorizzazioni, senza dovere tooshare le chiavi di accesso di account.

Hello passaggi seguenti viene illustrato come toocreate una firma di accesso condiviso per un file di condividere: +

1. Aprire Storage Explorer (anteprima).

2. Nel riquadro di sinistra hello, espandere account di archiviazione hello contenente hello condivisione di file per i quali si desidera tooget una firma di accesso condiviso.

3. Espandere l'account di archiviazione hello **condivisioni File**.

4. Condivisione di file desiderato hello e - scegliere dal menu di scelta rapida hello - **ottenere firma di accesso condiviso**.

    ![Ottenere la firma di accesso condiviso](media/vs-azure-tools-storage-explorer-files/image10.png)

5. In hello **firma di accesso condiviso** finestra di dialogo, specificare i criteri di hello, le date di inizio e di scadenza, fuso orario e desiderato per risorse hello livelli di accesso.

    ![Finestra di dialogo Firma di accesso condiviso](media/vs-azure-tools-storage-explorer-files/image11.png)

6. Al termine della specifica di opzioni di firma di accesso condiviso hello, selezionare **crea**.

7. Un secondo **firma di accesso condiviso** finestra di dialogo verrà quindi visualizzato che elenchi hello condivisione file e URL hello e che è possibile utilizzare tooaccess QueryStrings hello risorsa di archiviazione. Selezionare **copia** Avanti URL toohello desiderato toocopy toohello Appunti.
    
    ![Seconda finestra di dialogo Firma di accesso condiviso](media/vs-azure-tools-storage-explorer-files/image12.png)

8. Al termine, scegliere **Chiudi**.

## <a name="manage-access-policies-for-a-file-share"></a>Gestire i criteri di accesso per una condivisione file

Hello passaggi seguenti viene illustrato come toomanage (aggiungere e rimuovere) criteri di accesso per una condivisione file: +. i criteri di accesso Hello viene utilizzato per la creazione di URL di firma di accesso condiviso tramite la quale gli utenti possono utilizzare tooaccess hello risorsa di archiviazione File durante un periodo di tempo definito.

1. Aprire Storage Explorer (anteprima).

2. Nel riquadro di sinistra hello, espandere account di archiviazione hello contenente hello condivisione di file i cui criteri di accesso desiderato toomanage.

3. Espandere l'account di archiviazione hello **condivisioni File**.

4. Selezionare condivisione di file desiderato hello e - dal menu di scelta rapida hello - **gestire criteri di accesso**.

    ![Menu di scelta rapida Manage Access Policies (Gestisci criteri di accesso)](media/vs-azure-tools-storage-explorer-files/image13.png)

5. Hello **criteri di accesso** finestra di dialogo verrà elencati i criteri di accesso già creati per la condivisione di file selezionato hello.
    
    ![Criteri di accesso](media/vs-azure-tools-storage-explorer-files/image14.png)

6. Seguire questi passaggi a seconda delle attività di gestione criteri di accesso hello:
    
    - **Aggiungere nuovi criteri di accesso**: selezionare **Aggiungi**. Una volta generate, hello **criteri di accesso** finestra di dialogo verrà visualizzato hello appena aggiunto accedere criteri (con le impostazioni predefinite).

    - **Modificare i criteri di accesso**: apportare le modifiche desiderate e scegliere **Salva**.

    - **Rimuovere un criterio di accesso** : selezionare questa opzione **rimuovere** desiderato tooremove un criterio di accesso toohello successivo.

7. Creare un nuovo URL di firma di accesso condiviso con criteri di accesso creato in precedenza hello:
    
    ![Ottenere una firma di accesso condiviso](media/vs-azure-tools-storage-explorer-files/image15.png)
    
    ![Nome e proprietà della firma di accesso condiviso](media/vs-azure-tools-storage-explorer-files/image16.png)

## <a name="managing-files-in-a-file-share"></a>Gestione dei file in una condivisione file

Dopo aver creato una condivisione file, è possibile caricare una condivisione di file toothat file, scaricare un computer locale tooyour di file, aprire un file nel computer locale e molto altro ancora.

Hello passaggi seguenti viene illustrato come condividono toomanage hello file (e cartelle) all'interno di un file.

1.  Aprire Storage Explorer (anteprima).

2.  Nel riquadro di sinistra hello, espandere account di archiviazione di hello contenente desiderato toomanage condivisione di file hello.

3.  Espandere l'account di archiviazione hello **condivisioni File**.

4.  Fare doppio clic su condivisione file hello desiderato tooview.

5.  riquadro principale Hello verrà visualizzato il contenuto della condivisione di file hello.

    ![contenuto della condivisione di Hello](media/vs-azure-tools-storage-explorer-files/image17.png)

6.  riquadro principale Hello verrà visualizzato il contenuto della condivisione di file hello.

7.  Seguire questi che passaggi a seconda attività hello desiderato tooperform:

    - **Caricare una condivisione di file tooa**

        a.  Sulla barra degli strumenti del riquadro principale hello, selezionare **caricare**e quindi **Carica file** dal menu a discesa hello.

        ![Caricare file](media/vs-azure-tools-storage-explorer-files/image18.png)
        
        b. In hello **caricare file** finestra di dialogo, i puntini di sospensione selezionare hello (**...** ) pulsante a destra hello hello **file** file hello tooselect desiderato tooupload casella di testo.

        ![Aggiunta di file](media/vs-azure-tools-storage-explorer-files/image19.png)

        c. Selezionare **Carica**.

    - **Caricare una condivisione di file di cartella tooa**
        
        a. Sulla barra degli strumenti del riquadro principale hello, selezionare **caricare**e quindi **cartella caricare** dal menu a discesa hello.

        ![Menu di Upload Folder (Carica cartella)](media/vs-azure-tools-storage-explorer-files/image20.png)

        b. In hello **cartella caricamento** finestra di dialogo, i puntini di sospensione selezionare hello (**...** ) pulsante a destra hello hello **cartella** cartella hello di tooselect casella testo cui si desidera tooupload il contenuto.

        c. Facoltativamente, specificare una cartella di destinazione in cui hello verrà caricato il contenuto della cartella selezionata. Se la cartella di destinazione hello non esiste, verrà creato.

        d. Selezionare **Carica**.

    - **Scaricare un computer locale tooyour di file**
        
        a. Selezionare il file hello desiderato toodownload.
        
        b. Sulla barra degli strumenti del riquadro principale hello, selezionare **scaricare**.
        
        c. In hello **specificare dove toosave hello scaricati file** finestra di dialogo, specificare il percorso di hello in cui si desidera file hello scaricato e hello nome desiderato toogive è.

        d. Selezionare **Salva**.

    - **Aprire un file nel computer locale**
        
        a.  Selezionare il file hello desiderato tooopen.
        
        b.  Sulla barra degli strumenti del riquadro principale hello, selezionare **aprire**.
        
        c.  file Hello verrà scaricato e aperto con l'applicazione hello associata al tipo sottostante del file hello.

    - **Copiare negli Appunti toohello un file**

        a. Selezionare il file hello desiderato toocopy.

        b. Sulla barra degli strumenti del riquadro principale hello, selezionare **copia**.

        c. Nel riquadro di sinistra hello, passare tooanother condivisione di file e fare doppio clic tooview nel riquadro principale hello.

        d. Sulla barra degli strumenti del riquadro principale hello, selezionare **Incolla** toocreate una copia del file hello.

    - **Eliminare un file**

        a. Selezionare il file hello desiderato toodelete.

        b. Sulla barra degli strumenti del riquadro principale hello, selezionare **eliminare**.

        c. Selezionare **Sì** toohello nella finestra di conferma.

## <a name="next-steps"></a>Passaggi successivi

- Hello vista [note sulla versione di esplorazione dell'archiviazione (anteprima) e video più recenti](http://www.storageexplorer.com/).

- Informazioni su come troppo[creare applicazioni usando BLOB di Azure, tabelle, code e i file](https://azure.microsoft.com/documentation/services/storage/).
