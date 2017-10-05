---
title: Creare una funzione che viene eseguita in una pianificazione | Microsoft Docs
description: Informazioni su come creare una funzione in Azure eseguita in base a una pianificazione definita.
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
ms.openlocfilehash: 03cc5e71e8eb20002cf58e713fc0fc92a9129874
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-in-azure-that-is-triggered-by-a-timer"></a><span data-ttu-id="1a9e0-103">Creare una funzione in Azure attivata da un timer</span><span class="sxs-lookup"><span data-stu-id="1a9e0-103">Create a function in Azure that is triggered by a timer</span></span>

<span data-ttu-id="1a9e0-104">Informazioni su come usare Funzioni di Azure per creare una funzione eseguita in base a una pianificazione definita.</span><span class="sxs-lookup"><span data-stu-id="1a9e0-104">Learn how to use Azure Functions to create a function that runs based a schedule that you define.</span></span>

![Creare un'app per le funzioni nel portale di Azure](./media/functions-create-scheduled-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="1a9e0-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1a9e0-106">Prerequisites</span></span>

<span data-ttu-id="1a9e0-107">Per completare questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="1a9e0-107">To complete this tutorial:</span></span>

+ <span data-ttu-id="1a9e0-108">Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="1a9e0-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="1a9e0-109">Creare un'app per le funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="1a9e0-109">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![App per le funzioni creata correttamente.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="1a9e0-111">Si creerà ora una funzione nella nuova app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="1a9e0-111">Next, you create a function in the new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-timer-triggered-function"></a><span data-ttu-id="1a9e0-112">Creare una funzione attivata da un timer</span><span class="sxs-lookup"><span data-stu-id="1a9e0-112">Create a timer triggered function</span></span>

1. <span data-ttu-id="1a9e0-113">Espandere l'app per le funzioni e fare clic sul pulsante **+** accanto a **Funzioni**.</span><span class="sxs-lookup"><span data-stu-id="1a9e0-113">Expand your function app and click the **+** button next to **Functions**.</span></span> <span data-ttu-id="1a9e0-114">Se questa è la prima funzione nell'app per le funzioni, selezionare **Funzione personalizzata**.</span><span class="sxs-lookup"><span data-stu-id="1a9e0-114">If this is the first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="1a9e0-115">Verrà visualizzato il set completo di modelli di funzione.</span><span class="sxs-lookup"><span data-stu-id="1a9e0-115">This displays the complete set of function templates.</span></span>

    ![Pagina della guida introduttiva di Funzioni nel portale di Azure](./media/functions-create-scheduled-function/add-first-function.png)

2. <span data-ttu-id="1a9e0-117">Selezionare il modello **TimerTrigger** per la lingua desiderata.</span><span class="sxs-lookup"><span data-stu-id="1a9e0-117">Select the **TimerTrigger** template for your desired language.</span></span> <span data-ttu-id="1a9e0-118">Usare quindi le impostazioni specificate nella tabella:</span><span class="sxs-lookup"><span data-stu-id="1a9e0-118">Then use the settings as specified in the table:</span></span>

    ![Creare una funzione attivata da un timer nel portale di Azure.](./media/functions-create-scheduled-function/functions-create-timer-trigger.png)

    | <span data-ttu-id="1a9e0-120">Impostazione</span><span class="sxs-lookup"><span data-stu-id="1a9e0-120">Setting</span></span> | <span data-ttu-id="1a9e0-121">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="1a9e0-121">Suggested value</span></span> | <span data-ttu-id="1a9e0-122">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1a9e0-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="1a9e0-123">**Dare un nome alla funzione**</span><span class="sxs-lookup"><span data-stu-id="1a9e0-123">**Name your function**</span></span> | <span data-ttu-id="1a9e0-124">TimerTriggerCSharp1</span><span class="sxs-lookup"><span data-stu-id="1a9e0-124">TimerTriggerCSharp1</span></span> | <span data-ttu-id="1a9e0-125">Definisce il nome della funzione attivata dal timer.</span><span class="sxs-lookup"><span data-stu-id="1a9e0-125">Defines the name of your timer triggered function.</span></span> |
    | <span data-ttu-id="1a9e0-126">**[Pianificazione](http://en.wikipedia.org/wiki/Cron#CRON_expression)**</span><span class="sxs-lookup"><span data-stu-id="1a9e0-126">**[Schedule](http://en.wikipedia.org/wiki/Cron#CRON_expression)**</span></span> | <span data-ttu-id="1a9e0-127">0 \*/1 \* \* \* \*</span><span class="sxs-lookup"><span data-stu-id="1a9e0-127">0 \*/1 \* \* \* \*</span></span> | <span data-ttu-id="1a9e0-128">[Espressione CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression) a sei campi che pianifica la funzione in modo che venga eseguita ogni minuto.</span><span class="sxs-lookup"><span data-stu-id="1a9e0-128">A six field [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression) that schedules your function to run every minute.</span></span> |

2. <span data-ttu-id="1a9e0-129">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="1a9e0-129">Click **Create**.</span></span> <span data-ttu-id="1a9e0-130">Viene creata una funzione nel linguaggio scelto che verrà eseguita ogni minuto.</span><span class="sxs-lookup"><span data-stu-id="1a9e0-130">A function is created in your chosen language that runs every minute.</span></span>

3. <span data-ttu-id="1a9e0-131">Verificare l'esecuzione visualizzando le informazioni di traccia scritte nei log.</span><span class="sxs-lookup"><span data-stu-id="1a9e0-131">Verify execution by viewing trace information written to the logs.</span></span>

    ![Visualizzatore log di Funzioni nel portale di Azure.](./media/functions-create-scheduled-function/functions-timer-trigger-view-logs2.png)

<span data-ttu-id="1a9e0-133">È possibile ora modificare la pianificazione della funzione in modo che venga eseguita con meno frequenza, ad esempio ogni ora.</span><span class="sxs-lookup"><span data-stu-id="1a9e0-133">Now, you can change the function's schedule so that it runs less often, such as once every hour.</span></span> 

## <a name="update-the-timer-schedule"></a><span data-ttu-id="1a9e0-134">Aggiornare la pianificazione del timer</span><span class="sxs-lookup"><span data-stu-id="1a9e0-134">Update the timer schedule</span></span>

1. <span data-ttu-id="1a9e0-135">Espandere la funzione e fare clic su **Integrazione**.</span><span class="sxs-lookup"><span data-stu-id="1a9e0-135">Expand your function and click **Integrate**.</span></span> <span data-ttu-id="1a9e0-136">È a questo punto che si definiscono i binding di input e di output e si imposta la pianificazione.</span><span class="sxs-lookup"><span data-stu-id="1a9e0-136">This is where you define input and output bindings for your function and also set the schedule.</span></span> 

2. <span data-ttu-id="1a9e0-137">Nel campo **Pianificazione** immettere il nuovo valore `0 0 */1 * * *` e quindi fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="1a9e0-137">Enter a new **Schedule** value of `0 0 */1 * * *`, and then click **Save**.</span></span>  

![Pianificazione del timer di aggiornamento di Funzioni nel portale di Azure.](./media/functions-create-scheduled-function/functions-timer-trigger-change-schedule.png)

<span data-ttu-id="1a9e0-139">È ora disponibile una funzione che viene eseguita ogni ora.</span><span class="sxs-lookup"><span data-stu-id="1a9e0-139">You now have a function that runs once every hour.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="1a9e0-140">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="1a9e0-140">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="1a9e0-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1a9e0-141">Next steps</span></span>

<span data-ttu-id="1a9e0-142">È stata creata una funzione eseguita in base a una pianificazione.</span><span class="sxs-lookup"><span data-stu-id="1a9e0-142">You have created a function that runs based on a schedule.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="1a9e0-143">Per altre informazioni sui trigger timer, vedere [Pianificare l'esecuzione di codice con Funzioni di Azure](functions-bindings-timer.md).</span><span class="sxs-lookup"><span data-stu-id="1a9e0-143">For more information timer triggers, see [Schedule code execution with Azure Functions](functions-bindings-timer.md).</span></span>