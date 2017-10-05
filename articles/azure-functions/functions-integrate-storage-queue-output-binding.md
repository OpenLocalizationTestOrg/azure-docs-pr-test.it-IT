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
# <a name="add-messages-to-an-azure-storage-queue-using-functions"></a><span data-ttu-id="32c7a-103">Aggiungere messaggi a una coda di archiviazione di Azure tramite Funzioni</span><span class="sxs-lookup"><span data-stu-id="32c7a-103">Add messages to an Azure Storage queue using Functions</span></span>

<span data-ttu-id="32c7a-104">In Funzioni di Azure, i binding di input e di output forniscono una modalità dichiarativa per connettersi a dati di servizio esterni dalla funzione.</span><span class="sxs-lookup"><span data-stu-id="32c7a-104">In Azure Functions, input and output bindings provide a declarative way to connect to external service data from your function.</span></span> <span data-ttu-id="32c7a-105">Questo argomento illustra come aggiornare una funzione esistente mediante l'aggiunta di un binding di output che invia messaggi all'archiviazione code di Azure.</span><span class="sxs-lookup"><span data-stu-id="32c7a-105">In this topic, learn how to update an existing function by adding an output binding that sends messages to Azure Queue storage.</span></span>  

![Visualizzare il messaggio nei log.](./media/functions-integrate-storage-queue-output-binding/functions-integrate-storage-binding-in-portal.png)

## <a name="prerequisites"></a><span data-ttu-id="32c7a-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="32c7a-107">Prerequisites</span></span> 

[!INCLUDE [Previous topics](../../includes/functions-quickstart-previous-topics.md)]

* <span data-ttu-id="32c7a-108">Installare [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="32c7a-108">Install the [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <span data-ttu-id="32c7a-109"><a name="add-binding"></a>Aggiungere un binding di output</span><span class="sxs-lookup"><span data-stu-id="32c7a-109"><a name="add-binding"></a>Add an output binding</span></span>
 
1. <span data-ttu-id="32c7a-110">Espandere sia l'app per le funzioni sia la funzione.</span><span class="sxs-lookup"><span data-stu-id="32c7a-110">Expand both your function app and your function.</span></span>

2. <span data-ttu-id="32c7a-111">Selezionare **Integrazione**, **+ Nuovo output** e quindi scegliere **Archiviazione code di Azure** e **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="32c7a-111">Select **Integrate** and **+ New output**, then choose **Azure Queue storage** and choose **Select**.</span></span>
    
    ![Aggiungere un binding di output di Archiviazione code a una funzione nel portale di Azure.](./media/functions-integrate-storage-queue-output-binding/function-add-queue-storage-output-binding.png)

3. <span data-ttu-id="32c7a-113">Usare le impostazioni specificate nella tabella:</span><span class="sxs-lookup"><span data-stu-id="32c7a-113">Use the settings as specified in the table:</span></span> 

    ![Aggiungere un binding di output di Archiviazione code a una funzione nel portale di Azure.](./media/functions-integrate-storage-queue-output-binding/function-add-queue-storage-output-binding-2.png)

    | <span data-ttu-id="32c7a-115">Impostazione</span><span class="sxs-lookup"><span data-stu-id="32c7a-115">Setting</span></span>      |  <span data-ttu-id="32c7a-116">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="32c7a-116">Suggested value</span></span>   | <span data-ttu-id="32c7a-117">Descrizione</span><span class="sxs-lookup"><span data-stu-id="32c7a-117">Description</span></span>                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | <span data-ttu-id="32c7a-118">**Nome coda**</span><span class="sxs-lookup"><span data-stu-id="32c7a-118">**Queue name**</span></span>   | <span data-ttu-id="32c7a-119">myqueue-items</span><span class="sxs-lookup"><span data-stu-id="32c7a-119">myqueue-items</span></span>    | <span data-ttu-id="32c7a-120">Nome della coda a cui connettersi nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="32c7a-120">The name of the queue to connect to in your Storage account.</span></span> |
    | <span data-ttu-id="32c7a-121">**Connessione dell'account di archiviazione**</span><span class="sxs-lookup"><span data-stu-id="32c7a-121">**Storage account connection**</span></span> | <span data-ttu-id="32c7a-122">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="32c7a-122">AzureWebJobStorage</span></span> | <span data-ttu-id="32c7a-123">È possibile usare la connessione dell'account di archiviazione già usata dall'app per le funzioni oppure crearne una nuova.</span><span class="sxs-lookup"><span data-stu-id="32c7a-123">You can use the storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="32c7a-124">**Nome del parametro del messaggio**</span><span class="sxs-lookup"><span data-stu-id="32c7a-124">**Message parameter name**</span></span> | <span data-ttu-id="32c7a-125">outputQueueItem</span><span class="sxs-lookup"><span data-stu-id="32c7a-125">outputQueueItem</span></span> | <span data-ttu-id="32c7a-126">Nome del parametro di binding di output.</span><span class="sxs-lookup"><span data-stu-id="32c7a-126">The name of the output binding parameter.</span></span> | 

4. <span data-ttu-id="32c7a-127">Fare clic su **Salva** per aggiungere il binding.</span><span class="sxs-lookup"><span data-stu-id="32c7a-127">Click **Save** to add the binding.</span></span>
 
<span data-ttu-id="32c7a-128">Dopo aver definito un binding di output, è necessario ora aggiornare il codice in modo da usare il binding per aggiungere messaggi a una coda.</span><span class="sxs-lookup"><span data-stu-id="32c7a-128">Now that you have an output binding defined, you need to update the code to use the binding to add messages to a queue.</span></span>  

## <a name="update-the-function-code"></a><span data-ttu-id="32c7a-129">Aggiornare il codice funzione</span><span class="sxs-lookup"><span data-stu-id="32c7a-129">Update the function code</span></span>

1. <span data-ttu-id="32c7a-130">Selezionare la funzione per visualizzare il codice funzione nell'editor.</span><span class="sxs-lookup"><span data-stu-id="32c7a-130">Select your function to display the function code in the editor.</span></span> 

2. <span data-ttu-id="32c7a-131">Per una funzione C#, aggiornare la definizione di funzione come illustrato di seguito per aggiungere il parametro di binding di archiviazione **outputQueueItem**.</span><span class="sxs-lookup"><span data-stu-id="32c7a-131">For a C# function, update your function definition as follows to add the **outputQueueItem** storage binding parameter.</span></span> <span data-ttu-id="32c7a-132">Ignorare questo passaggio per le funzioni JavaScript.</span><span class="sxs-lookup"><span data-stu-id="32c7a-132">Skip this step for a JavaScript function.</span></span>

    ```cs   
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, 
        ICollector<string> outputQueueItem, TraceWriter log)
    {
        ....
    }
    ```

3. <span data-ttu-id="32c7a-133">Aggiungere il codice seguente alla funzione poco prima che venga restituito il metodo.</span><span class="sxs-lookup"><span data-stu-id="32c7a-133">Add the following code to the function just before the method returns.</span></span> <span data-ttu-id="32c7a-134">Usare il frammento appropriato per il linguaggio della funzione.</span><span class="sxs-lookup"><span data-stu-id="32c7a-134">Use the appropriate snippet for the language of your function.</span></span>

    ```javascript
    context.bindings.outputQueueItem = "Name passed to the function: " + 
                (req.query.name || req.body.name);
    ```

    ```cs
    outputQueueItem.Add("Name passed to the function: " + name);     
    ```

4. <span data-ttu-id="32c7a-135">Selezionare **Salva** per salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="32c7a-135">Select **Save** to save changes.</span></span>

<span data-ttu-id="32c7a-136">Il valore passato al trigger HTTP è incluso in un messaggio aggiunto alla coda.</span><span class="sxs-lookup"><span data-stu-id="32c7a-136">The value passed to the HTTP trigger is included in a message added to the queue.</span></span>
 
## <a name="test-the-function"></a><span data-ttu-id="32c7a-137">Testare la funzione</span><span class="sxs-lookup"><span data-stu-id="32c7a-137">Test the function</span></span> 

1. <span data-ttu-id="32c7a-138">Dopo aver salvato le modifiche al codice, selezionare **Esegui**.</span><span class="sxs-lookup"><span data-stu-id="32c7a-138">After the code changes are saved, select **Run**.</span></span> 

    ![Aggiungere un binding di output di Archiviazione code a una funzione nel portale di Azure.](./media/functions-integrate-storage-queue-output-binding/functions-test-run-function.png)

2. <span data-ttu-id="32c7a-140">Controllare i log per assicurarsi che la funzione abbia avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="32c7a-140">Check the logs to make sure that the function succeeded.</span></span> <span data-ttu-id="32c7a-141">Quando il binding di output viene usato per la prima volta, nell'account di archiviazione viene creata dal runtime Funzioni una nuova coda denominata **outqueue**.</span><span class="sxs-lookup"><span data-stu-id="32c7a-141">A new queue named **outqueue** is created in your Storage account by the Functions runtime when the output binding is first used.</span></span>

<span data-ttu-id="32c7a-142">È possibile quindi connettersi all'account di archiviazione per verificare la nuova coda e il messaggio aggiunto.</span><span class="sxs-lookup"><span data-stu-id="32c7a-142">Next, you can connect to your storage account to verify the new queue and the message you added to it.</span></span> 

## <a name="connect-to-the-queue"></a><span data-ttu-id="32c7a-143">Connettersi alla coda</span><span class="sxs-lookup"><span data-stu-id="32c7a-143">Connect to the queue</span></span>

<span data-ttu-id="32c7a-144">Ignorare i primi tre passaggi se Esplora archivi è già stato installato e connesso all'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="32c7a-144">Skip the first three steps if you have already installed Storage Explorer and connected it to your storage account.</span></span>    

1. <span data-ttu-id="32c7a-145">Nella funzione scegliere **Integrazione** e il nuovo binding di output **Archiviazione code di Azure** e quindi espandere **Documentazione**.</span><span class="sxs-lookup"><span data-stu-id="32c7a-145">In your function, choose **Integrate** and the new **Azure Queue storage** output binding, then expand **Documentation**.</span></span> <span data-ttu-id="32c7a-146">Copiare sia **Nome account** sia **Chiave account**.</span><span class="sxs-lookup"><span data-stu-id="32c7a-146">Copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="32c7a-147">Usare queste credenziali per connettersi all'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="32c7a-147">You use these credentials to connect to the storage account.</span></span>
 
    ![Ottenere le credenziali per la connessione all'account di archiviazione.](./media/functions-integrate-storage-queue-output-binding/function-get-storage-account-credentials.png)

2. <span data-ttu-id="32c7a-149">Eseguire lo strumento [Microsoft Azure Storage Explorer](http://storageexplorer.com/), selezionare l'icona di connessione a sinistra, scegliere **Use a storage account name and key** (Usare il nome e la chiave di un account di archiviazione) e selezionare **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="32c7a-149">Run the [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, select the connect icon on the left, choose **Use a storage account name and key**, and select **Next**.</span></span>

    ![Eseguire lo strumento di esplorazione dell'account di archiviazione.](./media/functions-integrate-storage-queue-output-binding/functions-storage-manager-connect-1.png)
    
3. <span data-ttu-id="32c7a-151">Incollare il **Nome account** e la **Chiave dell'account** dal Passaggio 1 nei rispettivi campi corrispondenti, quindi selezionare **Avanti** e infine **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="32c7a-151">Paste the **Account name** and **Account key** from step 1 into their corresponding fields, then select **Next**, and **Connect**.</span></span> 
  
    ![Incollare le credenziali di archiviazione ed eseguire la connessione.](./media/functions-integrate-storage-queue-output-binding/functions-storage-manager-connect-2.png)

4. <span data-ttu-id="32c7a-153">Espandere l'account di archiviazione associato e **Code** e quindi verificare che esista una coda denominata **myqueue-items**.</span><span class="sxs-lookup"><span data-stu-id="32c7a-153">Expand the attached storage account, expand **Queues** and verify that a queue named **myqueue-items** exists.</span></span> <span data-ttu-id="32c7a-154">Dovrebbe anche essere presente un messaggio nella coda.</span><span class="sxs-lookup"><span data-stu-id="32c7a-154">You should also see a message already in the queue.</span></span>  
 
    ![Creare una coda di archiviazione.](./media/functions-integrate-storage-queue-output-binding/function-queue-storage-output-view-queue.png)
 

## <a name="clean-up-resources"></a><span data-ttu-id="32c7a-156">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="32c7a-156">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="32c7a-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="32c7a-157">Next steps</span></span>

<span data-ttu-id="32c7a-158">È stato aggiunto un binding di output a una funzione esistente.</span><span class="sxs-lookup"><span data-stu-id="32c7a-158">You have added an output binding to an existing function.</span></span> 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="32c7a-159">Per altre informazioni sul binding all'archiviazione code, vedere [Associazioni della coda dell'archiviazione di Funzioni di Azure](functions-bindings-storage-queue.md).</span><span class="sxs-lookup"><span data-stu-id="32c7a-159">For more information about binding to Queue storage, see [Azure Functions Storage queue bindings](functions-bindings-storage-queue.md).</span></span> 



