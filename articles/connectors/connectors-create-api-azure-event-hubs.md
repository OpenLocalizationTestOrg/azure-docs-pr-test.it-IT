---
title: Configurare il monitoraggio degli eventi con Hub eventi di Azure per App per la logica di Azure | Microsoft Docs
description: Monitorare i flussi di dati per ricevere e inviare eventi per App per la logica di Azure con Hub eventi di Azure
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
ms.openlocfilehash: 2ca27fb8269d1796fb1181fc4d0a8744a592d548
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-receive-and-send-events-with-the-event-hubs-connector"></a><span data-ttu-id="ad418-104">Monitorare, ricevere e inviare eventi con il connettore di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="ad418-104">Monitor, receive, and send events with the Event Hubs connector</span></span>

<span data-ttu-id="ad418-105">Per configurare il monitoraggio degli eventi in modo che un'app per la logica possa rilevare, ricevere e inviare eventi, connettersi a un [hub eventi di Azure](https://azure.microsoft.com/services/event-hubs) dall'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="ad418-105">To set up an event monitor so that your logic app can detect events, receive events, and send events, connect to an [Azure Event Hub](https://azure.microsoft.com/services/event-hubs) from your logic app.</span></span> <span data-ttu-id="ad418-106">Altre informazioni su [Hub eventi di Azure](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="ad418-106">Learn more about [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>

## <a name="requirements"></a><span data-ttu-id="ad418-107">Requisiti</span><span class="sxs-lookup"><span data-stu-id="ad418-107">Requirements</span></span>

* <span data-ttu-id="ad418-108">È necessario avere uno [spazio dei nomi di Hub eventi e un hub eventi](../event-hubs/event-hubs-create.md) in Azure.</span><span class="sxs-lookup"><span data-stu-id="ad418-108">You have to have an [Event Hubs namespace and Event Hub](../event-hubs/event-hubs-create.md) in Azure.</span></span> <span data-ttu-id="ad418-109">Leggere le informazioni su [come creare uno spazio dei nomi di Hub eventi e un hub eventi](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="ad418-109">Learn [how to create an Event Hubs namespace and Event Hub](../event-hubs/event-hubs-create.md).</span></span> 

* <span data-ttu-id="ad418-110">Per usare [qualsiasi connettore](https://docs.microsoft.com/azure/connectors/apis-list) nell'app per la logica, è prima necessario creare un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="ad418-110">To use [any connector](https://docs.microsoft.com/azure/connectors/apis-list) in your logic app, you have to create a logic app first.</span></span> <span data-ttu-id="ad418-111">Leggere le informazioni su [come creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="ad418-111">Learn [how to create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

<a name="permissions-connection-string"></a>
## <a name="check-event-hubs-namespace-permissions-and-find-the-connection-string"></a><span data-ttu-id="ad418-112">Controllare le autorizzazioni dello spazio dei nomi di Hub eventi e trovare la stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="ad418-112">Check Event Hubs namespace permissions and find the connection string</span></span>

<span data-ttu-id="ad418-113">Per consentire all'app per la logica di accedere a qualsiasi servizio, è necessario creare una [*connessione*](./connectors-overview.md) tra l'app per la logica e il servizio, se non è già presente.</span><span class="sxs-lookup"><span data-stu-id="ad418-113">For your logic app to access any service, you have to create a [*connection*](./connectors-overview.md) between your logic app and the service, if you haven't already.</span></span> <span data-ttu-id="ad418-114">Questa connessione autorizza l'app per la logica ad accedere ai dati.</span><span class="sxs-lookup"><span data-stu-id="ad418-114">This connection authorizes your logic app to access data.</span></span>
<span data-ttu-id="ad418-115">Affinché l'app per la logica possa accedere all'hub eventi, è necessario avere le autorizzazioni di **gestione** e la stringa di connessione per lo spazio dei nomi di Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="ad418-115">For your logic app to access your Event Hub, you have to have **Manage** permissions and the connection string for your Event Hubs namespace.</span></span>

<span data-ttu-id="ad418-116">Per controllare le autorizzazioni e ottenere la stringa di connessione, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="ad418-116">To check your permissions and get the connection string, follow these steps.</span></span>

1.  <span data-ttu-id="ad418-117">Accedere al [Portale di Azure](https://portal.azure.com "Portale di Azure").</span><span class="sxs-lookup"><span data-stu-id="ad418-117">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span> 

2.  <span data-ttu-id="ad418-118">Passare allo *spazio dei nomi* di Hub eventi, non all'hub eventi specifico.</span><span class="sxs-lookup"><span data-stu-id="ad418-118">Go to your Event Hubs *namespace*, not the specific Event Hub.</span></span> <span data-ttu-id="ad418-119">Nel pannello dello spazio dei nomi scegliere **Criteri di accesso condivisi** in **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="ad418-119">On the namespace blade, under **Settings**, choose **Shared access policies**.</span></span> <span data-ttu-id="ad418-120">In **Attestazioni** controllare di avere le autorizzazioni di **gestione** per lo spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="ad418-120">Under **Claims**, check that you have **Manage** permissions for that namespace.</span></span>

    ![Gestire le autorizzazioni per lo spazio dei nomi di Hub eventi](./media/connectors-create-api-azure-event-hubs/event-hubs-namespace.png)

3.  <span data-ttu-id="ad418-122">Per copiare la stringa di connessione per lo spazio dei nomi di Hub eventi, scegliere **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="ad418-122">To copy the connection string for the Event Hubs namespace, choose **RootManageSharedAccessKey**.</span></span> <span data-ttu-id="ad418-123">Accanto alla stringa di connessione della chiave primaria scegliere il pulsante Copia.</span><span class="sxs-lookup"><span data-stu-id="ad418-123">Next to your primary key connection string, choose the copy button.</span></span>

    ![Copiare la stringa di connessione dello spazio dei nomi di Hub eventi](media/connectors-create-api-azure-event-hubs/find-event-hub-namespace-connection-string.png)

    > [!TIP]
    > <span data-ttu-id="ad418-125">Per verificare se la stringa di connessione è associata allo spazio dei nomi di Hub eventi o a un hub eventi specifico, controllare se nella stringa è presente il parametro `EntityPath`.</span><span class="sxs-lookup"><span data-stu-id="ad418-125">To confirm whether your connection string is associated with your Event Hubs namespace or with a specific Event Hub, check the connection string for the `EntityPath` parameter.</span></span> <span data-ttu-id="ad418-126">Se questo parametro è presente, la stringa di connessione è per un'entità hub eventi specifica e non è la stringa corretta da usare con l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="ad418-126">If you find this parameter, the connection string is for a specific Event Hub "entity", and is not the correct string to use with your logic app.</span></span>

4.  <span data-ttu-id="ad418-127">Quando vengono chieste le credenziali dopo l'aggiunta di un trigger o un'azione di Hub eventi per l'app per la logica, è possibile connettersi allo spazio dei nomi di Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="ad418-127">Now when you're prompted for credentials after adding an Event Hubs trigger or action to your logic app, you can connect to your Event Hubs namespace.</span></span> <span data-ttu-id="ad418-128">Assegnare un nome alla connessione, immettere la stringa di connessione copiata e quindi scegliere **Crea**.</span><span class="sxs-lookup"><span data-stu-id="ad418-128">Give your connection a name, enter the connection string that you copied, and choose **Create**.</span></span>

    ![Immettere la stringa di connessione per lo spazio dei nomi di Hub eventi](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    <span data-ttu-id="ad418-130">Dopo aver creato la connessione, il nome della connessione dovrebbe venire visualizzato nel trigger o nell'azione di Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="ad418-130">After you create your connection, the connection name should appear in the Event Hubs trigger or action.</span></span> 
    <span data-ttu-id="ad418-131">È quindi possibile continuare con gli altri passaggi nell'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="ad418-131">You can then continue with the other steps in your logic app.</span></span>

    ![Connessione allo spazio dei nomi di Hub eventi creata](./media/connectors-create-api-azure-event-hubs/event-hubs-connection-created.png)

## <a name="start-workflow-when-your-event-hub-receives-new-events"></a><span data-ttu-id="ad418-133">Avviare il flusso di lavoro quando l'hub eventi riceve nuovi eventi</span><span class="sxs-lookup"><span data-stu-id="ad418-133">Start workflow when your Event Hub receives new events</span></span>

<span data-ttu-id="ad418-134">Un [*trigger*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) è un evento che avvia un flusso di lavoro nell'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="ad418-134">A [*trigger*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is an event that starts a workflow in your logic app.</span></span> <span data-ttu-id="ad418-135">Per avviare un flusso di lavoro quando nuovi eventi vengono inviati all'hub eventi, seguire questa procedura per l'aggiunta del trigger che rileva questo evento.</span><span class="sxs-lookup"><span data-stu-id="ad418-135">To start a workflow when new events are sent to your Event Hub, follow these steps for adding the trigger that detects this event.</span></span>

1.  <span data-ttu-id="ad418-136">Nel [portale di Azure](https://portal.azure.com "portale di Azure") passare all'app per la logica esistente o creare un'app per la logica vuota.</span><span class="sxs-lookup"><span data-stu-id="ad418-136">In the [Azure portal](https://portal.azure.com "Azure portal"), go to your existing logic app or create a blank logic app.</span></span>

2.  <span data-ttu-id="ad418-137">Nella casella di ricerca della finestra di progettazione dell'app per la logica immettere `event hubs` come filtro.</span><span class="sxs-lookup"><span data-stu-id="ad418-137">In the search box for the Logic App Designer, enter `event hubs` for your filter.</span></span> <span data-ttu-id="ad418-138">Selezionare il trigger: **Quando sono disponibili eventi nell'hub eventi**</span><span class="sxs-lookup"><span data-stu-id="ad418-138">Select this trigger: **When events are available in Event Hub**</span></span>

    ![Selezionare il trigger per quando l'hub eventi riceve nuovi eventi](./media/connectors-create-api-azure-event-hubs/find-event-hubs-trigger.png)

    <span data-ttu-id="ad418-140">Se non è ancora stata stabilita una connessione allo spazio dei nomi di Hub eventi, a questo punto viene chiesto di creare la connessione.</span><span class="sxs-lookup"><span data-stu-id="ad418-140">If you don't already have a connection to your Event Hubs namespace, you're prompted to create this connection now.</span></span> <span data-ttu-id="ad418-141">Assegnare un nome alla connessione e immettere la stringa di connessione per lo spazio dei nomi di Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="ad418-141">Give your connection a name, and enter the connection string for your Event Hubs namespace.</span></span> 
    <span data-ttu-id="ad418-142">Se necessario, leggere [come trovare la stringa di connessione](#permissions-connection-string).</span><span class="sxs-lookup"><span data-stu-id="ad418-142">If necessary, learn [how to find your connection string](#permissions-connection-string).</span></span>

    ![Immettere la stringa di connessione per lo spazio dei nomi di Hub eventi](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    <span data-ttu-id="ad418-144">Dopo aver creato la connessione, vengono visualizzate le impostazioni per il trigger **Quando sono disponibili eventi nell'hub eventi**.</span><span class="sxs-lookup"><span data-stu-id="ad418-144">After you create the connection, the settings for the **When an event in available in an Event Hub** trigger appear.</span></span>

    ![Impostazioni del trigger per quando l'hub eventi riceve nuovi eventi](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger.png)

3.  <span data-ttu-id="ad418-146">Immettere o selezionare il nome dell'hub di eventi da monitorare.</span><span class="sxs-lookup"><span data-stu-id="ad418-146">Enter or select the name for the Event Hub that you want to monitor.</span></span> <span data-ttu-id="ad418-147">Selezionare la frequenza e l'intervallo con cui si vuole controllare l'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="ad418-147">Select the frequency and interval for how often you want to check the Event Hub.</span></span>

    > [!TIP]
    > <span data-ttu-id="ad418-148">Per selezionare facoltativamente un gruppo di consumer per la lettura degli eventi, scegliere **Mostra opzioni avanzate**.</span><span class="sxs-lookup"><span data-stu-id="ad418-148">To optionally select a consumer group for reading events, choose **Show advanced options**.</span></span> 

    ![Specificare l'hub eventi o il gruppo di consumer](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger-details.png)

    <span data-ttu-id="ad418-150">A questo punto è stato impostato un trigger per avviare un flusso di lavoro per l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="ad418-150">You've now set up a trigger to start a workflow for your logic app.</span></span> 
    <span data-ttu-id="ad418-151">L'app per la logica controlla l'hub eventi specificato in base alla pianificazione impostata.</span><span class="sxs-lookup"><span data-stu-id="ad418-151">Your logic app checks the specified Event Hub based on the schedule that you set.</span></span> 
    <span data-ttu-id="ad418-152">Se l'app trova nuovi eventi nell'hub eventi, il trigger esegue altre azioni o trigger nell'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="ad418-152">If your app finds new events in the Event Hub, the trigger runs other actions or triggers in your logic app.</span></span>

## <a name="send-events-to-your-event-hub-from-your-logic-app"></a><span data-ttu-id="ad418-153">Inviare eventi all'hub eventi dall'app per la logica</span><span class="sxs-lookup"><span data-stu-id="ad418-153">Send events to your Event Hub from your logic app</span></span>

<span data-ttu-id="ad418-154">Un'[*azione*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) è un'attività eseguita dal flusso di lavoro dell'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="ad418-154">An [*action*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is a task performed by your logic app workflow.</span></span> <span data-ttu-id="ad418-155">Dopo avere aggiunto un trigger all'app per la logica, è possibile aggiungere un'azione per eseguire operazioni con i dati generati da tale trigger.</span><span class="sxs-lookup"><span data-stu-id="ad418-155">After you add a trigger to your logic app, you can add an action to perform operations with data generated by that trigger.</span></span> <span data-ttu-id="ad418-156">Per inviare un evento all'hub eventi dall'app per la logica, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="ad418-156">To send an event to your Event Hub from your logic app, follow these steps.</span></span>

1.  <span data-ttu-id="ad418-157">Nella finestra di progettazione dell'app per la logica scegliere **Nuovo passaggio** > **Aggiungi un'azione** sotto il trigger dell'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="ad418-157">In Logic App Designer, under your logic app trigger, choose **New step** > **Add an action**.</span></span>

    ![Scegliere "Nuovo passaggio" e quindi "Aggiungi un'azione"](./media/connectors-create-api-azure-event-hubs/add-action.png)

    <span data-ttu-id="ad418-159">A questo punto è possibile trovare e selezionare un'azione da eseguire.</span><span class="sxs-lookup"><span data-stu-id="ad418-159">Now you can find and select an action to perform.</span></span> 
    <span data-ttu-id="ad418-160">Anche se è possibile selezionare qualsiasi azione, in questo esempio si vuole che l'azione di Hub eventi corrisponda all'invio degli eventi.</span><span class="sxs-lookup"><span data-stu-id="ad418-160">Although you can select any action, for this example, we want the Event Hubs action to send events.</span></span>

2.  <span data-ttu-id="ad418-161">Nella casella di ricerca immettere `event hubs` come filtro.</span><span class="sxs-lookup"><span data-stu-id="ad418-161">In the search box, enter `event hubs` for your filter.</span></span>
<span data-ttu-id="ad418-162">Selezionare questa azione: **Invia evento**</span><span class="sxs-lookup"><span data-stu-id="ad418-162">Select this action: **Send event**</span></span>

    ![Selezionare l'azione "Hub eventi - Invia evento"](./media/connectors-create-api-azure-event-hubs/find-event-hubs-action.png)

3.  <span data-ttu-id="ad418-164">Immettere i dettagli richiesti per l'evento, ad esempio il nome dell'hub eventi a cui si vuole inviare l'evento.</span><span class="sxs-lookup"><span data-stu-id="ad418-164">Enter the required details for the event, such as the name for the Event Hub where you want to send the event.</span></span> <span data-ttu-id="ad418-165">Immettere eventuali altri dettagli facoltativi sull'evento, ad esempio il contenuto dell'evento.</span><span class="sxs-lookup"><span data-stu-id="ad418-165">Enter any other optional details about the event, such as content for that event.</span></span>

    > [!TIP]
    > <span data-ttu-id="ad418-166">Se si vuole specificare la partizione dell'hub eventi dove inviare l'evento, scegliere **Mostra opzioni avanzate**.</span><span class="sxs-lookup"><span data-stu-id="ad418-166">To optionally specify the Event Hub partition where to send the event, choose **Show advanced options**.</span></span> 

    ![Immettere il nome dell'hub eventi e i dettagli facoltativi dell'evento](./media/connectors-create-api-azure-event-hubs/event-hubs-send-event-action.png)

6.  <span data-ttu-id="ad418-168">Salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="ad418-168">Save your changes.</span></span>

    ![Salvare l'app per la logica](./media/connectors-create-api-azure-event-hubs/save-logic-app.png)

    <span data-ttu-id="ad418-170">A questo punto è stata configurata un'azione per inviare gli eventi dall'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="ad418-170">You've now set up an action to send events from your logic app.</span></span> 

## <a name="connector-specific-details"></a><span data-ttu-id="ad418-171">Dettagli specifici del connettore</span><span class="sxs-lookup"><span data-stu-id="ad418-171">Connector-specific details</span></span>

<span data-ttu-id="ad418-172">Per visualizzare eventuali azioni e trigger definiti in Swagger ed eventuali limiti, vedere i [dettagli del connettore](/connectors/eventhubs/).</span><span class="sxs-lookup"><span data-stu-id="ad418-172">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/eventhubs/).</span></span> 

## <a name="get-help"></a><span data-ttu-id="ad418-173">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="ad418-173">Get help</span></span>

<span data-ttu-id="ad418-174">Per porre domande, fornire risposte e ottenere informazioni sulle attività degli altri utenti delle app per la logica di Azure, vedere il [forum sulle app per la logica di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="ad418-174">To ask questions, answer questions, and see what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="ad418-175">Per contribuire al miglioramento delle app per la logica e dei connettori, votare o inviare idee al [sito dei commenti e suggerimenti degli utenti delle app per la logica](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="ad418-175">To help improve Logic Apps and connectors, vote on or submit ideas at the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad418-176">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ad418-176">Next steps</span></span>

*  [<span data-ttu-id="ad418-177">Trovare altri connettori per App per la logica di Azure</span><span class="sxs-lookup"><span data-stu-id="ad418-177">Find other connectors for Azure Logic apps</span></span>](./apis-list.md)