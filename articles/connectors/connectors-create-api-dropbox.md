---
title: connettore aaaDropbox nelle app di logica di Azure | Documenti Microsoft
description: "Creare app per la logica in Servizio app di Azure. Connettersi tooDropbox toomanage i file. In Dropbox è possibile eseguire diverse azioni, ad esempio caricare, aggiornare, ottenere ed eliminare file."
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
ms.openlocfilehash: 1f307477836104c0bc0008341604a1400860987f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-dropbox-connector"></a><span data-ttu-id="57eaf-105">Iniziare con il connettore di Dropbox hello</span><span class="sxs-lookup"><span data-stu-id="57eaf-105">Get started with hello Dropbox connector</span></span>
<span data-ttu-id="57eaf-106">Connettersi tooDropbox toomanage i file.</span><span class="sxs-lookup"><span data-stu-id="57eaf-106">Connect tooDropbox toomanage your files.</span></span> <span data-ttu-id="57eaf-107">In Dropbox è possibile eseguire diverse azioni, ad esempio caricare, aggiornare, ottenere ed eliminare file.</span><span class="sxs-lookup"><span data-stu-id="57eaf-107">You can perform various actions such as upload, update, get, and delete files in Dropbox.</span></span>

<span data-ttu-id="57eaf-108">toouse [i connettori](apis-list.md), è necessario innanzitutto toocreate un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="57eaf-108">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="57eaf-109">Come prima operazione [creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="57eaf-109">You can get started by [creating a Logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toodropbox"></a><span data-ttu-id="57eaf-110">Connettersi tooDropbox</span><span class="sxs-lookup"><span data-stu-id="57eaf-110">Connect tooDropbox</span></span>
<span data-ttu-id="57eaf-111">Prima che la logica app possa accedere a qualsiasi servizio, è necessario innanzitutto toocreate un *connessione* toohello servizio.</span><span class="sxs-lookup"><span data-stu-id="57eaf-111">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="57eaf-112">Una connessione fornisce la connettività tra un'app per la logica e un altro servizio.</span><span class="sxs-lookup"><span data-stu-id="57eaf-112">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="57eaf-113">Ad esempio, in ordine tooconnect tooDropbox, è necessario innanzitutto una Dropbox *connessione*.</span><span class="sxs-lookup"><span data-stu-id="57eaf-113">For example, in order tooconnect tooDropbox, you first need a Dropbox *connection*.</span></span> <span data-ttu-id="57eaf-114">toocreate una connessione, è necessario credenziali hello tooprovide utilizzato normalmente il servizio di hello tooaccess desiderato tooconnect per.</span><span class="sxs-lookup"><span data-stu-id="57eaf-114">toocreate a connection, you would need tooprovide hello credentials you normally use tooaccess hello service you wish tooconnect to.</span></span> <span data-ttu-id="57eaf-115">Nell'esempio di hello Dropbox, in tal caso, sarebbe necessario hello credenziali tooyour account Dropbox in ordine toocreate hello connessione tooDropbox.</span><span class="sxs-lookup"><span data-stu-id="57eaf-115">So, in hello Dropbox example, you would need hello credentials tooyour Dropbox account in order toocreate hello connection tooDropbox.</span></span> [<span data-ttu-id="57eaf-116">Altre informazioni sulle connessioni</span><span class="sxs-lookup"><span data-stu-id="57eaf-116">Learn more about connections</span></span>]()

### <a name="create-a-connection-toodropbox"></a><span data-ttu-id="57eaf-117">Creare una connessione tooDropbox</span><span class="sxs-lookup"><span data-stu-id="57eaf-117">Create a connection tooDropbox</span></span>
> [!INCLUDE [Steps toocreate a connection tooDropbox](../../includes/connectors-create-api-dropbox.md)]
> 
> 

## <a name="use-a-dropbox-trigger"></a><span data-ttu-id="57eaf-118">Usare un trigger Dropbox</span><span class="sxs-lookup"><span data-stu-id="57eaf-118">Use a Dropbox trigger</span></span>
<span data-ttu-id="57eaf-119">Un trigger è un evento che può essere utilizzato toostart flusso di lavoro hello definito in un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="57eaf-119">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="57eaf-120">[Altre informazioni sui trigger](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="57eaf-120">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="57eaf-121">In questo esempio utilizzeremo hello **quando viene creato un file** trigger.</span><span class="sxs-lookup"><span data-stu-id="57eaf-121">In this example, we will use hello **When a file is created** trigger.</span></span> <span data-ttu-id="57eaf-122">Quando si verifica questo trigger, chiameremo hello **ottenere il contenuto del file con percorso** azione Dropbox.</span><span class="sxs-lookup"><span data-stu-id="57eaf-122">When this trigger occurs, we will call hello **Get file content using path** Dropbox action.</span></span> 

1. <span data-ttu-id="57eaf-123">Immettere *dropbox* nella casella di ricerca hello sulla progettazione di App per la logica di hello, quindi selezionare hello **Dropbox - quando viene creato un file** trigger.</span><span class="sxs-lookup"><span data-stu-id="57eaf-123">Enter *dropbox* in hello search box on hello Logic Apps designer, then select hello **Dropbox - When a file is created** trigger.</span></span>      
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger.PNG)  
2. <span data-ttu-id="57eaf-124">Selezionare la cartella hello in cui si desidera tootrack la creazione di file.</span><span class="sxs-lookup"><span data-stu-id="57eaf-124">Select hello folder in which you want tootrack file creation.</span></span> <span data-ttu-id="57eaf-125">Seleziona... (identificato nella casella hello rosso) e Sfoglia toohello cartella in cui l'input del tooselect per trigger hello.</span><span class="sxs-lookup"><span data-stu-id="57eaf-125">Select ... (identified in hello red box) and browse toohello folder you wish tooselect for hello trigger's input.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger-2.PNG)  

## <a name="use-a-dropbox-action"></a><span data-ttu-id="57eaf-126">Usare un'azione Dropbox</span><span class="sxs-lookup"><span data-stu-id="57eaf-126">Use a Dropbox action</span></span>
<span data-ttu-id="57eaf-127">Un'azione è un'operazione effettuata dal flusso di lavoro hello definito in un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="57eaf-127">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="57eaf-128">[Altre informazioni sulle azioni](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="57eaf-128">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="57eaf-129">Ora che hello trigger è stato aggiunto, seguire questi tooadd passaggi un'azione che verrà visualizzato il contenuto di hello del nuovo file.</span><span class="sxs-lookup"><span data-stu-id="57eaf-129">Now that hello trigger has been added, follow these steps tooadd an action that will get hello new file's content.</span></span>

1. <span data-ttu-id="57eaf-130">Selezionare **+ nuovo passaggio** azione hello tooadd desideri tootake quando viene creato un nuovo file.</span><span class="sxs-lookup"><span data-stu-id="57eaf-130">Select **+ New Step** tooadd hello action you would like tootake when a new file is created.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action.PNG)
2. <span data-ttu-id="57eaf-131">Selezionare **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="57eaf-131">Select **Add an action**.</span></span> <span data-ttu-id="57eaf-132">Questa casella di ricerca hello viene visualizzata in cui è possibile cercare qualsiasi azione si desidera tootake.</span><span class="sxs-lookup"><span data-stu-id="57eaf-132">This opens hello search box where you can search for any action you would like tootake.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-2.PNG)
3. <span data-ttu-id="57eaf-133">Immettere *dropbox* toosearch per azioni correlate tooDropbox.</span><span class="sxs-lookup"><span data-stu-id="57eaf-133">Enter *dropbox* toosearch for actions related tooDropbox.</span></span>  
4. <span data-ttu-id="57eaf-134">Selezionare **Dropbox - Get contenuto del file con percorso** come hello tootake azione quando viene creato un nuovo file in hello Dropbox cartella selezionata.</span><span class="sxs-lookup"><span data-stu-id="57eaf-134">Select **Dropbox - Get file content using path** as hello action tootake when a new file is created in hello selected Dropbox folder.</span></span> <span data-ttu-id="57eaf-135">verrà visualizzata la finestra di blocco di controllo azione Hello.</span><span class="sxs-lookup"><span data-stu-id="57eaf-135">hello action control block opens.</span></span> <span data-ttu-id="57eaf-136">Si sarà richiesta tooauthorize tooaccess di app la logica di Dropbox account se si è già stato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="57eaf-136">You will be prompted tooauthorize your logic app tooaccess your Dropbox account if you have not done so previously.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-3.PNG)  
5. <span data-ttu-id="57eaf-137">Seleziona... (posizione destra hello di hello **percorso del File** controllo) e individuare il percorso di file toohello toouse desiderato.</span><span class="sxs-lookup"><span data-stu-id="57eaf-137">Select ... (located at hello right side of hello **File Path** control) and browse toohello file path you would like toouse.</span></span> <span data-ttu-id="57eaf-138">In alternativa, usare hello **percorso del file** toospeed token backup la creazione di app logica.</span><span class="sxs-lookup"><span data-stu-id="57eaf-138">Or, use hello **file path** token toospeed up your logic app creation.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-4.PNG)  
6. <span data-ttu-id="57eaf-139">Salvare il lavoro e creare un nuovo file in Dropbox tooactivate il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="57eaf-139">Save your work and create a new file in Dropbox tooactivate your workflow.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="57eaf-140">Dettagli specifici del connettore</span><span class="sxs-lookup"><span data-stu-id="57eaf-140">Connector-specific details</span></span>

<span data-ttu-id="57eaf-141">Visualizzare tutti i trigger e azioni definite in swagger hello e anche eventuali limiti di hello [dettagli connettore](/connectors/dropbox/).</span><span class="sxs-lookup"><span data-stu-id="57eaf-141">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/dropbox/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="57eaf-142">Altri connettori</span><span class="sxs-lookup"><span data-stu-id="57eaf-142">More connectors</span></span>
<span data-ttu-id="57eaf-143">Tornare indietro toohello [elenco API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="57eaf-143">Go back toohello [APIs list](apis-list.md).</span></span>
