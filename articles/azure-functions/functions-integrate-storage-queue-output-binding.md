---
title: una funzione in Azure attivato da messaggi in coda aaaCreate | Documenti Microsoft
description: Utilizzare le funzioni di Azure toocreate una funzione senza che viene richiamata da un messaggio inviato tooan coda di archiviazione di Azure.
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 0b609bc0-c264-4092-8e3e-0784dcc23b5d
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/17/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 44db90fa80bf77e31bf53dddabd7136de5800b11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-messages-tooan-azure-storage-queue-using-functions"></a>Aggiungere una coda di archiviazione di Azure tooan messaggi utilizzando le funzioni

Nelle funzioni di Azure, le associazioni di input e outpue forniscono dati di servizio tooexternal tooconnect una modalità dichiarativa dalla funzione. In questo argomento, informazioni su come tooupdate una funzione esistente aggiungendo un output di associazione che invia messaggi tooAzure l'archiviazione delle code.  

![Visualizza messaggio hello log.](./media/functions-integrate-storage-queue-output-binding/functions-integrate-storage-binding-in-portal.png)

## <a name="prerequisites"></a>Prerequisiti 

[!INCLUDE [Previous topics](../../includes/functions-quickstart-previous-topics.md)]

* Installare hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).

## <a name="add-binding"></a>Aggiungere un binding di output
 
1. Espandere sia l'app per le funzioni sia la funzione.

2. Selezionare **Integrazione**, **+ Nuovo output** e quindi scegliere **Archiviazione code di Azure** e **Seleziona**.
    
    ![Aggiungere una funzione di coda archiviazione output associazione tooa in hello portale di Azure.](./media/functions-integrate-storage-queue-output-binding/function-add-queue-storage-output-binding.png)

3. Utilizza le impostazioni di hello come specificato nella tabella hello: 

    ![Aggiungere una funzione di coda archiviazione output associazione tooa in hello portale di Azure.](./media/functions-integrate-storage-queue-output-binding/function-add-queue-storage-output-binding-2.png)

    | Impostazione      |  Valore consigliato   | Descrizione                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | **Nome coda**   | myqueue-items    | nome Hello di hello coda tooconnect tooin account di archiviazione. |
    | **Connessione dell'account di archiviazione** | AzureWebJobStorage | È possibile utilizzare una connessione ad account di archiviazione hello già in uso dalla tua app di funzione o crearne uno nuovo.  |
    | **Nome del parametro del messaggio** | outputQueueItem | nome Hello del parametro di associazione di output di hello. | 

4. Fare clic su **salvare** associazione hello tooadd.
 
Dopo aver creato un'associazione di output definita, è necessario tooupdate hello codice toouse hello associazione tooadd tooa coda dei messaggi.  

## <a name="update-hello-function-code"></a>Aggiornare il codice di funzione hello

1. Selezionare il codice della funzione hello toodisplay funzione nell'editor di hello. 

2. Per una funzione c#, aggiornare la definizione di funzione come segue hello tooadd **outputQueueItem** parametro di associazione di archiviazione. Ignorare questo passaggio per le funzioni JavaScript.

    ```cs   
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, 
        ICollector<string> outputQueueItem, TraceWriter log)
    {
        ....
    }
    ```

3. Aggiungere hello dopo la funzione di toohello codice appena prima di avviare hello metodo restituisce. Utilizzare frammento appropriato hello per lingua hello della funzione.

    ```javascript
    context.bindings.outputQueueItem = "Name passed toohello function: " + 
                (req.query.name || req.body.name);
    ```

    ```cs
    outputQueueItem.Add("Name passed toohello function: " + name);     
    ```

4. Selezionare **salvare** toosave modifiche.

il valore di Hello passato trigger HTTP toohello è incluso in una coda toohello aggiunto.
 
## <a name="test-hello-function"></a>Funzione hello test 

1. Dopo aver salvati le modifiche al codice hello, selezionare **eseguire**. 

    ![Aggiungere una funzione di coda archiviazione output associazione tooa in hello portale di Azure.](./media/functions-integrate-storage-queue-output-binding/functions-test-run-function.png)

2. Controllare toomake registri hello assicurarsi che la funzione hello ha avuto esito positivo. Una nuova coda denominata **outqueue** creati hello funzioni runtime quando l'associazione di output di hello viene innanzitutto utilizzata nell'account di archiviazione.

Successivamente, è possibile connettersi tooyour storage account tooverify hello nuova coda, il messaggio hello che tooit è stato aggiunto. 

## <a name="connect-toohello-queue"></a>Connettersi toohello coda

Ignora hello i primi tre passaggi se si dispone già installato soluzioni di archiviazione e averlo connesso tooyour account di archiviazione.    

1. Nella funzione, scegliere **integrazione** e hello nuovo **l'archiviazione delle code di Azure** associazione di output, quindi espandere **documentazione**. Copiare sia **Nome account** sia **Chiave account**. Utilizzare questi account di archiviazione di credenziali tooconnect toohello.
 
    ![Ottenere l'account di archiviazione hello le credenziali di connessione.](./media/functions-integrate-storage-queue-output-binding/function-get-storage-account-credentials.png)

2. Eseguire hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) strumento, seleziona hello icona a sinistra di hello della connessione, scegliere **utilizzare un nome account di archiviazione e una chiave**e selezionare **Avanti**.

    ![Eseguire lo strumento di esplorazione dell'archiviazione Account hello.](./media/functions-integrate-storage-queue-output-binding/functions-storage-manager-connect-1.png)
    
3. Hello Incolla **nome Account** e **chiave dell'Account** ottenuto al passaggio 1 in campi corrispondenti, quindi selezionare **Avanti**, e **Connetti**. 
  
    ![Incollare le credenziali di archiviazione hello e connettersi.](./media/functions-integrate-storage-queue-output-binding/functions-storage-manager-connect-2.png)

4. Espandere il nodo di account di archiviazione collegato hello, **code** e verificare che una coda denominata **myqueue elementi** esiste. Inoltre, si verrà visualizzato un messaggio già in coda hello.  
 
    ![Creare una coda di archiviazione.](./media/functions-integrate-storage-queue-output-binding/function-queue-storage-output-view-queue.png)
 

## <a name="clean-up-resources"></a>Pulire le risorse

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Passaggi successivi

È stata aggiunta una funzione di output associazione tooan esistente. 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Per ulteriori informazioni sull'associazione tooQueue archiviazione, vedere [associazioni di coda di archiviazione di Azure funzioni](functions-bindings-storage-queue.md). 



