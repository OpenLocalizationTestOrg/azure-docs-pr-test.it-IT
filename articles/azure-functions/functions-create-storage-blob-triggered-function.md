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
# <a name="create-a-function-triggered-by-azure-blob-storage"></a><span data-ttu-id="9c953-103">Creare una funzione attivata dall'archiviazione BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="9c953-103">Create a function triggered by Azure Blob storage</span></span>

<span data-ttu-id="9c953-104">Informazioni su come toocreate una funzione di attivazione eseguita quando i file vengono caricati tooor aggiornato nell'archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="9c953-104">Learn how toocreate a function triggered when files are uploaded tooor updated in Azure Blob storage.</span></span>

![Visualizza messaggio hello log.](./media/functions-create-storage-blob-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="9c953-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="9c953-106">Prerequisites</span></span>

+ <span data-ttu-id="9c953-107">Scaricare e installare hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="9c953-107">Download and install hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>
+ <span data-ttu-id="9c953-108">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="9c953-108">An Azure subscription.</span></span> <span data-ttu-id="9c953-109">Se non se ne ha una, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="9c953-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="9c953-110">Creare un'app per le funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="9c953-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![App per le funzioni creata correttamente.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="9c953-112">Creare quindi una funzione in hello nuova funzione app.</span><span class="sxs-lookup"><span data-stu-id="9c953-112">Next, you create a function in hello new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-blob-storage-triggered-function"></a><span data-ttu-id="9c953-113">Creare una funzione attivata dall'archiviazione BLOB</span><span class="sxs-lookup"><span data-stu-id="9c953-113">Create a Blob storage triggered function</span></span>

1. <span data-ttu-id="9c953-114">Espandere l'applicazione di funzione e fare clic su hello  **+**  accanto troppo**funzioni**.</span><span class="sxs-lookup"><span data-stu-id="9c953-114">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="9c953-115">Se si tratta di hello prima funzione di app di funzione, selezionare **funzione personalizzata**.</span><span class="sxs-lookup"><span data-stu-id="9c953-115">If this is hello first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="9c953-116">Consente di visualizzare il set completo di hello dei modelli di funzione.</span><span class="sxs-lookup"><span data-stu-id="9c953-116">This displays hello complete set of function templates.</span></span>

    ![Pagina di avvio rapido di funzioni in hello portale di Azure](./media/functions-create-storage-blob-triggered-function/add-first-function.png)

2. <span data-ttu-id="9c953-118">Seleziona hello **BlobTrigger** modello per la lingua desiderata e utilizza le impostazioni di hello come specificato nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="9c953-118">Select hello **BlobTrigger** template for your desired language, and use hello settings as specified in hello table.</span></span>

    ![Creare una funzione di archiviazione generato hello Blob.](./media/functions-create-storage-blob-triggered-function/functions-create-blob-storage-trigger-portal.png)

    | <span data-ttu-id="9c953-120">Impostazione</span><span class="sxs-lookup"><span data-stu-id="9c953-120">Setting</span></span> | <span data-ttu-id="9c953-121">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="9c953-121">Suggested value</span></span> | <span data-ttu-id="9c953-122">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9c953-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="9c953-123">**Percorso**</span><span class="sxs-lookup"><span data-stu-id="9c953-123">**Path**</span></span>   | <span data-ttu-id="9c953-124">mycontainer/{name}</span><span class="sxs-lookup"><span data-stu-id="9c953-124">mycontainer/{name}</span></span>    | <span data-ttu-id="9c953-125">Percorso da monitorare nell'archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="9c953-125">Location in Blob storage being monitored.</span></span> <span data-ttu-id="9c953-126">nome del file Hello del blob hello viene passato nell'associazione hello come hello _nome_ parametro.</span><span class="sxs-lookup"><span data-stu-id="9c953-126">hello file name of hello blob is passed in hello binding as hello _name_ parameter.</span></span>  |
    | <span data-ttu-id="9c953-127">**Connessione dell'account di archiviazione**</span><span class="sxs-lookup"><span data-stu-id="9c953-127">**Storage account connection**</span></span> | <span data-ttu-id="9c953-128">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="9c953-128">AzureWebJobStorage</span></span> | <span data-ttu-id="9c953-129">È possibile utilizzare una connessione ad account di archiviazione hello già in uso dalla tua app di funzione o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="9c953-129">You can use hello storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="9c953-130">**Dare un nome alla funzione**</span><span class="sxs-lookup"><span data-stu-id="9c953-130">**Name your function**</span></span> | <span data-ttu-id="9c953-131">Univoco nell'app per le funzioni</span><span class="sxs-lookup"><span data-stu-id="9c953-131">Unique in your function app</span></span> | <span data-ttu-id="9c953-132">Nome della funzione attivata dal BLOB.</span><span class="sxs-lookup"><span data-stu-id="9c953-132">Name of this blob triggered function.</span></span> |

3. <span data-ttu-id="9c953-133">Fare clic su **crea** toocreate la funzione.</span><span class="sxs-lookup"><span data-stu-id="9c953-133">Click **Create** toocreate your function.</span></span>

<span data-ttu-id="9c953-134">Successivamente, connettersi tooyour account di archiviazione Azure e creare hello **mycontainer** contenitore.</span><span class="sxs-lookup"><span data-stu-id="9c953-134">Next, you connect tooyour Azure Storage account and create hello **mycontainer** container.</span></span>

## <a name="create-hello-container"></a><span data-ttu-id="9c953-135">Creare il contenitore di hello</span><span class="sxs-lookup"><span data-stu-id="9c953-135">Create hello container</span></span>

1. <span data-ttu-id="9c953-136">Nella funzione fare clic su **Integrazione**, espandere **Documentazione** e copiare sia **Nome account** sia **Chiave account**.</span><span class="sxs-lookup"><span data-stu-id="9c953-136">In your function, click **Integrate**, expand **Documentation**, and copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="9c953-137">Utilizzare questi account di archiviazione di credenziali tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="9c953-137">You use these credentials tooconnect toohello storage account.</span></span> <span data-ttu-id="9c953-138">Se si è già connessi all'account di archiviazione, ignorare toostep 4.</span><span class="sxs-lookup"><span data-stu-id="9c953-138">If you have already connected your storage account, skip toostep 4.</span></span>

    ![Ottenere l'account di archiviazione hello le credenziali di connessione.](./media/functions-create-storage-blob-triggered-function/functions-storage-account-connection.png)

1. <span data-ttu-id="9c953-140">Eseguire hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) strumento, fare clic su hello icona a sinistra di hello della connessione, scegliere **utilizzare un nome account di archiviazione e una chiave**, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="9c953-140">Run hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, click hello connect icon on hello left, choose **Use a storage account name and key**, and click **Next**.</span></span>

    ![Eseguire lo strumento di esplorazione dell'archiviazione Account hello.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-1.png)

1. <span data-ttu-id="9c953-142">Immettere hello **nome Account** e **chiave dell'Account** nel passaggio 1, fare clic su **Avanti** e quindi **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="9c953-142">Enter hello **Account name** and **Account key** from step 1, click **Next** and then **Connect**.</span></span> 

    ![Immettere le credenziali di archiviazione hello e connettersi.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-2.png)

1. <span data-ttu-id="9c953-144">Espandere l'account di archiviazione collegato hello destro del mouse su **contenitori Blob**, fare clic su **crea contenitore blob**, tipo `mycontainer`, quindi premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="9c953-144">Expand hello attached storage account, right-click **Blob containers**, click **Create blob container**, type `mycontainer`, and then press enter.</span></span>

    ![Creare una coda di archiviazione.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-create-blob-container.png)

<span data-ttu-id="9c953-146">Dopo aver creato un contenitore blob, è possibile testare la funzione hello caricando un contenitore di toohello file.</span><span class="sxs-lookup"><span data-stu-id="9c953-146">Now that you have a blob container, you can test hello function by uploading a file toohello container.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="9c953-147">Funzione hello test</span><span class="sxs-lookup"><span data-stu-id="9c953-147">Test hello function</span></span>

1. <span data-ttu-id="9c953-148">Nel portale di Azure hello, funzione tooyour Sfoglia espandere hello **registri** nella parte inferiore di hello della pagina hello e assicurarsi che il log di streaming non è in pausa.</span><span class="sxs-lookup"><span data-stu-id="9c953-148">Back in hello Azure portal, browse tooyour function expand hello **Logs** at hello bottom of hello page and make sure that log streaming isn't paused.</span></span>

1. <span data-ttu-id="9c953-149">In Esplora archivi espandere l'account di archiviazione, **Contenitori BLOB** e **mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="9c953-149">In Storage Explorer, expand your storage account, **Blob containers**, and **mycontainer**.</span></span> <span data-ttu-id="9c953-150">Fare clic su **Carica** e quindi su **Carica file...**.</span><span class="sxs-lookup"><span data-stu-id="9c953-150">Click **Upload** and then **Upload files...**.</span></span>

    ![Caricare un contenitore di blob toohello file.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-upload-file-blob.png)

1. <span data-ttu-id="9c953-152">In hello **caricare file** finestra di dialogo fare clic su hello **file** campo.</span><span class="sxs-lookup"><span data-stu-id="9c953-152">In hello **Upload files** dialog box, click hello **Files** field.</span></span> <span data-ttu-id="9c953-153">Sfoglia file tooa nel computer locale, ad esempio un file di immagine, selezionarlo e fare clic su **aprire** e quindi **caricare**.</span><span class="sxs-lookup"><span data-stu-id="9c953-153">Browse tooa file on your local computer, such as an image file, select it and click **Open** and then **Upload**.</span></span>

1. <span data-ttu-id="9c953-154">Tornare indietro i log delle funzioni tooyour e verificare che BLOB hello è stato letto.</span><span class="sxs-lookup"><span data-stu-id="9c953-154">Go back tooyour function logs and verify that hello blob has been read.</span></span>

   ![Visualizza messaggio hello log.](./media/functions-create-storage-blob-triggered-function/functions-blob-storage-trigger-view-logs.png)

    >[!NOTE]
    > <span data-ttu-id="9c953-156">Quando l'app di funzione viene eseguita nel piano di utilizzo predefinito di hello, potrebbe esserci un ritardo di backup tooseveral minuti tra hello blob viene aggiunto o aggiornato e hello funzione venga attivata.</span><span class="sxs-lookup"><span data-stu-id="9c953-156">When your function app runs in hello default Consumption plan, there may be a delay of up tooseveral minutes between hello blob being added or updated and hello function being triggered.</span></span> <span data-ttu-id="9c953-157">Se nelle funzioni attivate dal BLOB è necessaria una bassa latenza, valutare l'opportunità di eseguire l'app per le funzioni in un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="9c953-157">If you need low latency in your blob triggered functions, consider running your function app in an App Service plan.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="9c953-158">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="9c953-158">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="9c953-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9c953-159">Next steps</span></span>

<span data-ttu-id="9c953-160">È stata creata una funzione che viene eseguito quando un blob viene aggiunto tooor aggiornato nell'archiviazione Blob.</span><span class="sxs-lookup"><span data-stu-id="9c953-160">You have created a function that runs when a blob is added tooor updated in Blob storage.</span></span> 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="9c953-161">Per altre informazioni sui trigger dell'archiviazione BLOB, vedere [Binding dell'archiviazione BLOB di Funzioni di Azure](functions-bindings-storage-blob.md).</span><span class="sxs-lookup"><span data-stu-id="9c953-161">For more information about Blob storage triggers, see [Azure Functions Blob storage bindings](functions-bindings-storage-blob.md).</span></span>
