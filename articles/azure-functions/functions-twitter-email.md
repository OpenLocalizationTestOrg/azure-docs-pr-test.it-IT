---
title: Creare una funzione che si integra con App per la logica di Azure | Microsoft Docs
description: "Creare una funzione che si integra con le app per la logica di Azure e i servizi cognitivi di Azure per classificare la valutazione dei tweet e inviare notifiche quando la valutazione è bassa."
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
ms.openlocfilehash: 4a5dc668e21c5328b308c8f5852aaa922232374d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-that-integrates-with-azure-logic-apps"></a><span data-ttu-id="f7d46-104">Creare una funzione che si integra con le app per la logica di Azure</span><span class="sxs-lookup"><span data-stu-id="f7d46-104">Create a function that integrates with Azure Logic Apps</span></span>

<span data-ttu-id="f7d46-105">Funzioni di Azure si integra con App per la logica di Azure in Progettazione app per la logica.</span><span class="sxs-lookup"><span data-stu-id="f7d46-105">Azure Functions integrates with Azure Logic Apps in the Logic Apps Designer.</span></span> <span data-ttu-id="f7d46-106">L'integrazione consente di usare la potenza di calcolo di Funzioni nelle orchestrazioni con altri servizi di Azure e di terze parti.</span><span class="sxs-lookup"><span data-stu-id="f7d46-106">This integration lets you use the computing power of Functions in orchestrations with other Azure and third-party services.</span></span> 

<span data-ttu-id="f7d46-107">Questa esercitazione illustra come usare Funzioni con App per la logica e Servizi cognitivi di Azure per analizzare i sentiment nei post di Twitter.</span><span class="sxs-lookup"><span data-stu-id="f7d46-107">This tutorial shows you how to use Functions with Logic Apps and Azure Cognitive Services to analyze sentiment from Twitter posts.</span></span> <span data-ttu-id="f7d46-108">Una funzione attivata tramite HTTP classifica i tweet come verde, giallo o rosso in base al punteggio del sentiment.</span><span class="sxs-lookup"><span data-stu-id="f7d46-108">An HTTP triggered function categorizes tweets as green, yellow, or red based on the sentiment score.</span></span> <span data-ttu-id="f7d46-109">Quando viene rilevato un livello di sentiment basso viene inviato un messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="f7d46-109">An email is sent when poor sentiment is detected.</span></span> 

![immagine dei primi due passaggi dell'app in Progettazione app per la logica](media/functions-twitter-email/designer1.png)

<span data-ttu-id="f7d46-111">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="f7d46-111">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f7d46-112">Creare un account di Servizi cognitivi.</span><span class="sxs-lookup"><span data-stu-id="f7d46-112">Create a Cognitive Services account.</span></span>
> * <span data-ttu-id="f7d46-113">Creare una funzione che classifica i sentiment nei tweet.</span><span class="sxs-lookup"><span data-stu-id="f7d46-113">Create a function that categorizes tweet sentiment.</span></span>
> * <span data-ttu-id="f7d46-114">Creare un'app per la logica che si connette a Twitter.</span><span class="sxs-lookup"><span data-stu-id="f7d46-114">Create a logic app that connects to Twitter.</span></span>
> * <span data-ttu-id="f7d46-115">Aggiungere il rilevamento dei sentiment all'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="f7d46-115">Add sentiment detection to the logic app.</span></span> 
> * <span data-ttu-id="f7d46-116">Connettere l'app per la logica alla funzione.</span><span class="sxs-lookup"><span data-stu-id="f7d46-116">Connect the logic app to the function.</span></span>
> * <span data-ttu-id="f7d46-117">Inviare un messaggio di posta elettronica in base alla risposta dalla funzione.</span><span class="sxs-lookup"><span data-stu-id="f7d46-117">Send an email based on the response from the function.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f7d46-118">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f7d46-118">Prerequisites</span></span>

+ <span data-ttu-id="f7d46-119">Un account [Twitter](https://twitter.com/) attivo.</span><span class="sxs-lookup"><span data-stu-id="f7d46-119">An active [Twitter](https://twitter.com/) account.</span></span> 
+ <span data-ttu-id="f7d46-120">Un account [Outlook.com](https://outlook.com/) per l'invio delle notifiche.</span><span class="sxs-lookup"><span data-stu-id="f7d46-120">An [Outlook.com](https://outlook.com/) account (for sending notifications).</span></span>
+ <span data-ttu-id="f7d46-121">Questo argomento usa per iniziare le risorse create in [Creare la prima funzione nel portale di Azure](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="f7d46-121">This topic uses as its starting point the resources created in [Create your first function from the Azure portal](functions-create-first-azure-function.md).</span></span>  
<span data-ttu-id="f7d46-122">Se queste procedure non sono state ancora completate, completarle ora per creare l'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="f7d46-122">If you haven't already done so, complete these steps now to create your function app.</span></span>

## <a name="create-a-cognitive-services-account"></a><span data-ttu-id="f7d46-123">Creare un account Servizi cognitivi</span><span class="sxs-lookup"><span data-stu-id="f7d46-123">Create a Cognitive Services account</span></span>

<span data-ttu-id="f7d46-124">È necessario un account Servizi cognitivi per rilevare il sentiment dei tweet monitorati.</span><span class="sxs-lookup"><span data-stu-id="f7d46-124">A Cognitive Services account is required to detect the sentiment of tweets being monitored.</span></span>

1. <span data-ttu-id="f7d46-125">Accedere al [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f7d46-125">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="f7d46-126">Fare clic sul pulsante **Nuovo** nell'angolo superiore sinistro del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f7d46-126">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

3. <span data-ttu-id="f7d46-127">Fare clic su **Dati e analisi** > **Servizi cognitivi**.</span><span class="sxs-lookup"><span data-stu-id="f7d46-127">Click **Data + Analytics** > **Cognitive  Services**.</span></span> <span data-ttu-id="f7d46-128">Usare quindi le impostazioni indicate nella tabella, accettare le condizioni e selezionare **Aggiungi al dashboard**.</span><span class="sxs-lookup"><span data-stu-id="f7d46-128">Then, use the settings as specified in the table, accept the terms, and check **Pin to dashboard**.</span></span>

    ![Pannello Creare account Servizi cognitivi](media/functions-twitter-email/cog_svcs_account.png)

    | <span data-ttu-id="f7d46-130">Impostazione</span><span class="sxs-lookup"><span data-stu-id="f7d46-130">Setting</span></span>      |  <span data-ttu-id="f7d46-131">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="f7d46-131">Suggested value</span></span>   | <span data-ttu-id="f7d46-132">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7d46-132">Description</span></span>                                        |
    | --- | --- | --- |
    | <span data-ttu-id="f7d46-133">**Nome**</span><span class="sxs-lookup"><span data-stu-id="f7d46-133">**Name**</span></span> | <span data-ttu-id="f7d46-134">MyCognitiveServicesAccnt</span><span class="sxs-lookup"><span data-stu-id="f7d46-134">MyCognitiveServicesAccnt</span></span> | <span data-ttu-id="f7d46-135">Scegliere un nome dell'account univoco.</span><span class="sxs-lookup"><span data-stu-id="f7d46-135">Choose a unique account name.</span></span> |
    | <span data-ttu-id="f7d46-136">**Tipo di API**</span><span class="sxs-lookup"><span data-stu-id="f7d46-136">**API type**</span></span> | <span data-ttu-id="f7d46-137">API Analisi del testo</span><span class="sxs-lookup"><span data-stu-id="f7d46-137">Text Analytics API</span></span> | <span data-ttu-id="f7d46-138">API usata per analizzare il testo.</span><span class="sxs-lookup"><span data-stu-id="f7d46-138">API used to analyze text.</span></span>  |
    | <span data-ttu-id="f7d46-139">**Posizione**</span><span class="sxs-lookup"><span data-stu-id="f7d46-139">**Location**</span></span> | <span data-ttu-id="f7d46-140">Stati Uniti occidentali</span><span class="sxs-lookup"><span data-stu-id="f7d46-140">West US</span></span> | <span data-ttu-id="f7d46-141">Attualmente, per l'analisi è disponibile solo **Stati Uniti occidentali**.</span><span class="sxs-lookup"><span data-stu-id="f7d46-141">Currently, only **West US** is available for text analytics.</span></span> |
    | <span data-ttu-id="f7d46-142">**Piano tariffario**</span><span class="sxs-lookup"><span data-stu-id="f7d46-142">**Pricing tier**</span></span> | <span data-ttu-id="f7d46-143">F0</span><span class="sxs-lookup"><span data-stu-id="f7d46-143">F0</span></span> | <span data-ttu-id="f7d46-144">Iniziare dal livello più basso.</span><span class="sxs-lookup"><span data-stu-id="f7d46-144">Start with the lowest tier.</span></span> <span data-ttu-id="f7d46-145">Se si esauriscono le chiamate, passare a un livello superiore.</span><span class="sxs-lookup"><span data-stu-id="f7d46-145">If you run out of calls, scale to a higher tier.</span></span>|
    | <span data-ttu-id="f7d46-146">**Gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="f7d46-146">**Resource group**</span></span> | <span data-ttu-id="f7d46-147">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f7d46-147">myResourceGroup</span></span> | <span data-ttu-id="f7d46-148">Usare lo stesso gruppo di risorse per tutti i servizi in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="f7d46-148">Use the same resource group for all services in this tutorial.</span></span>|

4. <span data-ttu-id="f7d46-149">Fare clic su **Crea** per creare l'account.</span><span class="sxs-lookup"><span data-stu-id="f7d46-149">Click **Create** to create your account.</span></span> <span data-ttu-id="f7d46-150">Dopo aver creato l'account, fare clic sul nuovo account Servizi cognitivi aggiunto al dashboard.</span><span class="sxs-lookup"><span data-stu-id="f7d46-150">After the account is created, click your new Cognitive Services account pinned to the dashboard.</span></span> 

5. <span data-ttu-id="f7d46-151">Nell'account fare clic su **Chiavi**, quindi copiare il valore di **Chiave 1** e salvarlo.</span><span class="sxs-lookup"><span data-stu-id="f7d46-151">In the account, click **Keys**, and then copy the value of **Key 1** and save it.</span></span> <span data-ttu-id="f7d46-152">Questa chiave viene usata per connettere l'app per la logica all'account Servizi cognitivi.</span><span class="sxs-lookup"><span data-stu-id="f7d46-152">You use this key to connect the logic app to your Cognitive Services account.</span></span> 
 
    ![Chiavi](media/functions-twitter-email/keys.png)

## <a name="create-the-function"></a><span data-ttu-id="f7d46-154">Creare la funzione</span><span class="sxs-lookup"><span data-stu-id="f7d46-154">Create the function</span></span>

<span data-ttu-id="f7d46-155">Funzioni permette di ripartire il carico di lavoro delle attività di elaborazione in un flusso di lavoro di app per la logica.</span><span class="sxs-lookup"><span data-stu-id="f7d46-155">Functions provides a great way to offload processing tasks in a logic apps workflow.</span></span> <span data-ttu-id="f7d46-156">Questa esercitazione fa uso di una funzione attivata tramite HTTP per elaborare i punteggi attribuiti da Servizi cognitivi ai sentiment dei tweet e restituire un valore categoria.</span><span class="sxs-lookup"><span data-stu-id="f7d46-156">This tutorial uses an HTTP triggered function to process tweet sentiment scores from Cognitive Services and return a category value.</span></span>  

1. <span data-ttu-id="f7d46-157">Espandere l'app per le funzioni, fare clic sul pulsante **+** accanto a **Funzioni** e fare clic sul modello **HTTPTrigger**.</span><span class="sxs-lookup"><span data-stu-id="f7d46-157">Expand your function app, click the **+** button next to **Functions**, click the **HTTPTrigger** template.</span></span> <span data-ttu-id="f7d46-158">Digitare `CategorizeSentiment` per il **Nome** della funzione e fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="f7d46-158">Type `CategorizeSentiment` for the function **Name** and click **Create**.</span></span>

    ![Pannello App per le funzioni, Funzioni +](media/functions-twitter-email/add_fun.png)

2. <span data-ttu-id="f7d46-160">Sostituire il contenuto del file run.csx con il codice seguente e quindi fare clic su **Salva**:</span><span class="sxs-lookup"><span data-stu-id="f7d46-160">Replace the contents of the run.csx file with the following code, then click **Save**:</span></span>

    ```c#
    using System.Net;
    
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
    {
        // The sentiment category defaults to 'GREEN'. 
        string category = "GREEN";
    
        // Get the sentiment score from the request body.
        double score = await req.Content.ReadAsAsync<double>();
        log.Info(string.Format("The sentiment score received is '{0}'.",
                    score.ToString()));
    
        // Set the category based on the sentiment score.
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
    <span data-ttu-id="f7d46-161">Questo codice di funzione restituisce una categoria colore in base al punteggio del sentiment ricevuto nella richiesta.</span><span class="sxs-lookup"><span data-stu-id="f7d46-161">This function code returns a color category based on the sentiment score received in the request.</span></span> 

3. <span data-ttu-id="f7d46-162">Per testare la funzione, fare clic su **Test** a destra per espandere la scheda Test. Digitare un valore di `0.2` per il **Corpo della richiesta** e quindi fare clic su **Esegui**.</span><span class="sxs-lookup"><span data-stu-id="f7d46-162">To test the function, click **Test** at the far right to expand the Test tab. Type a value of `0.2` for the **Request body**, and then click **Run**.</span></span> <span data-ttu-id="f7d46-163">Nel corpo della risposta verrà restituito il valore **RED**.</span><span class="sxs-lookup"><span data-stu-id="f7d46-163">A value of **RED** is returned in the body of the response.</span></span> 

    ![Testare la funzione nel portale di Azure](./media/functions-twitter-email/test.png)

<span data-ttu-id="f7d46-165">A questo punto è disponibile una funzione che classifica i punteggi dei sentiment.</span><span class="sxs-lookup"><span data-stu-id="f7d46-165">Now you have a function that categorizes sentiment scores.</span></span> <span data-ttu-id="f7d46-166">Nella fase successiva viene creata un'app per la logica che integra la funzione con gli account Twitter e Servizi cognitivi.</span><span class="sxs-lookup"><span data-stu-id="f7d46-166">Next, you create a logic app that integrates your function with your Twitter and Cognitive Services accounts.</span></span> 

## <a name="create-a-logic-app"></a><span data-ttu-id="f7d46-167">Creare un'app per la logica</span><span class="sxs-lookup"><span data-stu-id="f7d46-167">Create a logic app</span></span>   

1. <span data-ttu-id="f7d46-168">Nel portale di Azure fare clic sul pulsante **Nuovo** nell'angolo in alto a sinistra del portale.</span><span class="sxs-lookup"><span data-stu-id="f7d46-168">In the Azure portal, click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="f7d46-169">Fare clic su **Integrazione aziendale** > **App per la logica**.</span><span class="sxs-lookup"><span data-stu-id="f7d46-169">Click **Enterprise Integration** > **Logic App**.</span></span> <span data-ttu-id="f7d46-170">Usare quindi le impostazioni indicate nella tabella, selezionare **Aggiungi al dashboard** e fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="f7d46-170">Then, use the settings as specified in the table, check **Pin to dashboard**, and click **Create**.</span></span>
 
4. <span data-ttu-id="f7d46-171">Digitare un **Nome**, ad esempio `TweetSentiment`, usare le impostazioni indicate nella tabella, accettare le condizioni e selezionare **Aggiungi al dashboard**.</span><span class="sxs-lookup"><span data-stu-id="f7d46-171">Then, type a **Name** like `TweetSentiment`,  use the settings as specified in the table, accept the terms, and check **Pin to dashboard**.</span></span>

    ![Creare l'app per la logica nel portale di Azure](./media/functions-twitter-email/new_logicApp.png)

    | <span data-ttu-id="f7d46-173">Impostazione</span><span class="sxs-lookup"><span data-stu-id="f7d46-173">Setting</span></span>      |  <span data-ttu-id="f7d46-174">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="f7d46-174">Suggested value</span></span>   | <span data-ttu-id="f7d46-175">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7d46-175">Description</span></span>                                        |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="f7d46-176">**Nome**</span><span class="sxs-lookup"><span data-stu-id="f7d46-176">**Name**</span></span> | <span data-ttu-id="f7d46-177">TweetSentiment</span><span class="sxs-lookup"><span data-stu-id="f7d46-177">TweetSentiment</span></span> | <span data-ttu-id="f7d46-178">Scegliere un nome appropriato per l'app.</span><span class="sxs-lookup"><span data-stu-id="f7d46-178">Choose an appropriate name for your app.</span></span> |
    | <span data-ttu-id="f7d46-179">**Gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="f7d46-179">**Resource group**</span></span> | <span data-ttu-id="f7d46-180">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f7d46-180">myResourceGroup</span></span> | <span data-ttu-id="f7d46-181">API usata per analizzare il testo.</span><span class="sxs-lookup"><span data-stu-id="f7d46-181">API used to analyze text.</span></span>  |
    | <span data-ttu-id="f7d46-182">**Posizione**</span><span class="sxs-lookup"><span data-stu-id="f7d46-182">**Location**</span></span> | <span data-ttu-id="f7d46-183">Stati Uniti orientali</span><span class="sxs-lookup"><span data-stu-id="f7d46-183">East US</span></span> | <span data-ttu-id="f7d46-184">Scegliere una località vicina.</span><span class="sxs-lookup"><span data-stu-id="f7d46-184">Choose a location close to you.</span></span> |
    | <span data-ttu-id="f7d46-185">**Gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="f7d46-185">**Resource group**</span></span> | <span data-ttu-id="f7d46-186">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f7d46-186">myResourceGroup</span></span> | <span data-ttu-id="f7d46-187">Scegliere lo stesso gruppo di risorse esistente visto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7d46-187">Choose the same existing resource group as before.</span></span>|

4. <span data-ttu-id="f7d46-188">Fare clic su **Crea** per creare l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="f7d46-188">Click **Create** to create your logic app.</span></span> <span data-ttu-id="f7d46-189">Dopo aver creato l'app, fare clic sulla nuova app per la logica aggiunta al dashboard.</span><span class="sxs-lookup"><span data-stu-id="f7d46-189">After the app is created, click your new logic app pinned to the dashboard.</span></span> <span data-ttu-id="f7d46-190">In Progettazione app per la logica scorrere verso il basso e fare clic sul modello **App per la logica vuota**.</span><span class="sxs-lookup"><span data-stu-id="f7d46-190">Then in the Logic Apps Designer, scroll down and click the **Blank Logic App** template.</span></span> 

    ![Modello App per la logica vuota](media/functions-twitter-email/blank.png)

<span data-ttu-id="f7d46-192">A questo punto è possibile usare Progettazione app per la logica per aggiungere servizi e trigger all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f7d46-192">You can now use the Logic Apps Designer to add services and triggers to your app.</span></span>

## <a name="connect-to-twitter"></a><span data-ttu-id="f7d46-193">Connettersi a Twitter</span><span class="sxs-lookup"><span data-stu-id="f7d46-193">Connect to Twitter</span></span>

<span data-ttu-id="f7d46-194">Creare prima di tutto una connessione all'account Twitter.</span><span class="sxs-lookup"><span data-stu-id="f7d46-194">First, create a connection to your Twitter account.</span></span> <span data-ttu-id="f7d46-195">L'app per la logica esegue il poll dei tweet, che attiva l'app da eseguire.</span><span class="sxs-lookup"><span data-stu-id="f7d46-195">The logic app polls for tweets, which trigger the app to run.</span></span>

1. <span data-ttu-id="f7d46-196">Nella finestra di progettazione, fare clic sul servizio **Twitter** e scegliere il trigger **Quando viene pubblicato un nuovo tweet**.</span><span class="sxs-lookup"><span data-stu-id="f7d46-196">In the designer, click the **Twitter** service, and click the **When a new tweet is posted** trigger.</span></span> <span data-ttu-id="f7d46-197">Accedere all'account Twitter e autorizzare App per la logica all'uso dell'account.</span><span class="sxs-lookup"><span data-stu-id="f7d46-197">Sign in to your Twitter account and authorize Logic Apps to use your account.</span></span>

2. <span data-ttu-id="f7d46-198">Usare le impostazioni del trigger Twitter come specificato nella tabella.</span><span class="sxs-lookup"><span data-stu-id="f7d46-198">Use the Twitter trigger settings as specified in the table.</span></span> 

    ![Impostazioni del connettore Twitter](media/functions-twitter-email/azure_tweet.png)

    | <span data-ttu-id="f7d46-200">Impostazione</span><span class="sxs-lookup"><span data-stu-id="f7d46-200">Setting</span></span>      |  <span data-ttu-id="f7d46-201">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="f7d46-201">Suggested value</span></span>   | <span data-ttu-id="f7d46-202">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7d46-202">Description</span></span>                                        |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="f7d46-203">**Testo di ricerca**</span><span class="sxs-lookup"><span data-stu-id="f7d46-203">**Search text**</span></span> | <span data-ttu-id="f7d46-204">#Azure</span><span class="sxs-lookup"><span data-stu-id="f7d46-204">#Azure</span></span> | <span data-ttu-id="f7d46-205">Usare un hashtag che sia abbastanza comune da generare nuovi tweet nell'intervallo selezionato.</span><span class="sxs-lookup"><span data-stu-id="f7d46-205">Use a hashtag that is popular enough for to generate new tweets in the chosen interval.</span></span> <span data-ttu-id="f7d46-206">Quando si usa un hashtag troppo comune con il livello gratuito, c'è il rischio di esaurire rapidamente le transazioni nell'account Servizi cognitivi.</span><span class="sxs-lookup"><span data-stu-id="f7d46-206">When using the Free tier and your hashtag is too popular, you can quickly use up the transactions in your Cognitive Services account.</span></span> |
    | <span data-ttu-id="f7d46-207">**Frequenza**</span><span class="sxs-lookup"><span data-stu-id="f7d46-207">**Frequency**</span></span> | <span data-ttu-id="f7d46-208">Minuto</span><span class="sxs-lookup"><span data-stu-id="f7d46-208">Minute</span></span> | <span data-ttu-id="f7d46-209">Unità di frequenza usata per eseguire il poll di Twitter.</span><span class="sxs-lookup"><span data-stu-id="f7d46-209">The frequency unit used for polling Twitter.</span></span>  |
    | <span data-ttu-id="f7d46-210">**Interval**</span><span class="sxs-lookup"><span data-stu-id="f7d46-210">**Interval**</span></span> | <span data-ttu-id="f7d46-211">15</span><span class="sxs-lookup"><span data-stu-id="f7d46-211">15</span></span> | <span data-ttu-id="f7d46-212">Tempo trascorso tra le richieste di Twitter, in unità di frequenza.</span><span class="sxs-lookup"><span data-stu-id="f7d46-212">The time elapsed between Twitter requests, in frequency units.</span></span> |

3.  <span data-ttu-id="f7d46-213">Fare clic su **Salva** per connettersi all'account Twitter.</span><span class="sxs-lookup"><span data-stu-id="f7d46-213">Click **Save** to connect to your Twitter account.</span></span> 

<span data-ttu-id="f7d46-214">A questo punto l'app è connessa a Twitter.</span><span class="sxs-lookup"><span data-stu-id="f7d46-214">Now your app is connected to Twitter.</span></span> <span data-ttu-id="f7d46-215">Connettersi ora all'analisi del testo per rilevare il sentiment dei tweet raccolti.</span><span class="sxs-lookup"><span data-stu-id="f7d46-215">Next, you connect to text analytics to detect the sentiment of collected tweets.</span></span>

## <a name="add-sentiment-detection"></a><span data-ttu-id="f7d46-216">Aggiungere il rilevamento dei sentiment</span><span class="sxs-lookup"><span data-stu-id="f7d46-216">Add sentiment detection</span></span>

1. <span data-ttu-id="f7d46-217">Selezionare **Nuovo passaggio** e quindi **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="f7d46-217">Click **New Step**, and then **Add an action**.</span></span>

    ![Nuovo passaggio e quindi Aggiungi un'azione.](media/functions-twitter-email/new_step.png)

2. <span data-ttu-id="f7d46-219">In **Scegliere un'azione** fare clic su **Analisi del testo** e quindi scegliere l'azione **Detect sentiment** (Rileva sentiment).</span><span class="sxs-lookup"><span data-stu-id="f7d46-219">In **Choose an action**, click **Text Analytics**, and then click the **Detect sentiment** action.</span></span>

    ![Rileva sentiment](media/functions-twitter-email/detect_sent.png)

3. <span data-ttu-id="f7d46-221">Digitare un nome per la connessione, ad esempio `MyCognitiveServicesConnection`, incollare la chiave dell'account Servizi cognitivi salvata in precedenza e fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="f7d46-221">Type a connection name such as `MyCognitiveServicesConnection`, paste the key for your Cognitive Services account that you saved, and click **Create**.</span></span>  

4. <span data-ttu-id="f7d46-222">Fare clic su **Text to analyze** (Testo da analizzare) > **Testo tweet** e quindi fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="f7d46-222">Click **Text to analyze** > **Tweet text**, and then click **Save**.</span></span>  

    ![Rileva sentiment](media/functions-twitter-email/ds_tta.png)

<span data-ttu-id="f7d46-224">Dopo aver configurato il rilevamento dei sentiment, è possibile aggiungere una connessione alla funzione che utilizza l'output del punteggio dei sentiment.</span><span class="sxs-lookup"><span data-stu-id="f7d46-224">Now that sentiment detection is configured, you can add a connection to your function that consumes the sentiment score output.</span></span>

## <a name="connect-sentiment-output-to-your-function"></a><span data-ttu-id="f7d46-225">Connettere l'output dei sentiment alla funzione</span><span class="sxs-lookup"><span data-stu-id="f7d46-225">Connect sentiment output to your function</span></span>

1. <span data-ttu-id="f7d46-226">In Progettazione app per la logica fare clic su **Nuovo passaggio** > **Aggiungi un'azione** e quindi scegliere **Funzioni di Azure**.</span><span class="sxs-lookup"><span data-stu-id="f7d46-226">In the Logic Apps Designer, click **New step** > **Add an action**, and then click **Azure Functions**.</span></span> 

2. <span data-ttu-id="f7d46-227">Fare clic su **Scegliere una funzione di Azure** e selezionare la funzione **CategorizeSentiment** creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f7d46-227">Click **Choose an Azure function**, select the **CategorizeSentiment** function you created earlier.</span></span>  

    ![Casella Funzione Azure con Scegliere una funzione di Azure](media/functions-twitter-email/choose_fun.png)

3. <span data-ttu-id="f7d46-229">In **Corpo della richiesta** fare clic su **Punteggio** e quindi su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="f7d46-229">In **Request Body**, click **Score** and then **Save**.</span></span>

    ![Score](media/functions-twitter-email/trigger_score.png)

<span data-ttu-id="f7d46-231">A questo punto, la funzione viene attivata quando l'app per la logica invia un punteggio di sentiment.</span><span class="sxs-lookup"><span data-stu-id="f7d46-231">Now, your function is triggered when a sentiment score is sent from the logic app.</span></span> <span data-ttu-id="f7d46-232">La funzione restituisce quindi una categoria colore all'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="f7d46-232">A color-coded category is returned to the logic app by the function.</span></span> <span data-ttu-id="f7d46-233">Aggiungere quindi l'invio di una notifica di posta elettronica quando la funzione restituisce un valore di sentiment **RED**.</span><span class="sxs-lookup"><span data-stu-id="f7d46-233">Next, you add an email notification that is sent when a sentiment value of **RED** is returned from the function.</span></span> 

## <a name="add-email-notifications"></a><span data-ttu-id="f7d46-234">Aggiungere le notifiche di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="f7d46-234">Add email notifications</span></span>

<span data-ttu-id="f7d46-235">L'ultima parte del flusso di lavoro consiste nell'attivare l'invio di un messaggio di posta elettronica quando il punteggio del sentiment è _RED_.</span><span class="sxs-lookup"><span data-stu-id="f7d46-235">The last part of the workflow is to trigger an email when the sentiment is scored as _RED_.</span></span> <span data-ttu-id="f7d46-236">Questo argomento fa uso di un connettore Outlook.com.</span><span class="sxs-lookup"><span data-stu-id="f7d46-236">This topic uses an Outlook.com connector.</span></span> <span data-ttu-id="f7d46-237">Per usare un connettore Gmail o Office 365 Outlook è possibile seguire una procedura simile.</span><span class="sxs-lookup"><span data-stu-id="f7d46-237">You can perform similar steps to use a Gmail or Office 365 Outlook connector.</span></span>   

1. <span data-ttu-id="f7d46-238">In Progettazione app per la logica fare clic su **Nuovo passaggio** > **Aggiungi una condizione**.</span><span class="sxs-lookup"><span data-stu-id="f7d46-238">In the Logic Apps Designer, click **New step** > **Add a condition**.</span></span> 

2. <span data-ttu-id="f7d46-239">Fare clic su **Scegliere un valore** e quindi su **Corpo**.</span><span class="sxs-lookup"><span data-stu-id="f7d46-239">Click **Choose a value**, then click **Body**.</span></span> <span data-ttu-id="f7d46-240">Selezionare **è uguale a**, fare clic su **Scegliere un valore**, digitare `RED` e quindi fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="f7d46-240">Select **is equal to**, click **Choose a value** and type `RED`, and click **Save**.</span></span> 

    ![Aggiungere una condizione all'app per la logica.](media/functions-twitter-email/condition.png)

3. <span data-ttu-id="f7d46-242">In **Se sì, non fare nulla** fare clic su **Aggiungi un'azione**, cercare `outlook.com`, fare clic su **Invia un messaggio di posta elettronica** e accedere all'account Outlook.com.</span><span class="sxs-lookup"><span data-stu-id="f7d46-242">In **IF YES, DO NOTHING**, click **Add an action**, search for `outlook.com`, click **Send an email**, and sign in to your Outlook.com account.</span></span>
    
    ![Scegliere un'azione per la condizione.](media/functions-twitter-email/outlook.png)

    > [!NOTE]
    > <span data-ttu-id="f7d46-244">Se non è disponibile un account Outlook.com, è possibile scegliere un altro connettore, ad esempio Gmail o Office 365 Outlook.</span><span class="sxs-lookup"><span data-stu-id="f7d46-244">If you don't have an Outlook.com account, you can choose another connector, such as Gmail or Office 365 Outlook</span></span>

4. <span data-ttu-id="f7d46-245">Nell'azione **Invia un messaggio di posta elettronica** usare le impostazioni di posta elettronica indicate nella tabella.</span><span class="sxs-lookup"><span data-stu-id="f7d46-245">In the **Send an email** action, use the email settings as specified in the table.</span></span> 

    ![Configurare la posta elettronica per l'azione Invia un messaggio di posta elettronica.](media/functions-twitter-email/sendemail.png)

    | <span data-ttu-id="f7d46-247">Impostazione</span><span class="sxs-lookup"><span data-stu-id="f7d46-247">Setting</span></span>      |  <span data-ttu-id="f7d46-248">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="f7d46-248">Suggested value</span></span>   | <span data-ttu-id="f7d46-249">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f7d46-249">Description</span></span>  |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="f7d46-250">**To**</span><span class="sxs-lookup"><span data-stu-id="f7d46-250">**To**</span></span> | <span data-ttu-id="f7d46-251">Digitare l'indirizzo di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="f7d46-251">Type your email address</span></span> | <span data-ttu-id="f7d46-252">Indirizzo di posta elettronica che riceve la notifica.</span><span class="sxs-lookup"><span data-stu-id="f7d46-252">The email address that receives the notification.</span></span> |
    | <span data-ttu-id="f7d46-253">**Oggetto**</span><span class="sxs-lookup"><span data-stu-id="f7d46-253">**Subject**</span></span> | <span data-ttu-id="f7d46-254">Rilevato sentiment di tweet negativo</span><span class="sxs-lookup"><span data-stu-id="f7d46-254">Negative tweet sentiment detected</span></span>  | <span data-ttu-id="f7d46-255">Riga dell'oggetto della notifica di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="f7d46-255">The subject line of the email notification.</span></span>  |
    | <span data-ttu-id="f7d46-256">**Corpo**</span><span class="sxs-lookup"><span data-stu-id="f7d46-256">**Body**</span></span> | <span data-ttu-id="f7d46-257">Testo tweet, Località</span><span class="sxs-lookup"><span data-stu-id="f7d46-257">Tweet text, Location</span></span> | <span data-ttu-id="f7d46-258">Fare clic sui parametri **Testo tweet** e **Località**.</span><span class="sxs-lookup"><span data-stu-id="f7d46-258">Click the **Tweet text** and **Location** parameters.</span></span> |

5.  <span data-ttu-id="f7d46-259">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="f7d46-259">Click **Save**.</span></span>

<span data-ttu-id="f7d46-260">Ora che il flusso di lavoro è completo, è possibile abilitare l'app per la logica e provarne il funzionamento.</span><span class="sxs-lookup"><span data-stu-id="f7d46-260">Now that the workflow is complete, you can enable the logic app and see the function at work.</span></span>

## <a name="test-the-workflow"></a><span data-ttu-id="f7d46-261">Testare il flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="f7d46-261">Test the workflow</span></span>

1. <span data-ttu-id="f7d46-262">In Progettazione app per la logica fare clic su **Esegui** per avviare l'app.</span><span class="sxs-lookup"><span data-stu-id="f7d46-262">In the Logic App Designer, click **Run** to start the app.</span></span>

2. <span data-ttu-id="f7d46-263">Nella colonna di sinistra fare clic su **Panoramica** per visualizzare lo stato dell'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="f7d46-263">In the left column, click **Overview** to see the status of the logic app.</span></span> 
 
    ![Stato di esecuzione dell'app per la logica](media/functions-twitter-email/over1.png)

3. <span data-ttu-id="f7d46-265">(Facoltativo) Fare clic su una delle esecuzioni per visualizzarne i dettagli.</span><span class="sxs-lookup"><span data-stu-id="f7d46-265">(Optional) Click one of the runs to see details of the execution.</span></span>

4. <span data-ttu-id="f7d46-266">Passare alla funzione, visualizzare i log e verificare che i valori dei sentiment siano stati ricevuti ed elaborati.</span><span class="sxs-lookup"><span data-stu-id="f7d46-266">Go to your function, view the logs, and verify that sentiment values were received and processed.</span></span>
 
    ![Visualizzare i log della funzione](media/functions-twitter-email/sent.png)

5. <span data-ttu-id="f7d46-268">Quando viene rilevato un sentiment potenzialmente negativo, si riceve un messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="f7d46-268">When a potentially negative sentiment is detected, you receive an email.</span></span> <span data-ttu-id="f7d46-269">Se non è stato ricevuto un messaggio di posta elettronica, è possibile modificare il codice della funzione per restituisca RED ogni volta:</span><span class="sxs-lookup"><span data-stu-id="f7d46-269">If you haven't received an email, you can change the function code to return RED every time:</span></span>

        return req.CreateResponse(HttpStatusCode.OK, "RED");

    <span data-ttu-id="f7d46-270">Dopo aver verificato le notifiche di posta elettronica, ripristinare il codice originale:</span><span class="sxs-lookup"><span data-stu-id="f7d46-270">After you have verified email notifications, change back to the original code:</span></span>

        return req.CreateResponse(HttpStatusCode.OK, category);

    > [!IMPORTANT]
    > <span data-ttu-id="f7d46-271">Al termine di questa esercitazione è consigliabile disabilitare l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="f7d46-271">After you have completed this tutorial, you should disable the logic app.</span></span> <span data-ttu-id="f7d46-272">In questo modo è possibile evitare di incorrere in addebiti per le esecuzioni e di esaurire le transazioni nell'account Servizi cognitivi.</span><span class="sxs-lookup"><span data-stu-id="f7d46-272">By disabling the app, you avoid being charged for executions and using up the transactions in your Cognitive Services account.</span></span>

<span data-ttu-id="f7d46-273">Come illustrato in questa esercitazione, integrare Funzioni in un flusso di lavoro di App per la logica è molto semplice.</span><span class="sxs-lookup"><span data-stu-id="f7d46-273">Now you have seen how easy it is to integrate Functions into a Logic Apps workflow.</span></span>

## <a name="disable-the-logic-app"></a><span data-ttu-id="f7d46-274">Disabilitare l'app per la logica</span><span class="sxs-lookup"><span data-stu-id="f7d46-274">Disable the logic app</span></span>

<span data-ttu-id="f7d46-275">Per disabilitare l'app per la logica, fare clic su **Panoramica** e quindi scegliere **Disabilita** nella parte superiore della schermata.</span><span class="sxs-lookup"><span data-stu-id="f7d46-275">To disable the logic app, click **Overview** and then click **Disable** at the top of the screen.</span></span> <span data-ttu-id="f7d46-276">Questo arresta l'esecuzione dell'app per la logica e permette di evitare addebiti per non aver eliminato l'app.</span><span class="sxs-lookup"><span data-stu-id="f7d46-276">This stops the logic app from running and incurring charges without deleting the app.</span></span> 

![Log della funzione](media/functions-twitter-email/disable-logic-app.png)

## <a name="next-steps"></a><span data-ttu-id="f7d46-278">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f7d46-278">Next steps</span></span>

<span data-ttu-id="f7d46-279">In questa esercitazione si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="f7d46-279">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f7d46-280">Creare un account di Servizi cognitivi.</span><span class="sxs-lookup"><span data-stu-id="f7d46-280">Create a Cognitive Services account.</span></span>
> * <span data-ttu-id="f7d46-281">Creare una funzione che classifica i sentiment nei tweet.</span><span class="sxs-lookup"><span data-stu-id="f7d46-281">Create a function that categorizes tweet sentiment.</span></span>
> * <span data-ttu-id="f7d46-282">Creare un'app per la logica che si connette a Twitter.</span><span class="sxs-lookup"><span data-stu-id="f7d46-282">Create a logic app that connects to Twitter.</span></span>
> * <span data-ttu-id="f7d46-283">Aggiungere il rilevamento dei sentiment all'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="f7d46-283">Add sentiment detection to the logic app.</span></span> 
> * <span data-ttu-id="f7d46-284">Connettere l'app per la logica alla funzione.</span><span class="sxs-lookup"><span data-stu-id="f7d46-284">Connect the logic app to the function.</span></span>
> * <span data-ttu-id="f7d46-285">Inviare un messaggio di posta elettronica in base alla risposta dalla funzione.</span><span class="sxs-lookup"><span data-stu-id="f7d46-285">Send an email based on the response from the function.</span></span>

<span data-ttu-id="f7d46-286">Passare all'esercitazione successiva per imparare a creare un'API senza server per la funzione.</span><span class="sxs-lookup"><span data-stu-id="f7d46-286">Advance to the next tutorial to learn how to create a serverless API for your function.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="f7d46-287">Creare un'API senza server mediante Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="f7d46-287">Create a serverless API using Azure Functions</span></span>](functions-create-serverless-api.md)

<span data-ttu-id="f7d46-288">Per altre informazioni sulle app per la logica, vedere [App per la logica di Azure](../logic-apps/logic-apps-what-are-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="f7d46-288">To learn more about Logic Apps, see [Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md).</span></span>

