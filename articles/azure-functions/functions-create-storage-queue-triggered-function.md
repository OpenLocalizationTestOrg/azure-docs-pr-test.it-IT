---
title: una funzione in Azure attivato da messaggi in coda aaaCreate | Documenti Microsoft
description: Utilizzare le funzioni di Azure toocreate una funzione senza che viene richiamata da un messaggio inviato tooan coda di archiviazione di Azure.
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 361da2a4-15d1-4903-bdc4-cc4b27fc3ff4
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: e9501ed336b502eaeee3fa62ec4ae085c76de0ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-azure-queue-storage"></a>Creare una funzione attivata dall'archiviazione code di Azure

Informazioni su come toocreate una funzione di attivazione eseguita quando i messaggi vengono inviati tooan coda di archiviazione di Azure.

![Visualizza messaggio hello log.](./media/functions-create-storage-queue-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>Prerequisiti

- Scaricare e installare hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).

- Una sottoscrizione di Azure. Se non se ne ha una, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>Creare un'app per le funzioni di Azure

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![App per le funzioni creata correttamente.](./media/functions-create-first-azure-function/function-app-create-success.png)

Creare quindi una funzione in hello nuova funzione app.

<a name="create-function"></a>

## <a name="create-a-queue-triggered-function"></a>Creare una funzione attivata da una coda

1. Espandere l'applicazione di funzione e fare clic su hello  **+**  accanto troppo**funzioni**. Se si tratta di hello prima funzione di app di funzione, selezionare **funzione personalizzata**. Consente di visualizzare il set completo di hello dei modelli di funzione.

    ![Pagina di avvio rapido di funzioni in hello portale di Azure](./media/functions-create-storage-queue-triggered-function/add-first-function.png)

2. Seleziona hello **QueueTrigger** modello per la lingua desiderata e utilizza le impostazioni di hello come specificato nella tabella hello.

    ![Creare una funzione hello archiviazione coda attivata.](./media/functions-create-storage-queue-triggered-function/functions-create-queue-storage-trigger-portal.png)
    
    | Impostazione | Valore consigliato | Descrizione |
    |---|---|---|
    | **Nome coda**   | myqueue-items    | Nome di hello coda tooconnect tooin account di archiviazione. |
    | **Connessione dell'account di archiviazione** | AzureWebJobStorage | È possibile utilizzare una connessione ad account di archiviazione hello già in uso dalla tua app di funzione o crearne uno nuovo.  |
    | **Dare un nome alla funzione** | Univoco nell'app per le funzioni | Nome della funzione attivata dalla coda. |

3. Fare clic su **crea** toocreate la funzione.

Successivamente, connettersi tooyour account di archiviazione Azure e creare hello **myqueue elementi** coda di archiviazione.

## <a name="create-hello-queue"></a>Creare la coda hello

1. Nella funzione fare clic su **Integrazione**, espandere **Documentazione** e copiare sia **Nome account** sia **Chiave account**. Utilizzare questi account di archiviazione di credenziali tooconnect toohello. Se si è già connessi all'account di archiviazione, ignorare toostep 4.

    ![Ottenere l'account di archiviazione hello le credenziali di connessione.](./media/functions-create-storage-queue-triggered-function/functions-storage-account-connection.png)v

1. Eseguire hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) strumento, fare clic su hello icona a sinistra di hello della connessione, scegliere **utilizzare un nome account di archiviazione e una chiave**, fare clic su **Avanti**.

    ![Eseguire lo strumento di esplorazione dell'archiviazione Account hello.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-1.png)

1. Immettere hello **nome Account** e **chiave dell'Account** nel passaggio 1, fare clic su **Avanti** e quindi **Connetti**.

    ![Immettere le credenziali di archiviazione hello e connettersi.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-2.png)

1. Espandere l'account di archiviazione collegato hello destro del mouse su **code**, fare clic su **Create queue**, tipo `myqueue-items`, e quindi premere INVIO.

    ![Creare una coda di archiviazione.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-create-queue.png)

Dopo aver creato una coda di archiviazione, è possibile testare la funzione hello mediante l'aggiunta di una coda di messaggi toohello.

## <a name="test-hello-function"></a>Funzione hello test

1. Nel portale di Azure hello, funzione tooyour Sfoglia espandere hello **registri** nella parte inferiore di hello della pagina hello e assicurarsi che il log di streaming non è in pausa.

1. In Esplora archivi espandere l'account di archiviazione, **Code** e **myqueue-items** e quindi fare clic su **Aggiungi messaggio**.

    ![Aggiungere una coda di messaggi toohello.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-add-message.png)

1. Digitare il proprio messaggio di benvenuto nel campo **Testo del messaggio** e fare clic su **OK**.

1. Attendere alcuni secondi, quindi tornare tooyour i log delle funzioni e verificare che il nuovo messaggio hello letto dalla coda hello.

    ![Visualizza messaggio hello log.](./media/functions-create-storage-queue-triggered-function/functions-queue-storage-trigger-view-logs.png)

1. In Esplora archivi, fare clic su **aggiornamento** e verificare il messaggio hello è stato elaborato e non è più in coda hello.

## <a name="clean-up-resources"></a>Pulire le risorse

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Passaggi successivi

È stata creata una funzione che viene eseguito quando un messaggio viene aggiunto tooa coda di archiviazione.

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Per altre informazioni sui trigger dell'archiviazione code, vedere [Associazioni della coda dell'archiviazione di Funzioni di Azure](functions-bindings-storage-queue.md).