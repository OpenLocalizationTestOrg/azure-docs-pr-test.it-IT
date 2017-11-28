---
title: Creare la prima funzione nel portale di Azure | Microsoft Docs
description: Informazioni su come creare la prima funzione di Azure per l'esecuzione senza server tramite il portale di Azure.
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 96cf87b9-8db6-41a8-863a-abb828e3d06d
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/07/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 3ec1f278f21d89782137625aff200f07f15fd9fb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-function-in-the-azure-portal"></a><span data-ttu-id="4b727-103">Creare la prima funzione nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="4b727-103">Create your first function in the Azure portal</span></span>

<span data-ttu-id="4b727-104">Funzioni di Azure consente di eseguire il codice in un ambiente senza server senza dover prima creare una macchina virtuale o pubblicare un'applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="4b727-104">Azure Functions lets you execute your code in a serverless environment without having to first create a VM or publish a web application.</span></span> <span data-ttu-id="4b727-105">Questo argomento fornisce informazioni su come usare Funzioni per creare una funzione di benvenuto nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4b727-105">In this topic, learn how to use Functions to create a "hello world" function in the Azure portal.</span></span>

![Creare un'app per le funzioni nel portale di Azure](./media/functions-create-first-azure-function/function-app-in-portal-editor.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="log-in-to-azure"></a><span data-ttu-id="4b727-107">Accedere ad Azure</span><span class="sxs-lookup"><span data-stu-id="4b727-107">Log in to Azure</span></span>

<span data-ttu-id="4b727-108">Accedere al [Portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4b727-108">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="4b727-109">Creare un'app per le funzioni</span><span class="sxs-lookup"><span data-stu-id="4b727-109">Create a function app</span></span>

<span data-ttu-id="4b727-110">Per ospitare l'esecuzione delle funzioni è necessaria un'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="4b727-110">You must have a function app to host the execution of your functions.</span></span> <span data-ttu-id="4b727-111">Un'app per le funzioni consente di raggruppare le funzioni come un'unità logica per semplificare la gestione, la distribuzione e la condivisione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="4b727-111">A function app lets you group functions as a logic unit for easier management, deployment, and sharing of resources.</span></span> 

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

<span data-ttu-id="4b727-112">Si creerà ora una funzione nella nuova app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="4b727-112">Next, you create a function in the new function app.</span></span>

## <span data-ttu-id="4b727-113"><a name="create-function"></a>Creare una funzione attivata tramite HTTP</span><span class="sxs-lookup"><span data-stu-id="4b727-113"><a name="create-function"></a>Create an HTTP triggered function</span></span>

1. <span data-ttu-id="4b727-114">Espandere la nuova app per le funzioni e quindi fare clic sul pulsante **+** accanto a **Funzioni**.</span><span class="sxs-lookup"><span data-stu-id="4b727-114">Expand your new function app, then click the **+** button next to **Functions**.</span></span>

2.  <span data-ttu-id="4b727-115">Nella pagina **Iniziare rapidamente con una funzione preconfezionata** selezionare **Webhook e API**, **scegliere un linguaggio** per la funzione e fare clic su **Creare questa funzione**.</span><span class="sxs-lookup"><span data-stu-id="4b727-115">In the **Get started quickly** page, select **WebHook + API**, **Choose a language** for your function, and click **Create this function**.</span></span> 
   
    ![Guida di avvio rapido di Funzioni nel portale di Azure.](./media/functions-create-first-azure-function/function-app-quickstart-node-webhook.png)

<span data-ttu-id="4b727-117">Viene creata una funzione nel linguaggio prescelto usando il modello per una funzione attivata tramite HTTP.</span><span class="sxs-lookup"><span data-stu-id="4b727-117">A function is created in your chosen language using the template for an HTTP triggered function.</span></span> <span data-ttu-id="4b727-118">È possibile eseguire la nuova funzione inviando una richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="4b727-118">You can run the new function by sending an HTTP request.</span></span>

## <a name="test-the-function"></a><span data-ttu-id="4b727-119">Testare la funzione</span><span class="sxs-lookup"><span data-stu-id="4b727-119">Test the function</span></span>

1. <span data-ttu-id="4b727-120">Nella nuova funzione fare clic su **</> Recupera URL della funzione**, selezionare **predefinito (tasto funzione)** e quindi fare clic su **Copia**.</span><span class="sxs-lookup"><span data-stu-id="4b727-120">In your new function, click **</> Get function URL**, select **default (Function key)**, and then click **Copy**.</span></span> 

    ![Creare l'URL della funzione dal portale di Azure](./media/functions-create-first-azure-function/function-app-develop-tab-testing.png)

2. <span data-ttu-id="4b727-122">Incollare l'URL della funzione nella barra degli indirizzi del browser.</span><span class="sxs-lookup"><span data-stu-id="4b727-122">Paste the function URL into your browser's address bar.</span></span> <span data-ttu-id="4b727-123">Aggiungere la stringa di query `&name=<yourname>` all'URL e premere il tasto `Enter` per eseguire la richiesta.</span><span class="sxs-lookup"><span data-stu-id="4b727-123">Append the query string `&name=<yourname>` to this URL and press the `Enter` key on your keyboard to execute the request.</span></span> <span data-ttu-id="4b727-124">L'esempio seguente riporta la risposta restituita dalla funzione nel browser Edge:</span><span class="sxs-lookup"><span data-stu-id="4b727-124">The following is an example of the response returned by the function in the Edge browser:</span></span>

    ![Risposta della funzione nel browser.](./media/functions-create-first-azure-function/function-app-browser-testing.png)

    <span data-ttu-id="4b727-126">L'URL della richiesta include una chiave necessaria per impostazione predefinita per accedere a una funzione tramite HTTP.</span><span class="sxs-lookup"><span data-stu-id="4b727-126">The request URL includes a key that is required, by default, to access your function over HTTP.</span></span>   

3. <span data-ttu-id="4b727-127">Quando viene eseguita la funzione, vengono scritte nei log informazioni di traccia.</span><span class="sxs-lookup"><span data-stu-id="4b727-127">When your function runs, trace information is written to the logs.</span></span> <span data-ttu-id="4b727-128">Per visualizzare l'output di traccia dell'esecuzione precedente, tornare alla funzione nel portale e fare clic sulla freccia verso l'alto nella parte inferiore della schermata per espandere **Log**.</span><span class="sxs-lookup"><span data-stu-id="4b727-128">To see the trace output from the previous execution, return to your function in the portal and click the up arrow at the bottom of the screen to expand **Logs**.</span></span> 

   ![Visualizzatore log di Funzioni nel portale di Azure.](./media/functions-create-first-azure-function/function-view-logs.png)

## <a name="clean-up-resources"></a><span data-ttu-id="4b727-130">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="4b727-130">Clean up resources</span></span>

[!INCLUDE [Clean up resources](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="4b727-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4b727-131">Next steps</span></span>

<span data-ttu-id="4b727-132">È stata creata un'app per le funzioni con una semplice funzione attivata tramite HTTP.</span><span class="sxs-lookup"><span data-stu-id="4b727-132">You have created a function app with a simple HTTP triggered function.</span></span>  

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="4b727-133">Per altre informazioni rivedere [Binding HTTP e webhook in Funzioni di Azure](functions-bindings-http-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="4b727-133">For more information, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span>



