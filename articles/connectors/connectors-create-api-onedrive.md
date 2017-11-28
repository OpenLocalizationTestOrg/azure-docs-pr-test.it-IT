---
title: connettore di OneDrive aaaAdd hello nelle App logica | Documenti Microsoft
description: Panoramica del connettore di hello OneDrive con i parametri di API REST
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
ms.openlocfilehash: 8303794bb3c2844de288f87f40639abb84c160fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-onedrive-connector"></a><span data-ttu-id="08d06-103">Iniziare con il connettore di OneDrive hello</span><span class="sxs-lookup"><span data-stu-id="08d06-103">Get started with hello OneDrive connector</span></span>
<span data-ttu-id="08d06-104">Connettersi tooOneDrive toomanage dei file, inclusi il caricamento, get, eliminare i file e molto altro.</span><span class="sxs-lookup"><span data-stu-id="08d06-104">Connect tooOneDrive toomanage your files, including upload, get, delete files, and more.</span></span> 

<span data-ttu-id="08d06-105">Con OneDrive è possibile:</span><span class="sxs-lookup"><span data-stu-id="08d06-105">With OneDrive, you:</span></span> 

* <span data-ttu-id="08d06-106">Creare un flusso di lavoro mediante l'archiviazione di file in OneDrive o aggiornare i file esistenti in OneDrive.</span><span class="sxs-lookup"><span data-stu-id="08d06-106">Build your workflow by storing files in OneDrive, or update existing files in OneDrive.</span></span> 
* <span data-ttu-id="08d06-107">Utilizzare trigger toostart il flusso di lavoro quando un file viene creato o aggiornato all'interno di OneDrive.</span><span class="sxs-lookup"><span data-stu-id="08d06-107">Use triggers toostart your workflow when a file is created or updated within your OneDrive.</span></span>
* <span data-ttu-id="08d06-108">Usare azioni toocreate un file, eliminare un file e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="08d06-108">Use actions toocreate a file, delete a file, and more.</span></span> <span data-ttu-id="08d06-109">Ad esempio, creare un nuovo file in OneDrive (azione) quando viene ricevuto un nuovo messaggio di posta elettronica di Office 365 con un allegato (trigger).</span><span class="sxs-lookup"><span data-stu-id="08d06-109">For example, when a new Office 365 email is received with an attachment (a trigger), create a new file in OneDrive (an action).</span></span>

<span data-ttu-id="08d06-110">Questo argomento viene illustrato come toouse hello OneDrive connettore in un'app di logica e anche gli elenchi di hello azioni e trigger.</span><span class="sxs-lookup"><span data-stu-id="08d06-110">This topic shows you how toouse hello OneDrive connector in a logic app, and also lists hello triggers and actions.</span></span>

<span data-ttu-id="08d06-111">toolearn informazioni sulle App per la logica, vedere [quali sono le app logica](../logic-apps/logic-apps-what-are-logic-apps.md) e [creare un'app di logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="08d06-111">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooonedrive"></a><span data-ttu-id="08d06-112">Connettersi tooOneDrive</span><span class="sxs-lookup"><span data-stu-id="08d06-112">Connect tooOneDrive</span></span>
<span data-ttu-id="08d06-113">Prima che la logica app possa accedere a qualsiasi servizio, creare innanzitutto un *connessione* toohello servizio.</span><span class="sxs-lookup"><span data-stu-id="08d06-113">Before your logic app can access any service, you first create a *connection* toohello service.</span></span> <span data-ttu-id="08d06-114">Una connessione fornisce la connettività tra un'app per la logica e un altro servizio.</span><span class="sxs-lookup"><span data-stu-id="08d06-114">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="08d06-115">Ad esempio, tooOneDrive tooconnect, è necessario innanzitutto un OneDrive *connessione*.</span><span class="sxs-lookup"><span data-stu-id="08d06-115">For example, tooconnect tooOneDrive, you first need a OneDrive *connection*.</span></span> <span data-ttu-id="08d06-116">toocreate una connessione, immettere le credenziali di hello utilizzato normalmente il servizio di hello tooaccess desiderato tooconnect per.</span><span class="sxs-lookup"><span data-stu-id="08d06-116">toocreate a connection, enter hello credentials you normally use tooaccess hello service you wish tooconnect to.</span></span> <span data-ttu-id="08d06-117">In tal caso, OneDrive, immettere hello credenziali tooyour OneDrive toocreate hello connessione ad account di.</span><span class="sxs-lookup"><span data-stu-id="08d06-117">So, with OneDrive, enter hello credentials tooyour OneDrive account  toocreate hello connection.</span></span>

### <a name="create-hello-connection"></a><span data-ttu-id="08d06-118">Creare una connessione hello</span><span class="sxs-lookup"><span data-stu-id="08d06-118">Create hello connection</span></span>
> [!INCLUDE [Steps toocreate a connection tooOneDrive](../../includes/connectors-create-api-onedrive.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="08d06-119">Usare un trigger</span><span class="sxs-lookup"><span data-stu-id="08d06-119">Use a trigger</span></span>
<span data-ttu-id="08d06-120">Un trigger è un evento che può essere utilizzato toostart flusso di lavoro hello definito in un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="08d06-120">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="08d06-121">I trigger "polling" servizio hello in corrispondenza di un intervallo e la frequenza desiderata.</span><span class="sxs-lookup"><span data-stu-id="08d06-121">Triggers "poll" hello service at an interval and frequency that you want.</span></span> <span data-ttu-id="08d06-122">[Altre informazioni sui trigger](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="08d06-122">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="08d06-123">Nell'app logica hello, digitare "onedrive" tooget un elenco dei trigger hello:</span><span class="sxs-lookup"><span data-stu-id="08d06-123">In hello logic app, type "onedrive" tooget a list of hello triggers:</span></span>  
   
    ![](./media/connectors-create-api-onedrive/onedrive-1.png)
2. <span data-ttu-id="08d06-124">Selezionare **Quando viene modificato un file**.</span><span class="sxs-lookup"><span data-stu-id="08d06-124">Select **When a file is modified**.</span></span> <span data-ttu-id="08d06-125">Se esiste già una connessione, quindi selezionare hello selezione Mostra pulsante tooselect una cartella.</span><span class="sxs-lookup"><span data-stu-id="08d06-125">If a connection already exists, then select hello Show Picker button tooselect a folder.</span></span>
   
    ![](./media/connectors-create-api-onedrive/sample-folder.png)
   
    <span data-ttu-id="08d06-126">Nel caso di richiesta toosign in, quindi immettere hello sign in connessione hello toocreate di dettagli.</span><span class="sxs-lookup"><span data-stu-id="08d06-126">If you are prompted toosign in, then enter hello sign in details toocreate hello connection.</span></span> <span data-ttu-id="08d06-127">[Creare una connessione hello](connectors-create-api-onedrive.md#create-the-connection) in questo argomento vengono elencati i passaggi di hello.</span><span class="sxs-lookup"><span data-stu-id="08d06-127">[Create hello connection](connectors-create-api-onedrive.md#create-the-connection) in this topic lists hello steps.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="08d06-128">In questo esempio hello logica app viene eseguita quando un file nella cartella hello che scelto viene aggiornato.</span><span class="sxs-lookup"><span data-stu-id="08d06-128">In this example, hello logic app runs when a file in hello folder you choose is updated.</span></span> <span data-ttu-id="08d06-129">risultati di hello toosee del trigger, aggiungere un'altra azione che invia un messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="08d06-129">toosee hello results of this trigger, add another action that sends you an email.</span></span> <span data-ttu-id="08d06-130">Ad esempio, aggiungere hello Outlook di Office 365 *invia un messaggio di posta elettronica* azione che tramite posta elettronica quando viene aggiornato un file.</span><span class="sxs-lookup"><span data-stu-id="08d06-130">For example, add hello Office 365 Outlook *Send an email* action that emails you when a file is updated.</span></span> 

3. <span data-ttu-id="08d06-131">Seleziona hello **modifica** pulsante e impostare hello **frequenza** e **intervallo** valori.</span><span class="sxs-lookup"><span data-stu-id="08d06-131">Select hello **Edit** button and set hello **Frequency** and **Interval** values.</span></span> <span data-ttu-id="08d06-132">Ad esempio, se si desidera hello trigger toopoll ogni 15 minuti, quindi impostare hello **frequenza** troppo**minuto**e set hello **intervallo** troppo**15**.</span><span class="sxs-lookup"><span data-stu-id="08d06-132">For example, if you want hello trigger toopoll every 15 minutes, then set hello **Frequency** too**Minute**, and set hello **Interval** too**15**.</span></span> 
   
    ![](./media/connectors-create-api-onedrive/trigger-properties.png)
4. <span data-ttu-id="08d06-133">**Salvare** le modifiche (angolo superiore sinistro della barra degli strumenti hello).</span><span class="sxs-lookup"><span data-stu-id="08d06-133">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="08d06-134">L'app per la logica viene salvata e può essere attivata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="08d06-134">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="08d06-135">Usare un'azione</span><span class="sxs-lookup"><span data-stu-id="08d06-135">Use an action</span></span>
<span data-ttu-id="08d06-136">Un'azione è un'operazione effettuata dal flusso di lavoro hello definito in un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="08d06-136">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="08d06-137">[Altre informazioni sulle azioni](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="08d06-137">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="08d06-138">Selezionare hello sul segno più.</span><span class="sxs-lookup"><span data-stu-id="08d06-138">Select hello plus sign.</span></span> <span data-ttu-id="08d06-139">Vedrai diverse opzioni: **aggiungere un'azione**, **aggiungere una condizione**, o uno dei hello **più** opzioni.</span><span class="sxs-lookup"><span data-stu-id="08d06-139">You see several choices: **Add an action**, **Add a condition**, or one of hello **More** options.</span></span>
   
    ![](./media/connectors-create-api-onedrive/add-action.png)
2. <span data-ttu-id="08d06-140">Selezionare **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="08d06-140">Choose **Add an action**.</span></span>
3. <span data-ttu-id="08d06-141">Nella casella di testo hello, digitare "onedrive" tooget un elenco di tutte le azioni disponibili hello.</span><span class="sxs-lookup"><span data-stu-id="08d06-141">In hello text box, type “onedrive” tooget a list of all hello available actions.</span></span>
   
    ![](./media/connectors-create-api-onedrive/onedrive-actions.png) 
4. <span data-ttu-id="08d06-142">Nell'esempio scegliere **OneDrive - Crea file**.</span><span class="sxs-lookup"><span data-stu-id="08d06-142">In our example, choose **OneDrive - Create file**.</span></span> <span data-ttu-id="08d06-143">Se esiste già una connessione, quindi selezionare hello **percorso della cartella** tooput hello file, immettere hello **nome File**e scegliere hello **contenuto File** desiderato:</span><span class="sxs-lookup"><span data-stu-id="08d06-143">If a connection already exists, then select hello **Folder Path** tooput hello file, enter hello **File Name**, and choose hello **File Content** you want:</span></span>  
   
    ![](./media/connectors-create-api-onedrive/sample-action.png)
   
    <span data-ttu-id="08d06-144">Se viene chiesto di hello informazioni di connessione, quindi immettere connessione hello toocreate dettagli di hello.</span><span class="sxs-lookup"><span data-stu-id="08d06-144">If you are prompted for hello connection information, then enter hello details toocreate hello connection.</span></span> <span data-ttu-id="08d06-145">[Creare una connessione hello](connectors-create-api-onedrive.md#create-the-connection) in questo argomento vengono descritte queste proprietà.</span><span class="sxs-lookup"><span data-stu-id="08d06-145">[Create hello connection](connectors-create-api-onedrive.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="08d06-146">In questo esempio creiamo un nuovo file in una cartella di OneDrive.</span><span class="sxs-lookup"><span data-stu-id="08d06-146">In this example, we create a new file in a OneDrive folder.</span></span> <span data-ttu-id="08d06-147">È possibile utilizzare l'output da un altro file di OneDrive hello di toocreate trigger.</span><span class="sxs-lookup"><span data-stu-id="08d06-147">You can use output from another trigger toocreate hello OneDrive file.</span></span> <span data-ttu-id="08d06-148">Ad esempio, aggiungere hello Outlook di Office 365 *all'arrivo di un nuovo indirizzo e-mail* trigger.</span><span class="sxs-lookup"><span data-stu-id="08d06-148">For example, add hello Office 365 Outlook *When a new email arrives* trigger.</span></span> <span data-ttu-id="08d06-149">Aggiungere quindi hello OneDrive *crea file* azione che utilizza hello allegati e i campi di tipo di contenuto all'interno di ForEach toocreate hello nuovo file in OneDrive.</span><span class="sxs-lookup"><span data-stu-id="08d06-149">Then add hello OneDrive *Create file* action that uses hello Attachments and Content-Type fields within a ForEach toocreate hello new file in OneDrive.</span></span> 
   > 
   > ![](./media/connectors-create-api-onedrive/foreach-action.png)

5. <span data-ttu-id="08d06-150">**Salvare** le modifiche (angolo superiore sinistro della barra degli strumenti hello).</span><span class="sxs-lookup"><span data-stu-id="08d06-150">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="08d06-151">L'app per la logica viene salvata e può essere attivata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="08d06-151">Your logic app is saved and may be automatically enabled.</span></span>


## <a name="connector-specific-details"></a><span data-ttu-id="08d06-152">Dettagli specifici del connettore</span><span class="sxs-lookup"><span data-stu-id="08d06-152">Connector-specific details</span></span>

<span data-ttu-id="08d06-153">Visualizzare tutti i trigger e azioni definite in swagger hello e anche eventuali limiti di hello [dettagli connettore](/connectors/onedriveconnector/).</span><span class="sxs-lookup"><span data-stu-id="08d06-153">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/onedriveconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="08d06-154">Altri connettori</span><span class="sxs-lookup"><span data-stu-id="08d06-154">More connectors</span></span>
<span data-ttu-id="08d06-155">Tornare indietro toohello [elenco API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="08d06-155">Go back toohello [APIs list](apis-list.md).</span></span>
