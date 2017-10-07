---
title: aaaCreate una funzione in attivata dall'archiviazione Blob di Azure | Documenti Microsoft
description: Utilizzare le funzioni di Azure toocreate una funzione senza che viene richiamata da elementi aggiunti tooAzure nell'archiviazione Blob.
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: d6bff41c-a624-40c1-bbc7-80590df29ded
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: acb7d29abb07a22da11d0e65d2ed54591f8e3f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-azure-blob-storage"></a>Creare una funzione attivata dall'archiviazione BLOB di Azure

Informazioni su come toocreate una funzione di attivazione eseguita quando i file vengono caricati tooor aggiornato nell'archiviazione Blob di Azure.

![Visualizza messaggio hello log.](./media/functions-create-storage-blob-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>Prerequisiti

+ Scaricare e installare hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).
+ Una sottoscrizione di Azure. Se non se ne ha una, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>Creare un'app per le funzioni di Azure

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![App per le funzioni creata correttamente.](./media/functions-create-first-azure-function/function-app-create-success.png)

Creare quindi una funzione in hello nuova funzione app.

<a name="create-function"></a>

## <a name="create-a-blob-storage-triggered-function"></a>Creare una funzione attivata dall'archiviazione BLOB

1. Espandere l'applicazione di funzione e fare clic su hello  **+**  accanto troppo**funzioni**. Se si tratta di hello prima funzione di app di funzione, selezionare **funzione personalizzata**. Consente di visualizzare il set completo di hello dei modelli di funzione.

    ![Pagina di avvio rapido di funzioni in hello portale di Azure](./media/functions-create-storage-blob-triggered-function/add-first-function.png)

2. Seleziona hello **BlobTrigger** modello per la lingua desiderata e utilizza le impostazioni di hello come specificato nella tabella hello.

    ![Creare una funzione di archiviazione generato hello Blob.](./media/functions-create-storage-blob-triggered-function/functions-create-blob-storage-trigger-portal.png)

    | Impostazione | Valore consigliato | Descrizione |
    |---|---|---|
    | **Percorso**   | mycontainer/{name}    | Percorso da monitorare nell'archiviazione BLOB. nome del file Hello del blob hello viene passato nell'associazione hello come hello _nome_ parametro.  |
    | **Connessione dell'account di archiviazione** | AzureWebJobStorage | È possibile utilizzare una connessione ad account di archiviazione hello già in uso dalla tua app di funzione o crearne uno nuovo.  |
    | **Dare un nome alla funzione** | Univoco nell'app per le funzioni | Nome della funzione attivata dal BLOB. |

3. Fare clic su **crea** toocreate la funzione.

Successivamente, connettersi tooyour account di archiviazione Azure e creare hello **mycontainer** contenitore.

## <a name="create-hello-container"></a>Creare il contenitore di hello

1. Nella funzione fare clic su **Integrazione**, espandere **Documentazione** e copiare sia **Nome account** sia **Chiave account**. Utilizzare questi account di archiviazione di credenziali tooconnect toohello. Se si è già connessi all'account di archiviazione, ignorare toostep 4.

    ![Ottenere l'account di archiviazione hello le credenziali di connessione.](./media/functions-create-storage-blob-triggered-function/functions-storage-account-connection.png)

1. Eseguire hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) strumento, fare clic su hello icona a sinistra di hello della connessione, scegliere **utilizzare un nome account di archiviazione e una chiave**, fare clic su **Avanti**.

    ![Eseguire lo strumento di esplorazione dell'archiviazione Account hello.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-1.png)

1. Immettere hello **nome Account** e **chiave dell'Account** nel passaggio 1, fare clic su **Avanti** e quindi **Connetti**. 

    ![Immettere le credenziali di archiviazione hello e connettersi.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-2.png)

1. Espandere l'account di archiviazione collegato hello destro del mouse su **contenitori Blob**, fare clic su **crea contenitore blob**, tipo `mycontainer`, quindi premere INVIO.

    ![Creare una coda di archiviazione.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-create-blob-container.png)

Dopo aver creato un contenitore blob, è possibile testare la funzione hello caricando un contenitore di toohello file.

## <a name="test-hello-function"></a>Funzione hello test

1. Nel portale di Azure hello, funzione tooyour Sfoglia espandere hello **registri** nella parte inferiore di hello della pagina hello e assicurarsi che il log di streaming non è in pausa.

1. In Esplora archivi espandere l'account di archiviazione, **Contenitori BLOB** e **mycontainer**. Fare clic su **Carica** e quindi su **Carica file...**.

    ![Caricare un contenitore di blob toohello file.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-upload-file-blob.png)

1. In hello **caricare file** finestra di dialogo fare clic su hello **file** campo. Sfoglia file tooa nel computer locale, ad esempio un file di immagine, selezionarlo e fare clic su **aprire** e quindi **caricare**.

1. Tornare indietro i log delle funzioni tooyour e verificare che BLOB hello è stato letto.

   ![Visualizza messaggio hello log.](./media/functions-create-storage-blob-triggered-function/functions-blob-storage-trigger-view-logs.png)

    >[!NOTE]
    > Quando l'app di funzione viene eseguita nel piano di utilizzo predefinito di hello, potrebbe esserci un ritardo di backup tooseveral minuti tra hello blob viene aggiunto o aggiornato e hello funzione venga attivata. Se nelle funzioni attivate dal BLOB è necessaria una bassa latenza, valutare l'opportunità di eseguire l'app per le funzioni in un piano di servizio app.

## <a name="clean-up-resources"></a>Pulire le risorse

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Passaggi successivi

È stata creata una funzione che viene eseguito quando un blob viene aggiunto tooor aggiornato nell'archiviazione Blob. 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Per altre informazioni sui trigger dell'archiviazione BLOB, vedere [Binding dell'archiviazione BLOB di Funzioni di Azure](functions-bindings-storage-blob.md).
