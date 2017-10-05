---
title: Analisi del sentiment su Twitter in tempo reale con Analisi di flusso di Azure | Microsoft Docs
description: Informazioni sull'uso di Analisi di flusso per l'analisi del sentiment su Twitter in tempo reale. Istruzioni dettagliate, dalla generazione degli eventi fino ai dati in un dashboard in tempo reale.
keywords: analisi delle tendenze twitter in tempo reale, analisi del sentiment, analisi dei social media, esempio di analisi delle tendenze
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 42068691-074b-4c3b-a527-acafa484fda2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: jeffstok
ms.openlocfilehash: 8de6850964700f5b3f71d144b40af927f2e52d7e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="real-time-twitter-sentiment-analysis-in-azure-stream-analytics"></a><span data-ttu-id="c0be8-105">Analisi del sentiment su Twitter in tempo reale in Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="c0be8-105">Real-time Twitter sentiment analysis in Azure Stream Analytics</span></span>

<span data-ttu-id="c0be8-106">Si imparerà a creare una soluzione di analisi del sentiment per i social media portando gli eventi di Twitter in tempo reale negli hub eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="c0be8-106">Learn how to build a sentiment analysis solution for social media analytics by bringing real-time Twitter events into Azure Event Hubs.</span></span> <span data-ttu-id="c0be8-107">Si potrà quindi scrivere una query di Analisi di flusso di Azure per analizzare i dati e archiviare i risultati per analisi successive o usare un dashboard e [Power BI](https://powerbi.com/) per rendere disponibili informazioni rilevanti in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="c0be8-107">You can then write an Azure Stream Analytics query to analyze the data and either store the results for later use or use a dashboard and [Power BI](https://powerbi.com/) to provide insights in real time.</span></span>

<span data-ttu-id="c0be8-108">Gli strumenti di analisi dei social media permettono alle organizzazioni di determinare gli argomenti di tendenza,</span><span class="sxs-lookup"><span data-stu-id="c0be8-108">Social media analytics tools help organizations understand trending topics.</span></span> <span data-ttu-id="c0be8-109">vale a dire gli argomenti e gli atteggiamenti che registrano un numero elevato di post nei social media.</span><span class="sxs-lookup"><span data-stu-id="c0be8-109">Trending topics are subjects and attitudes that have a high volume of posts in social media.</span></span> <span data-ttu-id="c0be8-110">L'analisi del sentiment, detta anche *opinion mining*, usa gli strumenti di analisi dei social media per determinare le attitudini rispetto a un prodotto, un'idea e così via.</span><span class="sxs-lookup"><span data-stu-id="c0be8-110">Sentiment analysis, which is also called *opinion mining*, uses social media analytics tools to determine attitudes toward a product, idea, and so on.</span></span> 

<span data-ttu-id="c0be8-111">L'analisi delle tendenze Twitter in tempo reale offre un ottimo esempio di strumento di analisi, perché il modello di sottoscrizione hashtag consente di ascoltare parole chiave specifiche (hashtag) e sviluppare l'analisi del sentiment del feed.</span><span class="sxs-lookup"><span data-stu-id="c0be8-111">Real-time Twitter trend analysis is a great example of an analytics tool, because the hashtag subscription model enables you to listen to specific keywords (hashtags) and develop sentiment analysis of the feed.</span></span>

## <a name="scenario-social-media-sentiment-analysis-in-real-time"></a><span data-ttu-id="c0be8-112">Scenario: analisi del sentiment su social media in tempo reale</span><span class="sxs-lookup"><span data-stu-id="c0be8-112">Scenario: Social media sentiment analysis in real time</span></span>

<span data-ttu-id="c0be8-113">Una società con un sito Web di notizie è interessata a superare la concorrenza offrendo contenuti del sito immediatamente fruibili per i lettori.</span><span class="sxs-lookup"><span data-stu-id="c0be8-113">A company that has a news media website is interested in gaining an advantage over its competitors by featuring site content that is immediately relevant to its readers.</span></span> <span data-ttu-id="c0be8-114">La società usa l'analisi dei social media su argomenti rilevanti per i lettori eseguendo l'analisi del sentiment in tempo reale sui dati di Twitter.</span><span class="sxs-lookup"><span data-stu-id="c0be8-114">The company uses social media analysis on topics that are relevant to readers by doing real-time sentiment analysis of Twitter data.</span></span>

<span data-ttu-id="c0be8-115">Per identificare in tempo reale gli argomenti di tendenza su Twitter, la società deve eseguire un'analisi in tempo reale sul volume dei tweet e sul sentiment relativo agli argomenti più importanti.</span><span class="sxs-lookup"><span data-stu-id="c0be8-115">To identify trending topics in real time on Twitter, the company needs real-time analytics about the tweet volume and sentiment for key topics.</span></span> <span data-ttu-id="c0be8-116">In altre parole, ciò che serve è un motore di analisi del sentiment basato su questo feed di social media.</span><span class="sxs-lookup"><span data-stu-id="c0be8-116">In other words, the need is a sentiment analysis analytics engine that's based on this social media feed.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c0be8-117">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c0be8-117">Prerequisites</span></span>
<span data-ttu-id="c0be8-118">In questa esercitazione si usa un'applicazione client che si connette a Twitter e cerca i tweet con determinati hashtag, che è possibile impostare.</span><span class="sxs-lookup"><span data-stu-id="c0be8-118">In this tutorial, you use a client application that connects to Twitter and looks for tweets that have certain hashtags (which you can set).</span></span> <span data-ttu-id="c0be8-119">Per eseguire l'applicazione e analizzare i tweet tramite Analisi di flusso di Azure, è necessario quanto segue:</span><span class="sxs-lookup"><span data-stu-id="c0be8-119">In order to run the application and analyze the tweets using Azure Streaming Analytics, you must have the following:</span></span>

* <span data-ttu-id="c0be8-120">Una sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="c0be8-120">An Azure subscription</span></span>
* <span data-ttu-id="c0be8-121">Un account Twitter</span><span class="sxs-lookup"><span data-stu-id="c0be8-121">A Twitter account</span></span> 
* <span data-ttu-id="c0be8-122">Un'applicazione Twitter e il [token di accesso OAuth](https://dev.twitter.com/oauth/overview/application-owner-access-tokens) per tale applicazione.</span><span class="sxs-lookup"><span data-stu-id="c0be8-122">A Twitter application, and the [OAuth access token](https://dev.twitter.com/oauth/overview/application-owner-access-tokens) for that application.</span></span> <span data-ttu-id="c0be8-123">Più avanti sono riportate istruzioni dettagliate per creare un'applicazione Twitter.</span><span class="sxs-lookup"><span data-stu-id="c0be8-123">We provide high-level instructions for how to create a Twitter application later.</span></span>
* <span data-ttu-id="c0be8-124">L'applicazione TwitterWPFClient, che legge il feed di Twitter.</span><span class="sxs-lookup"><span data-stu-id="c0be8-124">The TwitterWPFClient application, which reads the Twitter feed.</span></span> <span data-ttu-id="c0be8-125">Per ottenere questa applicazione, scaricare il file [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) da GitHub e decomprimere il pacchetto in una cartella nel computer.</span><span class="sxs-lookup"><span data-stu-id="c0be8-125">To get this application, download the [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) file from GitHub and then unzip the package into a folder on your computer.</span></span> <span data-ttu-id="c0be8-126">Per visualizzare il codice sorgente ed eseguire l'applicazione in un debugger, è possibile ottenere il codice sorgente da [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator).</span><span class="sxs-lookup"><span data-stu-id="c0be8-126">If you want to see the source code and run the application in a debugger, you can get the source code from [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator).</span></span> 

## <a name="create-an-event-hub-for-streaming-analytics-input"></a><span data-ttu-id="c0be8-127">Creare un hub eventi per l'input di Analisi di flusso</span><span class="sxs-lookup"><span data-stu-id="c0be8-127">Create an event hub for Streaming Analytics input</span></span>

<span data-ttu-id="c0be8-128">L'applicazione di esempio genera eventi e ne esegue il push a un hub eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="c0be8-128">The sample application generates events and pushes them to an Azure event hub.</span></span> <span data-ttu-id="c0be8-129">Gli hub eventi di Azure sono la soluzione preferita per l'inserimento di eventi per Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="c0be8-129">Azure event hubs are the preferred method of event ingestion for Stream Analytics.</span></span> <span data-ttu-id="c0be8-130">Per altre informazioni, vedere la [documentazione di Hub eventi di Azure](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="c0be8-130">For more information, see the [Azure Event Hubs documentation](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>


### <a name="create-an-event-hub-namespace-and-event-hub"></a><span data-ttu-id="c0be8-131">Creare uno spazio dei nomi dell'hub eventi e un hub eventi</span><span class="sxs-lookup"><span data-stu-id="c0be8-131">Create an event hub namespace and event hub</span></span>
<span data-ttu-id="c0be8-132">In questa procedura si creerà uno spazio dei nomi dell'hub eventi e quindi si aggiungerà un hub eventi a tale spazio.</span><span class="sxs-lookup"><span data-stu-id="c0be8-132">In this procedure, you first create an event hub namespace, and then you add an event hub to that namespace.</span></span> <span data-ttu-id="c0be8-133">Gli spazi dei nomi degli hub eventi consentono di raggruppare in modo logico le istanze dei bus di eventi correlate.</span><span class="sxs-lookup"><span data-stu-id="c0be8-133">Event hub namespaces are used to logically group related event bus instances.</span></span> 

1. <span data-ttu-id="c0be8-134">Accedere al portale di Azure e fare clic su **Nuovo** > **Internet delle cose** > **Hub eventi**.</span><span class="sxs-lookup"><span data-stu-id="c0be8-134">Log  in to the Azure portal and click **New** > **Internet of Things** > **Event Hub**.</span></span> 

2. <span data-ttu-id="c0be8-135">Nel pannello **Crea spazio dei nomi** immettere un nome per lo spazio dei nomi, ad esempio `<yourname>-socialtwitter-eh-ns`.</span><span class="sxs-lookup"><span data-stu-id="c0be8-135">In the **Create namespace** blade, enter a namespace name such as `<yourname>-socialtwitter-eh-ns`.</span></span> <span data-ttu-id="c0be8-136">È possibile usare qualsiasi nome per lo spazio dei nomi, a condizione che sia valido per un URL e univoco in Azure.</span><span class="sxs-lookup"><span data-stu-id="c0be8-136">You can use any name for the namespace, but the name must be valid for a URL and it must be unique across Azure.</span></span> 
    
3. <span data-ttu-id="c0be8-137">Selezionare una sottoscrizione, creare o scegliere un gruppo di risorse e quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c0be8-137">Select a subscription and create or choose a resource group, then click **Create**.</span></span> 

    ![Creare uno spazio dei nomi dell'hub eventi](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-namespace.png)
 
4. <span data-ttu-id="c0be8-139">Al termine della distribuzione, lo spazio dei nomi dell'hub eventi è disponibile nell'elenco delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="c0be8-139">When the namespace has finished deploying, find the event hub namespace in your list of Azure resources.</span></span> 

5. <span data-ttu-id="c0be8-140">Scegliere il nuovo spazio dei nomi e, nel relativo pannello, fare clic su  **+&nbsp;Hub eventi**.</span><span class="sxs-lookup"><span data-stu-id="c0be8-140">Click the new namespace, and in the namespace blade, click **+&nbsp;Event Hub**.</span></span> 

    ![<span data-ttu-id="c0be8-141">Pulsante Aggiungi hub eventi per creare un nuovo hub eventi</span><span class="sxs-lookup"><span data-stu-id="c0be8-141">The Add Event Hub button for creating a new event hub</span></span> ](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-button.png)    
 
6. <span data-ttu-id="c0be8-142">Assegnare il nome `socialtwitter-eh` al nuovo hub eventi.</span><span class="sxs-lookup"><span data-stu-id="c0be8-142">Name the new event hub `socialtwitter-eh`.</span></span> <span data-ttu-id="c0be8-143">È possibile usare un nome diverso.</span><span class="sxs-lookup"><span data-stu-id="c0be8-143">You can use a different name.</span></span> <span data-ttu-id="c0be8-144">In questo caso, tenerne traccia, poiché sarà necessario in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="c0be8-144">If you do, make a note of it, because you need the name later.</span></span> <span data-ttu-id="c0be8-145">Non sono richieste altre impostazioni per l'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="c0be8-145">You don't need to set any other options for the event hub.</span></span>

    ![Pannello per creare un nuovo hub eventi](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub.png)
 
7. <span data-ttu-id="c0be8-147">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c0be8-147">Click **Create**.</span></span>


### <a name="grant-access-to-the-event-hub"></a><span data-ttu-id="c0be8-148">Concedere l'accesso all'hub eventi</span><span class="sxs-lookup"><span data-stu-id="c0be8-148">Grant access to the event hub</span></span>

<span data-ttu-id="c0be8-149">Prima che un processo possa inviare dati a un hub eventi, è necessario che per l'hub siano configurati criteri che consentano l'accesso appropriato.</span><span class="sxs-lookup"><span data-stu-id="c0be8-149">Before a process can send data to an event hub, the event hub must have a policy that allows appropriate access.</span></span> <span data-ttu-id="c0be8-150">I criteri di accesso generano una stringa di connessione che include informazioni di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="c0be8-150">The access policy produces a connection string that includes authorization information.</span></span>

1.  <span data-ttu-id="c0be8-151">Nel pannello dello spazio dei nomi dell'evento fare clic su **Hub eventi** e quindi sul nome del nuovo hub eventi.</span><span class="sxs-lookup"><span data-stu-id="c0be8-151">In the event namespace blade, click **Event Hubs** and then click the name of your new event hub.</span></span>

2.  <span data-ttu-id="c0be8-152">Nel pannello dell'hub eventi fare clic su **Criteri di accesso condiviso** e quindi su **+&nbsp;Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c0be8-152">In the event hub blade, click **Shared access policies** and then click **+&nbsp;Add**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="c0be8-153">Verificare di usare l'hub eventi e non lo spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="c0be8-153">Make sure you're working with the event hub, not the event hub namespace.</span></span>

3.  <span data-ttu-id="c0be8-154">Aggiungere criteri denominati `socialtwitter-access` e per **Attestazione** selezionare **Gestisci**.</span><span class="sxs-lookup"><span data-stu-id="c0be8-154">Add a policy named `socialtwitter-access` and for **Claim**, select **Manage**.</span></span>

    ![Pannello per creare nuovi criteri di accesso all'hub eventi](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-shared-access-policy-manage.png)
 
4.  <span data-ttu-id="c0be8-156">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c0be8-156">Click **Create**.</span></span>

5.  <span data-ttu-id="c0be8-157">Dopo aver distribuito i criteri, fare clic nell'elenco dei criteri di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="c0be8-157">After the policy has been deployed, click it in the list of shared access policies.</span></span>

6.  <span data-ttu-id="c0be8-158">Individuare la casella con l'etichetta **CONNECTION STRING-PRIMARY KEY** e fare clic sul pulsante Copia accanto alla stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="c0be8-158">Find the box labeled **CONNECTION STRING-PRIMARY KEY** and click the copy button next to the connection string.</span></span> 
    
    ![Copia della chiave della stringa di connessione primaria dai criteri di accesso](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-shared-access-policy-copy-connection-string.png)
 
7.  <span data-ttu-id="c0be8-160">Incollare la stringa di connessione in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="c0be8-160">Paste the connection string into a text editor.</span></span> <span data-ttu-id="c0be8-161">Sarà necessario usare questa stringa nella sezione successiva, dopo avervi apportato alcune piccole modifiche.</span><span class="sxs-lookup"><span data-stu-id="c0be8-161">You need this connection string for the next section, after you make some small edits to it.</span></span>

    <span data-ttu-id="c0be8-162">La stringa di connessione ha un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="c0be8-162">The connection string looks like this:</span></span>

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=;EntityPath=socialtwitter-eh

    <span data-ttu-id="c0be8-163">Si noti che la stringa di connessione contiene più coppie chiave-valore, separate da punti e virgola: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey` e `EntityPath`.</span><span class="sxs-lookup"><span data-stu-id="c0be8-163">Notice that the connection string contains multiple key-value pairs, separated with semicolons: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, and `EntityPath`.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="c0be8-164">Per sicurezza, le parti della stringa di connessione nell'esempio sono state rimosse.</span><span class="sxs-lookup"><span data-stu-id="c0be8-164">For security, parts of the connection string in the example have been removed.</span></span>

8.  <span data-ttu-id="c0be8-165">Nell'editor di testo rimuovere la coppia `EntityPath` dalla stringa di connessione. Non dimenticare di rimuovere il punto e virgola che la precede.</span><span class="sxs-lookup"><span data-stu-id="c0be8-165">In the text editor, remove the `EntityPath` pair from the connection string (don't forget to remove the semicolon that precedes it).</span></span> <span data-ttu-id="c0be8-166">Al termine dell'operazione, la stringa di connessione ha un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="c0be8-166">When you're done, the connection string looks like this:</span></span>

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=


## <a name="configure-and-start-the-twitter-client-application"></a><span data-ttu-id="c0be8-167">Configurare e avviare l'applicazione client Twitter</span><span class="sxs-lookup"><span data-stu-id="c0be8-167">Configure and start the Twitter client application</span></span>
<span data-ttu-id="c0be8-168">L'applicazione client ottiene gli eventi tweet direttamente da Twitter.</span><span class="sxs-lookup"><span data-stu-id="c0be8-168">The client application gets tweet events directly from Twitter.</span></span> <span data-ttu-id="c0be8-169">A questo scopo, è necessaria l'autorizzazione per chiamare le API di streaming di Twitter.</span><span class="sxs-lookup"><span data-stu-id="c0be8-169">In order to do so, it needs permission to call the Twitter Streaming APIs.</span></span> <span data-ttu-id="c0be8-170">Per configurare questa autorizzazione, si crea un'applicazione in Twitter in modo da generare credenziali univoche, ad esempio un token OAuth.</span><span class="sxs-lookup"><span data-stu-id="c0be8-170">To configure that permission, you create an application in Twitter, which generates unique credentials (such as an OAuth token).</span></span> <span data-ttu-id="c0be8-171">Si può quindi configurare l'applicazione client in modo da usare queste credenziali quando esegue chiamate API.</span><span class="sxs-lookup"><span data-stu-id="c0be8-171">You can then configure the client application to use these credentials when it makes API calls.</span></span> 

### <a name="create-a-twitter-application"></a><span data-ttu-id="c0be8-172">Creare un'applicazione Twitter</span><span class="sxs-lookup"><span data-stu-id="c0be8-172">Create a Twitter application</span></span>
<span data-ttu-id="c0be8-173">Se si ha già un'applicazione Twitter utilizzabile per questa esercitazione, è possibile crearne una.</span><span class="sxs-lookup"><span data-stu-id="c0be8-173">If you do not already have a Twitter application that you can use for this tutorial, you can create one.</span></span> <span data-ttu-id="c0be8-174">È necessario avere già un account Twitter.</span><span class="sxs-lookup"><span data-stu-id="c0be8-174">You must already have a Twitter account.</span></span>

> [!NOTE]
> <span data-ttu-id="c0be8-175">La procedura esatta da seguire in Twitter per creare un'applicazione e ottenere le chiavi, i segreti e il token può cambiare.</span><span class="sxs-lookup"><span data-stu-id="c0be8-175">The exact process in Twitter for creating an application and getting the keys, secrets, and token might change.</span></span> <span data-ttu-id="c0be8-176">Se queste istruzioni non corrispondono alle informazioni visualizzate sul sito di Twitter, consultare la documentazione per sviluppatori di Twitter.</span><span class="sxs-lookup"><span data-stu-id="c0be8-176">If these instructions don't match what you see on the Twitter site, refer to the Twitter developer documentation.</span></span>

1. <span data-ttu-id="c0be8-177">Passare alla [pagina di gestione delle applicazioni Twitter](https://apps.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="c0be8-177">Go to the [Twitter application management page](https://apps.twitter.com/).</span></span> 

2. <span data-ttu-id="c0be8-178">Creare una nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="c0be8-178">Create a new application.</span></span> 

    * <span data-ttu-id="c0be8-179">Per l'URL del sito Web, specificare un URL valido.</span><span class="sxs-lookup"><span data-stu-id="c0be8-179">For the website URL, specify a valid URL.</span></span> <span data-ttu-id="c0be8-180">Non è necessario che corrisponda a un sito live,</span><span class="sxs-lookup"><span data-stu-id="c0be8-180">It does not have to be a live site.</span></span> <span data-ttu-id="c0be8-181">ma non è possibile specificare semplicemente `localhost`.</span><span class="sxs-lookup"><span data-stu-id="c0be8-181">(You can't specify just `localhost`.)</span></span>
    * <span data-ttu-id="c0be8-182">Lasciare vuoto il campo relativo al callback.</span><span class="sxs-lookup"><span data-stu-id="c0be8-182">Leave the callback field blank.</span></span> <span data-ttu-id="c0be8-183">L'applicazione client usata per questa esercitazione non richiede callback.</span><span class="sxs-lookup"><span data-stu-id="c0be8-183">The client application you use for this tutorial doesn't require callbacks.</span></span>

    ![Creazione di un'applicazione in Twitter](./media/stream-analytics-twitter-sentiment-analysis-trends/create-twitter-application.png)

3. <span data-ttu-id="c0be8-185">Facoltativamente, modificare le autorizzazioni dell'applicazione impostandole in sola lettura.</span><span class="sxs-lookup"><span data-stu-id="c0be8-185">Optionally, change the application's permissions to read-only.</span></span>

4. <span data-ttu-id="c0be8-186">Una volta creata l'applicazione, accedere alla pagina **Keys and Access Tokens** (Chiavi e token di accesso).</span><span class="sxs-lookup"><span data-stu-id="c0be8-186">When the application is created, go to the **Keys and Access Tokens** page.</span></span>

5. <span data-ttu-id="c0be8-187">Fare clic sul pulsante per generare un token di accesso e un segreto del token.</span><span class="sxs-lookup"><span data-stu-id="c0be8-187">Click the button to generate an access token and access token secret.</span></span>

<span data-ttu-id="c0be8-188">Tenere queste informazioni a portata di mano perché saranno necessarie nella procedura successiva.</span><span class="sxs-lookup"><span data-stu-id="c0be8-188">Keep this information handy, because you will need it in the next procedure.</span></span>

>[!NOTE]
><span data-ttu-id="c0be8-189">Le chiavi e i segreti dell'applicazione Twitter consentono l'accesso all'account Twitter personale.</span><span class="sxs-lookup"><span data-stu-id="c0be8-189">The keys and secrets for the Twitter application provide access to your Twitter account.</span></span> <span data-ttu-id="c0be8-190">Trattarle come dati sensibili, allo stesso modo della password di Twitter.</span><span class="sxs-lookup"><span data-stu-id="c0be8-190">Treat this information as sensitive, the same as you do your Twitter password.</span></span> <span data-ttu-id="c0be8-191">Evitare, ad esempio, di incorporare queste informazioni in un'applicazione che si prevede di distribuire ad altri utenti.</span><span class="sxs-lookup"><span data-stu-id="c0be8-191">For example, don't embed this information in an application that you give to others.</span></span> 


### <a name="configure-the-client-application"></a><span data-ttu-id="c0be8-192">Configurare l'applicazione client</span><span class="sxs-lookup"><span data-stu-id="c0be8-192">Configure the client application</span></span>
<span data-ttu-id="c0be8-193">È stata creata un'applicazione client che si connette ai dati di Twitter usando le [API di streaming di Twitter](https://dev.twitter.com/streaming/overview) per raccogliere gli eventi tweet relativi a un set specifico di argomenti.</span><span class="sxs-lookup"><span data-stu-id="c0be8-193">We've created a client application that connects to Twitter data using [Twitter's Streaming APIs](https://dev.twitter.com/streaming/overview) to collect tweet events about a specific set of topics.</span></span> <span data-ttu-id="c0be8-194">L'applicazione usa lo strumento open source [Sentiment140](http://help.sentiment140.com/) che assegna il valore di sentiment seguente a ogni tweet:</span><span class="sxs-lookup"><span data-stu-id="c0be8-194">The application uses the [Sentiment140](http://help.sentiment140.com/) open source tool, which assigns the following sentiment value to each tweet:</span></span>

* <span data-ttu-id="c0be8-195">0 = negativo</span><span class="sxs-lookup"><span data-stu-id="c0be8-195">0 = negative</span></span>
* <span data-ttu-id="c0be8-196">2 = neutrale</span><span class="sxs-lookup"><span data-stu-id="c0be8-196">2 = neutral</span></span>
* <span data-ttu-id="c0be8-197">4 = positivo</span><span class="sxs-lookup"><span data-stu-id="c0be8-197">4 = positive</span></span>

<span data-ttu-id="c0be8-198">Dopo l'assegnazione di un valore di sentiment, gli eventi tweet vengono inviati tramite push all'hub eventi creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c0be8-198">After the tweet events have been assigned a sentiment value, they are pushed to the event hub that you created earlier.</span></span>

<span data-ttu-id="c0be8-199">Prima di essere eseguita, l'applicazione richiede all'utente determinate informazioni, ad esempio le chiavi di Twitter e la stringa di connessione all'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="c0be8-199">Before the application runs, it requires certain information from you, like the Twitter keys and the event hub connection string.</span></span> <span data-ttu-id="c0be8-200">È possibile specificare le informazioni di configurazione nei modi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c0be8-200">You can provide the configuration information in these ways:</span></span>

* <span data-ttu-id="c0be8-201">Eseguire l'applicazione e quindi usare l'interfaccia utente dell'applicazione per immettere le chiavi, i segreti e stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="c0be8-201">Run the application, and then use the application's UI to enter the keys, secrets, and connection string.</span></span> <span data-ttu-id="c0be8-202">In questo caso, le informazioni di configurazione vengono usate per la sessione corrente, ma non vengono salvate.</span><span class="sxs-lookup"><span data-stu-id="c0be8-202">If you do this, the configuration information is used for your current session, but it isn't saved.</span></span>
* <span data-ttu-id="c0be8-203">Modificare il file config dell'applicazione e impostare i valori in tale file.</span><span class="sxs-lookup"><span data-stu-id="c0be8-203">Edit the application's .config file and set the values there.</span></span> <span data-ttu-id="c0be8-204">Questo approccio consente di salvare in modo permanente le informazioni di configurazione, ma questo significa anche che informazioni potenzialmente riservate vengono archiviate in testo normale nel computer.</span><span class="sxs-lookup"><span data-stu-id="c0be8-204">This approach persists the configuration information, but it also means that this potentially sensitive information is stored in plain text on your computer.</span></span>

<span data-ttu-id="c0be8-205">La procedura seguente illustra entrambi gli approcci.</span><span class="sxs-lookup"><span data-stu-id="c0be8-205">The following procedure documents both approaches.</span></span> 

1. <span data-ttu-id="c0be8-206">Verificare di aver scaricato e decompresso il file dell'applicazione [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip), come indicato nei prerequisiti.</span><span class="sxs-lookup"><span data-stu-id="c0be8-206">Make sure you've downloaded and unzipped the [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) application, as listed in the prerequisites.</span></span>

2. <span data-ttu-id="c0be8-207">Per impostare i valori in fase di esecuzione (e solo per la sessione corrente), eseguire l'applicazione `TwitterWPFClient.exe`.</span><span class="sxs-lookup"><span data-stu-id="c0be8-207">To set the values at run time (and only for the current session), run the `TwitterWPFClient.exe` application.</span></span> <span data-ttu-id="c0be8-208">Quando richiesto dall'applicazione, immettere i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="c0be8-208">When the application prompts you, enter the following values:</span></span>

    * <span data-ttu-id="c0be8-209">La chiave utente di Twitter (chiave API).</span><span class="sxs-lookup"><span data-stu-id="c0be8-209">The Twitter Consumer Key (API Key).</span></span>
    * <span data-ttu-id="c0be8-210">Il segreto utente di Twitter (segreto API).</span><span class="sxs-lookup"><span data-stu-id="c0be8-210">The Twitter Consumer Secret (API Secret).</span></span>
    * <span data-ttu-id="c0be8-211">Il token di accesso di Twitter.</span><span class="sxs-lookup"><span data-stu-id="c0be8-211">The Twitter Access Token.</span></span>
    * <span data-ttu-id="c0be8-212">Il segreto del token di accesso di Twitter.</span><span class="sxs-lookup"><span data-stu-id="c0be8-212">The Twitter Access Token Secret.</span></span>
    * <span data-ttu-id="c0be8-213">Le informazioni della stringa di connessione salvate in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c0be8-213">The connection string information that you saved earlier.</span></span> <span data-ttu-id="c0be8-214">Verificare di usare la stringa di connessione da cui è stata rimossa la coppia chiave-valore `EntityPath`.</span><span class="sxs-lookup"><span data-stu-id="c0be8-214">Make sure that you use the connection string that you removed the `EntityPath` key-value pair from.</span></span>
    * <span data-ttu-id="c0be8-215">Le parole chiave di Twitter per cui si vuole determinare il sentiment.</span><span class="sxs-lookup"><span data-stu-id="c0be8-215">The Twitter keywords that you want to determine sentiment for.</span></span>

   ![Applicazione TwitterWpfClient in esecuzione, con le impostazioni oscurate](./media/stream-analytics-twitter-sentiment-analysis-trends/wpfclientlines.png)

3. <span data-ttu-id="c0be8-217">Per impostare i valori in modo permanente, usare un editor di testo per aprire il file TwitterWpfClient.exe.config.</span><span class="sxs-lookup"><span data-stu-id="c0be8-217">To set the values persistently, use a text editor to open the TwitterWpfClient.exe.config file.</span></span> <span data-ttu-id="c0be8-218">Nell'elemento `<appSettings>` definire le impostazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="c0be8-218">Then in the `<appSettings>` element, do this:</span></span>

    * <span data-ttu-id="c0be8-219">Per `oauth_consumer_key` impostare la chiave utente di Twitter (chiave API).</span><span class="sxs-lookup"><span data-stu-id="c0be8-219">Set `oauth_consumer_key` to the Twitter Consumer Key (API Key).</span></span> 
    * <span data-ttu-id="c0be8-220">Per `oauth_consumer_secret` impostare il segreto utente di Twitter (segreto API).</span><span class="sxs-lookup"><span data-stu-id="c0be8-220">Set `oauth_consumer_secret` to the Twitter Consumer Secret (API Secret).</span></span>
    * <span data-ttu-id="c0be8-221">Per `oauth_token` impostare il token di accesso di Twitter.</span><span class="sxs-lookup"><span data-stu-id="c0be8-221">Set `oauth_token` to the Twitter Access Token.</span></span>
    * <span data-ttu-id="c0be8-222">Per `oauth_token_secret` impostare il segreto del token di accesso di Twitter.</span><span class="sxs-lookup"><span data-stu-id="c0be8-222">Set `oauth_token_secret` to the Twitter Access Token Secret.</span></span>

    <span data-ttu-id="c0be8-223">Più avanti, nell'elemento `<appSettings>`, apportare queste modifiche:</span><span class="sxs-lookup"><span data-stu-id="c0be8-223">Later in the `<appSettings>` element, make these changes:</span></span>

    * <span data-ttu-id="c0be8-224">Per `EventHubName` impostare il nome dell'hub eventi, ovvero il valore del percorso dell'entità.</span><span class="sxs-lookup"><span data-stu-id="c0be8-224">Set `EventHubName` to the event hub name (that is, to the value of the entity path).</span></span>
    * <span data-ttu-id="c0be8-225">Per `EventHubNameConnectionString` impostare la stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="c0be8-225">Set `EventHubNameConnectionString` to the connection string.</span></span> <span data-ttu-id="c0be8-226">Verificare di usare la stringa di connessione da cui è stata rimossa la coppia chiave-valore `EntityPath`.</span><span class="sxs-lookup"><span data-stu-id="c0be8-226">Make sure that you use the connection string that you removed the `EntityPath` key-value pair from.</span></span>

    <span data-ttu-id="c0be8-227">La sezione `<appSettings>` ha un aspetto simile all'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="c0be8-227">The `<appSettings>` section looks like the following example.</span></span> <span data-ttu-id="c0be8-228">Per motivi di chiarezza e sicurezza, è stato applicato il ritorno a capo automatico ad alcune righe e sono stati rimossi alcuni caratteri.</span><span class="sxs-lookup"><span data-stu-id="c0be8-228">(For clarity and security, we wrapped some lines and removed some characters.)</span></span>

    ![File di configurazione dell'applicazione TwitterWpfClient in un editor di testo che mostra i segreti e le chiavi di Twitter e le informazioni della stringa di connessione all'hub eventi](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-tiwtter-app-config.png)
 
4. <span data-ttu-id="c0be8-230">Se non si è già avviata l'applicazione, eseguire ora TwitterWpfClient.exe.</span><span class="sxs-lookup"><span data-stu-id="c0be8-230">If you didn't already start the application, run TwitterWpfClient.exe now.</span></span> 

5. <span data-ttu-id="c0be8-231">Fare clic sul pulsante di avvio verde per raccogliere i dati del sentiment sul social media.</span><span class="sxs-lookup"><span data-stu-id="c0be8-231">Click the green start button to collect social sentiment.</span></span> <span data-ttu-id="c0be8-232">Gli eventi tweet con i valori **CreatedAt**, **Topic** e **SentimentScore** vengono inviati all'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="c0be8-232">You see Tweet events with the **CreatedAt**, **Topic**, and **SentimentScore** values being sent to your event hub.</span></span>

    ![Applicazione TwitterWpfClient in esecuzione, con l'elenco di tweet visualizzato](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-app-listing.png)

    >[!NOTE]
    ><span data-ttu-id="c0be8-234">Se vengono restituiti errori e nella parte inferiore della finestra non viene visualizzato un flusso di tweet, controllare le chiavi e i segreti.</span><span class="sxs-lookup"><span data-stu-id="c0be8-234">If you see errors, and you don't see a stream of tweets displayed in the lower part of the window, double-check the keys and secrets.</span></span> <span data-ttu-id="c0be8-235">Verificare inoltre che la stringa di connessione non includa la chiave `EntityPath` e il relativo valore.</span><span class="sxs-lookup"><span data-stu-id="c0be8-235">Also check the connection string (make sure that it does not include the `EntityPath` key and value.)</span></span>


## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="c0be8-236">Creare un processo di Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="c0be8-236">Create a Stream Analytics job</span></span>

<span data-ttu-id="c0be8-237">Ora che gli eventi tweet vengono trasmessi in flusso in tempo reale da Twitter, è possibile impostare un processo di Analisi di flusso per analizzare questi eventi in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="c0be8-237">Now that tweet events are streaming in real time from Twitter, you can set up a Stream Analytics job to analyze these events in real time.</span></span>

1. <span data-ttu-id="c0be8-238">Nel portale di Azure fare clic su **Nuovo** > **Internet delle cose** > **Processo di Analisi di flusso**.</span><span class="sxs-lookup"><span data-stu-id="c0be8-238">In the Azure portal, click **New** > **Internet of Things** > **Stream Analytics job**.</span></span>

2. <span data-ttu-id="c0be8-239">Assegnare il nome `socialtwitter-sa-job` al processo, specificare una sottoscrizione, un gruppo di risorse e un percorso.</span><span class="sxs-lookup"><span data-stu-id="c0be8-239">Name the job `socialtwitter-sa-job` and specify a subscription, resource group, and location.</span></span>

    <span data-ttu-id="c0be8-240">È consigliabile posizionare il processo e l'hub eventi nella stessa area per ottenere prestazioni ottimali ed evitare di pagare il trasferimento dei dati tra aree.</span><span class="sxs-lookup"><span data-stu-id="c0be8-240">It's a good idea to place the job and the event hub in the same region for best performance and so that you don't pay to transfer data between regions.</span></span>

    ![Creazione di un nuovo processo di Analisi di flusso](./media/stream-analytics-twitter-sentiment-analysis-trends/newjob.png)

3. <span data-ttu-id="c0be8-242">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c0be8-242">Click **Create**.</span></span>

    <span data-ttu-id="c0be8-243">Verrà creato il processo e il portale visualizzerà i relativi dettagli.</span><span class="sxs-lookup"><span data-stu-id="c0be8-243">The job is created and the portal displays job details.</span></span>


## <a name="specify-the-job-input"></a><span data-ttu-id="c0be8-244">Specificare l'input del processo</span><span class="sxs-lookup"><span data-stu-id="c0be8-244">Specify the job input</span></span>

1. <span data-ttu-id="c0be8-245">Nel processo di Analisi di flusso, in **Topologia processo** nella parte centrale del pannello, fare clic su **Input**.</span><span class="sxs-lookup"><span data-stu-id="c0be8-245">In your Stream Analytics job, under **Job Topology** in the middle of the job blade, click **Inputs**.</span></span> 

2. <span data-ttu-id="c0be8-246">Nel pannello **Input** fare clic su **+&nbsp;Aggiungi** e quindi compilare il pannello con questi valori:</span><span class="sxs-lookup"><span data-stu-id="c0be8-246">In the **Inputs** blade, click **+&nbsp;Add** and then fill out the blade with these values:</span></span>

    * <span data-ttu-id="c0be8-247">**Alias di input**: usare il nome `TwitterStream`.</span><span class="sxs-lookup"><span data-stu-id="c0be8-247">**Input alias**: Use the name `TwitterStream`.</span></span> <span data-ttu-id="c0be8-248">Se si usa un nome diverso, tenerne traccia, poiché sarà necessario in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="c0be8-248">If you use a different name, make a note of it because you need it later.</span></span>
    * <span data-ttu-id="c0be8-249">**Tipo di origine**: selezionare **Flusso dati**.</span><span class="sxs-lookup"><span data-stu-id="c0be8-249">**Source type**: Select **Data stream**.</span></span>
    * <span data-ttu-id="c0be8-250">**Origine**: selezionare **Hub eventi**.</span><span class="sxs-lookup"><span data-stu-id="c0be8-250">**Source**: Select **Event hub**.</span></span>
    * <span data-ttu-id="c0be8-251">**Opzioni di importazione**: selezionare **Usa l'hub eventi della sottoscrizione corrente**.</span><span class="sxs-lookup"><span data-stu-id="c0be8-251">**Import option**: Select **Use event hub from current subscription**.</span></span> 
    * <span data-ttu-id="c0be8-252">**Spazio dei nomi del bus di servizio**: selezionare lo spazio dei nomi dell'hub eventi creato in precedenza (`<yourname>-socialtwitter-eh-ns`).</span><span class="sxs-lookup"><span data-stu-id="c0be8-252">**Service bus namespace**: Select the event hub namespace that you created earlier (`<yourname>-socialtwitter-eh-ns`).</span></span>
    * <span data-ttu-id="c0be8-253">**Hub eventi**: selezionare l'hub eventi creato in precedenza (`socialtwitter-eh`).</span><span class="sxs-lookup"><span data-stu-id="c0be8-253">**Event hub**: Select the event hub that you created earlier (`socialtwitter-eh`).</span></span>
    * <span data-ttu-id="c0be8-254">**Nome criteri hub eventi**: selezionare i criteri di accesso creati in precedenza (`socialtwitter-access`).</span><span class="sxs-lookup"><span data-stu-id="c0be8-254">**Event hub policy name**: Select the access policy that you created earlier (`socialtwitter-access`).</span></span>

    ![Creare un nuovo input per il processo di Analisi di flusso](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-new-input.png)

3. <span data-ttu-id="c0be8-256">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c0be8-256">Click **Create**.</span></span>


## <a name="specify-the-job-query"></a><span data-ttu-id="c0be8-257">Specificare la query del processo</span><span class="sxs-lookup"><span data-stu-id="c0be8-257">Specify the job query</span></span>

<span data-ttu-id="c0be8-258">Analisi di flusso supporta un semplice modello di query dichiarativa per descrivere le trasformazioni.</span><span class="sxs-lookup"><span data-stu-id="c0be8-258">Stream Analytics supports a simple, declarative query model that describes transformations.</span></span> <span data-ttu-id="c0be8-259">Per altre informazioni sul linguaggio, vedere le [Informazioni di riferimento sul linguaggio di query di analisi dei flussi di Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span><span class="sxs-lookup"><span data-stu-id="c0be8-259">To learn more about the language, see the [Azure Stream Analytics Query Language Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span></span>  <span data-ttu-id="c0be8-260">Questa esercitazione permette di creare e testare diverse query su dati di Twitter.</span><span class="sxs-lookup"><span data-stu-id="c0be8-260">This tutorial helps you author and test several queries over Twitter data.</span></span>

<span data-ttu-id="c0be8-261">Per confrontare il numero di menzioni tra gli argomenti, è possibile usare una [finestra a cascata](https://msdn.microsoft.com/library/azure/dn835055.aspx) per ottenere il conteggio delle menzioni per argomento ogni cinque secondi.</span><span class="sxs-lookup"><span data-stu-id="c0be8-261">To compare the number of mentions among topics, you can use a [Tumbling window](https://msdn.microsoft.com/library/azure/dn835055.aspx) to get the count of mentions by topic every five seconds.</span></span>

1. <span data-ttu-id="c0be8-262">Chiudere il pannello **Input** se non si è già fatto.</span><span class="sxs-lookup"><span data-stu-id="c0be8-262">Close the **Inputs** blade if you haven't already.</span></span>

2. <span data-ttu-id="c0be8-263">Nel pannello del processo fare clic sulla casella **Query**.</span><span class="sxs-lookup"><span data-stu-id="c0be8-263">In the job blade, click the **Query** box.</span></span> <span data-ttu-id="c0be8-264">Azure elenca gli input e gli output configurati per il processo e consente di creare una query per trasformare il flusso di input nel momento in cui viene inviato all'output.</span><span class="sxs-lookup"><span data-stu-id="c0be8-264">Azure lists the inputs and outputs that are configured for the job, and lets you create a query that lets you transform the input stream as it is sent to the output.</span></span>

3. <span data-ttu-id="c0be8-265">Verificare che l'applicazione TwitterWpfClient sia in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="c0be8-265">Make sure that the TwitterWpfClient application is running.</span></span> 

3. <span data-ttu-id="c0be8-266">Nel pannello **Query** fare clic sui puntini di sospensione accanto all'input `TwitterStream` e quindi selezionare **Campiona dati da input**.</span><span class="sxs-lookup"><span data-stu-id="c0be8-266">In the **Query** blade, click the dots next to the `TwitterStream` input and then select **Sample data from input**.</span></span>

    ![Voci di menu per usare dati di esempio per la voce del processo di Analisi di flusso, con l'opzione "Campiona dati da input" selezionata](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-sample-data-from-input.png)

    <span data-ttu-id="c0be8-268">Verrà aperto un pannello che consente di specificare la quantità di dati di esempio da ottenere, definita in termini di durata della lettura del flusso di input.</span><span class="sxs-lookup"><span data-stu-id="c0be8-268">This opens a blade that lets you specify how much sample data to get, defined in terms of how long to read the input stream.</span></span>

4. <span data-ttu-id="c0be8-269">Impostare **Minuti** su 3 e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="c0be8-269">Set **Minutes** to 3 and then click **OK**.</span></span> 
    
    ![Opzioni per il campionamento del flusso di input, con l'opzione "3 minuti" selezionata.](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-input-create-sample-data.png)

    <span data-ttu-id="c0be8-271">Azure campiona i dati dal flusso di input per una durata di tre minuti e invia una notifica quando i dati di esempio sono pronti.</span><span class="sxs-lookup"><span data-stu-id="c0be8-271">Azure samples 3 minutes' worth of data from the input stream and notifies you when the sample data is ready.</span></span> <span data-ttu-id="c0be8-272">Questa operazione richiede un breve tempo.</span><span class="sxs-lookup"><span data-stu-id="c0be8-272">(This takes a short while.)</span></span> 

    <span data-ttu-id="c0be8-273">I dati di esempio vengono archiviati temporaneamente e sono disponibili finché rimane aperta la finestra di query.</span><span class="sxs-lookup"><span data-stu-id="c0be8-273">The sample data is stored temporarily and is available while you have the query window open.</span></span> <span data-ttu-id="c0be8-274">Se si chiude la finestra di query, i dati di esempio verranno rimossi e sarà necessario creare un nuovo set di dati.</span><span class="sxs-lookup"><span data-stu-id="c0be8-274">If you close the query window, the sample data is discarded, and you have to create a new set of sample data.</span></span> 

5. <span data-ttu-id="c0be8-275">Modificare la query nell'editor di codice nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="c0be8-275">Change the query in the code editor to the following:</span></span>

    ```
    SELECT System.Timestamp as Time, Topic, COUNT(*)
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY TUMBLINGWINDOW(s, 5), Topic
    ```

    <span data-ttu-id="c0be8-276">Se non si è usato `TwitterStream` come alias per l'input, sostituire l'alias per `TwitterStream` nella query.</span><span class="sxs-lookup"><span data-stu-id="c0be8-276">If didn't use `TwitterStream` as the alias for the input, substitute your alias for `TwitterStream` in the query.</span></span>  

    <span data-ttu-id="c0be8-277">In questa query viene usata la parola chiave **TIMESTAMP BY** per specificare un campo di timestamp nel payload da usare nel calcolo temporale.</span><span class="sxs-lookup"><span data-stu-id="c0be8-277">This query uses the **TIMESTAMP BY** keyword to specify a timestamp field in the payload to be used in the temporal computation.</span></span> <span data-ttu-id="c0be8-278">Se il campo non è stato specificato, l'operazione di windowing viene eseguita usando l'ora in cui ogni evento è arrivato all'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="c0be8-278">If this field isn't specified, the windowing operation is performed by using the time that each event arrived at the event hub.</span></span> <span data-ttu-id="c0be8-279">Altre informazioni sono disponibili nella sezione relativa a tempo di arrivo e tempo di applicazione nelle [informazioni di riferimento sulle query di Analisi di flusso](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span><span class="sxs-lookup"><span data-stu-id="c0be8-279">Learn more in the "Arrival Time vs Application Time" section of [Stream Analytics Query Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span></span>

    <span data-ttu-id="c0be8-280">Questa query accede anche a un timestamp per la fine di ogni finestra usando la proprietà **System.Timestamp**.</span><span class="sxs-lookup"><span data-stu-id="c0be8-280">This query also accesses a timestamp for the end of each window by using the **System.Timestamp** property.</span></span>

5. <span data-ttu-id="c0be8-281">Fare clic su **Test**.</span><span class="sxs-lookup"><span data-stu-id="c0be8-281">Click **Test**.</span></span> <span data-ttu-id="c0be8-282">La query viene eseguita sui dati che sono stati campionati.</span><span class="sxs-lookup"><span data-stu-id="c0be8-282">The query runs against the data that you sampled.</span></span>
    
6. <span data-ttu-id="c0be8-283">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="c0be8-283">Click **Save**.</span></span> <span data-ttu-id="c0be8-284">In questo modo la query viene salvata nell'ambito del processo di Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="c0be8-284">This saves the query as part of the Streaming Analytics job.</span></span> <span data-ttu-id="c0be8-285">I dati di esempio non vengono salvati.</span><span class="sxs-lookup"><span data-stu-id="c0be8-285">(It doesn't save the sample data.)</span></span>


## <a name="experiment-using-different-fields-from-the-stream"></a><span data-ttu-id="c0be8-286">Provare a usare diversi campi dal flusso</span><span class="sxs-lookup"><span data-stu-id="c0be8-286">Experiment using different fields from the stream</span></span> 

<span data-ttu-id="c0be8-287">La tabella seguente elenca i campi che fanno parte dei dati di flusso JSON.</span><span class="sxs-lookup"><span data-stu-id="c0be8-287">The following table lists the fields that are part of the JSON streaming data.</span></span> <span data-ttu-id="c0be8-288">È possibile sperimentare nell'editor di query.</span><span class="sxs-lookup"><span data-stu-id="c0be8-288">Feel free to experiment in the query editor.</span></span>

|<span data-ttu-id="c0be8-289">Proprietà JSON</span><span class="sxs-lookup"><span data-stu-id="c0be8-289">JSON property</span></span> | <span data-ttu-id="c0be8-290">Definizione</span><span class="sxs-lookup"><span data-stu-id="c0be8-290">Definition</span></span>|
|--- | ---|
|<span data-ttu-id="c0be8-291">CreatedAt</span><span class="sxs-lookup"><span data-stu-id="c0be8-291">CreatedAt</span></span> | <span data-ttu-id="c0be8-292">Orario di creazione del tweet</span><span class="sxs-lookup"><span data-stu-id="c0be8-292">The time that the tweet was created</span></span>|
|<span data-ttu-id="c0be8-293">Argomento</span><span class="sxs-lookup"><span data-stu-id="c0be8-293">Topic</span></span> | <span data-ttu-id="c0be8-294">Argomento che corrisponde alla parola chiave specificata</span><span class="sxs-lookup"><span data-stu-id="c0be8-294">The topic that matches the specified keyword</span></span>|
|<span data-ttu-id="c0be8-295">SentimentScore</span><span class="sxs-lookup"><span data-stu-id="c0be8-295">SentimentScore</span></span> | <span data-ttu-id="c0be8-296">Punteggio del sentiment da Sentiment140</span><span class="sxs-lookup"><span data-stu-id="c0be8-296">The sentiment score from Sentiment140</span></span>|
|<span data-ttu-id="c0be8-297">Autore</span><span class="sxs-lookup"><span data-stu-id="c0be8-297">Author</span></span> | <span data-ttu-id="c0be8-298">Handle di Twitter che ha inviato il tweet</span><span class="sxs-lookup"><span data-stu-id="c0be8-298">The Twitter handle that sent the tweet</span></span>|
|<span data-ttu-id="c0be8-299">Text</span><span class="sxs-lookup"><span data-stu-id="c0be8-299">Text</span></span> | <span data-ttu-id="c0be8-300">Corpo completo del tweet</span><span class="sxs-lookup"><span data-stu-id="c0be8-300">The full body of the tweet</span></span>|


## <a name="create-an-output-sink"></a><span data-ttu-id="c0be8-301">Creare un sink di output</span><span class="sxs-lookup"><span data-stu-id="c0be8-301">Create an output sink</span></span>

<span data-ttu-id="c0be8-302">A questo punto sono stati definiti un flusso di eventi, un input dell'hub eventi per inserire gli eventi e una query per eseguire una trasformazione nel flusso.</span><span class="sxs-lookup"><span data-stu-id="c0be8-302">You have now defined an event stream, an event hub input to ingest events, and a query to perform a transformation over the stream.</span></span> <span data-ttu-id="c0be8-303">L'ultimo passaggio consiste nel definire un sink di output per il processo.</span><span class="sxs-lookup"><span data-stu-id="c0be8-303">The last step is to define an output sink for the job.</span></span>  

<span data-ttu-id="c0be8-304">In questa esercitazione gli eventi tweet aggregati ottenuti dalla query del processo vengono scritti nell'archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="c0be8-304">In this tutorial, you write the aggregated tweet events from the job query to Azure Blob storage.</span></span>  <span data-ttu-id="c0be8-305">È anche possibile eseguire il push dei risultati al database SQL di Azure, ad Archiviazione tabelle di Azure, a Hub eventi o a Power BI, in base alle esigenze specifiche dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c0be8-305">You can also push your results to Azure SQL Database, Azure Table storage, Event Hubs, or Power BI, depending on your application needs.</span></span>

## <a name="specify-the-job-output"></a><span data-ttu-id="c0be8-306">Specificare l'output del processo</span><span class="sxs-lookup"><span data-stu-id="c0be8-306">Specify the job output</span></span>

1. <span data-ttu-id="c0be8-307">Nella sezione **Topologia processo** fare clic sulla casella **Output**.</span><span class="sxs-lookup"><span data-stu-id="c0be8-307">In the **Job Topology** section, click the **Output** box.</span></span> 

2. <span data-ttu-id="c0be8-308">Nel pannello **Output** fare clic su **+&nbsp;Aggiungi** e quindi compilare il pannello con questi valori:</span><span class="sxs-lookup"><span data-stu-id="c0be8-308">In the **Outputs** blade, click **+&nbsp;Add** and then fill out the blade with these values:</span></span>

    * <span data-ttu-id="c0be8-309">**Alias di output**: usare il nome `TwitterStream-Output`.</span><span class="sxs-lookup"><span data-stu-id="c0be8-309">**Output alias**: Use the name `TwitterStream-Output`.</span></span> 
    * <span data-ttu-id="c0be8-310">**Sink**: selezionare **Archivio BLOB**.</span><span class="sxs-lookup"><span data-stu-id="c0be8-310">**Sink**: Select **Blob storage**.</span></span>
    * <span data-ttu-id="c0be8-311">**Opzioni di importazione**: selezionare **Usa l'archiviazione BLOB della sottoscrizione corrente**.</span><span class="sxs-lookup"><span data-stu-id="c0be8-311">**Import options**: Select **Use blob storage from current subscription**.</span></span>
    * <span data-ttu-id="c0be8-312">**Account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="c0be8-312">**Storage account**.</span></span> <span data-ttu-id="c0be8-313">Selezionare **Crea un nuovo account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="c0be8-313">Select **Create a new storage account.**</span></span>
    * <span data-ttu-id="c0be8-314">**Account di archiviazione** (seconda casella).</span><span class="sxs-lookup"><span data-stu-id="c0be8-314">**Storage account** (second box).</span></span> <span data-ttu-id="c0be8-315">Immettere `YOURNAMEsa`, dove `YOURNAME` rappresenta il nome o un'altra stringa univoca.</span><span class="sxs-lookup"><span data-stu-id="c0be8-315">Enter `YOURNAMEsa`, where `YOURNAME` is your name or another unique string.</span></span> <span data-ttu-id="c0be8-316">Il nome può contenere solo lettere minuscole e numeri e deve essere univoco in Azure.</span><span class="sxs-lookup"><span data-stu-id="c0be8-316">The name can use only lowercase letters and numbers, and it must be unique across Azure.</span></span> 
    * <span data-ttu-id="c0be8-317">**Contenitore**.</span><span class="sxs-lookup"><span data-stu-id="c0be8-317">**Container**.</span></span> <span data-ttu-id="c0be8-318">Immettere `socialtwitter`.</span><span class="sxs-lookup"><span data-stu-id="c0be8-318">Enter `socialtwitter`.</span></span>
    <span data-ttu-id="c0be8-319">Il nome dell'account di archiviazione e il nome del contenitore vengono usati insieme per fornire un URI per l'archiviazione BLOB, in modo simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="c0be8-319">The storage account name and container name are used together to provide a URI for the blob storage, like this:</span></span> 

    `http://YOURNAMEsa.blob.core.windows.net/socialtwitter/...`
    
    ![Pannello "Nuovo output" per il processo di Analisi di flusso](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-output-blob-storage.png)
    
4. <span data-ttu-id="c0be8-321">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c0be8-321">Click **Create**.</span></span> 

    <span data-ttu-id="c0be8-322">Azure crea l'account di archiviazione e genera automaticamente una chiave.</span><span class="sxs-lookup"><span data-stu-id="c0be8-322">Azure creates the storage account and generates a key automatically.</span></span> 

5. <span data-ttu-id="c0be8-323">Chiudere il pannello **Output**.</span><span class="sxs-lookup"><span data-stu-id="c0be8-323">Close the **Outputs** blade.</span></span> 


## <a name="start-the-job"></a><span data-ttu-id="c0be8-324">Avviare il processo</span><span class="sxs-lookup"><span data-stu-id="c0be8-324">Start the job</span></span>

<span data-ttu-id="c0be8-325">Sono stati specificati l'input del processo, la query e l'output.</span><span class="sxs-lookup"><span data-stu-id="c0be8-325">A job input, query, and output are specified.</span></span> <span data-ttu-id="c0be8-326">A questo punto si è pronti ad avviare il processo di Analisi di flusso.</span><span class="sxs-lookup"><span data-stu-id="c0be8-326">You are ready to start the Stream Analytics job.</span></span>

1. <span data-ttu-id="c0be8-327">Verificare che l'applicazione TwitterWpfClient sia in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="c0be8-327">Make sure that the TwitterWpfClient application is running.</span></span> 

2. <span data-ttu-id="c0be8-328">Nel pannello del processo fare clic su **Avvia**.</span><span class="sxs-lookup"><span data-stu-id="c0be8-328">In the job blade, click **Start**.</span></span>

    ![Avviare il processo di Analisi di flusso](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-output.png)

3. <span data-ttu-id="c0be8-330">Nel pannello **Avvia processo**, per **Ora di inizio dell'output del processo**, selezionare **Ora** e quindi fare clic su **Avvia**.</span><span class="sxs-lookup"><span data-stu-id="c0be8-330">In the **Start job** blade, for **Job output start time**, select **Now** and then click **Start**.</span></span> 

    ![Pannello "Avvia processo" per il processo di Analisi di flusso](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-job-blade.png)

    <span data-ttu-id="c0be8-332">Azure informa l'utente quando il processo viene avviato e, nel pannello del processo, lo stato viene visualizzato come **In esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="c0be8-332">Azure notifies you when the job has started, and in the job blade, the status is displayed as **Running**.</span></span>

    ![Processo in esecuzione](./media/stream-analytics-twitter-sentiment-analysis-trends/jobrunning.png)

## <a name="view-output-for-sentiment-analysis"></a><span data-ttu-id="c0be8-334">Visualizzare l'output per l'analisi del sentiment</span><span class="sxs-lookup"><span data-stu-id="c0be8-334">View output for sentiment analysis</span></span>

<span data-ttu-id="c0be8-335">Quando il processo è in esecuzione ed elabora il flusso di Twitter in tempo reale, è possibile visualizzare l'output per l'analisi del sentiment.</span><span class="sxs-lookup"><span data-stu-id="c0be8-335">After your job has started running and is processing the real-time Twitter stream, you can view the output for sentiment analysis.</span></span>

<span data-ttu-id="c0be8-336">Per visualizzare l'output del processo in tempo reale, usare uno strumento come [Azure Storage Explorer](https://http://storageexplorer.com/) o [Azure Explorer](http://www.cerebrata.com/products/azure-explorer/introduction).</span><span class="sxs-lookup"><span data-stu-id="c0be8-336">You can use a tool like [Azure Storage Explorer](https://http://storageexplorer.com/) or [Azure Explorer](http://www.cerebrata.com/products/azure-explorer/introduction) to view your job output in real time.</span></span> <span data-ttu-id="c0be8-337">A questo punto è possibile usare [Power BI](https://powerbi.com/) per estendere l'applicazione in modo da includere un dashboard personalizzato come quello riportato nello screenshot seguente:</span><span class="sxs-lookup"><span data-stu-id="c0be8-337">From here, you can use [Power BI](https://powerbi.com/) to extend your application to include a customized dashboard like the one shown in the following screenshot:</span></span>

![Power BI](./media/stream-analytics-twitter-sentiment-analysis-trends/power-bi.png)


## <a name="create-another-query-to-identify-trending-topics"></a><span data-ttu-id="c0be8-339">Creare un'altra query per identificare gli argomenti di tendenza</span><span class="sxs-lookup"><span data-stu-id="c0be8-339">Create another query to identify trending topics</span></span>

<span data-ttu-id="c0be8-340">Un'altra query che è possibile usare per comprendere il sentiment su Twitter si basa su un [finestra temporale scorrevole](https://msdn.microsoft.com/library/azure/dn835051.aspx).</span><span class="sxs-lookup"><span data-stu-id="c0be8-340">Another query you can use to understand Twitter sentiment is based on a [Sliding Window](https://msdn.microsoft.com/library/azure/dn835051.aspx).</span></span> <span data-ttu-id="c0be8-341">Per identificare gli argomenti di tendenza si cercano gli argomenti in cui le menzioni superano un valore soglia entro un determinato periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="c0be8-341">To identify trending topics, you look for topics that cross a threshold value for mentions in a specified amount of time.</span></span>

<span data-ttu-id="c0be8-342">Ai fini di questa esercitazione, si cercano gli argomenti menzionati più di 20 volte negli ultimi cinque secondi.</span><span class="sxs-lookup"><span data-stu-id="c0be8-342">For the purposes of this tutorial, you check for topics that are mentioned more than 20 times in the last 5 seconds.</span></span>

1. <span data-ttu-id="c0be8-343">Nel pannello del processo fare clic su **Arresta** per arrestare il processo.</span><span class="sxs-lookup"><span data-stu-id="c0be8-343">In the job blade, click **Stop** to stop the job.</span></span> 

2. <span data-ttu-id="c0be8-344">Nella sezione **Topologia processo** fare clic sulla casella **Query**.</span><span class="sxs-lookup"><span data-stu-id="c0be8-344">In the **Job Topology** section, click the **Query** box.</span></span> 

3. <span data-ttu-id="c0be8-345">Modificare la query nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="c0be8-345">Change the query to the following:</span></span>

    ```    
    SELECT System.Timestamp as Time, Topic, COUNT(*) as Mentions
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY SLIDINGWINDOW(s, 5), topic
    HAVING COUNT(*) > 20
    ```

4. <span data-ttu-id="c0be8-346">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="c0be8-346">Click **Save**.</span></span>

5. <span data-ttu-id="c0be8-347">Verificare che l'applicazione TwitterWpfClient sia in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="c0be8-347">Make sure that the TwitterWpfClient application is running.</span></span> 

6. <span data-ttu-id="c0be8-348">Fare clic su **Avvia** per riavviare il processo usando la nuova query.</span><span class="sxs-lookup"><span data-stu-id="c0be8-348">Click **Start** to restart the job using the new query.</span></span>


## <a name="get-support"></a><span data-ttu-id="c0be8-349">Supporto</span><span class="sxs-lookup"><span data-stu-id="c0be8-349">Get support</span></span>
<span data-ttu-id="c0be8-350">Per ulteriore assistenza, provare il [Forum di Analisi dei flussi di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="c0be8-350">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c0be8-351">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c0be8-351">Next steps</span></span>
* [<span data-ttu-id="c0be8-352">Introduzione ad Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="c0be8-352">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="c0be8-353">Introduzione all'uso di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="c0be8-353">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="c0be8-354">Ridimensionare i processi di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="c0be8-354">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="c0be8-355">Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure</span><span class="sxs-lookup"><span data-stu-id="c0be8-355">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="c0be8-356">Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure</span><span class="sxs-lookup"><span data-stu-id="c0be8-356">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
