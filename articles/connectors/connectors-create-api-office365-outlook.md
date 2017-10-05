---
title: Aggiungere il connettore Office 365 Outlook nelle app per la logica | Microsoft Docs
description: Creare app per la logica con il connettore Office 365 per consentire l'interazione con Office 365. Ad esempio, per creare, modificare e aggiornare contatti ed elementi del calendario.
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
ms.openlocfilehash: 5335dae62e61659b68e8befb4ed0d404dffb800c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-office-365-outlook-connector"></a><span data-ttu-id="c60ee-104">Guida introduttiva al connettore Outlook di Office 365</span><span class="sxs-lookup"><span data-stu-id="c60ee-104">Get started with the Office 365 Outlook connector</span></span>
<span data-ttu-id="c60ee-105">Il connettore Office 365 Outlook consente l'interazione con Outlook in Office 365.</span><span class="sxs-lookup"><span data-stu-id="c60ee-105">The Office 365 Outlook connector enables interaction with Outlook in Office 365.</span></span> <span data-ttu-id="c60ee-106">Usare questo connettore per creare, modificare e aggiornare i contatti e gli elementi del calendario e anche per ottenere, inviare e rispondere ai messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="c60ee-106">Use this connector to create, edit, and update contacts and calendar items, and also get, send, and reply to email.</span></span>

<span data-ttu-id="c60ee-107">Con Office 365 Outlook è possibile:</span><span class="sxs-lookup"><span data-stu-id="c60ee-107">With Office 365 Outlook, you:</span></span>

* <span data-ttu-id="c60ee-108">Creare il flusso di lavoro usando le funzionalità di posta elettronica e calendario in Office 365.</span><span class="sxs-lookup"><span data-stu-id="c60ee-108">Build your workflow using the email and calendar features within Office 365.</span></span> 
* <span data-ttu-id="c60ee-109">Usare i trigger per avviare il flusso di lavoro quando è presente un nuovo messaggio di posta elettronica, quando viene aggiornato un elemento del calendario e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="c60ee-109">Use triggers to start your workflow when there is a new email, when a calendar item is updated, and more.</span></span>
* <span data-ttu-id="c60ee-110">Usare azioni per inviare un messaggio di posta elettronica, creare un nuovo evento del calendario e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="c60ee-110">Use actions to send an email, create a new calendar event, and more.</span></span> <span data-ttu-id="c60ee-111">Ad esempio, quando è presente un nuovo oggetto in Salesforce (trigger), inviare un messaggio di posta elettronica a Office 365 Outlook (azione).</span><span class="sxs-lookup"><span data-stu-id="c60ee-111">For example, when there is a new object in Salesforce (a trigger), send an email to your Office 365 Outlook (an action).</span></span> 

<span data-ttu-id="c60ee-112">Questo argomento illustra come usare il connettore Office 365 Outlook in un'app per la logica ed elenca i trigger e le azioni.</span><span class="sxs-lookup"><span data-stu-id="c60ee-112">This topic shows you how to use the Office 365 Outlook connector in a logic app, and also lists the triggers and actions.</span></span>

> [!NOTE]
> <span data-ttu-id="c60ee-113">Questa versione dell'articolo si applica alla la disponibilità generale delle app per la logica.</span><span class="sxs-lookup"><span data-stu-id="c60ee-113">This version of the article applies to Logic Apps general availability (GA).</span></span>
> 
> 

<span data-ttu-id="c60ee-114">Per altre informazioni sulle app per la logica, vedere [Cosa sono le app per la logica](../logic-apps/logic-apps-what-are-logic-apps.md) e [Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="c60ee-114">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-office-365"></a><span data-ttu-id="c60ee-115">Connettersi a Office 365</span><span class="sxs-lookup"><span data-stu-id="c60ee-115">Connect to Office 365</span></span>
<span data-ttu-id="c60ee-116">Prima che l'app per la logica possa accedere a qualsiasi servizio, è necessario creare una *connessione* al servizio.</span><span class="sxs-lookup"><span data-stu-id="c60ee-116">Before your logic app can access any service, you first create a *connection* to the service.</span></span> <span data-ttu-id="c60ee-117">Una connessione fornisce la connettività tra un'app per la logica e un altro servizio.</span><span class="sxs-lookup"><span data-stu-id="c60ee-117">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="c60ee-118">Ad esempio, per connettersi a Office 365 Outlook, è necessaria prima di tutto una *connessione* a Office 365.</span><span class="sxs-lookup"><span data-stu-id="c60ee-118">For example, to connect to Office 365 Outlook, you first need an Office 365 *connection*.</span></span> <span data-ttu-id="c60ee-119">Per creare una connessione, immettere le credenziali che si usano normalmente per accedere al servizio a cui si vuole connettersi.</span><span class="sxs-lookup"><span data-stu-id="c60ee-119">To create a connection, enter the credentials you normally use to access the service you wish to connect to.</span></span> <span data-ttu-id="c60ee-120">Pertanto, per creare la connessione a Office 365 Outlook, immettere le credenziali dell'account Office 365 Outlook.</span><span class="sxs-lookup"><span data-stu-id="c60ee-120">So with Office 365 Outlook, enter the credentials to your Office 365 account to create the connection.</span></span>

## <a name="create-the-connection"></a><span data-ttu-id="c60ee-121">Creare la connessione</span><span class="sxs-lookup"><span data-stu-id="c60ee-121">Create the connection</span></span>
> [!INCLUDE [Steps to create a connection to Office 365](../../includes/connectors-create-api-office365-outlook.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="c60ee-122">Usare un trigger</span><span class="sxs-lookup"><span data-stu-id="c60ee-122">Use a trigger</span></span>
<span data-ttu-id="c60ee-123">Un trigger è un evento che può essere usato per avviare il flusso di lavoro definito in un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="c60ee-123">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="c60ee-124">I trigger eseguono il "polling" del servizio agli intervalli e con la frequenza desiderati.</span><span class="sxs-lookup"><span data-stu-id="c60ee-124">Triggers "poll" the service at an interval and frequency that you want.</span></span> <span data-ttu-id="c60ee-125">[Altre informazioni sui trigger](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="c60ee-125">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="c60ee-126">Nell'app per la logica digitare "office 365" per ottenere l'elenco dei trigger:</span><span class="sxs-lookup"><span data-stu-id="c60ee-126">In the logic app, type "office 365" to get a list of the triggers:</span></span>  
   
    ![](./media/connectors-create-api-office365-outlook/office365-trigger.png)
2. <span data-ttu-id="c60ee-127">Selezionare **Office 365 Outlook - All'avvio imminente di un prossimo evento**.</span><span class="sxs-lookup"><span data-stu-id="c60ee-127">Select **Office 365 Outlook - When an upcoming event is starting soon**.</span></span> <span data-ttu-id="c60ee-128">Se esiste già una connessione, selezionare un calendario dall'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="c60ee-128">If a connection already exists, then select a calendar from the drop-down list.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/sample-calendar.png)
   
    <span data-ttu-id="c60ee-129">Se viene chiesto di effettuare l'accesso, immettere i dettagli di accesso per creare la connessione.</span><span class="sxs-lookup"><span data-stu-id="c60ee-129">If you are prompted to sign in, then enter the sign in details to create the connection.</span></span> <span data-ttu-id="c60ee-130">La sezione [Creare la connessione](connectors-create-api-office365-outlook.md#create-the-connection) di questo argomento elenca i passaggi necessari.</span><span class="sxs-lookup"><span data-stu-id="c60ee-130">[Create the connection](connectors-create-api-office365-outlook.md#create-the-connection) in this topic lists the steps.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="c60ee-131">In questo esempio l'app per la logica viene eseguita quando viene aggiornato un evento del calendario.</span><span class="sxs-lookup"><span data-stu-id="c60ee-131">In this example, the logic app runs when a calendar event is updated.</span></span> <span data-ttu-id="c60ee-132">Per vedere i risultati del trigger, aggiungere un'altra azione che invia un SMS al proprio cellulare.</span><span class="sxs-lookup"><span data-stu-id="c60ee-132">To see the results of this trigger, add another action that sends you a text message.</span></span> <span data-ttu-id="c60ee-133">Ad esempio, aggiungere l'azione di Twilio *Send message* (Invia messaggio) che invia un SMS 15 minuti prima dell'avvio dell'evento del calendario.</span><span class="sxs-lookup"><span data-stu-id="c60ee-133">For example, add the Twilio *Send message* action that texts you when the calendar event is starting in 15 minutes.</span></span> 
   > 
   > 
3. <span data-ttu-id="c60ee-134">Selezionare il pulsante **Modifica** e impostare i valori **Frequenza** e **Intervallo**.</span><span class="sxs-lookup"><span data-stu-id="c60ee-134">Select the **Edit** button and set the **Frequency** and **Interval** values.</span></span> <span data-ttu-id="c60ee-135">Ad esempio, se si vuole che il trigger esegua il poll ogni 15 minuti, impostare **Frequenza** su **Minuto** e **Intervallo** su **15**.</span><span class="sxs-lookup"><span data-stu-id="c60ee-135">For example, if you want the trigger to poll every 15 minutes, then set the **Frequency** to **Minute**, and set the **Interval** to **15**.</span></span> 
   
    ![](./media/connectors-create-api-office365-outlook/calendar-settings.png)
4. <span data-ttu-id="c60ee-136">Scegliere **Salva** nell'angolo in alto a sinistra della barra degli strumenti per salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="c60ee-136">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="c60ee-137">L'app per la logica viene salvata e può essere attivata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="c60ee-137">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="c60ee-138">Usare un'azione</span><span class="sxs-lookup"><span data-stu-id="c60ee-138">Use an action</span></span>
<span data-ttu-id="c60ee-139">Un'azione è un'operazione eseguita dal flusso di lavoro e definita in un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="c60ee-139">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="c60ee-140">[Altre informazioni sulle azioni](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="c60ee-140">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="c60ee-141">Selezionare il segno più.</span><span class="sxs-lookup"><span data-stu-id="c60ee-141">Select the plus sign.</span></span> <span data-ttu-id="c60ee-142">Sono disponibili varie opzioni: **Aggiungi un'azione**, **Aggiungi una condizione** e le opzioni in **Altro**.</span><span class="sxs-lookup"><span data-stu-id="c60ee-142">You see several choices: **Add an action**, **Add a condition**, or one of the **More** options.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/add-action.png)
2. <span data-ttu-id="c60ee-143">Selezionare **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="c60ee-143">Choose **Add an action**.</span></span>
3. <span data-ttu-id="c60ee-144">Nella casella di testo digitare "office 365" per ottenere l'elenco di tutte le azioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="c60ee-144">In the text box, type “office 365” to get a list of all the available actions.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/office365-actions.png) 
4. <span data-ttu-id="c60ee-145">Nell'esempio scegliere **Office 365 Outlook - Crea contatto**.</span><span class="sxs-lookup"><span data-stu-id="c60ee-145">In our example, choose **Office 365 Outlook - Create contact**.</span></span> <span data-ttu-id="c60ee-146">Se esiste già una connessione, scegliere l'**ID cartella**, il **nome** e le altre proprietà:</span><span class="sxs-lookup"><span data-stu-id="c60ee-146">If a connection already exists, then choose the **Folder ID**, **Given Name**, and other properties:</span></span>  
   
    ![](./media/connectors-create-api-office365-outlook/office365-sampleaction.png)
   
    <span data-ttu-id="c60ee-147">Se viene richiesto di inserire le informazioni di connessione, immettere i dettagli per creare la connessione.</span><span class="sxs-lookup"><span data-stu-id="c60ee-147">If you are prompted for the connection information, then enter the details to create the connection.</span></span> <span data-ttu-id="c60ee-148">La sezione [Creare la connessione](connectors-create-api-office365-outlook.md#create-the-connection) di questo argomento descrive queste proprietà.</span><span class="sxs-lookup"><span data-stu-id="c60ee-148">[Create the connection](connectors-create-api-office365-outlook.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="c60ee-149">In questo esempio si crea un nuovo contatto in Office 365 Outlook.</span><span class="sxs-lookup"><span data-stu-id="c60ee-149">In this example, we create a new contact in Office 365 Outlook.</span></span> <span data-ttu-id="c60ee-150">Per creare il contatto è possibile usare l'output di un altro trigger.</span><span class="sxs-lookup"><span data-stu-id="c60ee-150">You can use output from another trigger to create the contact.</span></span> <span data-ttu-id="c60ee-151">Ad esempio, aggiungere il trigger di SalesForce *When an object is created* (Quando viene creato un oggetto).</span><span class="sxs-lookup"><span data-stu-id="c60ee-151">For example, add the SalesForce *When an object is created* trigger.</span></span> <span data-ttu-id="c60ee-152">Aggiungere quindi l'azione di Office 365 Outlook *Crea contatto* che usa i campi di SalesForce per creare il nuovo contatto in Office 365.</span><span class="sxs-lookup"><span data-stu-id="c60ee-152">Then add the Office 365 Outlook *Create contact* action that uses the SalesForce fields to create the new new contact in Office 365.</span></span> 
   > 
   > 
5. <span data-ttu-id="c60ee-153">Scegliere **Salva** nell'angolo in alto a sinistra della barra degli strumenti per salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="c60ee-153">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="c60ee-154">L'app per la logica viene salvata e può essere attivata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="c60ee-154">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="c60ee-155">Dettagli specifici del connettore</span><span class="sxs-lookup"><span data-stu-id="c60ee-155">Connector-specific details</span></span>

<span data-ttu-id="c60ee-156">Per visualizzare eventuali azioni e trigger definiti in Swagger ed eventuali limiti, vedere i [dettagli del connettore](/connectors/office365connector/).</span><span class="sxs-lookup"><span data-stu-id="c60ee-156">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/office365connector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c60ee-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c60ee-157">Next Steps</span></span>
<span data-ttu-id="c60ee-158">[Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="c60ee-158">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="c60ee-159">Esplorare gli altri connettori disponibili nelle app per la logica nell' [elenco delle API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="c60ee-159">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

