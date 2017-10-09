---
title: istruzione aaaSwitch per azioni diverse nelle app di logica di Azure | Documenti Microsoft
description: Scegliere tooperform azioni diverse in base ai valori dell'espressione, utilizzando un'istruzione switch App per la logica
services: logic-apps
keywords: Istruzione switch
author: derek1ee
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: LADocs; deli
ms.openlocfilehash: 09ed7e4a752003aba157e9156bf4dc89ef86f5ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="perform-different-actions-in-logic-apps-with-a-switch-statement"></a><span data-ttu-id="20156-104">Eseguire diverse azioni in app per la logica con un'istruzione switch</span><span class="sxs-lookup"><span data-stu-id="20156-104">Perform different actions in logic apps with a switch statement</span></span>

<span data-ttu-id="20156-105">Durante la creazione di un flusso di lavoro, spesso è tootake azioni diverse in base al valore di hello di un oggetto o l'espressione.</span><span class="sxs-lookup"><span data-stu-id="20156-105">When authoring a workflow, you often have tootake different actions based on hello value of an object or expression.</span></span> <span data-ttu-id="20156-106">Ad esempio, è il toobehave app logica in modo diverso in base al codice di stato hello di una richiesta HTTP o un'opzione selezionata in un messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="20156-106">For example, you might want your logic app toobehave differently based on hello status code of an HTTP request, or an option selected in an email.</span></span>

<span data-ttu-id="20156-107">È possibile utilizzare un tooimplement istruzione switch questi scenari.</span><span class="sxs-lookup"><span data-stu-id="20156-107">You can use a switch statement tooimplement these scenarios.</span></span> <span data-ttu-id="20156-108">L'app di logica possibile valutare un token o un'espressione e scegliere caso hello hello hello di tooexecute stesso valore specificato di azioni.</span><span class="sxs-lookup"><span data-stu-id="20156-108">Your logic app can evaluate a token or expression, and choose hello case with hello same value tooexecute hello specified actions.</span></span> <span data-ttu-id="20156-109">Un solo case deve corrispondere l'istruzione switch hello.</span><span class="sxs-lookup"><span data-stu-id="20156-109">Only one case should match hello switch statement.</span></span>

> [!TIP]
> <span data-ttu-id="20156-110">Come tutti i linguaggi di programmazione, le istruzioni switch supportano solo gli operatori di uguaglianza.</span><span class="sxs-lookup"><span data-stu-id="20156-110">Like all programming languages, switch statements support only equality operators.</span></span> <span data-ttu-id="20156-111">Se sono necessari altri operatori relazionali, ad esempio "maggiore di", usare un'istruzione di condizione.</span><span class="sxs-lookup"><span data-stu-id="20156-111">If you need other relational operators, such as "greater than", use a condition statement.</span></span>
> <span data-ttu-id="20156-112">comportamento di esecuzione deterministico tooensure, casi devono contenere un valore univoco e statico invece di token dinamico o un'espressione.</span><span class="sxs-lookup"><span data-stu-id="20156-112">tooensure deterministic execution behavior, cases must contain a unique and static value instead of dynamic tokens or expression.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="20156-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="20156-113">Prerequisites</span></span>

- <span data-ttu-id="20156-114">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="20156-114">An active Azure subscription.</span></span> <span data-ttu-id="20156-115">Se non si ha una sottoscrizione di Azure, [creare un account gratuito](https://azure.microsoft.com/free/) o provare l'[App per la logica gratuita](https://tryappservice.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="20156-115">If you don't have an active Azure subscription, [create a free account](https://azure.microsoft.com/free/), or try [Logic Apps for free](https://tryappservice.azure.com/).</span></span>
- [<span data-ttu-id="20156-116">Conoscenze di base di app per la logica</span><span class="sxs-lookup"><span data-stu-id="20156-116">Basic knowledge about logic apps</span></span>](logic-apps-what-are-logic-apps.md)

## <a name="add-a-switch-statement-tooyour-workflow"></a><span data-ttu-id="20156-117">Aggiungere un flusso di lavoro tooyour istruzione switch</span><span class="sxs-lookup"><span data-stu-id="20156-117">Add a switch statement tooyour workflow</span></span>

<span data-ttu-id="20156-118">tooshow funzionamento di un'istruzione switch, in questo esempio crea un'app di logica che i file di monitoraggi caricati tooDropbox.</span><span class="sxs-lookup"><span data-stu-id="20156-118">tooshow how a switch statement works, this example creates a logic app that monitors files uploaded tooDropbox.</span></span> <span data-ttu-id="20156-119">Quando vengono caricati i nuovi file hello, hello logica app Invia messaggio di posta elettronica tooan responsabile sceglie se tootransfer tooSharePoint tali file.</span><span class="sxs-lookup"><span data-stu-id="20156-119">When hello new files are uploaded, hello logic app sends email tooan approver who chooses whether tootransfer those files tooSharePoint.</span></span> <span data-ttu-id="20156-120">app Hello utilizza un'istruzione switch che consente di eseguire azioni diverse in base al valore di hello hello Seleziona responsabile approvazione.</span><span class="sxs-lookup"><span data-stu-id="20156-120">hello app uses a switch statement that performs different actions based on hello value that hello approver selects.</span></span>

1. <span data-ttu-id="20156-121">Creare un'app per la logica e selezionare questo trigger: **Dropbox - When a file is created** (Dropbox - Quando viene creato un file).</span><span class="sxs-lookup"><span data-stu-id="20156-121">Create a logic app, and select this trigger: **Dropbox - When a file is created**.</span></span>

   ![Usare il trigger Dropbox - When a file is created (Dropbox - Quando viene creato un file)](./media/logic-apps-switch-case/dropbox-trigger.jpg)

2. <span data-ttu-id="20156-123">Aggiungere trigger hello, questa azione: **Outlook.com - invio di email approvazione**</span><span class="sxs-lookup"><span data-stu-id="20156-123">Under hello trigger, add this action: **Outlook.com - Send approval email**</span></span>

   > [!TIP]
   > <span data-ttu-id="20156-124">Le app per la logica supportano anche gli scenari di posta elettronica di approvazione da un account di Outlook Office 365.</span><span class="sxs-lookup"><span data-stu-id="20156-124">Logic apps also support sending approval email scenarios from an Office 365 Outlook account.</span></span>

   - <span data-ttu-id="20156-125">Se non si dispone di una connessione esistente, viene chiesto toocreate uno.</span><span class="sxs-lookup"><span data-stu-id="20156-125">If you don't have an existing connection, you're prompted toocreate one.</span></span>
   - <span data-ttu-id="20156-126">Compilare i campi necessario hello.</span><span class="sxs-lookup"><span data-stu-id="20156-126">Fill in hello required fields.</span></span> <span data-ttu-id="20156-127">Ad esempio, in **a**, specificare l'indirizzo di posta elettronica hello per l'invio di posta elettronica responsabile approvazione hello.</span><span class="sxs-lookup"><span data-stu-id="20156-127">For example, under **To**, specify hello email address for sending hello approver email.</span></span>
   - <span data-ttu-id="20156-128">In **Opzioni utente**, inserire `Approve, Reject`.</span><span class="sxs-lookup"><span data-stu-id="20156-128">Under **User Options**, enter `Approve, Reject`.</span></span>

   ![Configurare la connessione](./media/logic-apps-switch-case/send-approval-email-action.jpg)

3. <span data-ttu-id="20156-130">Aggiungere un'istruzione switc.</span><span class="sxs-lookup"><span data-stu-id="20156-130">Add a switch statement.</span></span>

   - <span data-ttu-id="20156-131">Selezionare **+ Nuovo passaggio** > **... Altro** > **Aggiungi istruzione switch case**.</span><span class="sxs-lookup"><span data-stu-id="20156-131">Select **+ New step** > **... More** > **Add a switch case**.</span></span> 
   - <span data-ttu-id="20156-132">Ora desideriamo tooselect hello azione tooperform in base a hello `SelectedOptions` l'output di hello *inviare posta elettronica di approvazione* azione.</span><span class="sxs-lookup"><span data-stu-id="20156-132">Now we want tooselect hello action tooperform based on hello `SelectedOptions` output from hello *Send approval email* action.</span></span> 
   <span data-ttu-id="20156-133">Questo campo si trova in hello **aggiungere contenuto dinamico** selettore.</span><span class="sxs-lookup"><span data-stu-id="20156-133">You can find this field in hello **Add dynamic content** selector.</span></span>
   - <span data-ttu-id="20156-134">Utilizzare *caso 1* toohandle quando seleziona responsabile approvazione hello `Approve`.</span><span class="sxs-lookup"><span data-stu-id="20156-134">Use *Case 1* toohandle when hello approver selects `Approve`.</span></span>
     - <span data-ttu-id="20156-135">Se approvata, copiare hello originale file tooSharePoint Online con hello [ **SharePoint Online - creare file** azione](../connectors/connectors-create-api-sharepointonline.md).</span><span class="sxs-lookup"><span data-stu-id="20156-135">If approved, copy hello original file tooSharePoint Online with hello [**SharePoint Online - Create file** action](../connectors/connectors-create-api-sharepointonline.md).</span></span>
     - <span data-ttu-id="20156-136">Aggiungere un'altra azione all'interno di hello case toonotify utenti che un nuovo file è disponibile in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="20156-136">Add another action within hello case toonotify users that a new file is available on SharePoint.</span></span>
   - <span data-ttu-id="20156-137">Aggiungere un altro toohandle maiuscole quando l'utente seleziona `Reject`.</span><span class="sxs-lookup"><span data-stu-id="20156-137">Add another case toohandle when user selects `Reject`.</span></span>
     - <span data-ttu-id="20156-138">Se rifiutata, inviare una notifica tramite posta elettronica per informare gli altri revisori che file hello viene rifiutato e se è necessaria alcuna azione ulteriore.</span><span class="sxs-lookup"><span data-stu-id="20156-138">If rejected, send a notification email informing other approvers that hello file is rejected and no further action is required.</span></span>
   - <span data-ttu-id="20156-139">`SelectedOptions`sono disponibili solo due opzioni, pertanto, è possibile mantenere hello **predefinito** case vuota.</span><span class="sxs-lookup"><span data-stu-id="20156-139">`SelectedOptions` provides only two options, so we can leave hello **Default** case empty.</span></span>

   ![Istruzioni switch](./media/logic-apps-switch-case/switch.jpg)

   > [!NOTE]
   > <span data-ttu-id="20156-141">Un'istruzione switch è necessario almeno un case nel caso di aggiunta toohello predefinito.</span><span class="sxs-lookup"><span data-stu-id="20156-141">A switch statement needs at least one case in addition toohello default case.</span></span>

4. <span data-ttu-id="20156-142">Dopo l'istruzione switch hello, eliminare hello originale file caricato tooDropbox aggiungendo questa azione: **Dropbox - Elimina file**</span><span class="sxs-lookup"><span data-stu-id="20156-142">After hello switch statement, delete hello original file uploaded tooDropbox by adding this action: **Dropbox - Delete file**</span></span>

5. <span data-ttu-id="20156-143">Salvare l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="20156-143">Save your logic app.</span></span> <span data-ttu-id="20156-144">Testare l'app caricando un file tooDropbox.</span><span class="sxs-lookup"><span data-stu-id="20156-144">Test your app by uploading a file tooDropbox.</span></span> <span data-ttu-id="20156-145">Si dovrebbe ricevere in breve tempo un messaggio di posta elettronica di approvazione.</span><span class="sxs-lookup"><span data-stu-id="20156-145">You should receive an approval email shortly.</span></span> <span data-ttu-id="20156-146">Selezionare un'opzione e osservare il comportamento di hello.</span><span class="sxs-lookup"><span data-stu-id="20156-146">Select an option, and observe hello behavior.</span></span>

   > [!TIP]
   > <span data-ttu-id="20156-147">Estrarre come troppo[monitorare App per la logica](logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="20156-147">Check out how too[monitor your logic apps](logic-apps-monitor-your-logic-apps.md).</span></span>

## <a name="understand-hello-code-behind-switch-statements"></a><span data-ttu-id="20156-148">Comprendere il codice hello dietro istruzioni switch</span><span class="sxs-lookup"><span data-stu-id="20156-148">Understand hello code behind switch statements</span></span>

<span data-ttu-id="20156-149">Ora che è stato creato correttamente un'applicazione logica utilizzando un'istruzione switch, esaminare la definizione di codice hello dietro istruzione switch hello.</span><span class="sxs-lookup"><span data-stu-id="20156-149">Now that you successfully created a logic app using a switch statement, let's look at hello code definition behind hello switch statement.</span></span>

```json
"Switch": {
    "type": "Switch",
    "expression": "@body('Send_approval_email')?['SelectedOption']",
    "cases": {
        "Case 1" : {
            "case" : "Approved",
            "actions" : {}
        },
        "Case 2" : {
            "case" : "Rejected",
            "actions" : {}
        }
    },
    "default": {
        "actions": {}
    },
    "runAfter": {
        "Send_approval_email": [
            "Succeeded"
        ]
    }
}
```

* <span data-ttu-id="20156-150">`"Switch"`è il nome di hello dell'istruzione switch hello, che è possibile rinominare per migliorare la leggibilità.</span><span class="sxs-lookup"><span data-stu-id="20156-150">`"Switch"` is hello name of hello switch statement, which you can rename for readability.</span></span> 
* <span data-ttu-id="20156-151">`"type": "Switch"`indica che l'azione di hello è un'istruzione switch.</span><span class="sxs-lookup"><span data-stu-id="20156-151">`"type": "Switch"` indicates that hello action is a switch statement.</span></span> 
* <span data-ttu-id="20156-152">`"expression"`è l'opzione del revisore hello in questo esempio e viene valutato rispetto a ogni caso dichiarato in un secondo momento nella definizione di hello.</span><span class="sxs-lookup"><span data-stu-id="20156-152">`"expression"` is hello approver's selected option in this example and is evaluated against each case declared later in hello definition.</span></span> 
* <span data-ttu-id="20156-153">`"cases"` può contenere qualsiasi numero di case.</span><span class="sxs-lookup"><span data-stu-id="20156-153">`"cases"` can contain any number of cases.</span></span> <span data-ttu-id="20156-154">Per ogni case, `"Case *"` è il nome predefinito hello del case hello, che è possibile rinominare per migliorare la leggibilità.</span><span class="sxs-lookup"><span data-stu-id="20156-154">For each case, `"Case *"` is hello default name of hello case, which you can rename for readability.</span></span> 
<span data-ttu-id="20156-155">`"case"`Specifica l'etichetta case hello, che hello commutatore utilizzo delle espressioni per il confronto e deve essere un valore costante e univoco.</span><span class="sxs-lookup"><span data-stu-id="20156-155">`"case"` specifies hello case label, which hello switch expression uses for comparison, and must be a constant and unique value.</span></span> <span data-ttu-id="20156-156">Se nessuno dei casi hello corrisponde espressione switch hello, azioni `"default"` vengono eseguite.</span><span class="sxs-lookup"><span data-stu-id="20156-156">If none of hello cases match hello switch expression, actions under `"default"` are executed.</span></span>

## <a name="get-help"></a><span data-ttu-id="20156-157">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="20156-157">Get help</span></span>

<span data-ttu-id="20156-158">in caso di altri utenti le app di logica di Azure, vedere tooask domande e rispondere alle domande visitare hello [forum di Azure logica app](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="20156-158">tooask questions, answer questions, and see what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="20156-159">toohelp migliorare Azure logica App e connettori, votare o inviare idee in hello [sito commenti e suggerimenti dell'utente di Azure logica app](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="20156-159">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="20156-160">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="20156-160">Next steps</span></span>

- <span data-ttu-id="20156-161">Informazioni su come troppo[aggiungere condizioni](logic-apps-use-logic-app-features.md)</span><span class="sxs-lookup"><span data-stu-id="20156-161">Learn how too[add conditions](logic-apps-use-logic-app-features.md)</span></span>
- <span data-ttu-id="20156-162">Informazioni sulla [gestione di errori ed eccezioni](logic-apps-exception-handling.md)</span><span class="sxs-lookup"><span data-stu-id="20156-162">Learn about [error and exception handling](logic-apps-exception-handling.md)</span></span>
- <span data-ttu-id="20156-163">Esplorare altre [funzionalità di linguaggio del flusso di lavoro](logic-apps-author-definitions.md)</span><span class="sxs-lookup"><span data-stu-id="20156-163">Explore more [workflow language capabilities](logic-apps-author-definitions.md)</span></span>