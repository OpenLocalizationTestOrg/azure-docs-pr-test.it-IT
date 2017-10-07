---
title: una funzione che si integra con Azure logica App aaaCreate | Documenti Microsoft
description: "Creare una funzione che si integra con Azure logica App e servizi di Azure cognitivi sentiment tweet toocategorize e inviare notifiche quando sentiment è scarsa."
services: functions, logic-apps, cognitive-services
keywords: flusso di lavoro, app cloud, servizi cloud, processi aziendali, integrazione di sistemi, enterprise application integration, EAI
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
ms.assetid: 60495cc5-1638-4bf0-8174-52786d227734
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: e176bd946af9a3684b3ad0e4b1bed1c3ee344019
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-that-integrates-with-azure-logic-apps"></a><span data-ttu-id="84143-104">Creare una funzione che si integra con le app per la logica di Azure</span><span class="sxs-lookup"><span data-stu-id="84143-104">Create a function that integrates with Azure Logic Apps</span></span>

<span data-ttu-id="84143-105">Funzioni di Azure si integra con Azure logica App in hello logica di progettazione di App.</span><span class="sxs-lookup"><span data-stu-id="84143-105">Azure Functions integrates with Azure Logic Apps in hello Logic Apps Designer.</span></span> <span data-ttu-id="84143-106">Questa integrazione consente di usare hello elaborazione delle funzioni in orchestrazioni con altri servizi di terze parti e di Azure.</span><span class="sxs-lookup"><span data-stu-id="84143-106">This integration lets you use hello computing power of Functions in orchestrations with other Azure and third-party services.</span></span> 

<span data-ttu-id="84143-107">Questa esercitazione viene illustrato il funzionamento toouse con logica App e servizi di Azure cognitivi sentiment tooanalyze da Twitter post.</span><span class="sxs-lookup"><span data-stu-id="84143-107">This tutorial shows you how toouse Functions with Logic Apps and Azure Cognitive Services tooanalyze sentiment from Twitter posts.</span></span> <span data-ttu-id="84143-108">Una funzione di attivazione HTTP classifica TWEET come verde, giallo o rosso basato sul punteggio sentiment hello.</span><span class="sxs-lookup"><span data-stu-id="84143-108">An HTTP triggered function categorizes tweets as green, yellow, or red based on hello sentiment score.</span></span> <span data-ttu-id="84143-109">Quando viene rilevato un livello di sentiment basso viene inviato un messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="84143-109">An email is sent when poor sentiment is detected.</span></span> 

![immagine dei primi due passaggi dell'app in Progettazione app per la logica](media/functions-twitter-email/designer1.png)

<span data-ttu-id="84143-111">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="84143-111">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="84143-112">Creare un account di Servizi cognitivi.</span><span class="sxs-lookup"><span data-stu-id="84143-112">Create a Cognitive Services account.</span></span>
> * <span data-ttu-id="84143-113">Creare una funzione che classifica i sentiment nei tweet.</span><span class="sxs-lookup"><span data-stu-id="84143-113">Create a function that categorizes tweet sentiment.</span></span>
> * <span data-ttu-id="84143-114">Creare un'app di logica che si connette tooTwitter.</span><span class="sxs-lookup"><span data-stu-id="84143-114">Create a logic app that connects tooTwitter.</span></span>
> * <span data-ttu-id="84143-115">Aggiungere app per la logica toohello sentiment rilevamento.</span><span class="sxs-lookup"><span data-stu-id="84143-115">Add sentiment detection toohello logic app.</span></span> 
> * <span data-ttu-id="84143-116">Hello logica app toohello funzione di connessione.</span><span class="sxs-lookup"><span data-stu-id="84143-116">Connect hello logic app toohello function.</span></span>
> * <span data-ttu-id="84143-117">Inviare un messaggio di posta elettronica in base alla risposta hello dalla funzione hello.</span><span class="sxs-lookup"><span data-stu-id="84143-117">Send an email based on hello response from hello function.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="84143-118">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="84143-118">Prerequisites</span></span>

+ <span data-ttu-id="84143-119">Un account [Twitter](https://twitter.com/) attivo.</span><span class="sxs-lookup"><span data-stu-id="84143-119">An active [Twitter](https://twitter.com/) account.</span></span> 
+ <span data-ttu-id="84143-120">Un account [Outlook.com](https://outlook.com/) per l'invio delle notifiche.</span><span class="sxs-lookup"><span data-stu-id="84143-120">An [Outlook.com](https://outlook.com/) account (for sending notifications).</span></span>
+ <span data-ttu-id="84143-121">Questo argomento viene utilizzato come le risorse di hello punto iniziale create in [creare la prima funzione dal portale di Azure hello](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="84143-121">This topic uses as its starting point hello resources created in [Create your first function from hello Azure portal](functions-create-first-azure-function.md).</span></span>  
<span data-ttu-id="84143-122">Se non già stato fatto, completare questi toocreate ora i passaggi dell'app di funzione.</span><span class="sxs-lookup"><span data-stu-id="84143-122">If you haven't already done so, complete these steps now toocreate your function app.</span></span>

## <a name="create-a-cognitive-services-account"></a><span data-ttu-id="84143-123">Creare un account Servizi cognitivi</span><span class="sxs-lookup"><span data-stu-id="84143-123">Create a Cognitive Services account</span></span>

<span data-ttu-id="84143-124">Un account di servizi cognitivi è obbligatorio toodetect hello sentiment di tweet monitorato.</span><span class="sxs-lookup"><span data-stu-id="84143-124">A Cognitive Services account is required toodetect hello sentiment of tweets being monitored.</span></span>

1. <span data-ttu-id="84143-125">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="84143-125">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="84143-126">Fare clic su hello **New** pulsante disponibile nella hello angolo superiore sinistro del portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="84143-126">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

3. <span data-ttu-id="84143-127">Fare clic su **Dati e analisi** > **Servizi cognitivi**.</span><span class="sxs-lookup"><span data-stu-id="84143-127">Click **Data + Analytics** > **Cognitive  Services**.</span></span> <span data-ttu-id="84143-128">Quindi, utilizza le impostazioni di hello come specificato nella tabella di hello, accettare le condizioni di hello e controllare **toodashboard Pin**.</span><span class="sxs-lookup"><span data-stu-id="84143-128">Then, use hello settings as specified in hello table, accept hello terms, and check **Pin toodashboard**.</span></span>

    ![Pannello Creare account Servizi cognitivi](media/functions-twitter-email/cog_svcs_account.png)

    | <span data-ttu-id="84143-130">Impostazione</span><span class="sxs-lookup"><span data-stu-id="84143-130">Setting</span></span>      |  <span data-ttu-id="84143-131">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="84143-131">Suggested value</span></span>   | <span data-ttu-id="84143-132">Descrizione</span><span class="sxs-lookup"><span data-stu-id="84143-132">Description</span></span>                                        |
    | --- | --- | --- |
    | <span data-ttu-id="84143-133">**Nome**</span><span class="sxs-lookup"><span data-stu-id="84143-133">**Name**</span></span> | <span data-ttu-id="84143-134">MyCognitiveServicesAccnt</span><span class="sxs-lookup"><span data-stu-id="84143-134">MyCognitiveServicesAccnt</span></span> | <span data-ttu-id="84143-135">Scegliere un nome dell'account univoco.</span><span class="sxs-lookup"><span data-stu-id="84143-135">Choose a unique account name.</span></span> |
    | <span data-ttu-id="84143-136">**Tipo di API**</span><span class="sxs-lookup"><span data-stu-id="84143-136">**API type**</span></span> | <span data-ttu-id="84143-137">API Analisi del testo</span><span class="sxs-lookup"><span data-stu-id="84143-137">Text Analytics API</span></span> | <span data-ttu-id="84143-138">L'API utilizzata tooanalyze testo.</span><span class="sxs-lookup"><span data-stu-id="84143-138">API used tooanalyze text.</span></span>  |
    | <span data-ttu-id="84143-139">**Posizione**</span><span class="sxs-lookup"><span data-stu-id="84143-139">**Location**</span></span> | <span data-ttu-id="84143-140">Stati Uniti occidentali</span><span class="sxs-lookup"><span data-stu-id="84143-140">West US</span></span> | <span data-ttu-id="84143-141">Attualmente, per l'analisi è disponibile solo **Stati Uniti occidentali**.</span><span class="sxs-lookup"><span data-stu-id="84143-141">Currently, only **West US** is available for text analytics.</span></span> |
    | <span data-ttu-id="84143-142">**Piano tariffario**</span><span class="sxs-lookup"><span data-stu-id="84143-142">**Pricing tier**</span></span> | <span data-ttu-id="84143-143">F0</span><span class="sxs-lookup"><span data-stu-id="84143-143">F0</span></span> | <span data-ttu-id="84143-144">Iniziare con il livello più basso di hello.</span><span class="sxs-lookup"><span data-stu-id="84143-144">Start with hello lowest tier.</span></span> <span data-ttu-id="84143-145">Se si esauriscono le chiamate, applicare la scalabilità tooa di livello superiore.</span><span class="sxs-lookup"><span data-stu-id="84143-145">If you run out of calls, scale tooa higher tier.</span></span>|
    | <span data-ttu-id="84143-146">**Gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="84143-146">**Resource group**</span></span> | <span data-ttu-id="84143-147">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="84143-147">myResourceGroup</span></span> | <span data-ttu-id="84143-148">Utilizzare hello stesso gruppo di risorse per tutti i servizi in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="84143-148">Use hello same resource group for all services in this tutorial.</span></span>|

4. <span data-ttu-id="84143-149">Fare clic su **crea** toocreate l'account.</span><span class="sxs-lookup"><span data-stu-id="84143-149">Click **Create** toocreate your account.</span></span> <span data-ttu-id="84143-150">Dopo aver creato l'account di hello, fare clic su nuovo dashboard toohello aggiunti account servizi cognitivi.</span><span class="sxs-lookup"><span data-stu-id="84143-150">After hello account is created, click your new Cognitive Services account pinned toohello dashboard.</span></span> 

5. <span data-ttu-id="84143-151">Nell'account hello, fare clic su **chiavi**e quindi copiare il valore di hello di **tasto 1** e salvarlo.</span><span class="sxs-lookup"><span data-stu-id="84143-151">In hello account, click **Keys**, and then copy hello value of **Key 1** and save it.</span></span> <span data-ttu-id="84143-152">Utilizzare questo tooyour di app logica hello tooconnect chiave account di servizi cognitivi.</span><span class="sxs-lookup"><span data-stu-id="84143-152">You use this key tooconnect hello logic app tooyour Cognitive Services account.</span></span> 
 
    ![Chiavi](media/functions-twitter-email/keys.png)

## <a name="create-hello-function"></a><span data-ttu-id="84143-154">Creare la funzione hello</span><span class="sxs-lookup"><span data-stu-id="84143-154">Create hello function</span></span>

<span data-ttu-id="84143-155">Funzioni include le attività di elaborazione in un flusso di lavoro logica App toooffload un ottimo modo.</span><span class="sxs-lookup"><span data-stu-id="84143-155">Functions provides a great way toooffload processing tasks in a logic apps workflow.</span></span> <span data-ttu-id="84143-156">Questa esercitazione viene utilizzato un punteggi HTTP attivato funzione tooprocess tweet sentiment da servizi cognitivi e restituire un valore di categoria.</span><span class="sxs-lookup"><span data-stu-id="84143-156">This tutorial uses an HTTP triggered function tooprocess tweet sentiment scores from Cognitive Services and return a category value.</span></span>  

1. <span data-ttu-id="84143-157">Espandere l'applicazione di funzione, fare clic su hello  **+**  accanto troppo**funzioni**, fare clic su hello **HTTPTrigger** modello.</span><span class="sxs-lookup"><span data-stu-id="84143-157">Expand your function app, click hello **+** button next too**Functions**, click hello **HTTPTrigger** template.</span></span> <span data-ttu-id="84143-158">Tipo `CategorizeSentiment` per la funzione hello **nome** e fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="84143-158">Type `CategorizeSentiment` for hello function **Name** and click **Create**.</span></span>

    ![Pannello App per le funzioni, Funzioni +](media/functions-twitter-email/add_fun.png)

2. <span data-ttu-id="84143-160">Sostituire il contenuto di hello del file run.csx hello con hello seguente di codice, quindi fare clic su **salvare**:</span><span class="sxs-lookup"><span data-stu-id="84143-160">Replace hello contents of hello run.csx file with hello following code, then click **Save**:</span></span>

    ```c#
    using System.Net;
    
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
    {
        // hello sentiment category defaults too'GREEN'. 
        string category = "GREEN";
    
        // Get hello sentiment score from hello request body.
        double score = await req.Content.ReadAsAsync<double>();
        log.Info(string.Format("hello sentiment score received is '{0}'.",
                    score.ToString()));
    
        // Set hello category based on hello sentiment score.
        if (score < .3)
        {
            category = "RED";
        }
        else if (score < .6)
        {
            category = "YELLOW";
        }
        return req.CreateResponse(HttpStatusCode.OK, category);
    }
    ```
    <span data-ttu-id="84143-161">Questo codice di funzione restituisce una categoria di colore basata sul punteggio sentiment hello ricevuti nella richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="84143-161">This function code returns a color category based on hello sentiment score received in hello request.</span></span> 

3. <span data-ttu-id="84143-162">funzione hello tootest, fare clic su **Test** scheda Test hello di hello tooexpand estrema destra. Digitare un valore di `0.2` per hello **corpo della richiesta**, quindi fare clic su **eseguire**.</span><span class="sxs-lookup"><span data-stu-id="84143-162">tootest hello function, click **Test** at hello far right tooexpand hello Test tab. Type a value of `0.2` for hello **Request body**, and then click **Run**.</span></span> <span data-ttu-id="84143-163">Il valore **rosso** viene restituito nel corpo di hello della risposta hello.</span><span class="sxs-lookup"><span data-stu-id="84143-163">A value of **RED** is returned in hello body of hello response.</span></span> 

    ![Testare la funzione hello in hello portale di Azure](./media/functions-twitter-email/test.png)

<span data-ttu-id="84143-165">A questo punto è disponibile una funzione che classifica i punteggi dei sentiment.</span><span class="sxs-lookup"><span data-stu-id="84143-165">Now you have a function that categorizes sentiment scores.</span></span> <span data-ttu-id="84143-166">Nella fase successiva viene creata un'app per la logica che integra la funzione con gli account Twitter e Servizi cognitivi.</span><span class="sxs-lookup"><span data-stu-id="84143-166">Next, you create a logic app that integrates your function with your Twitter and Cognitive Services accounts.</span></span> 

## <a name="create-a-logic-app"></a><span data-ttu-id="84143-167">Creare un'app per la logica</span><span class="sxs-lookup"><span data-stu-id="84143-167">Create a logic app</span></span>   

1. <span data-ttu-id="84143-168">In hello portale di Azure, fare clic su hello **New** pulsante disponibile nella hello angolo superiore sinistro del portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="84143-168">In hello Azure portal, click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="84143-169">Fare clic su **Integrazione aziendale** > **App per la logica**.</span><span class="sxs-lookup"><span data-stu-id="84143-169">Click **Enterprise Integration** > **Logic App**.</span></span> <span data-ttu-id="84143-170">Quindi, utilizza le impostazioni di hello come specificato nella tabella di hello, controllare **Pin toodashboard**, fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="84143-170">Then, use hello settings as specified in hello table, check **Pin toodashboard**, and click **Create**.</span></span>
 
4. <span data-ttu-id="84143-171">Digitare quindi un **nome** come `TweetSentiment`, utilizzare le impostazioni di hello come specificato nella tabella hello, accettare le condizioni di hello e controllare **toodashboard Pin**.</span><span class="sxs-lookup"><span data-stu-id="84143-171">Then, type a **Name** like `TweetSentiment`,  use hello settings as specified in hello table, accept hello terms, and check **Pin toodashboard**.</span></span>

    ![Creare app per la logica in hello portale di Azure](./media/functions-twitter-email/new_logicApp.png)

    | <span data-ttu-id="84143-173">Impostazione</span><span class="sxs-lookup"><span data-stu-id="84143-173">Setting</span></span>      |  <span data-ttu-id="84143-174">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="84143-174">Suggested value</span></span>   | <span data-ttu-id="84143-175">Descrizione</span><span class="sxs-lookup"><span data-stu-id="84143-175">Description</span></span>                                        |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="84143-176">**Nome**</span><span class="sxs-lookup"><span data-stu-id="84143-176">**Name**</span></span> | <span data-ttu-id="84143-177">TweetSentiment</span><span class="sxs-lookup"><span data-stu-id="84143-177">TweetSentiment</span></span> | <span data-ttu-id="84143-178">Scegliere un nome appropriato per l'app.</span><span class="sxs-lookup"><span data-stu-id="84143-178">Choose an appropriate name for your app.</span></span> |
    | <span data-ttu-id="84143-179">**Gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="84143-179">**Resource group**</span></span> | <span data-ttu-id="84143-180">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="84143-180">myResourceGroup</span></span> | <span data-ttu-id="84143-181">L'API utilizzata tooanalyze testo.</span><span class="sxs-lookup"><span data-stu-id="84143-181">API used tooanalyze text.</span></span>  |
    | <span data-ttu-id="84143-182">**Posizione**</span><span class="sxs-lookup"><span data-stu-id="84143-182">**Location**</span></span> | <span data-ttu-id="84143-183">Stati Uniti Orientali</span><span class="sxs-lookup"><span data-stu-id="84143-183">East US</span></span> | <span data-ttu-id="84143-184">Scegliere un tooyou Chiudi percorso.</span><span class="sxs-lookup"><span data-stu-id="84143-184">Choose a location close tooyou.</span></span> |
    | <span data-ttu-id="84143-185">**Gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="84143-185">**Resource group**</span></span> | <span data-ttu-id="84143-186">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="84143-186">myResourceGroup</span></span> | <span data-ttu-id="84143-187">Scegliere hello stesso gruppo di risorse esistente come prima.</span><span class="sxs-lookup"><span data-stu-id="84143-187">Choose hello same existing resource group as before.</span></span>|

4. <span data-ttu-id="84143-188">Fare clic su **crea** toocreate app logica.</span><span class="sxs-lookup"><span data-stu-id="84143-188">Click **Create** toocreate your logic app.</span></span> <span data-ttu-id="84143-189">Dopo aver creato l'applicazione hello, fare clic su nuovo dashboard aggiunti toohello logica app.</span><span class="sxs-lookup"><span data-stu-id="84143-189">After hello app is created, click your new logic app pinned toohello dashboard.</span></span> <span data-ttu-id="84143-190">Nella finestra di progettazione logica App hello, scorrere verso il basso, quindi fare clic su hello **App vuota per la logica** modello.</span><span class="sxs-lookup"><span data-stu-id="84143-190">Then in hello Logic Apps Designer, scroll down and click hello **Blank Logic App** template.</span></span> 

    ![Modello App per la logica vuota](media/functions-twitter-email/blank.png)

<span data-ttu-id="84143-192">È ora possibile utilizzare hello logica App tooadd servizi e i trigger tooyour app Designer.</span><span class="sxs-lookup"><span data-stu-id="84143-192">You can now use hello Logic Apps Designer tooadd services and triggers tooyour app.</span></span>

## <a name="connect-tootwitter"></a><span data-ttu-id="84143-193">Connettersi tooTwitter</span><span class="sxs-lookup"><span data-stu-id="84143-193">Connect tooTwitter</span></span>

<span data-ttu-id="84143-194">Innanzitutto, creare un account Twitter di tooyour connessione.</span><span class="sxs-lookup"><span data-stu-id="84143-194">First, create a connection tooyour Twitter account.</span></span> <span data-ttu-id="84143-195">Hello logica app esegue il polling di tweet, che attivano toorun app hello.</span><span class="sxs-lookup"><span data-stu-id="84143-195">hello logic app polls for tweets, which trigger hello app toorun.</span></span>

1. <span data-ttu-id="84143-196">Nella finestra di progettazione hello, fare clic su hello **Twitter** del servizio e fare clic su hello **durante il postback un tweet nuovo** trigger.</span><span class="sxs-lookup"><span data-stu-id="84143-196">In hello designer, click hello **Twitter** service, and click hello **When a new tweet is posted** trigger.</span></span> <span data-ttu-id="84143-197">Accedi tooyour account Twitter e autorizzare la logica App toouse l'account.</span><span class="sxs-lookup"><span data-stu-id="84143-197">Sign in tooyour Twitter account and authorize Logic Apps toouse your account.</span></span>

2. <span data-ttu-id="84143-198">Utilizzare le impostazioni di trigger di hello Twitter come specificato nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="84143-198">Use hello Twitter trigger settings as specified in hello table.</span></span> 

    ![Impostazioni del connettore Twitter](media/functions-twitter-email/azure_tweet.png)

    | <span data-ttu-id="84143-200">Impostazione</span><span class="sxs-lookup"><span data-stu-id="84143-200">Setting</span></span>      |  <span data-ttu-id="84143-201">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="84143-201">Suggested value</span></span>   | <span data-ttu-id="84143-202">Descrizione</span><span class="sxs-lookup"><span data-stu-id="84143-202">Description</span></span>                                        |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="84143-203">**Testo di ricerca**</span><span class="sxs-lookup"><span data-stu-id="84143-203">**Search text**</span></span> | <span data-ttu-id="84143-204">#Azure</span><span class="sxs-lookup"><span data-stu-id="84143-204">#Azure</span></span> | <span data-ttu-id="84143-205">Utilizzare un hashtag che è abbastanza comune per toogenerate nuovo TWEET nell'intervallo di hello scelto.</span><span class="sxs-lookup"><span data-stu-id="84143-205">Use a hashtag that is popular enough for toogenerate new tweets in hello chosen interval.</span></span> <span data-ttu-id="84143-206">Quando si utilizza livello gratuito hello e il hashtag è troppo comune, è possibile utilizzare le transazioni hello rapidamente nell'account di servizi cognitivi.</span><span class="sxs-lookup"><span data-stu-id="84143-206">When using hello Free tier and your hashtag is too popular, you can quickly use up hello transactions in your Cognitive Services account.</span></span> |
    | <span data-ttu-id="84143-207">**Frequenza**</span><span class="sxs-lookup"><span data-stu-id="84143-207">**Frequency**</span></span> | <span data-ttu-id="84143-208">Minuto</span><span class="sxs-lookup"><span data-stu-id="84143-208">Minute</span></span> | <span data-ttu-id="84143-209">unità di frequenza Hello utilizzato per il polling di Twitter.</span><span class="sxs-lookup"><span data-stu-id="84143-209">hello frequency unit used for polling Twitter.</span></span>  |
    | <span data-ttu-id="84143-210">**Interval**</span><span class="sxs-lookup"><span data-stu-id="84143-210">**Interval**</span></span> | <span data-ttu-id="84143-211">15</span><span class="sxs-lookup"><span data-stu-id="84143-211">15</span></span> | <span data-ttu-id="84143-212">tempo di Hello trascorso tra le richieste a Twitter, in unità di frequenza.</span><span class="sxs-lookup"><span data-stu-id="84143-212">hello time elapsed between Twitter requests, in frequency units.</span></span> |

3.  <span data-ttu-id="84143-213">Fare clic su **salvare** tooconnect tooyour account Twitter.</span><span class="sxs-lookup"><span data-stu-id="84143-213">Click **Save** tooconnect tooyour Twitter account.</span></span> 

<span data-ttu-id="84143-214">A questo punto l'app tooTwitter connesso.</span><span class="sxs-lookup"><span data-stu-id="84143-214">Now your app is connected tooTwitter.</span></span> <span data-ttu-id="84143-215">Connettersi quindi sentiment di tootext analitica toodetect hello di tweet raccolti.</span><span class="sxs-lookup"><span data-stu-id="84143-215">Next, you connect tootext analytics toodetect hello sentiment of collected tweets.</span></span>

## <a name="add-sentiment-detection"></a><span data-ttu-id="84143-216">Aggiungere il rilevamento dei sentiment</span><span class="sxs-lookup"><span data-stu-id="84143-216">Add sentiment detection</span></span>

1. <span data-ttu-id="84143-217">Selezionare **Nuovo passaggio** e quindi **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="84143-217">Click **New Step**, and then **Add an action**.</span></span>

    ![Nuovo passaggio e quindi Aggiungi un'azione.](media/functions-twitter-email/new_step.png)

2. <span data-ttu-id="84143-219">In **scegliere un'azione**, fare clic su **testo Analitica**, quindi fare clic su hello **rilevare sentiment** azione.</span><span class="sxs-lookup"><span data-stu-id="84143-219">In **Choose an action**, click **Text Analytics**, and then click hello **Detect sentiment** action.</span></span>

    ![Rileva sentiment](media/functions-twitter-email/detect_sent.png)

3. <span data-ttu-id="84143-221">Digitare un nome di connessione, ad esempio `MyCognitiveServicesConnection`, incollare la chiave hello per i servizi cognitivi account salvato e fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="84143-221">Type a connection name such as `MyCognitiveServicesConnection`, paste hello key for your Cognitive Services account that you saved, and click **Create**.</span></span>  

4. <span data-ttu-id="84143-222">Fare clic su **testo tooanalyze** > **Tweet testo**, quindi fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="84143-222">Click **Text tooanalyze** > **Tweet text**, and then click **Save**.</span></span>  

    ![Rileva sentiment](media/functions-twitter-email/ds_tta.png)

<span data-ttu-id="84143-224">Dopo avere configurato il rilevamento di valutazione, è possibile aggiungere una funzione tooyour di connessione che utilizza l'output di hello sentiment punteggio.</span><span class="sxs-lookup"><span data-stu-id="84143-224">Now that sentiment detection is configured, you can add a connection tooyour function that consumes hello sentiment score output.</span></span>

## <a name="connect-sentiment-output-tooyour-function"></a><span data-ttu-id="84143-225">Sentiment output tooyour funzione di connessione</span><span class="sxs-lookup"><span data-stu-id="84143-225">Connect sentiment output tooyour function</span></span>

1. <span data-ttu-id="84143-226">Nella finestra di progettazione logica App hello, fare clic su **nuovo passaggio** > **aggiungere un'azione**e quindi fare clic su **Azure funzioni**.</span><span class="sxs-lookup"><span data-stu-id="84143-226">In hello Logic Apps Designer, click **New step** > **Add an action**, and then click **Azure Functions**.</span></span> 

2. <span data-ttu-id="84143-227">Fare clic su **scegliere una funzione di Azure**selezionare hello **CategorizeSentiment** funzione creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="84143-227">Click **Choose an Azure function**, select hello **CategorizeSentiment** function you created earlier.</span></span>  

    ![Casella Funzione Azure con Scegliere una funzione di Azure](media/functions-twitter-email/choose_fun.png)

3. <span data-ttu-id="84143-229">In **Corpo della richiesta** fare clic su **Punteggio** e quindi su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="84143-229">In **Request Body**, click **Score** and then **Save**.</span></span>

    ![Score](media/functions-twitter-email/trigger_score.png)

<span data-ttu-id="84143-231">A questo punto, la funzione viene attivata quando viene inviato un punteggio sentiment da hello logica app.</span><span class="sxs-lookup"><span data-stu-id="84143-231">Now, your function is triggered when a sentiment score is sent from hello logic app.</span></span> <span data-ttu-id="84143-232">Una categoria con codifica a colori viene restituita toohello logica app dalla funzione hello.</span><span class="sxs-lookup"><span data-stu-id="84143-232">A color-coded category is returned toohello logic app by hello function.</span></span> <span data-ttu-id="84143-233">Aggiungere quindi una notifica di posta elettronica viene inviata quando il valore sentiment **rosso** restituiti dalla funzione hello.</span><span class="sxs-lookup"><span data-stu-id="84143-233">Next, you add an email notification that is sent when a sentiment value of **RED** is returned from hello function.</span></span> 

## <a name="add-email-notifications"></a><span data-ttu-id="84143-234">Aggiungere le notifiche di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="84143-234">Add email notifications</span></span>

<span data-ttu-id="84143-235">ultima parte di Hello del flusso di lavoro hello è tootrigger un messaggio di posta elettronica quando viene calcolato il punteggio sentiment hello come _rosso_.</span><span class="sxs-lookup"><span data-stu-id="84143-235">hello last part of hello workflow is tootrigger an email when hello sentiment is scored as _RED_.</span></span> <span data-ttu-id="84143-236">Questo argomento fa uso di un connettore Outlook.com.</span><span class="sxs-lookup"><span data-stu-id="84143-236">This topic uses an Outlook.com connector.</span></span> <span data-ttu-id="84143-237">È possibile eseguire simile passaggi toouse un connettore Gmail o Outlook di Office 365.</span><span class="sxs-lookup"><span data-stu-id="84143-237">You can perform similar steps toouse a Gmail or Office 365 Outlook connector.</span></span>   

1. <span data-ttu-id="84143-238">Nella finestra di progettazione logica App hello, fare clic su **nuovo passaggio** > **aggiungere una condizione**.</span><span class="sxs-lookup"><span data-stu-id="84143-238">In hello Logic Apps Designer, click **New step** > **Add a condition**.</span></span> 

2. <span data-ttu-id="84143-239">Fare clic su **Scegliere un valore** e quindi su **Corpo**.</span><span class="sxs-lookup"><span data-stu-id="84143-239">Click **Choose a value**, then click **Body**.</span></span> <span data-ttu-id="84143-240">Selezionare **è uguale a**, fare clic su **Scegliere un valore**, digitare `RED` e quindi fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="84143-240">Select **is equal to**, click **Choose a value** and type `RED`, and click **Save**.</span></span> 

    ![Aggiungi condizione toohello logica app.](media/functions-twitter-email/condition.png)

3. <span data-ttu-id="84143-242">In **in caso AFFERMATIVO, non eseguire alcuna operazione**, fare clic su **aggiungere un'azione**, cercare `outlook.com`, fare clic su **invia un messaggio di posta elettronica**ed eseguire l'accesso tooyour account Outlook.com.</span><span class="sxs-lookup"><span data-stu-id="84143-242">In **IF YES, DO NOTHING**, click **Add an action**, search for `outlook.com`, click **Send an email**, and sign in tooyour Outlook.com account.</span></span>
    
    ![Scegliere un'azione per la condizione hello.](media/functions-twitter-email/outlook.png)

    > [!NOTE]
    > <span data-ttu-id="84143-244">Se non è disponibile un account Outlook.com, è possibile scegliere un altro connettore, ad esempio Gmail o Office 365 Outlook.</span><span class="sxs-lookup"><span data-stu-id="84143-244">If you don't have an Outlook.com account, you can choose another connector, such as Gmail or Office 365 Outlook</span></span>

4. <span data-ttu-id="84143-245">In hello **invia un messaggio di posta elettronica** azione, utilizza le impostazioni di posta elettronica hello come specificato nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="84143-245">In hello **Send an email** action, use hello email settings as specified in hello table.</span></span> 

    ![Configurare la posta elettronica hello per l'invio di hello un'azione di posta elettronica.](media/functions-twitter-email/sendemail.png)

    | <span data-ttu-id="84143-247">Impostazione</span><span class="sxs-lookup"><span data-stu-id="84143-247">Setting</span></span>      |  <span data-ttu-id="84143-248">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="84143-248">Suggested value</span></span>   | <span data-ttu-id="84143-249">Descrizione</span><span class="sxs-lookup"><span data-stu-id="84143-249">Description</span></span>  |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="84143-250">**To**</span><span class="sxs-lookup"><span data-stu-id="84143-250">**To**</span></span> | <span data-ttu-id="84143-251">Digitare l'indirizzo di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="84143-251">Type your email address</span></span> | <span data-ttu-id="84143-252">indirizzo di posta elettronica Hello che riceve la notifica di hello.</span><span class="sxs-lookup"><span data-stu-id="84143-252">hello email address that receives hello notification.</span></span> |
    | <span data-ttu-id="84143-253">**Oggetto**</span><span class="sxs-lookup"><span data-stu-id="84143-253">**Subject**</span></span> | <span data-ttu-id="84143-254">Rilevato sentiment di tweet negativo</span><span class="sxs-lookup"><span data-stu-id="84143-254">Negative tweet sentiment detected</span></span>  | <span data-ttu-id="84143-255">riga dell'oggetto Hello di notifica tramite posta elettronica hello.</span><span class="sxs-lookup"><span data-stu-id="84143-255">hello subject line of hello email notification.</span></span>  |
    | <span data-ttu-id="84143-256">**Corpo**</span><span class="sxs-lookup"><span data-stu-id="84143-256">**Body**</span></span> | <span data-ttu-id="84143-257">Testo tweet, Località</span><span class="sxs-lookup"><span data-stu-id="84143-257">Tweet text, Location</span></span> | <span data-ttu-id="84143-258">Fare clic su hello **Tweet testo** e **percorso** parametri.</span><span class="sxs-lookup"><span data-stu-id="84143-258">Click hello **Tweet text** and **Location** parameters.</span></span> |

5.  <span data-ttu-id="84143-259">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="84143-259">Click **Save**.</span></span>

<span data-ttu-id="84143-260">Ora che hello è completato, è possibile abilitare hello logica app e vedere la funzione hello al lavoro.</span><span class="sxs-lookup"><span data-stu-id="84143-260">Now that hello workflow is complete, you can enable hello logic app and see hello function at work.</span></span>

## <a name="test-hello-workflow"></a><span data-ttu-id="84143-261">Flusso di lavoro di test hello</span><span class="sxs-lookup"><span data-stu-id="84143-261">Test hello workflow</span></span>

1. <span data-ttu-id="84143-262">Nella finestra di progettazione logica App hello, fare clic su **eseguire** toostart hello app.</span><span class="sxs-lookup"><span data-stu-id="84143-262">In hello Logic App Designer, click **Run** toostart hello app.</span></span>

2. <span data-ttu-id="84143-263">Nella colonna sinistra hello, fare clic su **Panoramica** stato hello toosee di hello logica app.</span><span class="sxs-lookup"><span data-stu-id="84143-263">In hello left column, click **Overview** toosee hello status of hello logic app.</span></span> 
 
    ![Stato di esecuzione dell'app per la logica](media/functions-twitter-email/over1.png)

3. <span data-ttu-id="84143-265">(Facoltativo) Fare clic su uno di hello esecuzioni toosee dettagli di esecuzione hello.</span><span class="sxs-lookup"><span data-stu-id="84143-265">(Optional) Click one of hello runs toosee details of hello execution.</span></span>

4. <span data-ttu-id="84143-266">Funzione tooyour mano, visualizzare i log di hello e verificare che i valori di valutazione ricevuti ed elaborati.</span><span class="sxs-lookup"><span data-stu-id="84143-266">Go tooyour function, view hello logs, and verify that sentiment values were received and processed.</span></span>
 
    ![Visualizzare i log della funzione](media/functions-twitter-email/sent.png)

5. <span data-ttu-id="84143-268">Quando viene rilevato un sentiment potenzialmente negativo, si riceve un messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="84143-268">When a potentially negative sentiment is detected, you receive an email.</span></span> <span data-ttu-id="84143-269">Se non si è ricevuto un messaggio di posta elettronica, è possibile modificare ogni volta hello funzione codice tooreturn rosso:</span><span class="sxs-lookup"><span data-stu-id="84143-269">If you haven't received an email, you can change hello function code tooreturn RED every time:</span></span>

        return req.CreateResponse(HttpStatusCode.OK, "RED");

    <span data-ttu-id="84143-270">Dopo aver verificato le notifiche di posta elettronica, modificare il codice originale toohello indietro:</span><span class="sxs-lookup"><span data-stu-id="84143-270">After you have verified email notifications, change back toohello original code:</span></span>

        return req.CreateResponse(HttpStatusCode.OK, category);

    > [!IMPORTANT]
    > <span data-ttu-id="84143-271">Dopo aver completato questa esercitazione, è consigliabile disabilitare hello logica app.</span><span class="sxs-lookup"><span data-stu-id="84143-271">After you have completed this tutorial, you should disable hello logic app.</span></span> <span data-ttu-id="84143-272">Disabilitando l'applicazione hello evitare di essere addebitati per le esecuzioni e utilizzare le transazioni hello nell'account di servizi cognitivi.</span><span class="sxs-lookup"><span data-stu-id="84143-272">By disabling hello app, you avoid being charged for executions and using up hello transactions in your Cognitive Services account.</span></span>

<span data-ttu-id="84143-273">Ora è stato illustrato come è facile toointegrate funzioni in un flusso di lavoro App per la logica.</span><span class="sxs-lookup"><span data-stu-id="84143-273">Now you have seen how easy it is toointegrate Functions into a Logic Apps workflow.</span></span>

## <a name="disable-hello-logic-app"></a><span data-ttu-id="84143-274">Disabilitare hello logica app</span><span class="sxs-lookup"><span data-stu-id="84143-274">Disable hello logic app</span></span>

<span data-ttu-id="84143-275">toodisable hello logica app, fare clic su **Panoramica** e quindi fare clic su **disabilitare** in alto hello hello.</span><span class="sxs-lookup"><span data-stu-id="84143-275">toodisable hello logic app, click **Overview** and then click **Disable** at hello top of hello screen.</span></span> <span data-ttu-id="84143-276">Questo arresta hello app per la logica di esecuzione e gli addebiti senza eliminare l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="84143-276">This stops hello logic app from running and incurring charges without deleting hello app.</span></span> 

![Log della funzione](media/functions-twitter-email/disable-logic-app.png)

## <a name="next-steps"></a><span data-ttu-id="84143-278">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="84143-278">Next steps</span></span>

<span data-ttu-id="84143-279">In questa esercitazione si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="84143-279">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="84143-280">Creare un account di Servizi cognitivi.</span><span class="sxs-lookup"><span data-stu-id="84143-280">Create a Cognitive Services account.</span></span>
> * <span data-ttu-id="84143-281">Creare una funzione che classifica i sentiment nei tweet.</span><span class="sxs-lookup"><span data-stu-id="84143-281">Create a function that categorizes tweet sentiment.</span></span>
> * <span data-ttu-id="84143-282">Creare un'app di logica che si connette tooTwitter.</span><span class="sxs-lookup"><span data-stu-id="84143-282">Create a logic app that connects tooTwitter.</span></span>
> * <span data-ttu-id="84143-283">Aggiungere app per la logica toohello sentiment rilevamento.</span><span class="sxs-lookup"><span data-stu-id="84143-283">Add sentiment detection toohello logic app.</span></span> 
> * <span data-ttu-id="84143-284">Hello logica app toohello funzione di connessione.</span><span class="sxs-lookup"><span data-stu-id="84143-284">Connect hello logic app toohello function.</span></span>
> * <span data-ttu-id="84143-285">Inviare un messaggio di posta elettronica in base alla risposta hello dalla funzione hello.</span><span class="sxs-lookup"><span data-stu-id="84143-285">Send an email based on hello response from hello function.</span></span>

<span data-ttu-id="84143-286">Spostare toolearn esercitazione successiva toohello come toocreate un'API senza server per la funzione.</span><span class="sxs-lookup"><span data-stu-id="84143-286">Advance toohello next tutorial toolearn how toocreate a serverless API for your function.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="84143-287">Creare un'API senza server mediante Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="84143-287">Create a serverless API using Azure Functions</span></span>](functions-create-serverless-api.md)

<span data-ttu-id="84143-288">toolearn informazioni sulle App per la logica, vedere [Azure logica app](../logic-apps/logic-apps-what-are-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="84143-288">toolearn more about Logic Apps, see [Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md).</span></span>

