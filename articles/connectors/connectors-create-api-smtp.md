---
title: connettore aaaSMTP nelle app di logica di Azure | Documenti Microsoft
description: Creare app per la logica con Servizio app di Azure. Connettersi tramite posta elettronica toosend tooSMTP.
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d4141c08-88d7-4e59-a757-c06d0dc74300
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/15/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 36bb836851014d24f2e069fda8376ad7a08c943b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-smtp-connector"></a><span data-ttu-id="4e906-104">Iniziare con il connettore SMTP hello</span><span class="sxs-lookup"><span data-stu-id="4e906-104">Get started with hello SMTP connector</span></span>
<span data-ttu-id="4e906-105">Connettersi tramite posta elettronica toosend tooSMTP.</span><span class="sxs-lookup"><span data-stu-id="4e906-105">Connect tooSMTP toosend email.</span></span>

<span data-ttu-id="4e906-106">toouse [i connettori](apis-list.md), è necessario innanzitutto toocreate un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="4e906-106">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="4e906-107">Come prima operazione [creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="4e906-107">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toosmtp"></a><span data-ttu-id="4e906-108">Connettersi tooSMTP</span><span class="sxs-lookup"><span data-stu-id="4e906-108">Connect tooSMTP</span></span>
<span data-ttu-id="4e906-109">Prima che la logica app possa accedere a qualsiasi servizio, è necessario innanzitutto toocreate un *connessione* toohello servizio.</span><span class="sxs-lookup"><span data-stu-id="4e906-109">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="4e906-110">Una [connessione](connectors-overview.md) fornisce la connettività tra un'app per la logica e un altro servizio.</span><span class="sxs-lookup"><span data-stu-id="4e906-110">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="4e906-111">Ad esempio, tooSMTP tooconnect, è necessario innanzitutto un SMTP *connessione*.</span><span class="sxs-lookup"><span data-stu-id="4e906-111">For example, tooconnect tooSMTP, you first need an SMTP *connection*.</span></span> <span data-ttu-id="4e906-112">toocreate una connessione, immettere le credenziali di hello utilizzato normalmente il servizio di hello tooaccess ci si connette a.</span><span class="sxs-lookup"><span data-stu-id="4e906-112">toocreate a connection, enter hello credentials you normally use tooaccess hello service you connect to.</span></span> <span data-ttu-id="4e906-113">In tal caso, nell'esempio hello SMTP immettere hello credenziali tooyour connessione nome, indirizzo del server SMTP e utente accesso informazioni toocreate hello connessione tooSMTP.</span><span class="sxs-lookup"><span data-stu-id="4e906-113">So, in hello SMTP example, enter hello credentials tooyour connection name, SMTP server address, and user login information toocreate hello connection tooSMTP.</span></span>  

### <a name="create-a-connection-toosmtp"></a><span data-ttu-id="4e906-114">Creare una connessione tooSMTP</span><span class="sxs-lookup"><span data-stu-id="4e906-114">Create a connection tooSMTP</span></span>
> [!INCLUDE [Steps toocreate a connection tooSMTP](../../includes/connectors-create-api-smtp.md)]
> 
> 

## <a name="use-an-smtp-trigger"></a><span data-ttu-id="4e906-115">Usare un trigger SMTP</span><span class="sxs-lookup"><span data-stu-id="4e906-115">Use an SMTP trigger</span></span>
<span data-ttu-id="4e906-116">Un trigger è un evento che può essere utilizzato toostart flusso di lavoro hello definito in un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="4e906-116">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="4e906-117">[Altre informazioni sui trigger](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="4e906-117">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="4e906-118">In questo esempio, perché non dispone di un trigger di un proprio, SMTP utilizzeremo hello **Salesforce - quando viene creato un oggetto** trigger.</span><span class="sxs-lookup"><span data-stu-id="4e906-118">In this example, because SMTP does not have a trigger of its own, we'll use hello **Salesforce - When an object is created** trigger.</span></span> <span data-ttu-id="4e906-119">Questo trigger viene attivato quando viene creato un nuovo oggetto in Salesforce.</span><span class="sxs-lookup"><span data-stu-id="4e906-119">This trigger activates when a new object is created in Salesforce.</span></span> <span data-ttu-id="4e906-120">Per questo esempio, verrà configurato tale che ogni volta un nuovo cliente potenziale creato in Salesforce, un *inviare posta elettronica* azione si verifica tramite il connettore SMTP hello con una notifica di hello nuovo cliente potenziale da creare.</span><span class="sxs-lookup"><span data-stu-id="4e906-120">For our example, we'll set it up such that every time a new lead is created in Salesforce, a *send email* action occurs via hello SMTP connector with a notification of hello new lead being created.</span></span>

1. <span data-ttu-id="4e906-121">Immettere *salesforce* nella casella di ricerca hello nella finestra di progettazione di hello logica App, quindi selezionare hello **Salesforce - quando viene creato un oggetto** trigger.</span><span class="sxs-lookup"><span data-stu-id="4e906-121">Enter *salesforce* in hello search box on hello logic apps designer then select hello **Salesforce - When an object is created** trigger.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-1.png)  
2. <span data-ttu-id="4e906-122">Hello **quando viene creato un oggetto** controllo viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="4e906-122">hello **When an object is created** control is displayed.</span></span>
   ![](../../includes/media/connectors-create-api-salesforce/trigger-2.png)  
3. <span data-ttu-id="4e906-123">Seleziona hello **tipo di oggetto** selezionare *causare* elenco hello degli oggetti.</span><span class="sxs-lookup"><span data-stu-id="4e906-123">Select hello **Object Type** then select *Lead* from hello list of objects.</span></span> <span data-ttu-id="4e906-124">In questo passaggio si indica che si sta creando un trigger che invierà una notifica all'app per la logica ogni volta che viene creato un nuovo lead in Salesforce.</span><span class="sxs-lookup"><span data-stu-id="4e906-124">In this step you are indicating that you are creating a trigger that will notify your logic app whenever a new lead is created in Salesforce.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger3.png)  
4. <span data-ttu-id="4e906-125">Hello trigger è stato creato.</span><span class="sxs-lookup"><span data-stu-id="4e906-125">hello trigger has been created.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-4.png)  

## <a name="use-an-smtp-action"></a><span data-ttu-id="4e906-126">Usare un'azione SMTP</span><span class="sxs-lookup"><span data-stu-id="4e906-126">Use an SMTP action</span></span>
<span data-ttu-id="4e906-127">Un'azione è un'operazione effettuata dal flusso di lavoro hello definito in un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="4e906-127">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="4e906-128">[Altre informazioni sulle azioni](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="4e906-128">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="4e906-129">Ora che hello trigger è stato aggiunto, seguire queste azioni tooadd un SMTP passaggi che si verificano quando viene creato un nuovo cliente potenziale in Salesforce.</span><span class="sxs-lookup"><span data-stu-id="4e906-129">Now that hello trigger has been added, follow these steps tooadd an SMTP action that will occur when a new lead is created in Salesforce.</span></span>

1. <span data-ttu-id="4e906-130">Selezionare **+ nuovo passaggio** azione hello tooadd desideri tootake quando viene creato un nuovo cliente potenziale.</span><span class="sxs-lookup"><span data-stu-id="4e906-130">Select **+ New Step** tooadd hello action you would like tootake when a new lead is created.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger4.png)  
2. <span data-ttu-id="4e906-131">Selezionare **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="4e906-131">Select **Add an action**.</span></span> <span data-ttu-id="4e906-132">Questa casella di ricerca hello viene visualizzata in cui è possibile cercare qualsiasi azione si desidera tootake.</span><span class="sxs-lookup"><span data-stu-id="4e906-132">This opens hello search box where you can search for any action you would like tootake.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-2.png)  
3. <span data-ttu-id="4e906-133">Immettere *smtp* toosearch per azioni correlate tooSMTP.</span><span class="sxs-lookup"><span data-stu-id="4e906-133">Enter *smtp* toosearch for actions related tooSMTP.</span></span>  
4. <span data-ttu-id="4e906-134">Selezionare **SMTP - invio di posta elettronica** come hello tootake azione quando viene creato nuovo lead hello.</span><span class="sxs-lookup"><span data-stu-id="4e906-134">Select **SMTP - Send Email** as hello action tootake when hello new lead is created.</span></span> <span data-ttu-id="4e906-135">verrà visualizzata la finestra di blocco di controllo azione Hello.</span><span class="sxs-lookup"><span data-stu-id="4e906-135">hello action control block opens.</span></span> <span data-ttu-id="4e906-136">Sarà necessario tooestablish la connessione smtp nel blocco progettazione hello se si è già stato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="4e906-136">You will have tooestablish your smtp connection in hello designer block if you have not done so previously.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/smtp-2.png)    
5. <span data-ttu-id="4e906-137">Immettere le informazioni del messaggio di posta elettronica desiderato in hello **SMTP - invio di posta elettronica** blocco.</span><span class="sxs-lookup"><span data-stu-id="4e906-137">Input your desired email information in hello **SMTP - Send Email** block.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-4.PNG)  
6. <span data-ttu-id="4e906-138">Salvare il lavoro in ordine tooactivate il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="4e906-138">Save your work in order tooactivate your workflow.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="4e906-139">Dettagli specifici del connettore</span><span class="sxs-lookup"><span data-stu-id="4e906-139">Connector-specific details</span></span>

<span data-ttu-id="4e906-140">Visualizzare tutti i trigger e azioni definite in swagger hello e anche eventuali limiti di hello [dettagli connettore](/connectors/smtpconnector/).</span><span class="sxs-lookup"><span data-stu-id="4e906-140">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/smtpconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="4e906-141">Altri connettori</span><span class="sxs-lookup"><span data-stu-id="4e906-141">More connectors</span></span>
<span data-ttu-id="4e906-142">Tornare indietro toohello [elenco API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="4e906-142">Go back toohello [APIs list](apis-list.md).</span></span>
