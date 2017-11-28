---
title: Istruzione switch per diverse azioni in app per la logica di Azure | Microsoft Docs
description: Scegliere diverse azioni da eseguire in app per la logica in base ai valori di espressione tramite un'istruzione switch
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
ms.openlocfilehash: 338b6a5b549d7bf81186550295608438ac4aee32
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="perform-different-actions-in-logic-apps-with-a-switch-statement"></a><span data-ttu-id="a3276-104">Eseguire diverse azioni in app per la logica con un'istruzione switch</span><span class="sxs-lookup"><span data-stu-id="a3276-104">Perform different actions in logic apps with a switch statement</span></span>

<span data-ttu-id="a3276-105">Durante la creazione di un flusso di lavoro, è spesso necessario eseguire diverse azioni in base al valore di un oggetto o di un'espressione.</span><span class="sxs-lookup"><span data-stu-id="a3276-105">When authoring a workflow, you often have to take different actions based on the value of an object or expression.</span></span> <span data-ttu-id="a3276-106">Ad esempio, si vuole che l'app per la logica si comporti diversamente in base al codice di stato di una richiesta HTTP o all'opzione selezionata in un messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="a3276-106">For example, you might want your logic app to behave differently based on the status code of an HTTP request, or an option selected in an email.</span></span>

<span data-ttu-id="a3276-107">È possibile usare un'istruzione switch per implementare questi scenari.</span><span class="sxs-lookup"><span data-stu-id="a3276-107">You can use a switch statement to implement these scenarios.</span></span> <span data-ttu-id="a3276-108">Le app per la logica possono valutare un'espressione o un token e scegliere il case con lo stesso valore per eseguire le azioni specificate.</span><span class="sxs-lookup"><span data-stu-id="a3276-108">Your logic app can evaluate a token or expression, and choose the case with the same value to execute the specified actions.</span></span> <span data-ttu-id="a3276-109">All'istruzione switch deve corrispondere un solo caso.</span><span class="sxs-lookup"><span data-stu-id="a3276-109">Only one case should match the switch statement.</span></span>

> [!TIP]
> <span data-ttu-id="a3276-110">Come tutti i linguaggi di programmazione, le istruzioni switch supportano solo gli operatori di uguaglianza.</span><span class="sxs-lookup"><span data-stu-id="a3276-110">Like all programming languages, switch statements support only equality operators.</span></span> <span data-ttu-id="a3276-111">Se sono necessari altri operatori relazionali, ad esempio "maggiore di", usare un'istruzione di condizione.</span><span class="sxs-lookup"><span data-stu-id="a3276-111">If you need other relational operators, such as "greater than", use a condition statement.</span></span>
> <span data-ttu-id="a3276-112">Per garantire il comportamento di esecuzione deterministico, i casi devono contenere un valore univoco e statico anziché un token dinamico o un'espressione.</span><span class="sxs-lookup"><span data-stu-id="a3276-112">To ensure deterministic execution behavior, cases must contain a unique and static value instead of dynamic tokens or expression.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a3276-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a3276-113">Prerequisites</span></span>

- <span data-ttu-id="a3276-114">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="a3276-114">An active Azure subscription.</span></span> <span data-ttu-id="a3276-115">Se non si ha una sottoscrizione di Azure, [creare un account gratuito](https://azure.microsoft.com/free/) o provare l'[App per la logica gratuita](https://tryappservice.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a3276-115">If you don't have an active Azure subscription, [create a free account](https://azure.microsoft.com/free/), or try [Logic Apps for free](https://tryappservice.azure.com/).</span></span>
- [<span data-ttu-id="a3276-116">Conoscenze di base di app per la logica</span><span class="sxs-lookup"><span data-stu-id="a3276-116">Basic knowledge about logic apps</span></span>](logic-apps-what-are-logic-apps.md)

## <a name="add-a-switch-statement-to-your-workflow"></a><span data-ttu-id="a3276-117">Aggiungere un'istruzione switch al flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="a3276-117">Add a switch statement to your workflow</span></span>

<span data-ttu-id="a3276-118">Per illustrare l'uso delle istruzioni switch, questo esempio crea un'app per la logica che monitora i file caricati in Dropbox.</span><span class="sxs-lookup"><span data-stu-id="a3276-118">To show how a switch statement works, this example creates a logic app that monitors files uploaded to Dropbox.</span></span> <span data-ttu-id="a3276-119">Quando i nuovi file vengono caricati, l'app per la logica invia un messaggio di posta elettronica a un revisore che sceglie se trasferire o meno i file a SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a3276-119">When the new files are uploaded, the logic app sends email to an approver who chooses whether to transfer those files to SharePoint.</span></span> <span data-ttu-id="a3276-120">L'app usa un'istruzione switch che esegue diverse azioni in base al valore selezionato dal revisore.</span><span class="sxs-lookup"><span data-stu-id="a3276-120">The app uses a switch statement that performs different actions based on the value that the approver selects.</span></span>

1. <span data-ttu-id="a3276-121">Creare un'app per la logica e selezionare questo trigger: **Dropbox - When a file is created** (Dropbox - Quando viene creato un file).</span><span class="sxs-lookup"><span data-stu-id="a3276-121">Create a logic app, and select this trigger: **Dropbox - When a file is created**.</span></span>

   ![Usare il trigger Dropbox - When a file is created (Dropbox - Quando viene creato un file)](./media/logic-apps-switch-case/dropbox-trigger.jpg)

2. <span data-ttu-id="a3276-123">Sotto il trigger, aggiungere questa azione: **Outlook.com - Invia messaggio di posta elettronica di approvazione**</span><span class="sxs-lookup"><span data-stu-id="a3276-123">Under the trigger, add this action: **Outlook.com - Send approval email**</span></span>

   > [!TIP]
   > <span data-ttu-id="a3276-124">Le app per la logica supportano anche gli scenari di posta elettronica di approvazione da un account di Outlook Office 365.</span><span class="sxs-lookup"><span data-stu-id="a3276-124">Logic apps also support sending approval email scenarios from an Office 365 Outlook account.</span></span>

   - <span data-ttu-id="a3276-125">Se non si ha una connessione esistente, viene richiesto di crearne una.</span><span class="sxs-lookup"><span data-stu-id="a3276-125">If you don't have an existing connection, you're prompted to create one.</span></span>
   - <span data-ttu-id="a3276-126">Compilare i campi obbligatori.</span><span class="sxs-lookup"><span data-stu-id="a3276-126">Fill in the required fields.</span></span> <span data-ttu-id="a3276-127">Ad esempio, sotto **A**, specificare l'indirizzo di posta elettronica per inviare il messaggio di posta elettronica al revisore.</span><span class="sxs-lookup"><span data-stu-id="a3276-127">For example, under **To**, specify the email address for sending the approver email.</span></span>
   - <span data-ttu-id="a3276-128">In **Opzioni utente**, inserire `Approve, Reject`.</span><span class="sxs-lookup"><span data-stu-id="a3276-128">Under **User Options**, enter `Approve, Reject`.</span></span>

   ![Configurare la connessione](./media/logic-apps-switch-case/send-approval-email-action.jpg)

3. <span data-ttu-id="a3276-130">Aggiungere un'istruzione switc.</span><span class="sxs-lookup"><span data-stu-id="a3276-130">Add a switch statement.</span></span>

   - <span data-ttu-id="a3276-131">Selezionare **+ Nuovo passaggio** > **... Altro** > **Aggiungi istruzione switch case**.</span><span class="sxs-lookup"><span data-stu-id="a3276-131">Select **+ New step** > **... More** > **Add a switch case**.</span></span> 
   - <span data-ttu-id="a3276-132">Si vuole ora selezionare l'azione da eseguire in base all'output di `SelectedOptions` dall'azione *Invia messaggio di posta elettronica di approvazione*.</span><span class="sxs-lookup"><span data-stu-id="a3276-132">Now we want to select the action to perform based on the `SelectedOptions` output from the *Send approval email* action.</span></span> 
   <span data-ttu-id="a3276-133">È possibile trovare questo campo nel selettore **Aggiungi contenuto dinamico**.</span><span class="sxs-lookup"><span data-stu-id="a3276-133">You can find this field in the **Add dynamic content** selector.</span></span>
   - <span data-ttu-id="a3276-134">Usare *Case1* per eseguire la gestione quando l'utente seleziona `Approve`.</span><span class="sxs-lookup"><span data-stu-id="a3276-134">Use *Case 1* to handle when the approver selects `Approve`.</span></span>
     - <span data-ttu-id="a3276-135">Se approvato, copiare il file originale in SharePoint Online con l'azione [**SharePoint Online - Crea file**](../connectors/connectors-create-api-sharepointonline.md).</span><span class="sxs-lookup"><span data-stu-id="a3276-135">If approved, copy the original file to SharePoint Online with the [**SharePoint Online - Create file** action](../connectors/connectors-create-api-sharepointonline.md).</span></span>
     - <span data-ttu-id="a3276-136">Aggiungere un'altra azione nel caso per informare gli utenti che un nuovo file è disponibile in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a3276-136">Add another action within the case to notify users that a new file is available on SharePoint.</span></span>
   - <span data-ttu-id="a3276-137">Aggiungere un altro case da gestire quando l'utente seleziona `Reject`.</span><span class="sxs-lookup"><span data-stu-id="a3276-137">Add another case to handle when user selects `Reject`.</span></span>
     - <span data-ttu-id="a3276-138">In caso di rifiuto, inviare un'email di notifica per informare gli altri approvatori che il file è stato rifiutato e non è richiesta alcuna azione successiva.</span><span class="sxs-lookup"><span data-stu-id="a3276-138">If rejected, send a notification email informing other approvers that the file is rejected and no further action is required.</span></span>
   - <span data-ttu-id="a3276-139">Dato che `SelectedOptions` offre solo due opzioni, è possibile lasciare il case vuoto **predefinito**.</span><span class="sxs-lookup"><span data-stu-id="a3276-139">`SelectedOptions` provides only two options, so we can leave the **Default** case empty.</span></span>

   ![Istruzioni switch](./media/logic-apps-switch-case/switch.jpg)

   > [!NOTE]
   > <span data-ttu-id="a3276-141">Le istruzioni switch richiedono almeno un case aggiuntivo oltre al case predefinito.</span><span class="sxs-lookup"><span data-stu-id="a3276-141">A switch statement needs at least one case in addition to the default case.</span></span>

4. <span data-ttu-id="a3276-142">Dopo l'istruzione switch, eliminare il file originale caricato in Dropbox aggiungendo l'azione **Dropbox - Elimina file**</span><span class="sxs-lookup"><span data-stu-id="a3276-142">After the switch statement, delete the original file uploaded to Dropbox by adding this action: **Dropbox - Delete file**</span></span>

5. <span data-ttu-id="a3276-143">Salvare l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="a3276-143">Save your logic app.</span></span> <span data-ttu-id="a3276-144">Testare l'app caricando un file in Dropbox.</span><span class="sxs-lookup"><span data-stu-id="a3276-144">Test your app by uploading a file to Dropbox.</span></span> <span data-ttu-id="a3276-145">Si dovrebbe ricevere in breve tempo un messaggio di posta elettronica di approvazione.</span><span class="sxs-lookup"><span data-stu-id="a3276-145">You should receive an approval email shortly.</span></span> <span data-ttu-id="a3276-146">Selezionare un'opzione e osservare il comportamento.</span><span class="sxs-lookup"><span data-stu-id="a3276-146">Select an option, and observe the behavior.</span></span>

   > [!TIP]
   > <span data-ttu-id="a3276-147">Vedere come [monitorare le app per la logica](logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="a3276-147">Check out how to [monitor your logic apps](logic-apps-monitor-your-logic-apps.md).</span></span>

## <a name="understand-the-code-behind-switch-statements"></a><span data-ttu-id="a3276-148">Capire il codice dietro le istruzioni switch</span><span class="sxs-lookup"><span data-stu-id="a3276-148">Understand the code behind switch statements</span></span>

<span data-ttu-id="a3276-149">Dopo aver creato correttamente un'app per la logica tramite un'istruzione switch, esaminare la definizione del codice dietro l'istruzione switch.</span><span class="sxs-lookup"><span data-stu-id="a3276-149">Now that you successfully created a logic app using a switch statement, let's look at the code definition behind the switch statement.</span></span>

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

* <span data-ttu-id="a3276-150">`"Switch"` è il nome dell'istruzione switch che può essere rinominata per migliorarne la leggibilità.</span><span class="sxs-lookup"><span data-stu-id="a3276-150">`"Switch"` is the name of the switch statement, which you can rename for readability.</span></span> 
* <span data-ttu-id="a3276-151">`"type": "Switch"` indica che l'azione è un'istruzione switch.</span><span class="sxs-lookup"><span data-stu-id="a3276-151">`"type": "Switch"` indicates that the action is a switch statement.</span></span> 
* <span data-ttu-id="a3276-152">`"expression"` è l'opzione selezionata dal revisore in questo esempio e viene valutata in ogni case dichiarato successivamente nella definizione.</span><span class="sxs-lookup"><span data-stu-id="a3276-152">`"expression"` is the approver's selected option in this example and is evaluated against each case declared later in the definition.</span></span> 
* <span data-ttu-id="a3276-153">`"cases"` può contenere qualsiasi numero di case.</span><span class="sxs-lookup"><span data-stu-id="a3276-153">`"cases"` can contain any number of cases.</span></span> <span data-ttu-id="a3276-154">Per ogni case, `"Case *"` è il nome predefinito del case, che è possibile rinominare per migliorare la leggibilità.</span><span class="sxs-lookup"><span data-stu-id="a3276-154">For each case, `"Case *"` is the default name of the case, which you can rename for readability.</span></span> 
<span data-ttu-id="a3276-155">`"case"` specifica l'etichetta di case, che viene usata dall'espressione switch per effettuare un confronto e deve contenere un valore costante e univoco.</span><span class="sxs-lookup"><span data-stu-id="a3276-155">`"case"` specifies the case label, which the switch expression uses for comparison, and must be a constant and unique value.</span></span> <span data-ttu-id="a3276-156">Se nessuno dei case corrisponde all'espressione switch, vengono eseguite le azioni incluse in `"default"`.</span><span class="sxs-lookup"><span data-stu-id="a3276-156">If none of the cases match the switch expression, actions under `"default"` are executed.</span></span>

## <a name="get-help"></a><span data-ttu-id="a3276-157">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="a3276-157">Get help</span></span>

<span data-ttu-id="a3276-158">Per porre domande, fornire risposte e ottenere informazioni sulle attività degli altri utenti delle app per la logica di Azure, vedere il [forum sulle app per la logica di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="a3276-158">To ask questions, answer questions, and see what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="a3276-159">Per contribuire al miglioramento delle App per la logica di Azure e dei connettori, votare o inviare idee al [sito dei commenti e suggerimenti degli utenti di App per la logica di Azure](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="a3276-159">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3276-160">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a3276-160">Next steps</span></span>

- <span data-ttu-id="a3276-161">Informazioni su come [aggiungere condizioni](logic-apps-use-logic-app-features.md)</span><span class="sxs-lookup"><span data-stu-id="a3276-161">Learn how to [add conditions](logic-apps-use-logic-app-features.md)</span></span>
- <span data-ttu-id="a3276-162">Informazioni sulla [gestione di errori ed eccezioni](logic-apps-exception-handling.md)</span><span class="sxs-lookup"><span data-stu-id="a3276-162">Learn about [error and exception handling](logic-apps-exception-handling.md)</span></span>
- <span data-ttu-id="a3276-163">Esplorare altre [funzionalità di linguaggio del flusso di lavoro](logic-apps-author-definitions.md)</span><span class="sxs-lookup"><span data-stu-id="a3276-163">Explore more [workflow language capabilities](logic-apps-author-definitions.md)</span></span>