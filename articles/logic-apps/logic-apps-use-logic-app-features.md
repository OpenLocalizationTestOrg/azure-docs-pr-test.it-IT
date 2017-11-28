---
title: le condizioni e avviare i flussi di lavoro - App Azure per la logica di aaaAdd | Documenti Microsoft
description: Controllare l'esecuzione dei flussi di lavoro nelle app per la logica di Azure mediante l'aggiunta di logica condizionale, trigger, azioni e parametri.
author: stepsic-microsoft-com
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: e4e24de4-049a-4b3a-a14c-3bf3163287a8
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/28/2017
ms.author: LADocs; stepsic
ms.openlocfilehash: 76d5e44590ffa14cf70d7a93b99a241d286d555b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-logic-apps-features"></a><span data-ttu-id="81854-103">Usare le funzionalità delle app per la logica</span><span class="sxs-lookup"><span data-stu-id="81854-103">Use Logic Apps features</span></span>

<span data-ttu-id="81854-104">In un [argomento precedente](../logic-apps/logic-apps-create-a-logic-app.md) è stata creata la prima app per la logica.</span><span class="sxs-lookup"><span data-stu-id="81854-104">In a [previous topic](../logic-apps/logic-apps-create-a-logic-app.md), you created your first logic app.</span></span> <span data-ttu-id="81854-105">toocontrol flusso di lavoro logica dell'applicazione, è possibile specificare percorsi diversi per il toorun app logica e come troppo elaborare i dati in batch, le raccolte e matrici.</span><span class="sxs-lookup"><span data-stu-id="81854-105">toocontrol your logic app's workflow, you can specify different paths for your logic app toorun and how too process data in arrays, collections, and batches.</span></span> <span data-ttu-id="81854-106">È possibile includere questi elementi nel flusso di lavoro dell'app per la logica:</span><span class="sxs-lookup"><span data-stu-id="81854-106">You can include these elements in your logic app workflow:</span></span>

* <span data-ttu-id="81854-107">Le condizioni e le [istruzioni switch](../logic-apps/logic-apps-switch-case.md) consentono all'app per la logica di eseguire azioni diverse in base al fatto che vengano soddisfatte o meno condizioni specifiche.</span><span class="sxs-lookup"><span data-stu-id="81854-107">Conditions and [switch statements](../logic-apps/logic-apps-switch-case.md) let your logic app run different actions based on whether specific conditions are met.</span></span>

* <span data-ttu-id="81854-108">I [cicli](../logic-apps/logic-apps-loops-and-scopes.md) consentono di eseguire ripetutamente passaggi dell'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="81854-108">[Loops](../logic-apps/logic-apps-loops-and-scopes.md) let your logic app run steps repeatedly.</span></span> <span data-ttu-id="81854-109">Ad esempio, è possibile ripetere azioni su una matrice quando si usa un ciclo **For_each**.</span><span class="sxs-lookup"><span data-stu-id="81854-109">For example, you can repeat actions over an array when you use a **For_each** loop.</span></span> <span data-ttu-id="81854-110">Oppure è possibile ripetere azioni fino a quando non viene soddisfatta una condizione se si usa un ciclo **Until**.</span><span class="sxs-lookup"><span data-stu-id="81854-110">Or you can repeat actions until a condition is met when you use an **Until** loop.</span></span>

* <span data-ttu-id="81854-111">[Gli ambiti](../logic-apps/logic-apps-loops-and-scopes.md) consentono raggruppare serie di azioni, ad esempio, la gestione delle eccezioni tooimplement.</span><span class="sxs-lookup"><span data-stu-id="81854-111">[Scopes](../logic-apps/logic-apps-loops-and-scopes.md) let you group series of actions together, for example, tooimplement exception handling.</span></span>

* <span data-ttu-id="81854-112">[Scomposizione dei batch](../logic-apps/logic-apps-loops-and-scopes.md) consente di avviare i flussi di lavoro separati per gli elementi in una matrice quando si utilizza hello app logica **SplitOn** comando.</span><span class="sxs-lookup"><span data-stu-id="81854-112">[Debatching](../logic-apps/logic-apps-loops-and-scopes.md) lets your logic app start separate workflows for items in an array when you use hello **SplitOn** command.</span></span>

<span data-ttu-id="81854-113">Questo argomento introduce altri concetti per la compilazione dell'app per la logica:</span><span class="sxs-lookup"><span data-stu-id="81854-113">This topic introduces other concepts for building your logic app:</span></span>

* <span data-ttu-id="81854-114">Visualizzazione tooedit un'app esistente per la logica del codice</span><span class="sxs-lookup"><span data-stu-id="81854-114">Code view tooedit an existing logic app</span></span>
* <span data-ttu-id="81854-115">Opzioni per avviare un flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="81854-115">Options for starting a workflow</span></span>

## <a name="conditions-run-steps-only-after-meeting-a-condition"></a><span data-ttu-id="81854-116">Condizioni: eseguire i passaggi solo quando è soddisfatta una condizione</span><span class="sxs-lookup"><span data-stu-id="81854-116">Conditions: Run steps only after meeting a condition</span></span>

<span data-ttu-id="81854-117">toohave logica app eseguire passaggi solo quando i dati soddisfano criteri specifici, è possibile aggiungere una condizione che confronta i dati nel flusso di lavoro hello in campi specifici o valori.</span><span class="sxs-lookup"><span data-stu-id="81854-117">toohave your logic app run steps only when data meets specific criteria, you can add a condition that compares data in hello workflow against specific fields or values.</span></span>

<span data-ttu-id="81854-118">Si supponga, ad esempio, di avere un'app per la logica che invia troppi messaggi di posta elettronica per i post sul feed RSS di un sito Web.</span><span class="sxs-lookup"><span data-stu-id="81854-118">For example, suppose you have a logic app that sends you too many emails for posts on a website's RSS feed.</span></span> <span data-ttu-id="81854-119">È possibile aggiungere una condizione in modo che l'app logica invia posta elettronica solo quando Registra nuovo hello categoria specifica tooa appartiene.</span><span class="sxs-lookup"><span data-stu-id="81854-119">You can add a condition so that your logic app sends email only when hello new post belongs tooa specific category.</span></span>

1. <span data-ttu-id="81854-120">In hello [portale di Azure](https://portal.azure.com), trovare e aprire l'app logica nella finestra di progettazione logica App.</span><span class="sxs-lookup"><span data-stu-id="81854-120">In hello [Azure portal](https://portal.azure.com), find and open your logic app in Logic App Designer.</span></span>

2. <span data-ttu-id="81854-121">Aggiungere un percorso del flusso di lavoro toohello a condizione che si desidera.</span><span class="sxs-lookup"><span data-stu-id="81854-121">Add a condition toohello workflow location that you want.</span></span> 

   <span data-ttu-id="81854-122">condizione di hello tooadd tra i passaggi esistenti nel flusso di lavoro di hello logica app, spostare il puntatore di hello sulla freccia di hello in cui si desidera condizione hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="81854-122">tooadd hello condition between existing steps in hello logic app workflow, move hello pointer over hello arrow where you want tooadd hello condition.</span></span> 
   <span data-ttu-id="81854-123">Scegliere hello **segno** (**+**), quindi scegliere **aggiungere una condizione**.</span><span class="sxs-lookup"><span data-stu-id="81854-123">Choose hello **plus sign** (**+**), then choose **Add a condition**.</span></span> <span data-ttu-id="81854-124">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="81854-124">For example:</span></span>

   ![Aggiungi condizione toologic app](./media/logic-apps-use-logic-app-features/add-condition.png)

   > [!NOTE]
   > <span data-ttu-id="81854-126">Se si desidera tooadd una condizione alla fine di hello del flusso di lavoro corrente, toohello inferiore dell'app logica, quindi **+ nuovo passaggio**.</span><span class="sxs-lookup"><span data-stu-id="81854-126">If you want tooadd a condition at hello end of your current workflow, go toohello bottom of your logic app, and choose **+ New step**.</span></span>

3. <span data-ttu-id="81854-127">Ora definire la condizione hello.</span><span class="sxs-lookup"><span data-stu-id="81854-127">Now define hello condition.</span></span> <span data-ttu-id="81854-128">Specificare il campo di origine hello che si desidera tooevaluate, hello operazione tooperform e il valore di destinazione hello o un campo.</span><span class="sxs-lookup"><span data-stu-id="81854-128">Specify hello source field that you want tooevaluate, hello operation tooperform, and hello target value or field.</span></span> <span data-ttu-id="81854-129">tooadd esistente campi tooyour condizione, scegliere hello **elenco contenuto dinamico Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="81854-129">tooadd existing fields tooyour condition, choose from hello **Add dynamic content list**.</span></span>

   <span data-ttu-id="81854-130">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="81854-130">For example:</span></span>

   ![Modificare la condizione nella modalità di base](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode.png)

   <span data-ttu-id="81854-132">Di seguito è la condizione completa hello:</span><span class="sxs-lookup"><span data-stu-id="81854-132">Here's hello complete condition:</span></span>

   ![Condizione completa](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode-2.png)

   > [!TIP]
   > <span data-ttu-id="81854-134">condizione di hello toodefine nel codice, scegliere **modifica nella modalità avanzata**.</span><span class="sxs-lookup"><span data-stu-id="81854-134">toodefine hello condition in code, choose **Edit in advanced mode**.</span></span> <span data-ttu-id="81854-135">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="81854-135">For example:</span></span>
   > 
   > ![Modificare la condizione nel codice](./media/logic-apps-use-logic-app-features/edit-condition-advanced-mode.png)

4. <span data-ttu-id="81854-137">In **Sì se** e **NO se**, aggiungere tooperform passaggi hello in base che hello condizione è soddisfatta.</span><span class="sxs-lookup"><span data-stu-id="81854-137">Under **IF YES** and **IF NO**, add hello steps tooperform based on whether hello condition is met.</span></span>

   <span data-ttu-id="81854-138">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="81854-138">For example:</span></span>

   ![Condizione con percorsi SÌ e NO](./media/logic-apps-use-logic-app-features/condition-yes-no-path.png)

   > [!TIP]
   > <span data-ttu-id="81854-140">È possibile trascinare le azioni esistenti nel hello **Sì se** e **NO se** percorsi.</span><span class="sxs-lookup"><span data-stu-id="81854-140">You can drag existing actions into hello **IF YES** and **IF NO** paths.</span></span>

5. <span data-ttu-id="81854-141">Al termine, salvare l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="81854-141">When you're done, save your logic app.</span></span>

<span data-ttu-id="81854-142">Ora si ottiene i messaggi di posta elettronica solo quando il postback hello soddisfa la condizione.</span><span class="sxs-lookup"><span data-stu-id="81854-142">Now you get emails only when hello posts meet your condition.</span></span>

## <a name="repeat-actions-over-a-list-with-foreach"></a><span data-ttu-id="81854-143">Ripetere l'azione in un elenco con forEach</span><span class="sxs-lookup"><span data-stu-id="81854-143">Repeat actions over a list with forEach</span></span>

<span data-ttu-id="81854-144">ciclo forEach Hello specifica un toorepeat matrice un'azione su.</span><span class="sxs-lookup"><span data-stu-id="81854-144">hello forEach loop specifies an array toorepeat an action over.</span></span> <span data-ttu-id="81854-145">Se non è una matrice, il flusso di hello ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="81854-145">If it is not an array, hello flow fails.</span></span> <span data-ttu-id="81854-146">Ad esempio, se è azione1 che restituisce una matrice di messaggi che si desidera toosend ogni messaggio, è possibile includere l'istruzione forEach nelle proprietà hello dell'azione:`forEach : "@action('action1').outputs.messages"`</span><span class="sxs-lookup"><span data-stu-id="81854-146">For example, if you have action1 that outputs an array of messages, and you want toosend each message, you can include this forEach statement in hello properties of your action: `forEach : "@action('action1').outputs.messages"`</span></span>

## <a name="edit-hello-code-definition-for-a-logic-app"></a><span data-ttu-id="81854-147">Modifica definizione di codice hello per un'app di logica</span><span class="sxs-lookup"><span data-stu-id="81854-147">Edit hello code definition for a logic app</span></span>

<span data-ttu-id="81854-148">Anche se non si hello progettazione applicazione logica, è possibile modificare direttamente il codice hello che definisce un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="81854-148">Although you have hello Logic App Designer, you can directly edit hello code that defines a logic app.</span></span>

1. <span data-ttu-id="81854-149">Nella barra dei comandi di hello, scegliere **Code vista**.</span><span class="sxs-lookup"><span data-stu-id="81854-149">On hello command bar, choose **Code view**.</span></span>

    <span data-ttu-id="81854-150">Un editor completo viene visualizzata la definizione di hello che è stato modificato.</span><span class="sxs-lookup"><span data-stu-id="81854-150">A full editor opens and shows hello definition you edited.</span></span>

    ![Visualizzazione Codice](media/logic-apps-use-logic-app-features/codeview.png)

    <span data-ttu-id="81854-152">Nell'editor di testo hello, è possibile copiare e incollare qualsiasi numero di azioni all'interno di hello stessa logica app o tra App per la logica.</span><span class="sxs-lookup"><span data-stu-id="81854-152">In hello text editor, you can copy and paste any number of actions within hello same logic app or between logic apps.</span></span> 
    <span data-ttu-id="81854-153">È possibile anche aggiungere o rimuovere intere sezioni dalla definizione di hello ed è anche possibile condividere definizioni con altri utenti.</span><span class="sxs-lookup"><span data-stu-id="81854-153">You can also easily add or remove entire sections from hello definition, and you can also share definitions with others.</span></span>

2. <span data-ttu-id="81854-154">Scegliere le modifiche, toosave **salvare**.</span><span class="sxs-lookup"><span data-stu-id="81854-154">toosave your edits, choose **Save**.</span></span>

## <a name="parameters"></a><span data-ttu-id="81854-155">parameters</span><span class="sxs-lookup"><span data-stu-id="81854-155">Parameters</span></span>

<span data-ttu-id="81854-156">Alcune funzionalità delle app per la logica sono disponibili solo nella visualizzazione codice, ad esempio, i parametri.</span><span class="sxs-lookup"><span data-stu-id="81854-156">Some Logic Apps capabilities are available only in code view, for example, parameters.</span></span> <span data-ttu-id="81854-157">Parametri rendono facile tooreuse valori in tutta la logica app.</span><span class="sxs-lookup"><span data-stu-id="81854-157">Parameters make it easy tooreuse values throughout your logic app.</span></span> <span data-ttu-id="81854-158">Ad esempio, se si ha un indirizzo e-mail che si vuole usare in diverse azioni, è consigliabile definirlo come parametro.</span><span class="sxs-lookup"><span data-stu-id="81854-158">For example, if you have an email address that you want use in several actions, you should define that email address as a parameter.</span></span>

<span data-ttu-id="81854-159">I parametri sono ideali per l'estrazione di valori che si è molto probabile toochange.</span><span class="sxs-lookup"><span data-stu-id="81854-159">Parameters are good for pulling out values that you are likely toochange a lot.</span></span> <span data-ttu-id="81854-160">Sono particolarmente utili quando è necessario toooverride parametri in ambienti diversi.</span><span class="sxs-lookup"><span data-stu-id="81854-160">They are especially useful when you need toooverride parameters in different environments.</span></span> <span data-ttu-id="81854-161">toolearn toooverride parametri basati sull'ambiente, vedere [creare definizioni di logica app](../logic-apps/logic-apps-author-definitions.md) e [documentazione dell'API REST](https://docs.microsoft.com/rest/api/logic).</span><span class="sxs-lookup"><span data-stu-id="81854-161">toolearn how toooverride parameters based on environment, see [Author logic app definitions](../logic-apps/logic-apps-author-definitions.md) and [REST API documentation](https://docs.microsoft.com/rest/api/logic).</span></span>

<span data-ttu-id="81854-162">Questo esempio viene illustrato come tooupdate app logica esistente in modo che è possibile utilizzare i parametri per il termine di query hello.</span><span class="sxs-lookup"><span data-stu-id="81854-162">This example shows how tooupdate your existing logic app so that you can use parameters for hello query term.</span></span>

1. <span data-ttu-id="81854-163">Nella visualizzazione codice, trovare hello `parameters : {}` e aggiungere un `currentFeedUrl` oggetto:</span><span class="sxs-lookup"><span data-stu-id="81854-163">In code view, find hello `parameters : {}` object, and add a `currentFeedUrl` object:</span></span>

        "currentFeedUrl" : {
            "type" : "string",
            "defaultValue" : "http://rss.cnn.com/rss/cnn_topstories.rss"
        }

2. <span data-ttu-id="81854-164">Passare toohello `When_a_feed-item_is_published` azione, hello trova `queries` sezione e sostituire il valore di query hello con:`"feedUrl": "#@{parameters('currentFeedUrl')}"`</span><span class="sxs-lookup"><span data-stu-id="81854-164">Go toohello `When_a_feed-item_is_published` action, find hello `queries` section, and replace hello query value with : `"feedUrl": "#@{parameters('currentFeedUrl')}"`</span></span> 

    <span data-ttu-id="81854-165">toojoin due o più stringhe, è inoltre possibile utilizzare hello `concat` (funzione).</span><span class="sxs-lookup"><span data-stu-id="81854-165">toojoin two or more strings, you can also use hello `concat` function.</span></span> 
    <span data-ttu-id="81854-166">Ad esempio, `"@concat('#',parameters('currentFeedUrl'))"` works hello stesso come hello precedente.</span><span class="sxs-lookup"><span data-stu-id="81854-166">For example, `"@concat('#',parameters('currentFeedUrl'))"` works hello same as hello above.</span></span>

3.  <span data-ttu-id="81854-167">Al termine dell'operazione, scegliere **Salva**.</span><span class="sxs-lookup"><span data-stu-id="81854-167">When you're done, choose **Save**.</span></span> 

    <span data-ttu-id="81854-168">Ora è possibile modificare RSS del sito Web di hello feed passando un URL diverso tramite hello `currentFeedURL` oggetto.</span><span class="sxs-lookup"><span data-stu-id="81854-168">Now you can change hello website's RSS feed by passing a different URL through hello `currentFeedURL` object.</span></span>

<span data-ttu-id="81854-169">Altre informazioni, vedere [come definizioni di tooauthor logica app](../logic-apps/logic-apps-author-definitions.md).</span><span class="sxs-lookup"><span data-stu-id="81854-169">Learn more about [how tooauthor logic app definitions](../logic-apps/logic-apps-author-definitions.md).</span></span>

## <a name="start-logic-app-workflows"></a><span data-ttu-id="81854-170">Avviare i flussi di lavoro delle app per la logica</span><span class="sxs-lookup"><span data-stu-id="81854-170">Start logic app workflows</span></span>

<span data-ttu-id="81854-171">Sono disponibili opzioni diverse per l'avvio del flusso di lavoro hello definito nell'applicazione la logica.</span><span class="sxs-lookup"><span data-stu-id="81854-171">You have different options for starting hello workflow defined in your logic app.</span></span> <span data-ttu-id="81854-172">È sempre possibile avviare un flusso di lavoro su richiesta in hello [portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="81854-172">You can always start a workflow on-demand in hello [Azure portal].</span></span>

### <a name="recurrence-triggers"></a><span data-ttu-id="81854-173">Trigger di ricorrenza</span><span class="sxs-lookup"><span data-stu-id="81854-173">Recurrence triggers</span></span>

<span data-ttu-id="81854-174">Un trigger di ricorrenza viene eseguito a un intervallo specificato dall'utente.</span><span class="sxs-lookup"><span data-stu-id="81854-174">A recurrence trigger runs at an interval that you specify.</span></span> <span data-ttu-id="81854-175">Quando il trigger di hello logica condizionale, trigger hello determina necessità di un flusso di lavoro hello toorun.</span><span class="sxs-lookup"><span data-stu-id="81854-175">When hello trigger has conditional logic, hello trigger determines whether hello workflow needs toorun.</span></span> <span data-ttu-id="81854-176">Un trigger indica flusso di lavoro hello devono essere eseguite tramite la restituzione di un `200` codice di stato.</span><span class="sxs-lookup"><span data-stu-id="81854-176">A trigger indicates hello workflow should run by returning a `200` status code.</span></span> <span data-ttu-id="81854-177">Quando non è necessaria toorun, flusso di lavoro hello trigger hello restituisce un `202` codice di stato.</span><span class="sxs-lookup"><span data-stu-id="81854-177">When hello workflow doesn't need toorun, hello trigger returns a `202` status code.</span></span>

### <a name="callback-using-rest-apis"></a><span data-ttu-id="81854-178">Callback tramite le API REST</span><span class="sxs-lookup"><span data-stu-id="81854-178">Callback using REST APIs</span></span>

<span data-ttu-id="81854-179">toostart un flusso di lavoro, è possono chiamare un endpoint di app logica servizi.</span><span class="sxs-lookup"><span data-stu-id="81854-179">toostart a workflow, services can call a logic app endpoint.</span></span> <span data-ttu-id="81854-180">Scegliere questo tipo di logica dell'applicazione su richiesta, toostart **Esegui ora** hello barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="81854-180">toostart this kind of logic app on-demand, choose **Run now** on hello command bar.</span></span> <span data-ttu-id="81854-181">Vedere [Avviare i flussi di lavoro chiamando endpoint dell'app per la logica come trigger](../logic-apps/logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="81854-181">See [Start workflows by calling logic app endpoints as triggers](../logic-apps/logic-apps-http-endpoint.md).</span></span> 

<!-- Shared links -->
[portale di Azure]: https://portal.azure.com

## <a name="next-steps"></a><span data-ttu-id="81854-183">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="81854-183">Next steps</span></span>

* [<span data-ttu-id="81854-184">Istruzioni switch</span><span class="sxs-lookup"><span data-stu-id="81854-184">Switch statements</span></span>](../logic-apps/logic-apps-switch-case.md) 
* [<span data-ttu-id="81854-185">Cicli, ambiti e debatching</span><span class="sxs-lookup"><span data-stu-id="81854-185">Loops, scopes, and debatching</span></span>](../logic-apps/logic-apps-loops-and-scopes.md)
* [<span data-ttu-id="81854-186">Creare definizioni di app per la logica</span><span class="sxs-lookup"><span data-stu-id="81854-186">Author logic app definitions</span></span>](../logic-apps/logic-apps-author-definitions.md)