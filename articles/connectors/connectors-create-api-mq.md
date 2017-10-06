---
title: aaaLearn come toouse hello connettore MQ nelle app di logica di Azure | Documenti Microsoft
description: Collegare tooan locale o server MQ Azure dalla toobrowse di flusso di lavoro app logica, ricevere e inviare messaggi tooWebSphere MQ
services: logic-apps
author: valthom
manager: anneta
documentationcenter: 
editor: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 06/01/2017
ms.author: valthom; ladocs
ms.openlocfilehash: 8b36d53b457ced1a7461c229aecfcf8e4ae668a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-ibm-mq-server-from-logic-apps-using-hello-mq-connector"></a><span data-ttu-id="9bf35-103">Connessione server IBM MQ tooan da logica App usando il connettore MQ hello</span><span class="sxs-lookup"><span data-stu-id="9bf35-103">Connect tooan IBM MQ server from logic apps using hello MQ connector</span></span> 

<span data-ttu-id="9bf35-104">Microsoft Connector per MQ consente di inviare e recuperare i messaggi archiviati in un server MQ locale o in Azure.</span><span class="sxs-lookup"><span data-stu-id="9bf35-104">Microsoft Connector for MQ sends and retrieves messages stored in an MQ Server on-premises, or in Azure.</span></span> <span data-ttu-id="9bf35-105">Il connettore include un client MQ Microsoft che comunica con un server IBM MQ remoto tramite una rete TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="9bf35-105">This connector includes a Microsoft MQ client that communicates with a remote IBM MQ server across a TCP/IP network.</span></span> <span data-ttu-id="9bf35-106">Questo documento è un connettore MQ starter Guida toouse hello.</span><span class="sxs-lookup"><span data-stu-id="9bf35-106">This document is a starter guide toouse hello MQ connector.</span></span> <span data-ttu-id="9bf35-107">È consigliabile iniziare cercando un singolo messaggio in una coda e quindi si tenta di hello altre azioni.</span><span class="sxs-lookup"><span data-stu-id="9bf35-107">We recommended you begin by browsing a single message on a queue, and then trying hello other actions.</span></span>    

<span data-ttu-id="9bf35-108">connettore MQ Hello include hello seguenti azioni.</span><span class="sxs-lookup"><span data-stu-id="9bf35-108">hello MQ connector includes hello following actions.</span></span> <span data-ttu-id="9bf35-109">Non sono disponibili trigger.</span><span class="sxs-lookup"><span data-stu-id="9bf35-109">There are no triggers.</span></span>

-   <span data-ttu-id="9bf35-110">Selezionare un singolo messaggio senza eliminare il messaggio hello dal Server IBM MQ hello</span><span class="sxs-lookup"><span data-stu-id="9bf35-110">Browse a single message without deleting hello message from hello IBM MQ Server</span></span>
-   <span data-ttu-id="9bf35-111">Selezionare un batch di messaggi senza eliminare i messaggi hello dal Server IBM MQ hello</span><span class="sxs-lookup"><span data-stu-id="9bf35-111">Browse a batch of messages without deleting hello messages from hello IBM MQ Server</span></span>
-   <span data-ttu-id="9bf35-112">Un singolo messaggio di ricezione ed eliminare messaggio hello dal Server IBM MQ hello</span><span class="sxs-lookup"><span data-stu-id="9bf35-112">Receive a single message and delete hello message from hello IBM MQ Server</span></span>
-   <span data-ttu-id="9bf35-113">Ricevere un batch di messaggi ed eliminare messaggi hello dalla hello Server IBM MQ</span><span class="sxs-lookup"><span data-stu-id="9bf35-113">Receive a batch of messages and delete hello messages from hello IBM MQ Server</span></span>
-   <span data-ttu-id="9bf35-114">Inviare toohello un singolo messaggio IBM MQ Server</span><span class="sxs-lookup"><span data-stu-id="9bf35-114">Send a single message toohello IBM MQ Server</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="9bf35-115">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="9bf35-115">Prerequisites</span></span>

* <span data-ttu-id="9bf35-116">Se si utilizza un server di MSMQ locale, [installare il gateway dati locale di hello](../logic-apps/logic-apps-gateway-install.md) in un server all'interno della rete.</span><span class="sxs-lookup"><span data-stu-id="9bf35-116">If using an on-premises MQ server, [install hello on-premises data gateway](../logic-apps/logic-apps-gateway-install.md) on a server within your network.</span></span> <span data-ttu-id="9bf35-117">Se hello Server MQ pubblicamente disponibili, o all'interno di Azure, quindi gateway dati hello non è utilizzate o necessarie.</span><span class="sxs-lookup"><span data-stu-id="9bf35-117">If hello MQ Server is publicly available, or available within Azure, then hello data gateway is not used or required.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9bf35-118">server Hello in hello è installato il Gateway dati locale deve inoltre disporre di .net Framework 4.6 per hello connettore MQ toofunction installato.</span><span class="sxs-lookup"><span data-stu-id="9bf35-118">hello server where hello On-Premises Data Gateway is installed must also have .Net Framework 4.6 installed for hello MQ Connector toofunction.</span></span>

* <span data-ttu-id="9bf35-119">Creare risorse di Azure per il gateway dati locale di hello - hello [impostare la connessione del gateway dati hello](../logic-apps/logic-apps-gateway-connection.md).</span><span class="sxs-lookup"><span data-stu-id="9bf35-119">Create hello Azure resource for hello on-premises data gateway - [Set up hello data gateway connection](../logic-apps/logic-apps-gateway-connection.md).</span></span>

* <span data-ttu-id="9bf35-120">Versioni supportate ufficialmente di IBM WebSphere MQ:</span><span class="sxs-lookup"><span data-stu-id="9bf35-120">Officially supported IBM WebSphere MQ versions:</span></span>
   * <span data-ttu-id="9bf35-121">MQ 7.5</span><span class="sxs-lookup"><span data-stu-id="9bf35-121">MQ 7.5</span></span>
   * <span data-ttu-id="9bf35-122">MQ 8.0</span><span class="sxs-lookup"><span data-stu-id="9bf35-122">MQ 8.0</span></span>

## <a name="create-a-logic-app"></a><span data-ttu-id="9bf35-123">Creare un'app per la logica</span><span class="sxs-lookup"><span data-stu-id="9bf35-123">Create a logic app</span></span>

1. <span data-ttu-id="9bf35-124">In hello **Azure avviare discussioni**selezionare  **+**  (segno), **Web e dispositivi mobili**e quindi **logica App**.</span><span class="sxs-lookup"><span data-stu-id="9bf35-124">In hello **Azure start board**, select **+** (plus sign), **Web + Mobile**, and then **Logic App**.</span></span> 
2. <span data-ttu-id="9bf35-125">Immettere hello **nome**, ad esempio, MQTestApp **sottoscrizione**, **gruppo di risorse**, e **percorso** (utilizzare il percorso di hello dove hello connessione Gateway dati locale è configurato).</span><span class="sxs-lookup"><span data-stu-id="9bf35-125">Enter hello **Name**, such as MQTestApp, **Subscription**, **Resource group**, and **Location** (use hello location where hello on-premises Data Gateway connection is configured).</span></span> <span data-ttu-id="9bf35-126">Selezionare **Pin toodashboard**e selezionare **crea**.</span><span class="sxs-lookup"><span data-stu-id="9bf35-126">Select **Pin toodashboard**, and select **Create**.</span></span>  
<span data-ttu-id="9bf35-127">![Creare un'app per la logica](media/connectors-create-api-mq/Create_Logic_App.png)</span><span class="sxs-lookup"><span data-stu-id="9bf35-127">![Create Logic App](media/connectors-create-api-mq/Create_Logic_App.png)</span></span>

## <a name="add-a-trigger"></a><span data-ttu-id="9bf35-128">Aggiungere un trigger</span><span class="sxs-lookup"><span data-stu-id="9bf35-128">Add a trigger</span></span>

> [!NOTE]
> <span data-ttu-id="9bf35-129">Hello MQ connettore non dispone di tutti i trigger.</span><span class="sxs-lookup"><span data-stu-id="9bf35-129">hello MQ Connector does not have any triggers.</span></span> <span data-ttu-id="9bf35-130">In tal caso, utilizzare un altro trigger toostart app logica, ad esempio hello **ricorrenza** trigger.</span><span class="sxs-lookup"><span data-stu-id="9bf35-130">So, use another trigger toostart your logic app, such as hello **Recurrence** trigger.</span></span> 

1. <span data-ttu-id="9bf35-131">Hello **logica App progettazione** viene visualizzata, selezionare **ricorrenza** nell'elenco di hello dei trigger comune.</span><span class="sxs-lookup"><span data-stu-id="9bf35-131">hello **Logic Apps Designer** opens, select **Recurrence** in hello list of common triggers.</span></span>
2. <span data-ttu-id="9bf35-132">Selezionare **modifica** all'interno di hello ricorrenza Trigger.</span><span class="sxs-lookup"><span data-stu-id="9bf35-132">Select **Edit** within hello Recurrence Trigger.</span></span> 
3. <span data-ttu-id="9bf35-133">Set hello **frequenza** troppo**giorno**e set hello **intervallo** troppo**7**.</span><span class="sxs-lookup"><span data-stu-id="9bf35-133">Set hello **Frequency** too**Day**, and set hello **Interval** too**7**.</span></span> 

## <a name="browse-a-single-message"></a><span data-ttu-id="9bf35-134">Visualizzare un singolo messaggio</span><span class="sxs-lookup"><span data-stu-id="9bf35-134">Browse a single message</span></span>
1. <span data-ttu-id="9bf35-135">Selezionare **+ Nuovo passaggio** e quindi **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="9bf35-135">Select **+ New step**, and select **Add an action**.</span></span>
2. <span data-ttu-id="9bf35-136">Nella casella di ricerca hello, digitare `mq`, quindi selezionare **MQ - Sfoglia messaggio**.</span><span class="sxs-lookup"><span data-stu-id="9bf35-136">In hello search box, type `mq`, and then select **MQ - Browse message**.</span></span>  
<span data-ttu-id="9bf35-137">![Browse message](media/connectors-create-api-mq/Browse_message.png) (Visualizza messaggio)</span><span class="sxs-lookup"><span data-stu-id="9bf35-137">![Browse message](media/connectors-create-api-mq/Browse_message.png)</span></span>

3. <span data-ttu-id="9bf35-138">Se non è disponibile una connessione MSMQ esistente, quindi creare la connessione hello:</span><span class="sxs-lookup"><span data-stu-id="9bf35-138">If there isn't an existing MQ connection, then create hello connection:</span></span>  

    1. <span data-ttu-id="9bf35-139">Selezionare **Connetti tramite il gateway dati locale**e immettere le proprietà di hello del server MQ.</span><span class="sxs-lookup"><span data-stu-id="9bf35-139">Select **Connect via on-premises data gateway**, and enter hello properties of your MQ server.</span></span>  
    <span data-ttu-id="9bf35-140">Per **Server**, è possibile immettere il nome di server MQ hello o immettere l'indirizzo IP hello seguita da una virgola e hello il numero di porta.</span><span class="sxs-lookup"><span data-stu-id="9bf35-140">For **Server**, you can enter hello MQ server name, or enter hello IP address followed by a colon and hello port number.</span></span> 
    2. <span data-ttu-id="9bf35-141">Hello **gateway** tutte le connessioni gateway esistenti che sono state configurate gli elenchi a discesa.</span><span class="sxs-lookup"><span data-stu-id="9bf35-141">hello **gateway** dropdown lists any existing gateway connections that have been configured.</span></span> <span data-ttu-id="9bf35-142">Selezionare il gateway.</span><span class="sxs-lookup"><span data-stu-id="9bf35-142">Select your gateway.</span></span>
    3. <span data-ttu-id="9bf35-143">Selezionare **Create** (Crea) al termine.</span><span class="sxs-lookup"><span data-stu-id="9bf35-143">Select **Create** when finished.</span></span> <span data-ttu-id="9bf35-144">La connessione è simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="9bf35-144">Your connection looks similar toohello following:</span></span>   
    <span data-ttu-id="9bf35-145">![Proprietà connessione](media/connectors-create-api-mq/Connection_Properties.png)</span><span class="sxs-lookup"><span data-stu-id="9bf35-145">![Connection Properties](media/connectors-create-api-mq/Connection_Properties.png)</span></span>

4. <span data-ttu-id="9bf35-146">Nelle proprietà di azione hello, è possibile:</span><span class="sxs-lookup"><span data-stu-id="9bf35-146">In hello action properties, you can:</span></span>  

    * <span data-ttu-id="9bf35-147">Hello utilizzare **coda** tooaccess proprietà un nome diverso rispetto a quello definito nella connessione hello</span><span class="sxs-lookup"><span data-stu-id="9bf35-147">Use hello **Queue** property tooaccess a different queue name than what is defined in hello connection</span></span>
    * <span data-ttu-id="9bf35-148">Hello utilizzare **MessageId**, **CorrelationId**, **GroupId**, toobrowse altre proprietà per un messaggio in base alle proprietà dei messaggi MSMQ diversi hello e</span><span class="sxs-lookup"><span data-stu-id="9bf35-148">Use hello **MessageId**, **CorrelationId**, **GroupId**, and other properties toobrowse for a message based on hello different MQ message properties</span></span>
    * <span data-ttu-id="9bf35-149">Impostare **IncludeInfo** troppo**True** tooinclude informazioni di altri messaggi nell'output di hello.</span><span class="sxs-lookup"><span data-stu-id="9bf35-149">Set **IncludeInfo** too**True** tooinclude additional message information in hello output.</span></span> <span data-ttu-id="9bf35-150">O, impostare il valore troppo**False** toonot includere informazioni di altri messaggi nell'output di hello.</span><span class="sxs-lookup"><span data-stu-id="9bf35-150">Or, set it too**False** toonot include additional message information in hello output.</span></span>
    * <span data-ttu-id="9bf35-151">Immettere un **Timeout** valore toodetermine toowait il tempo per tooarrive un messaggio in una coda vuota.</span><span class="sxs-lookup"><span data-stu-id="9bf35-151">Enter a **Timeout** value toodetermine how long toowait for a message tooarrive in an empty queue.</span></span> <span data-ttu-id="9bf35-152">Se si specifica alcun valore, viene recuperato il primo messaggio hello nella coda di hello e non vi è alcun tempo di attesa per tooappear un messaggio.</span><span class="sxs-lookup"><span data-stu-id="9bf35-152">If nothing is entered, hello first message in hello queue is retrieved, and there is no time spent waiting for a message tooappear.</span></span>  
    <span data-ttu-id="9bf35-153">![Visualizzare le proprietà del messaggio](media/connectors-create-api-mq/Browse_message_Props.png)</span><span class="sxs-lookup"><span data-stu-id="9bf35-153">![Browse Message Properties](media/connectors-create-api-mq/Browse_message_Props.png)</span></span>

5. <span data-ttu-id="9bf35-154">**Salvare** le modifiche e quindi **eseguire** l'app per la logica:</span><span class="sxs-lookup"><span data-stu-id="9bf35-154">**Save** your changes, and then **Run** your logic app:</span></span>  
<span data-ttu-id="9bf35-155">![Salvare ed eseguire](media/connectors-create-api-mq/Save_Run.png)</span><span class="sxs-lookup"><span data-stu-id="9bf35-155">![Save and run](media/connectors-create-api-mq/Save_Run.png)</span></span>

6. <span data-ttu-id="9bf35-156">Dopo alcuni secondi, vengono illustrati i passaggi di hello di hello eseguire e output di hello è possibile esaminare.</span><span class="sxs-lookup"><span data-stu-id="9bf35-156">After a few seconds, hello steps of hello run are shown, and you can look at hello output.</span></span> <span data-ttu-id="9bf35-157">Selezionare hello segno di spunta verde toosee dettagli di ogni passaggio.</span><span class="sxs-lookup"><span data-stu-id="9bf35-157">Select hello green checkmark toosee details of each step.</span></span> <span data-ttu-id="9bf35-158">Selezionare **vedere output raw** toosee ulteriori dettagli su hello i dati di output.</span><span class="sxs-lookup"><span data-stu-id="9bf35-158">Select **See raw outputs** toosee additional details on hello output data.</span></span>  
<span data-ttu-id="9bf35-159">![Visualizzare l'output del messaggio](media/connectors-create-api-mq/Browse_message_output.png)</span><span class="sxs-lookup"><span data-stu-id="9bf35-159">![Browse message output](media/connectors-create-api-mq/Browse_message_output.png)</span></span>  

    <span data-ttu-id="9bf35-160">Output non elaborato:</span><span class="sxs-lookup"><span data-stu-id="9bf35-160">Raw output:</span></span>  
    ![Visualizzare l'output non elaborato del messaggio](media/connectors-create-api-mq/Browse_message_raw_output.png)

7. <span data-ttu-id="9bf35-162">Quando hello **IncludeInfo** impostazione tootrue, viene visualizzato hello seguente output:</span><span class="sxs-lookup"><span data-stu-id="9bf35-162">When hello **IncludeInfo** option is set tootrue, hello following output is displayed:</span></span>  
<span data-ttu-id="9bf35-163">![Visualizzare le informazioni incluse del messaggio](media/connectors-create-api-mq/Browse_message_Include_Info.png)</span><span class="sxs-lookup"><span data-stu-id="9bf35-163">![Browse message include info](media/connectors-create-api-mq/Browse_message_Include_Info.png)</span></span>

## <a name="browse-multiple-messages"></a><span data-ttu-id="9bf35-164">Visualizzare più messaggi</span><span class="sxs-lookup"><span data-stu-id="9bf35-164">Browse multiple messages</span></span>
<span data-ttu-id="9bf35-165">Hello **visualizzare messaggi di** azione include un **BatchSize** tooindicate opzione deve essere restituito il numero di messaggi dalla coda hello.</span><span class="sxs-lookup"><span data-stu-id="9bf35-165">hello **Browse messages** action includes a **BatchSize** option tooindicate how many messages should be returned from hello queue.</span></span>  <span data-ttu-id="9bf35-166">In assenza di un valore per **BatchSize**, vengono restituiti tutti i messaggi.</span><span class="sxs-lookup"><span data-stu-id="9bf35-166">If **BatchSize** has no entry, all messages are returned.</span></span> <span data-ttu-id="9bf35-167">Hello ha restituito l'output è una matrice di messaggi.</span><span class="sxs-lookup"><span data-stu-id="9bf35-167">hello returned output is an array of messages.</span></span>

1. <span data-ttu-id="9bf35-168">Quando si aggiungono hello **visualizzare messaggi** azione, hello prima connessione che è configurato sia selezionata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="9bf35-168">When adding hello **Browse messages** action, hello first connection that is configured is selected by default.</span></span> <span data-ttu-id="9bf35-169">Selezionare **Cambia connessione** toocreate una nuova connessione, oppure selezionare una connessione diversa.</span><span class="sxs-lookup"><span data-stu-id="9bf35-169">Select **Change connection** toocreate a new connection, or select a different connection.</span></span>

2. <span data-ttu-id="9bf35-170">output di Hello di Sfoglia messaggi Mostra:</span><span class="sxs-lookup"><span data-stu-id="9bf35-170">hello output of Browse messages shows:</span></span>  
![Output dell'azione Browse messages (Visualizza messaggi)](media/connectors-create-api-mq/Browse_messages_output.png)

## <a name="receive-a-single-message"></a><span data-ttu-id="9bf35-172">Ricevere un singolo messaggio</span><span class="sxs-lookup"><span data-stu-id="9bf35-172">Receive a single message</span></span>
<span data-ttu-id="9bf35-173">Hello **Ricevi messaggio** azione ha hello stesso input e output di hello **messaggio Sfoglia** azione.</span><span class="sxs-lookup"><span data-stu-id="9bf35-173">hello **Receive message** action has hello same inputs and outputs as hello **Browse message** action.</span></span> <span data-ttu-id="9bf35-174">Quando si utilizza **Ricevi messaggio**, il messaggio hello viene eliminato dalla coda hello.</span><span class="sxs-lookup"><span data-stu-id="9bf35-174">When using **Receive message**, hello message is deleted from hello queue.</span></span>

## <a name="receive-multiple-messages"></a><span data-ttu-id="9bf35-175">Ricevere più messaggi</span><span class="sxs-lookup"><span data-stu-id="9bf35-175">Receive multiple messages</span></span>
<span data-ttu-id="9bf35-176">Hello **ricevere messaggi** azione ha hello stesso input e output di hello **visualizzare messaggi** azione.</span><span class="sxs-lookup"><span data-stu-id="9bf35-176">hello **Receive messages** action has hello same inputs and outputs as hello **Browse messages** action.</span></span> <span data-ttu-id="9bf35-177">Quando si utilizza **ricevere messaggi**, messaggi hello vengono eliminati dalla coda hello.</span><span class="sxs-lookup"><span data-stu-id="9bf35-177">When using **Receive messages**, hello messages are deleted from hello queue.</span></span>

<span data-ttu-id="9bf35-178">Se non sono presenti messaggi nella coda di hello quando si esegue una ricerca o un'operazione di ricezione, passaggio hello ha esito negativo con hello seguente output:</span><span class="sxs-lookup"><span data-stu-id="9bf35-178">If there are no messages in hello queue when doing a browse or a receive, hello step fails with hello following output:</span></span>  
![Errore di nessun messaggio in MQ](media/connectors-create-api-mq/MQ_No_Msg_Error.png)

## <a name="send-a-message"></a><span data-ttu-id="9bf35-180">Inviare un messaggio</span><span class="sxs-lookup"><span data-stu-id="9bf35-180">Send a message</span></span>
1. <span data-ttu-id="9bf35-181">Quando si aggiungono hello **Send message** azione, hello prima connessione che è configurato sia selezionata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="9bf35-181">When adding hello **Send message** action, hello first connection that is configured is selected by default.</span></span> <span data-ttu-id="9bf35-182">Selezionare **Cambia connessione** toocreate una nuova connessione, oppure selezionare una connessione diversa.</span><span class="sxs-lookup"><span data-stu-id="9bf35-182">Select **Change connection** toocreate a new connection, or select a different connection.</span></span> <span data-ttu-id="9bf35-183">Hello valido **tipi di messaggio** sono **datagramma**, **risposta**, o **richiesta**.</span><span class="sxs-lookup"><span data-stu-id="9bf35-183">hello valid **Message Types** are **Datagram**, **Reply**, or **Request**.</span></span>  
<span data-ttu-id="9bf35-184">![Proprietà dell'azione Send message (Invia messaggio)](media/connectors-create-api-mq/Send_Msg_Props.png)</span><span class="sxs-lookup"><span data-stu-id="9bf35-184">![Send Msg Props](media/connectors-create-api-mq/Send_Msg_Props.png)</span></span>

2. <span data-ttu-id="9bf35-185">Hello output del messaggio di trasmissione simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="9bf35-185">hello output of Send message looks like hello following:</span></span>  
![Output dell'azione Send message (Invia messaggio)](media/connectors-create-api-mq/Send_Msg_Output.png)

## <a name="connector-specific-details"></a><span data-ttu-id="9bf35-187">Dettagli specifici del connettore</span><span class="sxs-lookup"><span data-stu-id="9bf35-187">Connector-specific details</span></span>

<span data-ttu-id="9bf35-188">Visualizzare tutti i trigger e azioni definite in swagger hello e anche eventuali limiti di hello [dettagli connettore](/connectors/mq/).</span><span class="sxs-lookup"><span data-stu-id="9bf35-188">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/mq/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9bf35-189">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9bf35-189">Next steps</span></span>
<span data-ttu-id="9bf35-190">[Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="9bf35-190">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="9bf35-191">Esplorare hello altri connettori disponibile in App per la logica nel nostro [elenco API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="9bf35-191">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
