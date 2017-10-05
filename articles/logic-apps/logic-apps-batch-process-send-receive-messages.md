---
title: Elaborare in batch i messaggi come gruppo o raccolta - App per la logica di Azure | Microsoft Docs
description: Inviare e ricevere messaggi per l'elaborazione in batch nelle app per la logica
keywords: batch, processo batch
author: jonfancey
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/7/2017
ms.author: LADocs; estfan; jonfan
ms.openlocfilehash: 480ffce5dbe7c25181bb0ba5639de884e98ff4e6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="send-receive-and-batch-process-messages-in-logic-apps"></a><span data-ttu-id="fa07b-104">Inviare, ricevere ed elaborare in batch i messaggi nelle app per la logica</span><span class="sxs-lookup"><span data-stu-id="fa07b-104">Send, receive, and batch process messages in logic apps</span></span>

<span data-ttu-id="fa07b-105">Per elaborare i messaggi in gruppi, è possibile inviare elementi di dati o messaggi a un *batch* e quindi elaborarli come batch.</span><span class="sxs-lookup"><span data-stu-id="fa07b-105">To process messages together in groups, you can send data items, or messages, to a *batch*, and then process those items as a batch.</span></span> <span data-ttu-id="fa07b-106">Questo approccio è utile quando si desidera che gli elementi di dati vengano raggruppati secondo una modalità specifica ed elaborati insieme.</span><span class="sxs-lookup"><span data-stu-id="fa07b-106">This approach is useful when you want to make sure data items are grouped in a specific way and are processed together.</span></span> 

<span data-ttu-id="fa07b-107">È possibile creare app per la logica che ricevono gli elementi in batch usando il trigger **Batch**.</span><span class="sxs-lookup"><span data-stu-id="fa07b-107">You can create logic apps that receive items as a batch by using the **Batch** trigger.</span></span> <span data-ttu-id="fa07b-108">È possibile creare quindi app per la logica che inviano elementi a un batch usando l'azione **Batch**.</span><span class="sxs-lookup"><span data-stu-id="fa07b-108">You can then create logic apps that send items to a batch by using the **Batch** action.</span></span>

<span data-ttu-id="fa07b-109">Questo argomento illustra come compilare una soluzione di invio in batch mediante l'esecuzione di queste attività:</span><span class="sxs-lookup"><span data-stu-id="fa07b-109">This topic shows how you can build a batching solution by performing these tasks:</span></span> 

* <span data-ttu-id="fa07b-110">[Creare un'app per la logica che riceve e raccoglie gli elementi in batch](#batch-receiver).</span><span class="sxs-lookup"><span data-stu-id="fa07b-110">[Create a logic app that receives and collects items as a batch](#batch-receiver).</span></span> <span data-ttu-id="fa07b-111">Nell'app per la logica "ricevente il batch" si specificano il nome del batch e i criteri di rilascio da soddisfare perché l'app ricevente rilasci ed elabori gli elementi.</span><span class="sxs-lookup"><span data-stu-id="fa07b-111">This "batch receiver" logic app specifies the batch name and release criteria to meet before the receiver logic app releases and processes items.</span></span> 

* <span data-ttu-id="fa07b-112">[Creare un'app per la logica che invia elementi a un batch](#batch-sender).</span><span class="sxs-lookup"><span data-stu-id="fa07b-112">[Create a logic app that sends items to a batch](#batch-sender).</span></span> <span data-ttu-id="fa07b-113">Nell'app per la logica "mittente del batch" si specifica dove inviare gli elementi. La destinazione degli elementi deve essere un'app per la logica ricevente esistente.</span><span class="sxs-lookup"><span data-stu-id="fa07b-113">This "batch sender" logic app specifies where to send items, which must be an existing batch receiver logic app.</span></span> <span data-ttu-id="fa07b-114">È inoltre possibile specificare una chiave univoca, ad esempio un numero cliente, per "partizionare" o suddividere il batch di destinazione in subset in base alla chiave.</span><span class="sxs-lookup"><span data-stu-id="fa07b-114">You can also specify a unique key, like a customer number, to "partition", or divide, the target batch into subsets based on that key.</span></span> <span data-ttu-id="fa07b-115">Tutti gli elementi con questa chiave verranno così raccolti ed elaborati insieme.</span><span class="sxs-lookup"><span data-stu-id="fa07b-115">That way, all items with that key are collected and processed together.</span></span> 

## <a name="requirements"></a><span data-ttu-id="fa07b-116">Requisiti</span><span class="sxs-lookup"><span data-stu-id="fa07b-116">Requirements</span></span>

<span data-ttu-id="fa07b-117">Per seguire questo esempio, è necessario disporre di questi elementi:</span><span class="sxs-lookup"><span data-stu-id="fa07b-117">To follow this example, you need these items:</span></span>

* <span data-ttu-id="fa07b-118">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="fa07b-118">An Azure subscription.</span></span> <span data-ttu-id="fa07b-119">Se non si ha una sottoscrizione, è possibile [creare un account Azure gratuito](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="fa07b-119">If you don't have a subscription, you can [start with a free Azure account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="fa07b-120">In alternativa, è possibile [iscriversi per ottenere una sottoscrizione con pagamento in base al consumo](https://azure.microsoft.com/pricing/purchase-options/).</span><span class="sxs-lookup"><span data-stu-id="fa07b-120">Otherwise, you can [sign up for a Pay-As-You-Go subscription](https://azure.microsoft.com/pricing/purchase-options/).</span></span>

* <span data-ttu-id="fa07b-121">Conoscenza di base di [come creare le app per la logica](../logic-apps/logic-apps-create-a-logic-app.md)</span><span class="sxs-lookup"><span data-stu-id="fa07b-121">Basic knowledge about [how to create logic apps](../logic-apps/logic-apps-create-a-logic-app.md)</span></span> 

* <span data-ttu-id="fa07b-122">Un account di posta elettronica con un [provider di posta elettronica supportato da App per la logica di Azure](../connectors/apis-list.md)</span><span class="sxs-lookup"><span data-stu-id="fa07b-122">An email account with any [email provider supported by Azure Logic Apps](../connectors/apis-list.md)</span></span>

<a name="batch-receiver"></a>

## <a name="create-logic-apps-that-receive-messages-as-a-batch"></a><span data-ttu-id="fa07b-123">Creare app per la logica che ricevono messaggi in batch</span><span class="sxs-lookup"><span data-stu-id="fa07b-123">Create logic apps that receive messages as a batch</span></span>

<span data-ttu-id="fa07b-124">Prima di poter inviare messaggi a un batch, è necessario creare un'app per la logica "ricevente il batch" con il trigger **Batch**.</span><span class="sxs-lookup"><span data-stu-id="fa07b-124">Before you can send messages to a batch, you must first create a "batch receiver" logic app with the **Batch** trigger.</span></span> <span data-ttu-id="fa07b-125">Sarà possibile in questo modo selezionare questa app ricevente quando si creerà l'app per la logica mittente.</span><span class="sxs-lookup"><span data-stu-id="fa07b-125">That way, you can select this receiver logic app when you create the sender logic app.</span></span> <span data-ttu-id="fa07b-126">Nell'app ricevente occorre specificare il nome del batch, i criteri di rilascio e altre impostazioni.</span><span class="sxs-lookup"><span data-stu-id="fa07b-126">For the receiver, you specify the batch name, release criteria, and other settings.</span></span> 

<span data-ttu-id="fa07b-127">Nelle app per la logica mittenti è necessario specificare dove inviare gli elementi, mentre in quelle riceventi non è necessario aggiungere informazioni sulle app mittenti.</span><span class="sxs-lookup"><span data-stu-id="fa07b-127">Sender logic apps need know where to send items, while receiver logic apps don't need to know anything about the senders.</span></span>

1. <span data-ttu-id="fa07b-128">Nel [portale di Azure](https://portal.azure.com) creare un'app per la logica con questo nome: "BatchReceiver"</span><span class="sxs-lookup"><span data-stu-id="fa07b-128">In the [Azure portal](https://portal.azure.com), create a logic app with this name: "BatchReceiver"</span></span> 

2. <span data-ttu-id="fa07b-129">Nella finestra Progettazione app per la logica aggiungere il trigger **batch**, che avvia il flusso di lavoro dell'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="fa07b-129">In Logic Apps Designer, add the **Batch** trigger, which starts your logic app workflow.</span></span> <span data-ttu-id="fa07b-130">Nella casella di ricerca digitare "batch" come filtro.</span><span class="sxs-lookup"><span data-stu-id="fa07b-130">In the search box, enter "batch" as your filter.</span></span> <span data-ttu-id="fa07b-131">Selezionare il trigger: **Batch - Messaggi batch**</span><span class="sxs-lookup"><span data-stu-id="fa07b-131">Select this trigger: **Batch – Batch messages**</span></span>

   ![Aggiungere il trigger Batch](./media/logic-apps-batch-process-send-receive-messages/add-batch-receiver-trigger.png)

3. <span data-ttu-id="fa07b-133">Specificare un nome per il batch e specificare i criteri per il rilascio del batch, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="fa07b-133">Provide a name for the batch, and specify criteria for releasing the batch, for example:</span></span>

   * <span data-ttu-id="fa07b-134">**Nome batch**: il nome usato per identificare il batch, in questo esempio "TestBatch".</span><span class="sxs-lookup"><span data-stu-id="fa07b-134">**Batch Name**: The name used to identify the batch, which is "TestBatch" in this example.</span></span>
   * <span data-ttu-id="fa07b-135">**Numero messaggi**: il numero di messaggi da inserire in un batch prima del rilascio per l'elaborazione, in questo esempio "5".</span><span class="sxs-lookup"><span data-stu-id="fa07b-135">**Message Count**: The number of messages to hold as a batch before releasing for processing, which is "5" in this example.</span></span>

   ![Specificare i dettagli del trigger Batch](./media/logic-apps-batch-process-send-receive-messages/receive-batch-trigger-details.png)

4. <span data-ttu-id="fa07b-137">Aggiungere un'altra azione che invia un messaggio di posta elettronica quando viene attivato il trigger Batch.</span><span class="sxs-lookup"><span data-stu-id="fa07b-137">Add another action that sends an email when the batch trigger fires.</span></span> <span data-ttu-id="fa07b-138">Ogni volta che il batch contiene cinque elementi, l'app per la logica invia un messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="fa07b-138">Each time the batch has five items, the logic app sends an email.</span></span>

   1. <span data-ttu-id="fa07b-139">Nel trigger batch scegliere **+ Nuovo passaggio** > **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="fa07b-139">Under the batch trigger, choose **+ New Step** > **Add an action**.</span></span>

   2. <span data-ttu-id="fa07b-140">Nella casella di ricerca digitare "email" come filtro.</span><span class="sxs-lookup"><span data-stu-id="fa07b-140">In the search box, enter "email" as your filter.</span></span>
   <span data-ttu-id="fa07b-141">In base al provider di posta elettronica in uso, selezionare un connettore di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="fa07b-141">Based on your email provider, select an email connector.</span></span>
   
      <span data-ttu-id="fa07b-142">Se si dispone, ad esempio, di un account aziendale o dell'istituto di istruzione, selezionare il connettore Office 365 Outlook.</span><span class="sxs-lookup"><span data-stu-id="fa07b-142">For example, if you have a work or school account, select the Office 365 Outlook connector.</span></span> 
      <span data-ttu-id="fa07b-143">Se si dispone di un account Gmail, selezionare il connettore Gmail.</span><span class="sxs-lookup"><span data-stu-id="fa07b-143">If you have a Gmail account, select the Gmail connector.</span></span>

   3. <span data-ttu-id="fa07b-144">Selezionare questa azione per il connettore: **{*provider di posta elettronica*} - Invia messaggio di posta elettronica**,</span><span class="sxs-lookup"><span data-stu-id="fa07b-144">Select this action for your connector: **{*email provider*} - Send an email**</span></span>

      <span data-ttu-id="fa07b-145">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="fa07b-145">For example:</span></span>

      ![Selezionare l'azione "Invia un messaggio di posta elettronica" per il provider di posta elettronica](./media/logic-apps-batch-process-send-receive-messages/add-send-email-action.png)

5. <span data-ttu-id="fa07b-147">Se non è stata creata prima una connessione per il provider di posta elettronica, immettere al prompt le credenziali per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="fa07b-147">If you didn't previously create a connection for your email provider, provide your email credentials for authentication when prompted.</span></span> <span data-ttu-id="fa07b-148">Leggere altre informazioni sull'[autenticazione delle credenziali di posta elettronica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="fa07b-148">Learn more about [authenticating your email credentials](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

6. <span data-ttu-id="fa07b-149">Impostare le proprietà per l'azione appena aggiunta.</span><span class="sxs-lookup"><span data-stu-id="fa07b-149">Set the properties for the action you just added.</span></span>

   * <span data-ttu-id="fa07b-150">Nella casella **A** immettere l'indirizzo di posta elettronica del destinatario.</span><span class="sxs-lookup"><span data-stu-id="fa07b-150">In the **To** box, enter the recipient's email address.</span></span> 
   <span data-ttu-id="fa07b-151">AI fini del test delle app è possibile indicare il proprio indirizzo di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="fa07b-151">For testing purposes, you can use your own email address.</span></span>

   * <span data-ttu-id="fa07b-152">Nella casella **Oggetto**, quando viene visualizzato l'elenco **Contenuto dinamico**, selezionare il campo **Nome partizione**.</span><span class="sxs-lookup"><span data-stu-id="fa07b-152">In the **Subject** box, when the **Dynamic content** list appears, select the **Partition Name** field.</span></span>

     ![Nell'elenco "Contenuto dinamico" selezionare "Nome partizione"](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details.png)

     <span data-ttu-id="fa07b-154">In una sezione più avanti si specificherà una chiave di partizione univoca che divide il batch di destinazione in set logici a cui inviare i messaggi.</span><span class="sxs-lookup"><span data-stu-id="fa07b-154">In a later section, you can specify a unique partition key that divides the target batch into logical sets to where you can send messages.</span></span> 
     <span data-ttu-id="fa07b-155">Ogni set è associato a un numero univoco che viene generato dall'app per la logica mittente.</span><span class="sxs-lookup"><span data-stu-id="fa07b-155">Each set has a unique number that's generated by the sender logic app.</span></span> 
     <span data-ttu-id="fa07b-156">Questa funzionalità consente di usare un unico batch con più subset e di assegnare a ogni subset il nome desiderato.</span><span class="sxs-lookup"><span data-stu-id="fa07b-156">This capability lets you use a single batch with multiple subsets and define each subset with the name that you provide.</span></span>

   * <span data-ttu-id="fa07b-157">Nella casella **Corpo**, quando viene visualizzato l'elenco **Contenuto dinamico**, selezionare il campo **ID messaggio**.</span><span class="sxs-lookup"><span data-stu-id="fa07b-157">In the **Body** box, when the **Dynamic content** list appears, select the **Message Id** field.</span></span>

     ![Per la casella "Body" selezionare "ID messaggio"](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details-for-each.png)

     <span data-ttu-id="fa07b-159">Poiché l'input per l'azione di invio del messaggio di posta elettronica è una matrice, la finestra di progettazione aggiunge automaticamente un ciclo **For each** per l'azione **Invia un messaggio di posta elettronica**.</span><span class="sxs-lookup"><span data-stu-id="fa07b-159">Because the input for the send email action is an array, the designer automatically adds a **For each** loop around the **Send an email** action.</span></span> 
     <span data-ttu-id="fa07b-160">Questo ciclo esegue l'azione interna su ogni elemento nel batch.</span><span class="sxs-lookup"><span data-stu-id="fa07b-160">This loop performs the inner action on each item in the batch.</span></span> 
     <span data-ttu-id="fa07b-161">Con il trigger batch impostato su cinque elementi, si ottengono quindi cinque messaggi di posta elettronica ogni volta che viene attivato il trigger.</span><span class="sxs-lookup"><span data-stu-id="fa07b-161">So, with the batch trigger set to five items, you get five emails each time the trigger fires.</span></span>

7.  <span data-ttu-id="fa07b-162">Ora che è stata creata un'app per la logica ricevente, occorre salvarla.</span><span class="sxs-lookup"><span data-stu-id="fa07b-162">Now that you created a batch receiver logic app, save your logic app.</span></span>

    ![Salvare l'app per la logica](./media/logic-apps-batch-process-send-receive-messages/save-batch-receiver-logic-app.png)

<a name="batch-sender"></a>

## <a name="create-logic-apps-that-send-messages-to-a-batch"></a><span data-ttu-id="fa07b-164">Creare app per la logica che inviano messaggi a un batch</span><span class="sxs-lookup"><span data-stu-id="fa07b-164">Create logic apps that send messages to a batch</span></span>

<span data-ttu-id="fa07b-165">Creare a questo punto una o più app per la logica che inviano elementi al batch definito dall'app per la logica ricevente.</span><span class="sxs-lookup"><span data-stu-id="fa07b-165">Now create one or more logic apps that send items to the batch defined by the receiver logic app.</span></span> <span data-ttu-id="fa07b-166">Nell'app mittente specificare il nome del batch e dell'app per la logica ricevente, il contenuto del messaggio ed eventuali altre impostazioni.</span><span class="sxs-lookup"><span data-stu-id="fa07b-166">For the sender, you specify the receiver logic app and batch name, message content, and any other settings.</span></span> <span data-ttu-id="fa07b-167">È possibile specificare anche una chiave di partizione univoca per dividere il batch in subset che raccolgano gli elementi a cui è assegnata tale chiave.</span><span class="sxs-lookup"><span data-stu-id="fa07b-167">You can optionally provide a unique partition key to divide the batch into subsets to collect items with that key.</span></span>

<span data-ttu-id="fa07b-168">Nelle app per la logica mittenti è necessario specificare dove inviare gli elementi, mentre in quelle riceventi non è necessario aggiungere informazioni sulle app mittenti.</span><span class="sxs-lookup"><span data-stu-id="fa07b-168">Sender logic apps need know where to send items, while receiver logic apps don't need to know anything about the senders.</span></span>

1. <span data-ttu-id="fa07b-169">Creare un'altra app per la logica con questo nome: "BatchSender"</span><span class="sxs-lookup"><span data-stu-id="fa07b-169">Create another logic app with this name: "BatchSender"</span></span>

   1. <span data-ttu-id="fa07b-170">Nella casella di ricerca digitare "ricorrenza" come filtro.</span><span class="sxs-lookup"><span data-stu-id="fa07b-170">In the search box, enter "recurrence" as your filter.</span></span> 
   <span data-ttu-id="fa07b-171">Selezionare il trigger **Pianificazione - Ricorrenza**</span><span class="sxs-lookup"><span data-stu-id="fa07b-171">Select this trigger: **Schedule - Recurrence**</span></span>

      ![Aggiungere il trigger "Pianificazione - Ricorrenza"](./media/logic-apps-batch-process-send-receive-messages/add-schedule-trigger-batch-receiver.png)

   2. <span data-ttu-id="fa07b-173">Impostare la frequenza e l'intervallo in modo da eseguire l'app per la logica mittente ogni minuto.</span><span class="sxs-lookup"><span data-stu-id="fa07b-173">Set the frequency and interval to run the sender logic app every minute.</span></span>

      ![Impostare la frequenza e l'intervallo del trigger di ricorrenza](./media/logic-apps-batch-process-send-receive-messages/recurrence-trigger-batch-receiver-details.png)

2. <span data-ttu-id="fa07b-175">Aggiungere un nuovo passaggio per l'invio di messaggi a un batch.</span><span class="sxs-lookup"><span data-stu-id="fa07b-175">Add a new step for sending messages to a batch.</span></span>

   1. <span data-ttu-id="fa07b-176">Nel trigger ricorrenza scegliere **+ Nuovo passaggio** > **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="fa07b-176">Under the recurrence trigger, choose **+ New Step** > **Add an action**.</span></span>

   2. <span data-ttu-id="fa07b-177">Nella casella di ricerca digitare "batch" come filtro.</span><span class="sxs-lookup"><span data-stu-id="fa07b-177">In the search box, enter "batch" as your filter.</span></span> 

   3. <span data-ttu-id="fa07b-178">Selezionare l'azione **Invia messaggi al batch - Scegliere un flusso di lavoro delle app per la logica con un trigger batch**</span><span class="sxs-lookup"><span data-stu-id="fa07b-178">Select this action: **Send messages to batch – Choose a Logic Apps workflow with batch trigger**</span></span>

      ![Selezionare "Invia messaggi al batch"](./media/logic-apps-batch-process-send-receive-messages/send-messages-batch-action.png)

   4. <span data-ttu-id="fa07b-180">Selezionare a questo punto l'app per la logica "BatchReceiver" creata in precedenza, che ora viene visualizzata sotto forma di azione.</span><span class="sxs-lookup"><span data-stu-id="fa07b-180">Now select your "BatchReceiver" logic app that you previously created, which now appears as an action.</span></span>

      ![Selezionare l'app per la logica "ricevente il batch"](./media/logic-apps-batch-process-send-receive-messages/send-batch-select-batch-receiver.png)

      > [!NOTE]
      > <span data-ttu-id="fa07b-182">L'elenco mostra anche tutte le altre app per la logica che dispongono di trigger batch.</span><span class="sxs-lookup"><span data-stu-id="fa07b-182">The list also shows any other logic apps that have batch triggers.</span></span>

3. <span data-ttu-id="fa07b-183">Impostare le proprietà del batch.</span><span class="sxs-lookup"><span data-stu-id="fa07b-183">Set the batch properties.</span></span>

   * <span data-ttu-id="fa07b-184">**Nome batch**: il nome del batch definito dall'app per la logica ricevente, che in questo esempio è "TestBatch" e viene convalidato in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="fa07b-184">**Batch Name**: The batch name defined by the receiver logic app, which is "TestBatch" in this example and is validated at runtime.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="fa07b-185">Assicurarsi di non modificare il nome del batch in quanto deve corrispondere al nome batch specificato dall'app per la logica ricevente.</span><span class="sxs-lookup"><span data-stu-id="fa07b-185">Make sure that you don't change the batch name, which must match the batch name that's specified by the receiver logic app.</span></span>
     > <span data-ttu-id="fa07b-186">Se si modifica il nome del batch, l'esecuzione dell'app per la logica mittente ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="fa07b-186">Changing the batch name causes the sender logic app to fail.</span></span>

   * <span data-ttu-id="fa07b-187">**Contenuto messaggio**: il contenuto del messaggio che si desidera inviare.</span><span class="sxs-lookup"><span data-stu-id="fa07b-187">**Message Content**: The message content that you want to send.</span></span> 
   <span data-ttu-id="fa07b-188">Per questo esempio aggiungere questa espressione che inserisce la data e l'ora correnti nel contenuto del messaggio da inviare al batch:</span><span class="sxs-lookup"><span data-stu-id="fa07b-188">For this example, add this expression that inserts the current date and time into the message content that you send to the batch:</span></span>

     1. <span data-ttu-id="fa07b-189">Quando viene visualizzato l'elenco **Contenuto dinamico**, scegliere **Espressione**.</span><span class="sxs-lookup"><span data-stu-id="fa07b-189">When the **Dynamic content** list appears, choose **Expression**.</span></span> 
     2. <span data-ttu-id="fa07b-190">Immettere l'espressione **utcnow()** e scegliere **OK**.</span><span class="sxs-lookup"><span data-stu-id="fa07b-190">Enter the expression **utcnow()**, and choose **OK**.</span></span> 

        ![In "Contenuto messaggio" scegliere "Espressione".](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details.png)

4. <span data-ttu-id="fa07b-193">Configurare a questo punto una partizione per il batch.</span><span class="sxs-lookup"><span data-stu-id="fa07b-193">Now set up a partition for the batch.</span></span> <span data-ttu-id="fa07b-194">Nell'azione "BatchReceiver" scegliere **Mostra opzioni avanzate**.</span><span class="sxs-lookup"><span data-stu-id="fa07b-194">In the "BatchReceiver" action, choose **Show advanced options**.</span></span>

   * <span data-ttu-id="fa07b-195">**Nome partizione**: una chiave di partizione univoca facoltativa da usare per la suddivisione del batch di destinazione.</span><span class="sxs-lookup"><span data-stu-id="fa07b-195">**Partition Name**: An optional unique partition key to use for dividing the target batch.</span></span> <span data-ttu-id="fa07b-196">Per questo esempio aggiungere un'espressione che genera un numero casuale compreso tra uno e cinque.</span><span class="sxs-lookup"><span data-stu-id="fa07b-196">For this example, add an expression that generates a random number between one and five.</span></span>
   
     1. <span data-ttu-id="fa07b-197">Quando viene visualizzato l'elenco **Contenuto dinamico**, scegliere **Espressione**.</span><span class="sxs-lookup"><span data-stu-id="fa07b-197">When the **Dynamic content** list appears, choose **Expression**.</span></span>
     2. <span data-ttu-id="fa07b-198">Immettere l'espressione **rand(1,6)**</span><span class="sxs-lookup"><span data-stu-id="fa07b-198">Enter this expression: **rand(1,6)**</span></span>

        ![Configurare una partizione per il batch di destinazione](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-partition-advanced-options.png)

        <span data-ttu-id="fa07b-200">Questa funzione **rand** genera un numero compreso tra uno e cinque.</span><span class="sxs-lookup"><span data-stu-id="fa07b-200">This **rand** function generates a number between one and five.</span></span> 
        <span data-ttu-id="fa07b-201">Si divide pertanto il batch in cinque partizioni numerate, che questa espressione imposta in modo dinamico.</span><span class="sxs-lookup"><span data-stu-id="fa07b-201">So you are dividing this batch into five numbered partitions, which this expression dynamically sets.</span></span>

   * <span data-ttu-id="fa07b-202">**ID messaggio**: un identificatore di messaggio facoltativo e GUID generato quando vuoto.</span><span class="sxs-lookup"><span data-stu-id="fa07b-202">**Message Id**: An optional message identifier and is a generated GUID when empty.</span></span> 
   <span data-ttu-id="fa07b-203">Per questo esempio lasciare vuota questa casella.</span><span class="sxs-lookup"><span data-stu-id="fa07b-203">For this example, leave this box blank.</span></span>

5. <span data-ttu-id="fa07b-204">Salvare l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="fa07b-204">Save your logic app.</span></span> <span data-ttu-id="fa07b-205">L'app per la logica appare ora simile a questo esempio:</span><span class="sxs-lookup"><span data-stu-id="fa07b-205">Your sender logic app now looks similar to this example:</span></span>

   ![Salvare l'app per la logica mittente](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details-finished.png)

## <a name="test-your-logic-apps"></a><span data-ttu-id="fa07b-207">Testare le app per la logica</span><span class="sxs-lookup"><span data-stu-id="fa07b-207">Test your logic apps</span></span>

<span data-ttu-id="fa07b-208">Per testare la soluzione per l'invio in batch, lasciare in esecuzione le app per la logica per alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="fa07b-208">To test your batching solution, leave your logic apps running for a few minutes.</span></span> <span data-ttu-id="fa07b-209">Si inizierà presto a ricevere messaggi di posta elettronica a gruppi di cinque, tutti con la stessa chiave di partizione.</span><span class="sxs-lookup"><span data-stu-id="fa07b-209">Soon, you start getting emails in groups of five, all with the same partition key.</span></span>

<span data-ttu-id="fa07b-210">L'app per la logica BatchSender viene eseguita ogni minuto, genera un numero casuale compreso tra uno e cinque e lo usa come chiave di partizione per il batch di destinazione a cui vengono inviati i messaggi.</span><span class="sxs-lookup"><span data-stu-id="fa07b-210">Your BatchSender logic app runs every minute, generates a random number between one and five, and uses this generated number as the partition key for the target batch where messages are sent.</span></span> <span data-ttu-id="fa07b-211">Ogni volta che il batch contiene cinque elementi con la stessa chiave di partizione, l'app per la logica BatchReceiver si attiva e invia posta elettronica per ogni messaggio.</span><span class="sxs-lookup"><span data-stu-id="fa07b-211">Each time the batch has five items with the same partition key, your BatchReceiver logic app fires and sends mail for each message.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fa07b-212">Al termine dei test, assicurarsi di disabilitare l'app per la logica BatchSender per arrestare l'invio di messaggi ed evitare il sovraccarico della casella di posta in arrivo.</span><span class="sxs-lookup"><span data-stu-id="fa07b-212">When you're done testing, make sure that you disable the BatchSender logic app to stop sending messages and avoid overloading your inbox.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa07b-213">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fa07b-213">Next steps</span></span>

* <span data-ttu-id="fa07b-214">[Build on logic app definitions by using JSON](../logic-apps/logic-apps-author-definitions.md) (Compilare definizioni di app per la logica on JSON)</span><span class="sxs-lookup"><span data-stu-id="fa07b-214">[Build on logic app definitions by using JSON](../logic-apps/logic-apps-author-definitions.md)</span></span>
* [<span data-ttu-id="fa07b-215">Compilare un'app senza server in Visual Studio con App per la logica e Funzioni</span><span class="sxs-lookup"><span data-stu-id="fa07b-215">Build a serverless app in Visual Studio with Azure Logic Apps and Functions</span></span>](../logic-apps/logic-apps-serverless-get-started-vs.md)
* [<span data-ttu-id="fa07b-216">Gestione delle eccezioni e registrazione degli errori per le app per la logica</span><span class="sxs-lookup"><span data-stu-id="fa07b-216">Exception handling and error logging for logic apps</span></span>](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
