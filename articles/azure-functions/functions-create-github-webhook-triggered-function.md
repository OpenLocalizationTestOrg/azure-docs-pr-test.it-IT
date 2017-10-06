---
title: una funzione in Azure attivata da un webhook di GitHub aaaCreate | Documenti Microsoft
description: Utilizzare le funzioni di Azure toocreate una funzione senza che viene richiamata da un webhook di GitHub.
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 36ef34b8-3729-4940-86d2-cb8e176fcc06
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 8ffcde82c9310d749159ed53eab113658e38a030
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-a-github-webhook"></a><span data-ttu-id="d4d8f-103">Creare una funzione attivata da un webhook GitHub</span><span class="sxs-lookup"><span data-stu-id="d4d8f-103">Create a function triggered by a GitHub webhook</span></span>

<span data-ttu-id="d4d8f-104">Informazioni su come toocreate una funzione che viene attivata da una richiesta di webhook HTTP con un payload specifico di GitHub.</span><span class="sxs-lookup"><span data-stu-id="d4d8f-104">Learn how toocreate a function that is triggered by an HTTP webhook request with a GitHub-specific payload.</span></span>

![Github Webhook è attivata nel portale di Azure hello (funzione)](./media/functions-create-github-webhook-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="d4d8f-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d4d8f-106">Prerequisites</span></span>

+ <span data-ttu-id="d4d8f-107">Un account GitHub con almeno un progetto.</span><span class="sxs-lookup"><span data-stu-id="d4d8f-107">A GitHub account with at least one project.</span></span>
+ <span data-ttu-id="d4d8f-108">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d4d8f-108">An Azure subscription.</span></span> <span data-ttu-id="d4d8f-109">Se non se ne ha una, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="d4d8f-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="d4d8f-110">Creare un'app per le funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="d4d8f-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![App per le funzioni creata correttamente.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="d4d8f-112">Creare quindi una funzione in hello nuova funzione app.</span><span class="sxs-lookup"><span data-stu-id="d4d8f-112">Next, you create a function in hello new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-github-webhook-triggered-function"></a><span data-ttu-id="d4d8f-113">Creare una funzione attivata da webhook GitHub</span><span class="sxs-lookup"><span data-stu-id="d4d8f-113">Create a GitHub webhook triggered function</span></span>

1. <span data-ttu-id="d4d8f-114">Espandere l'applicazione di funzione e fare clic su hello  **+**  accanto troppo**funzioni**.</span><span class="sxs-lookup"><span data-stu-id="d4d8f-114">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="d4d8f-115">Se si tratta di hello prima funzione di app di funzione, selezionare **funzione personalizzata**.</span><span class="sxs-lookup"><span data-stu-id="d4d8f-115">If this is hello first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="d4d8f-116">Consente di visualizzare il set completo di hello dei modelli di funzione.</span><span class="sxs-lookup"><span data-stu-id="d4d8f-116">This displays hello complete set of function templates.</span></span>

    ![Pagina di avvio rapido di funzioni in hello portale di Azure](./media/functions-create-github-webhook-triggered-function/add-first-function.png)

2. <span data-ttu-id="d4d8f-118">Seleziona hello **GitHub WebHook** modello per la lingua desiderata.</span><span class="sxs-lookup"><span data-stu-id="d4d8f-118">Select hello **GitHub WebHook** template for your desired language.</span></span> <span data-ttu-id="d4d8f-119">**Assegnare un nome alla funzione** e quindi selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d4d8f-119">**Name your function**, then select **Create**.</span></span>

     ![Creare una funzione di webhook attivato GitHub in hello portale di Azure](./media/functions-create-github-webhook-triggered-function/functions-create-github-webhook-trigger.png) 

3. <span data-ttu-id="d4d8f-121">Nella nuova funzione, fare clic su **<> / Get funzione URL**, quindi copiare e salvare i valori hello.</span><span class="sxs-lookup"><span data-stu-id="d4d8f-121">In your new function, click **</> Get function URL**, then copy and save hello values.</span></span> <span data-ttu-id="d4d8f-122">Hello stessa operazione per **<> / GitHub ottenere segreto**.</span><span class="sxs-lookup"><span data-stu-id="d4d8f-122">Do hello same thing for **</> Get GitHub secret**.</span></span> <span data-ttu-id="d4d8f-123">Utilizzare queste webhook hello tooconfigure di valori in GitHub.</span><span class="sxs-lookup"><span data-stu-id="d4d8f-123">You use these values tooconfigure hello webhook in GitHub.</span></span>

    ![Esaminare il codice di funzione hello](./media/functions-create-github-webhook-triggered-function/functions-copy-function-url-github-secret.png)

<span data-ttu-id="d4d8f-125">Viene successivamente creato un webhook nel repository GitHub.</span><span class="sxs-lookup"><span data-stu-id="d4d8f-125">Next, you create a webhook in your GitHub repository.</span></span>

## <a name="configure-hello-webhook"></a><span data-ttu-id="d4d8f-126">Configurare hello webhook</span><span class="sxs-lookup"><span data-stu-id="d4d8f-126">Configure hello webhook</span></span>

1. <span data-ttu-id="d4d8f-127">In GitHub passare tooa repository che si è proprietari.</span><span class="sxs-lookup"><span data-stu-id="d4d8f-127">In GitHub, navigate tooa repository that you own.</span></span> <span data-ttu-id="d4d8f-128">È possibile usare anche qualsiasi repository biforcato.</span><span class="sxs-lookup"><span data-stu-id="d4d8f-128">You can also use any repository that you have forked.</span></span> <span data-ttu-id="d4d8f-129">Se è necessario un repository toofork, utilizzare <https://github.com/Azure-Samples/functions-quickstart>.</span><span class="sxs-lookup"><span data-stu-id="d4d8f-129">If you need toofork a repository, use <https://github.com/Azure-Samples/functions-quickstart>.</span></span>

1. <span data-ttu-id="d4d8f-130">Fare clic su **Impostazioni**, quindi su **Webhook** e infine su **Aggiungi webhook**.</span><span class="sxs-lookup"><span data-stu-id="d4d8f-130">Click **Settings**, then click **Webhooks**, and  **Add webhook**.</span></span>

    ![Aggiungere un webhook di GitHub](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-2.png)

1. <span data-ttu-id="d4d8f-132">Utilizzare le impostazioni come specificato nella tabella hello, quindi fare clic su **aggiungere webhook**.</span><span class="sxs-lookup"><span data-stu-id="d4d8f-132">Use settings as specified in hello table, then click **Add webhook**.</span></span>

    ![Impostare l'URL del webhook hello e il segreto](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-3.png)

| <span data-ttu-id="d4d8f-134">Impostazione</span><span class="sxs-lookup"><span data-stu-id="d4d8f-134">Setting</span></span> | <span data-ttu-id="d4d8f-135">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="d4d8f-135">Suggested value</span></span> | <span data-ttu-id="d4d8f-136">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d4d8f-136">Description</span></span> |
|---|---|---|
| <span data-ttu-id="d4d8f-137">**Payload URL** (URL payload)</span><span class="sxs-lookup"><span data-stu-id="d4d8f-137">**Payload URL**</span></span> | <span data-ttu-id="d4d8f-138">Valore copiato</span><span class="sxs-lookup"><span data-stu-id="d4d8f-138">Copied value</span></span> | <span data-ttu-id="d4d8f-139">Utilizzare il valore di hello restituito da **<> / Get funzione URL**.</span><span class="sxs-lookup"><span data-stu-id="d4d8f-139">Use hello value returned by  **</> Get function URL**.</span></span> |
| <span data-ttu-id="d4d8f-140">**Segreto**</span><span class="sxs-lookup"><span data-stu-id="d4d8f-140">**Secret**</span></span>   | <span data-ttu-id="d4d8f-141">Valore copiato</span><span class="sxs-lookup"><span data-stu-id="d4d8f-141">Copied value</span></span> | <span data-ttu-id="d4d8f-142">Utilizzare il valore di hello restituito da **<> / GitHub ottenere segreto**.</span><span class="sxs-lookup"><span data-stu-id="d4d8f-142">Use hello value returned by  **</> Get GitHub secret**.</span></span> |
| <span data-ttu-id="d4d8f-143">**Tipo contenuto**</span><span class="sxs-lookup"><span data-stu-id="d4d8f-143">**Content type**</span></span> | <span data-ttu-id="d4d8f-144">application/json</span><span class="sxs-lookup"><span data-stu-id="d4d8f-144">application/json</span></span> | <span data-ttu-id="d4d8f-145">funzione Hello prevede un payload JSON.</span><span class="sxs-lookup"><span data-stu-id="d4d8f-145">hello function expects a JSON payload.</span></span> |
| <span data-ttu-id="d4d8f-146">Trigger di evento</span><span class="sxs-lookup"><span data-stu-id="d4d8f-146">Event triggers</span></span> | <span data-ttu-id="d4d8f-147">Selezione di singoli eventi</span><span class="sxs-lookup"><span data-stu-id="d4d8f-147">Let me select individual events</span></span> | <span data-ttu-id="d4d8f-148">Vogliamo solo tootrigger sugli eventi di commento problema.</span><span class="sxs-lookup"><span data-stu-id="d4d8f-148">We only want tootrigger on issue comment events.</span></span>  |
| | <span data-ttu-id="d4d8f-149">Commento al problema</span><span class="sxs-lookup"><span data-stu-id="d4d8f-149">Issue comment</span></span> |  |

<span data-ttu-id="d4d8f-150">A questo punto, hello webhook è la funzione tootrigger configurata quando viene aggiunto un nuovo commento problema.</span><span class="sxs-lookup"><span data-stu-id="d4d8f-150">Now, hello webhook is configured tootrigger your function when a new issue comment is added.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="d4d8f-151">Funzione hello test</span><span class="sxs-lookup"><span data-stu-id="d4d8f-151">Test hello function</span></span>

1. <span data-ttu-id="d4d8f-152">Nel repository GitHub, aprire hello **problemi** scheda in una nuova finestra del browser.</span><span class="sxs-lookup"><span data-stu-id="d4d8f-152">In your GitHub repository, open hello **Issues** tab in a new browser window.</span></span>

1. <span data-ttu-id="d4d8f-153">In nuova finestra hello, fare clic su **nuovo problema**, digitare un titolo e quindi fare clic su **inviare di nuovo problema**.</span><span class="sxs-lookup"><span data-stu-id="d4d8f-153">In hello new window, click **New Issue**, type a title, and then click **Submit new issue**.</span></span>

1. <span data-ttu-id="d4d8f-154">Problema di hello, digitare un commento e fare clic su **commento**.</span><span class="sxs-lookup"><span data-stu-id="d4d8f-154">In hello issue, type a comment and click **Comment**.</span></span>

    ![Aggiungere un commento al problema GitHub.](./media/functions-create-github-webhook-triggered-function/functions-github-webhook-add-comment.png)

1. <span data-ttu-id="d4d8f-156">Tornare indietro toohello portale e visualizzare i registri di hello.</span><span class="sxs-lookup"><span data-stu-id="d4d8f-156">Go back toohello portal and view hello logs.</span></span> <span data-ttu-id="d4d8f-157">Verrà visualizzata una voce di traccia con nuovo testo del commento hello.</span><span class="sxs-lookup"><span data-stu-id="d4d8f-157">You should see a trace entry with hello new comment text.</span></span>

     ![Visualizza il testo del commento hello nei registri hello.](./media/functions-create-github-webhook-triggered-function/function-app-view-logs.png)

## <a name="clean-up-resources"></a><span data-ttu-id="d4d8f-159">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="d4d8f-159">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="d4d8f-160">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d4d8f-160">Next steps</span></span>

<span data-ttu-id="d4d8f-161">È stata creata una funzione che viene eseguita quando viene ricevuta una richiesta da un webhook GitHub.</span><span class="sxs-lookup"><span data-stu-id="d4d8f-161">You have created a function that runs when a request is received from a GitHub webhook.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="d4d8f-162">Per altre informazioni sui trigger webhook, vedere [Associazioni HTTP e webhook in Funzioni di Azure](functions-bindings-http-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="d4d8f-162">For more information about webhook triggers, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span>
