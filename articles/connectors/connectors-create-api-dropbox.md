---
title: Connettore Dropbox per App per la logica di Azure | Microsoft Docs
description: "Creare app per la logica in Servizio app di Azure. Connettersi a Dropbox per gestire i file. In Dropbox è possibile eseguire diverse azioni, ad esempio caricare, aggiornare, ottenere ed eliminare file."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: cb0ae033-aba7-4ac9-beaa-be561a0f0cac
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/15/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 0d09580c60fd620811b539147439d0922839fe7e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-dropbox-connector"></a><span data-ttu-id="44431-105">Introduzione al connettore Dropbox</span><span class="sxs-lookup"><span data-stu-id="44431-105">Get started with the Dropbox connector</span></span>
<span data-ttu-id="44431-106">Connettersi a Dropbox per gestire i file.</span><span class="sxs-lookup"><span data-stu-id="44431-106">Connect to Dropbox to manage your files.</span></span> <span data-ttu-id="44431-107">In Dropbox è possibile eseguire diverse azioni, ad esempio caricare, aggiornare, ottenere ed eliminare file.</span><span class="sxs-lookup"><span data-stu-id="44431-107">You can perform various actions such as upload, update, get, and delete files in Dropbox.</span></span>

<span data-ttu-id="44431-108">Per usare [qualsiasi connettore](apis-list.md), è necessario innanzitutto creare un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="44431-108">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="44431-109">Come prima operazione [creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="44431-109">You can get started by [creating a Logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-dropbox"></a><span data-ttu-id="44431-110">Connettersi a Dropbox</span><span class="sxs-lookup"><span data-stu-id="44431-110">Connect to Dropbox</span></span>
<span data-ttu-id="44431-111">Perché l'app per la logica possa accedere a qualsiasi servizio, è necessario creare una *connessione* al servizio.</span><span class="sxs-lookup"><span data-stu-id="44431-111">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="44431-112">Una connessione fornisce la connettività tra un'app per la logica e un altro servizio.</span><span class="sxs-lookup"><span data-stu-id="44431-112">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="44431-113">Ad esempio, per connettersi a Dropbox creare prima di tutto una *connessione* a Dropbox.</span><span class="sxs-lookup"><span data-stu-id="44431-113">For example, in order to connect to Dropbox, you first need a Dropbox *connection*.</span></span> <span data-ttu-id="44431-114">Per creare una connessione, è necessario fornire le credenziali che si usano normalmente per accedere al servizio a cui si vuole connettersi.</span><span class="sxs-lookup"><span data-stu-id="44431-114">To create a connection, you would need to provide the credentials you normally use to access the service you wish to connect to.</span></span> <span data-ttu-id="44431-115">Nell'esempio relativo a Dropbox saranno quindi necessarie le credenziali dell'account di Dropbox per creare la connessione a Dropbox.</span><span class="sxs-lookup"><span data-stu-id="44431-115">So, in the Dropbox example, you would need the credentials to your Dropbox account in order to create the connection to Dropbox.</span></span> [<span data-ttu-id="44431-116">Altre informazioni sulle connessioni</span><span class="sxs-lookup"><span data-stu-id="44431-116">Learn more about connections</span></span>]()

### <a name="create-a-connection-to-dropbox"></a><span data-ttu-id="44431-117">Creare una connessione a Dropbox</span><span class="sxs-lookup"><span data-stu-id="44431-117">Create a connection to Dropbox</span></span>
> [!INCLUDE [Steps to create a connection to Dropbox](../../includes/connectors-create-api-dropbox.md)]
> 
> 

## <a name="use-a-dropbox-trigger"></a><span data-ttu-id="44431-118">Usare un trigger Dropbox</span><span class="sxs-lookup"><span data-stu-id="44431-118">Use a Dropbox trigger</span></span>
<span data-ttu-id="44431-119">Un trigger è un evento che può essere usato per avviare il flusso di lavoro definito in un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="44431-119">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="44431-120">[Altre informazioni sui trigger](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="44431-120">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="44431-121">In questo esempio si userà il trigger **Quando viene creato un file**.</span><span class="sxs-lookup"><span data-stu-id="44431-121">In this example, we will use the **When a file is created** trigger.</span></span> <span data-ttu-id="44431-122">Con questo trigger viene chiamata l'azione **Ottenere contenuto di file in base al percorso** di Dropbox.</span><span class="sxs-lookup"><span data-stu-id="44431-122">When this trigger occurs, we will call the **Get file content using path** Dropbox action.</span></span> 

1. <span data-ttu-id="44431-123">Immettere *dropbox* nella casella di ricerca della finestra di progettazione di app per la logica, quindi selezionare il trigger **Dropbox - Quando viene creato un file**.</span><span class="sxs-lookup"><span data-stu-id="44431-123">Enter *dropbox* in the search box on the Logic Apps designer, then select the **Dropbox - When a file is created** trigger.</span></span>      
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger.PNG)  
2. <span data-ttu-id="44431-124">Selezionare la cartella in cui tenere traccia della creazione di file.</span><span class="sxs-lookup"><span data-stu-id="44431-124">Select the folder in which you want to track file creation.</span></span> <span data-ttu-id="44431-125">Selezionare... (identificato nella casella rossa) e passare alla cartella che si vuole selezionare per l'input del trigger.</span><span class="sxs-lookup"><span data-stu-id="44431-125">Select ... (identified in the red box) and browse to the folder you wish to select for the trigger's input.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger-2.PNG)  

## <a name="use-a-dropbox-action"></a><span data-ttu-id="44431-126">Usare un'azione Dropbox</span><span class="sxs-lookup"><span data-stu-id="44431-126">Use a Dropbox action</span></span>
<span data-ttu-id="44431-127">Un'azione è un'operazione eseguita dal flusso di lavoro e definita in un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="44431-127">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="44431-128">[Altre informazioni sulle azioni](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="44431-128">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="44431-129">Ora che il trigger è stato aggiunto, seguire questi passaggi per aggiungere un'azione che ottiene il contenuto del nuovo file.</span><span class="sxs-lookup"><span data-stu-id="44431-129">Now that the trigger has been added, follow these steps to add an action that will get the new file's content.</span></span>

1. <span data-ttu-id="44431-130">Selezionare **+ Nuovo passaggio** per aggiungere l'azione da eseguire quando viene creato un nuovo file.</span><span class="sxs-lookup"><span data-stu-id="44431-130">Select **+ New Step** to add the action you would like to take when a new file is created.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action.PNG)
2. <span data-ttu-id="44431-131">Selezionare **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="44431-131">Select **Add an action**.</span></span> <span data-ttu-id="44431-132">Viene aperta la casella di ricerca per cercare qualsiasi azione si desideri eseguire.</span><span class="sxs-lookup"><span data-stu-id="44431-132">This opens the search box where you can search for any action you would like to take.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-2.PNG)
3. <span data-ttu-id="44431-133">Immettere *dropbox* per cercare le azioni correlate a Dropbox.</span><span class="sxs-lookup"><span data-stu-id="44431-133">Enter *dropbox* to search for actions related to Dropbox.</span></span>  
4. <span data-ttu-id="44431-134">Selezionare **Dropbox - Ottenere contenuto di file in base al percorso** come azione da eseguire quando viene creato un nuovo file nella cartella di Dropbox selezionata.</span><span class="sxs-lookup"><span data-stu-id="44431-134">Select **Dropbox - Get file content using path** as the action to take when a new file is created in the selected Dropbox folder.</span></span> <span data-ttu-id="44431-135">Si apre il blocco di controllo azione.</span><span class="sxs-lookup"><span data-stu-id="44431-135">The action control block opens.</span></span> <span data-ttu-id="44431-136">Verrà richiesto di autorizzare l'app per la logica ad accedere all'account di Dropbox, se non è stato fatto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="44431-136">You will be prompted to authorize your logic app to access your Dropbox account if you have not done so previously.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-3.PNG)  
5. <span data-ttu-id="44431-137">Selezionare... sul lato destro del controllo **Percorso file** e passare al percorso file che si vuole usare.</span><span class="sxs-lookup"><span data-stu-id="44431-137">Select ... (located at the right side of the **File Path** control) and browse to the file path you would like to use.</span></span> <span data-ttu-id="44431-138">In alternativa, usare il token **file path** per rendere più rapida la creazione di app per la logica.</span><span class="sxs-lookup"><span data-stu-id="44431-138">Or, use the **file path** token to speed up your logic app creation.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-4.PNG)  
6. <span data-ttu-id="44431-139">Salvare il lavoro e creare un nuovo file in Dropbox per attivare il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="44431-139">Save your work and create a new file in Dropbox to activate your workflow.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="44431-140">Dettagli specifici del connettore</span><span class="sxs-lookup"><span data-stu-id="44431-140">Connector-specific details</span></span>

<span data-ttu-id="44431-141">Per visualizzare eventuali azioni e trigger definiti in Swagger ed eventuali limiti, vedere i [dettagli del connettore](/connectors/dropbox/).</span><span class="sxs-lookup"><span data-stu-id="44431-141">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/dropbox/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="44431-142">Altri connettori</span><span class="sxs-lookup"><span data-stu-id="44431-142">More connectors</span></span>
<span data-ttu-id="44431-143">Tornare all' [elenco di API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="44431-143">Go back to the [APIs list](apis-list.md).</span></span>