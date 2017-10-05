---
title: Connettore SMTP per App per la logica di Azure | Microsoft Docs
description: Creare app per la logica con Servizio app di Azure. Connettersi a SMTP per inviare messaggi di posta elettronica.
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
ms.openlocfilehash: 1cf96bbf8bd215d7ddb3c99860a5cb4e668be3c2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-smtp-connector"></a><span data-ttu-id="4c700-104">Introduzione al connettore SMTP</span><span class="sxs-lookup"><span data-stu-id="4c700-104">Get started with the SMTP connector</span></span>
<span data-ttu-id="4c700-105">Connettersi a SMTP per inviare messaggi di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="4c700-105">Connect to SMTP to send email.</span></span>

<span data-ttu-id="4c700-106">Per usare [qualsiasi connettore](apis-list.md), è necessario innanzitutto creare un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="4c700-106">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="4c700-107">Come prima operazione [creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="4c700-107">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-smtp"></a><span data-ttu-id="4c700-108">Connettersi a un server SMTP</span><span class="sxs-lookup"><span data-stu-id="4c700-108">Connect to SMTP</span></span>
<span data-ttu-id="4c700-109">Perché l'app per la logica possa accedere a qualsiasi servizio, è necessario creare una *connessione* al servizio.</span><span class="sxs-lookup"><span data-stu-id="4c700-109">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="4c700-110">Una [connessione](connectors-overview.md) fornisce la connettività tra un'app per la logica e un altro servizio.</span><span class="sxs-lookup"><span data-stu-id="4c700-110">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="4c700-111">Ad esempio, per connettersi a un server SMTP, è necessaria prima di tutto una *connessione* SMTP.</span><span class="sxs-lookup"><span data-stu-id="4c700-111">For example, to connect to SMTP, you first need an SMTP *connection*.</span></span> <span data-ttu-id="4c700-112">Per creare una connessione, immettere le credenziali che si usano normalmente per accedere al servizio a cui si vuole connettersi.</span><span class="sxs-lookup"><span data-stu-id="4c700-112">To create a connection, enter the credentials you normally use to access the service you connect to.</span></span> <span data-ttu-id="4c700-113">Nell'esempio SMTP è quindi necessario immettere le credenziali per nome della connessione, indirizzo del server SMTP e informazioni sull'accesso utente per creare la connessione a SMTP.</span><span class="sxs-lookup"><span data-stu-id="4c700-113">So, in the SMTP example, enter the credentials to your connection name, SMTP server address, and user login information to create the connection to SMTP.</span></span>  

### <a name="create-a-connection-to-smtp"></a><span data-ttu-id="4c700-114">Creare una connessione a SMTP</span><span class="sxs-lookup"><span data-stu-id="4c700-114">Create a connection to SMTP</span></span>
> [!INCLUDE [Steps to create a connection to SMTP](../../includes/connectors-create-api-smtp.md)]
> 
> 

## <a name="use-an-smtp-trigger"></a><span data-ttu-id="4c700-115">Usare un trigger SMTP</span><span class="sxs-lookup"><span data-stu-id="4c700-115">Use an SMTP trigger</span></span>
<span data-ttu-id="4c700-116">Un trigger è un evento che può essere usato per avviare il flusso di lavoro definito in un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="4c700-116">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="4c700-117">[Altre informazioni sui trigger](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="4c700-117">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="4c700-118">In questo esempio, poiché SMTP non ha un trigger proprio, si userà il trigger **Salesforce - Quando viene creato un oggetto**.</span><span class="sxs-lookup"><span data-stu-id="4c700-118">In this example, because SMTP does not have a trigger of its own, we'll use the **Salesforce - When an object is created** trigger.</span></span> <span data-ttu-id="4c700-119">Questo trigger viene attivato quando viene creato un nuovo oggetto in Salesforce.</span><span class="sxs-lookup"><span data-stu-id="4c700-119">This trigger activates when a new object is created in Salesforce.</span></span> <span data-ttu-id="4c700-120">Per questo esempio verrà impostato in modo che, ogni volta che viene creato un nuovo cliente potenziale in Salesforce, venga eseguita un'azione di *invio messaggio di posta elettronica* usando il connettore SMTP con una notifica della creazione del nuovo cliente potenziale.</span><span class="sxs-lookup"><span data-stu-id="4c700-120">For our example, we'll set it up such that every time a new lead is created in Salesforce, a *send email* action occurs via the SMTP connector with a notification of the new lead being created.</span></span>

1. <span data-ttu-id="4c700-121">Immettere *salesforce* nella casella di ricerca della finestra di progettazione App per la logica, quindi selezionare il trigger **Salesforce - Quando viene creato un oggetto** .</span><span class="sxs-lookup"><span data-stu-id="4c700-121">Enter *salesforce* in the search box on the logic apps designer then select the **Salesforce - When an object is created** trigger.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-1.png)  
2. <span data-ttu-id="4c700-122">Viene visualizzato il controllo **Quando viene creato un oggetto** .</span><span class="sxs-lookup"><span data-stu-id="4c700-122">The **When an object is created** control is displayed.</span></span>
   ![](../../includes/media/connectors-create-api-salesforce/trigger-2.png)  
3. <span data-ttu-id="4c700-123">Selezionare **Tipo di oggetto** e *Lead* dall'elenco di oggetti.</span><span class="sxs-lookup"><span data-stu-id="4c700-123">Select the **Object Type** then select *Lead* from the list of objects.</span></span> <span data-ttu-id="4c700-124">In questo passaggio si indica che si sta creando un trigger che invierà una notifica all'app per la logica ogni volta che viene creato un nuovo lead in Salesforce.</span><span class="sxs-lookup"><span data-stu-id="4c700-124">In this step you are indicating that you are creating a trigger that will notify your logic app whenever a new lead is created in Salesforce.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger3.png)  
4. <span data-ttu-id="4c700-125">Il trigger è stato creato.</span><span class="sxs-lookup"><span data-stu-id="4c700-125">The trigger has been created.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-4.png)  

## <a name="use-an-smtp-action"></a><span data-ttu-id="4c700-126">Usare un'azione SMTP</span><span class="sxs-lookup"><span data-stu-id="4c700-126">Use an SMTP action</span></span>
<span data-ttu-id="4c700-127">Un'azione è un'operazione eseguita dal flusso di lavoro e definita in un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="4c700-127">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="4c700-128">[Altre informazioni sulle azioni](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="4c700-128">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="4c700-129">Ora che il trigger è stato aggiunto, seguire questi passaggi per aggiungere un'azione SMTP che viene eseguita quando viene creato un nuovo cliente potenziale in Salesforce.</span><span class="sxs-lookup"><span data-stu-id="4c700-129">Now that the trigger has been added, follow these steps to add an SMTP action that will occur when a new lead is created in Salesforce.</span></span>

1. <span data-ttu-id="4c700-130">Selezionare **+ Nuovo passaggio** per aggiungere l'azione da eseguire quando viene creato un nuovo cliente potenziale.</span><span class="sxs-lookup"><span data-stu-id="4c700-130">Select **+ New Step** to add the action you would like to take when a new lead is created.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger4.png)  
2. <span data-ttu-id="4c700-131">Selezionare **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="4c700-131">Select **Add an action**.</span></span> <span data-ttu-id="4c700-132">Viene aperta la casella di ricerca per cercare qualsiasi azione si desideri eseguire.</span><span class="sxs-lookup"><span data-stu-id="4c700-132">This opens the search box where you can search for any action you would like to take.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-2.png)  
3. <span data-ttu-id="4c700-133">Immettere *smtp* per cercare le azioni correlate a SMTP.</span><span class="sxs-lookup"><span data-stu-id="4c700-133">Enter *smtp* to search for actions related to SMTP.</span></span>  
4. <span data-ttu-id="4c700-134">Selezionare **SMTP - Invia messaggio di posta elettronica** come azione da eseguire quando viene creato il cliente potenziale.</span><span class="sxs-lookup"><span data-stu-id="4c700-134">Select **SMTP - Send Email** as the action to take when the new lead is created.</span></span> <span data-ttu-id="4c700-135">Si apre il blocco di controllo azione.</span><span class="sxs-lookup"><span data-stu-id="4c700-135">The action control block opens.</span></span> <span data-ttu-id="4c700-136">È necessario stabilire la connessione SMTP nel blocco di progettazione se non lo si è ancora fatto.</span><span class="sxs-lookup"><span data-stu-id="4c700-136">You will have to establish your smtp connection in the designer block if you have not done so previously.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/smtp-2.png)    
5. <span data-ttu-id="4c700-137">Immettere le informazioni di posta elettronica nel blocco **SMTP - Invia messaggio di posta elettronica**.</span><span class="sxs-lookup"><span data-stu-id="4c700-137">Input your desired email information in the **SMTP - Send Email** block.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-4.PNG)  
6. <span data-ttu-id="4c700-138">Salvare il lavoro per attivare il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="4c700-138">Save your work in order to activate your workflow.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="4c700-139">Dettagli specifici del connettore</span><span class="sxs-lookup"><span data-stu-id="4c700-139">Connector-specific details</span></span>

<span data-ttu-id="4c700-140">Per visualizzare eventuali azioni e trigger definiti in Swagger ed eventuali limiti, vedere i [dettagli del connettore](/connectors/smtpconnector/).</span><span class="sxs-lookup"><span data-stu-id="4c700-140">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/smtpconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="4c700-141">Altri connettori</span><span class="sxs-lookup"><span data-stu-id="4c700-141">More connectors</span></span>
<span data-ttu-id="4c700-142">Tornare all' [elenco di API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="4c700-142">Go back to the [APIs list](apis-list.md).</span></span>