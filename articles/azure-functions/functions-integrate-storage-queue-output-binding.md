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
# <a name="add-messages-tooan-azure-storage-queue-using-functions"></a><span data-ttu-id="14dff-103">Aggiungere una coda di archiviazione di Azure tooan messaggi utilizzando le funzioni</span><span class="sxs-lookup"><span data-stu-id="14dff-103">Add messages tooan Azure Storage queue using Functions</span></span>

<span data-ttu-id="14dff-104">Nelle funzioni di Azure, le associazioni di input e outpue forniscono dati di servizio tooexternal tooconnect una modalità dichiarativa dalla funzione.</span><span class="sxs-lookup"><span data-stu-id="14dff-104">In Azure Functions, input and output bindings provide a declarative way tooconnect tooexternal service data from your function.</span></span> <span data-ttu-id="14dff-105">In questo argomento, informazioni su come tooupdate una funzione esistente aggiungendo un output di associazione che invia messaggi tooAzure l'archiviazione delle code.</span><span class="sxs-lookup"><span data-stu-id="14dff-105">In this topic, learn how tooupdate an existing function by adding an output binding that sends messages tooAzure Queue storage.</span></span>  

![Visualizza messaggio hello log.](./media/functions-integrate-storage-queue-output-binding/functions-integrate-storage-binding-in-portal.png)

## <a name="prerequisites"></a><span data-ttu-id="14dff-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="14dff-107">Prerequisites</span></span> 

[!INCLUDE [Previous topics](../../includes/functions-quickstart-previous-topics.md)]

* <span data-ttu-id="14dff-108">Installare hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="14dff-108">Install hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <span data-ttu-id="14dff-109"><a name="add-binding"></a>Aggiungere un binding di output</span><span class="sxs-lookup"><span data-stu-id="14dff-109"><a name="add-binding"></a>Add an output binding</span></span>
 
1. <span data-ttu-id="14dff-110">Espandere sia l'app per le funzioni sia la funzione.</span><span class="sxs-lookup"><span data-stu-id="14dff-110">Expand both your function app and your function.</span></span>

2. <span data-ttu-id="14dff-111">Selezionare **Integrazione**, **+ Nuovo output** e quindi scegliere **Archiviazione code di Azure** e **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="14dff-111">Select **Integrate** and **+ New output**, then choose **Azure Queue storage** and choose **Select**.</span></span>
    
    ![Aggiungere una funzione di coda archiviazione output associazione tooa in hello portale di Azure.](./media/functions-integrate-storage-queue-output-binding/function-add-queue-storage-output-binding.png)

3. <span data-ttu-id="14dff-113">Utilizza le impostazioni di hello come specificato nella tabella hello:</span><span class="sxs-lookup"><span data-stu-id="14dff-113">Use hello settings as specified in hello table:</span></span> 

    ![Aggiungere una funzione di coda archiviazione output associazione tooa in hello portale di Azure.](./media/functions-integrate-storage-queue-output-binding/function-add-queue-storage-output-binding-2.png)

    | <span data-ttu-id="14dff-115">Impostazione</span><span class="sxs-lookup"><span data-stu-id="14dff-115">Setting</span></span>      |  <span data-ttu-id="14dff-116">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="14dff-116">Suggested value</span></span>   | <span data-ttu-id="14dff-117">Descrizione</span><span class="sxs-lookup"><span data-stu-id="14dff-117">Description</span></span>                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | <span data-ttu-id="14dff-118">**Nome coda**</span><span class="sxs-lookup"><span data-stu-id="14dff-118">**Queue name**</span></span>   | <span data-ttu-id="14dff-119">myqueue-items</span><span class="sxs-lookup"><span data-stu-id="14dff-119">myqueue-items</span></span>    | <span data-ttu-id="14dff-120">nome Hello di hello coda tooconnect tooin account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="14dff-120">hello name of hello queue tooconnect tooin your Storage account.</span></span> |
    | <span data-ttu-id="14dff-121">**Connessione dell'account di archiviazione**</span><span class="sxs-lookup"><span data-stu-id="14dff-121">**Storage account connection**</span></span> | <span data-ttu-id="14dff-122">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="14dff-122">AzureWebJobStorage</span></span> | <span data-ttu-id="14dff-123">È possibile utilizzare una connessione ad account di archiviazione hello già in uso dalla tua app di funzione o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="14dff-123">You can use hello storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="14dff-124">**Nome del parametro del messaggio**</span><span class="sxs-lookup"><span data-stu-id="14dff-124">**Message parameter name**</span></span> | <span data-ttu-id="14dff-125">outputQueueItem</span><span class="sxs-lookup"><span data-stu-id="14dff-125">outputQueueItem</span></span> | <span data-ttu-id="14dff-126">nome Hello del parametro di associazione di output di hello.</span><span class="sxs-lookup"><span data-stu-id="14dff-126">hello name of hello output binding parameter.</span></span> | 

4. <span data-ttu-id="14dff-127">Fare clic su **salvare** associazione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="14dff-127">Click **Save** tooadd hello binding.</span></span>
 
<span data-ttu-id="14dff-128">Dopo aver creato un'associazione di output definita, è necessario tooupdate hello codice toouse hello associazione tooadd tooa coda dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="14dff-128">Now that you have an output binding defined, you need tooupdate hello code toouse hello binding tooadd messages tooa queue.</span></span>  

## <a name="update-hello-function-code"></a><span data-ttu-id="14dff-129">Aggiornare il codice di funzione hello</span><span class="sxs-lookup"><span data-stu-id="14dff-129">Update hello function code</span></span>

1. <span data-ttu-id="14dff-130">Selezionare il codice della funzione hello toodisplay funzione nell'editor di hello.</span><span class="sxs-lookup"><span data-stu-id="14dff-130">Select your function toodisplay hello function code in hello editor.</span></span> 

2. <span data-ttu-id="14dff-131">Per una funzione c#, aggiornare la definizione di funzione come segue hello tooadd **outputQueueItem** parametro di associazione di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="14dff-131">For a C# function, update your function definition as follows tooadd hello **outputQueueItem** storage binding parameter.</span></span> <span data-ttu-id="14dff-132">Ignorare questo passaggio per le funzioni JavaScript.</span><span class="sxs-lookup"><span data-stu-id="14dff-132">Skip this step for a JavaScript function.</span></span>

    ```cs   
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, 
        ICollector<string> outputQueueItem, TraceWriter log)
    {
        ....
    }
    ```

3. <span data-ttu-id="14dff-133">Aggiungere hello dopo la funzione di toohello codice appena prima di avviare hello metodo restituisce.</span><span class="sxs-lookup"><span data-stu-id="14dff-133">Add hello following code toohello function just before hello method returns.</span></span> <span data-ttu-id="14dff-134">Utilizzare frammento appropriato hello per lingua hello della funzione.</span><span class="sxs-lookup"><span data-stu-id="14dff-134">Use hello appropriate snippet for hello language of your function.</span></span>

    ```javascript
    context.bindings.outputQueueItem = "Name passed toohello function: " + 
                (req.query.name || req.body.name);
    ```

    ```cs
    outputQueueItem.Add("Name passed toohello function: " + name);     
    ```

4. <span data-ttu-id="14dff-135">Selezionare **salvare** toosave modifiche.</span><span class="sxs-lookup"><span data-stu-id="14dff-135">Select **Save** toosave changes.</span></span>

<span data-ttu-id="14dff-136">il valore di Hello passato trigger HTTP toohello è incluso in una coda toohello aggiunto.</span><span class="sxs-lookup"><span data-stu-id="14dff-136">hello value passed toohello HTTP trigger is included in a message added toohello queue.</span></span>
 
## <a name="test-hello-function"></a><span data-ttu-id="14dff-137">Funzione hello test</span><span class="sxs-lookup"><span data-stu-id="14dff-137">Test hello function</span></span> 

1. <span data-ttu-id="14dff-138">Dopo aver salvati le modifiche al codice hello, selezionare **eseguire**.</span><span class="sxs-lookup"><span data-stu-id="14dff-138">After hello code changes are saved, select **Run**.</span></span> 

    ![Aggiungere una funzione di coda archiviazione output associazione tooa in hello portale di Azure.](./media/functions-integrate-storage-queue-output-binding/functions-test-run-function.png)

2. <span data-ttu-id="14dff-140">Controllare toomake registri hello assicurarsi che la funzione hello ha avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="14dff-140">Check hello logs toomake sure that hello function succeeded.</span></span> <span data-ttu-id="14dff-141">Una nuova coda denominata **outqueue** creati hello funzioni runtime quando l'associazione di output di hello viene innanzitutto utilizzata nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="14dff-141">A new queue named **outqueue** is created in your Storage account by hello Functions runtime when hello output binding is first used.</span></span>

<span data-ttu-id="14dff-142">Successivamente, è possibile connettersi tooyour storage account tooverify hello nuova coda, il messaggio hello che tooit è stato aggiunto.</span><span class="sxs-lookup"><span data-stu-id="14dff-142">Next, you can connect tooyour storage account tooverify hello new queue and hello message you added tooit.</span></span> 

## <a name="connect-toohello-queue"></a><span data-ttu-id="14dff-143">Connettersi toohello coda</span><span class="sxs-lookup"><span data-stu-id="14dff-143">Connect toohello queue</span></span>

<span data-ttu-id="14dff-144">Ignora hello i primi tre passaggi se si dispone già installato soluzioni di archiviazione e averlo connesso tooyour account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="14dff-144">Skip hello first three steps if you have already installed Storage Explorer and connected it tooyour storage account.</span></span>    

1. <span data-ttu-id="14dff-145">Nella funzione, scegliere **integrazione** e hello nuovo **l'archiviazione delle code di Azure** associazione di output, quindi espandere **documentazione**.</span><span class="sxs-lookup"><span data-stu-id="14dff-145">In your function, choose **Integrate** and hello new **Azure Queue storage** output binding, then expand **Documentation**.</span></span> <span data-ttu-id="14dff-146">Copiare sia **Nome account** sia **Chiave account**.</span><span class="sxs-lookup"><span data-stu-id="14dff-146">Copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="14dff-147">Utilizzare questi account di archiviazione di credenziali tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="14dff-147">You use these credentials tooconnect toohello storage account.</span></span>
 
    ![Ottenere l'account di archiviazione hello le credenziali di connessione.](./media/functions-integrate-storage-queue-output-binding/function-get-storage-account-credentials.png)

2. <span data-ttu-id="14dff-149">Eseguire hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) strumento, seleziona hello icona a sinistra di hello della connessione, scegliere **utilizzare un nome account di archiviazione e una chiave**e selezionare **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="14dff-149">Run hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, select hello connect icon on hello left, choose **Use a storage account name and key**, and select **Next**.</span></span>

    ![Eseguire lo strumento di esplorazione dell'archiviazione Account hello.](./media/functions-integrate-storage-queue-output-binding/functions-storage-manager-connect-1.png)
    
3. <span data-ttu-id="14dff-151">Hello Incolla **nome Account** e **chiave dell'Account** ottenuto al passaggio 1 in campi corrispondenti, quindi selezionare **Avanti**, e **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="14dff-151">Paste hello **Account name** and **Account key** from step 1 into their corresponding fields, then select **Next**, and **Connect**.</span></span> 
  
    ![Incollare le credenziali di archiviazione hello e connettersi.](./media/functions-integrate-storage-queue-output-binding/functions-storage-manager-connect-2.png)

4. <span data-ttu-id="14dff-153">Espandere il nodo di account di archiviazione collegato hello, **code** e verificare che una coda denominata **myqueue elementi** esiste.</span><span class="sxs-lookup"><span data-stu-id="14dff-153">Expand hello attached storage account, expand **Queues** and verify that a queue named **myqueue-items** exists.</span></span> <span data-ttu-id="14dff-154">Inoltre, si verrà visualizzato un messaggio già in coda hello.</span><span class="sxs-lookup"><span data-stu-id="14dff-154">You should also see a message already in hello queue.</span></span>  
 
    ![Creare una coda di archiviazione.](./media/functions-integrate-storage-queue-output-binding/function-queue-storage-output-view-queue.png)
 

## <a name="clean-up-resources"></a><span data-ttu-id="14dff-156">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="14dff-156">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="14dff-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="14dff-157">Next steps</span></span>

<span data-ttu-id="14dff-158">È stata aggiunta una funzione di output associazione tooan esistente.</span><span class="sxs-lookup"><span data-stu-id="14dff-158">You have added an output binding tooan existing function.</span></span> 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="14dff-159">Per ulteriori informazioni sull'associazione tooQueue archiviazione, vedere [associazioni di coda di archiviazione di Azure funzioni](functions-bindings-storage-queue.md).</span><span class="sxs-lookup"><span data-stu-id="14dff-159">For more information about binding tooQueue storage, see [Azure Functions Storage queue bindings](functions-bindings-storage-queue.md).</span></span> 



