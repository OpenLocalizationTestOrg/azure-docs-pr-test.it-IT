---
title: aaaSet di monitoraggio di eventi agli hub di eventi di Azure per le app di logica di Azure | Documenti Microsoft
description: Monitorare gli eventi tooreceive flussi di dati e inviare eventi per le app di logica di Azure con hub eventi di Azure
services: logic-apps
keywords: flusso di dati, monitoraggio eventi, hub eventi
author: ecfan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/31/2017
ms.author: estfan; LADocs
ms.openlocfilehash: 4aad2c2ac1134b4d4d440019b4773559e49be122
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-receive-and-send-events-with-hello-event-hubs-connector"></a><span data-ttu-id="2801e-104">Monitorare, ricevere e inviare eventi con il connettore di hub eventi hello</span><span class="sxs-lookup"><span data-stu-id="2801e-104">Monitor, receive, and send events with hello Event Hubs connector</span></span>

<span data-ttu-id="2801e-105">tooset di un monitoraggio di eventi in modo che l'app logica può rilevare gli eventi, ricevere eventi e inviare eventi, connettersi tooan [Hub di eventi di Azure](https://azure.microsoft.com/services/event-hubs) dall'app logica.</span><span class="sxs-lookup"><span data-stu-id="2801e-105">tooset up an event monitor so that your logic app can detect events, receive events, and send events, connect tooan [Azure Event Hub](https://azure.microsoft.com/services/event-hubs) from your logic app.</span></span> <span data-ttu-id="2801e-106">Altre informazioni su [Hub eventi di Azure](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="2801e-106">Learn more about [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>

## <a name="requirements"></a><span data-ttu-id="2801e-107">Requisiti</span><span class="sxs-lookup"><span data-stu-id="2801e-107">Requirements</span></span>

* <span data-ttu-id="2801e-108">Si dispone di toohave un [gli hub di eventi dello spazio dei nomi e Hub eventi](../event-hubs/event-hubs-create.md) in Azure.</span><span class="sxs-lookup"><span data-stu-id="2801e-108">You have toohave an [Event Hubs namespace and Event Hub](../event-hubs/event-hubs-create.md) in Azure.</span></span> <span data-ttu-id="2801e-109">Informazioni su [come toocreate un hub eventi dello spazio dei nomi e Hub eventi](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="2801e-109">Learn [how toocreate an Event Hubs namespace and Event Hub](../event-hubs/event-hubs-create.md).</span></span> 

* <span data-ttu-id="2801e-110">toouse [i connettori](https://docs.microsoft.com/azure/connectors/apis-list) in app logica, è necessario toocreate un'app logica prima.</span><span class="sxs-lookup"><span data-stu-id="2801e-110">toouse [any connector](https://docs.microsoft.com/azure/connectors/apis-list) in your logic app, you have toocreate a logic app first.</span></span> <span data-ttu-id="2801e-111">Informazioni su [come un'app di logica toocreate](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="2801e-111">Learn [how toocreate a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

<a name="permissions-connection-string"></a>
## <a name="check-event-hubs-namespace-permissions-and-find-hello-connection-string"></a><span data-ttu-id="2801e-112">Controllare le autorizzazioni dello spazio dei nomi di hub eventi e trovare la stringa di connessione hello</span><span class="sxs-lookup"><span data-stu-id="2801e-112">Check Event Hubs namespace permissions and find hello connection string</span></span>

<span data-ttu-id="2801e-113">Per i tooaccess app logica qualsiasi servizio, si dispone di toocreate un [ *connessione* ](./connectors-overview.md) tra il logica app hello servizio e, se hai già fatto.</span><span class="sxs-lookup"><span data-stu-id="2801e-113">For your logic app tooaccess any service, you have toocreate a [*connection*](./connectors-overview.md) between your logic app and hello service, if you haven't already.</span></span> <span data-ttu-id="2801e-114">Questa connessione, si autorizza i dati di tooaccess logica app.</span><span class="sxs-lookup"><span data-stu-id="2801e-114">This connection authorizes your logic app tooaccess data.</span></span>
<span data-ttu-id="2801e-115">Per i tooaccess app logica dell'Hub eventi, è necessario toohave **Gestisci** autorizzazioni e la stringa di connessione hello per lo spazio dei nomi dell'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="2801e-115">For your logic app tooaccess your Event Hub, you have toohave **Manage** permissions and hello connection string for your Event Hubs namespace.</span></span>

<span data-ttu-id="2801e-116">toocheck le autorizzazioni e la stringa di connessione hello get, seguire questi passaggi.</span><span class="sxs-lookup"><span data-stu-id="2801e-116">toocheck your permissions and get hello connection string, follow these steps.</span></span>

1.  <span data-ttu-id="2801e-117">Accedi toohello [portale di Azure](https://portal.azure.com "portale di Azure").</span><span class="sxs-lookup"><span data-stu-id="2801e-117">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span> 

2.  <span data-ttu-id="2801e-118">Passare gli hub di eventi tooyour *dello spazio dei nomi*, non hello Hub eventi specifico.</span><span class="sxs-lookup"><span data-stu-id="2801e-118">Go tooyour Event Hubs *namespace*, not hello specific Event Hub.</span></span> <span data-ttu-id="2801e-119">Nel Pannello di hello dello spazio dei nomi, in **impostazioni**, scegliere **criteri di accesso condiviso**.</span><span class="sxs-lookup"><span data-stu-id="2801e-119">On hello namespace blade, under **Settings**, choose **Shared access policies**.</span></span> <span data-ttu-id="2801e-120">In **Attestazioni** controllare di avere le autorizzazioni di **gestione** per lo spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="2801e-120">Under **Claims**, check that you have **Manage** permissions for that namespace.</span></span>

    ![Gestire le autorizzazioni per lo spazio dei nomi di Hub eventi](./media/connectors-create-api-azure-event-hubs/event-hubs-namespace.png)

3.  <span data-ttu-id="2801e-122">stringa di connessione di hello toocopy per hello dello spazio dei nomi di hub eventi, scegliere **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="2801e-122">toocopy hello connection string for hello Event Hubs namespace, choose **RootManageSharedAccessKey**.</span></span> <span data-ttu-id="2801e-123">Avanti tooyour primario chiave di stringa di connessione, scegliere il pulsante di copia hello.</span><span class="sxs-lookup"><span data-stu-id="2801e-123">Next tooyour primary key connection string, choose hello copy button.</span></span>

    ![Copiare la stringa di connessione dello spazio dei nomi di Hub eventi](media/connectors-create-api-azure-event-hubs/find-event-hub-namespace-connection-string.png)

    > [!TIP]
    > <span data-ttu-id="2801e-125">tooconfirm se la stringa di connessione è associato a uno spazio dei nomi di hub eventi o a un Hub di eventi specifici, verificare la stringa di connessione hello per hello `EntityPath` parametro.</span><span class="sxs-lookup"><span data-stu-id="2801e-125">tooconfirm whether your connection string is associated with your Event Hubs namespace or with a specific Event Hub, check hello connection string for hello `EntityPath` parameter.</span></span> <span data-ttu-id="2801e-126">Se questo parametro, la stringa di connessione hello è per un Hub eventi specifico "entità" e non è hello stringa corretta toouse con l'app logica.</span><span class="sxs-lookup"><span data-stu-id="2801e-126">If you find this parameter, hello connection string is for a specific Event Hub "entity", and is not hello correct string toouse with your logic app.</span></span>

4.  <span data-ttu-id="2801e-127">Ora quando viene chiesto di credenziali dopo l'aggiunta di un'app hub di eventi trigger o azione tooyour logica, è possibile connettersi dello spazio dei nomi di tooyour hub eventi.</span><span class="sxs-lookup"><span data-stu-id="2801e-127">Now when you're prompted for credentials after adding an Event Hubs trigger or action tooyour logic app, you can connect tooyour Event Hubs namespace.</span></span> <span data-ttu-id="2801e-128">Assegnare un nome di connessione, immettere stringa di connessione hello copiato e scegliere **crea**.</span><span class="sxs-lookup"><span data-stu-id="2801e-128">Give your connection a name, enter hello connection string that you copied, and choose **Create**.</span></span>

    ![Immettere la stringa di connessione per lo spazio dei nomi di Hub eventi](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    <span data-ttu-id="2801e-130">Dopo aver creato la connessione, nome connessione hello compariranno in hello gli hub di eventi trigger o un'azione.</span><span class="sxs-lookup"><span data-stu-id="2801e-130">After you create your connection, hello connection name should appear in hello Event Hubs trigger or action.</span></span> 
    <span data-ttu-id="2801e-131">È quindi possibile continuare con gli altri passaggi di logica app hello.</span><span class="sxs-lookup"><span data-stu-id="2801e-131">You can then continue with hello other steps in your logic app.</span></span>

    ![Connessione allo spazio dei nomi di Hub eventi creata](./media/connectors-create-api-azure-event-hubs/event-hubs-connection-created.png)

## <a name="start-workflow-when-your-event-hub-receives-new-events"></a><span data-ttu-id="2801e-133">Avviare il flusso di lavoro quando l'hub eventi riceve nuovi eventi</span><span class="sxs-lookup"><span data-stu-id="2801e-133">Start workflow when your Event Hub receives new events</span></span>

<span data-ttu-id="2801e-134">Un [*trigger*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) è un evento che avvia un flusso di lavoro nell'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="2801e-134">A [*trigger*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is an event that starts a workflow in your logic app.</span></span> <span data-ttu-id="2801e-135">Per avviare un flusso di lavoro quando i nuovi eventi vengono inviati tooyour Hub eventi, seguire questi passaggi per l'aggiunta di trigger hello in grado di rilevare questo evento.</span><span class="sxs-lookup"><span data-stu-id="2801e-135">To start a workflow when new events are sent tooyour Event Hub, follow these steps for adding hello trigger that detects this event.</span></span>

1.  <span data-ttu-id="2801e-136">In hello [portale di Azure](https://portal.azure.com "portale di Azure"), passare tooyour app per la logica esistente o creare un'app logica vuoto.</span><span class="sxs-lookup"><span data-stu-id="2801e-136">In hello [Azure portal](https://portal.azure.com "Azure portal"), go tooyour existing logic app or create a blank logic app.</span></span>

2.  <span data-ttu-id="2801e-137">Nella casella di ricerca hello per hello progettazione applicazione logica, immettere `event hubs` per il filtro.</span><span class="sxs-lookup"><span data-stu-id="2801e-137">In hello search box for hello Logic App Designer, enter `event hubs` for your filter.</span></span> <span data-ttu-id="2801e-138">Selezionare il trigger: **Quando sono disponibili eventi nell'hub eventi**</span><span class="sxs-lookup"><span data-stu-id="2801e-138">Select this trigger: **When events are available in Event Hub**</span></span>

    ![Selezionare il trigger per quando l'hub eventi riceve nuovi eventi](./media/connectors-create-api-azure-event-hubs/find-event-hubs-trigger.png)

    <span data-ttu-id="2801e-140">Se si dispone già di uno spazio dei nomi di connessione tooyour hub eventi, viene chiesto toocreate ora questa connessione.</span><span class="sxs-lookup"><span data-stu-id="2801e-140">If you don't already have a connection tooyour Event Hubs namespace, you're prompted toocreate this connection now.</span></span> <span data-ttu-id="2801e-141">Assegnare un nome di connessione e immettere la stringa di connessione hello per lo spazio dei nomi dell'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="2801e-141">Give your connection a name, and enter hello connection string for your Event Hubs namespace.</span></span> 
    <span data-ttu-id="2801e-142">Se necessario, informazioni su [come toofind la stringa di connessione](#permissions-connection-string).</span><span class="sxs-lookup"><span data-stu-id="2801e-142">If necessary, learn [how toofind your connection string](#permissions-connection-string).</span></span>

    ![Immettere la stringa di connessione per lo spazio dei nomi di Hub eventi](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    <span data-ttu-id="2801e-144">Dopo aver creato una connessione di hello, hello le impostazioni per hello **quando un evento in disponibile in un Hub eventi** trigger vengono visualizzati.</span><span class="sxs-lookup"><span data-stu-id="2801e-144">After you create hello connection, hello settings for hello **When an event in available in an Event Hub** trigger appear.</span></span>

    ![Impostazioni del trigger per quando l'hub eventi riceve nuovi eventi](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger.png)

3.  <span data-ttu-id="2801e-146">Immettere o selezionare il nome di hello per Hub di eventi che si desidera toomonitor hello.</span><span class="sxs-lookup"><span data-stu-id="2801e-146">Enter or select hello name for hello Event Hub that you want toomonitor.</span></span> <span data-ttu-id="2801e-147">Selezionare la frequenza di hello e intervallo per la frequenza con cui toocheck hello Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="2801e-147">Select hello frequency and interval for how often you want toocheck hello Event Hub.</span></span>

    > [!TIP]
    > <span data-ttu-id="2801e-148">Selezionare un gruppo di consumer per la lettura degli eventi, scegliere di toooptionally **Visualizza le opzioni avanzate**.</span><span class="sxs-lookup"><span data-stu-id="2801e-148">toooptionally select a consumer group for reading events, choose **Show advanced options**.</span></span> 

    ![Specificare l'hub eventi o il gruppo di consumer](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger-details.png)

    <span data-ttu-id="2801e-150">Ora impostati un toostart trigger un flusso di lavoro per l'app logica.</span><span class="sxs-lookup"><span data-stu-id="2801e-150">You've now set up a trigger toostart a workflow for your logic app.</span></span> 
    <span data-ttu-id="2801e-151">Logica app controlla hello specificato Hub eventi in base a una pianificazione hello è impostata.</span><span class="sxs-lookup"><span data-stu-id="2801e-151">Your logic app checks hello specified Event Hub based on hello schedule that you set.</span></span> 
    <span data-ttu-id="2801e-152">Se l'app consente di individuare nuovi eventi hello Hub eventi, nell'app logica trigger hello esegue altre azioni e trigger.</span><span class="sxs-lookup"><span data-stu-id="2801e-152">If your app finds new events in hello Event Hub, hello trigger runs other actions or triggers in your logic app.</span></span>

## <a name="send-events-tooyour-event-hub-from-your-logic-app"></a><span data-ttu-id="2801e-153">Inviare gli eventi tooyour Hub eventi dalla tua app di logica</span><span class="sxs-lookup"><span data-stu-id="2801e-153">Send events tooyour Event Hub from your logic app</span></span>

<span data-ttu-id="2801e-154">Un'[*azione*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) è un'attività eseguita dal flusso di lavoro dell'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="2801e-154">An [*action*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is a task performed by your logic app workflow.</span></span> <span data-ttu-id="2801e-155">Dopo avere aggiunto un'app di logica tooyour trigger, è possibile aggiungere un tooperform operazioni con i dati generati dal trigger.</span><span class="sxs-lookup"><span data-stu-id="2801e-155">After you add a trigger tooyour logic app, you can add an action tooperform operations with data generated by that trigger.</span></span> <span data-ttu-id="2801e-156">toosend tooyour un evento Hub eventi dalla logica app, seguire questi passaggi.</span><span class="sxs-lookup"><span data-stu-id="2801e-156">toosend an event tooyour Event Hub from your logic app, follow these steps.</span></span>

1.  <span data-ttu-id="2801e-157">Nella finestra di progettazione dell'app per la logica scegliere **Nuovo passaggio** > **Aggiungi un'azione** sotto il trigger dell'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="2801e-157">In Logic App Designer, under your logic app trigger, choose **New step** > **Add an action**.</span></span>

    ![Scegliere "Nuovo passaggio" e quindi "Aggiungi un'azione"](./media/connectors-create-api-azure-event-hubs/add-action.png)

    <span data-ttu-id="2801e-159">Ora è possibile trovare e selezionare tooperform un'azione.</span><span class="sxs-lookup"><span data-stu-id="2801e-159">Now you can find and select an action tooperform.</span></span> 
    <span data-ttu-id="2801e-160">Sebbene sia possibile selezionare qualsiasi azione, per questo esempio, si desidera hello hub eventi azione toosend eventi.</span><span class="sxs-lookup"><span data-stu-id="2801e-160">Although you can select any action, for this example, we want hello Event Hubs action toosend events.</span></span>

2.  <span data-ttu-id="2801e-161">Nella casella di ricerca hello, immettere `event hubs` per il filtro.</span><span class="sxs-lookup"><span data-stu-id="2801e-161">In hello search box, enter `event hubs` for your filter.</span></span>
<span data-ttu-id="2801e-162">Selezionare questa azione: **Invia evento**</span><span class="sxs-lookup"><span data-stu-id="2801e-162">Select this action: **Send event**</span></span>

    ![Selezionare l'azione "Hub eventi - Invia evento"](./media/connectors-create-api-azure-event-hubs/find-event-hubs-action.png)

3.  <span data-ttu-id="2801e-164">Immettere i dettagli di hello necessario per l'evento hello, ad esempio nome hello per Hub eventi in cui si desidera evento hello toosend hello.</span><span class="sxs-lookup"><span data-stu-id="2801e-164">Enter hello required details for hello event, such as hello name for hello Event Hub where you want toosend hello event.</span></span> <span data-ttu-id="2801e-165">Immettere gli altri dettagli sull'evento hello, ad esempio il contenuto per tale evento facoltativi.</span><span class="sxs-lookup"><span data-stu-id="2801e-165">Enter any other optional details about hello event, such as content for that event.</span></span>

    > [!TIP]
    > <span data-ttu-id="2801e-166">toooptionally specificare partizione dell'Hub eventi hello dove toosend hello evento, scegliere **Visualizza le opzioni avanzate**.</span><span class="sxs-lookup"><span data-stu-id="2801e-166">toooptionally specify hello Event Hub partition where toosend hello event, choose **Show advanced options**.</span></span> 

    ![Immettere il nome dell'hub eventi e i dettagli facoltativi dell'evento](./media/connectors-create-api-azure-event-hubs/event-hubs-send-event-action.png)

6.  <span data-ttu-id="2801e-168">Salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="2801e-168">Save your changes.</span></span>

    ![Salvare l'app per la logica](./media/connectors-create-api-azure-event-hubs/save-logic-app.png)

    <span data-ttu-id="2801e-170">A questo punto sono stati impostati gli eventi di toosend un'azione dall'app logica.</span><span class="sxs-lookup"><span data-stu-id="2801e-170">You've now set up an action toosend events from your logic app.</span></span> 

## <a name="connector-specific-details"></a><span data-ttu-id="2801e-171">Dettagli specifici del connettore</span><span class="sxs-lookup"><span data-stu-id="2801e-171">Connector-specific details</span></span>

<span data-ttu-id="2801e-172">Visualizzare tutti i trigger e azioni definite in swagger hello e anche eventuali limiti di hello [dettagli connettore](/connectors/eventhubs/).</span><span class="sxs-lookup"><span data-stu-id="2801e-172">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/eventhubs/).</span></span> 

## <a name="get-help"></a><span data-ttu-id="2801e-173">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="2801e-173">Get help</span></span>

<span data-ttu-id="2801e-174">in caso di altri utenti le app di logica di Azure, vedere tooask domande e rispondere alle domande visitare hello [forum di Azure logica app](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="2801e-174">tooask questions, answer questions, and see what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="2801e-175">toohelp migliorare App per la logica e i connettori, votare o inviare idee in hello [sito di commenti e suggerimenti dell'utente di App per la logica](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="2801e-175">toohelp improve Logic Apps and connectors, vote on or submit ideas at hello [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2801e-176">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2801e-176">Next steps</span></span>

*  [<span data-ttu-id="2801e-177">Trovare altri connettori per App per la logica di Azure</span><span class="sxs-lookup"><span data-stu-id="2801e-177">Find other connectors for Azure Logic apps</span></span>](./apis-list.md)