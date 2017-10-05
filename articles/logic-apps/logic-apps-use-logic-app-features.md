---
title: Aggiungere condizioni e avviare i flussi di lavoro - App per la logica di Azure | Microsoft Docs
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
ms.openlocfilehash: e632c48ed31e82536db55a9c54438bece0c38fd4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-logic-apps-features"></a><span data-ttu-id="c2ff1-103">Usare le funzionalità delle app per la logica</span><span class="sxs-lookup"><span data-stu-id="c2ff1-103">Use Logic Apps features</span></span>

<span data-ttu-id="c2ff1-104">In un [argomento precedente](../logic-apps/logic-apps-create-a-logic-app.md) è stata creata la prima app per la logica.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-104">In a [previous topic](../logic-apps/logic-apps-create-a-logic-app.md), you created your first logic app.</span></span> <span data-ttu-id="c2ff1-105">Per il controllo del flusso di lavoro delle app per la logica, è possibile specificare percorsi diversi per l'app per la logica da eseguire e la modalità di elaborazione dati in matrici, raccolte e batch.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-105">To control your logic app's workflow, you can specify different paths for your logic app to run and how to process data in arrays, collections, and batches.</span></span> <span data-ttu-id="c2ff1-106">È possibile includere questi elementi nel flusso di lavoro dell'app per la logica:</span><span class="sxs-lookup"><span data-stu-id="c2ff1-106">You can include these elements in your logic app workflow:</span></span>

* <span data-ttu-id="c2ff1-107">Le condizioni e le [istruzioni switch](../logic-apps/logic-apps-switch-case.md) consentono all'app per la logica di eseguire azioni diverse in base al fatto che vengano soddisfatte o meno condizioni specifiche.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-107">Conditions and [switch statements](../logic-apps/logic-apps-switch-case.md) let your logic app run different actions based on whether specific conditions are met.</span></span>

* <span data-ttu-id="c2ff1-108">I [cicli](../logic-apps/logic-apps-loops-and-scopes.md) consentono di eseguire ripetutamente passaggi dell'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-108">[Loops](../logic-apps/logic-apps-loops-and-scopes.md) let your logic app run steps repeatedly.</span></span> <span data-ttu-id="c2ff1-109">Ad esempio, è possibile ripetere azioni su una matrice quando si usa un ciclo **For_each**.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-109">For example, you can repeat actions over an array when you use a **For_each** loop.</span></span> <span data-ttu-id="c2ff1-110">Oppure è possibile ripetere azioni fino a quando non viene soddisfatta una condizione se si usa un ciclo **Until**.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-110">Or you can repeat actions until a condition is met when you use an **Until** loop.</span></span>

* <span data-ttu-id="c2ff1-111">Gli [ambiti](../logic-apps/logic-apps-loops-and-scopes.md) consentono di raggruppare serie di azioni, ad esempio per implementare la gestione delle eccezioni.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-111">[Scopes](../logic-apps/logic-apps-loops-and-scopes.md) let you group series of actions together, for example, to implement exception handling.</span></span>

* <span data-ttu-id="c2ff1-112">La [scomposizione dei batch](../logic-apps/logic-apps-loops-and-scopes.md) consente all'app per la logica di avviare flussi di lavoro separati per gli elementi di una matrice quando si usa il comando **SplitOn**.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-112">[Debatching](../logic-apps/logic-apps-loops-and-scopes.md) lets your logic app start separate workflows for items in an array when you use the **SplitOn** command.</span></span>

<span data-ttu-id="c2ff1-113">Questo argomento introduce altri concetti per la compilazione dell'app per la logica:</span><span class="sxs-lookup"><span data-stu-id="c2ff1-113">This topic introduces other concepts for building your logic app:</span></span>

* <span data-ttu-id="c2ff1-114">Visualizzazione Codice per modificare un'app per la logica esistente</span><span class="sxs-lookup"><span data-stu-id="c2ff1-114">Code view to edit an existing logic app</span></span>
* <span data-ttu-id="c2ff1-115">Opzioni per avviare un flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="c2ff1-115">Options for starting a workflow</span></span>

## <a name="conditions-run-steps-only-after-meeting-a-condition"></a><span data-ttu-id="c2ff1-116">Condizioni: eseguire i passaggi solo quando è soddisfatta una condizione</span><span class="sxs-lookup"><span data-stu-id="c2ff1-116">Conditions: Run steps only after meeting a condition</span></span>

<span data-ttu-id="c2ff1-117">Per fare in modo che l'app per la logica esegua i passaggi solo quando i dati soddisfano criteri specifici, è possibile aggiungere una condizione che confronta i dati nel flusso di lavoro in base a campi o valori specifici.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-117">To have your logic app run steps only when data meets specific criteria, you can add a condition that compares data in the workflow against specific fields or values.</span></span>

<span data-ttu-id="c2ff1-118">Si supponga, ad esempio, di avere un'app per la logica che invia troppi messaggi di posta elettronica per i post sul feed RSS di un sito Web.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-118">For example, suppose you have a logic app that sends you too many emails for posts on a website's RSS feed.</span></span> <span data-ttu-id="c2ff1-119">È possibile aggiungere una condizione in modo che l'app per la logica invii un messaggio solo quando il nuovo post appartiene a una categoria specifica.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-119">You can add a condition so that your logic app sends email only when the new post belongs to a specific category.</span></span>

1. <span data-ttu-id="c2ff1-120">Nel [portale di Azure](https://portal.azure.com) individuare e aprire l'app per la logica in Progettazione app per la logica.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-120">In the [Azure portal](https://portal.azure.com), find and open your logic app in Logic App Designer.</span></span>

2. <span data-ttu-id="c2ff1-121">Aggiungere una condizione al percorso del flusso di lavoro da usare.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-121">Add a condition to the workflow location that you want.</span></span> 

   <span data-ttu-id="c2ff1-122">Per aggiungere la condizione tra i passaggi esistenti nel flusso di lavoro dell'app per la logica, spostare il puntatore sulla freccia dove si vuole aggiungere la condizione.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-122">To add the condition between existing steps in the logic app workflow, move the pointer over the arrow where you want to add the condition.</span></span> 
   <span data-ttu-id="c2ff1-123">Scegliere il **segno più** (**+**), quindi **Aggiungi una condizione**.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-123">Choose the **plus sign** (**+**), then choose **Add a condition**.</span></span> <span data-ttu-id="c2ff1-124">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="c2ff1-124">For example:</span></span>

   ![Aggiungere una condizione all'app per la logica](./media/logic-apps-use-logic-app-features/add-condition.png)

   > [!NOTE]
   > <span data-ttu-id="c2ff1-126">Se si vuole aggiungere una condizione alla fine del flusso di lavoro corrente, andare alla fine dell'app per la logica e scegliere **+ Nuovo passaggio**.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-126">If you want to add a condition at the end of your current workflow, go to the bottom of your logic app, and choose **+ New step**.</span></span>

3. <span data-ttu-id="c2ff1-127">Ora definire la condizione.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-127">Now define the condition.</span></span> <span data-ttu-id="c2ff1-128">Specificare il campo di origine da valutare, l'operazione da eseguire e il valore o il campo di destinazione.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-128">Specify the source field that you want to evaluate, the operation to perform, and the target value or field.</span></span> <span data-ttu-id="c2ff1-129">Per aggiungere alla condizione campi già esistenti, sceglierli dall'**elenco Aggiungi contenuto dinamico**.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-129">To add existing fields to your condition, choose from the **Add dynamic content list**.</span></span>

   <span data-ttu-id="c2ff1-130">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="c2ff1-130">For example:</span></span>

   ![Modificare la condizione nella modalità di base](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode.png)

   <span data-ttu-id="c2ff1-132">Questa è la condizione completa:</span><span class="sxs-lookup"><span data-stu-id="c2ff1-132">Here's the complete condition:</span></span>

   ![Condizione completa](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode-2.png)

   > [!TIP]
   > <span data-ttu-id="c2ff1-134">Per definire la condizione nel codice, scegliere **Modifica in modalità avanzata**.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-134">To define the condition in code, choose **Edit in advanced mode**.</span></span> <span data-ttu-id="c2ff1-135">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="c2ff1-135">For example:</span></span>
   > 
   > ![Modificare la condizione nel codice](./media/logic-apps-use-logic-app-features/edit-condition-advanced-mode.png)

4. <span data-ttu-id="c2ff1-137">In **SE SÌ** e **SE NO** aggiungere i passaggi da eseguire in base al fatto che la condizione sia soddisfatta o meno.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-137">Under **IF YES** and **IF NO**, add the steps to perform based on whether the condition is met.</span></span>

   <span data-ttu-id="c2ff1-138">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="c2ff1-138">For example:</span></span>

   ![Condizione con percorsi SÌ e NO](./media/logic-apps-use-logic-app-features/condition-yes-no-path.png)

   > [!TIP]
   > <span data-ttu-id="c2ff1-140">È possibile trascinare le azioni esistenti nei percorsi **SE SÌ** e **SE NO**.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-140">You can drag existing actions into the **IF YES** and **IF NO** paths.</span></span>

5. <span data-ttu-id="c2ff1-141">Al termine, salvare l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-141">When you're done, save your logic app.</span></span>

<span data-ttu-id="c2ff1-142">Ora si ricevono messaggi di posta elettronica solo quando i post soddisfano la condizione.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-142">Now you get emails only when the posts meet your condition.</span></span>

## <a name="repeat-actions-over-a-list-with-foreach"></a><span data-ttu-id="c2ff1-143">Ripetere l'azione in un elenco con forEach</span><span class="sxs-lookup"><span data-stu-id="c2ff1-143">Repeat actions over a list with forEach</span></span>

<span data-ttu-id="c2ff1-144">Il ciclo forEach specifica una matrice per la ripetizione di un'azione.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-144">The forEach loop specifies an array to repeat an action over.</span></span> <span data-ttu-id="c2ff1-145">Se non è una matrice, il flusso ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-145">If it is not an array, the flow fails.</span></span> <span data-ttu-id="c2ff1-146">Ad esempio, se action1 genera una matrice di messaggi e si vuole inviare ogni messaggio, è possibile inserire questa istruzione forEach nelle proprietà dell'azione: `forEach : "@action('action1').outputs.messages"`</span><span class="sxs-lookup"><span data-stu-id="c2ff1-146">For example, if you have action1 that outputs an array of messages, and you want to send each message, you can include this forEach statement in the properties of your action: `forEach : "@action('action1').outputs.messages"`</span></span>

## <a name="edit-the-code-definition-for-a-logic-app"></a><span data-ttu-id="c2ff1-147">Modificare la definizione di codice per un'app per la logica</span><span class="sxs-lookup"><span data-stu-id="c2ff1-147">Edit the code definition for a logic app</span></span>

<span data-ttu-id="c2ff1-148">Oltre che nella finestra di progettazione dell'app per la logica, è possibile modificare direttamente il codice che definisce un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-148">Although you have the Logic App Designer, you can directly edit the code that defines a logic app.</span></span>

1. <span data-ttu-id="c2ff1-149">Nella barra dei comandi fare clic su **Visualizzazione Codice**.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-149">On the command bar, choose **Code view**.</span></span>

    <span data-ttu-id="c2ff1-150">Verrà aperto un editor completo che mostra la definizione appena modificata.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-150">A full editor opens and shows the definition you edited.</span></span>

    ![Visualizzazione Codice](media/logic-apps-use-logic-app-features/codeview.png)

    <span data-ttu-id="c2ff1-152">Nell'editor di testo, è possibile copiare e incollare un numero qualsiasi di azioni all'interno della stessa app per la logica o tra app per la logica.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-152">In the text editor, you can copy and paste any number of actions within the same logic app or between logic apps.</span></span> 
    <span data-ttu-id="c2ff1-153">È anche possibile aggiungere o rimuovere facilmente intere sezioni dalla definizione, oltre a condividere definizioni con altri.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-153">You can also easily add or remove entire sections from the definition, and you can also share definitions with others.</span></span>

2. <span data-ttu-id="c2ff1-154">Per salvare le modifiche, scegliere **Salva**.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-154">To save your edits, choose **Save**.</span></span>

## <a name="parameters"></a><span data-ttu-id="c2ff1-155">Parametri</span><span class="sxs-lookup"><span data-stu-id="c2ff1-155">Parameters</span></span>

<span data-ttu-id="c2ff1-156">Alcune funzionalità delle app per la logica sono disponibili solo nella visualizzazione codice, ad esempio, i parametri.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-156">Some Logic Apps capabilities are available only in code view, for example, parameters.</span></span> <span data-ttu-id="c2ff1-157">I parametri semplificano il riutilizzo dei valori all'interno di un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-157">Parameters make it easy to reuse values throughout your logic app.</span></span> <span data-ttu-id="c2ff1-158">Ad esempio, se si ha un indirizzo e-mail che si vuole usare in diverse azioni, è consigliabile definirlo come parametro.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-158">For example, if you have an email address that you want use in several actions, you should define that email address as a parameter.</span></span>

<span data-ttu-id="c2ff1-159">I parametri costituiscono un buon metodo per estrarre valori che probabilmente verranno modificati molto.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-159">Parameters are good for pulling out values that you are likely to change a lot.</span></span> <span data-ttu-id="c2ff1-160">Sono particolarmente utili quando è necessario eseguire l'override dei parametri in diversi ambienti.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-160">They are especially useful when you need to override parameters in different environments.</span></span> <span data-ttu-id="c2ff1-161">Per informazioni sull'esecuzione dell'override dei parametri in base all'ambiente, vedere l'argomento relativo alla [creazione di definizioni di app per la logica](../logic-apps/logic-apps-author-definitions.md) e la [documentazione dell'API REST](https://docs.microsoft.com/rest/api/logic).</span><span class="sxs-lookup"><span data-stu-id="c2ff1-161">To learn how to override parameters based on environment, see [Author logic app definitions](../logic-apps/logic-apps-author-definitions.md) and [REST API documentation](https://docs.microsoft.com/rest/api/logic).</span></span>

<span data-ttu-id="c2ff1-162">Questo esempio illustra come aggiornare l'app per la logica esistente in modo che sia possibile usare i parametri per il termine della query.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-162">This example shows how to update your existing logic app so that you can use parameters for the query term.</span></span>

1. <span data-ttu-id="c2ff1-163">Nella visualizzazione codice trovare l'oggetto `parameters : {}` e aggiungere un oggetto `currentFeedUrl`:</span><span class="sxs-lookup"><span data-stu-id="c2ff1-163">In code view, find the `parameters : {}` object, and add a `currentFeedUrl` object:</span></span>

        "currentFeedUrl" : {
            "type" : "string",
            "defaultValue" : "http://rss.cnn.com/rss/cnn_topstories.rss"
        }

2. <span data-ttu-id="c2ff1-164">Andare all'azione `When_a_feed-item_is_published`, trovare la sezione `queries` e sostituire il valore della query con `"feedUrl": "#@{parameters('currentFeedUrl')}"`.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-164">Go to the `When_a_feed-item_is_published` action, find the `queries` section, and replace the query value with : `"feedUrl": "#@{parameters('currentFeedUrl')}"`</span></span> 

    <span data-ttu-id="c2ff1-165">Per unire due o più stringhe, è inoltre possibile usare la funzione `concat`.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-165">To join two or more strings, you can also use the `concat` function.</span></span> 
    <span data-ttu-id="c2ff1-166">Ad esempio, `"@concat('#',parameters('currentFeedUrl'))"` funziona come sopra.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-166">For example, `"@concat('#',parameters('currentFeedUrl'))"` works the same as the above.</span></span>

3.  <span data-ttu-id="c2ff1-167">Al termine dell'operazione, scegliere **Salva**.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-167">When you're done, choose **Save**.</span></span> 

    <span data-ttu-id="c2ff1-168">Ora è possibile modificare il feed RSS del sito Web passando un URL diverso attraverso l'oggetto `currentFeedURL`.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-168">Now you can change the website's RSS feed by passing a different URL through the `currentFeedURL` object.</span></span>

<span data-ttu-id="c2ff1-169">Altre informazioni su come [creare definizioni di app per la logica](../logic-apps/logic-apps-author-definitions.md).</span><span class="sxs-lookup"><span data-stu-id="c2ff1-169">Learn more about [how to author logic app definitions](../logic-apps/logic-apps-author-definitions.md).</span></span>

## <a name="start-logic-app-workflows"></a><span data-ttu-id="c2ff1-170">Avviare i flussi di lavoro delle app per la logica</span><span class="sxs-lookup"><span data-stu-id="c2ff1-170">Start logic app workflows</span></span>

<span data-ttu-id="c2ff1-171">Sono disponibili diverse opzioni per avviare il flusso di lavoro definito nell'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-171">You have different options for starting the workflow defined in your logic app.</span></span> <span data-ttu-id="c2ff1-172">Un flusso di lavoro può sempre essere avviato su richiesta nel [Portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="c2ff1-172">You can always start a workflow on-demand in the [Azure portal].</span></span>

### <a name="recurrence-triggers"></a><span data-ttu-id="c2ff1-173">Trigger di ricorrenza</span><span class="sxs-lookup"><span data-stu-id="c2ff1-173">Recurrence triggers</span></span>

<span data-ttu-id="c2ff1-174">Un trigger di ricorrenza viene eseguito a un intervallo specificato dall'utente.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-174">A recurrence trigger runs at an interval that you specify.</span></span> <span data-ttu-id="c2ff1-175">Quando il trigger è caratterizzato dalla logica condizionale, determina se è necessario eseguire il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-175">When the trigger has conditional logic, the trigger determines whether the workflow needs to run.</span></span> <span data-ttu-id="c2ff1-176">Un trigger indica che il flusso di lavoro deve essere eseguito restituendo un codice di stato `200` .</span><span class="sxs-lookup"><span data-stu-id="c2ff1-176">A trigger indicates the workflow should run by returning a `200` status code.</span></span> <span data-ttu-id="c2ff1-177">Quando non è necessaria l'esecuzione del flusso di lavoro, il trigger restituisce un codice di stato `202`.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-177">When the workflow doesn't need to run, the trigger returns a `202` status code.</span></span>

### <a name="callback-using-rest-apis"></a><span data-ttu-id="c2ff1-178">Callback tramite le API REST</span><span class="sxs-lookup"><span data-stu-id="c2ff1-178">Callback using REST APIs</span></span>

<span data-ttu-id="c2ff1-179">Per avviare un flusso di lavoro, i servizi possono chiamare un endpoint dell'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-179">To start a workflow, services can call a logic app endpoint.</span></span> <span data-ttu-id="c2ff1-180">Per avviare questa tipologia di app per la logica su richiesta, fare clic su **Run now** (Esegui ora) nella barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="c2ff1-180">To start this kind of logic app on-demand, choose **Run now** on the command bar.</span></span> <span data-ttu-id="c2ff1-181">Vedere [Avviare i flussi di lavoro chiamando endpoint dell'app per la logica come trigger](../logic-apps/logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="c2ff1-181">See [Start workflows by calling logic app endpoints as triggers](../logic-apps/logic-apps-http-endpoint.md).</span></span> 

<!-- Shared links -->
<span data-ttu-id="c2ff1-182">[Portale di Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="c2ff1-182">[Azure portal]: https://portal.azure.com</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2ff1-183">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c2ff1-183">Next steps</span></span>

* [<span data-ttu-id="c2ff1-184">Istruzioni switch</span><span class="sxs-lookup"><span data-stu-id="c2ff1-184">Switch statements</span></span>](../logic-apps/logic-apps-switch-case.md) 
* [<span data-ttu-id="c2ff1-185">Cicli, ambiti e debatching</span><span class="sxs-lookup"><span data-stu-id="c2ff1-185">Loops, scopes, and debatching</span></span>](../logic-apps/logic-apps-loops-and-scopes.md)
* [<span data-ttu-id="c2ff1-186">Creare definizioni di app per la logica</span><span class="sxs-lookup"><span data-stu-id="c2ff1-186">Author logic app definitions</span></span>](../logic-apps/logic-apps-author-definitions.md)