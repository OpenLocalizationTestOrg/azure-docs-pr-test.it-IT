---
title: una funzione che viene eseguito in una pianificazione in Azure aaaCreate | Documenti Microsoft
description: Informazioni su come toocreate in Azure che esegue una funzione basato su una pianificazione definita.
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: ba50ee47-58e0-4972-b67b-828f2dc48701
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 793b06a65a154466dfd4c121bcc88082227cd597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-in-azure-that-is-triggered-by-a-timer"></a><span data-ttu-id="b5de9-103">Creare una funzione in Azure attivata da un timer</span><span class="sxs-lookup"><span data-stu-id="b5de9-103">Create a function in Azure that is triggered by a timer</span></span>

<span data-ttu-id="b5de9-104">Informazioni su come toouse Azure funzioni toocreate una funzione che viene eseguito in base una pianificazione definita.</span><span class="sxs-lookup"><span data-stu-id="b5de9-104">Learn how toouse Azure Functions toocreate a function that runs based a schedule that you define.</span></span>

![Creare app di funzione in hello portale di Azure](./media/functions-create-scheduled-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="b5de9-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b5de9-106">Prerequisites</span></span>

<span data-ttu-id="b5de9-107">toocomplete questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="b5de9-107">toocomplete this tutorial:</span></span>

+ <span data-ttu-id="b5de9-108">Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="b5de9-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="b5de9-109">Creare un'app per le funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="b5de9-109">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![App per le funzioni creata correttamente.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="b5de9-111">Creare quindi una funzione in hello nuova funzione app.</span><span class="sxs-lookup"><span data-stu-id="b5de9-111">Next, you create a function in hello new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-timer-triggered-function"></a><span data-ttu-id="b5de9-112">Creare una funzione attivata da un timer</span><span class="sxs-lookup"><span data-stu-id="b5de9-112">Create a timer triggered function</span></span>

1. <span data-ttu-id="b5de9-113">Espandere l'applicazione di funzione e fare clic su hello  **+**  accanto troppo**funzioni**.</span><span class="sxs-lookup"><span data-stu-id="b5de9-113">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="b5de9-114">Se si tratta di hello prima funzione di app di funzione, selezionare **funzione personalizzata**.</span><span class="sxs-lookup"><span data-stu-id="b5de9-114">If this is hello first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="b5de9-115">Consente di visualizzare il set completo di hello dei modelli di funzione.</span><span class="sxs-lookup"><span data-stu-id="b5de9-115">This displays hello complete set of function templates.</span></span>

    ![Pagina di avvio rapido di funzioni in hello portale di Azure](./media/functions-create-scheduled-function/add-first-function.png)

2. <span data-ttu-id="b5de9-117">Seleziona hello **TimerTrigger** modello per la lingua desiderata.</span><span class="sxs-lookup"><span data-stu-id="b5de9-117">Select hello **TimerTrigger** template for your desired language.</span></span> <span data-ttu-id="b5de9-118">Utilizzare quindi le impostazioni di hello come specificato nella tabella hello:</span><span class="sxs-lookup"><span data-stu-id="b5de9-118">Then use hello settings as specified in hello table:</span></span>

    ![Creare una funzione di timer attivato in hello portale di Azure.](./media/functions-create-scheduled-function/functions-create-timer-trigger.png)

    | <span data-ttu-id="b5de9-120">Impostazione</span><span class="sxs-lookup"><span data-stu-id="b5de9-120">Setting</span></span> | <span data-ttu-id="b5de9-121">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="b5de9-121">Suggested value</span></span> | <span data-ttu-id="b5de9-122">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b5de9-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="b5de9-123">**Dare un nome alla funzione**</span><span class="sxs-lookup"><span data-stu-id="b5de9-123">**Name your function**</span></span> | <span data-ttu-id="b5de9-124">TimerTriggerCSharp1</span><span class="sxs-lookup"><span data-stu-id="b5de9-124">TimerTriggerCSharp1</span></span> | <span data-ttu-id="b5de9-125">Definisce il nome di hello della funzione di timer attivato.</span><span class="sxs-lookup"><span data-stu-id="b5de9-125">Defines hello name of your timer triggered function.</span></span> |
    | <span data-ttu-id="b5de9-126">**[Pianificazione](http://en.wikipedia.org/wiki/Cron#CRON_expression)**</span><span class="sxs-lookup"><span data-stu-id="b5de9-126">**[Schedule](http://en.wikipedia.org/wiki/Cron#CRON_expression)**</span></span> | <span data-ttu-id="b5de9-127">0 \*/1 \* \* \* \*</span><span class="sxs-lookup"><span data-stu-id="b5de9-127">0 \*/1 \* \* \* \*</span></span> | <span data-ttu-id="b5de9-128">Un campo sei [espressione CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression) toorun la funzione che pianifica ogni minuto.</span><span class="sxs-lookup"><span data-stu-id="b5de9-128">A six field [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression) that schedules your function toorun every minute.</span></span> |

2. <span data-ttu-id="b5de9-129">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="b5de9-129">Click **Create**.</span></span> <span data-ttu-id="b5de9-130">Viene creata una funzione nel linguaggio scelto che verrà eseguita ogni minuto.</span><span class="sxs-lookup"><span data-stu-id="b5de9-130">A function is created in your chosen language that runs every minute.</span></span>

3. <span data-ttu-id="b5de9-131">Verificare l'esecuzione visualizzando le informazioni di traccia toohello log scritte.</span><span class="sxs-lookup"><span data-stu-id="b5de9-131">Verify execution by viewing trace information written toohello logs.</span></span>

    ![Funzioni di accesso Visualizzatore hello portale di Azure.](./media/functions-create-scheduled-function/functions-timer-trigger-view-logs2.png)

<span data-ttu-id="b5de9-133">A questo punto, è possibile modificare la pianificazione della funzione hello in modo che venga eseguito meno frequentemente, ad esempio una volta ogni ora.</span><span class="sxs-lookup"><span data-stu-id="b5de9-133">Now, you can change hello function's schedule so that it runs less often, such as once every hour.</span></span> 

## <a name="update-hello-timer-schedule"></a><span data-ttu-id="b5de9-134">Pianificazione di aggiornamento hello timer</span><span class="sxs-lookup"><span data-stu-id="b5de9-134">Update hello timer schedule</span></span>

1. <span data-ttu-id="b5de9-135">Espandere la funzione e fare clic su **Integrazione**.</span><span class="sxs-lookup"><span data-stu-id="b5de9-135">Expand your function and click **Integrate**.</span></span> <span data-ttu-id="b5de9-136">Questo è possibile definire l'input e output associazioni per la funzione e inoltre impostare la pianificazione hello.</span><span class="sxs-lookup"><span data-stu-id="b5de9-136">This is where you define input and output bindings for your function and also set hello schedule.</span></span> 

2. <span data-ttu-id="b5de9-137">Nel campo **Pianificazione** immettere il nuovo valore `0 0 */1 * * *` e quindi fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="b5de9-137">Enter a new **Schedule** value of `0 0 */1 * * *`, and then click **Save**.</span></span>  

![Funzioni di aggiornare la pianificazione di timer in hello portale di Azure.](./media/functions-create-scheduled-function/functions-timer-trigger-change-schedule.png)

<span data-ttu-id="b5de9-139">È ora disponibile una funzione che viene eseguita ogni ora.</span><span class="sxs-lookup"><span data-stu-id="b5de9-139">You now have a function that runs once every hour.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="b5de9-140">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="b5de9-140">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="b5de9-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b5de9-141">Next steps</span></span>

<span data-ttu-id="b5de9-142">È stata creata una funzione eseguita in base a una pianificazione.</span><span class="sxs-lookup"><span data-stu-id="b5de9-142">You have created a function that runs based on a schedule.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="b5de9-143">Per altre informazioni sui trigger timer, vedere [Pianificare l'esecuzione di codice con Funzioni di Azure](functions-bindings-timer.md).</span><span class="sxs-lookup"><span data-stu-id="b5de9-143">For more information timer triggers, see [Schedule code execution with Azure Functions](functions-bindings-timer.md).</span></span>