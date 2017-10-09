---
title: la prima funzione dal portale di Azure hello aaaCreate | Documenti Microsoft
description: Informazioni su come toocreate di Azure prima funzione per l'esecuzione senza tramite hello portale di Azure.
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
ms.openlocfilehash: 84283d7d4bc6015061946af4589f9a70ae61f36b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-in-hello-azure-portal"></a><span data-ttu-id="0ef72-103">Creare la prima funzione in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="0ef72-103">Create your first function in hello Azure portal</span></span>

<span data-ttu-id="0ef72-104">Funzioni di Azure consente di eseguire il codice in un ambiente senza server senza dover toofirst crea una macchina virtuale o si pubblica un'applicazione web.</span><span class="sxs-lookup"><span data-stu-id="0ef72-104">Azure Functions lets you execute your code in a serverless environment without having toofirst create a VM or publish a web application.</span></span> <span data-ttu-id="0ef72-105">In questo argomento, informazioni su come toouse funzioni toocreate una funzione di "hello world" nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="0ef72-105">In this topic, learn how toouse Functions toocreate a "hello world" function in hello Azure portal.</span></span>

![Creare app di funzione in hello portale di Azure](./media/functions-create-first-azure-function/function-app-in-portal-editor.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="log-in-tooazure"></a><span data-ttu-id="0ef72-107">Accedi tooAzure</span><span class="sxs-lookup"><span data-stu-id="0ef72-107">Log in tooAzure</span></span>

<span data-ttu-id="0ef72-108">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0ef72-108">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="0ef72-109">Creare un'app per le funzioni</span><span class="sxs-lookup"><span data-stu-id="0ef72-109">Create a function app</span></span>

<span data-ttu-id="0ef72-110">È necessario disporre di un'esecuzione di hello toohost app funzione delle funzioni.</span><span class="sxs-lookup"><span data-stu-id="0ef72-110">You must have a function app toohost hello execution of your functions.</span></span> <span data-ttu-id="0ef72-111">Un'app per le funzioni consente di raggruppare le funzioni come un'unità logica per semplificare la gestione, la distribuzione e la condivisione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="0ef72-111">A function app lets you group functions as a logic unit for easier management, deployment, and sharing of resources.</span></span> 

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

<span data-ttu-id="0ef72-112">Creare quindi una funzione in hello nuova funzione app.</span><span class="sxs-lookup"><span data-stu-id="0ef72-112">Next, you create a function in hello new function app.</span></span>

## <span data-ttu-id="0ef72-113"><a name="create-function"></a>Creare una funzione attivata tramite HTTP</span><span class="sxs-lookup"><span data-stu-id="0ef72-113"><a name="create-function"></a>Create an HTTP triggered function</span></span>

1. <span data-ttu-id="0ef72-114">Espandere la nuova app di funzione, quindi fare clic su hello  **+**  accanto troppo**funzioni**.</span><span class="sxs-lookup"><span data-stu-id="0ef72-114">Expand your new function app, then click hello **+** button next too**Functions**.</span></span>

2.  <span data-ttu-id="0ef72-115">In hello **iniziare rapidamente** selezionare **WebHook + API**, **scegliere una lingua** per la funzione, fare clic su **creare questa funzione** .</span><span class="sxs-lookup"><span data-stu-id="0ef72-115">In hello **Get started quickly** page, select **WebHook + API**, **Choose a language** for your function, and click **Create this function**.</span></span> 
   
    ![Funzioni delle Guide rapide in hello portale di Azure.](./media/functions-create-first-azure-function/function-app-quickstart-node-webhook.png)

<span data-ttu-id="0ef72-117">Viene creata una funzione nella lingua scelta, utilizzando il modello di hello per una funzione di attivazione HTTP.</span><span class="sxs-lookup"><span data-stu-id="0ef72-117">A function is created in your chosen language using hello template for an HTTP triggered function.</span></span> <span data-ttu-id="0ef72-118">È possibile eseguire una nuova funzione hello inviando una richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="0ef72-118">You can run hello new function by sending an HTTP request.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="0ef72-119">Funzione hello test</span><span class="sxs-lookup"><span data-stu-id="0ef72-119">Test hello function</span></span>

1. <span data-ttu-id="0ef72-120">Nella nuova funzione fare clic su **</> Recupera URL della funzione**, selezionare **predefinito (tasto funzione)** e quindi fare clic su **Copia**.</span><span class="sxs-lookup"><span data-stu-id="0ef72-120">In your new function, click **</> Get function URL**, select **default (Function key)**, and then click **Copy**.</span></span> 

    ![Copiare l'URL funzione hello da hello portale di Azure](./media/functions-create-first-azure-function/function-app-develop-tab-testing.png)

2. <span data-ttu-id="0ef72-122">Incollare l'URL funzione hello nella barra degli indirizzi del browser.</span><span class="sxs-lookup"><span data-stu-id="0ef72-122">Paste hello function URL into your browser's address bar.</span></span> <span data-ttu-id="0ef72-123">Aggiungere la stringa di query hello `&name=<yourname>` toothis URL e premere hello `Enter` chiave della richiesta di hello tooexecute tastiera.</span><span class="sxs-lookup"><span data-stu-id="0ef72-123">Append hello query string `&name=<yourname>` toothis URL and press hello `Enter` key on your keyboard tooexecute hello request.</span></span> <span data-ttu-id="0ef72-124">Hello Ecco un esempio di risposta hello restituito dalla funzione hello nel browser Edge hello:</span><span class="sxs-lookup"><span data-stu-id="0ef72-124">hello following is an example of hello response returned by hello function in hello Edge browser:</span></span>

    ![Risposta della funzione nel browser hello.](./media/functions-create-first-azure-function/function-app-browser-testing.png)

    <span data-ttu-id="0ef72-126">richiesta di Hello URL include una chiave che è necessario, per impostazione predefinita, tooaccess la funzione su HTTP.</span><span class="sxs-lookup"><span data-stu-id="0ef72-126">hello request URL includes a key that is required, by default, tooaccess your function over HTTP.</span></span>   

3. <span data-ttu-id="0ef72-127">Quando viene eseguita la funzione, le informazioni di traccia viene scritto toohello log.</span><span class="sxs-lookup"><span data-stu-id="0ef72-127">When your function runs, trace information is written toohello logs.</span></span> <span data-ttu-id="0ef72-128">output di traccia toosee hello in seguito all'esecuzione precedente hello, restituire la funzione tooyour nel portale di hello e fare clic su hello freccia nella parte inferiore di hello di hello schermata tooexpand **log**.</span><span class="sxs-lookup"><span data-stu-id="0ef72-128">toosee hello trace output from hello previous execution, return tooyour function in hello portal and click hello up arrow at hello bottom of hello screen tooexpand **Logs**.</span></span> 

   ![Funzioni di accesso Visualizzatore hello portale di Azure.](./media/functions-create-first-azure-function/function-view-logs.png)

## <a name="clean-up-resources"></a><span data-ttu-id="0ef72-130">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="0ef72-130">Clean up resources</span></span>

[!INCLUDE [Clean up resources](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="0ef72-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0ef72-131">Next steps</span></span>

<span data-ttu-id="0ef72-132">È stata creata un'app per le funzioni con una semplice funzione attivata tramite HTTP.</span><span class="sxs-lookup"><span data-stu-id="0ef72-132">You have created a function app with a simple HTTP triggered function.</span></span>  

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="0ef72-133">Per altre informazioni rivedere [Binding HTTP e webhook in Funzioni di Azure](functions-bindings-http-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="0ef72-133">For more information, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span>



