---
title: connettore di Office 365 Outlook hello aaaAdd nelle App logica | Documenti Microsoft
description: Creare App per la logica con l'interazione di tooenable connettore di Office 365 con Office 365. Ad esempio, per creare, modificare e aggiornare contatti ed elementi del calendario.
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b2f6cc2c-bba2-493a-b0ba-841785462a80
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 86a573c9c54701de3d3f0500d19eaf545e0710ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-office-365-outlook-connector"></a><span data-ttu-id="07431-104">Iniziare con il connettore di Office 365 Outlook hello</span><span class="sxs-lookup"><span data-stu-id="07431-104">Get started with hello Office 365 Outlook connector</span></span>
<span data-ttu-id="07431-105">connettore di Office 365 Outlook Hello consente l'interazione con Outlook per Office 365.</span><span class="sxs-lookup"><span data-stu-id="07431-105">hello Office 365 Outlook connector enables interaction with Outlook in Office 365.</span></span> <span data-ttu-id="07431-106">Utilizzare questo connettore toocreate, modificare e Aggiorna contatti e gli elementi del calendario e anche ottenere, inviare e rispondere tooemail.</span><span class="sxs-lookup"><span data-stu-id="07431-106">Use this connector toocreate, edit, and update contacts and calendar items, and also get, send, and reply tooemail.</span></span>

<span data-ttu-id="07431-107">Con Office 365 Outlook è possibile:</span><span class="sxs-lookup"><span data-stu-id="07431-107">With Office 365 Outlook, you:</span></span>

* <span data-ttu-id="07431-108">Compilare il flusso di lavoro utilizzando le funzionalità di posta elettronica e al calendario hello in Office 365.</span><span class="sxs-lookup"><span data-stu-id="07431-108">Build your workflow using hello email and calendar features within Office 365.</span></span> 
* <span data-ttu-id="07431-109">Utilizzare trigger toostart il flusso di lavoro quando si verifica un nuovo indirizzo e-mail, quando viene aggiornato un elemento del calendario e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="07431-109">Use triggers toostart your workflow when there is a new email, when a calendar item is updated, and more.</span></span>
* <span data-ttu-id="07431-110">Utilizzare azioni toosend un messaggio di posta elettronica, creare un nuovo evento del calendario e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="07431-110">Use actions toosend an email, create a new calendar event, and more.</span></span> <span data-ttu-id="07431-111">Ad esempio, quando è presente un nuovo oggetto in Salesforce (trigger), inviare un messaggio di posta elettronica tooyour Outlook di Office 365 (azione).</span><span class="sxs-lookup"><span data-stu-id="07431-111">For example, when there is a new object in Salesforce (a trigger), send an email tooyour Office 365 Outlook (an action).</span></span> 

<span data-ttu-id="07431-112">Questo argomento viene illustrato come toouse hello connettore Outlook di Office 365 in un'app per la logica e anche gli elenchi di hello azioni e trigger.</span><span class="sxs-lookup"><span data-stu-id="07431-112">This topic shows you how toouse hello Office 365 Outlook connector in a logic app, and also lists hello triggers and actions.</span></span>

> [!NOTE]
> <span data-ttu-id="07431-113">Questa versione di hello articolo applica tooLogic disponibilità generale di App (GA).</span><span class="sxs-lookup"><span data-stu-id="07431-113">This version of hello article applies tooLogic Apps general availability (GA).</span></span>
> 
> 

<span data-ttu-id="07431-114">toolearn informazioni sulle App per la logica, vedere [quali sono le app logica](../logic-apps/logic-apps-what-are-logic-apps.md) e [creare un'app di logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="07431-114">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toooffice-365"></a><span data-ttu-id="07431-115">Connettersi tooOffice 365</span><span class="sxs-lookup"><span data-stu-id="07431-115">Connect tooOffice 365</span></span>
<span data-ttu-id="07431-116">Prima che la logica app possa accedere a qualsiasi servizio, creare innanzitutto un *connessione* toohello servizio.</span><span class="sxs-lookup"><span data-stu-id="07431-116">Before your logic app can access any service, you first create a *connection* toohello service.</span></span> <span data-ttu-id="07431-117">Una connessione fornisce la connettività tra un'app per la logica e un altro servizio.</span><span class="sxs-lookup"><span data-stu-id="07431-117">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="07431-118">Ad esempio, tooconnect tooOffice 365 Outlook, è necessario innanzitutto Office 365 *connessione*.</span><span class="sxs-lookup"><span data-stu-id="07431-118">For example, tooconnect tooOffice 365 Outlook, you first need an Office 365 *connection*.</span></span> <span data-ttu-id="07431-119">toocreate una connessione, immettere le credenziali di hello utilizzato normalmente il servizio di hello tooaccess desiderato tooconnect per.</span><span class="sxs-lookup"><span data-stu-id="07431-119">toocreate a connection, enter hello credentials you normally use tooaccess hello service you wish tooconnect to.</span></span> <span data-ttu-id="07431-120">Così con Outlook di Office 365, immettere le credenziali di hello tooyour connessione hello toocreate dell'account Office 365.</span><span class="sxs-lookup"><span data-stu-id="07431-120">So with Office 365 Outlook, enter hello credentials tooyour Office 365 account toocreate hello connection.</span></span>

## <a name="create-hello-connection"></a><span data-ttu-id="07431-121">Creare una connessione hello</span><span class="sxs-lookup"><span data-stu-id="07431-121">Create hello connection</span></span>
> [!INCLUDE [Steps toocreate a connection tooOffice 365](../../includes/connectors-create-api-office365-outlook.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="07431-122">Usare un trigger</span><span class="sxs-lookup"><span data-stu-id="07431-122">Use a trigger</span></span>
<span data-ttu-id="07431-123">Un trigger è un evento che può essere utilizzato toostart flusso di lavoro hello definito in un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="07431-123">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="07431-124">I trigger "polling" servizio hello in corrispondenza di un intervallo e la frequenza desiderata.</span><span class="sxs-lookup"><span data-stu-id="07431-124">Triggers "poll" hello service at an interval and frequency that you want.</span></span> <span data-ttu-id="07431-125">[Altre informazioni sui trigger](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="07431-125">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="07431-126">Nell'app logica hello, digitare "office 365" tooget un elenco dei trigger hello:</span><span class="sxs-lookup"><span data-stu-id="07431-126">In hello logic app, type "office 365" tooget a list of hello triggers:</span></span>  
   
    ![](./media/connectors-create-api-office365-outlook/office365-trigger.png)
2. <span data-ttu-id="07431-127">Selezionare **Office 365 Outlook - All'avvio imminente di un prossimo evento**.</span><span class="sxs-lookup"><span data-stu-id="07431-127">Select **Office 365 Outlook - When an upcoming event is starting soon**.</span></span> <span data-ttu-id="07431-128">Se esiste già una connessione, quindi selezionare un calendario dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="07431-128">If a connection already exists, then select a calendar from hello drop-down list.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/sample-calendar.png)
   
    <span data-ttu-id="07431-129">Nel caso di richiesta toosign in, quindi immettere hello sign in connessione hello toocreate di dettagli.</span><span class="sxs-lookup"><span data-stu-id="07431-129">If you are prompted toosign in, then enter hello sign in details toocreate hello connection.</span></span> <span data-ttu-id="07431-130">[Creare una connessione hello](connectors-create-api-office365-outlook.md#create-the-connection) in questo argomento vengono elencati i passaggi di hello.</span><span class="sxs-lookup"><span data-stu-id="07431-130">[Create hello connection](connectors-create-api-office365-outlook.md#create-the-connection) in this topic lists hello steps.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="07431-131">In questo esempio hello logica app viene eseguita quando viene aggiornato un evento del calendario.</span><span class="sxs-lookup"><span data-stu-id="07431-131">In this example, hello logic app runs when a calendar event is updated.</span></span> <span data-ttu-id="07431-132">risultati di hello toosee del trigger, aggiungere un'altra azione che invia un messaggio di testo.</span><span class="sxs-lookup"><span data-stu-id="07431-132">toosee hello results of this trigger, add another action that sends you a text message.</span></span> <span data-ttu-id="07431-133">Ad esempio, aggiungere hello Twilio *Send message* azione testi quando hello calendario eventi in fase di avvio in 15 minuti.</span><span class="sxs-lookup"><span data-stu-id="07431-133">For example, add hello Twilio *Send message* action that texts you when hello calendar event is starting in 15 minutes.</span></span> 
   > 
   > 
3. <span data-ttu-id="07431-134">Seleziona hello **modifica** pulsante e impostare hello **frequenza** e **intervallo** valori.</span><span class="sxs-lookup"><span data-stu-id="07431-134">Select hello **Edit** button and set hello **Frequency** and **Interval** values.</span></span> <span data-ttu-id="07431-135">Ad esempio, se si desidera hello trigger toopoll ogni 15 minuti, quindi impostare hello **frequenza** troppo**minuto**e set hello **intervallo** troppo**15**.</span><span class="sxs-lookup"><span data-stu-id="07431-135">For example, if you want hello trigger toopoll every 15 minutes, then set hello **Frequency** too**Minute**, and set hello **Interval** too**15**.</span></span> 
   
    ![](./media/connectors-create-api-office365-outlook/calendar-settings.png)
4. <span data-ttu-id="07431-136">**Salvare** le modifiche (angolo superiore sinistro della barra degli strumenti hello).</span><span class="sxs-lookup"><span data-stu-id="07431-136">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="07431-137">L'app per la logica viene salvata e può essere attivata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="07431-137">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="07431-138">Usare un'azione</span><span class="sxs-lookup"><span data-stu-id="07431-138">Use an action</span></span>
<span data-ttu-id="07431-139">Un'azione è un'operazione effettuata dal flusso di lavoro hello definito in un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="07431-139">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="07431-140">[Altre informazioni sulle azioni](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="07431-140">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="07431-141">Selezionare hello sul segno più.</span><span class="sxs-lookup"><span data-stu-id="07431-141">Select hello plus sign.</span></span> <span data-ttu-id="07431-142">Vedrai diverse opzioni: **aggiungere un'azione**, **aggiungere una condizione**, o uno dei hello **più** opzioni.</span><span class="sxs-lookup"><span data-stu-id="07431-142">You see several choices: **Add an action**, **Add a condition**, or one of hello **More** options.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/add-action.png)
2. <span data-ttu-id="07431-143">Selezionare **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="07431-143">Choose **Add an action**.</span></span>
3. <span data-ttu-id="07431-144">Nella casella di testo hello, digitare "office 365" tooget un elenco di tutte le azioni disponibili hello.</span><span class="sxs-lookup"><span data-stu-id="07431-144">In hello text box, type “office 365” tooget a list of all hello available actions.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/office365-actions.png) 
4. <span data-ttu-id="07431-145">Nell'esempio scegliere **Office 365 Outlook - Crea contatto**.</span><span class="sxs-lookup"><span data-stu-id="07431-145">In our example, choose **Office 365 Outlook - Create contact**.</span></span> <span data-ttu-id="07431-146">Se esiste già una connessione, quindi scegliere hello **ID cartella**, **nome**e altre proprietà:</span><span class="sxs-lookup"><span data-stu-id="07431-146">If a connection already exists, then choose hello **Folder ID**, **Given Name**, and other properties:</span></span>  
   
    ![](./media/connectors-create-api-office365-outlook/office365-sampleaction.png)
   
    <span data-ttu-id="07431-147">Se viene chiesto di hello informazioni di connessione, quindi immettere connessione hello toocreate dettagli di hello.</span><span class="sxs-lookup"><span data-stu-id="07431-147">If you are prompted for hello connection information, then enter hello details toocreate hello connection.</span></span> <span data-ttu-id="07431-148">[Creare una connessione hello](connectors-create-api-office365-outlook.md#create-the-connection) in questo argomento vengono descritte queste proprietà.</span><span class="sxs-lookup"><span data-stu-id="07431-148">[Create hello connection](connectors-create-api-office365-outlook.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="07431-149">In questo esempio si crea un nuovo contatto in Office 365 Outlook.</span><span class="sxs-lookup"><span data-stu-id="07431-149">In this example, we create a new contact in Office 365 Outlook.</span></span> <span data-ttu-id="07431-150">È possibile utilizzare l'output dal contatto di un altro trigger toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="07431-150">You can use output from another trigger toocreate hello contact.</span></span> <span data-ttu-id="07431-151">Ad esempio, aggiungere hello SalesForce *quando viene creato un oggetto* trigger.</span><span class="sxs-lookup"><span data-stu-id="07431-151">For example, add hello SalesForce *When an object is created* trigger.</span></span> <span data-ttu-id="07431-152">Aggiungere quindi hello Outlook di Office 365 *creare contatto* azione che utilizza hello SalesForce campi toocreate hello nuovo nuovo contatto in Office 365.</span><span class="sxs-lookup"><span data-stu-id="07431-152">Then add hello Office 365 Outlook *Create contact* action that uses hello SalesForce fields toocreate hello new new contact in Office 365.</span></span> 
   > 
   > 
5. <span data-ttu-id="07431-153">**Salvare** le modifiche (angolo superiore sinistro della barra degli strumenti hello).</span><span class="sxs-lookup"><span data-stu-id="07431-153">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="07431-154">L'app per la logica viene salvata e può essere attivata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="07431-154">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="07431-155">Dettagli specifici del connettore</span><span class="sxs-lookup"><span data-stu-id="07431-155">Connector-specific details</span></span>

<span data-ttu-id="07431-156">Visualizzare tutti i trigger e azioni definite in swagger hello e anche eventuali limiti di hello [dettagli connettore](/connectors/office365connector/).</span><span class="sxs-lookup"><span data-stu-id="07431-156">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/office365connector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="07431-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="07431-157">Next Steps</span></span>
<span data-ttu-id="07431-158">[Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="07431-158">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="07431-159">Esplorare hello altri connettori disponibile in App per la logica nel nostro [elenco API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="07431-159">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

