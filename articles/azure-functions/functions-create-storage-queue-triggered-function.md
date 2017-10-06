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
# <a name="create-a-function-triggered-by-azure-queue-storage"></a><span data-ttu-id="eed2c-103">Creare una funzione attivata dall'archiviazione code di Azure</span><span class="sxs-lookup"><span data-stu-id="eed2c-103">Create a function triggered by Azure Queue storage</span></span>

<span data-ttu-id="eed2c-104">Informazioni su come toocreate una funzione di attivazione eseguita quando i messaggi vengono inviati tooan coda di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="eed2c-104">Learn how toocreate a function triggered when messages are submitted tooan Azure Storage queue.</span></span>

![Visualizza messaggio hello log.](./media/functions-create-storage-queue-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="eed2c-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="eed2c-106">Prerequisites</span></span>

- <span data-ttu-id="eed2c-107">Scaricare e installare hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="eed2c-107">Download and install hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

- <span data-ttu-id="eed2c-108">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="eed2c-108">An Azure subscription.</span></span> <span data-ttu-id="eed2c-109">Se non se ne ha una, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="eed2c-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="eed2c-110">Creare un'app per le funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="eed2c-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![App per le funzioni creata correttamente.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="eed2c-112">Creare quindi una funzione in hello nuova funzione app.</span><span class="sxs-lookup"><span data-stu-id="eed2c-112">Next, you create a function in hello new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-queue-triggered-function"></a><span data-ttu-id="eed2c-113">Creare una funzione attivata da una coda</span><span class="sxs-lookup"><span data-stu-id="eed2c-113">Create a Queue triggered function</span></span>

1. <span data-ttu-id="eed2c-114">Espandere l'applicazione di funzione e fare clic su hello  **+**  accanto troppo**funzioni**.</span><span class="sxs-lookup"><span data-stu-id="eed2c-114">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="eed2c-115">Se si tratta di hello prima funzione di app di funzione, selezionare **funzione personalizzata**.</span><span class="sxs-lookup"><span data-stu-id="eed2c-115">If this is hello first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="eed2c-116">Consente di visualizzare il set completo di hello dei modelli di funzione.</span><span class="sxs-lookup"><span data-stu-id="eed2c-116">This displays hello complete set of function templates.</span></span>

    ![Pagina di avvio rapido di funzioni in hello portale di Azure](./media/functions-create-storage-queue-triggered-function/add-first-function.png)

2. <span data-ttu-id="eed2c-118">Seleziona hello **QueueTrigger** modello per la lingua desiderata e utilizza le impostazioni di hello come specificato nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="eed2c-118">Select hello **QueueTrigger** template for your desired language, and  use hello settings as specified in hello table.</span></span>

    ![Creare una funzione hello archiviazione coda attivata.](./media/functions-create-storage-queue-triggered-function/functions-create-queue-storage-trigger-portal.png)
    
    | <span data-ttu-id="eed2c-120">Impostazione</span><span class="sxs-lookup"><span data-stu-id="eed2c-120">Setting</span></span> | <span data-ttu-id="eed2c-121">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="eed2c-121">Suggested value</span></span> | <span data-ttu-id="eed2c-122">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eed2c-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="eed2c-123">**Nome coda**</span><span class="sxs-lookup"><span data-stu-id="eed2c-123">**Queue name**</span></span>   | <span data-ttu-id="eed2c-124">myqueue-items</span><span class="sxs-lookup"><span data-stu-id="eed2c-124">myqueue-items</span></span>    | <span data-ttu-id="eed2c-125">Nome di hello coda tooconnect tooin account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="eed2c-125">Name of hello queue tooconnect tooin your Storage account.</span></span> |
    | <span data-ttu-id="eed2c-126">**Connessione dell'account di archiviazione**</span><span class="sxs-lookup"><span data-stu-id="eed2c-126">**Storage account connection**</span></span> | <span data-ttu-id="eed2c-127">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="eed2c-127">AzureWebJobStorage</span></span> | <span data-ttu-id="eed2c-128">È possibile utilizzare una connessione ad account di archiviazione hello già in uso dalla tua app di funzione o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="eed2c-128">You can use hello storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="eed2c-129">**Dare un nome alla funzione**</span><span class="sxs-lookup"><span data-stu-id="eed2c-129">**Name your function**</span></span> | <span data-ttu-id="eed2c-130">Univoco nell'app per le funzioni</span><span class="sxs-lookup"><span data-stu-id="eed2c-130">Unique in your function app</span></span> | <span data-ttu-id="eed2c-131">Nome della funzione attivata dalla coda.</span><span class="sxs-lookup"><span data-stu-id="eed2c-131">Name of this queue triggered function.</span></span> |

3. <span data-ttu-id="eed2c-132">Fare clic su **crea** toocreate la funzione.</span><span class="sxs-lookup"><span data-stu-id="eed2c-132">Click **Create** toocreate your function.</span></span>

<span data-ttu-id="eed2c-133">Successivamente, connettersi tooyour account di archiviazione Azure e creare hello **myqueue elementi** coda di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="eed2c-133">Next, you connect tooyour Azure Storage account and create hello **myqueue-items** storage queue.</span></span>

## <a name="create-hello-queue"></a><span data-ttu-id="eed2c-134">Creare la coda hello</span><span class="sxs-lookup"><span data-stu-id="eed2c-134">Create hello queue</span></span>

1. <span data-ttu-id="eed2c-135">Nella funzione fare clic su **Integrazione**, espandere **Documentazione** e copiare sia **Nome account** sia **Chiave account**.</span><span class="sxs-lookup"><span data-stu-id="eed2c-135">In your function, click **Integrate**, expand **Documentation**, and copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="eed2c-136">Utilizzare questi account di archiviazione di credenziali tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="eed2c-136">You use these credentials tooconnect toohello storage account.</span></span> <span data-ttu-id="eed2c-137">Se si è già connessi all'account di archiviazione, ignorare toostep 4.</span><span class="sxs-lookup"><span data-stu-id="eed2c-137">If you have already connected your storage account, skip toostep 4.</span></span>

    ![Ottenere l'account di archiviazione hello le credenziali di connessione.](./media/functions-create-storage-queue-triggered-function/functions-storage-account-connection.png)<span data-ttu-id="eed2c-139">v</span><span class="sxs-lookup"><span data-stu-id="eed2c-139">v</span></span>

1. <span data-ttu-id="eed2c-140">Eseguire hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) strumento, fare clic su hello icona a sinistra di hello della connessione, scegliere **utilizzare un nome account di archiviazione e una chiave**, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="eed2c-140">Run hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, click hello connect icon on hello left, choose **Use a storage account name and key**, and click **Next**.</span></span>

    ![Eseguire lo strumento di esplorazione dell'archiviazione Account hello.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-1.png)

1. <span data-ttu-id="eed2c-142">Immettere hello **nome Account** e **chiave dell'Account** nel passaggio 1, fare clic su **Avanti** e quindi **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="eed2c-142">Enter hello **Account name** and **Account key** from step 1, click **Next** and then **Connect**.</span></span>

    ![Immettere le credenziali di archiviazione hello e connettersi.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-2.png)

1. <span data-ttu-id="eed2c-144">Espandere l'account di archiviazione collegato hello destro del mouse su **code**, fare clic su **Create queue**, tipo `myqueue-items`, e quindi premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="eed2c-144">Expand hello attached storage account, right-click **Queues**, click **Create queue**, type `myqueue-items`, and then press enter.</span></span>

    ![Creare una coda di archiviazione.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-create-queue.png)

<span data-ttu-id="eed2c-146">Dopo aver creato una coda di archiviazione, è possibile testare la funzione hello mediante l'aggiunta di una coda di messaggi toohello.</span><span class="sxs-lookup"><span data-stu-id="eed2c-146">Now that you have a storage queue, you can test hello function by adding a message toohello queue.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="eed2c-147">Funzione hello test</span><span class="sxs-lookup"><span data-stu-id="eed2c-147">Test hello function</span></span>

1. <span data-ttu-id="eed2c-148">Nel portale di Azure hello, funzione tooyour Sfoglia espandere hello **registri** nella parte inferiore di hello della pagina hello e assicurarsi che il log di streaming non è in pausa.</span><span class="sxs-lookup"><span data-stu-id="eed2c-148">Back in hello Azure portal, browse tooyour function expand hello **Logs** at hello bottom of hello page and make sure that log streaming isn't paused.</span></span>

1. <span data-ttu-id="eed2c-149">In Esplora archivi espandere l'account di archiviazione, **Code** e **myqueue-items** e quindi fare clic su **Aggiungi messaggio**.</span><span class="sxs-lookup"><span data-stu-id="eed2c-149">In Storage Explorer, expand your storage account, **Queues**, and **myqueue-items**, then click **Add message**.</span></span>

    ![Aggiungere una coda di messaggi toohello.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-add-message.png)

1. <span data-ttu-id="eed2c-151">Digitare il proprio messaggio di benvenuto</span><span class="sxs-lookup"><span data-stu-id="eed2c-151">Type your "Hello World!"</span></span> <span data-ttu-id="eed2c-152">nel campo **Testo del messaggio** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="eed2c-152">message in **Message text** and click **OK**.</span></span>

1. <span data-ttu-id="eed2c-153">Attendere alcuni secondi, quindi tornare tooyour i log delle funzioni e verificare che il nuovo messaggio hello letto dalla coda hello.</span><span class="sxs-lookup"><span data-stu-id="eed2c-153">Wait for a few seconds, then go back tooyour function logs and verify that hello new message has been read from hello queue.</span></span>

    ![Visualizza messaggio hello log.](./media/functions-create-storage-queue-triggered-function/functions-queue-storage-trigger-view-logs.png)

1. <span data-ttu-id="eed2c-155">In Esplora archivi, fare clic su **aggiornamento** e verificare il messaggio hello è stato elaborato e non è più in coda hello.</span><span class="sxs-lookup"><span data-stu-id="eed2c-155">Back in Storage Explorer, click **Refresh** and verify that hello message has been processed and is no longer in hello queue.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="eed2c-156">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="eed2c-156">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="eed2c-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="eed2c-157">Next steps</span></span>

<span data-ttu-id="eed2c-158">È stata creata una funzione che viene eseguito quando un messaggio viene aggiunto tooa coda di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="eed2c-158">You have created a function that runs when a message is added tooa storage queue.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="eed2c-159">Per altre informazioni sui trigger dell'archiviazione code, vedere [Associazioni della coda dell'archiviazione di Funzioni di Azure](functions-bindings-storage-queue.md).</span><span class="sxs-lookup"><span data-stu-id="eed2c-159">For more information about Queue storage triggers, see [Azure Functions Storage queue bindings](functions-bindings-storage-queue.md).</span></span>