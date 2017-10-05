---
title: Creare una funzione in Azure attivata dall'archiviazione BLOB| Microsoft Docs
description: Usare Funzioni di Azure per creare una funzione senza server che viene richiamata da elementi aggiunti all'archiviazione BLOB di Azure.
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
ms.openlocfilehash: 1ddd056903b1a2f973a58bd7054ea2b8281607c3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-triggered-by-azure-blob-storage"></a><span data-ttu-id="871e7-103">Creare una funzione attivata dall'archiviazione BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="871e7-103">Create a function triggered by Azure Blob storage</span></span>

<span data-ttu-id="871e7-104">Informazioni su come creare una funzione attivata nel momento in cui vengono caricati o aggiornati file nell'archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="871e7-104">Learn how to create a function triggered when files are uploaded to or updated in Azure Blob storage.</span></span>

![Visualizzare il messaggio nei log.](./media/functions-create-storage-blob-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="871e7-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="871e7-106">Prerequisites</span></span>

+ <span data-ttu-id="871e7-107">Scaricare e installare [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="871e7-107">Download and install the [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>
+ <span data-ttu-id="871e7-108">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="871e7-108">An Azure subscription.</span></span> <span data-ttu-id="871e7-109">Se non se ne ha una, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="871e7-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="871e7-110">Creare un'app per le funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="871e7-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![App per le funzioni creata correttamente.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="871e7-112">Si creerà ora una funzione nella nuova app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="871e7-112">Next, you create a function in the new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-blob-storage-triggered-function"></a><span data-ttu-id="871e7-113">Creare una funzione attivata dall'archiviazione BLOB</span><span class="sxs-lookup"><span data-stu-id="871e7-113">Create a Blob storage triggered function</span></span>

1. <span data-ttu-id="871e7-114">Espandere l'app per le funzioni e fare clic sul pulsante **+** accanto a **Funzioni**.</span><span class="sxs-lookup"><span data-stu-id="871e7-114">Expand your function app and click the **+** button next to **Functions**.</span></span> <span data-ttu-id="871e7-115">Se questa è la prima funzione nell'app per le funzioni, selezionare **Funzione personalizzata**.</span><span class="sxs-lookup"><span data-stu-id="871e7-115">If this is the first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="871e7-116">Verrà visualizzato il set completo di modelli di funzione.</span><span class="sxs-lookup"><span data-stu-id="871e7-116">This displays the complete set of function templates.</span></span>

    ![Pagina della guida introduttiva di Funzioni nel portale di Azure](./media/functions-create-storage-blob-triggered-function/add-first-function.png)

2. <span data-ttu-id="871e7-118">Selezionare il modello **BlobTrigger** per la lingua desiderata e usare le impostazioni specificate nella tabella.</span><span class="sxs-lookup"><span data-stu-id="871e7-118">Select the **BlobTrigger** template for your desired language, and use the settings as specified in the table.</span></span>

    ![Creare una funzione attivata dall'archiviazione BLOB.](./media/functions-create-storage-blob-triggered-function/functions-create-blob-storage-trigger-portal.png)

    | <span data-ttu-id="871e7-120">Impostazione</span><span class="sxs-lookup"><span data-stu-id="871e7-120">Setting</span></span> | <span data-ttu-id="871e7-121">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="871e7-121">Suggested value</span></span> | <span data-ttu-id="871e7-122">Descrizione</span><span class="sxs-lookup"><span data-stu-id="871e7-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="871e7-123">**Percorso**</span><span class="sxs-lookup"><span data-stu-id="871e7-123">**Path**</span></span>   | <span data-ttu-id="871e7-124">mycontainer/{name}</span><span class="sxs-lookup"><span data-stu-id="871e7-124">mycontainer/{name}</span></span>    | <span data-ttu-id="871e7-125">Percorso da monitorare nell'archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="871e7-125">Location in Blob storage being monitored.</span></span> <span data-ttu-id="871e7-126">Il nome file del BLOB viene passato nel binding come parametro _name_.</span><span class="sxs-lookup"><span data-stu-id="871e7-126">The file name of the blob is passed in the binding as the _name_ parameter.</span></span>  |
    | <span data-ttu-id="871e7-127">**Connessione dell'account di archiviazione**</span><span class="sxs-lookup"><span data-stu-id="871e7-127">**Storage account connection**</span></span> | <span data-ttu-id="871e7-128">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="871e7-128">AzureWebJobStorage</span></span> | <span data-ttu-id="871e7-129">È possibile usare la connessione dell'account di archiviazione già usata dall'app per le funzioni oppure crearne una nuova.</span><span class="sxs-lookup"><span data-stu-id="871e7-129">You can use the storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="871e7-130">**Dare un nome alla funzione**</span><span class="sxs-lookup"><span data-stu-id="871e7-130">**Name your function**</span></span> | <span data-ttu-id="871e7-131">Univoco nell'app per le funzioni</span><span class="sxs-lookup"><span data-stu-id="871e7-131">Unique in your function app</span></span> | <span data-ttu-id="871e7-132">Nome della funzione attivata dal BLOB.</span><span class="sxs-lookup"><span data-stu-id="871e7-132">Name of this blob triggered function.</span></span> |

3. <span data-ttu-id="871e7-133">Fare clic su **Crea** per creare la funzione.</span><span class="sxs-lookup"><span data-stu-id="871e7-133">Click **Create** to create your function.</span></span>

<span data-ttu-id="871e7-134">Connettersi quindi all'account di archiviazione di Azure e creare il contenitore **mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="871e7-134">Next, you connect to your Azure Storage account and create the **mycontainer** container.</span></span>

## <a name="create-the-container"></a><span data-ttu-id="871e7-135">Creare il contenitore</span><span class="sxs-lookup"><span data-stu-id="871e7-135">Create the container</span></span>

1. <span data-ttu-id="871e7-136">Nella funzione fare clic su **Integrazione**, espandere **Documentazione** e copiare sia **Nome account** sia **Chiave account**.</span><span class="sxs-lookup"><span data-stu-id="871e7-136">In your function, click **Integrate**, expand **Documentation**, and copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="871e7-137">Usare queste credenziali per connettersi all'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="871e7-137">You use these credentials to connect to the storage account.</span></span> <span data-ttu-id="871e7-138">Se si è già connessi all'account di archiviazione, andare al passaggio 4.</span><span class="sxs-lookup"><span data-stu-id="871e7-138">If you have already connected your storage account, skip to step 4.</span></span>

    ![Ottenere le credenziali per la connessione all'account di archiviazione.](./media/functions-create-storage-blob-triggered-function/functions-storage-account-connection.png)

1. <span data-ttu-id="871e7-140">Eseguire lo strumento [Microsoft Azure Storage Explorer](http://storageexplorer.com/), fare clic sull'icona di connessione a sinistra, scegliere **Use a storage account name and key** (Usare il nome e la chiave di un account di archiviazione) e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="871e7-140">Run the [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, click the connect icon on the left, choose **Use a storage account name and key**, and click **Next**.</span></span>

    ![Eseguire lo strumento di esplorazione dell'account di archiviazione.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-1.png)

1. <span data-ttu-id="871e7-142">Immettere i valori **Nome account** e **Chiave account** definiti nel passaggio 1, fare clic su **Avanti** e quindi su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="871e7-142">Enter the **Account name** and **Account key** from step 1, click **Next** and then **Connect**.</span></span> 

    ![Immettere le credenziali di archiviazione ed eseguire la connessione.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-2.png)

1. <span data-ttu-id="871e7-144">Espandere l'account di archiviazione associato, fare doppio clic su **Contenitori BLOB**, fare clic su **Crea contenitore BLOB**, digitare `mycontainer` e quindi premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="871e7-144">Expand the attached storage account, right-click **Blob containers**, click **Create blob container**, type `mycontainer`, and then press enter.</span></span>

    ![Creare una coda di archiviazione.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-create-blob-container.png)

<span data-ttu-id="871e7-146">Dopo aver creato un contenitore BLOB, è possibile ora testare la funzione caricando un file nel contenitore.</span><span class="sxs-lookup"><span data-stu-id="871e7-146">Now that you have a blob container, you can test the function by uploading a file to the container.</span></span>

## <a name="test-the-function"></a><span data-ttu-id="871e7-147">Testare la funzione</span><span class="sxs-lookup"><span data-stu-id="871e7-147">Test the function</span></span>

1. <span data-ttu-id="871e7-148">Tornare al portale di Azure, selezionare la funzione, espandere i **log** nella parte inferiore della pagina e assicurarsi che lo streaming dei log non sia stato interrotto.</span><span class="sxs-lookup"><span data-stu-id="871e7-148">Back in the Azure portal, browse to your function expand the **Logs** at the bottom of the page and make sure that log streaming isn't paused.</span></span>

1. <span data-ttu-id="871e7-149">In Esplora archivi espandere l'account di archiviazione, **Contenitori BLOB** e **mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="871e7-149">In Storage Explorer, expand your storage account, **Blob containers**, and **mycontainer**.</span></span> <span data-ttu-id="871e7-150">Fare clic su **Carica** e quindi su **Carica file...**.</span><span class="sxs-lookup"><span data-stu-id="871e7-150">Click **Upload** and then **Upload files...**.</span></span>

    ![Caricare un file nel contenitore BLOB.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-upload-file-blob.png)

1. <span data-ttu-id="871e7-152">Nella finestra di dialogo **Carica file** fare clic sul campo **File**.</span><span class="sxs-lookup"><span data-stu-id="871e7-152">In the **Upload files** dialog box, click the **Files** field.</span></span> <span data-ttu-id="871e7-153">Identificare un file nel computer locale, ad esempio un file di immagine, selezionarlo e fare clic su **Apri** e quindi su **Carica**.</span><span class="sxs-lookup"><span data-stu-id="871e7-153">Browse to a file on your local computer, such as an image file, select it and click **Open** and then **Upload**.</span></span>

1. <span data-ttu-id="871e7-154">Tornare ai log di funzione e verificare che il BLOB sia stato letto.</span><span class="sxs-lookup"><span data-stu-id="871e7-154">Go back to your function logs and verify that the blob has been read.</span></span>

   ![Visualizzare il messaggio nei log.](./media/functions-create-storage-blob-triggered-function/functions-blob-storage-trigger-view-logs.png)

    >[!NOTE]
    > <span data-ttu-id="871e7-156">Se l'app per le funzioni viene eseguita nel piano a consumo predefinito, è possibile che si verifichi un ritardo di alcuni minuti tra il momento in cui il BLOB viene aggiunto o aggiornato e il momento in cui viene attivata la funzione.</span><span class="sxs-lookup"><span data-stu-id="871e7-156">When your function app runs in the default Consumption plan, there may be a delay of up to several minutes between the blob being added or updated and the function being triggered.</span></span> <span data-ttu-id="871e7-157">Se nelle funzioni attivate dal BLOB è necessaria una bassa latenza, valutare l'opportunità di eseguire l'app per le funzioni in un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="871e7-157">If you need low latency in your blob triggered functions, consider running your function app in an App Service plan.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="871e7-158">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="871e7-158">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="871e7-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="871e7-159">Next steps</span></span>

<span data-ttu-id="871e7-160">È stata creata una funzione che viene eseguita nel momento in cui nell'archiviazione BLOB viene aggiunto o aggiornato un BLOB.</span><span class="sxs-lookup"><span data-stu-id="871e7-160">You have created a function that runs when a blob is added to or updated in Blob storage.</span></span> 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="871e7-161">Per altre informazioni sui trigger dell'archiviazione BLOB, vedere [Binding dell'archiviazione BLOB di Funzioni di Azure](functions-bindings-storage-blob.md).</span><span class="sxs-lookup"><span data-stu-id="871e7-161">For more information about Blob storage triggers, see [Azure Functions Blob storage bindings](functions-bindings-storage-blob.md).</span></span>
