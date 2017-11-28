---
title: aaaLearn come toouse hello in App per la logica del connettore Twitter | Documenti Microsoft
description: Panoramica del connettore Twitter con i parametri dell'API REST
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 8bce2183-544d-4668-a2dc-9a62c152d9fa
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: ead4e4dc95bf894fd72b908c5375b407ba27642d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-twitter-connector"></a><span data-ttu-id="85960-103">Iniziare con il connettore di Twitter hello</span><span class="sxs-lookup"><span data-stu-id="85960-103">Get started with hello Twitter connector</span></span>
<span data-ttu-id="85960-104">Con il connettore di Twitter hello è possibile:</span><span class="sxs-lookup"><span data-stu-id="85960-104">With hello Twitter connector you can:</span></span>

* <span data-ttu-id="85960-105">Pubblicare e recuperare tweet</span><span class="sxs-lookup"><span data-stu-id="85960-105">Post tweets and get tweets</span></span>
* <span data-ttu-id="85960-106">Accedere a timeline, amici e follower</span><span class="sxs-lookup"><span data-stu-id="85960-106">Access timelines, friends and followers</span></span>
* <span data-ttu-id="85960-107">Eseguire una delle hello altre azioni e trigger descritto di seguito</span><span class="sxs-lookup"><span data-stu-id="85960-107">Perform any of hello other actions and triggers described below</span></span>  

<span data-ttu-id="85960-108">toouse [i connettori](apis-list.md), è necessario innanzitutto toocreate un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="85960-108">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="85960-109">Come prima operazione [creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="85960-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>  

## <a name="connect-tootwitter"></a><span data-ttu-id="85960-110">Connettersi tooTwitter</span><span class="sxs-lookup"><span data-stu-id="85960-110">Connect tooTwitter</span></span>
<span data-ttu-id="85960-111">Prima che la logica app possa accedere a qualsiasi servizio, è necessario innanzitutto toocreate un *connessione* toohello servizio.</span><span class="sxs-lookup"><span data-stu-id="85960-111">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="85960-112">Una [connessione](connectors-overview.md) fornisce la connettività tra un'app per la logica e un altro servizio.</span><span class="sxs-lookup"><span data-stu-id="85960-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-tootwitter"></a><span data-ttu-id="85960-113">Creare una connessione tooTwitter</span><span class="sxs-lookup"><span data-stu-id="85960-113">Create a connection tooTwitter</span></span>
> [!INCLUDE [Steps toocreate a connection tooTwitter](../../includes/connectors-create-api-twitter.md)]
> 
> 

## <a name="use-a-twitter-trigger"></a><span data-ttu-id="85960-114">Usare un trigger di Twitter</span><span class="sxs-lookup"><span data-stu-id="85960-114">Use a Twitter trigger</span></span>
<span data-ttu-id="85960-115">Un trigger è un evento che può essere utilizzato toostart flusso di lavoro hello definito in un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="85960-115">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="85960-116">[Altre informazioni sui trigger](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="85960-116">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="85960-117">In questo esempio, verrà spiegato come hello toouse **durante il postback un tweet nuovo** attivare toosearch per #Seattle e, se viene trovato #Seattle, è possibile aggiornare un file nell'area di sincronizzazione con il testo hello tweet hello.</span><span class="sxs-lookup"><span data-stu-id="85960-117">In this example, I will show you how toouse hello **When a new tweet is posted**  trigger toosearch for #Seattle and, if #Seattle is found, update a file in Dropbox with hello text from hello tweet.</span></span> <span data-ttu-id="85960-118">In un esempio di enterprise, è possibile cercare il nome della società hello e aggiornare un database SQL con il testo hello tweet hello.</span><span class="sxs-lookup"><span data-stu-id="85960-118">In an enterprise example, you could search for hello name of your company and update a SQL database with hello text from hello tweet.</span></span>

1. <span data-ttu-id="85960-119">Immettere *twitter* nella casella di ricerca hello nella finestra di progettazione di hello logica App, quindi selezionare hello **Twitter - quando viene inserito un nuovo tweet** trigger</span><span class="sxs-lookup"><span data-stu-id="85960-119">Enter *twitter* in hello search box on hello logic apps designer then select hello **Twitter - When a new tweet is posted**  trigger</span></span>   
   <span data-ttu-id="85960-120">![Immagine di trigger Twitter 1](./media/connectors-create-api-twitter/trigger-1.png)</span><span class="sxs-lookup"><span data-stu-id="85960-120">![Twitter trigger image 1](./media/connectors-create-api-twitter/trigger-1.png)</span></span>  
2. <span data-ttu-id="85960-121">Immettere *#Seattle* in hello **testo di ricerca** controllo</span><span class="sxs-lookup"><span data-stu-id="85960-121">Enter *#Seattle* in hello **Search Text** control</span></span>  
   <span data-ttu-id="85960-122">![Immagine di trigger Twitter 2](./media/connectors-create-api-twitter/trigger-2.png)</span><span class="sxs-lookup"><span data-stu-id="85960-122">![Twitter trigger image 2](./media/connectors-create-api-twitter/trigger-2.png)</span></span> 

<span data-ttu-id="85960-123">A questo punto, l'app di logica è stato configurato con un trigger che verrà avviata un'esecuzione di hello altre azioni nel flusso di lavoro hello e il trigger.</span><span class="sxs-lookup"><span data-stu-id="85960-123">At this point, your logic app has been configured with a trigger that will begin a run of hello other triggers and actions in hello workflow.</span></span> 

> [!NOTE]
> <span data-ttu-id="85960-124">Per un toobe di app logica funzionale, deve contenere almeno un trigger e un'azione.</span><span class="sxs-lookup"><span data-stu-id="85960-124">For a logic app toobe functional, it must contain at least one trigger and one action.</span></span> <span data-ttu-id="85960-125">Seguire passaggi hello hello successiva sezione tooadd un'azione.</span><span class="sxs-lookup"><span data-stu-id="85960-125">Follow hello steps in hello next section tooadd an action.</span></span>  
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="85960-126">Add a condition</span><span class="sxs-lookup"><span data-stu-id="85960-126">Add a condition</span></span>
<span data-ttu-id="85960-127">Poiché si intende solo TWEET da utenti con più di 50 utenti, una condizione che il numero di hello di anelli di conferma deve essere aggiunto toohello logica app.</span><span class="sxs-lookup"><span data-stu-id="85960-127">Since we are only interested in tweets from users with more than 50 users, a condition that confirms hello number of followers must first be added toohello logic app.</span></span>  

1. <span data-ttu-id="85960-128">Selezionare **+ nuovo passaggio** azione hello tooadd desideri tootake quando #Seattle si trova in un tweet nuovo</span><span class="sxs-lookup"><span data-stu-id="85960-128">Select **+ New step** tooadd hello action you would like tootake when #Seattle is found in a new tweet</span></span>  
   <span data-ttu-id="85960-129">![Immagine di azione Twitter 1](../../includes/media/connectors-create-api-twitter/action-1.png)</span><span class="sxs-lookup"><span data-stu-id="85960-129">![Twitter action image 1](../../includes/media/connectors-create-api-twitter/action-1.png)</span></span>  
2. <span data-ttu-id="85960-130">Seleziona hello **aggiungere una condizione** collegamento.</span><span class="sxs-lookup"><span data-stu-id="85960-130">Select hello **Add a condition** link.</span></span>  
   <span data-ttu-id="85960-131">![Immagine di condizione Twitter 1](../../includes/media/connectors-create-api-twitter/condition-1.png) </span><span class="sxs-lookup"><span data-stu-id="85960-131">![Twitter condition image 1](../../includes/media/connectors-create-api-twitter/condition-1.png) </span></span>  
   <span data-ttu-id="85960-132">Verrà visualizzata hello **condizione** controllo in cui è possibile controllare le condizioni, ad esempio *è uguale a*, *è minore di*, *è maggiore di*, *contiene*e così via.</span><span class="sxs-lookup"><span data-stu-id="85960-132">This opens hello **Condition** control where you can check conditions such as *is equal to*, *is less than*, *is greater than*, *contains*, etc.</span></span>  
   <span data-ttu-id="85960-133">![Immagine di condizione Twitter 2](../../includes/media/connectors-create-api-twitter/condition-2.png)</span><span class="sxs-lookup"><span data-stu-id="85960-133">![Twitter condition image 2](../../includes/media/connectors-create-api-twitter/condition-2.png)</span></span>   
3. <span data-ttu-id="85960-134">Seleziona hello **scegliere un valore** controllo.</span><span class="sxs-lookup"><span data-stu-id="85960-134">Select hello **Choose a value** control.</span></span>  
   <span data-ttu-id="85960-135">In questo controllo, è possibile selezionare uno o più proprietà hello dalle azioni precedenti o i trigger come valore di hello la cui condizione verrà valutata tootrue o false.</span><span class="sxs-lookup"><span data-stu-id="85960-135">In this control, you can select one or more of hello properties from any previous actions or triggers as hello value whose condition will be evaluated tootrue or false.</span></span>
   <span data-ttu-id="85960-136">![Immagine di condizione Twitter 3](../../includes/media/connectors-create-api-twitter/condition-3.png)</span><span class="sxs-lookup"><span data-stu-id="85960-136">![Twitter condition image 3](../../includes/media/connectors-create-api-twitter/condition-3.png)</span></span>   
4. <span data-ttu-id="85960-137">Seleziona hello **...**  tooexpand hello elenco di proprietà in modo da visualizzare tutte le proprietà di hello disponibili.</span><span class="sxs-lookup"><span data-stu-id="85960-137">Select hello **...** tooexpand hello list of properties so you can see all hello properties that are available.</span></span>        
   <span data-ttu-id="85960-138">![Immagine di condizione Twitter 4](../../includes/media/connectors-create-api-twitter/condition-4.png)</span><span class="sxs-lookup"><span data-stu-id="85960-138">![Twitter condition image 4](../../includes/media/connectors-create-api-twitter/condition-4.png)</span></span>   
5. <span data-ttu-id="85960-139">Seleziona hello **il numero di anelli** proprietà.</span><span class="sxs-lookup"><span data-stu-id="85960-139">Select hello **Followers count** property.</span></span>    
   <span data-ttu-id="85960-140">![Immagine di condizione Twitter 5](../../includes/media/connectors-create-api-twitter/condition-5.png)</span><span class="sxs-lookup"><span data-stu-id="85960-140">![Twitter condition image 5](../../includes/media/connectors-create-api-twitter/condition-5.png)</span></span>   
6. <span data-ttu-id="85960-141">Si noti bisogno di hello seguenti proprietà di conteggio è ora nel controllo value hello.</span><span class="sxs-lookup"><span data-stu-id="85960-141">Notice hello Followers count property is now in hello value control.</span></span>    
   ![Immagine di condizione Twitter 6](../../includes/media/connectors-create-api-twitter/condition-6.png)   
7. <span data-ttu-id="85960-143">Selezionare **è maggiore di** dall'elenco di operatori hello.</span><span class="sxs-lookup"><span data-stu-id="85960-143">Select **is greater than** from hello operators list.</span></span>    
   <span data-ttu-id="85960-144">![Immagine di condizione Twitter 7](../../includes/media/connectors-create-api-twitter/condition-7.png)</span><span class="sxs-lookup"><span data-stu-id="85960-144">![Twitter condition image 7](../../includes/media/connectors-create-api-twitter/condition-7.png)</span></span>   
8. <span data-ttu-id="85960-145">Immettere 50 come operando per hello hello *è maggiore di* operatore.</span><span class="sxs-lookup"><span data-stu-id="85960-145">Enter 50 as hello operand for hello *is greater than* operator.</span></span>  
   <span data-ttu-id="85960-146">condizione Hello viene aggiunto.</span><span class="sxs-lookup"><span data-stu-id="85960-146">hello condition is now added.</span></span> <span data-ttu-id="85960-147">Salvare il lavoro usando hello **salvare** collegamento nel menu hello precedente.</span><span class="sxs-lookup"><span data-stu-id="85960-147">Save your work using hello **Save** link on hello menu above.</span></span>    
   <span data-ttu-id="85960-148">![Immagine di condizione Twitter 8](../../includes/media/connectors-create-api-twitter/condition-8.png)</span><span class="sxs-lookup"><span data-stu-id="85960-148">![Twitter condition image 8](../../includes/media/connectors-create-api-twitter/condition-8.png)</span></span>   

## <a name="use-a-twitter-action"></a><span data-ttu-id="85960-149">Usare un'azione di Twitter</span><span class="sxs-lookup"><span data-stu-id="85960-149">Use a Twitter action</span></span>
<span data-ttu-id="85960-150">Un'azione è un'operazione effettuata dal flusso di lavoro hello definito in un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="85960-150">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="85960-151">[Altre informazioni sulle azioni](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="85960-151">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="85960-152">Dopo avere aggiunto un trigger, seguire questi tooadd passaggi un'azione che verrà registrato un nuovo tweet con contenuto hello di hello TWEET trovato dal trigger hello.</span><span class="sxs-lookup"><span data-stu-id="85960-152">Now that you have added a trigger, follow these steps tooadd an action that will post a new tweet with hello contents of hello tweets found by hello trigger.</span></span> <span data-ttu-id="85960-153">Ai fini di hello di questa procedura dettagliata verrà registrato solo TWEET da utenti con più di 50 anelli.</span><span class="sxs-lookup"><span data-stu-id="85960-153">For hello purposes of this walk-through only tweets from users with more than 50 followers will be posted.</span></span>  

<span data-ttu-id="85960-154">Nel passaggio successivo hello, si aggiungerà un'azione di Twitter che eseguirà un tweet utilizzando alcune delle proprietà hello di ogni tweet che è stata registrata da un utente che ha bisogno di più di 50 seguenti.</span><span class="sxs-lookup"><span data-stu-id="85960-154">In hello next step, you will add a Twitter action that will post a tweet using some of hello properties of each tweet that has been posted by a user who has more than 50 followers.</span></span>  

1. <span data-ttu-id="85960-155">Selezionare **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="85960-155">Select **Add an action**.</span></span> <span data-ttu-id="85960-156">Verrà aperto il controllo di ricerca hello in cui è possibile cercare altre azioni e trigger.</span><span class="sxs-lookup"><span data-stu-id="85960-156">This opens hello search control where you can search for other actions and triggers.</span></span>  
   <span data-ttu-id="85960-157">![Immagine di condizione Twitter 9](../../includes/media/connectors-create-api-twitter/condition-9.png)</span><span class="sxs-lookup"><span data-stu-id="85960-157">![Twitter condition image 9](../../includes/media/connectors-create-api-twitter/condition-9.png)</span></span>   
2. <span data-ttu-id="85960-158">Immettere *twitter* nella casella di ricerca hello, quindi selezionare hello **Twitter: registrare un tweet** azione.</span><span class="sxs-lookup"><span data-stu-id="85960-158">Enter *twitter* into hello search box then select hello **Twitter - Post a tweet** action.</span></span> <span data-ttu-id="85960-159">Verrà visualizzata hello **registra un tweet** controllare dove verrà immesso tutti i dettagli per tweet hello inviata.</span><span class="sxs-lookup"><span data-stu-id="85960-159">This opens hello **Post a tweet** control where you will enter all details for hello tweet being posted.</span></span>      
   <span data-ttu-id="85960-160">![Immagine di azione Twitter 1-5](../../includes/media/connectors-create-api-twitter/action-1-5.png)</span><span class="sxs-lookup"><span data-stu-id="85960-160">![Twitter action image 1-5](../../includes/media/connectors-create-api-twitter/action-1-5.png)</span></span>   
3. <span data-ttu-id="85960-161">Seleziona hello **Tweet testo** controllo.</span><span class="sxs-lookup"><span data-stu-id="85960-161">Select hello **Tweet text** control.</span></span> <span data-ttu-id="85960-162">Tutti gli output di azioni precedenti e i trigger in hello logica app sono ora visibili.</span><span class="sxs-lookup"><span data-stu-id="85960-162">All outputs from previous actions and triggers in hello logic app are now visible.</span></span> <span data-ttu-id="85960-163">È possibile selezionare una delle seguenti e utilizzarle come parte del testo tweet hello di tweet nuovo hello.</span><span class="sxs-lookup"><span data-stu-id="85960-163">You can select any of these and use them as part of hello tweet text of hello new tweet.</span></span>     
   <span data-ttu-id="85960-164">![Immagine di azione Twitter 2](../../includes/media/connectors-create-api-twitter/action-2.png)</span><span class="sxs-lookup"><span data-stu-id="85960-164">![Twitter action image 2](../../includes/media/connectors-create-api-twitter/action-2.png)</span></span>   
4. <span data-ttu-id="85960-165">Selezionare **Nome utente**</span><span class="sxs-lookup"><span data-stu-id="85960-165">Select **User name**</span></span>   
5. <span data-ttu-id="85960-166">Immettere *afferma:* nel controllo di testo tweet hello.</span><span class="sxs-lookup"><span data-stu-id="85960-166">Enter *says:* in hello tweet text control.</span></span> <span data-ttu-id="85960-167">Eseguire questa operazione subito dopo il nome utente.</span><span class="sxs-lookup"><span data-stu-id="85960-167">Do this just after User name.</span></span>  
6. <span data-ttu-id="85960-168">Selezionare *Testo del tweet*.</span><span class="sxs-lookup"><span data-stu-id="85960-168">Select *Tweet text*.</span></span>       
   <span data-ttu-id="85960-169">![Immagine di azione Twitter 3](../../includes/media/connectors-create-api-twitter/action-3.png)</span><span class="sxs-lookup"><span data-stu-id="85960-169">![Twitter action image 3](../../includes/media/connectors-create-api-twitter/action-3.png)</span></span>   
7. <span data-ttu-id="85960-170">Salvare il lavoro e invii un tweet con hello #Seattle hashtag tooactivate il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="85960-170">Save your work and send a tweet with hello #Seattle hashtag tooactivate your workflow.</span></span>  


## <a name="connector-specific-details"></a><span data-ttu-id="85960-171">Dettagli specifici del connettore</span><span class="sxs-lookup"><span data-stu-id="85960-171">Connector-specific details</span></span>

<span data-ttu-id="85960-172">Visualizzare tutti i trigger e azioni definite in swagger hello e anche eventuali limiti di hello [dettagli connettore](/connectors/twitterconnector/).</span><span class="sxs-lookup"><span data-stu-id="85960-172">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/twitterconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="85960-173">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="85960-173">Next steps</span></span>
[<span data-ttu-id="85960-174">Creare un'app per la logica</span><span class="sxs-lookup"><span data-stu-id="85960-174">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

