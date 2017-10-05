---
title: Creare una funzione in Azure attivata da messaggi di coda | Microsoft Docs
description: Usare Funzioni di Azure per creare una funzione senza server che viene richiamata da un messaggio inviato a una coda di archiviazione di Azure.
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
ms.openlocfilehash: 57c59273a9da55f3e357764c522b444ae2d73cb5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="add-messages-to-an-azure-storage-queue-using-functions"></a>Aggiungere messaggi a una coda di archiviazione di Azure tramite Funzioni

In Funzioni di Azure, i binding di input e di output forniscono una modalità dichiarativa per connettersi a dati di servizio esterni dalla funzione. Questo argomento illustra come aggiornare una funzione esistente mediante l'aggiunta di un binding di output che invia messaggi all'archiviazione code di Azure.  

![Visualizzare il messaggio nei log.](./media/functions-integrate-storage-queue-output-binding/functions-integrate-storage-binding-in-portal.png)

## <a name="prerequisites"></a>Prerequisiti 

[!INCLUDE [Previous topics](../../includes/functions-quickstart-previous-topics.md)]

* Installare [Microsoft Azure Storage Explorer](http://storageexplorer.com/).

## <a name="add-binding"></a>Aggiungere un binding di output
 
1. Espandere sia l'app per le funzioni sia la funzione.

2. Selezionare **Integrazione**, **+ Nuovo output** e quindi scegliere **Archiviazione code di Azure** e **Seleziona**.
    
    ![Aggiungere un binding di output di Archiviazione code a una funzione nel portale di Azure.](./media/functions-integrate-storage-queue-output-binding/function-add-queue-storage-output-binding.png)

3. Usare le impostazioni specificate nella tabella: 

    ![Aggiungere un binding di output di Archiviazione code a una funzione nel portale di Azure.](./media/functions-integrate-storage-queue-output-binding/function-add-queue-storage-output-binding-2.png)

    | Impostazione      |  Valore consigliato   | Descrizione                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | **Nome coda**   | myqueue-items    | Nome della coda a cui connettersi nell'account di archiviazione. |
    | **Connessione dell'account di archiviazione** | AzureWebJobStorage | È possibile usare la connessione dell'account di archiviazione già usata dall'app per le funzioni oppure crearne una nuova.  |
    | **Nome del parametro del messaggio** | outputQueueItem | Nome del parametro di binding di output. | 

4. Fare clic su **Salva** per aggiungere il binding.
 
Dopo aver definito un binding di output, è necessario ora aggiornare il codice in modo da usare il binding per aggiungere messaggi a una coda.  

## <a name="update-the-function-code"></a>Aggiornare il codice funzione

1. Selezionare la funzione per visualizzare il codice funzione nell'editor. 

2. Per una funzione C#, aggiornare la definizione di funzione come illustrato di seguito per aggiungere il parametro di binding di archiviazione **outputQueueItem**. Ignorare questo passaggio per le funzioni JavaScript.

    ```cs   
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, 
        ICollector<string> outputQueueItem, TraceWriter log)
    {
        ....
    }
    ```

3. Aggiungere il codice seguente alla funzione poco prima che venga restituito il metodo. Usare il frammento appropriato per il linguaggio della funzione.

    ```javascript
    context.bindings.outputQueueItem = "Name passed to the function: " + 
                (req.query.name || req.body.name);
    ```

    ```cs
    outputQueueItem.Add("Name passed to the function: " + name);     
    ```

4. Selezionare **Salva** per salvare le modifiche.

Il valore passato al trigger HTTP è incluso in un messaggio aggiunto alla coda.
 
## <a name="test-the-function"></a>Testare la funzione 

1. Dopo aver salvato le modifiche al codice, selezionare **Esegui**. 

    ![Aggiungere un binding di output di Archiviazione code a una funzione nel portale di Azure.](./media/functions-integrate-storage-queue-output-binding/functions-test-run-function.png)

2. Controllare i log per assicurarsi che la funzione abbia avuto esito positivo. Quando il binding di output viene usato per la prima volta, nell'account di archiviazione viene creata dal runtime Funzioni una nuova coda denominata **outqueue**.

È possibile quindi connettersi all'account di archiviazione per verificare la nuova coda e il messaggio aggiunto. 

## <a name="connect-to-the-queue"></a>Connettersi alla coda

Ignorare i primi tre passaggi se Esplora archivi è già stato installato e connesso all'account di archiviazione.    

1. Nella funzione scegliere **Integrazione** e il nuovo binding di output **Archiviazione code di Azure** e quindi espandere **Documentazione**. Copiare sia **Nome account** sia **Chiave account**. Usare queste credenziali per connettersi all'account di archiviazione.
 
    ![Ottenere le credenziali per la connessione all'account di archiviazione.](./media/functions-integrate-storage-queue-output-binding/function-get-storage-account-credentials.png)

2. Eseguire lo strumento [Microsoft Azure Storage Explorer](http://storageexplorer.com/), selezionare l'icona di connessione a sinistra, scegliere **Use a storage account name and key** (Usare il nome e la chiave di un account di archiviazione) e selezionare **Avanti**.

    ![Eseguire lo strumento di esplorazione dell'account di archiviazione.](./media/functions-integrate-storage-queue-output-binding/functions-storage-manager-connect-1.png)
    
3. Incollare il **Nome account** e la **Chiave dell'account** dal Passaggio 1 nei rispettivi campi corrispondenti, quindi selezionare **Avanti** e infine **Connetti**. 
  
    ![Incollare le credenziali di archiviazione ed eseguire la connessione.](./media/functions-integrate-storage-queue-output-binding/functions-storage-manager-connect-2.png)

4. Espandere l'account di archiviazione associato e **Code** e quindi verificare che esista una coda denominata **myqueue-items**. Dovrebbe anche essere presente un messaggio nella coda.  
 
    ![Creare una coda di archiviazione.](./media/functions-integrate-storage-queue-output-binding/function-queue-storage-output-view-queue.png)
 

## <a name="clean-up-resources"></a>Pulire le risorse

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Passaggi successivi

È stato aggiunto un binding di output a una funzione esistente. 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Per altre informazioni sul binding all'archiviazione code, vedere [Associazioni della coda dell'archiviazione di Funzioni di Azure](functions-bindings-storage-queue.md). 



