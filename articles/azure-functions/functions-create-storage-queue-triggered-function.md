---
title: Creare una funzione in Azure attivata da messaggi di coda | Microsoft Docs
description: Usare Funzioni di Azure per creare una funzione senza server che viene richiamata da un messaggio inviato a una coda di archiviazione di Azure.
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
ms.openlocfilehash: 92a03154bf5a8945e2de9606afd138803c76fafe
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-triggered-by-azure-queue-storage"></a><span data-ttu-id="5cdb3-103">Creare una funzione attivata dall'archiviazione code di Azure</span><span class="sxs-lookup"><span data-stu-id="5cdb3-103">Create a function triggered by Azure Queue storage</span></span>

<span data-ttu-id="5cdb3-104">Informazioni su come creare una funzione attivata nel momento in cui vengono inviati messaggi a una coda di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="5cdb3-104">Learn how to create a function triggered when messages are submitted to an Azure Storage queue.</span></span>

![Visualizzare il messaggio nei log.](./media/functions-create-storage-queue-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="5cdb3-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5cdb3-106">Prerequisites</span></span>

- <span data-ttu-id="5cdb3-107">Scaricare e installare [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="5cdb3-107">Download and install the [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

- <span data-ttu-id="5cdb3-108">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="5cdb3-108">An Azure subscription.</span></span> <span data-ttu-id="5cdb3-109">Se non se ne ha una, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="5cdb3-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="5cdb3-110">Creare un'app per le funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="5cdb3-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![App per le funzioni creata correttamente.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="5cdb3-112">Si creerà ora una funzione nella nuova app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="5cdb3-112">Next, you create a function in the new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-queue-triggered-function"></a><span data-ttu-id="5cdb3-113">Creare una funzione attivata da una coda</span><span class="sxs-lookup"><span data-stu-id="5cdb3-113">Create a Queue triggered function</span></span>

1. <span data-ttu-id="5cdb3-114">Espandere l'app per le funzioni e fare clic sul pulsante **+** accanto a **Funzioni**.</span><span class="sxs-lookup"><span data-stu-id="5cdb3-114">Expand your function app and click the **+** button next to **Functions**.</span></span> <span data-ttu-id="5cdb3-115">Se questa è la prima funzione nell'app per le funzioni, selezionare **Funzione personalizzata**.</span><span class="sxs-lookup"><span data-stu-id="5cdb3-115">If this is the first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="5cdb3-116">Verrà visualizzato il set completo di modelli di funzione.</span><span class="sxs-lookup"><span data-stu-id="5cdb3-116">This displays the complete set of function templates.</span></span>

    ![Pagina della guida introduttiva di Funzioni nel portale di Azure](./media/functions-create-storage-queue-triggered-function/add-first-function.png)

2. <span data-ttu-id="5cdb3-118">Selezionare il modello **QueueTrigger** per la lingua desiderata e usare le impostazioni specificate nella tabella.</span><span class="sxs-lookup"><span data-stu-id="5cdb3-118">Select the **QueueTrigger** template for your desired language, and  use the settings as specified in the table.</span></span>

    ![Creare una funzione attivata da una coda di archiviazione.](./media/functions-create-storage-queue-triggered-function/functions-create-queue-storage-trigger-portal.png)
    
    | <span data-ttu-id="5cdb3-120">Impostazione</span><span class="sxs-lookup"><span data-stu-id="5cdb3-120">Setting</span></span> | <span data-ttu-id="5cdb3-121">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="5cdb3-121">Suggested value</span></span> | <span data-ttu-id="5cdb3-122">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5cdb3-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="5cdb3-123">**Nome coda**</span><span class="sxs-lookup"><span data-stu-id="5cdb3-123">**Queue name**</span></span>   | <span data-ttu-id="5cdb3-124">myqueue-items</span><span class="sxs-lookup"><span data-stu-id="5cdb3-124">myqueue-items</span></span>    | <span data-ttu-id="5cdb3-125">Nome della coda a cui connettersi nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="5cdb3-125">Name of the queue to connect to in your Storage account.</span></span> |
    | <span data-ttu-id="5cdb3-126">**Connessione dell'account di archiviazione**</span><span class="sxs-lookup"><span data-stu-id="5cdb3-126">**Storage account connection**</span></span> | <span data-ttu-id="5cdb3-127">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="5cdb3-127">AzureWebJobStorage</span></span> | <span data-ttu-id="5cdb3-128">È possibile usare la connessione dell'account di archiviazione già usata dall'app per le funzioni oppure crearne una nuova.</span><span class="sxs-lookup"><span data-stu-id="5cdb3-128">You can use the storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="5cdb3-129">**Dare un nome alla funzione**</span><span class="sxs-lookup"><span data-stu-id="5cdb3-129">**Name your function**</span></span> | <span data-ttu-id="5cdb3-130">Univoco nell'app per le funzioni</span><span class="sxs-lookup"><span data-stu-id="5cdb3-130">Unique in your function app</span></span> | <span data-ttu-id="5cdb3-131">Nome della funzione attivata dalla coda.</span><span class="sxs-lookup"><span data-stu-id="5cdb3-131">Name of this queue triggered function.</span></span> |

3. <span data-ttu-id="5cdb3-132">Fare clic su **Crea** per creare la funzione.</span><span class="sxs-lookup"><span data-stu-id="5cdb3-132">Click **Create** to create your function.</span></span>

<span data-ttu-id="5cdb3-133">Connettersi quindi all'account di archiviazione di Azure e creare la coda di archiviazione **myqueue-items**.</span><span class="sxs-lookup"><span data-stu-id="5cdb3-133">Next, you connect to your Azure Storage account and create the **myqueue-items** storage queue.</span></span>

## <a name="create-the-queue"></a><span data-ttu-id="5cdb3-134">Creare la coda</span><span class="sxs-lookup"><span data-stu-id="5cdb3-134">Create the queue</span></span>

1. <span data-ttu-id="5cdb3-135">Nella funzione fare clic su **Integrazione**, espandere **Documentazione** e copiare sia **Nome account** sia **Chiave account**.</span><span class="sxs-lookup"><span data-stu-id="5cdb3-135">In your function, click **Integrate**, expand **Documentation**, and copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="5cdb3-136">Usare queste credenziali per connettersi all'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="5cdb3-136">You use these credentials to connect to the storage account.</span></span> <span data-ttu-id="5cdb3-137">Se si è già connessi all'account di archiviazione, andare al passaggio 4.</span><span class="sxs-lookup"><span data-stu-id="5cdb3-137">If you have already connected your storage account, skip to step 4.</span></span>

    ![Ottenere le credenziali per la connessione all'account di archiviazione.](./media/functions-create-storage-queue-triggered-function/functions-storage-account-connection.png)<span data-ttu-id="5cdb3-139">v</span><span class="sxs-lookup"><span data-stu-id="5cdb3-139">v</span></span>

1. <span data-ttu-id="5cdb3-140">Eseguire lo strumento [Microsoft Azure Storage Explorer](http://storageexplorer.com/), fare clic sull'icona di connessione a sinistra, scegliere **Use a storage account name and key** (Usare il nome e la chiave di un account di archiviazione) e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="5cdb3-140">Run the [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, click the connect icon on the left, choose **Use a storage account name and key**, and click **Next**.</span></span>

    ![Eseguire lo strumento di esplorazione dell'account di archiviazione.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-1.png)

1. <span data-ttu-id="5cdb3-142">Immettere i valori **Nome account** e **Chiave account** definiti nel passaggio 1, fare clic su **Avanti** e quindi su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="5cdb3-142">Enter the **Account name** and **Account key** from step 1, click **Next** and then **Connect**.</span></span>

    ![Immettere le credenziali di archiviazione ed eseguire la connessione.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-2.png)

1. <span data-ttu-id="5cdb3-144">Espandere l'account di archiviazione associato, fare doppio clic su **Code**, fare clic su **Crea coda**, digitare `myqueue-items` e quindi premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="5cdb3-144">Expand the attached storage account, right-click **Queues**, click **Create queue**, type `myqueue-items`, and then press enter.</span></span>

    ![Creare una coda di archiviazione.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-create-queue.png)

<span data-ttu-id="5cdb3-146">È possibile ora testare la funzione aggiungendo un messaggio alla coda.</span><span class="sxs-lookup"><span data-stu-id="5cdb3-146">Now that you have a storage queue, you can test the function by adding a message to the queue.</span></span>

## <a name="test-the-function"></a><span data-ttu-id="5cdb3-147">Testare la funzione</span><span class="sxs-lookup"><span data-stu-id="5cdb3-147">Test the function</span></span>

1. <span data-ttu-id="5cdb3-148">Tornare al portale di Azure, selezionare la funzione, espandere i **log** nella parte inferiore della pagina e assicurarsi che lo streaming dei log non sia stato interrotto.</span><span class="sxs-lookup"><span data-stu-id="5cdb3-148">Back in the Azure portal, browse to your function expand the **Logs** at the bottom of the page and make sure that log streaming isn't paused.</span></span>

1. <span data-ttu-id="5cdb3-149">In Esplora archivi espandere l'account di archiviazione, **Code** e **myqueue-items** e quindi fare clic su **Aggiungi messaggio**.</span><span class="sxs-lookup"><span data-stu-id="5cdb3-149">In Storage Explorer, expand your storage account, **Queues**, and **myqueue-items**, then click **Add message**.</span></span>

    ![Aggiungere un messaggio alla coda.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-add-message.png)

1. <span data-ttu-id="5cdb3-151">Digitare il proprio messaggio di benvenuto</span><span class="sxs-lookup"><span data-stu-id="5cdb3-151">Type your "Hello World!"</span></span> <span data-ttu-id="5cdb3-152">nel campo **Testo del messaggio** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="5cdb3-152">message in **Message text** and click **OK**.</span></span>

1. <span data-ttu-id="5cdb3-153">Attendere alcuni secondi, tornare ai log di funzione e verificare che il nuovo messaggio sia stato letto dalla coda.</span><span class="sxs-lookup"><span data-stu-id="5cdb3-153">Wait for a few seconds, then go back to your function logs and verify that the new message has been read from the queue.</span></span>

    ![Visualizzare il messaggio nei log.](./media/functions-create-storage-queue-triggered-function/functions-queue-storage-trigger-view-logs.png)

1. <span data-ttu-id="5cdb3-155">Tornare a Esplora archivi, fare clic su **Aggiorna** e verificare che il messaggio sia stato elaborato e non sia più in coda.</span><span class="sxs-lookup"><span data-stu-id="5cdb3-155">Back in Storage Explorer, click **Refresh** and verify that the message has been processed and is no longer in the queue.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="5cdb3-156">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="5cdb3-156">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="5cdb3-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5cdb3-157">Next steps</span></span>

<span data-ttu-id="5cdb3-158">È stata creata una funzione che viene eseguita nel momento in cui un messaggio viene aggiunto a una coda di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="5cdb3-158">You have created a function that runs when a message is added to a storage queue.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="5cdb3-159">Per altre informazioni sui trigger dell'archiviazione code, vedere [Associazioni della coda dell'archiviazione di Funzioni di Azure](functions-bindings-storage-queue.md).</span><span class="sxs-lookup"><span data-stu-id="5cdb3-159">For more information about Queue storage triggers, see [Azure Functions Storage queue bindings](functions-bindings-storage-queue.md).</span></span>