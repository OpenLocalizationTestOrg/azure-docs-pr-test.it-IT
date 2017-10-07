---
title: risorse di archiviazione Blob di Azure aaaManage con Esplora risorse di archiviazione (anteprima) | Documenti Microsoft
description: Gestire contenitori BLOB e BLOB di Azure con Storage Explorer (anteprima)
services: storage
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 2f09e545-ec94-4d89-b96c-14783cc9d7a9
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 503dd061b205875da127378ab48e8d465800fc09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-blob-storage-resources-with-storage-explorer-preview"></a>Gestire le risorse dell'archivio BLOB di Azure con Storage Explorer (anteprima)
## <a name="overview"></a>Panoramica
[Archiviazione Blob di Azure](storage/blobs/storage-dotnet-how-to-use-blobs.md) è un servizio per l'archiviazione di grandi quantità di dati non strutturati, ad esempio dati di testo o binario, che è possibile accedere da qualsiasi in HelloWorld tramite HTTP o HTTPS.
È possibile utilizzare dati tooexpose di archiviazione Blob pubblicamente toohello world o dati dell'applicazione toostore privatamente. In questo articolo si apprenderà come toouse Esplora archivi (Preview) toowork blob contenitori e BLOB.

## <a name="prerequisites"></a>Prerequisiti
passaggi di hello toocomplete in questo articolo, è necessario seguente hello:

* [Scaricare e installare Storage Explorer (anteprima)](http://www.storageexplorer.com)
* [Connettersi al servizio o account di archiviazione di Azure tooa](vs-azure-tools-storage-manage-with-storage-explorer.md#connect-to-a-storage-account-or-service)

## <a name="create-a-blob-container"></a>Creare un contenitore BLOB
Tutti i BLOB devono risiedere in un contenitore BLOB, che è semplicemente un raggruppamento logico di BLOB. Un account può contenere un numero illimitato di contenitori e ogni contenitore può archiviare un numero illimitato di BLOB.

Hello passaggi seguenti viene illustrato come toocreate un contenitore di blob all'interno di soluzioni di archiviazione (anteprima).

1. Aprire Storage Explorer (anteprima).
2. Nel riquadro di sinistra hello, espandere account di archiviazione hello entro il quale si desidera contenitore di blob toocreate hello.
3. Fare doppio clic su **contenitori Blob**e - scegliere dal menu di scelta rapida hello - **crea contenitore Blob**.

   ![Menu di scelta rapida Crea contenitore BLOB][0]
4. Verrà visualizzata una casella di testo di sotto di hello **contenitori Blob** cartella. Immettere il nome di hello per il contenitore del blob. Vedere hello [le regole di denominazione contenitore](storage/blobs/storage-dotnet-how-to-use-blobs.md#create-a-container) sezione per un elenco di regole e restrizioni relative alla denominazione contenitori blob.

   ![Casella di testo Crea contenitore BLOB][1]
5. Premere **invio** termine contenitore blob hello toocreate o **Esc** toocancel. Dopo aver creato correttamente il contenitore di blob hello, che verrà visualizzato in hello **contenitori Blob** cartella per hello selezionato di account di archiviazione.

   ![Contenitore BLOB creato][2]

## <a name="view-a-blob-containers-contents"></a>Visualizzare il contenuto di un contenitore BLOB
I contenitori BLOB includono BLOB e cartelle, che possono anche contenere BLOB.

Hello passaggi seguenti viene illustrato come contenuto di hello tooview di un contenitore di blob all'interno di soluzioni di archiviazione (anteprima):

1. Aprire Storage Explorer (anteprima).
2. Nel riquadro di sinistra hello, espandere il contenitore di blob hello desiderato tooview account di archiviazione di hello.
3. Espandere l'account di archiviazione hello **contenitori Blob**.
4. Contenitore di blob hello pulsante destro del mouse si desidera tooview e - scegliere dal menu di scelta rapida hello - **Apri Editor di contenitore Blob**.
   È anche possibile fare doppio clic sul contenitore blob hello desiderato tooview.

   ![Menu di scelta rapida Open Blob Container Editor (Apri editor contenitori BLOB)][19]
5. riquadro principale Hello verrà visualizzato il contenuto del contenitore blob hello.

   ![Editor contenitori BLOB][3]

## <a name="delete-a-blob-container"></a>Eliminare un contenitore BLOB
I contenitori di BLOB possono essere creati facilmente ed eliminati in base alle esigenze. (toosee come blob singolo toodelete, fare riferimento a sezione toohello [gestione dei BLOB in un contenitore blob](#managing-blobs-in-a-blob-container).)

Hello passaggi seguenti viene illustrato come toodelete un contenitore di blob all'interno di soluzioni di archiviazione (anteprima):

1. Aprire Storage Explorer (anteprima).
2. Nel riquadro di sinistra hello, espandere il contenitore di blob hello desiderato tooview account di archiviazione di hello.
3. Espandere l'account di archiviazione hello **contenitori Blob**.
4. Contenitore di blob hello pulsante destro del mouse si desidera toodelete e - scegliere dal menu di scelta rapida hello - **eliminare**.
   È anche possibile premere **eliminare** contenitore di toodelete hello blob attualmente selezionato.

   ![Menu di scelta rapida Elimina per il contenitore BLOB][4]
5. Selezionare **Sì** toohello nella finestra di conferma.

   ![Menu di scelta rapida dell'eliminazione per il contenitore BLOB][5]

## <a name="copy-a-blob-container"></a>Copiare un contenitore BLOB
Esplorazione dell'archiviazione (anteprima) permette di toocopy toohello Appunti contenitore blob e quindi incollare che blob contenitore in un altro account di archiviazione. (toosee come blob singolo toocopy, fare riferimento a sezione toohello [gestione dei BLOB in un contenitore blob](#managing-blobs-in-a-blob-container).)

Hello alla procedura seguente viene illustrato come un contenitore di blob da un archivio toocopy account tooanother.

1. Aprire Storage Explorer (anteprima).
2. Nel riquadro di sinistra hello, espandere il contenitore di blob hello desiderato toocopy account di archiviazione di hello.
3. Espandere l'account di archiviazione hello **contenitori Blob**.
4. Contenitore di blob hello pulsante destro del mouse si desidera toocopy e - scegliere dal menu di scelta rapida hello - **contenitore Blob di copia**.

   ![Menu di scelta Copy Blob Container (Copia contenitore BLOB)][6]
5. Fare doppio clic su account di archiviazione di destinazione"hello desiderato" in cui desidera toopaste hello blob contenitore e - dal menu di scelta rapida hello - selezionare **contenitore Blob Incolla**.

   ![Menu di scelta rapida Paste Blob Container (Incolla contenitore BLOB)][7]

## <a name="get-hello-sas-for-a-blob-container"></a>Ottenere hello firma di accesso condiviso per un contenitore blob
Oggetto [firma di accesso condiviso (SAS)](storage/common/storage-dotnet-shared-access-signature-part-1.md) fornisce l'accesso delegato tooresources nell'account di archiviazione.
Ciò significa che è possibile concedere a che un client limitate tooobjects autorizzazioni nell'account di archiviazione per un determinato periodo di tempo e con un set specificato di autorizzazioni, senza la necessità di condividere le chiavi di accesso di account.

Hello passaggi seguenti viene illustrato come toocreate una firma di accesso condiviso per un contenitore di blob:

1. Aprire Storage Explorer (anteprima).
2. Nel riquadro di sinistra hello, espandere account di archiviazione hello contenitore hello blob per i quali si desidera tooget una firma di accesso condiviso.
3. Espandere l'account di archiviazione hello **contenitori Blob**.
4. Contenitore blob desiderato hello e - scegliere dal menu di scelta rapida hello - **ottenere firma di accesso condiviso**.

   ![Menu di scelta rapida Get Shared Access Signature (Ottieni firma di accesso condiviso)][8]
5. In hello **firma di accesso condiviso** finestra di dialogo, specificare i criteri di hello, le date di inizio e di scadenza, fuso orario e desiderato per risorse hello livelli di accesso.

   ![Opzioni di Get Shared Access Signature (Ottieni firma di accesso condiviso)][9]
6. Al termine della specifica di opzioni di firma di accesso condiviso hello, selezionare **crea**.
7. Un secondo **firma di accesso condiviso** finestra di dialogo verrà quindi visualizzato elenchi hello contenitore blob insieme hello URL che è possibile utilizzare tooaccess QueryStrings hello risorsa di archiviazione.
   Selezionare **copia** Avanti URL toohello desiderato toocopy toohello Appunti.

   ![Copiare gli URL della firma di accesso condiviso][10]
8. Al termine, scegliere **Chiudi**.

## <a name="manage-access-policies-for-a-blob-container"></a>Gestire i criteri di accesso per un contenitore BLOB
Hello passaggi seguenti viene illustrato come toomanage (aggiungere e rimuovere) criteri di accesso per un contenitore blob:

1. Aprire Storage Explorer (anteprima).
2. Nel riquadro di sinistra hello, espandere account di archiviazione hello contenitore hello blob i cui criteri di accesso desiderato toomanage.
3. Espandere l'account di archiviazione hello **contenitori Blob**.
4. Selezionare il contenitore di blob desiderato hello e - dal menu di scelta rapida hello - **gestire criteri di accesso**.

   ![Menu di scelta rapida Manage Access Policies (Gestisci criteri di accesso)][11]
5. Hello **criteri di accesso** finestra di dialogo verrà elencati i criteri di accesso già creati per il contenitore di blob selezionati hello.

   ![Opzioni di Criteri di accesso][12]        
6. Seguire questi passaggi a seconda delle attività di gestione criteri di accesso hello:

   * **Aggiungere nuovi criteri di accesso**: selezionare **Aggiungi**. Una volta generate, hello **criteri di accesso** finestra di dialogo verrà visualizzato hello appena aggiunto accedere criteri (con le impostazioni predefinite).
   * **Modificare i criteri di accesso**: apportare le modifiche desiderate e scegliere **Salva**.
   * **Rimuovere un criterio di accesso** : selezionare questa opzione **rimuovere** desiderato tooremove un criterio di accesso toohello successivo.

## <a name="set-hello-public-access-level-for-a-blob-container"></a>Impostare hello a livello di accesso pubblico per un contenitore blob
Per impostazione predefinita, ogni contenitore di blob è troppo "Nessun accesso pubblico".

Hello passaggi seguenti viene illustrato come toospecify pubblica accedere a livello di un contenitore blob.

1. Aprire Storage Explorer (anteprima).
2. Nel riquadro di sinistra hello, espandere account di archiviazione hello contenitore hello blob i cui criteri di accesso desiderato toomanage.
3. Espandere l'account di archiviazione hello **contenitori Blob**.
4. Selezionare il contenitore di blob desiderato hello e - dal menu di scelta rapida hello - **impostare livello di accesso pubblico**.

   ![Menu di scelta rapida Set Public Access Level (Imposta livello di accesso pubblico)][13]
5. In hello **impostare livello di accesso pubblico contenitore** finestra di dialogo, specificare il livello di accesso di hello desiderato.

   ![Opzioni di Set Public Access Level (Imposta livello di accesso pubblico)][14]
6. Selezionare **Applica**.

## <a name="managing-blobs-in-a-blob-container"></a>Gestione dei BLOB in un contenitore BLOB
Dopo aver creato un contenitore blob, è possibile caricare un contenitore di blob toothat blob, scaricare un computer locale tooyour di blob, aprire un blob nel computer locale e molto altro ancora.

Hello alla procedura seguente viene illustrato come toomanage hello BLOB (e cartelle) all'interno di un contenitore blob.

1. Aprire Storage Explorer (anteprima).
2. Nel riquadro di sinistra hello, espandere il contenitore di blob hello desiderato toomanage account di archiviazione di hello.
3. Espandere l'account di archiviazione hello **contenitori Blob**.
4. Fare doppio clic sul contenitore di blob hello desiderato tooview.
5. riquadro principale Hello verrà visualizzato il contenuto del contenitore blob hello.

   ![Visualizzazione del contenitore BLOB][3]
6. riquadro principale Hello verrà visualizzato il contenuto del contenitore blob hello.
7. Seguire questi che passaggi a seconda attività hello desiderato tooperform:

   * **Caricare contenitore blob tooa di file**

     1. Sulla barra degli strumenti del riquadro principale hello, selezionare **caricare**e quindi **Carica file** dal menu a discesa hello.

        ![Menu Carica i file][15]
     2. In hello **caricare file** finestra di dialogo, i puntini di sospensione selezionare hello (**...** ) pulsante a destra hello hello **file** file hello tooselect desiderato tooupload casella di testo.

        ![Opzioni di Carica i file][16]
     3. Specificare il tipo di hello di **Blob tipo**. articolo Hello [Introduzione all'archiviazione Blob di Azure usando .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) vengono illustrate le differenze di hello tra hello vari tipi di blob.
     4. Facoltativamente, specificare una cartella di destinazione in cui verranno caricati i file selezionati hello. Se la cartella di destinazione hello non esiste, verrà creato.
     5. Selezionare **Carica**.
   * **Caricare un contenitore di blob tooa cartella**

     1. Sulla barra degli strumenti del riquadro principale hello, selezionare **caricare**e quindi **cartella caricare** dal menu a discesa hello.

        ![Menu di Upload Folder (Carica cartella)][17]
     2. In hello **cartella caricamento** finestra di dialogo, i puntini di sospensione selezionare hello (**...** ) pulsante a destra hello hello **cartella** cartella hello di tooselect casella testo cui si desidera tooupload il contenuto.

        ![Opzioni di Upload Folder (Carica cartella)][18]
     3. Specificare il tipo di hello di **Blob tipo**. articolo Hello [Introduzione all'archiviazione Blob di Azure usando .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) vengono illustrate le differenze di hello tra hello vari tipi di blob.
     4. Facoltativamente, specificare una cartella di destinazione in cui hello verrà caricato il contenuto della cartella selezionata. Se la cartella di destinazione hello non esiste, verrà creato.
     5. Selezionare **Carica**.
   * **Scaricare un computer locale tooyour di blob**

     1. Selezionare i blob hello desiderato toodownload.
     2. Sulla barra degli strumenti del riquadro principale hello, selezionare **scaricare**.
     3. In hello **specificare dove toosave hello scaricato blob** finestra di dialogo, specificare il percorso di hello in cui si desidera blob hello scaricato e hello nome desiderato toogive è.  
     4. Selezionare **Salva**.
   * **Aprire un BLOB nel computer locale**

     1. Selezionare i blob hello desiderato tooopen.
     2. Sulla barra degli strumenti del riquadro principale hello, selezionare **aprire**.
     3. blob Hello verrà scaricato e aperto con l'applicazione hello associata al tipo di file sottostante del blob hello.
   * **Copiare negli Appunti toohello un blob**

     1. Selezionare i blob hello desiderato toocopy.
     2. Sulla barra degli strumenti del riquadro principale hello, selezionare **copia**.
     3. Nel riquadro di sinistra hello, passare il contenitore di blob tooanother e fare doppio clic tooview nel riquadro principale hello.
     4. Sulla barra degli strumenti del riquadro principale hello, selezionare **Incolla** toocreate una copia di blob hello.
   * **Eliminare un BLOB**

     1. Selezionare i blob hello desiderato toodelete.
     2. Sulla barra degli strumenti del riquadro principale hello, selezionare **eliminare**.
     3. Selezionare **Sì** toohello nella finestra di conferma.

## <a name="next-steps"></a>Passaggi successivi
* Hello vista [note sulla versione di esplorazione dell'archiviazione (anteprima) e video più recenti](http://www.storageexplorer.com).
* Informazioni su come troppo[creare applicazioni usando BLOB di Azure, tabelle, code e i file](https://azure.microsoft.com/documentation/services/storage/).

[0]: ./media/vs-azure-tools-storage-explorer-blobs/blob-containers-create-context-menu.png
[1]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-create.png
[2]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-create-done.png
[3]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-editor.png
[4]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-context-menu.png
[5]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-confirmation.png
[6]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-copy-context-menu.png
[7]: ./media/vs-azure-tools-storage-explorer-blobs/blob-containers-paste-context-menu.png
[8]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-context-menu.png
[9]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-options.png
[10]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-urls.png
[11]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-context-menu.png
[12]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-options.png
[13]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-context-menu.png
[14]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-options.png
[15]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-menu.png
[16]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-options.png
[17]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-menu.png
[18]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-options.png
[19]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-open-editor-context-menu.png
