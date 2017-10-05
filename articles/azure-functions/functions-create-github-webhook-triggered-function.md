---
title: Creare una funzione in Azure attivata da un webhook GitHub | Microsoft Docs
description: Usare Funzioni di Azure per creare una funzione senza server che viene richiamata da un webhook GitHub.
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
ms.openlocfilehash: 038bb4cf0a9278416261c05ddaa0ee97d83b63c5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-triggered-by-a-github-webhook"></a><span data-ttu-id="a821e-103">Creare una funzione attivata da un webhook GitHub</span><span class="sxs-lookup"><span data-stu-id="a821e-103">Create a function triggered by a GitHub webhook</span></span>

<span data-ttu-id="a821e-104">Informazioni su come creare una funzione attivata da una richiesta di webhook HTTP con un payload specifico di GitHub.</span><span class="sxs-lookup"><span data-stu-id="a821e-104">Learn how to create a function that is triggered by an HTTP webhook request with a GitHub-specific payload.</span></span>

![Funzione attivata da un webhook GitHub nel portale di Azure](./media/functions-create-github-webhook-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="a821e-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a821e-106">Prerequisites</span></span>

+ <span data-ttu-id="a821e-107">Un account GitHub con almeno un progetto.</span><span class="sxs-lookup"><span data-stu-id="a821e-107">A GitHub account with at least one project.</span></span>
+ <span data-ttu-id="a821e-108">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a821e-108">An Azure subscription.</span></span> <span data-ttu-id="a821e-109">Se non se ne ha una, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="a821e-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="a821e-110">Creare un'app per le funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="a821e-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![App per le funzioni creata correttamente.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="a821e-112">Si creerà ora una funzione nella nuova app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="a821e-112">Next, you create a function in the new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-github-webhook-triggered-function"></a><span data-ttu-id="a821e-113">Creare una funzione attivata da webhook GitHub</span><span class="sxs-lookup"><span data-stu-id="a821e-113">Create a GitHub webhook triggered function</span></span>

1. <span data-ttu-id="a821e-114">Espandere l'app per le funzioni e fare clic sul pulsante **+** accanto a **Funzioni**.</span><span class="sxs-lookup"><span data-stu-id="a821e-114">Expand your function app and click the **+** button next to **Functions**.</span></span> <span data-ttu-id="a821e-115">Se questa è la prima funzione nell'app per le funzioni, selezionare **Funzione personalizzata**.</span><span class="sxs-lookup"><span data-stu-id="a821e-115">If this is the first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="a821e-116">Verrà visualizzato il set completo di modelli di funzione.</span><span class="sxs-lookup"><span data-stu-id="a821e-116">This displays the complete set of function templates.</span></span>

    ![Pagina della guida introduttiva di Funzioni nel portale di Azure](./media/functions-create-github-webhook-triggered-function/add-first-function.png)

2. <span data-ttu-id="a821e-118">Selezionare il modello **GitHubWebHook** per il linguaggio desiderato.</span><span class="sxs-lookup"><span data-stu-id="a821e-118">Select the **GitHub WebHook** template for your desired language.</span></span> <span data-ttu-id="a821e-119">**Assegnare un nome alla funzione** e quindi selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="a821e-119">**Name your function**, then select **Create**.</span></span>

     ![Creare una funzione attivata da webhook GitHub nel portale di Azure](./media/functions-create-github-webhook-triggered-function/functions-create-github-webhook-trigger.png) 

3. <span data-ttu-id="a821e-121">Nella nuova funzione fare clic su **</> Get function URL** (Ottieni URL funzione) e quindi copiare e salvare i valori.</span><span class="sxs-lookup"><span data-stu-id="a821e-121">In your new function, click **</> Get function URL**, then copy and save the values.</span></span> <span data-ttu-id="a821e-122">Eseguire la stessa operazione per **</> Recupera segreto GitHub**.</span><span class="sxs-lookup"><span data-stu-id="a821e-122">Do the same thing for **</> Get GitHub secret**.</span></span> <span data-ttu-id="a821e-123">Questi valori servono per configurare il webhook in GitHub.</span><span class="sxs-lookup"><span data-stu-id="a821e-123">You use these values to configure the webhook in GitHub.</span></span>

    ![Esaminare il codice funzione](./media/functions-create-github-webhook-triggered-function/functions-copy-function-url-github-secret.png)

<span data-ttu-id="a821e-125">Viene successivamente creato un webhook nel repository GitHub.</span><span class="sxs-lookup"><span data-stu-id="a821e-125">Next, you create a webhook in your GitHub repository.</span></span>

## <a name="configure-the-webhook"></a><span data-ttu-id="a821e-126">Configurare il webhook</span><span class="sxs-lookup"><span data-stu-id="a821e-126">Configure the webhook</span></span>

1. <span data-ttu-id="a821e-127">In GitHub passare a un repository di cui si è proprietari.</span><span class="sxs-lookup"><span data-stu-id="a821e-127">In GitHub, navigate to a repository that you own.</span></span> <span data-ttu-id="a821e-128">È possibile usare anche qualsiasi repository biforcato.</span><span class="sxs-lookup"><span data-stu-id="a821e-128">You can also use any repository that you have forked.</span></span> <span data-ttu-id="a821e-129">Se è necessario creare una copia tramite fork di un repository, usare <https://github.com/Azure-Samples/functions-quickstart>.</span><span class="sxs-lookup"><span data-stu-id="a821e-129">If you need to fork a repository, use <https://github.com/Azure-Samples/functions-quickstart>.</span></span>

1. <span data-ttu-id="a821e-130">Fare clic su **Impostazioni**, quindi su **Webhook** e infine su **Aggiungi webhook**.</span><span class="sxs-lookup"><span data-stu-id="a821e-130">Click **Settings**, then click **Webhooks**, and  **Add webhook**.</span></span>

    ![Aggiungere un webhook di GitHub](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-2.png)

1. <span data-ttu-id="a821e-132">Usare le impostazioni come indicato nella tabella e quindi fare clic su **Add webhook** (Aggiungi webhook).</span><span class="sxs-lookup"><span data-stu-id="a821e-132">Use settings as specified in the table, then click **Add webhook**.</span></span>

    ![Impostare l'URL del webhook e il segreto](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-3.png)

| <span data-ttu-id="a821e-134">Impostazione</span><span class="sxs-lookup"><span data-stu-id="a821e-134">Setting</span></span> | <span data-ttu-id="a821e-135">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="a821e-135">Suggested value</span></span> | <span data-ttu-id="a821e-136">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a821e-136">Description</span></span> |
|---|---|---|
| <span data-ttu-id="a821e-137">**Payload URL** (URL payload)</span><span class="sxs-lookup"><span data-stu-id="a821e-137">**Payload URL**</span></span> | <span data-ttu-id="a821e-138">Valore copiato</span><span class="sxs-lookup"><span data-stu-id="a821e-138">Copied value</span></span> | <span data-ttu-id="a821e-139">Usare il valore restituito da **</> Get function URL** (Ottieni URL funzione).</span><span class="sxs-lookup"><span data-stu-id="a821e-139">Use the value returned by  **</> Get function URL**.</span></span> |
| <span data-ttu-id="a821e-140">**Segreto**</span><span class="sxs-lookup"><span data-stu-id="a821e-140">**Secret**</span></span>   | <span data-ttu-id="a821e-141">Valore copiato</span><span class="sxs-lookup"><span data-stu-id="a821e-141">Copied value</span></span> | <span data-ttu-id="a821e-142">Usare il valore restituito da **</> Get GitHub secret** (Ottieni segreto GitHub).</span><span class="sxs-lookup"><span data-stu-id="a821e-142">Use the value returned by  **</> Get GitHub secret**.</span></span> |
| <span data-ttu-id="a821e-143">**Tipo contenuto**</span><span class="sxs-lookup"><span data-stu-id="a821e-143">**Content type**</span></span> | <span data-ttu-id="a821e-144">application/json</span><span class="sxs-lookup"><span data-stu-id="a821e-144">application/json</span></span> | <span data-ttu-id="a821e-145">La funzione prevede un payload JSON.</span><span class="sxs-lookup"><span data-stu-id="a821e-145">The function expects a JSON payload.</span></span> |
| <span data-ttu-id="a821e-146">Trigger di evento</span><span class="sxs-lookup"><span data-stu-id="a821e-146">Event triggers</span></span> | <span data-ttu-id="a821e-147">Selezione di singoli eventi</span><span class="sxs-lookup"><span data-stu-id="a821e-147">Let me select individual events</span></span> | <span data-ttu-id="a821e-148">Attivazione solo in caso di eventi di commento al problema.</span><span class="sxs-lookup"><span data-stu-id="a821e-148">We only want to trigger on issue comment events.</span></span>  |
| | <span data-ttu-id="a821e-149">Commento al problema</span><span class="sxs-lookup"><span data-stu-id="a821e-149">Issue comment</span></span> |  |

<span data-ttu-id="a821e-150">Il webhook ora è configurato per attivare la funzione quando un nuovo commento al problema viene aggiunto.</span><span class="sxs-lookup"><span data-stu-id="a821e-150">Now, the webhook is configured to trigger your function when a new issue comment is added.</span></span>

## <a name="test-the-function"></a><span data-ttu-id="a821e-151">Testare la funzione</span><span class="sxs-lookup"><span data-stu-id="a821e-151">Test the function</span></span>

1. <span data-ttu-id="a821e-152">Nel repository GitHub aprire la scheda **Issues** (Problemi) in una nuova finestra del browser.</span><span class="sxs-lookup"><span data-stu-id="a821e-152">In your GitHub repository, open the **Issues** tab in a new browser window.</span></span>

1. <span data-ttu-id="a821e-153">Nella nuova finestra fare clic su **Nuovo problema**, digitare un titolo e quindi fare clic su **Submit new issue** (Invia nuovo problema).</span><span class="sxs-lookup"><span data-stu-id="a821e-153">In the new window, click **New Issue**, type a title, and then click **Submit new issue**.</span></span>

1. <span data-ttu-id="a821e-154">Nel problema, digitare un commento e fare clic su **Comment (Commento)**.</span><span class="sxs-lookup"><span data-stu-id="a821e-154">In the issue, type a comment and click **Comment**.</span></span>

    ![Aggiungere un commento al problema GitHub.](./media/functions-create-github-webhook-triggered-function/functions-github-webhook-add-comment.png)

1. <span data-ttu-id="a821e-156">Tornare al portale e visualizzare i log.</span><span class="sxs-lookup"><span data-stu-id="a821e-156">Go back to the portal and view the logs.</span></span> <span data-ttu-id="a821e-157">Verrà visualizzata una voce di traccia con il nuovo testo del commento.</span><span class="sxs-lookup"><span data-stu-id="a821e-157">You should see a trace entry with the new comment text.</span></span>

     ![Visualizzare il testo del commento nei log.](./media/functions-create-github-webhook-triggered-function/function-app-view-logs.png)

## <a name="clean-up-resources"></a><span data-ttu-id="a821e-159">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="a821e-159">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="a821e-160">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a821e-160">Next steps</span></span>

<span data-ttu-id="a821e-161">È stata creata una funzione che viene eseguita quando viene ricevuta una richiesta da un webhook GitHub.</span><span class="sxs-lookup"><span data-stu-id="a821e-161">You have created a function that runs when a request is received from a GitHub webhook.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="a821e-162">Per altre informazioni sui trigger webhook, vedere [Associazioni HTTP e webhook in Funzioni di Azure](functions-bindings-http-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="a821e-162">For more information about webhook triggers, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span>
