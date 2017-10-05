---
title: Aggiungere il connettore OneDrive nelle app per la logica | Documentazione Microsoft
description: Panoramica del connettore OneDrive con i parametri dell'API REST.
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 47a8582a-1b1a-4fc3-beb5-97c60c4306fe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 63bd33bf4e09b98aa53dcfec9fcc4a0109204952
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-onedrive-connector"></a><span data-ttu-id="79c39-103">Introduzione al connettore OneDrive</span><span class="sxs-lookup"><span data-stu-id="79c39-103">Get started with the OneDrive connector</span></span>
<span data-ttu-id="79c39-104">Connettersi a OneDrive per gestire i file, ad esempio, caricare, recuperare ed eliminare i file e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="79c39-104">Connect to OneDrive to manage your files, including upload, get, delete files, and more.</span></span> 

<span data-ttu-id="79c39-105">Con OneDrive è possibile:</span><span class="sxs-lookup"><span data-stu-id="79c39-105">With OneDrive, you:</span></span> 

* <span data-ttu-id="79c39-106">Creare un flusso di lavoro mediante l'archiviazione di file in OneDrive o aggiornare i file esistenti in OneDrive.</span><span class="sxs-lookup"><span data-stu-id="79c39-106">Build your workflow by storing files in OneDrive, or update existing files in OneDrive.</span></span> 
* <span data-ttu-id="79c39-107">Usare trigger per avviare il flusso di lavoro quando un file viene creato o aggiornato in OneDrive.</span><span class="sxs-lookup"><span data-stu-id="79c39-107">Use triggers to start your workflow when a file is created or updated within your OneDrive.</span></span>
* <span data-ttu-id="79c39-108">Usare le azioni per creare un file, eliminarlo e così via.</span><span class="sxs-lookup"><span data-stu-id="79c39-108">Use actions to create a file, delete a file, and more.</span></span> <span data-ttu-id="79c39-109">Ad esempio, creare un nuovo file in OneDrive (azione) quando viene ricevuto un nuovo messaggio di posta elettronica di Office 365 con un allegato (trigger).</span><span class="sxs-lookup"><span data-stu-id="79c39-109">For example, when a new Office 365 email is received with an attachment (a trigger), create a new file in OneDrive (an action).</span></span>

<span data-ttu-id="79c39-110">Questo argomento illustra come usare il connettore OneDrive in un'app per la logica ed elenca i trigger e le azioni.</span><span class="sxs-lookup"><span data-stu-id="79c39-110">This topic shows you how to use the OneDrive connector in a logic app, and also lists the triggers and actions.</span></span>

<span data-ttu-id="79c39-111">Per altre informazioni sulle app per la logica, vedere [Cosa sono le app per la logica](../logic-apps/logic-apps-what-are-logic-apps.md) e [Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="79c39-111">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-onedrive"></a><span data-ttu-id="79c39-112">Connettersi a OneDrive</span><span class="sxs-lookup"><span data-stu-id="79c39-112">Connect to OneDrive</span></span>
<span data-ttu-id="79c39-113">Prima che l'app per la logica possa accedere a qualsiasi servizio, è necessario creare una *connessione* al servizio.</span><span class="sxs-lookup"><span data-stu-id="79c39-113">Before your logic app can access any service, you first create a *connection* to the service.</span></span> <span data-ttu-id="79c39-114">Una connessione fornisce la connettività tra un'app per la logica e un altro servizio.</span><span class="sxs-lookup"><span data-stu-id="79c39-114">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="79c39-115">Ad esempio, per connettersi a OneDrive, è necessaria prima di tutto una *connessione* a OneDrive.</span><span class="sxs-lookup"><span data-stu-id="79c39-115">For example, to connect to OneDrive, you first need a OneDrive *connection*.</span></span> <span data-ttu-id="79c39-116">Per creare una connessione, immettere le credenziali che si usano normalmente per accedere al servizio a cui si vuole connettersi.</span><span class="sxs-lookup"><span data-stu-id="79c39-116">To create a connection, enter the credentials you normally use to access the service you wish to connect to.</span></span> <span data-ttu-id="79c39-117">Quindi, per creare la connessione a OneDrive, immettere le credenziali dell'account OneDrive.</span><span class="sxs-lookup"><span data-stu-id="79c39-117">So, with OneDrive, enter the credentials to your OneDrive account  to create the connection.</span></span>

### <a name="create-the-connection"></a><span data-ttu-id="79c39-118">Creare la connessione</span><span class="sxs-lookup"><span data-stu-id="79c39-118">Create the connection</span></span>
> [!INCLUDE [Steps to create a connection to OneDrive](../../includes/connectors-create-api-onedrive.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="79c39-119">Usare un trigger</span><span class="sxs-lookup"><span data-stu-id="79c39-119">Use a trigger</span></span>
<span data-ttu-id="79c39-120">Un trigger è un evento che può essere usato per avviare il flusso di lavoro definito in un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="79c39-120">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="79c39-121">I trigger eseguono il "polling" del servizio agli intervalli e con la frequenza desiderati.</span><span class="sxs-lookup"><span data-stu-id="79c39-121">Triggers "poll" the service at an interval and frequency that you want.</span></span> <span data-ttu-id="79c39-122">[Altre informazioni sui trigger](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="79c39-122">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="79c39-123">Nell'app per la logica digitare "onedrive" per ottenere l'elenco dei trigger:</span><span class="sxs-lookup"><span data-stu-id="79c39-123">In the logic app, type "onedrive" to get a list of the triggers:</span></span>  
   
    ![](./media/connectors-create-api-onedrive/onedrive-1.png)
2. <span data-ttu-id="79c39-124">Selezionare **Quando viene modificato un file**.</span><span class="sxs-lookup"><span data-stu-id="79c39-124">Select **When a file is modified**.</span></span> <span data-ttu-id="79c39-125">Se esiste già una connessione, selezionare il pulsante Mostra selezione per selezionare una cartella.</span><span class="sxs-lookup"><span data-stu-id="79c39-125">If a connection already exists, then select the Show Picker button to select a folder.</span></span>
   
    ![](./media/connectors-create-api-onedrive/sample-folder.png)
   
    <span data-ttu-id="79c39-126">Se viene chiesto di effettuare l'accesso, immettere i dettagli di accesso per creare la connessione.</span><span class="sxs-lookup"><span data-stu-id="79c39-126">If you are prompted to sign in, then enter the sign in details to create the connection.</span></span> <span data-ttu-id="79c39-127">La sezione [Creare la connessione](connectors-create-api-onedrive.md#create-the-connection) di questo argomento elenca i passaggi necessari.</span><span class="sxs-lookup"><span data-stu-id="79c39-127">[Create the connection](connectors-create-api-onedrive.md#create-the-connection) in this topic lists the steps.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="79c39-128">In questo esempio l'app per la logica viene eseguita quando viene aggiornato un file nella cartella scelta.</span><span class="sxs-lookup"><span data-stu-id="79c39-128">In this example, the logic app runs when a file in the folder you choose is updated.</span></span> <span data-ttu-id="79c39-129">Per vedere i risultati del trigger, aggiungere un'altra azione che invia un messaggio di posta elettronica al proprio indirizzo.</span><span class="sxs-lookup"><span data-stu-id="79c39-129">To see the results of this trigger, add another action that sends you an email.</span></span> <span data-ttu-id="79c39-130">Ad esempio, aggiungere l'azione di Office 365 Outlook *Invia un messaggio di posta elettronica* per ricevere un messaggio di posta elettronica quando un file viene aggiornato.</span><span class="sxs-lookup"><span data-stu-id="79c39-130">For example, add the Office 365 Outlook *Send an email* action that emails you when a file is updated.</span></span> 

3. <span data-ttu-id="79c39-131">Selezionare il pulsante **Modifica** e impostare i valori **Frequenza** e **Intervallo**.</span><span class="sxs-lookup"><span data-stu-id="79c39-131">Select the **Edit** button and set the **Frequency** and **Interval** values.</span></span> <span data-ttu-id="79c39-132">Ad esempio, se si vuole che il trigger esegua il poll ogni 15 minuti, impostare **Frequenza** su **Minuto** e **Intervallo** su **15**.</span><span class="sxs-lookup"><span data-stu-id="79c39-132">For example, if you want the trigger to poll every 15 minutes, then set the **Frequency** to **Minute**, and set the **Interval** to **15**.</span></span> 
   
    ![](./media/connectors-create-api-onedrive/trigger-properties.png)
4. <span data-ttu-id="79c39-133">Scegliere **Salva** nell'angolo in alto a sinistra della barra degli strumenti per salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="79c39-133">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="79c39-134">L'app per la logica viene salvata e può essere attivata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="79c39-134">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="79c39-135">Usare un'azione</span><span class="sxs-lookup"><span data-stu-id="79c39-135">Use an action</span></span>
<span data-ttu-id="79c39-136">Un'azione è un'operazione eseguita dal flusso di lavoro e definita in un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="79c39-136">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="79c39-137">[Altre informazioni sulle azioni](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="79c39-137">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="79c39-138">Selezionare il segno più.</span><span class="sxs-lookup"><span data-stu-id="79c39-138">Select the plus sign.</span></span> <span data-ttu-id="79c39-139">Sono disponibili varie opzioni: **Aggiungi un'azione**, **Aggiungi una condizione** e le opzioni in **Altro**.</span><span class="sxs-lookup"><span data-stu-id="79c39-139">You see several choices: **Add an action**, **Add a condition**, or one of the **More** options.</span></span>
   
    ![](./media/connectors-create-api-onedrive/add-action.png)
2. <span data-ttu-id="79c39-140">Selezionare **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="79c39-140">Choose **Add an action**.</span></span>
3. <span data-ttu-id="79c39-141">Nella casella di testo digitare "onedrive" per ottenere l'elenco di tutte le azioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="79c39-141">In the text box, type “onedrive” to get a list of all the available actions.</span></span>
   
    ![](./media/connectors-create-api-onedrive/onedrive-actions.png) 
4. <span data-ttu-id="79c39-142">Nell'esempio scegliere **OneDrive - Crea file**.</span><span class="sxs-lookup"><span data-stu-id="79c39-142">In our example, choose **OneDrive - Create file**.</span></span> <span data-ttu-id="79c39-143">Se esiste già una connessione, selezionare il **percorso della cartella** in cui inserire il file, immettere il **nome del file** e scegliere il **contenuto del file** desiderato:</span><span class="sxs-lookup"><span data-stu-id="79c39-143">If a connection already exists, then select the **Folder Path** to put the file, enter the **File Name**, and choose the **File Content** you want:</span></span>  
   
    ![](./media/connectors-create-api-onedrive/sample-action.png)
   
    <span data-ttu-id="79c39-144">Se viene richiesto di inserire le informazioni di connessione, immettere i dettagli per creare la connessione.</span><span class="sxs-lookup"><span data-stu-id="79c39-144">If you are prompted for the connection information, then enter the details to create the connection.</span></span> <span data-ttu-id="79c39-145">La sezione [Creare la connessione](connectors-create-api-onedrive.md#create-the-connection) di questo argomento descrive queste proprietà.</span><span class="sxs-lookup"><span data-stu-id="79c39-145">[Create the connection](connectors-create-api-onedrive.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="79c39-146">In questo esempio creiamo un nuovo file in una cartella di OneDrive.</span><span class="sxs-lookup"><span data-stu-id="79c39-146">In this example, we create a new file in a OneDrive folder.</span></span> <span data-ttu-id="79c39-147">Per creare il file di OneDrive è possibile usare l'output di un altro trigger.</span><span class="sxs-lookup"><span data-stu-id="79c39-147">You can use output from another trigger to create the OneDrive file.</span></span> <span data-ttu-id="79c39-148">Ad esempio aggiungere il trigger di Office 365 Outlook *All'arrivo di un nuovo messaggio di posta elettronica*.</span><span class="sxs-lookup"><span data-stu-id="79c39-148">For example, add the Office 365 Outlook *When a new email arrives* trigger.</span></span> <span data-ttu-id="79c39-149">Quindi aggiungere l'azione di OneDrive *Crea file* che usa i campi Allegati e Content-Type in un ciclo ForEach per creare il nuovo file in OneDrive.</span><span class="sxs-lookup"><span data-stu-id="79c39-149">Then add the OneDrive *Create file* action that uses the Attachments and Content-Type fields within a ForEach to create the new file in OneDrive.</span></span> 
   > 
   > ![](./media/connectors-create-api-onedrive/foreach-action.png)

5. <span data-ttu-id="79c39-150">Scegliere **Salva** nell'angolo in alto a sinistra della barra degli strumenti per salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="79c39-150">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="79c39-151">L'app per la logica viene salvata e può essere attivata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="79c39-151">Your logic app is saved and may be automatically enabled.</span></span>


## <a name="connector-specific-details"></a><span data-ttu-id="79c39-152">Dettagli specifici del connettore</span><span class="sxs-lookup"><span data-stu-id="79c39-152">Connector-specific details</span></span>

<span data-ttu-id="79c39-153">Per visualizzare eventuali azioni e trigger definiti in Swagger ed eventuali limiti, vedere i [dettagli del connettore](/connectors/onedriveconnector/).</span><span class="sxs-lookup"><span data-stu-id="79c39-153">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/onedriveconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="79c39-154">Altri connettori</span><span class="sxs-lookup"><span data-stu-id="79c39-154">More connectors</span></span>
<span data-ttu-id="79c39-155">Tornare all' [elenco di API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="79c39-155">Go back to the [APIs list](apis-list.md).</span></span>