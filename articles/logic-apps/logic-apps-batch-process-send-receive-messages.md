---
title: aaaBatch elaborare i messaggi a un gruppo o raccolta - App Azure per la logica | Documenti Microsoft
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
ms.openlocfilehash: 2603db71ee0659d5b6bf5ce3d32f1b0d13c34194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="send-receive-and-batch-process-messages-in-logic-apps"></a><span data-ttu-id="fa2ec-104">Inviare, ricevere ed elaborare in batch i messaggi nelle app per la logica</span><span class="sxs-lookup"><span data-stu-id="fa2ec-104">Send, receive, and batch process messages in logic apps</span></span>

<span data-ttu-id="fa2ec-105">messaggi tooprocess riuniti in gruppi, è possibile inviare dati elementi o i messaggi, tooa *batch*e quindi elaborare tali elementi come un batch.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-105">tooprocess messages together in groups, you can send data items, or messages, tooa *batch*, and then process those items as a batch.</span></span> <span data-ttu-id="fa2ec-106">Questo approccio è utile quando si desidera toomake gli elementi di dati che vengono raggruppati in modo specifico e vengono elaborati insieme.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-106">This approach is useful when you want toomake sure data items are grouped in a specific way and are processed together.</span></span> 

<span data-ttu-id="fa2ec-107">È possibile creare App per la logica che ricevono gli elementi come un batch utilizzando hello **Batch** trigger.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-107">You can create logic apps that receive items as a batch by using hello **Batch** trigger.</span></span> <span data-ttu-id="fa2ec-108">È quindi possibile creare App per la logica che inviano elementi tooa batch utilizzando hello **Batch** azione.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-108">You can then create logic apps that send items tooa batch by using hello **Batch** action.</span></span>

<span data-ttu-id="fa2ec-109">Questo argomento illustra come compilare una soluzione di invio in batch mediante l'esecuzione di queste attività:</span><span class="sxs-lookup"><span data-stu-id="fa2ec-109">This topic shows how you can build a batching solution by performing these tasks:</span></span> 

* <span data-ttu-id="fa2ec-110">[Creare un'app per la logica che riceve e raccoglie gli elementi in batch](#batch-receiver).</span><span class="sxs-lookup"><span data-stu-id="fa2ec-110">[Create a logic app that receives and collects items as a batch](#batch-receiver).</span></span> <span data-ttu-id="fa2ec-111">Questa app "ricevitore batch" per la logica specifica hello batch nome e la versione criteri toomeet prima hello ricevitore logica app rilascia ed elabora gli elementi.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-111">This "batch receiver" logic app specifies hello batch name and release criteria toomeet before hello receiver logic app releases and processes items.</span></span> 

* <span data-ttu-id="fa2ec-112">[Creare un'app di logica che invia gli elementi tooa batch](#batch-sender).</span><span class="sxs-lookup"><span data-stu-id="fa2ec-112">[Create a logic app that sends items tooa batch](#batch-sender).</span></span> <span data-ttu-id="fa2ec-113">Questa app "mittente batch" per la logica specifica dove toosend elementi, che devono essere un'app di logica di ricevitore batch esistente.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-113">This "batch sender" logic app specifies where toosend items, which must be an existing batch receiver logic app.</span></span> <span data-ttu-id="fa2ec-114">Si può inoltre specificare una chiave univoca, ad esempio un numero cliente, troppo "partizione" o divide, batch di destinazione hello in subset in base a tale chiave.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-114">You can also specify a unique key, like a customer number, too"partition", or divide, hello target batch into subsets based on that key.</span></span> <span data-ttu-id="fa2ec-115">Tutti gli elementi con questa chiave verranno così raccolti ed elaborati insieme.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-115">That way, all items with that key are collected and processed together.</span></span> 

## <a name="requirements"></a><span data-ttu-id="fa2ec-116">Requisiti</span><span class="sxs-lookup"><span data-stu-id="fa2ec-116">Requirements</span></span>

<span data-ttu-id="fa2ec-117">toofollow in questo esempio, è necessario di questi elementi:</span><span class="sxs-lookup"><span data-stu-id="fa2ec-117">toofollow this example, you need these items:</span></span>

* <span data-ttu-id="fa2ec-118">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-118">An Azure subscription.</span></span> <span data-ttu-id="fa2ec-119">Se non si ha una sottoscrizione, è possibile [creare un account Azure gratuito](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="fa2ec-119">If you don't have a subscription, you can [start with a free Azure account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="fa2ec-120">In alternativa, è possibile [iscriversi per ottenere una sottoscrizione con pagamento in base al consumo](https://azure.microsoft.com/pricing/purchase-options/).</span><span class="sxs-lookup"><span data-stu-id="fa2ec-120">Otherwise, you can [sign up for a Pay-As-You-Go subscription](https://azure.microsoft.com/pricing/purchase-options/).</span></span>

* <span data-ttu-id="fa2ec-121">Conoscenza di base [come toocreate logica App](../logic-apps/logic-apps-create-a-logic-app.md)</span><span class="sxs-lookup"><span data-stu-id="fa2ec-121">Basic knowledge about [how toocreate logic apps](../logic-apps/logic-apps-create-a-logic-app.md)</span></span> 

* <span data-ttu-id="fa2ec-122">Un account di posta elettronica con un [provider di posta elettronica supportato da App per la logica di Azure](../connectors/apis-list.md)</span><span class="sxs-lookup"><span data-stu-id="fa2ec-122">An email account with any [email provider supported by Azure Logic Apps](../connectors/apis-list.md)</span></span>

<a name="batch-receiver"></a>

## <a name="create-logic-apps-that-receive-messages-as-a-batch"></a><span data-ttu-id="fa2ec-123">Creare app per la logica che ricevono messaggi in batch</span><span class="sxs-lookup"><span data-stu-id="fa2ec-123">Create logic apps that receive messages as a batch</span></span>

<span data-ttu-id="fa2ec-124">Prima di poter inviare batch di messaggi tooa, è innanzitutto necessario creare un'app di logica "ricevitore batch" con hello **Batch** trigger.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-124">Before you can send messages tooa batch, you must first create a "batch receiver" logic app with hello **Batch** trigger.</span></span> <span data-ttu-id="fa2ec-125">In questo modo, quando si crea un'app di hello mittente logica, è possibile selezionare questa app logica ricevitore.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-125">That way, you can select this receiver logic app when you create hello sender logic app.</span></span> <span data-ttu-id="fa2ec-126">Per i ricevitori di hello, specificare nome batch hello, criteri di rilascio e altre impostazioni.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-126">For hello receiver, you specify hello batch name, release criteria, and other settings.</span></span> 

<span data-ttu-id="fa2ec-127">Mittente logica App necessario sapere dove gli elementi toosend, mentre ricevitore logica App non è necessario tooknow qualsiasi valore sulla mittenti hello.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-127">Sender logic apps need know where toosend items, while receiver logic apps don't need tooknow anything about hello senders.</span></span>

1. <span data-ttu-id="fa2ec-128">In hello [portale di Azure](https://portal.azure.com), creare un'app logica con questo nome: "BatchReceiver"</span><span class="sxs-lookup"><span data-stu-id="fa2ec-128">In hello [Azure portal](https://portal.azure.com), create a logic app with this name: "BatchReceiver"</span></span> 

2. <span data-ttu-id="fa2ec-129">Nella finestra di progettazione di logica di App, aggiungere hello **Batch** trigger, che avvia il flusso di lavoro logica app.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-129">In Logic Apps Designer, add hello **Batch** trigger, which starts your logic app workflow.</span></span> <span data-ttu-id="fa2ec-130">Nella casella di ricerca hello, immettere "batch" come filtro.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-130">In hello search box, enter "batch" as your filter.</span></span> <span data-ttu-id="fa2ec-131">Selezionare il trigger: **Batch - Messaggi batch**</span><span class="sxs-lookup"><span data-stu-id="fa2ec-131">Select this trigger: **Batch – Batch messages**</span></span>

   ![Aggiungere il trigger Batch](./media/logic-apps-batch-process-send-receive-messages/add-batch-receiver-trigger.png)

3. <span data-ttu-id="fa2ec-133">Specificare un nome per il batch di hello e specificare i criteri per il rilascio di batch di hello, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="fa2ec-133">Provide a name for hello batch, and specify criteria for releasing hello batch, for example:</span></span>

   * <span data-ttu-id="fa2ec-134">**Nome batch**: hello nome utilizzato tooidentify hello batch, ovvero "TestBatch" in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-134">**Batch Name**: hello name used tooidentify hello batch, which is "TestBatch" in this example.</span></span>
   * <span data-ttu-id="fa2ec-135">**Numero di messaggi**: hello numero di messaggi toohold come un batch prima del rilascio per l'elaborazione, ovvero "5" in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-135">**Message Count**: hello number of messages toohold as a batch before releasing for processing, which is "5" in this example.</span></span>

   ![Specificare i dettagli del trigger Batch](./media/logic-apps-batch-process-send-receive-messages/receive-batch-trigger-details.png)

4. <span data-ttu-id="fa2ec-137">Aggiungere un'altra azione che invia un messaggio di posta elettronica quando viene attivato il trigger di batch hello.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-137">Add another action that sends an email when hello batch trigger fires.</span></span> <span data-ttu-id="fa2ec-138">Ogni batch di hello ora ha cinque elementi, hello logica app invia un messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-138">Each time hello batch has five items, hello logic app sends an email.</span></span>

   1. <span data-ttu-id="fa2ec-139">In trigger batch hello, scegliere **+ nuovo passaggio** > **aggiungere un'azione**.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-139">Under hello batch trigger, choose **+ New Step** > **Add an action**.</span></span>

   2. <span data-ttu-id="fa2ec-140">Nella casella di ricerca hello, immettere "email" come filtro.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-140">In hello search box, enter "email" as your filter.</span></span>
   <span data-ttu-id="fa2ec-141">In base al provider di posta elettronica in uso, selezionare un connettore di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-141">Based on your email provider, select an email connector.</span></span>
   
      <span data-ttu-id="fa2ec-142">Ad esempio, se si dispone di un account aziendale o dell'istituto di istruzione, selezionare il connettore di Office 365 Outlook hello.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-142">For example, if you have a work or school account, select hello Office 365 Outlook connector.</span></span> 
      <span data-ttu-id="fa2ec-143">Se si dispone di un account Gmail, selezionare il connettore di Gmail hello.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-143">If you have a Gmail account, select hello Gmail connector.</span></span>

   3. <span data-ttu-id="fa2ec-144">Selezionare questa azione per il connettore: **{*provider di posta elettronica*} - Invia messaggio di posta elettronica**,</span><span class="sxs-lookup"><span data-stu-id="fa2ec-144">Select this action for your connector: **{*email provider*} - Send an email**</span></span>

      <span data-ttu-id="fa2ec-145">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="fa2ec-145">For example:</span></span>

      ![Selezionare l'azione "Invia un messaggio di posta elettronica" per il provider di posta elettronica](./media/logic-apps-batch-process-send-receive-messages/add-send-email-action.png)

5. <span data-ttu-id="fa2ec-147">Se non è stata creata prima una connessione per il provider di posta elettronica, immettere al prompt le credenziali per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-147">If you didn't previously create a connection for your email provider, provide your email credentials for authentication when prompted.</span></span> <span data-ttu-id="fa2ec-148">Leggere altre informazioni sull'[autenticazione delle credenziali di posta elettronica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="fa2ec-148">Learn more about [authenticating your email credentials](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

6. <span data-ttu-id="fa2ec-149">Impostare le proprietà hello azione hello che appena aggiunto.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-149">Set hello properties for hello action you just added.</span></span>

   * <span data-ttu-id="fa2ec-150">In hello **a** , immettere l'indirizzo di posta elettronica del destinatario hello.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-150">In hello **To** box, enter hello recipient's email address.</span></span> 
   <span data-ttu-id="fa2ec-151">AI fini del test delle app è possibile indicare il proprio indirizzo di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-151">For testing purposes, you can use your own email address.</span></span>

   * <span data-ttu-id="fa2ec-152">In hello **soggetto** casella quando hello **contenuto dinamico** viene visualizzato l'elenco, selezionare hello **nome partizione** campo.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-152">In hello **Subject** box, when hello **Dynamic content** list appears, select hello **Partition Name** field.</span></span>

     ![Selezionare "Nome di partizione" hello "Contenuto dinamico" elenco](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details.png)

     <span data-ttu-id="fa2ec-154">In una sezione successiva, è possibile specificare una chiave di partizione univoca che divide hello batch di destinazione in logico imposta toowhere è possibile inviare messaggi.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-154">In a later section, you can specify a unique partition key that divides hello target batch into logical sets toowhere you can send messages.</span></span> 
     <span data-ttu-id="fa2ec-155">Ogni set ha un numero univoco generato da hello mittente logica app.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-155">Each set has a unique number that's generated by hello sender logic app.</span></span> 
     <span data-ttu-id="fa2ec-156">Questa funzionalità consente di utilizzare un singolo batch con più sottoinsiemi e definire ogni subset con nome hello specificata dall'utente.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-156">This capability lets you use a single batch with multiple subsets and define each subset with hello name that you provide.</span></span>

   * <span data-ttu-id="fa2ec-157">In hello **corpo** casella quando hello **contenuto dinamico** viene visualizzato l'elenco, selezionare hello **Id messaggio** campo.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-157">In hello **Body** box, when hello **Dynamic content** list appears, select hello **Message Id** field.</span></span>

     ![Per la casella "Body" selezionare "ID messaggio"](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details-for-each.png)

     <span data-ttu-id="fa2ec-159">Poiché l'input hello per azione di hello invio messaggio di posta elettronica è una matrice, hello viene automaticamente aggiunta una **per ogni** cerchio attorno hello **invia un messaggio di posta elettronica** azione.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-159">Because hello input for hello send email action is an array, hello designer automatically adds a **For each** loop around hello **Send an email** action.</span></span> 
     <span data-ttu-id="fa2ec-160">Questo ciclo esegue l'azione interna hello su ogni elemento nel batch hello.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-160">This loop performs hello inner action on each item in hello batch.</span></span> 
     <span data-ttu-id="fa2ec-161">In tal caso, con elementi di toofive set trigger batch hello, sono disponibili cinque messaggi di posta elettronica che viene attivato ogni trigger hello ora.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-161">So, with hello batch trigger set toofive items, you get five emails each time hello trigger fires.</span></span>

7.  <span data-ttu-id="fa2ec-162">Ora che è stata creata un'app per la logica ricevente, occorre salvarla.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-162">Now that you created a batch receiver logic app, save your logic app.</span></span>

    ![Salvare l'app per la logica](./media/logic-apps-batch-process-send-receive-messages/save-batch-receiver-logic-app.png)

<a name="batch-sender"></a>

## <a name="create-logic-apps-that-send-messages-tooa-batch"></a><span data-ttu-id="fa2ec-164">Creare App per la logica che inviano batch di messaggi tooa</span><span class="sxs-lookup"><span data-stu-id="fa2ec-164">Create logic apps that send messages tooa batch</span></span>

<span data-ttu-id="fa2ec-165">Creare uno o più App per la logica che inviano batch toohello elementi definiti da hello ricevitore logica app.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-165">Now create one or more logic apps that send items toohello batch defined by hello receiver logic app.</span></span> <span data-ttu-id="fa2ec-166">Per il mittente di hello, si specifica hello ricevitore logica app e nome del batch, il contenuto del messaggio e tutte le altre impostazioni.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-166">For hello sender, you specify hello receiver logic app and batch name, message content, and any other settings.</span></span> <span data-ttu-id="fa2ec-167">È anche possibile specificare un batch di hello toodivide chiave di partizione univoca negli elementi toocollect subset con tale chiave.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-167">You can optionally provide a unique partition key toodivide hello batch into subsets toocollect items with that key.</span></span>

<span data-ttu-id="fa2ec-168">Mittente logica App necessario sapere dove gli elementi toosend, mentre ricevitore logica App non è necessario tooknow qualsiasi valore sulla mittenti hello.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-168">Sender logic apps need know where toosend items, while receiver logic apps don't need tooknow anything about hello senders.</span></span>

1. <span data-ttu-id="fa2ec-169">Creare un'altra app per la logica con questo nome: "BatchSender"</span><span class="sxs-lookup"><span data-stu-id="fa2ec-169">Create another logic app with this name: "BatchSender"</span></span>

   1. <span data-ttu-id="fa2ec-170">Nella casella di ricerca hello, immettere "recurrence" come filtro.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-170">In hello search box, enter "recurrence" as your filter.</span></span> 
   <span data-ttu-id="fa2ec-171">Selezionare il trigger **Pianificazione - Ricorrenza**</span><span class="sxs-lookup"><span data-stu-id="fa2ec-171">Select this trigger: **Schedule - Recurrence**</span></span>

      ![Aggiungere trigger hello "Ricorrenza pianificazione"](./media/logic-apps-batch-process-send-receive-messages/add-schedule-trigger-batch-receiver.png)

   2. <span data-ttu-id="fa2ec-173">Impostare la frequenza di hello e intervallo toorun hello mittente logica app ogni minuto.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-173">Set hello frequency and interval toorun hello sender logic app every minute.</span></span>

      ![Impostare la frequenza e l'intervallo del trigger di ricorrenza](./media/logic-apps-batch-process-send-receive-messages/recurrence-trigger-batch-receiver-details.png)

2. <span data-ttu-id="fa2ec-175">Aggiungere un nuovo passaggio per l'invio di batch di messaggi tooa.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-175">Add a new step for sending messages tooa batch.</span></span>

   1. <span data-ttu-id="fa2ec-176">Trigger di ricorrenza hello, scegliere **+ nuovo passaggio** > **aggiungere un'azione**.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-176">Under hello recurrence trigger, choose **+ New Step** > **Add an action**.</span></span>

   2. <span data-ttu-id="fa2ec-177">Nella casella di ricerca hello, immettere "batch" come filtro.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-177">In hello search box, enter "batch" as your filter.</span></span> 

   3. <span data-ttu-id="fa2ec-178">Selezionare l'azione: **inviare messaggi toobatch: scegliere un flusso di lavoro App per la logica con trigger batch**</span><span class="sxs-lookup"><span data-stu-id="fa2ec-178">Select this action: **Send messages toobatch – Choose a Logic Apps workflow with batch trigger**</span></span>

      ![Selezionare "Invia messaggi toobatch"](./media/logic-apps-batch-process-send-receive-messages/send-messages-batch-action.png)

   4. <span data-ttu-id="fa2ec-180">Selezionare a questo punto l'app per la logica "BatchReceiver" creata in precedenza, che ora viene visualizzata sotto forma di azione.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-180">Now select your "BatchReceiver" logic app that you previously created, which now appears as an action.</span></span>

      ![Selezionare l'app per la logica "ricevente il batch"](./media/logic-apps-batch-process-send-receive-messages/send-batch-select-batch-receiver.png)

      > [!NOTE]
      > <span data-ttu-id="fa2ec-182">elenco di Hello Mostra anche le altre app di logica a cui sono presenti trigger batch.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-182">hello list also shows any other logic apps that have batch triggers.</span></span>

3. <span data-ttu-id="fa2ec-183">Impostare le proprietà batch hello.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-183">Set hello batch properties.</span></span>

   * <span data-ttu-id="fa2ec-184">**Nome batch**: nome batch hello definito dall'applicazione logica ricevitore hello, "TestBatch" in questo esempio e viene convalidato in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-184">**Batch Name**: hello batch name defined by hello receiver logic app, which is "TestBatch" in this example and is validated at runtime.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="fa2ec-185">Assicurarsi di non modificare il nome batch hello, che deve corrispondere al nome specificato da hello ricevitore logica app batch hello.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-185">Make sure that you don't change hello batch name, which must match hello batch name that's specified by hello receiver logic app.</span></span>
     > <span data-ttu-id="fa2ec-186">Modifica nome batch di hello fa sì che il mittente hello logica app toofail.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-186">Changing hello batch name causes hello sender logic app toofail.</span></span>

   * <span data-ttu-id="fa2ec-187">**Contenuto del messaggio**: hello che si desidera toosend il contenuto del messaggio.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-187">**Message Content**: hello message content that you want toosend.</span></span> 
   <span data-ttu-id="fa2ec-188">Per questo esempio, aggiungere l'espressione che inserimenti hello data e ora correnti nel messaggio hello del contenuto che si invia toohello batch:</span><span class="sxs-lookup"><span data-stu-id="fa2ec-188">For this example, add this expression that inserts hello current date and time into hello message content that you send toohello batch:</span></span>

     1. <span data-ttu-id="fa2ec-189">Quando hello **contenuto dinamico** viene visualizzato l'elenco, scegliere **espressione**.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-189">When hello **Dynamic content** list appears, choose **Expression**.</span></span> 
     2. <span data-ttu-id="fa2ec-190">Immettere l'espressione hello **utcnow()**e scegliere **OK**.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-190">Enter hello expression **utcnow()**, and choose **OK**.</span></span> 

        ![In "Contenuto messaggio" scegliere "Espressione".](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details.png)

4. <span data-ttu-id="fa2ec-193">Ora consente di impostare una partizione per il batch di hello.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-193">Now set up a partition for hello batch.</span></span> <span data-ttu-id="fa2ec-194">Nell'azione "BatchReceiver" hello, scegliere **Visualizza le opzioni avanzate**.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-194">In hello "BatchReceiver" action, choose **Show advanced options**.</span></span>

   * <span data-ttu-id="fa2ec-195">**Nome di partizione**: un toouse chiave di partizione univoco facoltativo per la suddivisione del batch di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-195">**Partition Name**: An optional unique partition key toouse for dividing hello target batch.</span></span> <span data-ttu-id="fa2ec-196">Per questo esempio aggiungere un'espressione che genera un numero casuale compreso tra uno e cinque.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-196">For this example, add an expression that generates a random number between one and five.</span></span>
   
     1. <span data-ttu-id="fa2ec-197">Quando hello **contenuto dinamico** viene visualizzato l'elenco, scegliere **espressione**.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-197">When hello **Dynamic content** list appears, choose **Expression**.</span></span>
     2. <span data-ttu-id="fa2ec-198">Immettere l'espressione **rand(1,6)**</span><span class="sxs-lookup"><span data-stu-id="fa2ec-198">Enter this expression: **rand(1,6)**</span></span>

        ![Configurare una partizione per il batch di destinazione](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-partition-advanced-options.png)

        <span data-ttu-id="fa2ec-200">Questa funzione **rand** genera un numero compreso tra uno e cinque.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-200">This **rand** function generates a number between one and five.</span></span> 
        <span data-ttu-id="fa2ec-201">Si divide pertanto il batch in cinque partizioni numerate, che questa espressione imposta in modo dinamico.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-201">So you are dividing this batch into five numbered partitions, which this expression dynamically sets.</span></span>

   * <span data-ttu-id="fa2ec-202">**ID messaggio**: un identificatore di messaggio facoltativo e GUID generato quando vuoto.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-202">**Message Id**: An optional message identifier and is a generated GUID when empty.</span></span> 
   <span data-ttu-id="fa2ec-203">Per questo esempio lasciare vuota questa casella.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-203">For this example, leave this box blank.</span></span>

5. <span data-ttu-id="fa2ec-204">Salvare l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-204">Save your logic app.</span></span> <span data-ttu-id="fa2ec-205">Logica app mittente sarà esempio toothis simile:</span><span class="sxs-lookup"><span data-stu-id="fa2ec-205">Your sender logic app now looks similar toothis example:</span></span>

   ![Salvare l'app per la logica mittente](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details-finished.png)

## <a name="test-your-logic-apps"></a><span data-ttu-id="fa2ec-207">Testare le app per la logica</span><span class="sxs-lookup"><span data-stu-id="fa2ec-207">Test your logic apps</span></span>

<span data-ttu-id="fa2ec-208">tootest l'invio in batch di soluzione, lasciare l'App in esecuzione per alcuni minuti per la logica.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-208">tootest your batching solution, leave your logic apps running for a few minutes.</span></span> <span data-ttu-id="fa2ec-209">Presto iniziare il recupero di messaggi di posta elettronica nei gruppi di cinque, tutti con hello stessa chiave di partizione.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-209">Soon, you start getting emails in groups of five, all with hello same partition key.</span></span>

<span data-ttu-id="fa2ec-210">Logica app BatchSender viene eseguito ogni minuto, genera un numero casuale compreso tra uno e cinque e viene utilizzato questo numero generato come chiave di partizione hello per il batch di destinazione hello in cui i messaggi vengono inviati.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-210">Your BatchSender logic app runs every minute, generates a random number between one and five, and uses this generated number as hello partition key for hello target batch where messages are sent.</span></span> <span data-ttu-id="fa2ec-211">Ogni volta che il batch hello ha cinque elementi con hello stessa chiave di partizione, BatchReceiver logica app genera e invia posta elettronica per ogni messaggio.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-211">Each time hello batch has five items with hello same partition key, your BatchReceiver logic app fires and sends mail for each message.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fa2ec-212">Al termine di test, assicurarsi di disattivare hello BatchSender logica app toostop l'invio di messaggi e di evitare il sovraccarico di posta in arrivo.</span><span class="sxs-lookup"><span data-stu-id="fa2ec-212">When you're done testing, make sure that you disable hello BatchSender logic app toostop sending messages and avoid overloading your inbox.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa2ec-213">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fa2ec-213">Next steps</span></span>

* <span data-ttu-id="fa2ec-214">[Build on logic app definitions by using JSON](../logic-apps/logic-apps-author-definitions.md) (Compilare definizioni di app per la logica on JSON)</span><span class="sxs-lookup"><span data-stu-id="fa2ec-214">[Build on logic app definitions by using JSON](../logic-apps/logic-apps-author-definitions.md)</span></span>
* [<span data-ttu-id="fa2ec-215">Compilare un'app senza server in Visual Studio con App per la logica e Funzioni</span><span class="sxs-lookup"><span data-stu-id="fa2ec-215">Build a serverless app in Visual Studio with Azure Logic Apps and Functions</span></span>](../logic-apps/logic-apps-serverless-get-started-vs.md)
* [<span data-ttu-id="fa2ec-216">Gestione delle eccezioni e registrazione degli errori per le app per la logica</span><span class="sxs-lookup"><span data-stu-id="fa2ec-216">Exception handling and error logging for logic apps</span></span>](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
